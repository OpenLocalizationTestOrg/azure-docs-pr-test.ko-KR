---
title: "Azure Storage에서 Blob의 읽기 전용 스냅숏 만들기 | Microsoft Docs"
description: "지정된 시점에서 Blob 데이터를 백업하는 Blob의 스냅숏을 만드는 방법을 알아봅니다. 용량 요금을 최소화하기 위해 스냅숏의 청구 방법 및 사용 방법을 파악합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 6ebb77f4ec5f1887e5c55bf1c8c64224a9233654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="d2d0d-104">Blob 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="d2d0d-104">Create a blob snapshot</span></span>

<span data-ttu-id="d2d0d-105">스냅숏은 특정 시점에 생성된 Blob의 읽기 전용 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="d2d0d-106">스냅숏은 blob를 백업하는데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="d2d0d-107">스냅숏을 만든 후에 읽기, 복사 또는 삭제할 수 있지만 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="d2d0d-108">Blob URI에 스냅숏이 만들어진 시점의 시간을 나타내는 Blob URI에 추가된 **DateTime** 값이 있다는 점을 제외하고 Blob의 스냅숏은 해당 Blob와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="d2d0d-109">예를 들어 페이지 Blob URI가 `http://storagesample.core.blob.windows.net/mydrives/myvhd`이면 스냅숏 URI는 `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="d2d0d-110">모든 스냅숏은 기본 Blob의 URI를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="d2d0d-111">기본 Blob와 스냅숏의 유일한 차이는 추가된 **DateTime** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="d2d0d-112">Blob 하나에 여러 스냅숏이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="d2d0d-113">스냅숏을 명시적으로 삭제하기 전까지 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="d2d0d-114">스냅숏은 해당 기본 Blob보다 수명이 길 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="d2d0d-115">기본 Blob와 연결된 스냅숏을 열거하여 현재 스냅숏을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="d2d0d-116">Blob의 스냅숏을 만들면 blob의 시스템 속성이 같은 값으로 스냅숏에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="d2d0d-117">만들 때 스냅숏에 대한 별도의 메타데이터를 지정하지 않으면 기본 Blob의 메타데이터가 스냅숏에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="d2d0d-118">기본 blob와 연결된 모든 임대는 스냅숏에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="d2d0d-119">스냅숏에 대해 임대를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="d2d0d-120">VM 디스크에 대한 현재 정보 및 상태를 저장하는 데 VHD 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="d2d0d-121">VM 내에서 디스크를 분리하거나 VM을 종료하고, 해당 VHD 파일의 스냅숏을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="d2d0d-122">해당 스냅숏 파일을 나중에 사용하여 해당 시점에 VHD 파일을 검색하여 VM을 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="d2d0d-123">Blob이 있는 저장소 계정에 SSE(저장소 서비스 암호화)를 사용할 경우 해당 Blob의 스냅숏은 미사용 시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="d2d0d-124">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="d2d0d-124">Create a snapshot</span></span>
<span data-ttu-id="d2d0d-125">다음 코드 예제에서는 [.NET용 Azure Storage 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)를 사용하여 스냅숏을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="d2d0d-126">이 예제에서는 만들 때 스냅숏에 대한 추가 메타데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="d2d0d-127">스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="d2d0d-127">Copy snapshots</span></span>
<span data-ttu-id="d2d0d-128">Blob 및 스냅숏 관련 복사 작업에는 다음 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="d2d0d-129">기본 Blob에 대해 스냅숏을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="d2d0d-130">스냅숏의 수준을 기본 Blob 위치로 올리면 이전 Blob 버전을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="d2d0d-131">스냅숏은 그대로 유지되지만 기본 blob은 스냅숏의 쓰기 가능한 복사본으로 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="d2d0d-132">스냅숏을 다른 이름으로 대상 Blob에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="d2d0d-133">생성되는 대상 Blob은 스냅숏이 아닌 쓰기 가능한 Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="d2d0d-134">원본 Blob을 복사해도 해당 원본 Blob의 스냅숏은 대상에 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="d2d0d-135">대상 Blob을 복사본으로 덮어쓸 때 원래 대상 Blob와 연결된 스냅숏은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="d2d0d-136">블록 Blob의 스냅숏을 만들면 블록의 커밋된 블록 목록도 스냅숏에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="d2d0d-137">커밋되지 않은 블록은 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="d2d0d-138">액세스 조건 지정</span><span class="sxs-lookup"><span data-stu-id="d2d0d-138">Specify an access condition</span></span>
<span data-ttu-id="d2d0d-139">[CreateSnapshotAsync][dotnet_CreateSnapshotAsync]를 호출할 때 조건이 충족되어야 스냅숏이 작성되도록 액세스 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="d2d0d-140">액세스 조건을 지정하려면 [AccessCondition][dotnet_AccessCondition] 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="d2d0d-141">지정한 조건이 충족되지 않으면 스냅숏은 작성되지 않으며 Blob service는 상태 코드 [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="d2d0d-142">스냅숏 삭제</span><span class="sxs-lookup"><span data-stu-id="d2d0d-142">Delete snapshots</span></span>
<span data-ttu-id="d2d0d-143">스냅숏을 삭제하지 않으면 스냅숏이 포함된 Blob을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="d2d0d-144">스냅숏을 개별적으로 삭제하거나 원본 Blob를 삭제할 때 모든 스냅숏을 삭제되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="d2d0d-145">스냅숏이 있는 Blob을 삭제하려고 하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="d2d0d-146">다음 코드 예제에서는 .NET에서 Blob 및 해당 스냅숏을 삭제하는 방법을 보여 줍니다. 여기서 `blockBlob`은 [CloudBlockBlob][dotnet_CloudBlockBlob] 형식의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="d2d0d-147">Azure 프리미엄 저장소를 사용한 스냅숏</span><span class="sxs-lookup"><span data-stu-id="d2d0d-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="d2d0d-148">프리미엄 저장소에서 스냅숏을 사용할 때는 다음 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="d2d0d-149">프리미엄 저장소 계정의 페이지 Blob당 최대 스냅숏 수는 100개입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="d2d0d-150">해당 제한을 초과하면 스냅숏 Blob 작업에서 오류 코드 409(`SnapshotCountExceeded`)가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="d2d0d-151">프리미엄 저장소 계정의 페이지 Blob 스냅숏은 10분마다 한 번 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="d2d0d-152">해당 속도를 초과하면 스냅숏 Blob 작업에서 오류 코드 409(`SnapshotOperationRateExceeded`)가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="d2d0d-153">스냅숏을 읽으려는 경우 Blob 복사 작업을 사용하여 계정의 다른 페이지 Blob에 스냅숏을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="d2d0d-154">이때 복사 작업의 대상 Blob에는 기존 스냅숏이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="d2d0d-155">대상 Blob에 스냅숏이 있으면 Blob 복사 작업에서 오류 코드 409(`SnapshotsPresent`)가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="d2d0d-156">스냅숏에 대한 절대 URI 반환</span><span class="sxs-lookup"><span data-stu-id="d2d0d-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="d2d0d-157">이 C# 코드 예제에서는 스냅숏을 만들고 기본 위치에 대한 절대 URI를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="d2d0d-158">스냅숏 요금 청구 방법 이해</span><span class="sxs-lookup"><span data-stu-id="d2d0d-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="d2d0d-159">Blob의 읽기 전용 복사본인 스냅숏을 만들면 계정에 데이터 저장소 요금이 추가로 부과될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="d2d0d-160">응용 프로그램을 디자인할 때는 비용을 최소화할 수 있도록 이러한 요금 발생 방식을 파악하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="d2d0d-161">청구 관련 중요 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d2d0d-161">Important billing considerations</span></span>
<span data-ttu-id="d2d0d-162">아래 목록에는 스냅숏을 만들 때 고려할 주요 사항이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="d2d0d-163">저장소 계정에서는 고유 블록이나 페이지가 Blob에 있는지 혹은 스냅숏에 있는지에 관계없이 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="d2d0d-164">스냅숏의 기준이 되는 Blob을 업데이트할 때까지는 해당 Blob와 연결된 스냅숏에 대해 계정에 추가 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="d2d0d-165">기본 Blob를 업데이트한 후에 해당 스냅숏과 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="d2d0d-166">이 경우에 Blob 또는 스냅숏 각각에서 고유한 블록이나 페이지에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="d2d0d-167">블록 Blob 내의 블록을 바꾸고 나면 해당 블록은 이후부터 고유 블록으로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="d2d0d-168">블록의 ID와 데이터가 스냅숏에서와 같더라도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="d2d0d-169">블록을 다시 커밋하면 스냅숏의 해당 항목과 달라지므로 해당 데이터에 대해 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="d2d0d-170">같은 데이터로 업데이트하는 페이지 Blob 내 페이지의 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="d2d0d-171">[UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] 또는 [UploadFromByteArray][dotnet_UploadFromByteArray] 메서드를 호출하여 블록 Blob을 바꾸면 해당 Blob의 모든 블록이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="d2d0d-172">해당 Blob에 스냅숏이 연결되어 있으면 스냅숏과 기본 Blob의 모든 블록이 달라지므로 두 Blob의 모든 블록에 대해 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="d2d0d-173">이는 기본 Blob와 스냅숏의 데이터가 동일하게 유지되더라도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="d2d0d-174">Azure Blob 서비스에서는 두 블록이 같은 데이터를 포함하는지를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="d2d0d-175">업로드/커밋되는 각 블록은 데이터와 블록 ID가 같더라도 고유한 블록으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="d2d0d-176">고유한 블록에 대해서는 비용이 부과되므로 스냅숏이 포함된 Blob을 업데이트하면 고유한 블록이 추가로 생성되어 추가 비용이 발생함을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="d2d0d-177">스냅숏 관리 비용을 최소화</span><span class="sxs-lookup"><span data-stu-id="d2d0d-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="d2d0d-178">추가 비용을 방지하기 위해서는 스냅숏을 신중하게 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="d2d0d-179">스냅숏 저장으로 인해 발생하는 비용을 최소화하려면 다음 모범 사례를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="d2d0d-180">응용 프로그램 디자인상 스냅숏을 유지해야 하는 경우가 아니면, Blob을 업데이트할 때마다 같은 데이터로 업데이트하더라도 해당 Blob에 연결된 스냅숏을 삭제한 후에 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="d2d0d-181">Blob의 스냅숏을 삭제한 후에 다시 만들면 Blob와 스냅숏이 달라지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="d2d0d-182">Blob의 스냅숏을 유지하는 경우에는 [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] 또는 [UploadFromByteArray][dotnet_UploadFromByteArray]를 호출하여 Blob을 업데이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="d2d0d-183">이러한 메서드는 Blob의 모든 블록을 바꾸어 기본 Blob 및 해당 스냅숏이 심각하게 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="d2d0d-184">대신 [PutBlock][dotnet_PutBlock] 및 [PutBlockList][dotnet_PutBlockList] 메서드를 사용하여 가능한 최소 블록 수만 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="d2d0d-185">스냅숏 청구 시나리오</span><span class="sxs-lookup"><span data-stu-id="d2d0d-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="d2d0d-186">다음 시나리오에서는 블록 Blob와 해당 스냅숏에 대해 비용이 청구되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="d2d0d-187">**시나리오 1**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-187">**Scenario 1**</span></span>

<span data-ttu-id="d2d0d-188">시나리오 1에서는 스냅숏을 생성한 후 기본 Blob을 업데이트하지 않았으므로 고유 블록 1, 2, 3에 대해서만 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="d2d0d-190">**시나리오 2**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-190">**Scenario 2**</span></span>

<span data-ttu-id="d2d0d-191">시나리오 2에서는 기본 Blob은 업데이트되었지만 스냅숏은 업데이트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="d2d0d-192">블록 3이 업데이트되고 동일한 데이터와 동일한 ID를 가지고 있지만 스냅숏의 블록 3과 같지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="d2d0d-193">따라서 4개 블록에 대한 요금이 계정에 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-193">As a result, the account is charged for four blocks.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="d2d0d-195">**시나리오 3**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-195">**Scenario 3**</span></span>

<span data-ttu-id="d2d0d-196">시나리오 3에서는 기본 Blob은 업데이트되었지만 스냅숏은 업데이트되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="d2d0d-197">기본 Blob에서 블록 3이 블록 4로 바뀌었지만 스냅숏은 계속 블록 3을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="d2d0d-198">따라서 4개 블록에 대한 요금이 계정에 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-198">As a result, the account is charged for four blocks.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="d2d0d-200">**시나리오 4**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-200">**Scenario 4**</span></span>

<span data-ttu-id="d2d0d-201">시나리오 4에서는 기본 Blob이 완전히 업데이트되었으며 원래 블록을 하나도 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="d2d0d-202">따라서 8개 고유 블록 모두에 대한 요금이 계정에 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="d2d0d-203">[UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] 또는 [UploadFromByteArray][dotnet_UploadFromByteArray] 등의 업데이트 메서드를 사용하는 경우가 이러한 시나리오에 해당합니다. 이러한 메서드는 Blob의 모든 콘텐츠를 바꾸기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="d2d0d-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2d0d-205">Next steps</span></span>

* <span data-ttu-id="d2d0d-206">VM(가상 컴퓨터) 디스크 스냅숏 사용에 대한 자세한 내용은 [증분 스냅숏을 사용하여 Azure 관리되지 않는 VM 디스크 백업](storage-incremental-snapshots.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="d2d0d-207">Blob Storage를 사용하는 추가 코드 예제는 [Azure 코드 샘플](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="d2d0d-208">GitHub에서 샘플 응용 프로그램을 다운로드하고 실행하거나 코드를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx