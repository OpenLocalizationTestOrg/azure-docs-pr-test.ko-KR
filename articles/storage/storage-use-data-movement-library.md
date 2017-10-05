---
title: "Microsoft Azure Storage 데이터 이동 라이브러리를 사용하여 데이터 전송 | Microsoft Docs"
description: "데이터 이동 라이브러리를 사용하여 Blob과 파일 콘텐츠간에 데이터를 이동하거나 복사합니다. 로컬 파일에서 Azure 저장소로 데이터를 복사하거나, 저장소 계정 내에서 데이터를 복사하거나, 저장소 계정 간에 데이터를 복사합니다. 데이터를 Azure 저장소로 손쉽게 마이그레이션할 수 있습니다."
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="8da4f-105">Microsoft Azure Storage 데이터 이동 라이브러리를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="8da4f-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="8da4f-106">개요</span><span class="sxs-lookup"><span data-stu-id="8da4f-106">Overview</span></span>
<span data-ttu-id="8da4f-107">Microsoft Azure Storage 데이터 이동 라이브러리는 Azure Storage Blob 및 파일의 고성능 업로드, 다운로드 및 복사를 위해 설계된 플랫폼 간 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="8da4f-108">이 라이브러리는 [AzCopy](storage-use-azcopy.md)를 지원하는 핵심 데이터 이동 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="8da4f-109">데이터 이동 라이브러리는 기존의 [.NET Azure Storage 클라이언트 라이브러리](storage-dotnet-how-to-use-blobs.md)에서 사용할 수 없는 편리한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8da4f-110">여기에는 병렬 작업 수를 설정하고, 전송 진행률을 추적하며, 취소된 전송을 손쉽게 다시 시작하는 등의 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="8da4f-111">이 라이브러리는 .NET Core를 사용하기 때문에 Windows, Linux 및 macOS용 .NET 앱을 빌드할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="8da4f-112">.NET Core에 대한 자세한 내용은 [.NET Core 설명서](https://dotnet.github.io/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8da4f-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="8da4f-113">또한 이 라이브러리는 전통적인 Windows용 .NET Framework 앱에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="8da4f-114">이 문서에서는 Windows, Linux 및 macOS에서 실행되는 .NET Core 콘솔 응용 프로그램을 만들고 다음 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="8da4f-115">Blob Storage에 파일과 디렉터리를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="8da4f-116">데이터를 전송할 때 수행할 병렬 작업 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="8da4f-117">데이터 전송 진행률을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-117">Track data transfer progress.</span></span>
- <span data-ttu-id="8da4f-118">취소된 데이터 전송을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="8da4f-119">URL에서 Blob Storage로 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="8da4f-120">Blob Storage 간에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="8da4f-121">**필요한 항목**</span><span class="sxs-lookup"><span data-stu-id="8da4f-121">**What you need:**</span></span>

