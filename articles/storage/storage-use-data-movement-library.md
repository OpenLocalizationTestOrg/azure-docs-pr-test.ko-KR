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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="5d1f1-105">Microsoft Azure 저장소 데이터 이동을 라이브러리 hello로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="5d1f1-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="5d1f1-106">개요</span><span class="sxs-lookup"><span data-stu-id="5d1f1-106">Overview</span></span>
<span data-ttu-id="5d1f1-107">Microsoft Azure 저장소 데이터 이동을 라이브러리 hello는 고성능 업로드, 다운로드 및 Azure 저장소 Blob 및 파일의 복사를 위해 설계 된 오픈 소스 플랫폼 간 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="5d1f1-108">이 라이브러리는 hello 핵심 데이터 이동을 프레임 워크를 구동 하는 [AzCopy](storage-use-azcopy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-108">This library is hello core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="5d1f1-109">기존의 우리의에서 사용할 수 없는 편리한 메서드를 제공 하는 hello 데이터 이동을 라이브러리 [.NET Azure 저장소 클라이언트 라이브러리](storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="5d1f1-110">취소 된 전송 및 등을 쉽게 다시 시작할 병렬 작업, 진행률 추적 전송의 hello 기능 tooset hello 수를 포함 하는이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="5d1f1-111">이 라이브러리는 .NET Core를 사용하기 때문에 Windows, Linux 및 macOS용 .NET 앱을 빌드할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="5d1f1-112">.NET Core에 대 한 자세한 toolearn 참조 toohello [.NET Core 설명서](https://dotnet.github.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="5d1f1-113">또한 이 라이브러리는 전통적인 Windows용 .NET Framework 앱에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="5d1f1-114">이 문서에서는 toocreate.NET Core 콘솔 응용 프로그램 Windows, Linux 및 macOS에서 실행 하 고 hello 다음 시나리오를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="5d1f1-115">파일 및 디렉터리 tooBlob 저장소를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="5d1f1-116">데이터를 전송 하는 경우 병렬 작업의 hello 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="5d1f1-117">데이터 전송 진행률을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-117">Track data transfer progress.</span></span>
- <span data-ttu-id="5d1f1-118">취소된 데이터 전송을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="5d1f1-119">URL tooBlob 저장소에서에서 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="5d1f1-120">Blob 저장소 tooBlob 저장소에서에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="5d1f1-121">**필요한 항목**</span><span class="sxs-lookup"><span data-stu-id="5d1f1-121">**What you need:**</span></span>

* [<span data-ttu-id="5d1f1-122">Contact.java</span><span class="sxs-lookup"><span data-stu-id="5d1f1-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="5d1f1-123">[Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="5d1f1-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="5d1f1-124">이 가이드는 [Azure 저장소](https://azure.microsoft.com/services/storage/)에 대해 잘 알고 있다는 것을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="5d1f1-125">그렇지 않은 hello를 읽는 경우 [소개 tooAzure 저장소](storage-introduction.md) 설명서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="5d1f1-126">너무 필요한 가장 중요 한 점은[저장소 계정 만들기](storage-create-storage-account.md#create-a-storage-account) 데이터 이동을 라이브러리 hello toostart를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="5d1f1-127">설정</span><span class="sxs-lookup"><span data-stu-id="5d1f1-127">Setup</span></span>  

1. <span data-ttu-id="5d1f1-128">Hello 방문 [.NET Core 설치 가이드](https://www.microsoft.com/net/core) tooinstall.NET Core 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="5d1f1-129">사용자 환경을 선택할 때는 hello 명령줄 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="5d1f1-130">Hello 명령줄에서 프로젝트에 대 한 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="5d1f1-131">탐색을이 디렉터리에 입력 `dotnet new` toocreate C# 콘솔 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="5d1f1-132">Visual Studio Code에서 이 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="5d1f1-133">입력 하 여 hello 명령줄을 통해이 단계를 신속 하 게 수행할 수 있습니다 `code .`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="5d1f1-134">Hello 설치 [C# 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) hello Visual Studio Code 마켓플레이스에에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="5d1f1-135">Visual Studio Code를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="5d1f1-136">이 시점에서 두 가지 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="5d1f1-137">다른 하나는 "필요한 자산 toobuild 및 디버그 합니다."를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="5d1f1-138">"예"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-138">Click "yes."</span></span> <span data-ttu-id="5d1f1-139">또 다른 프롬프트는 해결되지 않은 종속성을 복원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="5d1f1-140">"복원"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-140">Click "restore."</span></span>
6. <span data-ttu-id="5d1f1-141">응용 프로그램이 포함 된 `launch.json` hello 아래 파일 `.vscode` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="5d1f1-142">이 파일에서 변경 hello `externalConsole` 너무 값`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="5d1f1-143">Visual Studio Code는 toodebug.NET Core 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="5d1f1-144">적중 `F5` toorun 응용 프로그램 설치 프로그램은 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="5d1f1-145">콘솔에 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="5d1f1-145">You should see "Hello World!"</span></span> <span data-ttu-id="5d1f1-146">인쇄 된 toohello 콘솔입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="5d1f1-147">데이터 이동 라이브러리 tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="5d1f1-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="5d1f1-148">Hello 최신 버전의 hello 데이터 이동을 라이브러리 toohello 추가 `dependencies` 섹션 프로그램 `project.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="5d1f1-149">이 버전의 쓰기 hello 시 것`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="5d1f1-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="5d1f1-150">추가 `"portable-net45+win8"` toohello `imports` 섹션.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="5d1f1-151">프롬프트 toorestore 프로젝트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="5d1f1-152">Hello "복원" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-152">Click hello "restore" button.</span></span> <span data-ttu-id="5d1f1-153">Hello 명령을 입력 하 여 hello 명령줄에서 프로젝트를 복원할 수도 있습니다 `dotnet restore` hello 루트 프로젝트 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="5d1f1-154">다음과 같이 `project.json`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="5d1f1-155">응용 프로그램의 기본 구조 hello 설정</span><span class="sxs-lookup"><span data-stu-id="5d1f1-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="5d1f1-156">hello 먼저 설정 되어 응용 프로그램의 hello "기본" 코드 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="5d1f1-157">이 코드는 저장소 계정 이름 및 계정 키에 대 한 us를 묻는 메시지가 표시 되며 이러한 자격 증명 toocreate를 사용 하 여 한 `CloudStorageAccount` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="5d1f1-158">이 개체는 모든 전송 시나리오에서이 저장소 계정으로 사용 되는 toointeract 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="5d1f1-159">hello 코드 라는 메시지도 표시 우리 toochoose hello 유형의 전송 작업 같은 tooexecute 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="5d1f1-160">다음과 같이 `Program.cs`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="5d1f1-161">로컬 파일 tooAzure Blob를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="5d1f1-162">Hello 메서드 추가 `GetSourcePath` 및 `GetBlob` 너무`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="5d1f1-163">Hello 수정 `TransferLocalFileToAzureBlob` 메서드:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="5d1f1-164">이 코드 hello 경로 tooa 로컬 파일, 기존 또는 새 컨테이너의 hello 이름 및 새 blob의 hello 이름에 대 한 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="5d1f1-165">hello `TransferManager.UploadAsync` 메서드는이 정보를 사용 하 여 hello 업로드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="5d1f1-166">적중 `F5` toorun 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="5d1f1-167">해당 hello 업로드 hello로 저장소 계정을 확인 하 여 발생 한 것을 확인할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="5d1f1-168">병렬 작업 수 설정</span><span class="sxs-lookup"><span data-stu-id="5d1f1-168">Set number of parallel operations</span></span>
<span data-ttu-id="5d1f1-169">데이터 이동 라이브러리는 병렬 작업 tooincrease hello 데이터 전송 처리량 hello 기능 tooset hello 수 hello에서 훌륭한 기능 제공.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="5d1f1-170">기본적으로 데이터 이동을 라이브러리 hello 설정 병렬 작업 too8 hello 수 * hello 컴퓨터에는 코어 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="5d1f1-171">대역폭이 낮은 환경에서 많은 병렬 작업 hello 네트워크 연결에 과부하가 하 고 실제로 작업이 완전히 완료를 방지 수 염두에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="5d1f1-172">해야 tooexperiment이 설정은 toodetermine와 작동 조건을 기반으로 가장 사용 가능한 네트워크 대역폭에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="5d1f1-173">병렬 작업의 tooset hello 수 있도록 하는 일부 코드를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="5d1f1-174">또한 시간이 소요 되는 시간 전송 toocomplete hello에 대 한 코드를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="5d1f1-175">추가 `SetNumberOfParallelOperations` 메서드 너무`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="5d1f1-176">Hello 수정 `ExecuteChoice` 메서드 toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="5d1f1-177">Hello 수정 `TransferLocalFileToAzureBlob` 메서드 toouse 타이머:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="5d1f1-178">전송 진행률 추적</span><span class="sxs-lookup"><span data-stu-id="5d1f1-178">Track transfer progress</span></span>
<span data-ttu-id="5d1f1-179">우리의 데이터 tootransfer에 걸린 시간을 알고 있으면 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="5d1f1-180">그러나 우리 전송의 수 toosee hello 진행 되 고 *중* hello 전송 작업을 더 좋은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="5d1f1-181">tooachieve이이 시나리오에서는 toocreate 필요는 `TransferContext` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="5d1f1-182">hello `TransferContext` 개체는 두 가지 형태로 제공: `SingleTransferContext` 및 `DirectoryTransferContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="5d1f1-183">hello 이전 (이 코드에서는 현재이) 단일 파일을 전송 되며 (나중에 추가 하 고)는 파일의 디렉터리를 전송 하기 위한 hello 후자는.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="5d1f1-184">Hello 메서드 추가 `GetSingleTransferContext` 및 `GetDirectoryTransferContext` 너무`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="5d1f1-185">Hello 수정 `TransferLocalFileToAzureBlob` 메서드 toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="5d1f1-186">취소된 전송 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5d1f1-186">Resume a canceled transfer</span></span>
<span data-ttu-id="5d1f1-187">Hello 데이터 이동을 라이브러리에서 제공 하는 또 다른 편리한 기능 hello 기능 tooresume 취소 된 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="5d1f1-188">입력 하 여 tootemporarily 취소 hello 전송 수 있는 일부 코드를 추가 해 보겠습니다 `c`, 고 hello 전송에 3 초 후 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="5d1f1-189">다음과 같이 `TransferLocalFileToAzureBlob`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="5d1f1-190">지금까지 우리의 `checkpoint` 값이 너무 설정 항상`null`합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="5d1f1-191">이제 hello 전송, 취소 했습니다 hello 업체 전송의 마지막 검사점을 검색할 경우 우리의 전송에이 새 검사점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="5d1f1-192">로컬 디렉터리 tooAzure Blob 디렉터리를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="5d1f1-193">Hello 데이터 이동을 라이브러리 수 한 번에 하나의 파일을 전송만 실망 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="5d1f1-194">다행히 hello 그렇지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="5d1f1-195">데이터 이동 라이브러리 hello hello 기능 tootransfer 파일 및 모든 하위 디렉터리의 디렉터리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="5d1f1-196">추가해보겠습니다 toodo 수 있는 몇 가지 코드 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="5d1f1-197">첫째, hello 메서드를 추가 합니다. `GetBlobDirectory` 너무`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="5d1f1-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="5d1f1-198">그런 후 다음과 같이 `TransferLocalDirectoryToAzureBlobDirectory`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="5d1f1-199">이 메서드를 hello 메서드 단일 파일을 업로드 하기 위한 몇 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="5d1f1-200">지금 사용 하 여 `TransferManager.UploadDirectoryAsync` 및 hello `getDirectoryTransferContext` 앞에서 만든 메서드.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="5d1f1-201">또한, 이제 제공는 `options` tooour 업로드 작업 우리의 업로드에서 tooinclude 하위 디렉터리 한다고 tooindicate 수 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="5d1f1-202">URL tooAzure Blob에서에서 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="5d1f1-203">이제 toocopy URL tooan Azure Blob에서에서 파일을 수 있는 코드를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="5d1f1-204">다음과 같이 `TransferUrlToAzureBlob`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="5d1f1-205">이 기능에 대 한 하나의 중요 한 사용 사례 때 다른 클라우드 서비스 (예: AWS) tooAzure toomove 데이터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="5d1f1-206">제공 하는 URL을가지고 toohello 리소스 액세스, hello를 사용 하 여 Azure Blob에 해당 리소스를 쉽게 이동할 수 있습니다 `TransferManager.CopyAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="5d1f1-207">또한 이 메서드는 새로운 부울 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="5d1f1-208">이 매개 변수를 너무 설정`true` toodo 비동기 서버 쪽 복사 한다고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="5d1f1-209">이 매개 변수를 너무 설정`false` hello 리소스는 로컬 컴퓨터에 다운로드 한 tooour 먼저 의미 하는 동기 복사-tooAzure Blob를 업로드 한 다음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="5d1f1-210">그러나 동기 복사본은 현재만 한 Azure 저장소 리소스 tooanother에서 복사 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="5d1f1-211">Azure Blob tooAzure Blob를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="5d1f1-212">고유 하 게 hello 데이터 이동을 라이브러리에서 제공 하는 또 다른 기능은 한 Azure 저장소 리소스 tooanother에서 hello 기능 toocopy입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="5d1f1-213">다음과 같이 `TransferAzureBlobToAzureBlob`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="5d1f1-214">이 예제 hello 부울 매개 변수 설정 `TransferManager.CopyAsync` 너무`false` tooindicate toodo 동기 복사 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="5d1f1-215">즉, hello 리소스는 다운로드 한 tooour 로컬 컴퓨터를 먼저 다음 tooAzure Blob을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="5d1f1-216">hello 동기 복사 옵션은 복사 작업에는 일관 된 속도 위한 훌륭한 방법 tooensure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="5d1f1-217">반면, 비동기 서버 쪽 복사본의 hello 속도 변동 수는 hello 서버에서 사용 가능한 네트워크 대역폭 hello에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="5d1f1-218">그러나 동기 복사 추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="5d1f1-219">hello 권장 접근 방식을 toouse hello에 있는 Azure VM에서 동기 복사는 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5d1f1-220">결론</span><span class="sxs-lookup"><span data-stu-id="5d1f1-220">Conclusion</span></span>
<span data-ttu-id="5d1f1-221">이제 데이터 이동 응용 프로그램이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-221">Our data movement application is now complete.</span></span> <span data-ttu-id="5d1f1-222">[hello 전체 코드 샘플은 GitHub에서 사용할 수 있는](https://github.com/azure-samples/storage-dotnet-data-movement-library-app)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d1f1-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d1f1-223">Next steps</span></span>
<span data-ttu-id="5d1f1-224">이 시작 자습서에서 Azure Storage와 상호 작용하고 Windows, Linux 및 macOS에서 실행되는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="5d1f1-225">이 입문서에서는 Blob Storage에 초점을 맞추었지만,</span><span class="sxs-lookup"><span data-stu-id="5d1f1-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="5d1f1-226">그러나이 동일한 기술 자료에 적용 된 tooFile 저장소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="5d1f1-227">toolearn을 체크 아웃 [Azure 저장소 데이터 이동을 라이브러리 참조 문서](https://azure.github.io/azure-storage-net-data-movement)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d1f1-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




