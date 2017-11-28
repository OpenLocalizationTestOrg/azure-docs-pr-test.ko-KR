---
title: "컨테이너 및 Azure Blob Storage의 Blob에 대한 공용 읽기 권한을 사용하도록 설정 | Microsoft Docs"
description: "컨테이너와 Blob에서 익명 액세스를 사용하도록 설정하는 방법 및 프로그래밍 방식으로 액세스하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8d4f4c7c208baf0db6155eb78a53e37c4ec1e023
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="4e00c-103">컨테이너 및 Blob에 대한 익명 읽기 권한 관리</span><span class="sxs-lookup"><span data-stu-id="4e00c-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="4e00c-104">컨테이너 및 Azure Blob Storage의 해당 Blob에 대한 익명의 공용 읽기 권한을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="4e00c-105">이렇게 하면 계정 키를 공유하지 않고 공유 액세스 서명(SAS)을 요구하지 않고도 이러한 리소스에 대해 읽기 전용 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="4e00c-106">공용 읽기 권한은 특정 Blob을 항상 익명 읽기 권한에 사용할 수 있게 하려는 경우에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="4e00c-107">보다 세부적인 제어를 위해 공유 액세스 서명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="4e00c-108">공유 액세스 서명을 사용하면 특정 기간 동안 다양한 권한을 사용하여 제한된 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="4e00c-109">공유 액세스 서명 만들기에 대한 자세한 내용은 [Azure Storage에서 SAS(공유 액세스 서명) 사용](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e00c-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="4e00c-110">컨테이너 및 Blob에 익명의 사용자 권한 부여</span><span class="sxs-lookup"><span data-stu-id="4e00c-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="4e00c-111">기본적으로는 저장소 계정 소유자만 컨테이너 및 해당 컨테이너 내의 모든 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="4e00c-112">익명 사용자에게 컨테이너와 해당 Blob에 대한 읽기 권한을 제공하려면 공용 액세스를 허용하도록 컨테이너 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="4e00c-113">그러면 익명 사용자가 요청을 인증하지 않고도 공개적으로 액세스 가능한 컨테이너 내의 Blob을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="4e00c-114">다음 권한으로 컨테이너를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="4e00c-115">**공용 읽기 액세스 권한 없음:** 저장소 계정 소유자만 컨테이너 및 해당 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="4e00c-116">이것이 새로운 모든 컨테이너에 대한 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="4e00c-117">**Blob 전용 공용 읽기 권한:** 이 컨테이너 내의 Blob은 익명 요청을 통해 읽을 수 있지만 컨테이너 데이터는 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="4e00c-118">익명 클라이언트는 컨테이너 내의 Blob을 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="4e00c-119">**전체 공용 읽기 권한:** 익명 요청을 통해 모든 컨테이너와 Blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="4e00c-120">클라이언트는 익명 요청을 통해 컨테이너 내에서 Blob을 열거할 수 있지만 저장소 계정 내에서 컨테이너를 열거할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="4e00c-121">다음을 사용하여 컨테이너 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="4e00c-122">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4e00c-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="4e00c-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e00c-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="4e00c-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e00c-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="4e00c-125">프로그래밍 방식으로, 저장소 클라이언트 라이브러리 중 하나 또는 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="4e00c-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="4e00c-126">Azure Portal에서 컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="4e00c-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="4e00c-127">[Azure Portal](https://portal.azure.com)에서 컨테이너 권한을 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="4e00c-128">포털에서 **저장소 계정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="4e00c-129">주 포털 메뉴 블레이드에서 **저장소 계정**을 선택하여 저장소 계정을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="4e00c-130">메뉴 블레이드의 **Blob service**에서 **컨테이너**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="4e00c-131">컨테이너 행을 마우스 오른쪽 단추로 클릭하거나 줄임표를 선택하여 컨테이너의 **상황에 맞는 메뉴**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="4e00c-132">상황에 맞는 메뉴에서 **액세스 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="4e00c-133">드롭다운 메뉴에서 **액세스 형식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-133">Select an **Access type** from the drop down menu.</span></span>

    ![컨테이너 메타데이터 편집 대화 상자](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="4e00c-135">.NET으로 컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="4e00c-135">Set container permissions with .NET</span></span>
<span data-ttu-id="4e00c-136">C# 및 .NET용 저장소 클라이언트 라이브러리를 사용하여 컨테이너에 대한 권한을 설정하려면 먼저 **GetPermissions** 메서드를 호출하여 컨테이너의 기존 권한을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="4e00c-137">그런 다음 **GetPermissions** 메서드에 의해 반환된 **BlobContainerPermissions** 개체에 대해 **PublicAccess** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="4e00c-138">마지막으로 업데이트된 권한으로 **SetPermissions** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="4e00c-139">다음 예제에서는 컨테이너의 권한을 전체 공용 읽기 권한으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="4e00c-140">권한을 Blob에 대해서만 공용 읽기 권한으로 설정하려면 **PublicAccess** 속성을 **BlobContainerPublicAccessType.Blob**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="4e00c-141">익명 사용자에 대한 모든 권한을 제거하려면 속성을 **BlobContainerPublicAccessType.Off**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="4e00c-142">컨테이너 및 Blob에 익명으로 액세스</span><span class="sxs-lookup"><span data-stu-id="4e00c-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="4e00c-143">컨테이너 및 Blob에 익명으로 액세스하는 클라이언트는 자격 증명을 필요로 하지 않는 생성자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="4e00c-144">다음 예제에서는 Blob 서비스 리소스를 익명으로 참조하는 약간 다른 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="4e00c-145">익명 클라이언트 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="4e00c-145">Create an anonymous client object</span></span>
<span data-ttu-id="4e00c-146">계정에 Blob 서비스 끝점을 제공하여 익명 액세스에 대한 새 서비스 클라이언트 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="4e00c-147">그러나 익명 액세스에 사용할 수 있는 해당 계정의 컨테이너 이름도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="4e00c-148">컨테이너를 익명으로 참조</span><span class="sxs-lookup"><span data-stu-id="4e00c-148">Reference a container anonymously</span></span>
<span data-ttu-id="4e00c-149">익명으로 사용할 수 있는 컨테이너에 대한 URL이 있는 경우 해당 URL을 사용하여 컨테이너를 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="4e00c-150">Blob을 익명으로 참조</span><span class="sxs-lookup"><span data-stu-id="4e00c-150">Reference a blob anonymously</span></span>
<span data-ttu-id="4e00c-151">익명 액세스에 사용할 수 있는 Blob에 대한 URL이 있는 경우 해당 URL을 사용하여 Blob을 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="4e00c-152">익명 사용자에게 제공되는 기능</span><span class="sxs-lookup"><span data-stu-id="4e00c-152">Features available to anonymous users</span></span>
<span data-ttu-id="4e00c-153">아래 표에는 컨테이너 ACL이 공용 액세스를 허용하도록 설정되어 있을 때 익명 사용자가 호출할 수 있는 작업이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e00c-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="4e00c-154">REST 작업</span><span class="sxs-lookup"><span data-stu-id="4e00c-154">REST Operation</span></span> | <span data-ttu-id="4e00c-155">전체 공용 읽기가 가능한 권한</span><span class="sxs-lookup"><span data-stu-id="4e00c-155">Permission with full public read access</span></span> | <span data-ttu-id="4e00c-156">Blob 전용 공용 읽기가 가능한 권한</span><span class="sxs-lookup"><span data-stu-id="4e00c-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e00c-157">컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="4e00c-157">List Containers</span></span> |<span data-ttu-id="4e00c-158">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-158">Owner only</span></span> |<span data-ttu-id="4e00c-159">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-159">Owner only</span></span> |
| <span data-ttu-id="4e00c-160">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="4e00c-160">Create Container</span></span> |<span data-ttu-id="4e00c-161">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-161">Owner only</span></span> |<span data-ttu-id="4e00c-162">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-162">Owner only</span></span> |
| <span data-ttu-id="4e00c-163">컨테이너 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-163">Get Container Properties</span></span> |<span data-ttu-id="4e00c-164">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-164">All</span></span> |<span data-ttu-id="4e00c-165">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-165">Owner only</span></span> |
| <span data-ttu-id="4e00c-166">컨테이너 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-166">Get Container Metadata</span></span> |<span data-ttu-id="4e00c-167">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-167">All</span></span> |<span data-ttu-id="4e00c-168">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-168">Owner only</span></span> |
| <span data-ttu-id="4e00c-169">컨테이너 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="4e00c-169">Set Container Metadata</span></span> |<span data-ttu-id="4e00c-170">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-170">Owner only</span></span> |<span data-ttu-id="4e00c-171">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-171">Owner only</span></span> |
| <span data-ttu-id="4e00c-172">컨테이너 ACL 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-172">Get Container ACL</span></span> |<span data-ttu-id="4e00c-173">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-173">Owner only</span></span> |<span data-ttu-id="4e00c-174">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-174">Owner only</span></span> |
| <span data-ttu-id="4e00c-175">컨테이너 ACL 설정</span><span class="sxs-lookup"><span data-stu-id="4e00c-175">Set Container ACL</span></span> |<span data-ttu-id="4e00c-176">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-176">Owner only</span></span> |<span data-ttu-id="4e00c-177">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-177">Owner only</span></span> |
| <span data-ttu-id="4e00c-178">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="4e00c-178">Delete Container</span></span> |<span data-ttu-id="4e00c-179">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-179">Owner only</span></span> |<span data-ttu-id="4e00c-180">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-180">Owner only</span></span> |
| <span data-ttu-id="4e00c-181">Blob 나열</span><span class="sxs-lookup"><span data-stu-id="4e00c-181">List Blobs</span></span> |<span data-ttu-id="4e00c-182">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-182">All</span></span> |<span data-ttu-id="4e00c-183">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-183">Owner only</span></span> |
| <span data-ttu-id="4e00c-184">Blob 배치</span><span class="sxs-lookup"><span data-stu-id="4e00c-184">Put Blob</span></span> |<span data-ttu-id="4e00c-185">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-185">Owner only</span></span> |<span data-ttu-id="4e00c-186">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-186">Owner only</span></span> |
| <span data-ttu-id="4e00c-187">Blob 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-187">Get Blob</span></span> |<span data-ttu-id="4e00c-188">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-188">All</span></span> |<span data-ttu-id="4e00c-189">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-189">All</span></span> |
| <span data-ttu-id="4e00c-190">Blob 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-190">Get Blob Properties</span></span> |<span data-ttu-id="4e00c-191">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-191">All</span></span> |<span data-ttu-id="4e00c-192">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-192">All</span></span> |
| <span data-ttu-id="4e00c-193">Blob 속성 설정</span><span class="sxs-lookup"><span data-stu-id="4e00c-193">Set Blob Properties</span></span> |<span data-ttu-id="4e00c-194">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-194">Owner only</span></span> |<span data-ttu-id="4e00c-195">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-195">Owner only</span></span> |
| <span data-ttu-id="4e00c-196">Blob 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-196">Get Blob Metadata</span></span> |<span data-ttu-id="4e00c-197">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-197">All</span></span> |<span data-ttu-id="4e00c-198">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-198">All</span></span> |
| <span data-ttu-id="4e00c-199">Blob 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="4e00c-199">Set Blob Metadata</span></span> |<span data-ttu-id="4e00c-200">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-200">Owner only</span></span> |<span data-ttu-id="4e00c-201">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-201">Owner only</span></span> |
| <span data-ttu-id="4e00c-202">블록 배치</span><span class="sxs-lookup"><span data-stu-id="4e00c-202">Put Block</span></span> |<span data-ttu-id="4e00c-203">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-203">Owner only</span></span> |<span data-ttu-id="4e00c-204">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-204">Owner only</span></span> |
| <span data-ttu-id="4e00c-205">블록 목록 가져오기(커밋된 블록만)</span><span class="sxs-lookup"><span data-stu-id="4e00c-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="4e00c-206">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-206">All</span></span> |<span data-ttu-id="4e00c-207">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-207">All</span></span> |
| <span data-ttu-id="4e00c-208">블록 목록 가져오기(커밋되지 않은 블록만 또는 모든 블록)</span><span class="sxs-lookup"><span data-stu-id="4e00c-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="4e00c-209">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-209">Owner only</span></span> |<span data-ttu-id="4e00c-210">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-210">Owner only</span></span> |
| <span data-ttu-id="4e00c-211">블록 목록 배치</span><span class="sxs-lookup"><span data-stu-id="4e00c-211">Put Block List</span></span> |<span data-ttu-id="4e00c-212">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-212">Owner only</span></span> |<span data-ttu-id="4e00c-213">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-213">Owner only</span></span> |
| <span data-ttu-id="4e00c-214">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="4e00c-214">Delete Blob</span></span> |<span data-ttu-id="4e00c-215">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-215">Owner only</span></span> |<span data-ttu-id="4e00c-216">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-216">Owner only</span></span> |
| <span data-ttu-id="4e00c-217">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="4e00c-217">Copy Blob</span></span> |<span data-ttu-id="4e00c-218">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-218">Owner only</span></span> |<span data-ttu-id="4e00c-219">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-219">Owner only</span></span> |
| <span data-ttu-id="4e00c-220">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="4e00c-220">Snapshot Blob</span></span> |<span data-ttu-id="4e00c-221">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-221">Owner only</span></span> |<span data-ttu-id="4e00c-222">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-222">Owner only</span></span> |
| <span data-ttu-id="4e00c-223">Blob 임대</span><span class="sxs-lookup"><span data-stu-id="4e00c-223">Lease Blob</span></span> |<span data-ttu-id="4e00c-224">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-224">Owner only</span></span> |<span data-ttu-id="4e00c-225">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-225">Owner only</span></span> |
| <span data-ttu-id="4e00c-226">페이지 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-226">Put Page</span></span> |<span data-ttu-id="4e00c-227">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-227">Owner only</span></span> |<span data-ttu-id="4e00c-228">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-228">Owner only</span></span> |
| <span data-ttu-id="4e00c-229">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e00c-229">Get Page Ranges</span></span> |<span data-ttu-id="4e00c-230">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-230">All</span></span> |<span data-ttu-id="4e00c-231">모두</span><span class="sxs-lookup"><span data-stu-id="4e00c-231">All</span></span> |
| <span data-ttu-id="4e00c-232">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="4e00c-232">Append Blob</span></span> |<span data-ttu-id="4e00c-233">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-233">Owner only</span></span> |<span data-ttu-id="4e00c-234">소유자만</span><span class="sxs-lookup"><span data-stu-id="4e00c-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e00c-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e00c-235">Next steps</span></span>

* [<span data-ttu-id="4e00c-236">Azure 저장소 서비스에 대한 인증</span><span class="sxs-lookup"><span data-stu-id="4e00c-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="4e00c-237">SAS(공유 액세스 서명) 사용</span><span class="sxs-lookup"><span data-stu-id="4e00c-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="4e00c-238">공유 액세스 서명을 사용하여 액세스 위임</span><span class="sxs-lookup"><span data-stu-id="4e00c-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
