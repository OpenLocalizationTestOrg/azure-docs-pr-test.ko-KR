---
title: "Microsoft Azure 저장소 데이터 이동을 라이브러리 hello로 데이터 aaaTransfer | Microsoft Docs"
description: "Blob 및 파일 콘텐츠에서 hello 데이터 이동을 라이브러리 toomove 또는 복사 데이터 tooor를 사용 합니다. 로컬 파일의 데이터 tooAzure 저장소를 복사 하 하거나 내에서 또는 저장소 계정 간에 데이터를 복사 합니다. 사용자 데이터 tooAzure 저장소를 쉽게 마이그레이션하십시오."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Microsoft Azure 저장소 데이터 이동을 라이브러리 hello로 데이터 전송

## <a name="overview"></a>개요
Microsoft Azure 저장소 데이터 이동을 라이브러리 hello는 고성능 업로드, 다운로드 및 Azure 저장소 Blob 및 파일의 복사를 위해 설계 된 오픈 소스 플랫폼 간 라이브러리입니다. 이 라이브러리는 hello 핵심 데이터 이동을 프레임 워크를 구동 하는 [AzCopy](storage-use-azcopy.md)합니다. 기존의 우리의에서 사용할 수 없는 편리한 메서드를 제공 하는 hello 데이터 이동을 라이브러리 [.NET Azure 저장소 클라이언트 라이브러리](storage-dotnet-how-to-use-blobs.md)합니다. 취소 된 전송 및 등을 쉽게 다시 시작할 병렬 작업, 진행률 추적 전송의 hello 기능 tooset hello 수를 포함 하는이 됩니다.  

