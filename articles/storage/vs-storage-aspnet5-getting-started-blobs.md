---
title: "blob 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (ASP.NET Core) | Microsoft Docs"
description: "연결 된 서비스 tooget 시작 Visual Studio를 사용 하 여 저장소 계정을 만든 후 Visual Studio ASP.NET Core 프로젝트에 Azure Blob 저장소를 사용 하는 방법"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="8bd4a-103">Azure Blob Storage 및 Visual Studio 연결된 서비스 시작(ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="8bd4a-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="8bd4a-104">개요</span><span class="sxs-lookup"><span data-stu-id="8bd4a-104">Overview</span></span>
<span data-ttu-id="8bd4a-105">이 문서에서는 tooget 시작 hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 ASP.NET Core 프로젝트에 Azure 저장소 계정을 참조 하거나 만든 후 Visual Studio에서 Azure Blob 저장소를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="8bd4a-106">Azure Blob 저장소는 많은 양의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="8bd4a-107">단일 Blob은 임의의 크기일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-107">A single blob can be any size.</span></span> <span data-ttu-id="8bd4a-108">Blob은 이미지, 오디오 및 비디오 파일, 원시 데이터, 문서 파일 등일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="8bd4a-109">이 문서에서는 Visual Studio hello를 사용 하 여 Azure 저장소 계정을 만든 후 tooget blob 저장소 시작 방법 설명 **연결 된 서비스 추가** ASP.NET Core 프로젝트에 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="8bd4a-110">파일이 폴더에 저장되듯이 저장소 Blob은 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="8bd4a-111">저장소를 만든 후에 hello 저장소에서 하나 이상의 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="8bd4a-112">예를 들어 "스크랩" 라는 저장소에서 "이미지" toostore 그림을 호출 하는 hello 저장소의 컨테이너를 만들 수 있습니다 및 다른 호출한 "오디오" toostore 오디오 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="8bd4a-113">Hello 컨테이너를 만든 후 파일 toothem 개별 blob를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="8bd4a-114">Blob을 프로그래밍 방식으로 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="8bd4a-115">코드에서 Blob 컨테이너에 액세스하기</span><span class="sxs-lookup"><span data-stu-id="8bd4a-115">Access blob containers in code</span></span>
<span data-ttu-id="8bd4a-116">ASP.NET Core 프로젝트에 대 한 액세스 blob tooprogrammatically 해야 tooadd hello 다음 항목을 이미 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="8bd4a-117">Hello 코드 네임 스페이스 선언을 toohello 위쪽 tooprogrammatically 액세스 메트릭을 제공 하기를 원하는 C# 파일에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="8bd4a-118">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8bd4a-119">다음 코드 tooget hello를 사용 하 여 저장소 연결 문자열 및 hello Azure 서비스 구성에서 저장소 계정 정보.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="8bd4a-120">**참고:** hello 다음 섹션에서에서 코드 hello 코드 앞에 위의 hello를 모두 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="8bd4a-121">사용 하 여 한 **CloudBlobClient** tooget 개체는 **CloudBlobContainer** 저장소 계정에 참조 tooan 기존 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="8bd4a-122">코드에서 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="8bd4a-122">Create a container in code</span></span>
<span data-ttu-id="8bd4a-123">Hello를 사용할 수도 있습니다 **CloudBlobClient** toocreate 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="8bd4a-124">Toodo 있으면 tooadd 호출 너무**CreateIfNotExistsAsync** 코드 다음 hello와 같이:</span><span class="sxs-lookup"><span data-stu-id="8bd4a-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="8bd4a-125">**참고:** hello에서 ASP.NET Core tooAzure 저장소 호출을 수행 하는 Api는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="8bd4a-126">자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="8bd4a-127">아래 hello 코드는 비동기 프로그래밍 메서드를 사용 하 되 고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="8bd4a-128">hello 컨테이너 사용 가능한 tooeveryone 내의 toomake hello 파일을 설정할 수 있습니다 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="8bd4a-129">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="8bd4a-129">Upload a blob into a container</span></span>
<span data-ttu-id="8bd4a-130">컨테이너에 있는 blob 파일 tooupload를 컨테이너 참조를 가져오고 tooget blob 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="8bd4a-131">Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 사용 하는 다음 업로드할 수 있습니다 **UploadFromStreamAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="8bd4a-132">이 작업은 아직 실행 하지 않은, 있거나 파일이 있으면 덮어씁니다 hello blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="8bd4a-133">hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="8bd4a-134">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="8bd4a-134">List hello blobs in a container</span></span>
<span data-ttu-id="8bd4a-135">먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="8bd4a-136">Hello 컨테이너를 호출할 수 있습니다 **ListBlobsSegmentedAsync** 메서드 tooretrieve hello blob 및/또는 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="8bd4a-137">tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **IListBlobItem**, tooa 캐스팅 해야 **CloudBlockBlob**, **CloudPageBlob**, 또는  **CloudBlobDirectory** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="8bd4a-138">경우 입력 hello blob를 알 수 없는 형식 검사 toodetermine 어떤 toocast를 사용할 수 있습니다, 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="8bd4a-139">코드 다음 hello tooretrieve 및 출력 컨테이너의 각 항목의 URI hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

<span data-ttu-id="8bd4a-140">Blob 컨테이너의 방법으로 toolist hello 내용의 다른 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="8bd4a-141">자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="8bd4a-142">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="8bd4a-142">Download a blob</span></span>
<span data-ttu-id="8bd4a-143">toodownload blob 가져오려면 먼저 참조 toohello blob를 hello 호출 **DownloadToStreamAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="8bd4a-144">hello 다음 예제에서는 hello **DownloadToStreamAsync** 메서드 tootransfer hello blob 내용 tooa 스트림 개체를 로컬 파일로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="8bd4a-145">다른 여러 가지 toosave blob 파일로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="8bd4a-146">자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md#download-blobs) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="8bd4a-147">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="8bd4a-147">Delete a blob</span></span>
<span data-ttu-id="8bd4a-148">toodelete blob 가져오려면 먼저 참조 toohello blob를 hello 호출 **DeleteAsync** 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd4a-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="8bd4a-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bd4a-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

