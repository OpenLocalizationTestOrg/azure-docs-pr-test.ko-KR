---
title: "Azure Blob 저장소에서 컨테이너 및 blob에 대 한 aaaEnable 공용 읽기 권한 | Microsoft Docs"
description: "자세한 방법을 toomake 컨테이너 및 blob에 익명 액세스를 사용할 수 있는 방법과 tooaccess에 프로그래밍 방식으로 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="b9310-103">익명 읽기 권한을 toocontainers 및 blob 관리</span><span class="sxs-lookup"><span data-stu-id="b9310-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="b9310-104">익명 공용 읽기 액세스 tooa 컨테이너와 그 blob Azure Blob 저장소에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="b9310-105">이렇게 하면 사용자의 계정 키를 공유 하지 않고 및 공유 액세스 서명 (SAS)를 요구 하지 않고 toothese 리소스 읽기 전용 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="b9310-106">공용 읽기 액세스 권한을 있는 시나리오는 특정 blob tooalways 익명 읽기 액세스용으로 제공 수에 대 한 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="b9310-107">보다 세부적인 제어를 위해 공유 액세스 서명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="b9310-108">공유 액세스 서명을 사용 하면 서로 다른 사용 권한을 사용 하 여 특정 기간에 대 한 제한 된 tooprovide 액세스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="b9310-109">공유 액세스 서명 만들기에 대한 자세한 내용은 [Azure Storage에서 SAS(공유 액세스 서명) 사용](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9310-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="b9310-110">익명 사용자에 게 사용 권한 toocontainers 및 blob를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="b9310-111">기본적으로 컨테이너와 그 안에 모든 blob hello 저장소 계정의 소유자 hello에 의해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="b9310-112">toogive 익명 사용자에 게 읽기 권한이 있으면 tooa 컨테이너와 그 blob hello 컨테이너 권한을 tooallow 공용 액세스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="b9310-113">익명 사용자에 게 hello 요청을 인증 하지 않고 공개적으로 액세스할 수 있는 컨테이너 내 blob를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="b9310-114">다음 권한을 hello로 컨테이너를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="b9310-115">**공용 읽기 권한 없음:** hello 컨테이너와 그 blob 저장소 계정 소유자 hello에 의해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="b9310-116">모든 새 컨테이너에 대 한 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="b9310-117">**공용 읽기 권한 blob에 대해서만:** 익명 요청에 의해 hello 컨테이너 내 Blob를 읽을 수 있지만 컨테이너 데이터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="b9310-118">익명 클라이언트 hello 컨테이너에서 hello blob를 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="b9310-119">**전체 공용 읽기 권한:** 익명 요청을 통해 모든 컨테이너와 Blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="b9310-120">클라이언트가 익명 요청을 하 여 hello 컨테이너 내 blob를 열거할 수 있지만 hello 저장소 계정 내 컨테이너는 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="b9310-121">Hello 다음 tooset 컨테이너 권한을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="b9310-122">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="b9310-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="b9310-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9310-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="b9310-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b9310-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="b9310-125">Hello 저장소 클라이언트 라이브러리 또는 hello REST API 중 하나를 사용 하 여 프로그래밍 방식으로,</span><span class="sxs-lookup"><span data-stu-id="b9310-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="b9310-126">Hello Azure 포털에서에서 컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="b9310-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="b9310-127">hello에 tooset 컨테이너 권한 [Azure 포털](https://portal.azure.com), 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="b9310-128">Open 프로그램 **저장소 계정** 블레이드 hello 포털에서.</span><span class="sxs-lookup"><span data-stu-id="b9310-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="b9310-129">선택 하 여 저장소 계정을 찾을 수 있습니다 **저장소 계정은** hello 주 포털 메뉴 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="b9310-130">아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="b9310-131">Hello 컨테이너 행 이나 선택 hello 줄임표 tooopen hello 컨테이너에서 마우스 오른쪽 단추로 클릭 **상황에 맞는 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="b9310-132">선택 **액세스 정책** hello 상황에 맞는 메뉴에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="b9310-133">선택 된 **액세스 형식** hello에서 드롭다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="b9310-133">Select an **Access type** from hello drop down menu.</span></span>

    ![컨테이너 메타데이터 편집 대화 상자](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="b9310-135">.NET으로 컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="b9310-135">Set container permissions with .NET</span></span>
<span data-ttu-id="b9310-136">.net, C# 및 hello 저장소 클라이언트 라이브러리를 사용 하 여 컨테이너에 대 한 사용 권한을 tooset hello를 호출 하 여 hello 컨테이너의 기존 사용 권한을 먼저 검색 **GetPermissions** 메서드.</span><span class="sxs-lookup"><span data-stu-id="b9310-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="b9310-137">그런 다음 세트 hello **PublicAccess** hello에 대 한 속성 **BlobContainerPermissions** hello에서 반환 되는 개체 **GetPermissions** 메서드.</span><span class="sxs-lookup"><span data-stu-id="b9310-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="b9310-138">마지막으로 hello 호출 **SetPermissions** hello로 메서드 사용 권한을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="b9310-139">다음 예제는 hello toofull 공용 읽기 액세스 권한을 hello 컨테이너의 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="b9310-140">blob에만 hello 설정에 대 한 읽기 액세스를 tooset 권한 toopublic **PublicAccess** 속성 너무**BlobContainerPublicAccessType.Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="b9310-141">tooremove 익명 사용자에 대 한 모든 사용 권한이 설정 속성을 너무 hello**BlobContainerPublicAccessType.Off**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="b9310-142">컨테이너 및 Blob에 익명으로 액세스</span><span class="sxs-lookup"><span data-stu-id="b9310-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="b9310-143">컨테이너 및 Blob에 익명으로 액세스하는 클라이언트는 자격 증명을 필요로 하지 않는 생성자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="b9310-144">다음 예제는 hello 몇 가지 방법을 보여 줍니다 tooreference Blob 서비스 리소스 익명으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="b9310-145">익명 클라이언트 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="b9310-145">Create an anonymous client object</span></span>
<span data-ttu-id="b9310-146">Hello 계정에 대 한 hello Blob 서비스 끝점을 제공 하 여 익명 액세스에 대 한 새 서비스 클라이언트 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="b9310-147">그러나 익명 액세스에 사용할 수 있는 해당 계정에 컨테이너의 hello 이름을 또한 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="b9310-148">컨테이너를 익명으로 참조</span><span class="sxs-lookup"><span data-stu-id="b9310-148">Reference a container anonymously</span></span>
<span data-ttu-id="b9310-149">익명으로 사용할 수 있는 hello URL tooa 컨테이너를 설정한 경우 사용할 수 있습니다 tooreference hello 컨테이너 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="b9310-150">Blob을 익명으로 참조</span><span class="sxs-lookup"><span data-stu-id="b9310-150">Reference a blob anonymously</span></span>
<span data-ttu-id="b9310-151">익명 액세스에 사용할 수 있는 hello URL tooa blob를 설정한 경우 해당 URL을 사용 하 여 직접 hello blob를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="b9310-152">사용 가능한 tooanonymous 사용자 기능</span><span class="sxs-lookup"><span data-stu-id="b9310-152">Features available tooanonymous users</span></span>
<span data-ttu-id="b9310-153">다음 표에서 hello 컨테이너의 ACL tooallow 공용 액세스가 설정 된 경우 익명 사용자가 어떤 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9310-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="b9310-154">REST 작업</span><span class="sxs-lookup"><span data-stu-id="b9310-154">REST Operation</span></span> | <span data-ttu-id="b9310-155">전체 공용 읽기가 가능한 권한</span><span class="sxs-lookup"><span data-stu-id="b9310-155">Permission with full public read access</span></span> | <span data-ttu-id="b9310-156">Blob 전용 공용 읽기가 가능한 권한</span><span class="sxs-lookup"><span data-stu-id="b9310-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9310-157">컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="b9310-157">List Containers</span></span> |<span data-ttu-id="b9310-158">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-158">Owner only</span></span> |<span data-ttu-id="b9310-159">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-159">Owner only</span></span> |
| <span data-ttu-id="b9310-160">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="b9310-160">Create Container</span></span> |<span data-ttu-id="b9310-161">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-161">Owner only</span></span> |<span data-ttu-id="b9310-162">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-162">Owner only</span></span> |
| <span data-ttu-id="b9310-163">컨테이너 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-163">Get Container Properties</span></span> |<span data-ttu-id="b9310-164">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-164">All</span></span> |<span data-ttu-id="b9310-165">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-165">Owner only</span></span> |
| <span data-ttu-id="b9310-166">컨테이너 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-166">Get Container Metadata</span></span> |<span data-ttu-id="b9310-167">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-167">All</span></span> |<span data-ttu-id="b9310-168">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-168">Owner only</span></span> |
| <span data-ttu-id="b9310-169">컨테이너 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="b9310-169">Set Container Metadata</span></span> |<span data-ttu-id="b9310-170">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-170">Owner only</span></span> |<span data-ttu-id="b9310-171">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-171">Owner only</span></span> |
| <span data-ttu-id="b9310-172">컨테이너 ACL 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-172">Get Container ACL</span></span> |<span data-ttu-id="b9310-173">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-173">Owner only</span></span> |<span data-ttu-id="b9310-174">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-174">Owner only</span></span> |
| <span data-ttu-id="b9310-175">컨테이너 ACL 설정</span><span class="sxs-lookup"><span data-stu-id="b9310-175">Set Container ACL</span></span> |<span data-ttu-id="b9310-176">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-176">Owner only</span></span> |<span data-ttu-id="b9310-177">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-177">Owner only</span></span> |
| <span data-ttu-id="b9310-178">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="b9310-178">Delete Container</span></span> |<span data-ttu-id="b9310-179">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-179">Owner only</span></span> |<span data-ttu-id="b9310-180">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-180">Owner only</span></span> |
| <span data-ttu-id="b9310-181">Blob 나열</span><span class="sxs-lookup"><span data-stu-id="b9310-181">List Blobs</span></span> |<span data-ttu-id="b9310-182">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-182">All</span></span> |<span data-ttu-id="b9310-183">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-183">Owner only</span></span> |
| <span data-ttu-id="b9310-184">Blob 배치</span><span class="sxs-lookup"><span data-stu-id="b9310-184">Put Blob</span></span> |<span data-ttu-id="b9310-185">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-185">Owner only</span></span> |<span data-ttu-id="b9310-186">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-186">Owner only</span></span> |
| <span data-ttu-id="b9310-187">Blob 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-187">Get Blob</span></span> |<span data-ttu-id="b9310-188">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-188">All</span></span> |<span data-ttu-id="b9310-189">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-189">All</span></span> |
| <span data-ttu-id="b9310-190">Blob 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-190">Get Blob Properties</span></span> |<span data-ttu-id="b9310-191">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-191">All</span></span> |<span data-ttu-id="b9310-192">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-192">All</span></span> |
| <span data-ttu-id="b9310-193">Blob 속성 설정</span><span class="sxs-lookup"><span data-stu-id="b9310-193">Set Blob Properties</span></span> |<span data-ttu-id="b9310-194">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-194">Owner only</span></span> |<span data-ttu-id="b9310-195">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-195">Owner only</span></span> |
| <span data-ttu-id="b9310-196">Blob 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-196">Get Blob Metadata</span></span> |<span data-ttu-id="b9310-197">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-197">All</span></span> |<span data-ttu-id="b9310-198">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-198">All</span></span> |
| <span data-ttu-id="b9310-199">Blob 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="b9310-199">Set Blob Metadata</span></span> |<span data-ttu-id="b9310-200">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-200">Owner only</span></span> |<span data-ttu-id="b9310-201">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-201">Owner only</span></span> |
| <span data-ttu-id="b9310-202">블록 배치</span><span class="sxs-lookup"><span data-stu-id="b9310-202">Put Block</span></span> |<span data-ttu-id="b9310-203">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-203">Owner only</span></span> |<span data-ttu-id="b9310-204">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-204">Owner only</span></span> |
| <span data-ttu-id="b9310-205">블록 목록 가져오기(커밋된 블록만)</span><span class="sxs-lookup"><span data-stu-id="b9310-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="b9310-206">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-206">All</span></span> |<span data-ttu-id="b9310-207">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-207">All</span></span> |
| <span data-ttu-id="b9310-208">블록 목록 가져오기(커밋되지 않은 블록만 또는 모든 블록)</span><span class="sxs-lookup"><span data-stu-id="b9310-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="b9310-209">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-209">Owner only</span></span> |<span data-ttu-id="b9310-210">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-210">Owner only</span></span> |
| <span data-ttu-id="b9310-211">블록 목록 배치</span><span class="sxs-lookup"><span data-stu-id="b9310-211">Put Block List</span></span> |<span data-ttu-id="b9310-212">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-212">Owner only</span></span> |<span data-ttu-id="b9310-213">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-213">Owner only</span></span> |
| <span data-ttu-id="b9310-214">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="b9310-214">Delete Blob</span></span> |<span data-ttu-id="b9310-215">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-215">Owner only</span></span> |<span data-ttu-id="b9310-216">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-216">Owner only</span></span> |
| <span data-ttu-id="b9310-217">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="b9310-217">Copy Blob</span></span> |<span data-ttu-id="b9310-218">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-218">Owner only</span></span> |<span data-ttu-id="b9310-219">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-219">Owner only</span></span> |
| <span data-ttu-id="b9310-220">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="b9310-220">Snapshot Blob</span></span> |<span data-ttu-id="b9310-221">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-221">Owner only</span></span> |<span data-ttu-id="b9310-222">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-222">Owner only</span></span> |
| <span data-ttu-id="b9310-223">Blob 임대</span><span class="sxs-lookup"><span data-stu-id="b9310-223">Lease Blob</span></span> |<span data-ttu-id="b9310-224">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-224">Owner only</span></span> |<span data-ttu-id="b9310-225">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-225">Owner only</span></span> |
| <span data-ttu-id="b9310-226">페이지 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-226">Put Page</span></span> |<span data-ttu-id="b9310-227">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-227">Owner only</span></span> |<span data-ttu-id="b9310-228">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-228">Owner only</span></span> |
| <span data-ttu-id="b9310-229">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9310-229">Get Page Ranges</span></span> |<span data-ttu-id="b9310-230">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-230">All</span></span> |<span data-ttu-id="b9310-231">모두</span><span class="sxs-lookup"><span data-stu-id="b9310-231">All</span></span> |
| <span data-ttu-id="b9310-232">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="b9310-232">Append Blob</span></span> |<span data-ttu-id="b9310-233">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-233">Owner only</span></span> |<span data-ttu-id="b9310-234">소유자만</span><span class="sxs-lookup"><span data-stu-id="b9310-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9310-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9310-235">Next steps</span></span>

* [<span data-ttu-id="b9310-236">Hello Azure 저장소 서비스에 대 한 인증</span><span class="sxs-lookup"><span data-stu-id="b9310-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="b9310-237">SAS(공유 액세스 서명) 사용</span><span class="sxs-lookup"><span data-stu-id="b9310-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="b9310-238">공유 액세스 서명을 사용하여 액세스 위임</span><span class="sxs-lookup"><span data-stu-id="b9310-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
