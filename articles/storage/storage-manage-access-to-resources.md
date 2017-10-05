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
ms.openlocfilehash: c7b83667b58649c156a62fa68cebd854c13e2cba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="51357-103">컨테이너 및 Blob에 대한 익명 읽기 권한 관리</span><span class="sxs-lookup"><span data-stu-id="51357-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="51357-104">컨테이너 및 Azure Blob Storage의 해당 Blob에 대한 익명의 공용 읽기 권한을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="51357-105">이렇게 하면 계정 키를 공유하지 않고 공유 액세스 서명(SAS)을 요구하지 않고도 이러한 리소스에 대해 읽기 전용 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="51357-106">공용 읽기 권한은 특정 Blob을 항상 익명 읽기 권한에 사용할 수 있게 하려는 경우에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="51357-107">보다 세부적인 제어를 위해 공유 액세스 서명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="51357-108">공유 액세스 서명을 사용하면 특정 기간 동안 다양한 권한을 사용하여 제한된 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="51357-109">공유 액세스 서명 만들기에 대한 자세한 내용은 [Azure Storage에서 SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51357-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="51357-110">컨테이너 및 Blob에 익명의 사용자 권한 부여</span><span class="sxs-lookup"><span data-stu-id="51357-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="51357-111">기본적으로는 저장소 계정 소유자만 컨테이너 및 해당 컨테이너 내의 모든 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="51357-112">익명 사용자에게 컨테이너와 해당 Blob에 대한 읽기 권한을 제공하려면 공용 액세스를 허용하도록 컨테이너 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="51357-113">그러면 익명 사용자가 요청을 인증하지 않고도 공개적으로 액세스 가능한 컨테이너 내의 Blob을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="51357-114">다음 권한으로 컨테이너를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="51357-115">**공용 읽기 액세스 권한 없음:** 저장소 계정 소유자만 컨테이너 및 해당 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="51357-116">이것이 새로운 모든 컨테이너에 대한 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="51357-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="51357-117">**Blob 전용 공용 읽기 권한:** 이 컨테이너 내의 Blob은 익명 요청을 통해 읽을 수 있지만 컨테이너 데이터는 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="51357-118">익명 클라이언트는 컨테이너 내의 Blob을 열거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="51357-119">**전체 공용 읽기 권한:** 익명 요청을 통해 모든 컨테이너와 Blob 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="51357-120">클라이언트는 익명 요청을 통해 컨테이너 내에서 Blob을 열거할 수 있지만 저장소 계정 내에서 컨테이너를 열거할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="51357-121">다음을 사용하여 컨테이너 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="51357-122">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="51357-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="51357-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="51357-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="51357-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="51357-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="51357-125">프로그래밍 방식으로, 저장소 클라이언트 라이브러리 중 하나 또는 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="51357-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="51357-126">Azure Portal에서 컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="51357-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="51357-127">[Azure Portal](https://portal.azure.com)에서 컨테이너 권한을 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="51357-128">포털에서 **저장소 계정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="51357-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="51357-129">주 포털 메뉴 블레이드에서 **저장소 계정**을 선택하여 저장소 계정을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="51357-130">메뉴 블레이드의 **Blob service**에서 **컨테이너**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="51357-131">컨테이너 행을 마우스 오른쪽 단추로 클릭하거나 줄임표를 선택하여 컨테이너의 **상황에 맞는 메뉴**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="51357-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="51357-132">상황에 맞는 메뉴에서 **액세스 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="51357-133">드롭다운 메뉴에서 **액세스 형식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-133">Select an **Access type** from the drop down menu.</span></span>

    ![컨테이너 메타데이터 편집 대화 상자](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="51357-135">.NET으로 컨테이너 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="51357-135">Set container permissions with .NET</span></span>
<span data-ttu-id="51357-136">C# 및 .NET용 저장소 클라이언트 라이브러리를 사용하여 컨테이너에 대한 권한을 설정하려면 먼저 **GetPermissions** 메서드를 호출하여 컨테이너의 기존 권한을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="51357-137">그런 다음 **GetPermissions** 메서드에 의해 반환된 **BlobContainerPermissions** 개체에 대해 **PublicAccess** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="51357-138">마지막으로 업데이트된 권한으로 **SetPermissions** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="51357-139">다음 예제에서는 컨테이너의 권한을 전체 공용 읽기 권한으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="51357-140">권한을 Blob에 대해서만 공용 읽기 권한으로 설정하려면 **PublicAccess** 속성을 **BlobContainerPublicAccessType.Blob**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="51357-141">익명 사용자에 대한 모든 권한을 제거하려면 속성을 **BlobContainerPublicAccessType.Off**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="51357-142">컨테이너 및 Blob에 익명으로 액세스</span><span class="sxs-lookup"><span data-stu-id="51357-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="51357-143">컨테이너 및 Blob에 익명으로 액세스하는 클라이언트는 자격 증명을 필요로 하지 않는 생성자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="51357-144">다음 예제에서는 Blob 서비스 리소스를 익명으로 참조하는 약간 다른 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51357-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="51357-145">익명 클라이언트 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="51357-145">Create an anonymous client object</span></span>
<span data-ttu-id="51357-146">계정에 Blob 서비스 끝점을 제공하여 익명 액세스에 대한 새 서비스 클라이언트 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="51357-147">그러나 익명 액세스에 사용할 수 있는 해당 계정의 컨테이너 이름도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51357-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

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

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="51357-148">컨테이너를 익명으로 참조</span><span class="sxs-lookup"><span data-stu-id="51357-148">Reference a container anonymously</span></span>
<span data-ttu-id="51357-149">익명으로 사용할 수 있는 컨테이너에 대한 URL이 있는 경우 해당 URL을 사용하여 컨테이너를 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

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

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="51357-150">Blob을 익명으로 참조</span><span class="sxs-lookup"><span data-stu-id="51357-150">Reference a blob anonymously</span></span>
<span data-ttu-id="51357-151">익명 액세스에 사용할 수 있는 Blob에 대한 URL이 있는 경우 해당 URL을 사용하여 Blob을 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="51357-152">익명 사용자에게 제공되는 기능</span><span class="sxs-lookup"><span data-stu-id="51357-152">Features available to anonymous users</span></span>
<span data-ttu-id="51357-153">아래 표에는 컨테이너 ACL이 공용 액세스를 허용하도록 설정되어 있을 때 익명 사용자가 호출할 수 있는 작업이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51357-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="51357-154">REST 작업</span><span class="sxs-lookup"><span data-stu-id="51357-154">REST Operation</span></span> | <span data-ttu-id="51357-155">전체 공용 읽기가 가능한 권한</span><span class="sxs-lookup"><span data-stu-id="51357-155">Permission with full public read access</span></span> | <span data-ttu-id="51357-156">Blob 전용 공용 읽기가 가능한 권한</span><span class="sxs-lookup"><span data-stu-id="51357-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51357-157">컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="51357-157">List Containers</span></span> |<span data-ttu-id="51357-158">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-158">Owner only</span></span> |<span data-ttu-id="51357-159">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-159">Owner only</span></span> |
| <span data-ttu-id="51357-160">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="51357-160">Create Container</span></span> |<span data-ttu-id="51357-161">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-161">Owner only</span></span> |<span data-ttu-id="51357-162">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-162">Owner only</span></span> |
| <span data-ttu-id="51357-163">컨테이너 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-163">Get Container Properties</span></span> |<span data-ttu-id="51357-164">모두</span><span class="sxs-lookup"><span data-stu-id="51357-164">All</span></span> |<span data-ttu-id="51357-165">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-165">Owner only</span></span> |
| <span data-ttu-id="51357-166">컨테이너 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-166">Get Container Metadata</span></span> |<span data-ttu-id="51357-167">모두</span><span class="sxs-lookup"><span data-stu-id="51357-167">All</span></span> |<span data-ttu-id="51357-168">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-168">Owner only</span></span> |
| <span data-ttu-id="51357-169">컨테이너 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="51357-169">Set Container Metadata</span></span> |<span data-ttu-id="51357-170">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-170">Owner only</span></span> |<span data-ttu-id="51357-171">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-171">Owner only</span></span> |
| <span data-ttu-id="51357-172">컨테이너 ACL 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-172">Get Container ACL</span></span> |<span data-ttu-id="51357-173">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-173">Owner only</span></span> |<span data-ttu-id="51357-174">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-174">Owner only</span></span> |
| <span data-ttu-id="51357-175">컨테이너 ACL 설정</span><span class="sxs-lookup"><span data-stu-id="51357-175">Set Container ACL</span></span> |<span data-ttu-id="51357-176">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-176">Owner only</span></span> |<span data-ttu-id="51357-177">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-177">Owner only</span></span> |
| <span data-ttu-id="51357-178">컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="51357-178">Delete Container</span></span> |<span data-ttu-id="51357-179">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-179">Owner only</span></span> |<span data-ttu-id="51357-180">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-180">Owner only</span></span> |
| <span data-ttu-id="51357-181">Blob 나열</span><span class="sxs-lookup"><span data-stu-id="51357-181">List Blobs</span></span> |<span data-ttu-id="51357-182">모두</span><span class="sxs-lookup"><span data-stu-id="51357-182">All</span></span> |<span data-ttu-id="51357-183">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-183">Owner only</span></span> |
| <span data-ttu-id="51357-184">Blob 배치</span><span class="sxs-lookup"><span data-stu-id="51357-184">Put Blob</span></span> |<span data-ttu-id="51357-185">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-185">Owner only</span></span> |<span data-ttu-id="51357-186">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-186">Owner only</span></span> |
| <span data-ttu-id="51357-187">Blob 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-187">Get Blob</span></span> |<span data-ttu-id="51357-188">모두</span><span class="sxs-lookup"><span data-stu-id="51357-188">All</span></span> |<span data-ttu-id="51357-189">모두</span><span class="sxs-lookup"><span data-stu-id="51357-189">All</span></span> |
| <span data-ttu-id="51357-190">Blob 속성 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-190">Get Blob Properties</span></span> |<span data-ttu-id="51357-191">모두</span><span class="sxs-lookup"><span data-stu-id="51357-191">All</span></span> |<span data-ttu-id="51357-192">모두</span><span class="sxs-lookup"><span data-stu-id="51357-192">All</span></span> |
| <span data-ttu-id="51357-193">Blob 속성 설정</span><span class="sxs-lookup"><span data-stu-id="51357-193">Set Blob Properties</span></span> |<span data-ttu-id="51357-194">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-194">Owner only</span></span> |<span data-ttu-id="51357-195">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-195">Owner only</span></span> |
| <span data-ttu-id="51357-196">Blob 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-196">Get Blob Metadata</span></span> |<span data-ttu-id="51357-197">모두</span><span class="sxs-lookup"><span data-stu-id="51357-197">All</span></span> |<span data-ttu-id="51357-198">모두</span><span class="sxs-lookup"><span data-stu-id="51357-198">All</span></span> |
| <span data-ttu-id="51357-199">Blob 메타데이터 설정</span><span class="sxs-lookup"><span data-stu-id="51357-199">Set Blob Metadata</span></span> |<span data-ttu-id="51357-200">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-200">Owner only</span></span> |<span data-ttu-id="51357-201">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-201">Owner only</span></span> |
| <span data-ttu-id="51357-202">블록 배치</span><span class="sxs-lookup"><span data-stu-id="51357-202">Put Block</span></span> |<span data-ttu-id="51357-203">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-203">Owner only</span></span> |<span data-ttu-id="51357-204">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-204">Owner only</span></span> |
| <span data-ttu-id="51357-205">블록 목록 가져오기(커밋된 블록만)</span><span class="sxs-lookup"><span data-stu-id="51357-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="51357-206">모두</span><span class="sxs-lookup"><span data-stu-id="51357-206">All</span></span> |<span data-ttu-id="51357-207">모두</span><span class="sxs-lookup"><span data-stu-id="51357-207">All</span></span> |
| <span data-ttu-id="51357-208">블록 목록 가져오기(커밋되지 않은 블록만 또는 모든 블록)</span><span class="sxs-lookup"><span data-stu-id="51357-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="51357-209">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-209">Owner only</span></span> |<span data-ttu-id="51357-210">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-210">Owner only</span></span> |
| <span data-ttu-id="51357-211">블록 목록 배치</span><span class="sxs-lookup"><span data-stu-id="51357-211">Put Block List</span></span> |<span data-ttu-id="51357-212">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-212">Owner only</span></span> |<span data-ttu-id="51357-213">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-213">Owner only</span></span> |
| <span data-ttu-id="51357-214">Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="51357-214">Delete Blob</span></span> |<span data-ttu-id="51357-215">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-215">Owner only</span></span> |<span data-ttu-id="51357-216">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-216">Owner only</span></span> |
| <span data-ttu-id="51357-217">Blob 복사</span><span class="sxs-lookup"><span data-stu-id="51357-217">Copy Blob</span></span> |<span data-ttu-id="51357-218">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-218">Owner only</span></span> |<span data-ttu-id="51357-219">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-219">Owner only</span></span> |
| <span data-ttu-id="51357-220">Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="51357-220">Snapshot Blob</span></span> |<span data-ttu-id="51357-221">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-221">Owner only</span></span> |<span data-ttu-id="51357-222">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-222">Owner only</span></span> |
| <span data-ttu-id="51357-223">Blob 임대</span><span class="sxs-lookup"><span data-stu-id="51357-223">Lease Blob</span></span> |<span data-ttu-id="51357-224">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-224">Owner only</span></span> |<span data-ttu-id="51357-225">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-225">Owner only</span></span> |
| <span data-ttu-id="51357-226">페이지 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-226">Put Page</span></span> |<span data-ttu-id="51357-227">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-227">Owner only</span></span> |<span data-ttu-id="51357-228">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-228">Owner only</span></span> |
| <span data-ttu-id="51357-229">페이지 범위 가져오기</span><span class="sxs-lookup"><span data-stu-id="51357-229">Get Page Ranges</span></span> |<span data-ttu-id="51357-230">모두</span><span class="sxs-lookup"><span data-stu-id="51357-230">All</span></span> |<span data-ttu-id="51357-231">모두</span><span class="sxs-lookup"><span data-stu-id="51357-231">All</span></span> |
| <span data-ttu-id="51357-232">Blob 추가</span><span class="sxs-lookup"><span data-stu-id="51357-232">Append Blob</span></span> |<span data-ttu-id="51357-233">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-233">Owner only</span></span> |<span data-ttu-id="51357-234">소유자만</span><span class="sxs-lookup"><span data-stu-id="51357-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="51357-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51357-235">Next steps</span></span>

* [<span data-ttu-id="51357-236">Azure 저장소 서비스에 대한 인증</span><span class="sxs-lookup"><span data-stu-id="51357-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="51357-237">SAS(공유 액세스 서명) 사용</span><span class="sxs-lookup"><span data-stu-id="51357-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="51357-238">공유 액세스 서명을 사용하여 액세스 위임</span><span class="sxs-lookup"><span data-stu-id="51357-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
