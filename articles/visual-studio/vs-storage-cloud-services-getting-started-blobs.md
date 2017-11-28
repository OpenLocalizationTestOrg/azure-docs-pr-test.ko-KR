---
title: "blob 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (클라우드 서비스) | Microsoft Docs"
description: "연결 된 서비스를 Visual Studio를 사용 하 여 tooa 저장소 계정을 연결 후 Visual Studio에서 클라우드 서비스 프로젝트에서 Azure Blob 저장소를 사용 하 여 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="2aa74-103">Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(클라우드 서비스 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="2aa74-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2aa74-104">개요</span><span class="sxs-lookup"><span data-stu-id="2aa74-104">Overview</span></span>
<span data-ttu-id="2aa74-105">이 문서에서 설명 하는 hello Visual Studio를 사용 하 여 Azure 저장소 계정을 참조 하거나 만든 후 tooget Azure Blob 저장소 시작 방법을 **연결 된 서비스 추가** 대화 상자에 Visual Studio 클라우드 서비스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="2aa74-106">방식을 보여줍니다 tooaccess blob 컨테이너 및 업로드, 나열 및 blob를 다운로드할 tooperform 일반적인 작업의 같은 방식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="2aa74-107">hello 샘플은 C로 작성 된\# hello를 사용 하 여 [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/dn261237.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="2aa74-108">Azure Blob 저장소는 많은 양의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="2aa74-109">단일 Blob은 임의의 크기일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-109">A single blob can be any size.</span></span> <span data-ttu-id="2aa74-110">Blob은 이미지, 오디오 및 비디오 파일, 원시 데이터, 문서 파일 등일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="2aa74-111">파일이 폴더에 저장되듯이 저장소 Blob은 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="2aa74-112">저장소를 만든 후에 hello 저장소에서 하나 이상의 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="2aa74-113">예를 들어 "스크랩" 라는 저장소에서 "이미지" toostore 그림을 호출 하는 hello 저장소의 컨테이너를 만들 수 있습니다 및 다른 호출한 "오디오" toostore 오디오 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="2aa74-114">Hello 컨테이너를 만든 후 파일 toothem 개별 blob를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="2aa74-115">프로그래밍 방식으로 조작하는 blob에 대한 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa74-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="2aa74-116">Azure 저장소에 대한 일반 정보는 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa74-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="2aa74-117">Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa74-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="2aa74-118">ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa74-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="2aa74-119">코드에서 Blob 컨테이너에 액세스하기</span><span class="sxs-lookup"><span data-stu-id="2aa74-119">Access blob containers in code</span></span>
<span data-ttu-id="2aa74-120">클라우드 서비스 프로젝트에서 blob를 액세스 하는 tooprogrammatically, 이미 존재 하지 않는 경우 다음 항목을 tooadd hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="2aa74-121">Azure 저장소 tooprogrammatically 액세스 원하는 모든 C# 파일의 코드 네임 스페이스 선언을 toohello 위쪽 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="2aa74-122">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2aa74-123">사용 하 여 hello tooget 코드를 다음 저장소 연결 문자열 및 hello Azure 서비스 구성에서 저장소 계정 정보 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="2aa74-124">가져오기는 **CloudBlobClient** tooreference 저장소 계정에 기존 컨테이너 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="2aa74-125">가져오기는 **CloudBlobContainer** tooreference 특정 blob 컨테이너 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="2aa74-126">모든 hello hello 다음 섹션에에서 표시 된 hello 코드 앞에 이전 절차에 표시 된 hello 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="2aa74-127">코드에서 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="2aa74-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="2aa74-128">ASP.NET에서 tooAzure 저장소 호출을 수행 하는 일부 Api는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="2aa74-129">자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa74-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="2aa74-130">다음 예에서는 hello에 hello 코드는 비동기 프로그래밍 메서드를 사용 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="2aa74-131">저장소 계정에서 컨테이너 toocreate toodo 가장 필요한 것은 호출 추가 너무**CreateIfNotExistsAsync** 코드 다음 hello와 같이:</span><span class="sxs-lookup"><span data-stu-id="2aa74-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="2aa74-132">hello 컨테이너 사용 가능한 tooeveryone 내의 toomake hello 파일을 설정할 수 있습니다 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="2aa74-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="2aa74-133">Hello 인터넷에서 누구나 공용 컨테이너의 blob를 볼 수 있지만 수정 하거나 hello 적절 한 액세스 키가 있는 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="2aa74-134">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="2aa74-134">Upload a blob into a container</span></span>
<span data-ttu-id="2aa74-135">Azure 저장소는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="2aa74-136">Hello 대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="2aa74-137">tooupload 파일 tooa 블록 blob 컨테이너 참조를 가져오고 tooget 블록 blob 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="2aa74-138">Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 만든 후 업로드할 수 있습니다 **UploadFromStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="2aa74-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="2aa74-139">이 작업은 이전에 없던 되거나 파일이 있으면 덮어씁니다 hello blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="2aa74-140">hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="2aa74-141">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="2aa74-141">List hello blobs in a container</span></span>
<span data-ttu-id="2aa74-142">먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="2aa74-143">Hello 컨테이너를 사용 하 여 있습니다 **ListBlobs** tooretrieve hello blob 메서드 및/또는 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="2aa74-144">tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **IListBlobItem**, tooa 캐스팅 해야 **CloudBlockBlob**, **CloudPageBlob**, 또는  **CloudBlobDirectory** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="2aa74-145">Hello 종류를 알 수 없는 경우 사용할 수 있습니다 형식 검사 toodetermine 어떤 toocast 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="2aa74-146">hello 다음 코드에서는 방법을 tooretrieve 및 출력 hello hello의 각 항목의 URI **사진** 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="2aa74-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
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

