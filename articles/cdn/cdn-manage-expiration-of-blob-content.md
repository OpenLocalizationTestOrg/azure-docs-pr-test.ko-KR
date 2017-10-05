---
title: "Azure CDN에서 Azure Storage Blob의 만료 관리 | Microsoft Docs"
description: "Azure CDN 캐싱의 Blob에 대한 TTL(Time-To-Live)을 제어하기 위한 옵션에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="77e0a-103">Azure CDN에서 Azure Storage Blob의 만료 관리</span><span class="sxs-lookup"><span data-stu-id="77e0a-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77e0a-104">Azure Web Apps/Cloud Services, ASP.NET 또는 IIS</span><span class="sxs-lookup"><span data-stu-id="77e0a-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="77e0a-105">Azure Storage Blob service</span><span class="sxs-lookup"><span data-stu-id="77e0a-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="77e0a-106">[Azure Storage](../storage/common/storage-introduction.md#blob-storage)에서 [Blob 서비스](../storage/common/storage-introduction.md)는 Azure CDN과 통합된 여러 Azure 기반 원본 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="77e0a-107">TTL(time-to-live)이 경과할 때까지 공개적으로 액세스 가능한 모든 Blob 콘텐츠는 Azure CDN에 캐시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="77e0a-108">TTL은 Azure Storage의 HTTP 응답에 있는 [*캐시 제어* 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) 에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="77e0a-109">Blob에 TTL을 설정하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="77e0a-110">이 경우에 Azure CDN은 기본 TTL인 7일을 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="77e0a-111">Blob 및 다른 파일에 대한 액세스 속도를 가속하기 위해 Azure CDN이 작동하는 방법에 대한 자세한 내용은 [Azure CDN 개요](cdn-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77e0a-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="77e0a-112">Azure Storage Blob 서비스에 대한 자세한 내용은 [Blob 서비스 개념](https://msdn.microsoft.com/library/dd179376.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77e0a-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="77e0a-113">이 자습서에서는 Azure Storage에서 Blob에 TTL을 설정할 수 있는 여러 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="77e0a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77e0a-114">Azure PowerShell</span></span>
<span data-ttu-id="77e0a-115">[Azure PowerShell](/powershell/azure/overview) 은 Azure 서비스를 관리하는 가장 강력하고 빠른 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="77e0a-116">`Get-AzureStorageBlob` cmdlet을 사용하여 Blob에 대한 참조를 가져온 다음 `.ICloudBlob.Properties.CacheControl` 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="77e0a-117">PowerShell을 사용하여 [CDN 프로필 및 끝점을 관리](cdn-manage-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="77e0a-118">.NET용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="77e0a-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="77e0a-119">.NET을 사용하여 Blob의 TTL을 설정하려면 [.NET용 Azure Storage 클라이언트 라이브러리](../storage/blobs/storage-dotnet-how-to-use-blobs.md)를 사용하여 [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="77e0a-120">[.NET용 Azure Blob 저장소 샘플](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)에서 사용할 수 있는 추가 .NET 코드 샘플이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="77e0a-121">다른 방법</span><span class="sxs-lookup"><span data-stu-id="77e0a-121">Other methods</span></span>
* [<span data-ttu-id="77e0a-122">Azure 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="77e0a-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="77e0a-123">Blob을 업로드하는 경우 `-p` 전환을 사용하여 *cacheControl* 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="77e0a-124">이 예제에서는 TTL을 1시간(3600초)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="77e0a-125">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="77e0a-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="77e0a-126">[Blob 배치](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [블록 목록 배치](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx) 또는 [Blob 속성 설정](https://msdn.microsoft.com/library/azure/ee691966.aspx) 요청에 *x-ms-blob-cache-control* 속성을 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="77e0a-127">타사 저장소 관리 도구</span><span class="sxs-lookup"><span data-stu-id="77e0a-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="77e0a-128">일부 타사 Azure Storage 관리 도구를 사용하면 Blob에 *CacheControl* 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="77e0a-129">*캐시 제어* 헤더 테스트</span><span class="sxs-lookup"><span data-stu-id="77e0a-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="77e0a-130">Blob의 TTL을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="77e0a-131">브라우저 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)를 사용하여 Blob에 *캐시 제어* 응답 헤더가 포함되어 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="77e0a-132">**wget**, [Postman](https://www.getpostman.com/) 또는 [Fiddler](http://www.telerik.com/fiddler)와 같은 도구를 사용하여 응답 헤더를 검사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77e0a-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77e0a-133">Next Steps</span></span>
* [<span data-ttu-id="77e0a-134">*캐시 제어* 헤더에 대해 참고하기</span><span class="sxs-lookup"><span data-stu-id="77e0a-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="77e0a-135">Azure CDN에서 클라우드 서비스 콘텐츠의 만료를 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="77e0a-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

