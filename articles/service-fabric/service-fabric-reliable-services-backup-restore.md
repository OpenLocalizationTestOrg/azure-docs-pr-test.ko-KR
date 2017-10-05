---
title: "Service Fabric 백업 및 복원 | Microsoft Docs"
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
ms.openlocfilehash: 4242962e7e03053ef25f198a0b2f6c8012e693eb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a><span data-ttu-id="69c98-103">Reliable Services 및 Reliable Actors 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="69c98-103">Back up and restore Reliable Services and Reliable Actors</span></span>
<span data-ttu-id="69c98-104">Azure 서비스 패브릭은 여러 노드에 걸쳐 상태를 복제하여 고가용성을 유지하는 고가용성 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-104">Azure Service Fabric is a high-availability platform that replicates the state across multiple nodes to maintain this high availability.</span></span>  <span data-ttu-id="69c98-105">따라서 클러스터의 한 노드에서 오류가 발생해도 서비스를 지속적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-105">Thus, even if one node in the cluster fails, the services continue to be available.</span></span> <span data-ttu-id="69c98-106">많은 경우 플랫폼에서 제공하는 이러한 기본 제공 중복성으로 충분하지만 어떤 경우에는 서비스를 위해 (외부 저장소에) 데이터를 백업하는 것이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-106">While this in-built redundancy provided by the platform may be sufficient for some, in certain cases it is desirable for the service to back up data (to an external store).</span></span>

> [!NOTE]
> <span data-ttu-id="69c98-107">데이터 손실 시나리오에서 복구할 수 있도록 데이터를 백업 및 복원(및 예상대로 작동하는지 테스트)하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-107">It is critical to backup and restore your data (and test that it works as expected) so you can recover from data loss scenarios.</span></span>
> 
> 

<span data-ttu-id="69c98-108">예를 들어 서비스에서 다음과 같은 시나리오로부터 보호하기 위해 데이터를 백업하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-108">For example, a service may want to back up data in order to protect from the following scenarios:</span></span>

- <span data-ttu-id="69c98-109">Service Fabric 클러스터 전체가 영구적으로 손실되는 경우</span><span class="sxs-lookup"><span data-stu-id="69c98-109">In the event of the permanent loss of an entire Service Fabric cluster.</span></span>
- <span data-ttu-id="69c98-110">서비스 파티션의 복제본 대다수가 영구적으로 손실되는 경우</span><span class="sxs-lookup"><span data-stu-id="69c98-110">Permanent loss of a majority of the replicas of a service partition</span></span>
- <span data-ttu-id="69c98-111">상태가 우발적으로 삭제되거나 손상된 관리 오류.</span><span class="sxs-lookup"><span data-stu-id="69c98-111">Administrative errors whereby the state accidentally gets deleted or corrupted.</span></span> <span data-ttu-id="69c98-112">예를 들어 충분한 권한이 있는 관리자가 실수로 서비스를 삭제한 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-112">For example, this may happen if an administrator with sufficient privilege erroneously deletes the service.</span></span>
- <span data-ttu-id="69c98-113">데이터 손상을 초래하는 서비스 내 버그.</span><span class="sxs-lookup"><span data-stu-id="69c98-113">Bugs in the service that cause data corruption.</span></span> <span data-ttu-id="69c98-114">예를 들어 신뢰할 수 있는 컬렉션에 잘못된 데이터 작성을 시작하는 서비스 코드가 업그레이드되는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-114">For example, this may happen when a service code upgrade starts writing faulty data to a Reliable Collection.</span></span> <span data-ttu-id="69c98-115">이런 경우 코드와 데이터 모두 이전 상태로 되돌아가야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-115">In such a case, both the code and the data may have to be reverted to an earlier state.</span></span>
- <span data-ttu-id="69c98-116">오프라인 데이터 처리.</span><span class="sxs-lookup"><span data-stu-id="69c98-116">Offline data processing.</span></span> <span data-ttu-id="69c98-117">데이터를 생성하는 서비스와는 별도로 비즈니스 인텔리전스를 위한 데이터를 오프라인 처리하는 것이 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-117">It might be convenient to have offline processing of data for business intelligence that happens separately from the service that generates the data.</span></span>

<span data-ttu-id="69c98-118">백업/복원 기능을 사용하면 Reliable Services API에 구축된 서비스로 백업을 만들고 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-118">The Backup/Restore feature allows services built on the Reliable Services API to create and restore backups.</span></span> <span data-ttu-id="69c98-119">플랫폼에서 제공하는 백업 API를 사용하면 읽기 또는 쓰기 작업을 차단하지 않고 서비스 파티션 상태를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-119">The backup APIs provided by the platform allow backup(s) of a service partition's state, without blocking read or write operations.</span></span> <span data-ttu-id="69c98-120">복원 API를 사용하면 선택한 백업에서 서비스 파티션의 상태를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-120">The restore APIs allow a service partition's state to be restored from a chosen backup.</span></span>

## <a name="types-of-backup"></a><span data-ttu-id="69c98-121">백업 유형</span><span class="sxs-lookup"><span data-stu-id="69c98-121">Types of Backup</span></span>
<span data-ttu-id="69c98-122">백업 옵션에는 전체 및 증분이라는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-122">There are two backup options: Full and Incremental.</span></span>
<span data-ttu-id="69c98-123">전체 백업은 검사점 및 모든 로그 레코드처럼 복제본의 상태를 다시 만드는 데 필요한 모든 데이터를 포함하는 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-123">A full backup is a backup that contains all the data required to recreate the state of the replica: checkpoints and all log records.</span></span>
<span data-ttu-id="69c98-124">전체 백업은 검사점 및 로그를 포함하므로 자체적으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-124">Since it has the checkpoints and the log, a full backup can be restored by itself.</span></span>