<span data-ttu-id="2aa74-147">Hello 앞의 코드 예제와 같이 hello blob 서비스에도 컨테이너 내에서 디렉터리의 hello 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="2aa74-148">따라서 폴더와 유사한 구조로 Blob을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="2aa74-149">예를 들어 라는 컨테이너에 블록 blob의 집합을 추적 하는 hello **사진**:</span><span class="sxs-lookup"><span data-stu-id="2aa74-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="2aa74-150">호출 하는 경우 **ListBlobs** hello 컨테이너 (예: hello 이전 샘플)를 반환 하는 hello 컬렉션 포함 **CloudBlobDirectory** 및 **CloudBlockBlob** 개체 hello 디렉터리 및 hello 최상위 수준에 포함 된 blob을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="2aa74-151">Hello 출력 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="2aa74-152">필요에 따라 hello를 설정할 수 있습니다 **UseFlatBlobListing** hello의 매개 변수 **ListBlobs** 메서드를 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="2aa74-153">이 경우 디렉터리에 관계없이 모든 Blob이 **CloudBlockBlob**으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="2aa74-154">Hello 호출을 너무 같습니다**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="2aa74-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="2aa74-155">및 다음은 hello 결과:</span><span class="sxs-lookup"><span data-stu-id="2aa74-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="2aa74-156">자세한 내용은 [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa74-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="2aa74-157">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="2aa74-157">Download blobs</span></span>
<span data-ttu-id="2aa74-158">toodownload blob을 먼저 blob 참조를 검색 하 고 hello 호출 **DownloadToStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="2aa74-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="2aa74-159">hello 다음 예제에서는 hello **DownloadToStream** 메서드 tootransfer hello blob 내용 tooa stream 개체 다음 tooa 로컬 파일 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="2aa74-160">Hello를 사용할 수도 있습니다 **DownloadToStream** 텍스트 문자열로 blob 내용의 toodownload hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="2aa74-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="2aa74-161">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="2aa74-161">Delete blobs</span></span>
<span data-ttu-id="2aa74-162">toodelete blob blob 참조를 먼저 가져온 고 호출 하 여 **삭제** 메서드.</span><span class="sxs-lookup"><span data-stu-id="2aa74-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="2aa74-163">여러 페이지에서 비동기식으로 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="2aa74-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="2aa74-164">많은 수의 blob 나열 하거나 하나의 나열 작업에서 반환 하는 결과 toocontrol hello 수, 결과의 페이지 blob을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="2aa74-165">이 예제에서는 표시 방법을 tooreturn 결과 페이지에서 비동기적으로 하 여 실행 tooreturn 다양 한 결과 기다리는 동안 차단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="2aa74-166">이 예에서는 플랫 blob을 나열 하지만 hello 설정 하 여 계층적 목록을 수행할 수도 있습니다 **useFlatBlobListing** hello의 매개 변수 **ListBlobsSegmentedAsync** 메서드 너무 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="2aa74-167">앞 hello로 해야 hello 예제 메서드는 비동기 메서드를 호출 하기 때문에 **비동기** 키워드 및이 반환 해야 합니다는 **작업** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="2aa74-168">hello await 키워드 hello에 대 한 지정 **ListBlobsSegmentedAsync** 메서드 hello 목록 작업이 완료 될 때까지 hello 샘플 메서드의 실행을 일시 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa74-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="2aa74-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2aa74-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

