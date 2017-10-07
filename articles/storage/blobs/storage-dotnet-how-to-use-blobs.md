---
title: ".NET을 사용 하 여 Azure Blob 저장소 (개체 저장소) aaaGet 시작 | Microsoft Docs"
description: "Azure Blob 저장소 (개체 저장소)를 사용 하는 hello 클라우드에 구조화 되지 않은 데이터를 저장 합니다."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="119a1-103">.NET을 사용하여 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="119a1-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="119a1-104">Azure Blob 저장소는 hello 클라우드에서 개체/blob으로 구조화 되지 않은 데이터를 저장 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="119a1-105">Blob storage는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="119a1-106">Blob 저장소 참조 tooas 개체 저장소 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="119a1-107">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="119a1-107">About this tutorial</span></span>
<span data-ttu-id="119a1-108">이 자습서에서는 Azure Blob 저장소를 사용 하 여 몇 가지 일반적인 시나리오에 대 한.NET toowrite 코드 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="119a1-109">Blob 업로드, 나열, 다운로드 및 삭제 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="119a1-110">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="119a1-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="119a1-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="119a1-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="119a1-112">.NET용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="119a1-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="119a1-113">.NET용 Azure 구성 관리자</span><span class="sxs-lookup"><span data-stu-id="119a1-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="119a1-114">[Azure 저장소 계정](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="119a1-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="119a1-115">추가 샘플</span><span class="sxs-lookup"><span data-stu-id="119a1-115">More samples</span></span>
<span data-ttu-id="119a1-116">Blob 저장소를 사용하는 추가 예제는 [.NET에서 Azure Blob 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="119a1-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="119a1-117">Hello 샘플 응용 프로그램을 다운로드 하 고 실행 하거나 GitHub에서 hello 코드를 찾아보려면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="119a1-118">지시문을 사용하여 추가</span><span class="sxs-lookup"><span data-stu-id="119a1-118">Add using directives</span></span>
<span data-ttu-id="119a1-119">Hello 다음 추가 **를 사용 하 여** 지시문 toohello 맨 hello `Program.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="119a1-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="119a1-120">Hello 연결 문자열을 구문 분석</span><span class="sxs-lookup"><span data-stu-id="119a1-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="119a1-121">Hello Blob 서비스 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="119a1-121">Create hello Blob service client</span></span>
<span data-ttu-id="119a1-122">hello **CloudBlobClient** 클래스를 사용 하면 tooretrieve 컨테이너 및 blob를 Blob 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="119a1-123">한 가지 방법은 toocreate hello 서비스 클라이언트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="119a1-124">이제 준비 toowrite 코드에서 데이터를 읽고 tooBlob 저장소 데이터를 기록 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="119a1-125">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="119a1-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="119a1-126">이 예에서는 어떻게 toocreate 아직 없는 경우 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="119a1-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="119a1-127">기본적으로 hello 새 컨테이너는 private,이 컨테이너에서 저장소 액세스 키 toodownload blob를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="119a1-128">Hello 컨테이너 사용 가능한 tooeveryone 내의 toomake hello 파일을 사용 하도록 하려는 경우 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="119a1-129">Hello 인터넷에서 모든 공용 컨테이너의 blob를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="119a1-130">그러나 수정 하거나 hello 적절 한 계정 액세스 키 또는 공유 액세스 서명이 있는 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="119a1-131">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="119a1-131">Upload a blob into a container</span></span>
<span data-ttu-id="119a1-132">Azure Blob Storage는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="119a1-133">대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="119a1-134">tooupload 파일 tooa 블록 blob 컨테이너 참조를 가져오고 tooget 블록 blob 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="119a1-135">Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 만든 후 업로드할 수 있습니다 **UploadFromStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="119a1-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="119a1-136">이 작업은 이전에 없던 되거나 파일이 있으면 덮어씁니다 hello blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="119a1-137">hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="119a1-138">컨테이너에서 hello blob 나열</span><span class="sxs-lookup"><span data-stu-id="119a1-138">List hello blobs in a container</span></span>
<span data-ttu-id="119a1-139">먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="119a1-140">Hello 컨테이너를 사용 하 여 있습니다 **ListBlobs** tooretrieve hello blob 메서드 및/또는 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="119a1-141">tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **IListBlobItem**, tooa 캐스팅 해야 **CloudBlockBlob**, **CloudPageBlob**, 또는  **CloudBlobDirectory** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="119a1-142">Hello 종류를 알 수 없는 경우 사용할 수 있습니다 형식 검사 toodetermine 어떤 toocast 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="119a1-143">hello 다음 코드에서는 방법을 tooretrieve 및 출력 hello hello의 각 항목의 URI _사진_ 컨테이너:</span><span class="sxs-lookup"><span data-stu-id="119a1-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

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
```

<span data-ttu-id="119a1-144">Blob 이름에서 경로 정보를 포함하여 기존 파일 시스템과 같이 구성하고 트래버스할 수 있는 가상 디렉터리 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="119a1-145">hello 디렉터리 구조는 가상 Blob 저장소에 사용할 수 있는 리소스 컨테이너 및 blob에만-hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="119a1-146">그러나 제공 hello 저장소 클라이언트 라이브러리는 **CloudBlobDirectory** toorefer tooa 가상 디렉터리 개체를 이러한 방식으로 구성 된 blob을 사용 하 여 처리 hello 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="119a1-147">예를 들어 라는 컨테이너에 블록 blob의 집합을 추적 하는 hello *사진*:</span><span class="sxs-lookup"><span data-stu-id="119a1-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="119a1-148">호출 하는 경우 **ListBlobs** hello에 *사진* 컨테이너 (예: hello 코드 조각 앞), 계층적 목록을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="119a1-149">둘 다 포함 되어 **CloudBlobDirectory** 및 **CloudBlockBlob** hello 디렉터리 및 hello 컨테이너의 blob를 각각 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="119a1-150">hello 결과 출력은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="119a1-151">필요에 따라 hello를 설정할 수 있습니다 **UseFlatBlobListing** hello의 매개 변수 **ListBlobs** 메서드를 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="119a1-152">Hello 컨테이너의 모든 blob로 반환 되는 경우에 **CloudBlockBlob** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="119a1-153">호출을 너무 hello**ListBlobs** tooreturn 플랫 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="119a1-154">및 hello 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="119a1-155">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="119a1-155">Download blobs</span></span>
<span data-ttu-id="119a1-156">toodownload blob을 먼저 blob 참조를 검색 하 고 hello 호출 **DownloadToStream** 메서드.</span><span class="sxs-lookup"><span data-stu-id="119a1-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="119a1-157">hello 다음 예제에서는 hello **DownloadToStream** 메서드 tootransfer hello blob 내용 tooa stream 개체 다음 tooa 로컬 파일 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="119a1-158">Hello를 사용할 수도 있습니다 **DownloadToStream** 텍스트 문자열로 blob 내용의 toodownload hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="119a1-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="119a1-159">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="119a1-159">Delete blobs</span></span>
<span data-ttu-id="119a1-160">toodelete blob blob 참조를 먼저 가져온 고 호출 하 여 **삭제** 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="119a1-161">여러 페이지에서 비동기식으로 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="119a1-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="119a1-162">많은 수의 blob 나열 하거나 하나의 나열 작업에서 반환 하는 결과 toocontrol hello 수, 결과의 페이지 blob을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="119a1-163">이 예제에서는 표시 방법을 tooreturn 결과 페이지에서 비동기적으로 하 여 실행 tooreturn 다양 한 결과 기다리는 동안 차단 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="119a1-164">이 예에서는 플랫 blob을 나열 하지만 hello 설정 하 여 계층적 목록을 수행할 수도 있습니다 _useFlatBlobListing_ hello의 매개 변수 **ListBlobsSegmentedAsync** 메서드 too_false_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="119a1-165">앞 hello로 해야 hello 예제 메서드는 비동기 메서드를 호출 하기 때문에 _비동기_ 키워드 및이 반환 해야 합니다는 **작업** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="119a1-166">hello await 키워드 hello에 대 한 지정 **ListBlobsSegmentedAsync** 메서드 hello 목록 작업이 완료 될 때까지 hello 샘플 메서드의 실행을 일시 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
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
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="119a1-167">쓰기 tooan 추가 blob</span><span class="sxs-lookup"><span data-stu-id="119a1-167">Writing tooan append blob</span></span>
<span data-ttu-id="119a1-168">추가 Blob은 로깅 등의 추가 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="119a1-169">블록 blob와 같은 추가 blob는 블록으로 구성 됩니다 이지만 새 블록 tooan 추가 blob에 추가 하면 항상 hello blob의 추가 toohello 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="119a1-170">추가 Blob의 기존 블록을 업데이트하거나 삭제할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="119a1-171">추가 blob에 대 한 hello 블록 Id에는 블록 blob으로 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="119a1-172">추가 blob의 각 블록 tooa 최대 4MB, 위로 크기가 다양할 수 있습니다 및 추가 blob는 최대 50, 000 블록을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="119a1-173">hello 추가 blob의 최대 크기 (4 MB X 50, 000 블록) 195 GB 보다 조금 더 큰 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="119a1-174">hello 감시할 새 blob를 만들고 간단한 로깅 작업을 시뮬레이션 일부 데이터 tooit 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="119a1-175">참조 [이해 블록 Blob, 페이지 Blob 및 Blob 추가](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) hello 차이 hello 세 가지 유형의 blob에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="119a1-176">Blob 보안 관리</span><span class="sxs-lookup"><span data-stu-id="119a1-176">Managing security for blobs</span></span>
<span data-ttu-id="119a1-177">기본적으로 Azure 저장소 데이터 보안 유지 hello 계정 액세스 키를 소유한 인 액세스 toohello 계정 소유자를 제한 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="119a1-178">저장소 계정에 tooshare blob 데이터를 필요한 경우에 중요 한 toodo 계정 액세스 키의 hello 보안을 유지 하면서 너무 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="119a1-179">또한 보안 hello 유선으로 및 Azure 저장소에 이동 하는 blob 데이터 tooensure를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="119a1-180">Tooblob 데이터 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-180">Controlling access tooblob data</span></span>
<span data-ttu-id="119a1-181">기본적으로 hello blob 데이터 저장소 계정에 액세스할 수 있는 유일한 toostorage 계정 소유자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="119a1-182">기본적으로 hello 계정 액세스 키를 필요 Blob 저장소에 대 한 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="119a1-183">그러나 toomake 수도 특정 blob 데이터 tooother 사용할 수 있는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="119a1-184">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-184">You have two options:</span></span>

* <span data-ttu-id="119a1-185">**익명 액세스:** 컨테이너나 Blob를 공개 제공하여 익명 액세스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="119a1-186">참조 [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="119a1-187">**공유 액세스 서명:** 지정 하는 권한으로 및 지정 된 간격으로 저장소 계정의 위임 된 액세스 tooa 리소스를 제공 하는 공유 액세스 서명 (SAS)으로 클라이언트를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="119a1-188">자세한 내용은 [SAS(공유 액세스 서명) 사용](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="119a1-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="119a1-189">Blob 데이터 암호화 </span><span class="sxs-lookup"><span data-stu-id="119a1-189">Encrypting blob data</span></span>
<span data-ttu-id="119a1-190">Azure 저장소 blob 데이터 hello 클라이언트와 서버 hello에 암호화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="119a1-191">**클라이언트 쪽 암호화:** .NET tooAzure 저장소에 업로드 하 고 toohello 클라이언트를 다운로드 하는 동안 데이터를 해독 하기 전에 클라이언트 응용 프로그램 내에서 데이터를 암호화 지원에 대 한 저장소 클라이언트 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="119a1-192">hello 라이브러리는 또한 저장소 계정 키 관리에 대 한 Azure 키 자격 증명 모음 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="119a1-193">자세한 내용은 [Microsoft Azure 저장소용 .NET을 사용하는 클라이언트 쪽 암호화](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="119a1-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="119a1-194">또한 [자습서: Microsoft Azure 저장소에서 Azure 주요 자격 증명 모음을 사용하여 Blob 암호화 및 해독](storage-encrypt-decrypt-blobs-key-vault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="119a1-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="119a1-195">**서버 쪽 암호화**: 이제 Azure 저장소에서는 서버 쪽 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="119a1-196">[미사용 데이터에 대한 Azure 저장소 서비스 암호화(미리 보기)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="119a1-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="119a1-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="119a1-197">Next steps</span></span>
<span data-ttu-id="119a1-198">Blob 저장소의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="119a1-199">Microsoft Azure 저장소 탐색기</span><span class="sxs-lookup"><span data-stu-id="119a1-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="119a1-200">[Microsoft Azure 저장소 탐색기 (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="119a1-201">Blob 저장소 샘플</span><span class="sxs-lookup"><span data-stu-id="119a1-201">Blob storage samples</span></span>
* [<span data-ttu-id="119a1-202">.NET에서 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="119a1-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="119a1-203">Blob 저장소 참조</span><span class="sxs-lookup"><span data-stu-id="119a1-203">Blob storage reference</span></span>
* [<span data-ttu-id="119a1-204">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="119a1-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="119a1-205">REST API 참조</span><span class="sxs-lookup"><span data-stu-id="119a1-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="119a1-206">개념적 지침</span><span class="sxs-lookup"><span data-stu-id="119a1-206">Conceptual guides</span></span>
* [<span data-ttu-id="119a1-207">Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="119a1-207">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="119a1-208">.NET용 파일 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="119a1-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="119a1-209">Toouse Azure blob 저장소 hello WebJobs SDK로 하는 방법</span><span class="sxs-lookup"><span data-stu-id="119a1-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
