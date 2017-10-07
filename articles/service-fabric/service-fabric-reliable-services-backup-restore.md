---
title: "aaaService 패브릭 백업 및 복원 | Microsoft Docs"
description: "서비스 패브릭 백업 및 복원에 관한 개념 설명서"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a><span data-ttu-id="f3718-103">Reliable Services 및 Reliable Actors 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="f3718-103">Back up and restore Reliable Services and Reliable Actors</span></span>
<span data-ttu-id="f3718-104">Azure 서비스 패브릭은이 고가용성 여러 노드 toomaintain 걸쳐 hello 상태를 복제 하는 고가용성 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-104">Azure Service Fabric is a high-availability platform that replicates hello state across multiple nodes toomaintain this high availability.</span></span>  <span data-ttu-id="f3718-105">따라서 hello 클러스터의 한 노드에서 오류가 발생 하더라도 hello 서비스 toobe 사용할 수 있는 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-105">Thus, even if one node in hello cluster fails, hello services continue toobe available.</span></span> <span data-ttu-id="f3718-106">Hello 플랫폼에서 제공 하는 이러한 기본 제공 중복 일부에 대 한 충분 한 수 있지만, 일부 경우에는 것이 좋습니다 (tooan 외부 저장소) 데이터를 서비스 tooback hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-106">While this in-built redundancy provided by hello platform may be sufficient for some, in certain cases it is desirable for hello service tooback up data (tooan external store).</span></span>

> [!NOTE]
> <span data-ttu-id="f3718-107">중요 한 toobackup 이며 데이터 (및 예상 대로 작동 하는지 테스트) 복원 되므로 데이터 손실 시나리오에서 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-107">It is critical toobackup and restore your data (and test that it works as expected) so you can recover from data loss scenarios.</span></span>
> 
> 

<span data-ttu-id="f3718-108">예를 들어 서비스 tooback 순서 tooprotect hello 다음 시나리오에서에서의 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-108">For example, a service may want tooback up data in order tooprotect from hello following scenarios:</span></span>

- <span data-ttu-id="f3718-109">전체 서비스 패브릭 클러스터를 완전히 잃 hello의 hello 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-109">In hello event of hello permanent loss of an entire Service Fabric cluster.</span></span>
- <span data-ttu-id="f3718-110">서비스 파티션 hello 복제본의 과반수가 영구 손실</span><span class="sxs-lookup"><span data-stu-id="f3718-110">Permanent loss of a majority of hello replicas of a service partition</span></span>
- <span data-ttu-id="f3718-111">그에 따라 hello 상태 실수로 가져옵니다 삭제 되거나 손상 된 관리 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-111">Administrative errors whereby hello state accidentally gets deleted or corrupted.</span></span> <span data-ttu-id="f3718-112">예를 들어 충분 한 권한 가진 관리자가 실수로 hello 서비스를 삭제 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-112">For example, this may happen if an administrator with sufficient privilege erroneously deletes hello service.</span></span>
- <span data-ttu-id="f3718-113">데이터가 손상 된 hello 서비스 버그입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-113">Bugs in hello service that cause data corruption.</span></span> <span data-ttu-id="f3718-114">예를 들어이 항목은 서비스 코드 업그레이드를 사용 하는 잘못 된 데이터 tooa 신뢰할 수 있는 컬렉션을 작성을 시작할 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-114">For example, this may happen when a service code upgrade starts writing faulty data tooa Reliable Collection.</span></span> <span data-ttu-id="f3718-115">이 경우 코드 hello 둘 다 고 hello 데이터 toobe를 가질 수 tooan 되돌릴 이전 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-115">In such a case, both hello code and hello data may have toobe reverted tooan earlier state.</span></span>
- <span data-ttu-id="f3718-116">오프라인 데이터 처리.</span><span class="sxs-lookup"><span data-stu-id="f3718-116">Offline data processing.</span></span> <span data-ttu-id="f3718-117">별도로 hello 데이터를 생성 하는 hello 서비스에서 발생 하는 비즈니스 인텔리전스에 대 한 데이터의 오프 라인 처리 편리한 toohave 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-117">It might be convenient toohave offline processing of data for business intelligence that happens separately from hello service that generates hello data.</span></span>

<span data-ttu-id="f3718-118">hello 백업/복원 기능은 hello 신뢰할 수 있는 서비스 API toocreate 및 복원 백업에 기반 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-118">hello Backup/Restore feature allows services built on hello Reliable Services API toocreate and restore backups.</span></span> <span data-ttu-id="f3718-119">hello hello 플랫폼에서 제공 하는 백업 Api 허용 백업을 차단 읽기 또는 쓰기 작업 하지 않고 서비스 파티션의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-119">hello backup APIs provided by hello platform allow backup(s) of a service partition's state, without blocking read or write operations.</span></span> <span data-ttu-id="f3718-120">hello 복원 Api에는 선택한 백업에서 복원 하는 서비스 파티션의 상태 toobe를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-120">hello restore APIs allow a service partition's state toobe restored from a chosen backup.</span></span>

## <a name="types-of-backup"></a><span data-ttu-id="f3718-121">백업 유형</span><span class="sxs-lookup"><span data-stu-id="f3718-121">Types of Backup</span></span>
<span data-ttu-id="f3718-122">백업 옵션에는 전체 및 증분이라는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-122">There are two backup options: Full and Incremental.</span></span>
<span data-ttu-id="f3718-123">전체 백업을 hello 복제본의 모든 hello 필요한 데이터 toorecreate hello 상태를 포함 하는 백업: 검사점과 모든 로그 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-123">A full backup is a backup that contains all hello data required toorecreate hello state of hello replica: checkpoints and all log records.</span></span>
<span data-ttu-id="f3718-124">Hello 검사점 및 로그 hello에 있기 때문에 전체 백업은 단독으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-124">Since it has hello checkpoints and hello log, a full backup can be restored by itself.</span></span>

