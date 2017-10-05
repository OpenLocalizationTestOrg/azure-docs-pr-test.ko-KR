---
title: ".NET을 사용하여 Azure Blob 저장소(개체 저장소) 시작 | Microsoft Docs"
description: "Azure Blob 저장소(개체 저장소)를 사용하여 클라우드에 구조화되지 않은 데이터를 저장합니다."
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
ms.openlocfilehash: 8393b2dc32f01cac301c713c2ae9f0ab7226ea37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="7d6a0-103">.NET을 사용하여 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="7d6a0-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="7d6a0-104">Azure Blob 저장소는 클라우드에 구조화되지 않은 데이터를 개체/Blob로 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-104">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="7d6a0-105">Blob 저장소는 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램과 같은 모든 종류의 텍스트 또는 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="7d6a0-106">또한 Blob 저장소를 개체 저장소라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-106">Blob storage is also referred to as object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="7d6a0-107">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="7d6a0-107">About this tutorial</span></span>
<span data-ttu-id="7d6a0-108">이 자습서에서는 Azure Blob 저장소를 사용하여 몇 가지 일반적인 시나리오에 대한 .NET 코드를 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-108">This tutorial shows how to write .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="7d6a0-109">Blob 업로드, 나열, 다운로드 및 삭제 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="7d6a0-110">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="7d6a0-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="7d6a0-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d6a0-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="7d6a0-112">.NET용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7d6a0-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="7d6a0-113">.NET용 Azure 구성 관리자</span><span class="sxs-lookup"><span data-stu-id="7d6a0-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="7d6a0-114">[Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="7d6a0-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="7d6a0-115">추가 샘플</span><span class="sxs-lookup"><span data-stu-id="7d6a0-115">More samples</span></span>
<span data-ttu-id="7d6a0-116">Blob 저장소를 사용하는 추가 예제는 [.NET에서 Azure Blob 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="7d6a0-117">GitHub에서 샘플 응용 프로그램을 다운로드하고 실행하거나 코드를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-117">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="7d6a0-118">지시문을 사용하여 추가</span><span class="sxs-lookup"><span data-stu-id="7d6a0-118">Add using directives</span></span>
<span data-ttu-id="7d6a0-119">다음 **using** 지시문을 `Program.cs` 파일 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-119">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="7d6a0-120">연결 문자열 구문 분석</span><span class="sxs-lookup"><span data-stu-id="7d6a0-120">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a><span data-ttu-id="7d6a0-121">Blob 서비스 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="7d6a0-121">Create the Blob service client</span></span>
<span data-ttu-id="7d6a0-122">**CloudBlobClient** 클래스를 통해 Blob 저장소에 저장된 컨테이너 및 Blob을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-122">The **CloudBlobClient** class enables you to retrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="7d6a0-123">서비스 클라이언트를 만드는 한 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-123">Here's one way to create the service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="7d6a0-124">이제 데이터를 읽어 오고 Blob 저장소에 데이터를 기록하는 코드를 작성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-124">Now you are ready to write code that reads data from and writes data to Blob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="7d6a0-125">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="7d6a0-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="7d6a0-126">이 예제에서는 컨테이너가 없는 경우 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-126">This example shows how to create a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="7d6a0-127">기본적으로 새 컨테이너는 전용입니다. 즉, 이 컨테이너에서 Blob을 다운로드하려면 저장소 액세스 키를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-127">By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="7d6a0-128">컨테이너 내의 파일을 모든 사용자가 사용할 수 있게 하려는 경우 다음 코드를 사용하여 컨테이너를 공용으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-128">If you want to make the files within the container available to everyone, you can set the container to be public using the following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="7d6a0-129">인터넷상의 누구든지 공용 컨테이너의 Blob을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-129">Anyone on the Internet can see blobs in a public container.</span></span> <span data-ttu-id="7d6a0-130">하지만 적절한 계정 선택키 또는 공유 액세스 서명이 있는 경우에만 수정하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-130">However, you can modify or delete them only if you have the appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="7d6a0-131">컨테이너에 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="7d6a0-131">Upload a blob into a container</span></span>
<span data-ttu-id="7d6a0-132">Azure Blob 저장소는 블록 Blob 및 페이지 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="7d6a0-133">대부분의 경우에는 블록 Blob을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-133">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="7d6a0-134">블록 Blob에 파일을 업로드하려면 컨테이너 참조를 가져온 다음 이 참조를 사용하여 블록 Blob 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-134">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="7d6a0-135">Blob 참조가 있는 경우 **UploadFromStream** 메서드를 호출하여 데이터 스트림을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-135">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="7d6a0-136">이 작업은 Blob이 없는 경우 새로 만들고, Blob이 있는 경우 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-136">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="7d6a0-137">다음 예제에서는 컨테이너에 Blob을 업로드하는 방법을 보여 주며, 컨테이너가 이미 만들어져 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-137">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite the "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="7d6a0-138">컨테이너의 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="7d6a0-138">List the blobs in a container</span></span>
<span data-ttu-id="7d6a0-139">컨테이너의 Blob을 나열하려면 먼저 컨테이너 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-139">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="7d6a0-140">컨테이너의 **ListBlobs** 메서드를 사용하여 컨테이너 내의 Blob 및/또는 디렉터리를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-140">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="7d6a0-141">반환된 **IListBlobItem**에 대한 풍부한 속성 및 메서드 집합에 액세스하려면 **CloudBlockBlob**, **CloudPageBlob** 또는 **CloudBlobDirectory** 개체로 캐스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-141">To access the  rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="7d6a0-142">형식을 알 수 없는 경우 형식 검사를 사용하여 캐스트할 형식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-142">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="7d6a0-143">다음 코드에서는 _photos_ 컨테이너에 있는 각 항목의 URI를 검색하고 출력하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-143">The following code demonstrates how to retrieve and output the URI of each item in the _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within the container and output the length and URI.
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

<span data-ttu-id="7d6a0-144">Blob 이름에서 경로 정보를 포함하여 기존 파일 시스템과 같이 구성하고 트래버스할 수 있는 가상 디렉터리 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="7d6a0-145">디렉터리 구조는 가상만 해당됩니다. 컨테이너 및 Blob만이 Blob Storage에서 사용할 수 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-145">The directory structure is virtual only--the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="7d6a0-146">하지만 저장소 클라이언트 라이브러리는 **CloudBlobDirectory** 개체를 제공하여 가상 디렉터리를 참조하며 이렇게 함으로써 구성된 Blob으로 작업하는 과정을 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-146">However, the storage client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="7d6a0-147">예를 들어 *photos*라는 컨테이너에 있는 다음 블록 Blob 집합을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-147">For example, consider the following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="7d6a0-148">이전 코드 조각과 같이 *photos* 컨테이너에서 **ListBlobs**를 호출하면 계층적 목록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-148">When you call **ListBlobs** on the *photos* container (as in the preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="7d6a0-149">컨테이너에서 각각 디렉터리와 Blob을 나타내는 **CloudBlobDirectory** 및 **CloudBlockBlob** 개체가 모두 이 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing the directories and blobs in the container, respectively.</span></span> <span data-ttu-id="7d6a0-150">결과 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-150">The resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="7d6a0-151">선택적으로 **ListBlobs** 메서드의 **UseFlatBlobListing** 매개 변수를 **true**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-151">Optionally, you can set the **UseFlatBlobListing** parameter of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="7d6a0-152">이 경우에 컨테이너의 모든 Blob은 **CloudBlockBlob** 개체로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-152">In this case, every blob in the container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="7d6a0-153">플랫 목록을 반환하는 **ListBlobs** 에 대한 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-153">The call to **ListBlobs** to return a flat listing looks like this:</span></span>

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="7d6a0-154">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-154">and the results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="7d6a0-155">Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="7d6a0-155">Download blobs</span></span>
<span data-ttu-id="7d6a0-156">Blob을 다운로드하려면 먼저 Blob 참조를 검색한 다음 **DownloadToStream** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-156">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="7d6a0-157">다음 예제에서는 **DownloadToStream** 메서드를 사용하여 Blob 콘텐츠를 스트림 개체로 전송한 다음 이 개체를 로컬 파일에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-157">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents to a file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="7d6a0-158">**DownloadToStream** 메서드를 사용하여 Blob 콘텐츠를 텍스트 문자열로 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-158">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="7d6a0-159">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="7d6a0-159">Delete blobs</span></span>
<span data-ttu-id="7d6a0-160">Blob을 삭제하려면 먼저 Blob 참조를 가져온 다음 **Delete** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-160">To delete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete the blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="7d6a0-161">여러 페이지에서 비동기식으로 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="7d6a0-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="7d6a0-162">많은 수의 Blob을 나열하거나 한 번의 나열 작업에서 반환되는 결과 수를 제어하려는 경우에는 여러 결과 페이지에 Blob을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-162">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="7d6a0-163">이 예제에서는 여러 페이지에서 비동기식으로 결과를 반환하는 방법을 보여 주므로 큰 결과 집합이 반환되도록 기다리는 동안 실행이 차단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-163">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="7d6a0-164">이 예제에서는 플랫 Blob 나열을 보여 주지만 **ListBlobsSegmentedAsync** 메서드의 _useFlatBlobListing_ 매개 변수를 _false_로 설정하여 계층적 나열을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the _useFlatBlobListing_ parameter of the **ListBlobsSegmentedAsync** method to _false_.</span></span>

<span data-ttu-id="7d6a0-165">샘플 메서드는 비동기 메서드를 호출하므로 앞에 _async_ 키워드를 추가해야 하며 **Task** 개체를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-165">Because the sample method calls an asynchronous method, it must be prefaced with the _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="7d6a0-166">**ListBlobsSegmentedAsync** 메서드에 대해 지정된 await 키워드는 나열 작업이 완료될 때까지 샘플 메서드의 실행을 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-166">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs to the console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get the continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="7d6a0-167">추가 Blob에 쓰기</span><span class="sxs-lookup"><span data-stu-id="7d6a0-167">Writing to an append blob</span></span>
<span data-ttu-id="7d6a0-168">추가 Blob은 로깅 등의 추가 작업에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="7d6a0-169">블록 Blob과 마찬가지로 추가 Blob은 블록으로 구성되지만 추가 Blob에 새 블록을 추가할 때 항상 Blob 끝에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="7d6a0-170">추가 Blob의 기존 블록을 업데이트하거나 삭제할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="7d6a0-171">블록 Blob과 달리 추가 Blob의 블록 ID는 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-171">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="7d6a0-172">추가 Blob의 각 블록은 최대 4MB까지 다양한 크기일 수 있으며, 추가 Blob 하나에 최대 50,000개의 블록이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-172">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="7d6a0-173">따라서 추가 Blob의 최대 크기는 195GB(4MB X 50,000개 블록)보다 약간 더 큽니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-173">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="7d6a0-174">아래 예제에서는 새 추가 Blob을 만들고 간단한 로깅 작업을 시뮬레이트하여 일부 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-174">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```csharp
//Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create the container if it does not already exist.
container.CreateIfNotExists();

//Get a reference to an append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create the append blob. Note that if the blob already exists, the CreateOrReplace() method will overwrite it.
//You can check whether the blob exists to avoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data to the end of the append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read the append blob to the console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="7d6a0-175">세 가지 Blob 유형의 차이점에 대한 자세한 내용은 [블록 Blob, 페이지 Blob 및 추가 Blob 이해](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about the differences between the three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="7d6a0-176">Blob 보안 관리</span><span class="sxs-lookup"><span data-stu-id="7d6a0-176">Managing security for blobs</span></span>
<span data-ttu-id="7d6a0-177">기본적으로 Azure 저장소는 데이터 액세스를 계정 액세스 키를 보유한 계정 소유자로 제한하여 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-177">By default, Azure Storage keeps your data secure by limiting access to the account owner, who is in possession of the account access keys.</span></span> <span data-ttu-id="7d6a0-178">저장소 계정의 Blob 데이터를 공유해야 할 경우 계정 액세스 키의 보안을 손상시키지 않고 공유하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-178">When you need to share blob data in your storage account, it is important to do so without compromising the security of your account access keys.</span></span> <span data-ttu-id="7d6a0-179">또한 Blob 데이터를 암호화하여 유선 및 Azure 저장소에서 데이터가 안전하게 이동하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-179">Additionally, you can encrypt blob data to ensure that it is secure going over the wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a><span data-ttu-id="7d6a0-180">Blob 데이터에 대한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="7d6a0-180">Controlling access to blob data</span></span>
<span data-ttu-id="7d6a0-181">기본적으로 저장소 계정의 Blob 데이터는 저장소 계정 소유자만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-181">By default, the blob data in your storage account is accessible only to storage account owner.</span></span> <span data-ttu-id="7d6a0-182">기본적으로 Blob 저장소에 대한 요청을 인증할 때는 계정 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-182">Authenticating requests against Blob storage requires the account access key by default.</span></span> <span data-ttu-id="7d6a0-183">그러나 다른 사용자에게 특정 Blob 데이터를 사용 가능하게 제공하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-183">However, you may wish to make certain blob data available to other users.</span></span> <span data-ttu-id="7d6a0-184">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-184">You have two options:</span></span>

* <span data-ttu-id="7d6a0-185">**익명 액세스:** 컨테이너나 Blob를 공개 제공하여 익명 액세스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="7d6a0-186">자세한 내용은 [컨테이너 및 Blob에 대한 익명읽기 권한 관리](storage-manage-access-to-resources.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-186">See [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="7d6a0-187">**공유 액세스 서명:** 공유 액세스 서명(SAS)을 클라이언트에 제공할 수 있습니다. 여기서는 저장소 계정의 리소스에 대해 사용자가 지정한 권한과 간격으로 위임된 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access to a resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="7d6a0-188">자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="7d6a0-189">Blob 데이터 암호화 </span><span class="sxs-lookup"><span data-stu-id="7d6a0-189">Encrypting blob data</span></span>
<span data-ttu-id="7d6a0-190">Azure 저장소는 클라이언트와 서버 모두에서 Blob 데이터를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-190">Azure Storage supports encrypting blob data both at the client and on the server:</span></span>

* <span data-ttu-id="7d6a0-191">**클라이언트 쪽 암호화:** NET용 Azure 저장소 클라이언트 라이브러리는 Azure 저장소에 업로드하기 전에 클라이언트 응용 프로그램 내부에서 데이터를 암호화하고 클라이언트로 다운로드하는 동안 데이터 암호를 해독하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-191">**Client-side encryption:** The Storage Client Library for .NET supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="7d6a0-192">라이브러리 또한 저장소 계정 키 관리를 위해 Azure 키 자격 증명 모음과의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-192">The library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="7d6a0-193">자세한 내용은 [Microsoft Azure 저장소용 .NET을 사용하는 클라이언트 쪽 암호화](storage-client-side-encryption.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="7d6a0-194">또한 [자습서: Microsoft Azure 저장소에서 Azure 주요 자격 증명 모음을 사용하여 Blob 암호화 및 해독](storage-encrypt-decrypt-blobs-key-vault.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="7d6a0-195">**서버 쪽 암호화**: 이제 Azure 저장소에서는 서버 쪽 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="7d6a0-196">[미사용 데이터에 대한 Azure 저장소 서비스 암호화(미리 보기)](storage-service-encryption.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d6a0-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d6a0-197">Next steps</span></span>
<span data-ttu-id="7d6a0-198">이제 Blob 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-198">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="7d6a0-199">Microsoft Azure 저장소 탐색기</span><span class="sxs-lookup"><span data-stu-id="7d6a0-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="7d6a0-200">[Microsoft Azure Storage 탐색기(MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md)는 Windows, MacOS 및 Linux에서 Azure Storage 데이터로 시각적으로 작업할 수 있도록 해주는 Microsoft의 독립 실행형 무료 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="7d6a0-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="7d6a0-201">Blob 저장소 샘플</span><span class="sxs-lookup"><span data-stu-id="7d6a0-201">Blob storage samples</span></span>
* [<span data-ttu-id="7d6a0-202">.NET에서 Azure Blob 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="7d6a0-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="7d6a0-203">Blob 저장소 참조</span><span class="sxs-lookup"><span data-stu-id="7d6a0-203">Blob storage reference</span></span>
* [<span data-ttu-id="7d6a0-204">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="7d6a0-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="7d6a0-205">REST API 참조</span><span class="sxs-lookup"><span data-stu-id="7d6a0-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="7d6a0-206">개념적 지침</span><span class="sxs-lookup"><span data-stu-id="7d6a0-206">Conceptual guides</span></span>
* [<span data-ttu-id="7d6a0-207">AzCopy 명령줄 유틸리티로 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="7d6a0-207">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="7d6a0-208">.NET용 파일 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="7d6a0-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="7d6a0-209">WebJob SDK를 사용하여 Azure Blob 저장소로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="7d6a0-209">How to use Azure blob storage with the WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
