---
title: "Azure 저장소에 blob의 읽기 전용 스냅숏 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 주어진 시점에 blob 데이터를 blob tooback의 스냅숏 합니다. 하 고 스냅숏을 요금을 청구 하는 방법 이해 toouse toominimize 용량 요금을 합니다."
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
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="db59d-104">Blob 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="db59d-104">Create a blob snapshot</span></span>

<span data-ttu-id="db59d-105">스냅숏은 특정 시점에 생성된 Blob의 읽기 전용 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="db59d-106">스냅숏은 blob를 백업하는데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="db59d-107">스냅숏을 만든 후에 읽기, 복사 또는 삭제할 수 있지만 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="db59d-108">Blob의 스냅숏을 기본 blob와 동일한 tooits 이면 해당 hello blob를 제외 하 고 URI에는 **DateTime** 값 toohello blob URI tooindicate hello 이루어진 지정 시간은 hello에 스냅숏 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="db59d-109">예를 들어, 페이지 blob URI가 `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello 스냅숏 URI는 너무 유사`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="db59d-110">모든 스냅숏이 hello 기본 blob URI를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="db59d-111">hello 기본 blob와 hello 스냅숏 차이 추가 hello만 hello **DateTime** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="db59d-112">Blob 하나에 여러 스냅숏이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="db59d-113">스냅숏을 명시적으로 삭제하기 전까지 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="db59d-114">스냅숏은 해당 기본 Blob보다 수명이 길 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="db59d-115">기본 blob tootrack hello와 연결 된 hello 스냅숏을 열거할 수 현재 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="db59d-116">Blob의 스냅숏을 만들 때 hello blob의 시스템 속성은 hello로 복사한 toohello 스냅숏 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="db59d-117">hello 기본 blob의 메타 데이터 스냅숏을 만들 때 hello에 대 한 별도 메타 데이터를 지정 하지 않으면 복사 된 toohello 스냅숏을 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="db59d-118">Hello 기본 blob와 연결 된 모든 임대 hello 스냅숏 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="db59d-119">스냅숏에 대해 임대를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="db59d-120">VHD 파일이 사용 되는 toostore hello에 대 한 현재 정보 및 VM 디스크에 대 한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="db59d-121">Hello VM 내에서 디스크를 분리 hello VM 종료 한 다음 해당 VHD 파일의 스냅숏을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="db59d-122">해당 스냅숏 파일을 사용할 수 이후 tooretrieve hello VHD 시간 해당 시점에 파일 및 hello VM을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="db59d-123">Hello 저장소 계정의 저장소 서비스 암호화 SSE () 사용 하는 경우는 hello에서 blob이 있는 다음 해당 blob의 스냅숏을 휴지 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="db59d-124">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="db59d-124">Create a snapshot</span></span>
<span data-ttu-id="db59d-125">hello 다음 코드 예제에서는 방법을 사용 하 여 스냅숏 toocreate hello [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="db59d-126">이 예제에서는 생성 될 때 hello 스냅숏에 대 한 추가 메타 데이터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="db59d-127">스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="db59d-127">Copy snapshots</span></span>
<span data-ttu-id="db59d-128">Blob 및 스냅숏 관련 복사 작업에는 다음 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="db59d-129">기본 Blob에 대해 스냅숏을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="db59d-130">Hello 기본 blob의 스냅숏 toohello 위치를 홍보 하 여 이전 버전의 blob 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="db59d-131">hello 스냅숏은 그대로 유지 하지만 hello 기본 blob에 쓰기 가능한 스냅숏 hello 덮어쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="db59d-132">다른 이름 사용 하 여 스냅숏 tooa 대상 blob를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="db59d-133">hello 결과 대상 blob에 쓰기 가능한 blob 이며 스냅숏이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="db59d-134">원본 blob 복사 되 면 hello 원본 blob의 스냅숏도 모두 복사한 toohello 대상 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="db59d-135">복사본으로 대상 blob을 덮어씀을 hello 원래 대상 blob와 연결 된 모든 스냅숏은 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="db59d-136">블록 blob의 스냅숏을 만들 때 hello blob의 커밋된 블록 목록 복사한 toohello 스냅숏 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="db59d-137">커밋되지 않은 블록은 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="db59d-138">액세스 조건 지정</span><span class="sxs-lookup"><span data-stu-id="db59d-138">Specify an access condition</span></span>
<span data-ttu-id="db59d-139">호출 하는 경우 [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], hello 스냅숏이 생성 된 조건이 충족 될 경우에 되도록 액세스 조건을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="db59d-140">toospecify 액세스 조건을 사용 하 여 hello [AccessCondition] [ dotnet_AccessCondition] 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="db59d-141">Hello 지정한 조건이 충족 되지 않으면, hello 스냅숏이 만들어지지 않으면 및 hello Blob 서비스가 상태 코드를 반환 하는 경우 [HTTPStatusCode][dotnet_HTTPStatusCode]합니다. PreconditionFailed 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="db59d-142">스냅숏 삭제</span><span class="sxs-lookup"><span data-stu-id="db59d-142">Delete snapshots</span></span>
<span data-ttu-id="db59d-143">Hello 스냅숏을 삭제 하지 않는 한 스냅숏과 함께 blob을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="db59d-144">스냅숏을 개별적으로 삭제 하거나 hello 원본 blob 삭제 될 때 모든 스냅숏을 삭제 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="db59d-145">Toodelete 스냅숏이 있는 blob을 시도 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="db59d-146">코드 예제에서 보여 주는 방법을 다음 hello toodelete blob와 스냅숏이.net, 여기서 `blockBlob` 형식의 개체가 [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="db59d-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="db59d-147">Azure 프리미엄 저장소를 사용한 스냅숏</span><span class="sxs-lookup"><span data-stu-id="db59d-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="db59d-148">프리미엄 저장소 스냅숏을 사용 하는 경우 규칙에 따라 hello 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="db59d-149">프리미엄 저장소 계정에 페이지 blob 당 스냅숏 hello 최대 수는 100입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="db59d-150">해당 제한을 초과 하는 hello 스냅숏 Blob 작업 반환 오류 코드 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="db59d-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="db59d-151">프리미엄 저장소 계정의 페이지 Blob 스냅숏은 10분마다 한 번 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="db59d-152">Hello 스냅숏 Blob 작업 오류 코드 409 반환 해당 속도 초과 하는 경우 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="db59d-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="db59d-153">스냅숏을 tooread hello 계정에서 Blob 복사 작업 toocopy hello 스냅숏 tooanother 페이지 blob를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="db59d-154">hello 복사 작업에 대 한 hello 대상 blob에 기존 스냅숏이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="db59d-155">Hello 대상 blob는 스냅숏, 한 경우 오류 코드 409를 반환 하는 hello Blob 복사 작업 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="db59d-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="db59d-156">절대 URI tooa 스냅숏 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="db59d-157">이 C# 코드 예제에서는 스냅숏을 만들고 hello 작성 hello 기본 위치에 대 한 절대 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="db59d-158">스냅숏 요금 청구 방법 이해</span><span class="sxs-lookup"><span data-stu-id="db59d-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="db59d-159">Blob의 읽기 전용 복사본 인 스냅숏을 만들면 추가 데이터 저장소 요금 tooyour 계정에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="db59d-160">응용 프로그램을 디자인할 때 중요 한 toobe 비용을 최소화할 수 있도록 이러한 비용 수 발생 하는 방법을 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="db59d-161">청구 관련 중요 고려 사항</span><span class="sxs-lookup"><span data-stu-id="db59d-161">Important billing considerations</span></span>
<span data-ttu-id="db59d-162">hello 목록 다음에 스냅숏을 만들 때 주요 사항을 tooconsider를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="db59d-163">저장소 계정 hello blob 또는 스냅숏의 hello 되었든 관계 없이 개별 블록 또는 페이지에 대 한 요금을 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="db59d-164">계정 기반는 hello blob를 업데이트할 때까지 blob와 연결 된 스냅숏 위한 추가 비용이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="db59d-165">Hello 기본 blob를 업데이트 한 후 해당 스냅숏에서 모델과.</span><span class="sxs-lookup"><span data-stu-id="db59d-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="db59d-166">이 경우 hello 고유 블록이 나 페이지에 각 blob 또는 스냅숏에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="db59d-167">블록 Blob 내의 블록을 바꾸고 나면 해당 블록은 이후부터 고유 블록으로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="db59d-168">이 hello 블록의 블록 ID를 동일 하 고 동일한 hello hello 하는 경우에 마찬가지 hello 스냅숏의 데이터를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="db59d-169">Hello 블록이 커밋된 후 다시, 모든 스냅숏의 바뀌므로 모델과 하 고 해당 데이터에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="db59d-170">마찬가지 페이지에 대 한 동일한 데이터로 업데이트 하는 페이지 blob의 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="db59d-171">Hello를 호출 하 여 블록 blob를 교체 [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], 또는 [UploadFromByteArray] [ dotnet_UploadFromByteArray] 메서드 hello blob에서 블록을 모두 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="db59d-172">해당 blob와 연결 된 스냅숏이 있는 경우에 hello 기본 blob와 스냅숏의 모든 블록을 이제 분기 하 고 모든 hello 블록에에서 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="db59d-173">Hello 데이터 hello 기본 blob와 hello 스냅숏에 동일 하 게 유지 하는 경우에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="db59d-174">hello Azure Blob 서비스는 동일한 데이터를 포함 하는 두 개의 블록 여부 수단 toodetermine가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="db59d-175">업로드 및 커밋되는 각 블록은 고유한 것으로 간주, 동일한 블록 id입니다. 동일한 데이터 및 hello hello에 경우에</span><span class="sxs-lookup"><span data-stu-id="db59d-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="db59d-176">고유한 블록에 대 한 비용 발생을 이므로 추가 비용이 발생 하 고 고유한 블록이 추가적으로 인해 스냅숏이 포함 된 blob를 업데이트 하는 중요 한 tooconsider 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="db59d-177">스냅숏 관리 비용을 최소화</span><span class="sxs-lookup"><span data-stu-id="db59d-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="db59d-178">전자 메일로 신중 하 게 관리 하는 것이 좋습니다 tooavoid 추가 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="db59d-179">Toohelp 스냅숏의 hello 저장소에서 발생 하는 hello 비용을 최소화 하는 다음 모범 사례를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="db59d-180">삭제 하 고 blob에 연결 된 hello blob를 업데이트할 때마다 응용 프로그램 디자인에서 스냅숏을 유지 하도록 요청 하지 않는 동일한 데이터로 업데이트 하는 경우에 스냅숏을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="db59d-181">삭제 하 고 다시 hello blob의 스냅숏 만들기, hello blob 및 스냅숏을 분기 하지 않는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="db59d-182">Blob의 스냅숏을 유지 관리할 때는 호출 하지 마세요. [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], 또는 [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob입니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="db59d-183">이러한 메서드를 대체 하 여 모든 사용자 기본 blob와 해당 스냅숏 toodiverge 현저 하 게 발생 하는 hello blob에 블록 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="db59d-184">대신, 업데이트 가능한 가장 적은 수의 블록을 hello를 사용 하 여 hello [PutBlock] [ dotnet_PutBlock] 및 [PutBlockList] [ dotnet_PutBlockList] 메서드.</span><span class="sxs-lookup"><span data-stu-id="db59d-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="db59d-185">스냅숏 청구 시나리오</span><span class="sxs-lookup"><span data-stu-id="db59d-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="db59d-186">다음 시나리오는 hello 블록 blob 및 그 스냅숏에 대 한 비용 발생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="db59d-187">**시나리오 1**</span><span class="sxs-lookup"><span data-stu-id="db59d-187">**Scenario 1**</span></span>

<span data-ttu-id="db59d-188">시나리오 1의에서 hello 기본 blob 업데이트 되지 않은 hello 스냅숏이 만들어진 후 하므로 고유 블록 1, 2 및 3에 대해서만 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="db59d-190">**시나리오 2**</span><span class="sxs-lookup"><span data-stu-id="db59d-190">**Scenario 2**</span></span>

<span data-ttu-id="db59d-191">시나리오 2에서는 hello 기본 blob가 업데이트 된 있지만 hello 스냅숏이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="db59d-192">블록 3 업데이트 된 하 고 있는 경우에 동일한 데이터 hello 및 동일한 ID hello에 하지 블록 3 hello 스냅숏의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="db59d-193">결과적으로, hello 계정에 4 개의 블록에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-193">As a result, hello account is charged for four blocks.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="db59d-195">**시나리오 3**</span><span class="sxs-lookup"><span data-stu-id="db59d-195">**Scenario 3**</span></span>

<span data-ttu-id="db59d-196">3 시나리오에서는 hello 기본 blob가 업데이트 되지만 hello 스냅숏이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="db59d-197">블록 3이 hello 기본 blob에 블록 4로 교체 되지만 hello 스냅숏 여전히 블록 3이 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="db59d-198">결과적으로, hello 계정에 4 개의 블록에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-198">As a result, hello account is charged for four blocks.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="db59d-200">**시나리오 4**</span><span class="sxs-lookup"><span data-stu-id="db59d-200">**Scenario 4**</span></span>

<span data-ttu-id="db59d-201">시나리오 4 hello 기본 blob은 완전히 업데이트 하 고 원래 블록 모두 달라졌습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="db59d-202">결과적으로, hello 계정 전체 8 개의 블록에 대 한 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="db59d-203">이 시나리오는 같은 업데이트 메서드를 사용 하는 경우에 발생할 수 있습니다 [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], 또는 [UploadFromByteArray][dotnet_UploadFromByteArray]이러한 메서드를 대체 하는 모든 blob의 내용을 hello 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Azure 저장소 리소스](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="db59d-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db59d-205">Next steps</span></span>

* <span data-ttu-id="db59d-206">VM(가상 컴퓨터) 디스크 스냅숏 사용에 대한 자세한 내용은 [증분 스냅숏을 사용하여 Azure 관리되지 않는 VM 디스크 백업](../../virtual-machines/windows/incremental-snapshots.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="db59d-207">Blob Storage를 사용하는 추가 코드 예제는 [Azure 코드 샘플](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db59d-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="db59d-208">샘플 응용 프로그램을 다운로드 하 고 실행 하거나 GitHub에서 hello 코드를 찾아보려면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db59d-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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