<span data-ttu-id="f3718-125">전체 백업 사용 하 여 hello 문제는 hello 검사점에는 큰 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-125">hello problem with full backups arises when hello checkpoints are large.</span></span>
<span data-ttu-id="f3718-126">예를 들어에 16GB의 상태는 복제본은 too16 g B 정도 구성 하는 검사점을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-126">For example, a replica that has 16 GB of state will have checkpoints that add up approximately too16 GB.</span></span>
<span data-ttu-id="f3718-127">5 분의 복구 지점 목표를 있는데 hello 복제본 toobe 5 분 마다 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-127">If we have a Recovery Point Objective of five minutes, hello replica needs toobe backed up every five minutes.</span></span>
<span data-ttu-id="f3718-128">Toocopy 필요한 백업 될 때마다 또한 검사점의 경우 16GB too50 MB (구성 가능 하 고 사용 하 여 `CheckpointThresholdInMB`) 로그의 가치입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-128">Each time it backs up it needs toocopy 16 GB of checkpoints in addition too50 MB (configurable using `CheckpointThresholdInMB`) worth of logs.</span></span>

![전체 백업 예입니다.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

<span data-ttu-id="f3718-130">hello 솔루션 toothis 문제는 백업만 포함 되어 있는 로그 레코드를 변경 하는 hello hello 마지막 백업 이후에 증분 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-130">hello solution toothis problem is incremental backups, where backup only contains hello changed log records since hello last backup.</span></span>

![증분 백업 예입니다.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

<span data-ttu-id="f3718-132">증분 백업 (hello 검사점을 포함 하지 않습니다) hello 마지막 백업 이후 변경 된 내용만 않으므로 더 빠르게 toobe 광범위 하지만 자체적으로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-132">Since incremental backups are only changes since hello last backup (does not include hello checkpoints), they tend toobe faster but they cannot be restored on their own.</span></span>
<span data-ttu-id="f3718-133">증분 백업을 toorestore hello 전체 백업 체인이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-133">toorestore an incremental backup, hello entire backup chain is required.</span></span>
<span data-ttu-id="f3718-134">백업 체인은 전체 백업으로 시작하여 이후 수많은 지속적인 증분 백업이 이어지는 백업의 체인입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-134">A backup chain is a chain of backups starting with a full backup and followed by a number of contiguous incremental backups.</span></span>

## <a name="backup-reliable-services"></a><span data-ttu-id="f3718-135">Reliable Services 백업</span><span class="sxs-lookup"><span data-stu-id="f3718-135">Backup Reliable Services</span></span>
<span data-ttu-id="f3718-136">hello 서비스 작성자가는 경우에 대 한 모든 권한 toomake 백업 및 백업이 저장 될 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-136">hello service author has full control of when toomake backups and where backups will be stored.</span></span>

<span data-ttu-id="f3718-137">백업 toostart hello 서비스가 필요한 tooinvoke hello 상속 된 멤버 함수 `BackupAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-137">toostart a backup, hello service needs tooinvoke hello inherited member function `BackupAsync`.</span></span>  
<span data-ttu-id="f3718-138">백업은 주 복제본 에서만에서 수행할 수 있습니다 및 쓰기 상태 toobe 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-138">Backups can be made only from primary replicas, and they require write status toobe granted.</span></span>

<span data-ttu-id="f3718-139">아래와 같이 `BackupAsync` 에 `BackupDescription` 개체를 하나 지정할 수 있는 콜백 함수 뿐만 아니라 전체 또는 증분 백업을, `Func<< BackupInfo, CancellationToken, Task<bool>>>` hello 백업 폴더에 로컬로 만들어지고 준비 toobe 제외 되어 toosome 때 호출 되는 외부 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-139">As shown below, `BackupAsync` takes in a `BackupDescription` object, where one can specify a full or incremental backup, as well as a callback function, `Func<< BackupInfo, CancellationToken, Task<bool>>>` that is invoked when hello backup folder has been created locally and is ready toobe moved out toosome external storage.</span></span>

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

<span data-ttu-id="f3718-140">증분 백업이 실패할 수 요청 tootake `FabricMissingFullBackupException`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-140">Request tootake an incremental backup can fail with `FabricMissingFullBackupException`.</span></span> <span data-ttu-id="f3718-141">이 예외 수행 중인 작업을 수행 하는 hello 중 하나를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-141">This exception indicates that one of hello following things is happening:</span></span>

- <span data-ttu-id="f3718-142">hello 복제본에 주 영역 바뀌었기 때문 전체 백업을 실행 되지 않음</span><span class="sxs-lookup"><span data-stu-id="f3718-142">hello replica has never taken a full backup since it has become primary,</span></span>
- <span data-ttu-id="f3718-143">잘린 hello 마지막 백업 이후 hello의 일부 로그 레코드 또는</span><span class="sxs-lookup"><span data-stu-id="f3718-143">some of hello log records since hello last backup has been truncated or</span></span>
- <span data-ttu-id="f3718-144">hello를 전달 하는 복제본 `MaxAccumulatedBackupLogSizeInMB` 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-144">replica passed hello `MaxAccumulatedBackupLogSizeInMB` limit.</span></span>

<span data-ttu-id="f3718-145">사용자가 hello 가능성을 수 toodo 증분 백업을 구성 하 여 늘릴 수 `MinLogSizeInMB` 또는 `TruncationThresholdFactor`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-145">Users can increase hello likelihood of being able toodo incremental backups by configuring `MinLogSizeInMB` or `TruncationThresholdFactor`.</span></span>
<span data-ttu-id="f3718-146">이러한 값을 늘리면 복제 디스크 사용량 당 hello 증가 한다는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-146">Note that increasing these values increases hello per replica disk usage.</span></span>
<span data-ttu-id="f3718-147">자세한 내용은 [Reliable Services 구성](service-fabric-reliable-services-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3718-147">For more information, see [Reliable Services Configuration](service-fabric-reliable-services-configuration.md)</span></span>

<span data-ttu-id="f3718-148">`BackupInfo`hello 런타임 hello 백업을 저장 하는 hello 폴더의 hello 위치를 포함 하 여 hello 백업, 관련 정보를 제공 (`BackupInfo.Directory`).</span><span class="sxs-lookup"><span data-stu-id="f3718-148">`BackupInfo` provides information regarding hello backup, including hello location of hello folder where hello runtime saved hello backup (`BackupInfo.Directory`).</span></span> <span data-ttu-id="f3718-149">hello 콜백 함수 hello를 이동할 수 `BackupInfo.Directory` tooan 외부 저장소 또는 다른 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-149">hello callback function can move hello `BackupInfo.Directory` tooan external store or another location.</span></span>  <span data-ttu-id="f3718-150">이 함수는 또한 수 toosuccessfully 이동 hello 백업 폴더 tooits 대상 위치를 했는지 여부를 나타내는 부울을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-150">This function also returns a bool that indicates whether it was able toosuccessfully move hello backup folder tooits target location.</span></span>

<span data-ttu-id="f3718-151">hello 다음 코드에서는 방법을 hello `BackupCallbackAsync` 메서드 사용된 tooupload hello 백업 tooAzure 저장소 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-151">hello following code demonstrates how hello `BackupCallbackAsync` method can be used tooupload hello backup tooAzure Storage:</span></span>

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

<span data-ttu-id="f3718-152">Hello 앞에 있는 예제에서 `ExternalBackupStore` 는 Azure Blob 저장소를 사용 하는 toointerface는 hello 샘플 클래스 및 `UploadBackupFolderAsync` hello 폴더를 압축 하 고 hello Azure Blob 저장소에 배치 하는 hello 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-152">In hello preceeding example, `ExternalBackupStore` is hello sample class that is used toointerface with Azure Blob storage, and `UploadBackupFolderAsync` is hello method that compresses hello folder and places it in hello Azure Blob store.</span></span>

<span data-ttu-id="f3718-153">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="f3718-153">Note that:</span></span>

  - <span data-ttu-id="f3718-154">특정 시점에서 처리 중인 복제본 당 하나의 백업 작업만이 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-154">There can be only one backup operation in-flight per replica at any given time.</span></span> <span data-ttu-id="f3718-155">둘 이상의 `BackupAsync` 호출 한 번에 발생 합니다 `FabricBackupInProgressException` toolimit 처리 중 백업 tooone 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-155">More than one `BackupAsync` call at a time will throw `FabricBackupInProgressException` toolimit inflight backups tooone.</span></span>
  - <span data-ttu-id="f3718-156">복제본 장애 조치 되 면 백업 진행 중인 동안, hello 백업 수 완료 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-156">If a replica fails over while a backup is in progress, hello backup may not have been completed.</span></span> <span data-ttu-id="f3718-157">따라서 hello 장애 조치 완료 되 면 hello 서비스 책임 toorestart hello 백업을 호출 하 여 `BackupAsync` 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-157">Thus, once hello failover finishes, it is hello service's responsibility toorestart hello backup by invoking `BackupAsync` as necessary.</span></span>

## <a name="restore-reliable-services"></a><span data-ttu-id="f3718-158">Reliable Services 복원</span><span class="sxs-lookup"><span data-stu-id="f3718-158">Restore Reliable Services</span></span>
<span data-ttu-id="f3718-159">일반적으로 hello 경우 tooperform 복원 작업을 할 수 있습니다 때 이러한 범주 중 하나에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-159">In general, hello cases when you might need tooperform a restore operation fall into one of these categories:</span></span>

  - <span data-ttu-id="f3718-160">손실 된 데이터를 분할 하는 hello 서비스.</span><span class="sxs-lookup"><span data-stu-id="f3718-160">hello service partition lost data.</span></span> <span data-ttu-id="f3718-161">예를 들어 (hello 주 복제본 포함)는 파티션에 대 한 2의 3 개의 복제본에 대 한 hello 디스크 손상 되거나 초기화를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-161">For example, hello disk for two out of three replicas for a partition (including hello primary replica) gets corrupted or wiped.</span></span> <span data-ttu-id="f3718-162">hello 새로운 주 toorestore 데이터를 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-162">hello new primary may need toorestore data from a backup.</span></span>
  - <span data-ttu-id="f3718-163">hello 전체 서비스는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-163">hello entire service is lost.</span></span> <span data-ttu-id="f3718-164">예를 들어 관리자 hello 전체 서비스를 제거 하 고 따라서 hello 서비스 및 hello 데이터 복원 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-164">For example, an administrator removes hello entire service and thus hello service and hello data need toobe restored.</span></span>
  - <span data-ttu-id="f3718-165">hello 서비스 (예: 응용 프로그램 버그)로 인해 손상 된 응용 프로그램 데이터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-165">hello service replicated corrupt application data (e.g., because of an application bug).</span></span> <span data-ttu-id="f3718-166">이 경우 hello 서비스에 toobe 업그레이드 되었거나 되돌린된 tooremove hello 원인 hello 손상 및 데이터 손상 되지 않은 toobe 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-166">In this case, hello service has toobe upgraded or reverted tooremove hello cause of hello corruption, and non-corrupt data has toobe restored.</span></span>

<span data-ttu-id="f3718-167">사용 하 여 보여 주는 예 제공 여러 접근 방식을 가능한 상태인 `RestoreAsync` hello 위의 시나리오에서에서 toorecover 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-167">While many approaches are possible, we offer some examples on using `RestoreAsync` toorecover from hello above scenarios.</span></span>

## <a name="partition-data-loss-in-reliable-services"></a><span data-ttu-id="f3718-168">Reliable Services의 파티션 데이터 손실</span><span class="sxs-lookup"><span data-stu-id="f3718-168">Partition data loss in Reliable Services</span></span>
<span data-ttu-id="f3718-169">이 경우 hello 런타임은 자동으로 검색 hello 데이터 손실 및 hello 호출 `OnDataLossAsync` API입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-169">In this case, hello runtime would automatically detect hello data loss and invoke hello `OnDataLossAsync` API.</span></span>

<span data-ttu-id="f3718-170">hello 서비스 작성자 tooperform hello toorecover 다음 항목이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-170">hello service author needs tooperform hello following toorecover:</span></span>

  - <span data-ttu-id="f3718-171">Hello 가상 기본 클래스 메서드를 재정의 `OnDataLossAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-171">Override hello virtual base class method `OnDataLossAsync`.</span></span>
  - <span data-ttu-id="f3718-172">Hello 서비스의 백업이 포함 되어 있는 hello 외부 위치에 최신 백업 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-172">Find hello latest backup in hello external location that contains hello service's backups.</span></span>
  - <span data-ttu-id="f3718-173">최신 백업 hello 다운로드 (및 압축 된 경우 hello 백업 폴더로 hello 백업-압축 해제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-173">Download hello latest backup (and uncompress hello backup into hello backup folder if it was compressed).</span></span>
  - <span data-ttu-id="f3718-174">hello `OnDataLossAsync` 메서드는 제공 된 `RestoreContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-174">hello `OnDataLossAsync` method provides a `RestoreContext`.</span></span> <span data-ttu-id="f3718-175">Hello 호출 `RestoreAsync` API를 제공 하는 hello `RestoreContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-175">Call hello `RestoreAsync` API on hello provided `RestoreContext`.</span></span>
  - <span data-ttu-id="f3718-176">Hello 복원에 성공 하면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-176">Return true if hello restoration was a success.</span></span>

<span data-ttu-id="f3718-177">다음은 hello의 예제 구현은 `OnDataLossAsync` 메서드:</span><span class="sxs-lookup"><span data-stu-id="f3718-177">Following is an example implementation of hello `OnDataLossAsync` method:</span></span>

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

<span data-ttu-id="f3718-178">`RestoreDescription`전달 된 toohello `RestoreContext.RestoreAsync` 호출 라는 멤버가 포함 되어 `BackupFolderPath`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-178">`RestoreDescription` passed in toohello `RestoreContext.RestoreAsync` call contains a member called `BackupFolderPath`.</span></span>
<span data-ttu-id="f3718-179">1 회 전체 백업, 복원 하는 경우이 `BackupFolderPath` toohello 전체 백업을 포함 하는 hello 폴더의 로컬 경로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-179">When restoring a single full backup, this `BackupFolderPath` should be set toohello local path of hello folder that contains your full backup.</span></span>
<span data-ttu-id="f3718-180">전체 백업 및 증분 백업의 수를 복원할 때 `BackupFolderPath` toohello 뿐만 아니라가 포함 된 hello 전체 백업에도 모든 hello 증분 백업을 hello 폴더의 로컬 경로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-180">When restoring a full backup and a number of incremental backups, `BackupFolderPath` should be set toohello local path of hello folder that not only contains hello full backup, but also all hello incremental backups.</span></span>
<span data-ttu-id="f3718-181">`RestoreAsync`호출 발생 시킬 수 `FabricMissingFullBackupException` 경우 hello `BackupFolderPath` 제공 된 전체 백업을 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-181">`RestoreAsync` call can throw `FabricMissingFullBackupException` if hello `BackupFolderPath` provided does not contain a full backup.</span></span>
<span data-ttu-id="f3718-182">`BackupFolderPath`에서 증분 백업 체인이 끊겨 있으면 `ArgumentException`이 발생(throw)될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-182">It can also throw `ArgumentException` if `BackupFolderPath` has a broken chain of incremental backups.</span></span>
<span data-ttu-id="f3718-183">예를 들어 hello 전체 백업에 포함 된 경우 증분 먼저 hello 및 세 번째 증분 백업이 되었지만 hello 두 번째 증분 백업이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-183">For example, if it contains hello full backup, hello first incremental and hello third incremental backup but no hello second incremental backup.</span></span>

> [!NOTE]
> <span data-ttu-id="f3718-184">hello RestorePolicy는 tooSafe 기본적으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-184">hello RestorePolicy is set tooSafe by default.</span></span>  <span data-ttu-id="f3718-185">즉, 해당 hello `RestoreAsync` 해당 hello 백업 폴더에 상태는이 복제본에 포함 된 보다 오래 된 크거나 toohello 상태를 검색 하는 경우 API ArgumentException 하면서 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-185">This means that hello `RestoreAsync` API will fail with ArgumentException if it detects that hello backup folder contains a state that is older than or equal toohello state contained in this replica.</span></span>  <span data-ttu-id="f3718-186">`RestorePolicy.Force`사용 되는 tooskip이 안전 검사 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-186">`RestorePolicy.Force` can be used tooskip this safety check.</span></span> <span data-ttu-id="f3718-187">이는 `RestoreDescription`의 일부로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-187">This is specified as part of `RestoreDescription`.</span></span>
> 

## <a name="deleted-or-lost-service"></a><span data-ttu-id="f3718-188">서비스 삭제 또는 손상</span><span class="sxs-lookup"><span data-stu-id="f3718-188">Deleted or lost service</span></span>
<span data-ttu-id="f3718-189">서비스 제거 되는 경우 먼저 다시 만들어야 hello 서비스 전에 hello 데이터를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-189">If a service is removed, you must first re-create hello service before hello data can be restored.</span></span>  <span data-ttu-id="f3718-190">그는 hello 구성이 동일한 예: 데이터는 hello 하므로 파티션 구성표를 원활 하 게 복원할 수 있는 중요 한 toocreate hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-190">It is important toocreate hello service with hello same configuration, e.g., partitioning scheme, so that hello data can be restored seamlessly.</span></span>  <span data-ttu-id="f3718-191">Hello 서비스가 실행 중인지, 되 면 hello API toorestore 데이터 (`OnDataLossAsync` 위에) toobe이이 서비스의 모든 파티션에 호출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-191">Once hello service is up, hello API toorestore data (`OnDataLossAsync` above) has toobe invoked on every partition of this service.</span></span> <span data-ttu-id="f3718-192">이를 달성하는 한 가지 방법은 모든 파티션에서 `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-192">One way of achieving this is by using `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` on every partition.</span></span>  

<span data-ttu-id="f3718-193">이 시점부터 구현 시나리오 위에 hello와 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-193">From this point, implementation is hello same as hello above scenario.</span></span> <span data-ttu-id="f3718-194">각 파티션에 toorestore hello 최신 관련 백업 hello 외부 저장소에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-194">Each partition needs toorestore hello latest relevant backup from hello external store.</span></span> <span data-ttu-id="f3718-195">한 가지 주의할 점은 ID 지금 변경 hello 런타임에서는 파티션 Id를 동적으로 생성 하므로 해당 hello 파티션입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-195">One caveat is that hello partition ID may have now changed, since hello runtime creates partition IDs dynamically.</span></span> <span data-ttu-id="f3718-196">따라서 hello 서비스 각 파티션에 대해 toostore hello 적절 한 파티션 정보 및 서비스 이름 tooidentify hello 올바른 최신 백업 toorestore에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-196">Thus, hello service needs toostore hello appropriate partition information and service name tooidentify hello correct latest backup toorestore from for each partition.</span></span>

> [!NOTE]
> <span data-ttu-id="f3718-197">Toouse 좋습니다 `FabricClient.ServiceManager.InvokeDataLossAsync` 각 파티션 toorestore hello 전체 서비스에는 클러스터 상태가 손상 될 수 있으므로 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-197">It is not recommended toouse `FabricClient.ServiceManager.InvokeDataLossAsync` on each partition toorestore hello entire service, since that may corrupt your cluster state.</span></span>
> 

## <a name="replication-of-corrupt-application-data"></a><span data-ttu-id="f3718-198">손상된 응용 프로그램 데이터의 복제</span><span class="sxs-lookup"><span data-stu-id="f3718-198">Replication of corrupt application data</span></span>
<span data-ttu-id="f3718-199">새로 배포 된 hello 응용 프로그램 업그레이드 버그가 있는 데이터가 손상이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-199">If hello newly deployed application upgrade has a bug, that may cause corruption of data.</span></span> <span data-ttu-id="f3718-200">예를 들어 응용 프로그램 업그레이드에서에서 시작할 수 있습니다 tooupdate 모든 전화 번호 레코드가 잘못 된 지역 번호를 사용 하 여 신뢰할 수 있는 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-200">For example, an application upgrade may start tooupdate every phone number record in a Reliable Dictionary with an invalid area code.</span></span>  <span data-ttu-id="f3718-201">이 경우 서비스 패브릭 저장 되는 hello 데이터의 hello 특성의 인식할 수 없기 때문에 hello 전화 번호가 잘못 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-201">In this case, hello invalid phone numbers will be replicated since Service Fabric is not aware of hello nature of hello data that is being stored.</span></span>

<span data-ttu-id="f3718-202">hello 먼저 데이터를 손상 시키는 이러한 egregious 버그를 발견 하면 후 toodo toofreeze hello 서비스 hello 응용 프로그램 수준에서 이며, 가능 하면 toohello 버전의 hello 버그 없는 hello 응용 프로그램 코드를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-202">hello first thing toodo after you detect such an egregious bug that causes data corruption is toofreeze hello service at hello application level and, if possible, upgrade toohello version of hello application code that does not have hello bug.</span></span>  <span data-ttu-id="f3718-203">그러나 hello 서비스 코드를 해결 한 후에 hello 데이터 손상 되었을 수 있습니다 및 데이터 복원 toobe를 할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-203">However, even after hello service code is fixed, hello data may still be corrupt and thus data may need toobe restored.</span></span>  <span data-ttu-id="f3718-204">않을 이러한 경우 하지 수 있습니다 충분 한 toorestore hello 최신 백업, 이후 hello 최신 백업도 손상 되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-204">In such cases, it may not be sufficient toorestore hello latest backup, since hello latest backups may also be corrupt.</span></span>  <span data-ttu-id="f3718-205">따라서 hello 데이터 손상 (를) 가져왔습니다 전에 만든 toofind hello 마지막 백업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-205">Thus, you have toofind hello last backup that was made before hello data got corrupted.</span></span>

<span data-ttu-id="f3718-206">새 서비스 패브릭 클러스터를 배포 하 고 "삭제 됨 또는 손실된 서비스" 위에 hello와 동일 하 게 영향을 받는 파티션 hello 백업을 복원할 수 손상 된 백업을 확실 하지 않은 경우 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-206">If you are not sure which backups are corrupt, you could deploy a new Service Fabric cluster and restore hello backups of affected partitions just like hello above "Deleted or lost service" scenario.</span></span>  <span data-ttu-id="f3718-207">각 파티션에 대해 최소 hello 가장 최근의 toohello에서 hello 백업 복원을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-207">For each partition, start restoring hello backups from hello most recent toohello least.</span></span> <span data-ttu-id="f3718-208">Hello 손상 하지 않은 백업을 찾으면 이동/삭제 된 백업) (보다 최신이 파티션의 모든 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-208">Once you find a backup that does not have hello corruption, move/delete all backups of this partition that were more recent (than that backup).</span></span> <span data-ttu-id="f3718-209">각 파티션에 대해 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-209">Repeat this process for each partition.</span></span> <span data-ttu-id="f3718-210">이제, `OnDataLossAsync` 라고 hello 프로덕션 클러스터의 hello 파티션에 hello 마지막 백업 있는 hello 외부 저장소 프로세스 위에 hello 하 여 hello 하나 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-210">Now, when `OnDataLossAsync` is called on hello partition in hello production cluster, hello last backup found in hello external store will be hello one picked by hello above process.</span></span>

<span data-ttu-id="f3718-211">Hello hello "삭제 됨 또는 손실된 서비스"의 단계를 이제 섹션 수 hello 오류가 있는 코드가 손상 된 hello 상태 전에 hello 서비스 toohello 상태의 toorestore hello 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-211">Now, hello steps in hello "Deleted or lost service" section can be used toorestore hello state of hello service toohello state before hello buggy code corrupted hello state.</span></span>

<span data-ttu-id="f3718-212">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="f3718-212">Note that:</span></span>

  - <span data-ttu-id="f3718-213">를 복원 하면 hello 백업 하는 데 사용 되 고지 않습니다 복원가 hello 파티션의 hello 상태 보다 오래 전에 hello 데이터가 손실 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-213">When you restore, there is a chance that hello backup being restored is older than hello state of hello partition before hello data was lost.</span></span> <span data-ttu-id="f3718-214">이 때문에 복원 해야 마지막 수단 toorecover로만 많은 데이터 최대한.</span><span class="sxs-lookup"><span data-stu-id="f3718-214">Because of this, you should restore only as a last resort toorecover as much data as possible.</span></span>
  - <span data-ttu-id="f3718-215">hello 백업 폴더 경로 나타내는 문자열 hello hello hello 백업 폴더 내 파일의 경로 수 있으며 hello FabricDataRoot 경로 및 응용 프로그램 종류 이름 길이 따라 255 자를 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-215">hello string that represents hello backup folder path and hello paths of files inside hello backup folder can be greater than 255 characters, depending on hello FabricDataRoot path and Application Type name's length.</span></span> <span data-ttu-id="f3718-216">따라서 일부.NET 메서드를 같은 발생할 수 있습니다 `Directory.Move`, toothrow hello `PathTooLongException` 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-216">This can cause some .NET methods, like `Directory.Move`, toothrow hello `PathTooLongException` exception.</span></span> <span data-ttu-id="f3718-217">한 가지 해결 방법은 toodirectly kernel32 Api와 같은 호출 `CopyFile`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-217">One workaround is toodirectly call kernel32 APIs, like `CopyFile`.</span></span>

## <a name="backup-and-restore-reliable-actors"></a><span data-ttu-id="f3718-218">Reliable Actors 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="f3718-218">Backup and restore Reliable Actors</span></span>


<span data-ttu-id="f3718-219">Reliable Actors 프레임워크는 Reliable Services를 기반으로 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-219">Reliable Actors Framework is built on top of Reliable Services.</span></span> <span data-ttu-id="f3718-220">hello ActorService hello actor(s)를 호스트 하는 상태 저장 신뢰할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-220">hello ActorService which hosts hello actor(s) is a stateful reliable service.</span></span> <span data-ttu-id="f3718-221">따라서 모든 hello 백업 및 복원 기능을 신뢰할 수 있는 서비스에서 사용할 수 있는 사용 가능한 tooReliable 행위자 (제외 동작에 특정 상태 공급자) 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-221">Hence, all hello backup and restore functionality available in Reliable Services is also available tooReliable Actors (except behaviors that are state provider specific).</span></span> <span data-ttu-id="f3718-222">백업이 파티션 단위로 수행되기 때문에 파티션에서 모든 행위자에 대한 상태는 백업됩니다(또한 복원은 비슷하고 파티션 기준으로 발생함).</span><span class="sxs-lookup"><span data-stu-id="f3718-222">Since backups will be taken on a per-partition basis, states for all actors in that partition will be backed up (and restoration is similar and will happen on a per-partition basis).</span></span> <span data-ttu-id="f3718-223">tooperform 백업/복원, hello 서비스 소유자 ActorService 클래스에서 파생 된 사용자 지정 행위자 서비스 클래스를 만들어야 및 다음 수행 백업/복원 비슷한 tooReliable 이전 섹션에서 설명한 것과 같이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-223">tooperform backup/restore, hello service owner should create a custom actor service class that derives from ActorService class and then do backup/restore similar tooReliable Services as described above in previous sections.</span></span>

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

<span data-ttu-id="f3718-224">사용자 지정 행위자 서비스 클래스를 만들면 hello 행위자를 등록할 때 tooregister도 즉가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-224">When you create a custom actor service class, you need tooregister that as well when registering hello actor.</span></span>

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

<span data-ttu-id="f3718-225">Reliable Actors에 대 한 hello 기본 상태 공급자는 `KvsActorStateProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-225">hello default state provider for Reliable Actors is `KvsActorStateProvider`.</span></span> <span data-ttu-id="f3718-226">`KvsActorStateProvider`에 대한 증분 백업은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-226">Incremental backup is not enabled by default for `KvsActorStateProvider`.</span></span> <span data-ttu-id="f3718-227">증분 백업을 사용 하도록 설정할 만들어 수 `KvsActorStateProvider` 적절 한 생성자에서 설정 하 고 다음 코드 조각에 나와 있는 것 처럼 tooActorService 생성자 전달 hello로:</span><span class="sxs-lookup"><span data-stu-id="f3718-227">You can enable incremental backup by creating `KvsActorStateProvider` with hello appropriate setting in its constructor and then passing it tooActorService constructor as shown in following code snippet:</span></span>

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

<span data-ttu-id="f3718-228">증분 백업에 설정한 후 다음 이유 중 하나로 FabricMissingFullBackupException 실패할 수 증분 백업을 수행 및 증분 백업을 수행 하기 전에 전체 백업을 tootake 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-228">After incremental backup has been enabled, taking an incremental backup can fail with FabricMissingFullBackupException for one of following reasons and you will need tootake a full backup before taking incremental backup(s):</span></span>

  - <span data-ttu-id="f3718-229">기본 된 이후의 hello 복제본에 전체 백업을 수행 하지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-229">hello replica has never taken a full backup since it became primary.</span></span>
  - <span data-ttu-id="f3718-230">Hello 로그 레코드의 일부를 마지막 백업 이후에 잘렸습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-230">Some of hello log records were truncated since last backup was taken.</span></span>

<span data-ttu-id="f3718-231">증분 백업을 사용 하는 경우 `KvsActorStateProvider` 순환 버퍼 toomanage 해당 로그를 기록 하 고 주기적으로 자동으로 잘립니다를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-231">When incremental backup is enabled, `KvsActorStateProvider` does not use circular buffer toomanage its log records and periodically truncates it.</span></span> <span data-ttu-id="f3718-232">사용 된 경우 백업이 없는 사용자가 45 분 동안에 대 한 hello 시스템 hello 로그 레코드를 자동으로 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-232">If no backup is taken by user for a period of 45 minutes, hello system automatically truncates hello log records.</span></span> <span data-ttu-id="f3718-233">이 간격을 지정 하 여 구성할 수 있습니다 `logTrunctationIntervalInMinutes` 에 `KvsActorStateProvider` 생성자 (유사한 toowhen 증분 백업을 사용 하도록 설정).</span><span class="sxs-lookup"><span data-stu-id="f3718-233">This interval can be configured by specifying `logTrunctationIntervalInMinutes` in `KvsActorStateProvider` constructor (similar toowhen enabling incremental backup).</span></span> <span data-ttu-id="f3718-234">hello 로그 레코드가 주 복제본이 필요 toobuild 다른 복제본의 모든 데이터를 전송 하 여 잘릴 가져올 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-234">hello log records may also get truncated if primary replica need toobuild another replica by sending all its data.</span></span>

<span data-ttu-id="f3718-235">백업 체인, 비슷한 tooReliable 서비스에서 복원을 수행할 때 hello BackupFolderPath 전체 백업 및 기타 증분 백업을 포함 하는 하위 디렉터리를 포함 하는 하나의 하위 디렉터리의 하위 디렉터리를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-235">When doing restore from a backup chain, similar tooReliable Services, hello BackupFolderPath should contain subdirectories with one subdirectory containing full backup and others subdirectories containing incremental backup(s).</span></span> <span data-ttu-id="f3718-236">hello 복원 API hello 백업 체인의 유효성 검사가 실패 하면 적절 한 오류 메시지와 함께 FabricException을 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-236">hello restore API will throw FabricException with appropriate error message if hello backup chain validation fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="f3718-237">`KvsActorStateProvider`현재 RestorePolicy.Safe hello 옵션을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-237">`KvsActorStateProvider` currently ignores hello option RestorePolicy.Safe.</span></span> <span data-ttu-id="f3718-238">이 기능은 이후 릴리스에서 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-238">Support for this feature is planned in an upcoming release.</span></span>
> 

## <a name="testing-backup-and-restore"></a><span data-ttu-id="f3718-239">테스트 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="f3718-239">Testing Backup and Restore</span></span>
<span data-ttu-id="f3718-240">것이 중요 한 tooensure는 중요 한 데이터 백업 되 고, 및에서 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-240">It is important tooensure that critical data is being backed up, and can be restored from.</span></span> <span data-ttu-id="f3718-241">Hello를 호출 하 여이 작업을 수행할 수 있습니다 `Start-ServiceFabricPartitionDataLoss` 여부 hello 데이터 백업 및 복원 기능을 정상적으로 작동 하 여 서비스에 대 한 특정 파티션 tootest에 데이터 손실의 유도할 수 있는 PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f3718-241">This can be done by invoking hello `Start-ServiceFabricPartitionDataLoss` cmdlet in PowerShell that can induce data loss in a particular partition tootest whether hello data backup and restore functionality for your service is working as expected.</span></span>  <span data-ttu-id="f3718-242">가능한 tooprogrammatically 이기도 데이터 손실을 호출 하 고 해당 이벤트에도에서 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-242">It is also possible tooprogrammatically invoke data loss and restore from that event as well.</span></span>

> [!NOTE]
> <span data-ttu-id="f3718-243">백업의 샘플 구현의 찾 및 hello GitHub에 웹 참조 응용 프로그램의에서 기능을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-243">You can find a sample implementation of backup and restore functionality in hello Web Reference App on GitHub.</span></span> <span data-ttu-id="f3718-244">Hello 살펴본 `Inventory.Service` 자세한 세부 정보에 대 한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-244">Please look at hello `Inventory.Service` service for more details.</span></span>
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a><span data-ttu-id="f3718-245">Hello 내부적: 백업 및 복원에 대 한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="f3718-245">Under hello hood: more details on backup and restore</span></span>
<span data-ttu-id="f3718-246">다음은 백업 및 복원에 대한 자세한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-246">Here's some more details on backup and restore.</span></span>

### <a name="backup"></a><span data-ttu-id="f3718-247">백업</span><span class="sxs-lookup"><span data-stu-id="f3718-247">Backup</span></span>
<span data-ttu-id="f3718-248">신뢰할 수 있는 상태 관리자 hello hello 기능 toocreate 차단 하지 않고 일관 된 백업을 읽기 또는 쓰기 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-248">hello Reliable State Manager provides hello ability toocreate consistent backups without blocking any read or write operations.</span></span> <span data-ttu-id="f3718-249">toodo, 검사점 및 로그 지 속성 메커니즘을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-249">toodo so, it utilizes a checkpoint and log persistence mechanism.</span></span>  <span data-ttu-id="f3718-250">hello 신뢰할 수 있는 상태 관리자 hello 트랜잭션 로그에서 특정 지점 toorelieve 압력에 유사 항목 (경량) 검사점 걸리며 복구 시간을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-250">hello Reliable State Manager takes fuzzy (lightweight) checkpoints at certain points toorelieve pressure from hello transactional log and improve recovery times.</span></span>  <span data-ttu-id="f3718-251">때 `BackupAsync` hello 신뢰할 수 있는 상태 관리자의 최신 검사점 파일 tooa 로컬 백업 폴더에 모든 신뢰할 수 있는 개체 toocopy 지시 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-251">When `BackupAsync` is called, hello Reliable State Manager instructs all Reliable objects toocopy their latest checkpoint files tooa local backup folder.</span></span>  <span data-ttu-id="f3718-252">그런 다음 신뢰할 수 있는 상태 관리자 hello hello 백업 폴더로 hello "포인터 시작" toohello 최신 로그 레코드부터 시작 하는 모든 로그 레코드를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-252">Then, hello Reliable State Manager copies all log records, starting from hello "start pointer" toohello latest log record into hello backup folder.</span></span>  <span data-ttu-id="f3718-253">Toohello 최신 로그 레코드를 모든 hello 로그 레코드는 hello 백업에 포함 되어 있으므로 hello 신뢰할 수 있는 상태 관리자 미리 쓰기 로깅을 유지 hello 신뢰할 수 있는 상태 관리자 내용이 취소 되도록 모든 트랜잭션이 있는 커밋된 (`CommitAsync` 를 반환 했습니다. 성공적으로) hello 백업에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-253">Since all hello log records up toohello latest log record are included in hello backup and hello Reliable State Manager preserves write-ahead logging, hello Reliable State Manager guarantees that all transactions that are committed (`CommitAsync` has returned successfully) are included in hello backup.</span></span>

<span data-ttu-id="f3718-254">후 커밋되는 모든 트랜잭션이 `BackupAsync` 년 5 월 호출한 또는 hello 백업에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-254">Any transaction that commits after `BackupAsync` has been called may or may not be in hello backup.</span></span>  <span data-ttu-id="f3718-255">로컬 백업 폴더 hello hello 플랫폼에 따라 채워진 후 (즉, 로컬 백업 완료 된 hello 런타임에서), 백업 hello 서비스 콜백이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-255">Once hello local backup folder has been populated by hello platform (i.e., local backup is completed by hello runtime), hello service's backup callback is invoked.</span></span>  <span data-ttu-id="f3718-256">이 콜백은 hello 백업 폴더 tooan Azure 저장소와 같은 외부 위치를 이동 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-256">This callback is responsible for moving hello backup folder tooan external location such as Azure Storage.</span></span>

### <a name="restore"></a><span data-ttu-id="f3718-257">복원</span><span class="sxs-lookup"><span data-stu-id="f3718-257">Restore</span></span>
<span data-ttu-id="f3718-258">hello 신뢰할 수 있는 상태 관리자는 hello 기능 toorestore 백업에서 사용 하 여 hello `RestoreAsync` API입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-258">hello Reliable State Manager provides hello ability toorestore from a backup by using hello `RestoreAsync` API.</span></span>  
<span data-ttu-id="f3718-259">hello `RestoreAsync` 메서드를 `RestoreContext` hello 내부 에서만 호출할 수 `OnDataLossAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f3718-259">hello `RestoreAsync` method on `RestoreContext` can be called only inside hello `OnDataLossAsync` method.</span></span>
<span data-ttu-id="f3718-260">반환 된 bool hello `OnDataLossAsync` hello 서비스 외부 소스에서 해당 상태를 복원 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-260">hello bool returned by `OnDataLossAsync` indicates whether hello service restored its state from an external source.</span></span>
<span data-ttu-id="f3718-261">경우 hello `OnDataLossAsync` 서비스 패브릭에서이 기본 다른 모든 복제본을 다시 작성 됩니다 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-261">If hello `OnDataLossAsync` returns true, Service Fabric will rebuild all other replicas from this primary.</span></span> <span data-ttu-id="f3718-262">서비스 패브릭 되도록 복제를 수신할 `OnDataLossAsync` 첫 번째 전환 toohello 주 역할을 호출 하지만 부여 상태를 읽지 않습니다 또는 상태를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-262">Service Fabric ensures that replicas that will receive `OnDataLossAsync` call first transition toohello primary role but are not granted read status or write status.</span></span>
<span data-ttu-id="f3718-263">즉 `OnDataLossAsync`가 성공적으로 완료될 때까지 StatefulService 구현자에 대해 `RunAsync`가 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-263">This implies that for StatefulService implementers, `RunAsync` will not be called until `OnDataLossAsync` finishes successfully.</span></span>
<span data-ttu-id="f3718-264">그런 다음 `OnDataLossAsync` hello 새 주 복제본에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-264">Then, `OnDataLossAsync` will be invoked on hello new primary.</span></span>
<span data-ttu-id="f3718-265">서비스를 성공적으로 (반환 하 여 true 또는 false)이이 API를 완료 hello 관련 재구성을 완료 될 때까지 hello API는 유지 되 고 호출 한 번에 하나씩.</span><span class="sxs-lookup"><span data-stu-id="f3718-265">Until a service completes this API successfully (by returning true or false) and finishes hello relevant reconfiguration, hello API will keep being called one at a time.</span></span>

<span data-ttu-id="f3718-266">`RestoreAsync`먼저 주 복제본에서 호출 된 hello에서 모든 기존 상태를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-266">`RestoreAsync` first drops all existing state in hello primary replica that it was called on.</span></span>  
<span data-ttu-id="f3718-267">그런 다음 hello 신뢰할 수 있는 상태 관리자는 hello 백업 폴더에 있는 모든 hello 신뢰할 수 있는 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-267">Then hello Reliable State Manager creates all hello Reliable objects that exist in hello backup folder.</span></span>  
<span data-ttu-id="f3718-268">다음으로 hello 신뢰할 수 있는 개체는 hello 백업 폴더에 해당 검사점에서 지시 toorestore입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-268">Next, hello Reliable objects are instructed toorestore from their checkpoints in hello backup folder.</span></span>  
<span data-ttu-id="f3718-269">마지막으로, 신뢰할 수 있는 상태 관리자 hello hello 백업 폴더의 로그 레코드 hello에서 자체의 상태를 복구 하 고 복구를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-269">Finally, hello Reliable State Manager recovers its own state from hello log records in hello backup folder and performs recovery.</span></span>  
<span data-ttu-id="f3718-270">Hello 복구 프로세스의 일환으로, 커밋 로그 레코드가 hello 백업 폴더에 있어야 하는 hello "시작점"에서 시작 하는 작업은 재생된 toohello 신뢰할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-270">As part of hello recovery process, operations starting from hello "starting point" that have commit log records in hello backup folder are replayed toohello Reliable objects.</span></span>  
<span data-ttu-id="f3718-271">이 단계를 수행 하면 해당 hello 복구 된 상태가 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3718-271">This step ensures that hello recovered state is consistent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3718-272">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3718-272">Next steps</span></span>
  - [<span data-ttu-id="f3718-273">신뢰할 수 있는 컬렉션</span><span class="sxs-lookup"><span data-stu-id="f3718-273">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
  - [<span data-ttu-id="f3718-274">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="f3718-274">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  - [<span data-ttu-id="f3718-275">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="f3718-275">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
  - [<span data-ttu-id="f3718-276">Reliable Services 구성</span><span class="sxs-lookup"><span data-stu-id="f3718-276">Reliable Services configuration</span></span>](service-fabric-reliable-services-configuration.md)
  - [<span data-ttu-id="f3718-277">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="f3718-277">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