<span data-ttu-id="69c98-125">전체 백업에서는 검사점이 큰 경우에 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-125">The problem with full backups arises when the checkpoints are large.</span></span>
<span data-ttu-id="69c98-126">예를 들어 16GB의 상태가 있는 복제본은 약 16GB까지 추가되는 검사점을 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-126">For example, a replica that has 16 GB of state will have checkpoints that add up approximately to 16 GB.</span></span>
<span data-ttu-id="69c98-127">복구 지점 목표가 5분인 경우 복제본을 5분마다 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-127">If we have a Recovery Point Objective of five minutes, the replica needs to be backed up every five minutes.</span></span>
<span data-ttu-id="69c98-128">백업할 때마다 50MB(`CheckpointThresholdInMB`를 사용하여 구성 가능)의 로그 외에도 16GB의 검사점을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-128">Each time it backs up it needs to copy 16 GB of checkpoints in addition to 50 MB (configurable using `CheckpointThresholdInMB`) worth of logs.</span></span>

![전체 백업 예입니다.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

<span data-ttu-id="69c98-130">이 문제에 대한 해결 방법은 증분 백업입니다. 여기서 백업에는 마지막 백업 이후에 변경된 로그 레코드만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-130">The solution to this problem is incremental backups, where backup only contains the changed log records since the last backup.</span></span>

![증분 백업 예입니다.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

<span data-ttu-id="69c98-132">증분 백업은 마지막 백업 이후 변경 사항만 백업(검사점은 포함하지 않음)하므로 속도는 더 빠르지만 자체적으로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-132">Since incremental backups are only changes since the last backup (does not include the checkpoints), they tend to be faster but they cannot be restored on their own.</span></span>
<span data-ttu-id="69c98-133">증분 백업을 복원하려면 전체 백업 체인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-133">To restore an incremental backup, the entire backup chain is required.</span></span>
<span data-ttu-id="69c98-134">백업 체인은 전체 백업으로 시작하여 이후 수많은 지속적인 증분 백업이 이어지는 백업의 체인입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-134">A backup chain is a chain of backups starting with a full backup and followed by a number of contiguous incremental backups.</span></span>

## <a name="backup-reliable-services"></a><span data-ttu-id="69c98-135">Reliable Services 백업</span><span class="sxs-lookup"><span data-stu-id="69c98-135">Backup Reliable Services</span></span>
<span data-ttu-id="69c98-136">서비스 작성자에는 백업 수행 시기와 백업 저장 위치에 대한 모든 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-136">The service author has full control of when to make backups and where backups will be stored.</span></span>

<span data-ttu-id="69c98-137">백업을 시작하려면 서비스에서 상속된 `BackupAsync` 멤버 함수를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-137">To start a backup, the service needs to invoke the inherited member function `BackupAsync`.</span></span>  
<span data-ttu-id="69c98-138">백업은 주 복제본에서만 수행되며 상태 쓰기 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-138">Backups can be made only from primary replicas, and they require write status to be granted.</span></span>

<span data-ttu-id="69c98-139">아래와 같이 `BackupAsync`는 `BackupDescription` 개체를 가져오며, 여기서는 `Func<< BackupInfo, CancellationToken, Task<bool>>>` 콜백 함수뿐만 아니라 전체 또는 증분 백업도 지정할 수 있습니다. 이 함수는 백업 폴더를 로컬로 만들 때 호출되고 일부 외부 저장소로 이동할 준비가 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-139">As shown below, `BackupAsync` takes in a `BackupDescription` object, where one can specify a full or incremental backup, as well as a callback function, `Func<< BackupInfo, CancellationToken, Task<bool>>>` that is invoked when the backup folder has been created locally and is ready to be moved out to some external storage.</span></span>

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

<span data-ttu-id="69c98-140">증분 백업을 수행하도록 요구하는 요청은 `FabricMissingFullBackupException`으로 인해 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-140">Request to take an incremental backup can fail with `FabricMissingFullBackupException`.</span></span> <span data-ttu-id="69c98-141">이 예외는 다음 중 하나가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-141">This exception indicates that one of the following things is happening:</span></span>

- <span data-ttu-id="69c98-142">이는 복제본이 전체 백업을 아예 가져올 수 없거나</span><span class="sxs-lookup"><span data-stu-id="69c98-142">the replica has never taken a full backup since it has become primary,</span></span>
- <span data-ttu-id="69c98-143">마지막 백업 이후 일부 로그 레코드가 잘렸거나</span><span class="sxs-lookup"><span data-stu-id="69c98-143">some of the log records since the last backup has been truncated or</span></span>
- <span data-ttu-id="69c98-144">복제본이 `MaxAccumulatedBackupLogSizeInMB` 제한을 초과했습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-144">replica passed the `MaxAccumulatedBackupLogSizeInMB` limit.</span></span>

<span data-ttu-id="69c98-145">사용자는 `MinLogSizeInMB` 또는 `TruncationThresholdFactor`를 구성하여 증분 백업을 수행할 수 있는 가능성을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-145">Users can increase the likelihood of being able to do incremental backups by configuring `MinLogSizeInMB` or `TruncationThresholdFactor`.</span></span>
<span data-ttu-id="69c98-146">이러한 값을 늘리면 복제본당 디스크 사용량이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-146">Note that increasing these values increases the per replica disk usage.</span></span>
<span data-ttu-id="69c98-147">자세한 내용은 [Reliable Services 구성](service-fabric-reliable-services-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c98-147">For more information, see [Reliable Services Configuration](service-fabric-reliable-services-configuration.md)</span></span>

<span data-ttu-id="69c98-148">`BackupInfo`는 런타임에서 백업을 저장한 폴더의 위치(`BackupInfo.Directory`)를 포함하여 백업과 관련된 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-148">`BackupInfo` provides information regarding the backup, including the location of the folder where the runtime saved the backup (`BackupInfo.Directory`).</span></span> <span data-ttu-id="69c98-149">콜백 함수는 `BackupInfo.Directory`를 외부 저장소 또는 다른 위치로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-149">The callback function can move the `BackupInfo.Directory` to an external store or another location.</span></span>  <span data-ttu-id="69c98-150">이 함수는 백업 폴더를 대상 위치로 이동할 수 있는지 여부를 표시하는 부울 값도 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-150">This function also returns a bool that indicates whether it was able to successfully move the backup folder to its target location.</span></span>

<span data-ttu-id="69c98-151">다음 코드에서는 `BackupCallbackAsync` 메서드를 사용하여 Azure Storage에 백업을 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-151">The following code demonstrates how the `BackupCallbackAsync` method can be used to upload the backup to Azure Storage:</span></span>

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

<span data-ttu-id="69c98-152">위의 예제에서 `ExternalBackupStore`는 Azure Blob 저장소와의 인터페이스에 사용되는 샘플 클래스이고, `UploadBackupFolderAsync`는 폴더를 압축하여 Azure Blob 저장소에 배치하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-152">In the preceeding example, `ExternalBackupStore` is the sample class that is used to interface with Azure Blob storage, and `UploadBackupFolderAsync` is the method that compresses the folder and places it in the Azure Blob store.</span></span>

<span data-ttu-id="69c98-153">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="69c98-153">Note that:</span></span>

  - <span data-ttu-id="69c98-154">특정 시점에서 처리 중인 복제본 당 하나의 백업 작업만이 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-154">There can be only one backup operation in-flight per replica at any given time.</span></span> <span data-ttu-id="69c98-155">한 번에 둘 이상의 `BackupAsync` 호출은 처리 중인 백업을 하나로 제한하기 위해 `FabricBackupInProgressException`이 발생됩니다(throw).</span><span class="sxs-lookup"><span data-stu-id="69c98-155">More than one `BackupAsync` call at a time will throw `FabricBackupInProgressException` to limit inflight backups to one.</span></span>
  - <span data-ttu-id="69c98-156">백업 진행 중에 복제본 장애 조치가 발생하면 백업이 완료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-156">If a replica fails over while a backup is in progress, the backup may not have been completed.</span></span> <span data-ttu-id="69c98-157">따라서 장애 조치가 완료되면 서비스에서 필요에 따라 `BackupAsync`를 호출하여 백업을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-157">Thus, once the failover finishes, it is the service's responsibility to restart the backup by invoking `BackupAsync` as necessary.</span></span>

## <a name="restore-reliable-services"></a><span data-ttu-id="69c98-158">Reliable Services 복원</span><span class="sxs-lookup"><span data-stu-id="69c98-158">Restore Reliable Services</span></span>
<span data-ttu-id="69c98-159">일반적으로 복원 작업을 수행해야 하는 경우는 다음 범주 중 하나에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-159">In general, the cases when you might need to perform a restore operation fall into one of these categories:</span></span>

  - <span data-ttu-id="69c98-160">서비스 파티션에서 데이터가 손실되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-160">The service partition lost data.</span></span> <span data-ttu-id="69c98-161">예를 들어, 파티션에 대한 세 복제본 중 두 복제본(주 복제본 포함)에 대한 디스크가 손상되거나 초기화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-161">For example, the disk for two out of three replicas for a partition (including the primary replica) gets corrupted or wiped.</span></span> <span data-ttu-id="69c98-162">새 주 복제본이 백업에서 데이터를 복원해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-162">The new primary may need to restore data from a backup.</span></span>
  - <span data-ttu-id="69c98-163">전체 서비스가 손실되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-163">The entire service is lost.</span></span> <span data-ttu-id="69c98-164">예를 들어, 관리자가 전체 서비스를 제거하여 서비스와 데이터를 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-164">For example, an administrator removes the entire service and thus the service and the data need to be restored.</span></span>
  - <span data-ttu-id="69c98-165">서비스가 손상된 응용 프로그래 데이터를 복제했습니다.(예: 응용 프로그램 버그 때문에)</span><span class="sxs-lookup"><span data-stu-id="69c98-165">The service replicated corrupt application data (e.g., because of an application bug).</span></span> <span data-ttu-id="69c98-166">이 경우 손상 원인을 제거하기 위해 서비스를 업그레이드하거나 되돌려야 하며 손상되지 않은 데이터를 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-166">In this case, the service has to be upgraded or reverted to remove the cause of the corruption, and non-corrupt data has to be restored.</span></span>

<span data-ttu-id="69c98-167">다양한 방법이 가능하지만, 위의 시나리오에서 `RestoreAsync`를 사용하여 복구하는 몇 가지 예제를 제공하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-167">While many approaches are possible, we offer some examples on using `RestoreAsync` to recover from the above scenarios.</span></span>

## <a name="partition-data-loss-in-reliable-services"></a><span data-ttu-id="69c98-168">Reliable Services의 파티션 데이터 손실</span><span class="sxs-lookup"><span data-stu-id="69c98-168">Partition data loss in Reliable Services</span></span>
<span data-ttu-id="69c98-169">이 경우 런타임에서 자동으로 데이터 손실을 검색하고 `OnDataLossAsync` API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-169">In this case, the runtime would automatically detect the data loss and invoke the `OnDataLossAsync` API.</span></span>

<span data-ttu-id="69c98-170">서비스 작성자는 복구하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-170">The service author needs to perform the following to recover:</span></span>

  - <span data-ttu-id="69c98-171">`OnDataLossAsync` 가상 기본 클래스 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-171">Override the virtual base class method `OnDataLossAsync`.</span></span>
  - <span data-ttu-id="69c98-172">서비스의 백업을 포함하는 외부 위치에서 최신 백업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-172">Find the latest backup in the external location that contains the service's backups.</span></span>
  - <span data-ttu-id="69c98-173">최신 백업을 다운로드(및 압축된 경우 백업에서 백업 폴더에 압축 해제)합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-173">Download the latest backup (and uncompress the backup into the backup folder if it was compressed).</span></span>
  - <span data-ttu-id="69c98-174">`OnDataLossAsync` 메서드에서 `RestoreContext`를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-174">The `OnDataLossAsync` method provides a `RestoreContext`.</span></span> <span data-ttu-id="69c98-175">제공된 `RestoreContext`에서 `RestoreAsync` API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-175">Call the `RestoreAsync` API on the provided `RestoreContext`.</span></span>
  - <span data-ttu-id="69c98-176">복원이 성공하면 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-176">Return true if the restoration was a success.</span></span>

<span data-ttu-id="69c98-177">다음은 `OnDataLossAsync` 메서드의 구현 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-177">Following is an example implementation of the `OnDataLossAsync` method:</span></span>

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

<span data-ttu-id="69c98-178">`RestoreContext.RestoreAsync` 호출에 전달된 `RestoreDescription`에는 `BackupFolderPath`라고 하는 멤버가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-178">`RestoreDescription` passed in to the `RestoreContext.RestoreAsync` call contains a member called `BackupFolderPath`.</span></span>
<span data-ttu-id="69c98-179">단일 전체 백업을 복원하는 경우 이 `BackupFolderPath`는 전체 백업이 포함되어 있는 폴더의 로컬 경로로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-179">When restoring a single full backup, this `BackupFolderPath` should be set to the local path of the folder that contains your full backup.</span></span>
<span data-ttu-id="69c98-180">전체 백업과 여러 개의 증분 백업을 복원하는 경우 `BackupFolderPath`는 전체 백업뿐만 아니라 모든 증분 백업도 포함되어 있는 폴더의 로컬 경로로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-180">When restoring a full backup and a number of incremental backups, `BackupFolderPath` should be set to the local path of the folder that not only contains the full backup, but also all the incremental backups.</span></span>
<span data-ttu-id="69c98-181">제공된 `BackupFolderPath`에 전체 백업이 포함되지 않은 경우 `RestoreAsync` 호출에서 `FabricMissingFullBackupException`이 발생(throw)될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-181">`RestoreAsync` call can throw `FabricMissingFullBackupException` if the `BackupFolderPath` provided does not contain a full backup.</span></span>
<span data-ttu-id="69c98-182">`BackupFolderPath`에서 증분 백업 체인이 끊겨 있으면 `ArgumentException`이 발생(throw)될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-182">It can also throw `ArgumentException` if `BackupFolderPath` has a broken chain of incremental backups.</span></span>
<span data-ttu-id="69c98-183">예를 들어, 전체 백업을 포함하는 경우 두 번째 증분 백업을 제외하고, 첫 번째 증분과 세 번째 증분 백업을 포함하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-183">For example, if it contains the full backup, the first incremental and the third incremental backup but no the second incremental backup.</span></span>

> [!NOTE]
> <span data-ttu-id="69c98-184">RestorePolicy는 기본적으로 Safe로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-184">The RestorePolicy is set to Safe by default.</span></span>  <span data-ttu-id="69c98-185">즉, 백업 폴더에 이 복제본에 포함된 상태와 같거나 그 이전의 상태가 포함되어 있음을 검색한 경우 `RestoreAsync` API가 ArgumentException으로 인해 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-185">This means that the `RestoreAsync` API will fail with ArgumentException if it detects that the backup folder contains a state that is older than or equal to the state contained in this replica.</span></span>  <span data-ttu-id="69c98-186">`RestorePolicy.Force`를 사용하여 이 안전 검사를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-186">`RestorePolicy.Force` can be used to skip this safety check.</span></span> <span data-ttu-id="69c98-187">이는 `RestoreDescription`의 일부로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-187">This is specified as part of `RestoreDescription`.</span></span>
> 

## <a name="deleted-or-lost-service"></a><span data-ttu-id="69c98-188">서비스 삭제 또는 손상</span><span class="sxs-lookup"><span data-stu-id="69c98-188">Deleted or lost service</span></span>
<span data-ttu-id="69c98-189">서비스가 제거된 경우 데이터 복원에 앞서 서비스를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-189">If a service is removed, you must first re-create the service before the data can be restored.</span></span>  <span data-ttu-id="69c98-190">데이터의 원할한 복원을 위해 파티션 구성표 등과 같은 동일한 구성의 서비스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-190">It is important to create the service with the same configuration, e.g., partitioning scheme, so that the data can be restored seamlessly.</span></span>  <span data-ttu-id="69c98-191">서비스가 작동되면 이 서비스의 모든 파티션에서 데이터를 복원하는 API(위의`OnDataLossAsync`)를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-191">Once the service is up, the API to restore data (`OnDataLossAsync` above) has to be invoked on every partition of this service.</span></span> <span data-ttu-id="69c98-192">이를 달성하는 한 가지 방법은 모든 파티션에서 `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-192">One way of achieving this is by using `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` on every partition.</span></span>  

<span data-ttu-id="69c98-193">이 시점부터는 앞의 시나리오와 같은 방식으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-193">From this point, implementation is the same as the above scenario.</span></span> <span data-ttu-id="69c98-194">각 파티션이 외부 저장소로부터 최신 관련 백업을 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-194">Each partition needs to restore the latest relevant backup from the external store.</span></span> <span data-ttu-id="69c98-195">한 가지 주의할 점은 런타임이 동적으로 파티션 ID를 생성하기 대문에 파티션 ID가 변경될 수 있다는 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-195">One caveat is that the partition ID may have now changed, since the runtime creates partition IDs dynamically.</span></span> <span data-ttu-id="69c98-196">따라서 서비스가 각 파티션에서 복원할 정확한 최신 백업을 식별할 수 있게 적합한 파티션 정보 및 서비스 이름을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-196">Thus, the service needs to store the appropriate partition information and service name to identify the correct latest backup to restore from for each partition.</span></span>

> [!NOTE]
> <span data-ttu-id="69c98-197">전체 서비스를 복원하기 위해 각 파티션에서 `FabricClient.ServiceManager.InvokeDataLossAsync`를 사용하는 것은 클러스터 상태를 손상시킬 수 있으므로 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-197">It is not recommended to use `FabricClient.ServiceManager.InvokeDataLossAsync` on each partition to restore the entire service, since that may corrupt your cluster state.</span></span>
> 

## <a name="replication-of-corrupt-application-data"></a><span data-ttu-id="69c98-198">손상된 응용 프로그램 데이터의 복제</span><span class="sxs-lookup"><span data-stu-id="69c98-198">Replication of corrupt application data</span></span>
<span data-ttu-id="69c98-199">새로 배포된 응용 프로그램 업그레이드에 버그가 있는 경우 데이터 손상을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-199">If the newly deployed application upgrade has a bug, that may cause corruption of data.</span></span> <span data-ttu-id="69c98-200">응용 프로그램 업그레이드를 시작하여 잘못된 지역 번호로 신뢰할 수 있는 사전의 모든 전화번호 레코드를 업데이트하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-200">For example, an application upgrade may start to update every phone number record in a Reliable Dictionary with an invalid area code.</span></span>  <span data-ttu-id="69c98-201">이 경우 서비스 패브릭이 저장하는 데이터의 본질을 인지하지 못하므로 잘못된 전화 번호가 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-201">In this case, the invalid phone numbers will be replicated since Service Fabric is not aware of the nature of the data that is being stored.</span></span>

<span data-ttu-id="69c98-202">이렇게 데이터 손상을 초래할 수 있는 황당한 버그를 탐지한 후 가장 먼저 할 일은 응용 프로그램 수준에서 서비스를 고정하고, 가능하다면 버그가 없는 응용 프로그램 코드의 버전으로 업그레이드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-202">The first thing to do after you detect such an egregious bug that causes data corruption is to freeze the service at the application level and, if possible, upgrade to the version of the application code that does not have the bug.</span></span>  <span data-ttu-id="69c98-203">그러나 서비스 코드가 고정된 후에도 데이터 손상이 지속되어 데이터 복원이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-203">However, even after the service code is fixed, the data may still be corrupt and thus data may need to be restored.</span></span>  <span data-ttu-id="69c98-204">이 경우에는 최신 백업도 손상되었을 수 있기 때문에 최신 백업을 복원하는 것으로는 부족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-204">In such cases, it may not be sufficient to restore the latest backup, since the latest backups may also be corrupt.</span></span>  <span data-ttu-id="69c98-205">따라서 데이터 손상 이전에 만든 최신 백업을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-205">Thus, you have to find the last backup that was made before the data got corrupted.</span></span>

<span data-ttu-id="69c98-206">백업이 손상되었는지 확실하지 않은 경우 새 서비스 패브릭 클러스터를 배포하고 위의 "삭제되거나 손상된 서비스" 시나리오와 마찬가지로 영향을 받는 파티션의 백업을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-206">If you are not sure which backups are corrupt, you could deploy a new Service Fabric cluster and restore the backups of affected partitions just like the above "Deleted or lost service" scenario.</span></span>  <span data-ttu-id="69c98-207">각 파티션에 대해 가장 최근부터 가장 오래된 순으로 백업을 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-207">For each partition, start restoring the backups from the most recent to the least.</span></span> <span data-ttu-id="69c98-208">손상되지 않은 백업을 찾은 후 이 파티션에 있는 모든 백업(해당 백업보다 최신 버전)을 이동/삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-208">Once you find a backup that does not have the corruption, move/delete all backups of this partition that were more recent (than that backup).</span></span> <span data-ttu-id="69c98-209">각 파티션에 대해 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-209">Repeat this process for each partition.</span></span> <span data-ttu-id="69c98-210">이제 프로덕션 클러스터의 파티션에서 `OnDataLossAsync`가 호출되면 외부 저장소에 있는 마지막 백업이 위의 프로세스로 선택된 백업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-210">Now, when `OnDataLossAsync` is called on the partition in the production cluster, the last backup found in the external store will be the one picked by the above process.</span></span>

<span data-ttu-id="69c98-211">이제 "삭제되거나 손실된 서비스" 섹션의 단계를 사용하여 버그가 있는 코드로 손상되기 이전의 상태로 서비스 상태를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-211">Now, the steps in the "Deleted or lost service" section can be used to restore the state of the service to the state before the buggy code corrupted the state.</span></span>

<span data-ttu-id="69c98-212">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="69c98-212">Note that:</span></span>

  - <span data-ttu-id="69c98-213">복원할 때 복원 중인 백업이 데이터 손실 이전의 파티션 상태보다 오래된 것일 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-213">When you restore, there is a chance that the backup being restored is older than the state of the partition before the data was lost.</span></span> <span data-ttu-id="69c98-214">이 때문에 가능한 많은 데이터를 복구하기 위한 마지막 수단으로만 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-214">Because of this, you should restore only as a last resort to recover as much data as possible.</span></span>
  - <span data-ttu-id="69c98-215">백업 폴더 경로와 백업 폴더 내 파일 경로를 나타내는 문자열은 FabricDataRoot 경로 및 응용 프로그램 형식 이름의 길이에 따라 255자보다 길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-215">The string that represents the backup folder path and the paths of files inside the backup folder can be greater than 255 characters, depending on the FabricDataRoot path and Application Type name's length.</span></span> <span data-ttu-id="69c98-216">이로 인해 `Directory.Move`와 같은 일부 .NET 메서드에서 `PathTooLongException` 예외가 발생(throw)될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-216">This can cause some .NET methods, like `Directory.Move`, to throw the `PathTooLongException` exception.</span></span> <span data-ttu-id="69c98-217">한 가지 해결 방법은 `CopyFile`과 같은 kernel32 API를 직접 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-217">One workaround is to directly call kernel32 APIs, like `CopyFile`.</span></span>

## <a name="backup-and-restore-reliable-actors"></a><span data-ttu-id="69c98-218">Reliable Actors 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="69c98-218">Backup and restore Reliable Actors</span></span>


<span data-ttu-id="69c98-219">Reliable Actors 프레임워크는 Reliable Services를 기반으로 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-219">Reliable Actors Framework is built on top of Reliable Services.</span></span> <span data-ttu-id="69c98-220">행위자를 호스팅하는 ActorService는 상태 저장 신뢰할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-220">The ActorService which hosts the actor(s) is a stateful reliable service.</span></span> <span data-ttu-id="69c98-221">따라서 Reliable Services에서 사용 가능한 모든 백업 및 복원 기능이 Reliable Actors에도 제공됩니다(상태 제공자와 관련된 동작은 제외).</span><span class="sxs-lookup"><span data-stu-id="69c98-221">Hence, all the backup and restore functionality available in Reliable Services is also available to Reliable Actors (except behaviors that are state provider specific).</span></span> <span data-ttu-id="69c98-222">백업이 파티션 단위로 수행되기 때문에 파티션에서 모든 행위자에 대한 상태는 백업됩니다(또한 복원은 비슷하고 파티션 기준으로 발생함).</span><span class="sxs-lookup"><span data-stu-id="69c98-222">Since backups will be taken on a per-partition basis, states for all actors in that partition will be backed up (and restoration is similar and will happen on a per-partition basis).</span></span> <span data-ttu-id="69c98-223">백업/복원을 수행하려면 서비스 소유자는 ActorService에서 파생되는 사용자 지정 행위자 서비스 클래스를 만든 다음 이전 섹션에서 설명한 것과 같이 Reliable Services와 유사한 백업/복원을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-223">To perform backup/restore, the service owner should create a custom actor service class that derives from ActorService class and then do backup/restore similar to Reliable Services as described above in previous sections.</span></span>

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

<span data-ttu-id="69c98-224">사용자 지정 행위자 서비스 클래스를 만들 경우 행위자를 등록할 때 사용자 지정 행위자 서비스도 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-224">When you create a custom actor service class, you need to register that as well when registering the actor.</span></span>

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

<span data-ttu-id="69c98-225">Reliable Actors에 대한 기본 상태 제공자는 `KvsActorStateProvider`입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-225">The default state provider for Reliable Actors is `KvsActorStateProvider`.</span></span> <span data-ttu-id="69c98-226">`KvsActorStateProvider`에 대한 증분 백업은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-226">Incremental backup is not enabled by default for `KvsActorStateProvider`.</span></span> <span data-ttu-id="69c98-227">다음 코드 조각과 같이 생성자에서 적절한 설정을 사용하여 `KvsActorStateProvider`를 만든 다음 ActorService 생성자에 전달하여 증분 백업을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-227">You can enable incremental backup by creating `KvsActorStateProvider` with the appropriate setting in its constructor and then passing it to ActorService constructor as shown in following code snippet:</span></span>

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

<span data-ttu-id="69c98-228">증분 백업을 사용하도록 설정한 후 다음 이유 중 하나로 인한 FabricMissingFullBackupException 때문에 증분 백업이 실패할 수 있으며, 증분 백업을 수행하기 전에 전체 백업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-228">After incremental backup has been enabled, taking an incremental backup can fail with FabricMissingFullBackupException for one of following reasons and you will need to take a full backup before taking incremental backup(s):</span></span>

  - <span data-ttu-id="69c98-229">복제본이 주가 된 이후로 전체 백업을 수행한 적이 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-229">The replica has never taken a full backup since it became primary.</span></span>
  - <span data-ttu-id="69c98-230">마지막 백업이 수행된 이후로 로그 레코드의 일부가 잘렸습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-230">Some of the log records were truncated since last backup was taken.</span></span>

<span data-ttu-id="69c98-231">증분 백업을 사용하도록 설정하면 `KvsActorStateProvider`에서 순환 버퍼를 사용하여 해당 로그 레코드를 관리하지 않으며 정기적으로 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-231">When incremental backup is enabled, `KvsActorStateProvider` does not use circular buffer to manage its log records and periodically truncates it.</span></span> <span data-ttu-id="69c98-232">사용자가 45분 동안 백업을 수행하지 않을 경우 시스템이 로그 레코드를 자동으로 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-232">If no backup is taken by user for a period of 45 minutes, the system automatically truncates the log records.</span></span> <span data-ttu-id="69c98-233">이 간격은 `KvsActorStateProvider` 생성자에서 `logTrunctationIntervalInMinutes`를 지정하여 구성할 수 있습니다(증분 백업을 사용하도록 설정하는 경우와 비슷함).</span><span class="sxs-lookup"><span data-stu-id="69c98-233">This interval can be configured by specifying `logTrunctationIntervalInMinutes` in `KvsActorStateProvider` constructor (similar to when enabling incremental backup).</span></span> <span data-ttu-id="69c98-234">주 복제본이 모든 데이터를 전송하여 다른 복제본을 구축해야 하는 경우 로그 레코드가 잘릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-234">The log records may also get truncated if primary replica need to build another replica by sending all its data.</span></span>

<span data-ttu-id="69c98-235">백업 체인에서 복원 작업을 수행할 때는 Reliable Services와 마찬가지로 BackupFolderPath에 전체 백업이 포함된 하위 디렉터리 하나와 증분 백업이 포함된 다른 하위 디렉터리가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-235">When doing restore from a backup chain, similar to Reliable Services, the BackupFolderPath should contain subdirectories with one subdirectory containing full backup and others subdirectories containing incremental backup(s).</span></span> <span data-ttu-id="69c98-236">백업 체인 유효성 검사에 실패할 경우 복원 API에서 적절한 오류 메시지와 함께 FabricException을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-236">The restore API will throw FabricException with appropriate error message if the backup chain validation fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="69c98-237">`KvsActorStateProvider`는 현재 RestorePolicy.Safe 옵션을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-237">`KvsActorStateProvider` currently ignores the option RestorePolicy.Safe.</span></span> <span data-ttu-id="69c98-238">이 기능은 이후 릴리스에서 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-238">Support for this feature is planned in an upcoming release.</span></span>
> 

## <a name="testing-backup-and-restore"></a><span data-ttu-id="69c98-239">테스트 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="69c98-239">Testing Backup and Restore</span></span>
<span data-ttu-id="69c98-240">데이터가 백업되고 복원될 수 있도록 하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-240">It is important to ensure that critical data is being backed up, and can be restored from.</span></span> <span data-ttu-id="69c98-241">이 작업은 특정 파티션에서 데이터 손실을 유도할 수 있는 PowerShell의 `Start-ServiceFabricPartitionDataLoss` cmdlet을 호출하여 서비스에 대한 데이터 백업 및 복원 기능이 예상대로 작동하는지 테스트함으로써 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-241">This can be done by invoking the `Start-ServiceFabricPartitionDataLoss` cmdlet in PowerShell that can induce data loss in a particular partition to test whether the data backup and restore functionality for your service is working as expected.</span></span>  <span data-ttu-id="69c98-242">프로그래밍 방식으로 데이터 손실을 호출하고 해당 이벤트에서 복원하는 것도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-242">It is also possible to programmatically invoke data loss and restore from that event as well.</span></span>

> [!NOTE]
> <span data-ttu-id="69c98-243">백업의 샘플 구현을 찾고 GitHub의 웹 참조 앱에서 기능을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-243">You can find a sample implementation of backup and restore functionality in the Web Reference App on GitHub.</span></span> <span data-ttu-id="69c98-244">자세한 내용은 `Inventory.Service` 서비스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c98-244">Please look at the `Inventory.Service` service for more details.</span></span>
> 
> 

## <a name="under-the-hood-more-details-on-backup-and-restore"></a><span data-ttu-id="69c98-245">내부 살펴보기: 백업 및 복원에 대한 자세한 내용 </span><span class="sxs-lookup"><span data-stu-id="69c98-245">Under the hood: more details on backup and restore</span></span>
<span data-ttu-id="69c98-246">다음은 백업 및 복원에 대한 자세한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-246">Here's some more details on backup and restore.</span></span>

### <a name="backup"></a><span data-ttu-id="69c98-247">백업</span><span class="sxs-lookup"><span data-stu-id="69c98-247">Backup</span></span>
<span data-ttu-id="69c98-248">Reliable State Manager는 읽기 및 쓰기 작업을 차단하지 않고 일관된 백업을 만드는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-248">The Reliable State Manager provides the ability to create consistent backups without blocking any read or write operations.</span></span> <span data-ttu-id="69c98-249">이를 위해 검사점 및 로그 지속성 메커니즘을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-249">To do so, it utilizes a checkpoint and log persistence mechanism.</span></span>  <span data-ttu-id="69c98-250">Reliable State Manager는 트랜잭션 로그로부터의 부담을 줄이고 복구 시간을 단축하기 위해 특정 지점에서 유사 항목(경량) 검사점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-250">The Reliable State Manager takes fuzzy (lightweight) checkpoints at certain points to relieve pressure from the transactional log and improve recovery times.</span></span>  <span data-ttu-id="69c98-251">`BackupAsync`가 호출되면 신뢰할 수 있는 상태 관리자에서 모든 신뢰할 수 있는 개체에 최신 검사점 파일을 로컬 백업 폴더에 복사하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-251">When `BackupAsync` is called, the Reliable State Manager instructs all Reliable objects to copy their latest checkpoint files to a local backup folder.</span></span>  <span data-ttu-id="69c98-252">그런 다음 Reliable State Manager가 "시작  포인터"에서부터 마지막 로그 레코드까지의 모든 로그 레코드를 백업 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-252">Then, the Reliable State Manager copies all log records, starting from the "start pointer" to the latest log record into the backup folder.</span></span>  <span data-ttu-id="69c98-253">최신 로그 레코드까지의 모든 로그 레코드가 백업에 포함되고 신뢰할 수 있는 상태 관리자에서 미리 쓰기 로깅을 유지하므로 신뢰할 수 있는 상태 관리자는 커밋된 모든 트랜잭션(`CommitAsync`가 성공적으로 반환됨)이 백업에 포함되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-253">Since all the log records up to the latest log record are included in the backup and the Reliable State Manager preserves write-ahead logging, the Reliable State Manager guarantees that all transactions that are committed (`CommitAsync` has returned successfully) are included in the backup.</span></span>

<span data-ttu-id="69c98-254">`BackupAsync`가 호출된 후에 커밋되는 모든 트랜잭션은 백업에 포함되거나 포함되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-254">Any transaction that commits after `BackupAsync` has been called may or may not be in the backup.</span></span>  <span data-ttu-id="69c98-255">로컬 백업 폴더를 플랫폼에서 입력합 후에는(즉, 런타임에서 로컬 백업 완료됨) 서비스의 백업 콜백이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-255">Once the local backup folder has been populated by the platform (i.e., local backup is completed by the runtime), the service's backup callback is invoked.</span></span>  <span data-ttu-id="69c98-256">이 콜백은 백업 폴더를 Azure 저장소 등의 외부 위치로 이동하는 것을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-256">This callback is responsible for moving the backup folder to an external location such as Azure Storage.</span></span>

### <a name="restore"></a><span data-ttu-id="69c98-257">복원</span><span class="sxs-lookup"><span data-stu-id="69c98-257">Restore</span></span>
<span data-ttu-id="69c98-258">신뢰할 수 있는 상태 관리자에서는 `RestoreAsync` API를 사용하여 백업에서 복원하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-258">The Reliable State Manager provides the ability to restore from a backup by using the `RestoreAsync` API.</span></span>  
<span data-ttu-id="69c98-259">`RestoreContext`의 `RestoreAsync` 메서드는 `OnDataLossAsync` 메서드 내에서만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-259">The `RestoreAsync` method on `RestoreContext` can be called only inside the `OnDataLossAsync` method.</span></span>
<span data-ttu-id="69c98-260">`OnDataLossAsync`에서 반환한 부울 값은 서비스에서 외부 원본으로부터 상태를 복원했는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-260">The bool returned by `OnDataLossAsync` indicates whether the service restored its state from an external source.</span></span>
<span data-ttu-id="69c98-261">`OnDataLossAsync`에서 true를 반환하면 Service Fabric에서 이 주 복제본의 다른 모든 복제본을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-261">If the `OnDataLossAsync` returns true, Service Fabric will rebuild all other replicas from this primary.</span></span> <span data-ttu-id="69c98-262">Service Fabric은 `OnDataLossAsync` 호출을 받는 복제본이 먼저 주 역할로 전환되지만 읽기 상태 또는 쓰기 상태가 부여되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-262">Service Fabric ensures that replicas that will receive `OnDataLossAsync` call first transition to the primary role but are not granted read status or write status.</span></span>
<span data-ttu-id="69c98-263">즉 `OnDataLossAsync`가 성공적으로 완료될 때까지 StatefulService 구현자에 대해 `RunAsync`가 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-263">This implies that for StatefulService implementers, `RunAsync` will not be called until `OnDataLossAsync` finishes successfully.</span></span>
<span data-ttu-id="69c98-264">그런 다음 `OnDataLossAsync`가 새 주 복제본에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-264">Then, `OnDataLossAsync` will be invoked on the new primary.</span></span>
<span data-ttu-id="69c98-265">서비스가 이 API를 성공적으로 완료하고(True 또는 False 반환) 관련 재구성을 마치면 한 번에 하나씩 API가 계속 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-265">Until a service completes this API successfully (by returning true or false) and finishes the relevant reconfiguration, the API will keep being called one at a time.</span></span>

<span data-ttu-id="69c98-266">`RestoreAsync`는 먼저 호출된 주 복제본의 모든 기존 상태를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-266">`RestoreAsync` first drops all existing state in the primary replica that it was called on.</span></span>  
<span data-ttu-id="69c98-267">그런 다음 신뢰할 수 있는 상태 관리자가 백업 폴더에 존재하는 모든 신뢰 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-267">Then the Reliable State Manager creates all the Reliable objects that exist in the backup folder.</span></span>  
<span data-ttu-id="69c98-268">다음으로 백업 폴더의 검사점으로부터 백업하도록 신뢰 개체에게 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-268">Next, the Reliable objects are instructed to restore from their checkpoints in the backup folder.</span></span>  
<span data-ttu-id="69c98-269">마지막으로 Reliable State Manager가 백업 폴더의 로그 레코드에서 자체 상태를 복구하고 복구를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-269">Finally, the Reliable State Manager recovers its own state from the log records in the backup folder and performs recovery.</span></span>  
<span data-ttu-id="69c98-270">복구 프로세스의 일환으로 백업 폴더에서 로그 레코드를 커밋한 "시작점"에서 시작하는 작업이 신뢰 개체에 재현됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-270">As part of the recovery process, operations starting from the "starting point" that have commit log records in the backup folder are replayed to the Reliable objects.</span></span>  
<span data-ttu-id="69c98-271">이 단계를 통해 일관된 복구 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="69c98-271">This step ensures that the recovered state is consistent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69c98-272">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69c98-272">Next steps</span></span>
  - [<span data-ttu-id="69c98-273">신뢰할 수 있는 컬렉션</span><span class="sxs-lookup"><span data-stu-id="69c98-273">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
  - [<span data-ttu-id="69c98-274">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="69c98-274">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  - [<span data-ttu-id="69c98-275">Reliable Services 알림</span><span class="sxs-lookup"><span data-stu-id="69c98-275">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
  - [<span data-ttu-id="69c98-276">Reliable Services 구성</span><span class="sxs-lookup"><span data-stu-id="69c98-276">Reliable Services configuration</span></span>](service-fabric-reliable-services-configuration.md)
  - [<span data-ttu-id="69c98-277">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="69c98-277">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

