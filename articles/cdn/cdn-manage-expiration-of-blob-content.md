---
title: "Azure CDN에서 Azure 저장소 blob의 aaaManage 만료 | Microsoft Docs"
description: "Azure CDN에서 캐싱에 blob에 대 한 활성 시간을 제어 하기 위한 hello 옵션에 알아봅니다."
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
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="fca1c-103">Azure CDN에서 Azure Storage Blob의 만료 관리</span><span class="sxs-lookup"><span data-stu-id="fca1c-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fca1c-104">Azure Web Apps/Cloud Services, ASP.NET 또는 IIS</span><span class="sxs-lookup"><span data-stu-id="fca1c-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="fca1c-105">Azure Storage Blob service</span><span class="sxs-lookup"><span data-stu-id="fca1c-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="fca1c-106">hello [blob 서비스](../storage/common/storage-introduction.md#blob-storage) 에 [Azure 저장소](../storage/common/storage-introduction.md) Azure CDN와 통합 되어 여러 Azure 기반 원본 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="fca1c-107">TTL(time-to-live)이 경과할 때까지 공개적으로 액세스 가능한 모든 Blob 콘텐츠는 Azure CDN에 캐시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="fca1c-108">hello TTL 따라 사용자가 hello [ *캐시 제어* 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) HTTP hello에 대 한 Azure 저장소에서 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="fca1c-109">Blob에 없는 TTL tooset를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="fca1c-110">이 경우에 Azure CDN은 기본 TTL인 7일을 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="fca1c-111">Azure CDN 액세스 tooblobs 및 기타 파일을 toospeed 작동 하는 방법에 대 한 자세한 내용은 참조 hello [Azure CDN 개요](cdn-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="fca1c-112">Hello Azure 저장소 blob 서비스에 대 한 자세한 내용은 참조 하십시오. [Blob 서비스 개념](https://msdn.microsoft.com/library/dd179376.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="fca1c-113">이 자습서에서는 Azure 저장소의 blob에 대해 TTL hello를 설정할 수 있는 여러 가지 방법으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="fca1c-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fca1c-114">Azure PowerShell</span></span>
<span data-ttu-id="fca1c-115">[Azure PowerShell](/powershell/azure/overview) Azure 서비스는 hello 가장 빠른 가장 강력한 방법 tooadminister 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="fca1c-116">사용 하 여 hello `Get-AzureStorageBlob` cmdlet tooget 참조 toohello blob에는 다음 hello 설정 `.ICloudBlob.Properties.CacheControl` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="fca1c-117">또한도 사용할 수 있습니다 PowerShell[CDN 프로필 및 끝점 관리](cdn-manage-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="fca1c-118">.NET용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="fca1c-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="fca1c-119">tooset blob의.NET을 사용 하 여 hello를 사용 하 여 TTL [.NET 용 Azure 저장소 클라이언트 라이브러리](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="fca1c-120">Hello에서 사용할 수 있는 추가.NET 코드 샘플은 [.NET 용 Azure Blob 저장소 예제](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="fca1c-121">다른 방법</span><span class="sxs-lookup"><span data-stu-id="fca1c-121">Other methods</span></span>
* [<span data-ttu-id="fca1c-122">Azure 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="fca1c-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="fca1c-123">Hello blob를 업로드할 때 설정 hello *cacheControl* hello를 사용 하 여 속성 `-p` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="fca1c-124">이 예제는 hello TTL tooone 시간 (3600 초)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="fca1c-125">Azure 저장소 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="fca1c-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="fca1c-126">명시적으로 집합 hello *x-ms-blob-캐시 제어* 속성에는 [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [블록 목록 배치](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), 또는 [Blob 속성 설정](https://msdn.microsoft.com/library/azure/ee691966.aspx) 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="fca1c-127">타사 저장소 관리 도구</span><span class="sxs-lookup"><span data-stu-id="fca1c-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="fca1c-128">일부 타사 Azure 저장소 관리 도구는 tooset hello 허용 *CacheControl* blob에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="fca1c-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="fca1c-129">테스트 hello *캐시 제어* 헤더</span><span class="sxs-lookup"><span data-stu-id="fca1c-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="fca1c-130">Blob의 TTL hello를 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="fca1c-131">브라우저의을 사용 하 여 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), blob는 hello 포함 하 여 테스트 *캐시 제어* 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="fca1c-132">와 같은 도구를 사용할 수도 있습니다 **wget**, [우체부](https://www.getpostman.com/), 또는 [Fiddler](http://www.telerik.com/fiddler) tooexamine hello 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="fca1c-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fca1c-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fca1c-133">Next Steps</span></span>
* [<span data-ttu-id="fca1c-134">Hello에 대 한 읽기 *캐시 제어* 헤더</span><span class="sxs-lookup"><span data-stu-id="fca1c-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="fca1c-135">자세한 내용은 방법 toomanage Azure CDN에서 클라우드 서비스 콘텐츠 만료</span><span class="sxs-lookup"><span data-stu-id="fca1c-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