이 라이브러리는 .NET Core를 사용하기 때문에 Windows, Linux 및 macOS용 .NET 앱을 빌드할 때 사용할 수 있습니다. .NET Core에 대 한 자세한 toolearn 참조 toohello [.NET Core 설명서](https://dotnet.github.io/)합니다. 또한 이 라이브러리는 전통적인 Windows용 .NET Framework 앱에서도 작동합니다. 

이 문서에서는 toocreate.NET Core 콘솔 응용 프로그램 Windows, Linux 및 macOS에서 실행 하 고 hello 다음 시나리오를 수행 하는 방법을 보여 줍니다.

- 파일 및 디렉터리 tooBlob 저장소를 업로드 합니다.
- 데이터를 전송 하는 경우 병렬 작업의 hello 수를 정의 합니다.
- 데이터 전송 진행률을 추적합니다.
- 취소된 데이터 전송을 다시 시작합니다. 
- URL tooBlob 저장소에서에서 파일을 복사 합니다. 
- Blob 저장소 tooBlob 저장소에서에서 복사 합니다.

**필요한 항목**

* [Contact.java](https://code.visualstudio.com/)
* [Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> 이 가이드는 [Azure 저장소](https://azure.microsoft.com/services/storage/)에 대해 잘 알고 있다는 것을 가정합니다. 그렇지 않은 hello를 읽는 경우 [소개 tooAzure 저장소](storage-introduction.md) 설명서 유용 합니다. 너무 필요한 가장 중요 한 점은[저장소 계정 만들기](storage-create-storage-account.md#create-a-storage-account) 데이터 이동을 라이브러리 hello toostart를 사용 하 여 합니다.
> 
> 

## <a name="setup"></a>설정  

1. Hello 방문 [.NET Core 설치 가이드](https://www.microsoft.com/net/core) tooinstall.NET Core 합니다. 사용자 환경을 선택할 때는 hello 명령줄 옵션을 선택 합니다. 
2. Hello 명령줄에서 프로젝트에 대 한 디렉터리를 만듭니다. 탐색을이 디렉터리에 입력 `dotnet new` toocreate C# 콘솔 프로젝트.
3. Visual Studio Code에서 이 디렉터리를 엽니다. 입력 하 여 hello 명령줄을 통해이 단계를 신속 하 게 수행할 수 있습니다 `code .`합니다.  
4. Hello 설치 [C# 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) hello Visual Studio Code 마켓플레이스에에서 합니다. Visual Studio Code를 다시 시작합니다. 
5. 이 시점에서 두 가지 프롬프트가 표시됩니다. 다른 하나는 "필요한 자산 toobuild 및 디버그 합니다."를 추가 합니다. "예"를 클릭합니다. 또 다른 프롬프트는 해결되지 않은 종속성을 복원하는 것입니다. "복원"을 클릭합니다.
6. 응용 프로그램이 포함 된 `launch.json` hello 아래 파일 `.vscode` 디렉터리입니다. 이 파일에서 변경 hello `externalConsole` 너무 값`true`합니다.
7. Visual Studio Code는 toodebug.NET Core 응용 프로그램이 있습니다. 적중 `F5` toorun 응용 프로그램 설치 프로그램은 작동 하는지 확인 합니다. 콘솔에 "Hello World!" 인쇄 된 toohello 콘솔입니다. 

## <a name="add-data-movement-library-tooyour-project"></a>데이터 이동 라이브러리 tooyour 프로젝트 추가

1. Hello 최신 버전의 hello 데이터 이동을 라이브러리 toohello 추가 `dependencies` 섹션 프로그램 `project.json` 파일입니다. 이 버전의 쓰기 hello 시 것`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. 추가 `"portable-net45+win8"` toohello `imports` 섹션. 
3. 프롬프트 toorestore 프로젝트가 표시 됩니다. Hello "복원" 단추를 클릭 합니다. Hello 명령을 입력 하 여 hello 명령줄에서 프로젝트를 복원할 수도 있습니다 `dotnet restore` hello 루트 프로젝트 디렉터리에 있습니다.

다음과 같이 `project.json`을 수정합니다.

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>응용 프로그램의 기본 구조 hello 설정
hello 먼저 설정 되어 응용 프로그램의 hello "기본" 코드 있습니다. 이 코드는 저장소 계정 이름 및 계정 키에 대 한 us를 묻는 메시지가 표시 되며 이러한 자격 증명 toocreate를 사용 하 여 한 `CloudStorageAccount` 개체입니다. 이 개체는 모든 전송 시나리오에서이 저장소 계정으로 사용 되는 toointeract 합니다. hello 코드 라는 메시지도 표시 우리 toochoose hello 유형의 전송 작업 같은 tooexecute 합니다. 

다음과 같이 `Program.cs`을 수정합니다.

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>로컬 파일 tooAzure Blob를 전송 합니다.
Hello 메서드 추가 `GetSourcePath` 및 `GetBlob` 너무`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Hello 수정 `TransferLocalFileToAzureBlob` 메서드:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

이 코드 hello 경로 tooa 로컬 파일, 기존 또는 새 컨테이너의 hello 이름 및 새 blob의 hello 이름에 대 한 라는 메시지가 나타납니다. hello `TransferManager.UploadAsync` 메서드는이 정보를 사용 하 여 hello 업로드를 수행 합니다. 

적중 `F5` toorun 응용 프로그램입니다. 해당 hello 업로드 hello로 저장소 계정을 확인 하 여 발생 한 것을 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.

## <a name="set-number-of-parallel-operations"></a>병렬 작업 수 설정
데이터 이동 라이브러리는 병렬 작업 tooincrease hello 데이터 전송 처리량 hello 기능 tooset hello 수 hello에서 훌륭한 기능 제공. 기본적으로 데이터 이동을 라이브러리 hello 설정 병렬 작업 too8 hello 수 * hello 컴퓨터에는 코어 수입니다. 

대역폭이 낮은 환경에서 많은 병렬 작업 hello 네트워크 연결에 과부하가 하 고 실제로 작업이 완전히 완료를 방지 수 염두에 둬야 합니다. 해야 tooexperiment이 설정은 toodetermine와 작동 조건을 기반으로 가장 사용 가능한 네트워크 대역폭에 합니다. 

병렬 작업의 tooset hello 수 있도록 하는 일부 코드를 추가 해 보겠습니다. 또한 시간이 소요 되는 시간 전송 toocomplete hello에 대 한 코드를 추가 해 보겠습니다.

추가 `SetNumberOfParallelOperations` 메서드 너무`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Hello 수정 `ExecuteChoice` 메서드 toouse `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Hello 수정 `TransferLocalFileToAzureBlob` 메서드 toouse 타이머:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>전송 진행률 추적
우리의 데이터 tootransfer에 걸린 시간을 알고 있으면 유용 합니다. 그러나 우리 전송의 수 toosee hello 진행 되 고 *중* hello 전송 작업을 더 좋은 것입니다. tooachieve이이 시나리오에서는 toocreate 필요는 `TransferContext` 개체입니다. hello `TransferContext` 개체는 두 가지 형태로 제공: `SingleTransferContext` 및 `DirectoryTransferContext`합니다. hello 이전 (이 코드에서는 현재이) 단일 파일을 전송 되며 (나중에 추가 하 고)는 파일의 디렉터리를 전송 하기 위한 hello 후자는.

Hello 메서드 추가 `GetSingleTransferContext` 및 `GetDirectoryTransferContext` 너무`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Hello 수정 `TransferLocalFileToAzureBlob` 메서드 toouse `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>취소된 전송 다시 시작
Hello 데이터 이동을 라이브러리에서 제공 하는 또 다른 편리한 기능 hello 기능 tooresume 취소 된 전송입니다. 입력 하 여 tootemporarily 취소 hello 전송 수 있는 일부 코드를 추가 해 보겠습니다 `c`, 고 hello 전송에 3 초 후 다시 합니다.

다음과 같이 `TransferLocalFileToAzureBlob`을 수정합니다.

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

지금까지 우리의 `checkpoint` 값이 너무 설정 항상`null`합니다. 이제 hello 전송, 취소 했습니다 hello 업체 전송의 마지막 검사점을 검색할 경우 우리의 전송에이 새 검사점을 사용 합니다. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>로컬 디렉터리 tooAzure Blob 디렉터리를 전송 합니다.
Hello 데이터 이동을 라이브러리 수 한 번에 하나의 파일을 전송만 실망 것입니다. 다행히 hello 그렇지는 않습니다. 데이터 이동 라이브러리 hello hello 기능 tootransfer 파일 및 모든 하위 디렉터리의 디렉터리를 제공합니다. 추가해보겠습니다 toodo 수 있는 몇 가지 코드 뿐입니다.

첫째, hello 메서드를 추가 합니다. `GetBlobDirectory` 너무`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

그런 후 다음과 같이 `TransferLocalDirectoryToAzureBlobDirectory`을 수정합니다.

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

이 메서드를 hello 메서드 단일 파일을 업로드 하기 위한 몇 가지 차이점이 있습니다. 지금 사용 하 여 `TransferManager.UploadDirectoryAsync` 및 hello `getDirectoryTransferContext` 앞에서 만든 메서드. 또한, 이제 제공는 `options` tooour 업로드 작업 우리의 업로드에서 tooinclude 하위 디렉터리 한다고 tooindicate 수 있는 값입니다. 

## <a name="copy-file-from-url-tooazure-blob"></a>URL tooAzure Blob에서에서 파일을 복사 합니다.
이제 toocopy URL tooan Azure Blob에서에서 파일을 수 있는 코드를 추가 해 보겠습니다. 

다음과 같이 `TransferUrlToAzureBlob`을 수정합니다.

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

이 기능에 대 한 하나의 중요 한 사용 사례 때 다른 클라우드 서비스 (예: AWS) tooAzure toomove 데이터가 필요 합니다. 제공 하는 URL을가지고 toohello 리소스 액세스, hello를 사용 하 여 Azure Blob에 해당 리소스를 쉽게 이동할 수 있습니다 `TransferManager.CopyAsync` 메서드. 또한 이 메서드는 새로운 부울 매개 변수를 사용합니다. 이 매개 변수를 너무 설정`true` toodo 비동기 서버 쪽 복사 한다고 나타냅니다. 이 매개 변수를 너무 설정`false` hello 리소스는 로컬 컴퓨터에 다운로드 한 tooour 먼저 의미 하는 동기 복사-tooAzure Blob를 업로드 한 다음을 나타냅니다. 그러나 동기 복사본은 현재만 한 Azure 저장소 리소스 tooanother에서 복사 하는 데 사용할 수 있습니다. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Azure Blob tooAzure Blob를 전송 합니다.
고유 하 게 hello 데이터 이동을 라이브러리에서 제공 하는 또 다른 기능은 한 Azure 저장소 리소스 tooanother에서 hello 기능 toocopy입니다. 

다음과 같이 `TransferAzureBlobToAzureBlob`을 수정합니다.

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

이 예제 hello 부울 매개 변수 설정 `TransferManager.CopyAsync` 너무`false` tooindicate toodo 동기 복사 한다고 합니다. 즉, hello 리소스는 다운로드 한 tooour 로컬 컴퓨터를 먼저 다음 tooAzure Blob을 업로드 합니다. hello 동기 복사 옵션은 복사 작업에는 일관 된 속도 위한 훌륭한 방법 tooensure 있습니다. 반면, 비동기 서버 쪽 복사본의 hello 속도 변동 수는 hello 서버에서 사용 가능한 네트워크 대역폭 hello에 종속 됩니다. 그러나 동기 복사 추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다. hello 권장 접근 방식을 toouse hello에 있는 Azure VM에서 동기 복사는 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.

## <a name="conclusion"></a>결론
이제 데이터 이동 응용 프로그램이 완료되었습니다. [hello 전체 코드 샘플은 GitHub에서 사용할 수 있는](https://github.com/azure-samples/storage-dotnet-data-movement-library-app)합니다. 

## <a name="next-steps"></a>다음 단계
이 시작 자습서에서 Azure Storage와 상호 작용하고 Windows, Linux 및 macOS에서 실행되는 응용 프로그램을 만들었습니다. 이 입문서에서는 Blob Storage에 초점을 맞추었지만, 그러나이 동일한 기술 자료에 적용 된 tooFile 저장소 수 있습니다. toolearn을 체크 아웃 [Azure 저장소 데이터 이동을 라이브러리 참조 문서](https://azure.github.io/azure-storage-net-data-movement)합니다.

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