* [<span data-ttu-id="8da4f-122">Contact.java</span><span class="sxs-lookup"><span data-stu-id="8da4f-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="8da4f-123">[Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8da4f-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="8da4f-124">이 가이드는 [Azure 저장소](https://azure.microsoft.com/services/storage/)에 대해 잘 알고 있다는 것을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="8da4f-125">그렇지 않은 경우 [Azure Storage 소개](storage-introduction.md) 설명서가 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="8da4f-126">가장 중요한 점은 데이터 이동 라이브러리의 사용을 시작하려면 [저장소 계정을 만들어야](storage-create-storage-account.md#create-a-storage-account) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="8da4f-127">설정</span><span class="sxs-lookup"><span data-stu-id="8da4f-127">Setup</span></span>  

1. <span data-ttu-id="8da4f-128">[.NET Core 설치 가이드](https://www.microsoft.com/net/core)를 방문하여 .NET Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="8da4f-129">사용자 환경을 선택할 때 명령줄 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="8da4f-130">명령줄에서 프로젝트에 대한 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="8da4f-131">이 디렉터리로 이동한 다음 `dotnet new`를 입력하여 C# 콘솔 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="8da4f-132">Visual Studio Code에서 이 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="8da4f-133">이 단계는 `code .`를 입력하여 명령줄을 통해 빠르게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="8da4f-134">Visual Studio Code Marketplace에서 [C# 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="8da4f-135">Visual Studio Code를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="8da4f-136">이 시점에서 두 가지 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="8da4f-137">하나는 "빌드 및 디버그에 필요한 자산"을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="8da4f-138">"예"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-138">Click "yes."</span></span> <span data-ttu-id="8da4f-139">또 다른 프롬프트는 해결되지 않은 종속성을 복원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="8da4f-140">"복원"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-140">Click "restore."</span></span>
6. <span data-ttu-id="8da4f-141">이제 응용 프로그램에는 `.vscode` 디렉터리에 `launch.json` 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="8da4f-142">이 파일에서 `externalConsole` 값을 `true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="8da4f-143">Visual Studio Code를 사용하면 .NET Core 응용 프로그램을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="8da4f-144">`F5` 키를 눌러 응용 프로그램을 실행하고 설정이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="8da4f-145">콘솔에 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="8da4f-145">You should see "Hello World!"</span></span> <span data-ttu-id="8da4f-146">가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="8da4f-147">프로젝트에 데이터 이동 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="8da4f-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="8da4f-148">`project.json` 파일의 `dependencies` 섹션에 최신 버전의 데이터 이동 라이브러리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="8da4f-149">이 문서를 작성한 시점에서 해당 버전은 `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="8da4f-150">`imports` 섹션에 `"portable-net45+win8"`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="8da4f-151">프로젝트를 복원하기 위해 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="8da4f-152">"복원" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-152">Click the "restore" button.</span></span> <span data-ttu-id="8da4f-153">또한 프로젝트 디렉터리의 루트에 `dotnet restore` 명령을 입력하여 명령줄에서 프로젝트를 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="8da4f-154">다음과 같이 `project.json`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="8da4f-155">응용 프로그램의 기본 구조 설정</span><span class="sxs-lookup"><span data-stu-id="8da4f-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="8da4f-156">가장 먼저 수행할 작업은 응용 프로그램의 "기본 구조" 코드를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="8da4f-157">이 코드는 저장소 계정 이름과 계정 키를 묻는 메시지를 표시하고 해당 자격 증명을 사용하여 `CloudStorageAccount` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="8da4f-158">이 개체는 모든 전송 시나리오에서 저장소 계정과 상호 작용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="8da4f-159">또한 이 코드는 실행하고자 하는 전송 작업의 유형도 선택하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="8da4f-160">다음과 같이 `Program.cs`를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="8da4f-161">Azure Blob으로 로컬 파일 전송</span><span class="sxs-lookup"><span data-stu-id="8da4f-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="8da4f-162">다음과 같이 `GetSourcePath`와 `GetBlob` 메서드를 `Program.cs`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="8da4f-163">다음과 같이 `TransferLocalFileToAzureBlob` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="8da4f-164">이 코드는 로컬 파일의 경로, 새 컨테이너 또는 기존 컨테이너의 이름 및 새 Blob의 이름을 입력하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="8da4f-165">`TransferManager.UploadAsync` 메서드에서 이 정보를 사용하여 업로드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="8da4f-166">`F5` 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="8da4f-167">[Microsoft Azure Storage 탐색기](http://storageexplorer.com/)로 저장소 계정을 확인하여 업로드를 수행했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="8da4f-168">병렬 작업 수 설정</span><span class="sxs-lookup"><span data-stu-id="8da4f-168">Set number of parallel operations</span></span>
<span data-ttu-id="8da4f-169">데이터 이동 라이브러리에서 제공하는 가장 큰 특징은 병렬 작업의 수를 설정하여 데이터 전송 처리량을 높일 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="8da4f-170">기본적으로 데이터 이동 라이브러리는 병렬 작업 수를 8 * 컴퓨터 코어 수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="8da4f-171">저대역폭 환경에서는 많은 병렬 작업으로 인해 네트워크 연결에 과부하가 걸릴 수 있으며 실제로 작업이 완전히 완료되지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="8da4f-172">사용 가능한 네트워크 대역폭에 따라 가장 적합한 설정을 결정하려면 해당 설정을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="8da4f-173">병렬 작업 수를 설정할 수 있는 몇 가지 코드를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="8da4f-174">전송이 완료되는 데 걸리는 시간을 제어하는 코드도 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="8da4f-175">다음과 같이 `SetNumberOfParallelOperations` 메서드를 `Program.cs`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="8da4f-176">다음과 같이 `SetNumberOfParallelOperations`를 사용하도록 `ExecuteChoice` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="8da4f-177">다음과 같이 타이머를 사용하도록 `TransferLocalFileToAzureBlob` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="8da4f-178">전송 진행률 추적</span><span class="sxs-lookup"><span data-stu-id="8da4f-178">Track transfer progress</span></span>
<span data-ttu-id="8da4f-179">데이터를 전송하는 데 얼마나 오랜 시간이 걸렸는지를 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="8da4f-180">하지만 *전송 중인* 진행 상황을 볼 수 있다면 전송 작업이 훨씬 더 효율적일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="8da4f-181">이 시나리오를 달성하려면 `TransferContext` 개체를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="8da4f-182">`TransferContext` 개체는 `SingleTransferContext`와 `DirectoryTransferContext`의 두 가지 형식으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="8da4f-183">전자는 하나의 파일(지금 사용 중인 파일)을 전송하기 위한 것이고, 후자는 파일의 디렉터리(나중에 추가)를 전송하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="8da4f-184">다음과 같이 `GetSingleTransferContext`와 `GetDirectoryTransferContext` 메서드를 `Program.cs`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="8da4f-185">다음과 같이 `GetSingleTransferContext`를 사용하도록 `TransferLocalFileToAzureBlob` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="8da4f-186">취소된 전송 다시 시작</span><span class="sxs-lookup"><span data-stu-id="8da4f-186">Resume a canceled transfer</span></span>
<span data-ttu-id="8da4f-187">데이터 이동 라이브러리에서 제공하는 또 다른 편리한 기능은 취소된 전송을 다시 시작할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="8da4f-188">`c`를 입력하여 전송을 일시적으로 취소할 수 있는 코드를 추가한 다음 3초 후에 전송을 다시 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="8da4f-189">다음과 같이 `TransferLocalFileToAzureBlob`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="8da4f-190">지금까지 `checkpoint` 값은 항상 `null`로 설정되어 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="8da4f-191">이제 전송을 취소하면 전송의 마지막 검사점을 검색한 다음 전송 컨텍스트에서 새로운 이 검사점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="8da4f-192">Azure Blob 디렉터리로 로컬 디렉터리 전송</span><span class="sxs-lookup"><span data-stu-id="8da4f-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="8da4f-193">데이터 이동 라이브러리에서 한 번에 파일 하나만 전송 가능하다면 충족스럽지 못할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="8da4f-194">다행히도 그렇지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-194">Luckily, this is not the case.</span></span> <span data-ttu-id="8da4f-195">데이터 이동 라이브러리는 파일의 디렉터리와 모든 해당 하위 디렉터리를 전송할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="8da4f-196">이렇게 수행할 수 있는 몇 가지 코드를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="8da4f-197">먼저 다음과 같이 `GetBlobDirectory` 메서드를 `Program.cs`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="8da4f-198">그런 후 다음과 같이 `TransferLocalDirectoryToAzureBlobDirectory`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="8da4f-199">이 메서드와 단일 파일 업로드 메서드 간에는 몇 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="8da4f-200">현재 `TransferManager.UploadDirectoryAsync`와 이전에 만든 `getDirectoryTransferContext` 메서드를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="8da4f-201">또한 업로드 작업에 `options` 값도 제공하므로 업로드 시 하위 디렉터리를 포함하도록 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="8da4f-202">URL에서 Azure Blob으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="8da4f-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="8da4f-203">이제 URL에서 Azure Blob으로 파일을 복사할 수 있는 코드를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="8da4f-204">다음과 같이 `TransferUrlToAzureBlob`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="8da4f-205">이 기능의 중요한 사용 사례 중 하나로 다른 클라우드 서비스(예: AWS)에서 Azure로 데이터를 이동해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="8da4f-206">이때 리소스에 액세스할 수 있는 URL이 있으면 `TransferManager.CopyAsync` 메서드를 사용하여 해당 리소스를 Azure Blob으로 쉽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="8da4f-207">또한 이 메서드는 새로운 부울 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="8da4f-208">이 매개 변수를 `true`로 설정하면 비동기 서버 쪽 복사를 수행하려고 한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="8da4f-209">이 매개 변수를 `false`로 설정하면 리소스를 로컬 시스템에 다운로드한 다음 Azure Blob에 업로드하는 동기 복사를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="8da4f-210">그러나 동기 복사는 현재 한 Azure Storage 리소스에서 다른 Azure Storage 리소스로 복사할 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="8da4f-211">Azure Blob 간 전송</span><span class="sxs-lookup"><span data-stu-id="8da4f-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="8da4f-212">데이터 이동 라이브러리에서 제공하는 또 다른 기능은 한 Azure Storage 리소스에서 다른Azure Storage 리소스로 복사하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="8da4f-213">다음과 같이 `TransferAzureBlobToAzureBlob`을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="8da4f-214">이 예제에서는 `TransferManager.CopyAsync`의 부울 매개 변수를 `false`로 설정하여 동기 복사를 수행하려고 한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="8da4f-215">즉 리소스를 로컬 시스템에 먼저 다운로드한 다음 Azure Blob으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="8da4f-216">동기 복사 옵션은 복사 작업을 일관된 속도로 수행하도록 보장하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="8da4f-217">반면에 비동기 서버 쪽 복사 속도는 서버에서 사용할 수 있는 네트워크 대역폭에 따라 다르며 변동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="8da4f-218">그러나 동기 복사는 비동기 복사에 비해 추가적인 송신 비용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="8da4f-219">원본 저장소 계정과 동일한 지역에 있는 Azure VM에서 동기 복사를 사용하여 송신 비용이 발생하지 않도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8da4f-220">결론</span><span class="sxs-lookup"><span data-stu-id="8da4f-220">Conclusion</span></span>
<span data-ttu-id="8da4f-221">이제 데이터 이동 응용 프로그램이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-221">Our data movement application is now complete.</span></span> <span data-ttu-id="8da4f-222">[전체 코드 샘플은 GitHub에서 사용할 수 있습니다](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="8da4f-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8da4f-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8da4f-223">Next steps</span></span>
<span data-ttu-id="8da4f-224">이 시작 자습서에서 Azure Storage와 상호 작용하고 Windows, Linux 및 macOS에서 실행되는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="8da4f-225">이 입문서에서는 Blob Storage에 초점을 맞추었지만,</span><span class="sxs-lookup"><span data-stu-id="8da4f-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="8da4f-226">이 동일한 정보를 File Storage에도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8da4f-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="8da4f-227">자세한 내용은 [Azure Storage 데이터 이동 라이브러리 참조 설명서](https://azure.github.io/azure-storage-net-data-movement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8da4f-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




