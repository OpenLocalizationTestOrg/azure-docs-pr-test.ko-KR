---
title: "백업에서 StorSimple 볼륨 복원 | Microsoft Docs"
description: "StorSimple 관리자 서비스 백업 카탈로그 페이지를 사용하여 백업 세트에서 StorSimple 볼륨을 복원하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="0a32e-103">백업 세트에서 StorSimple 볼륨 복원</span><span class="sxs-lookup"><span data-stu-id="0a32e-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="0a32e-104">개요</span><span class="sxs-lookup"><span data-stu-id="0a32e-104">Overview</span></span>
<span data-ttu-id="0a32e-105">**백업 카탈로그** 페이지는 수동 또는 자동화된 백업을 수행할 때 생성되는 모든 백업 세트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="0a32e-106">이 페이지를 사용하여 백업 정책 또는 볼륨에 대한 모든 백업을 나열하거나, 백업을 선택 또는 삭제하거나 백업을 사용하여 볼륨을 복원 또는 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![백업 카탈로그 페이지](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="0a32e-108">이 자습서에서는 **백업 카탈로그** 페이지를 사용하여 백업 세트에서 장치의 볼륨을 복원하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="0a32e-109">백업 카탈로그를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="0a32e-109">How to use the backup catalog</span></span>
<span data-ttu-id="0a32e-110">**백업 카탈로그** 페이지는 백업 세트 선택 범위를 좁히는 데 도움이 되는 쿼리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="0a32e-111">다음 매개 변수를 기반으로 검색되는 백업 세트를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="0a32e-112">**장치** – 백업 세트를 만든 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="0a32e-113">**백업 정책** 또는 **볼륨** – 백업 정책 또는 이 백업 세트와 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="0a32e-114">**시작** 및 **종료** – 백업 세트를 만든 날짜 및 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="0a32e-115">그런 다음 필터링된 백업 세트는 다음 특성을 기반으로 표로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="0a32e-116">**이름** – 백업 정책 또는 이 백업 세트와 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="0a32e-117">**크기** – 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="0a32e-118">**만든 날짜** – 백업이 만들어진 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="0a32e-119">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="0a32e-120">로컬 스냅숏은 장치에 로컬로 저장된 모든 볼륨 데이터의 백업인 반면 클라우드 스냅숏은 클라우드에 상주하는 볼륨 데이터의 백업을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="0a32e-121">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="0a32e-122">**시작 기준** – 일정에 따라 자동으로 또는 사용자가 수동으로 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="0a32e-123">(백업을 예약하기 위해 백업 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="0a32e-124">또는, **백업 수행** 옵션을 사용하여 대화형 백업을 수행할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="0a32e-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="0a32e-125">백업에서 StorSimple 볼륨을 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="0a32e-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="0a32e-126">**백업 카탈로그** 페이지를 사용하여 특정 백업에서 StorSimple 볼륨을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="0a32e-127">백업에서 복원되면 백업에서 기존 볼륨을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="0a32e-128">백업이 수행된 후 작성된 모든 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="0a32e-129">볼륨의 복원을 시작하기 전에 해당 볼륨이 오프라인 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="0a32e-130">먼저 호스트에서도 볼륨을 오프라인으로 전환한 다음 장치를 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="0a32e-131">[볼륨을 오프라인으로 전환](storsimple-manage-volumes.md#take-a-volume-offline)단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="0a32e-132">다음 단계를 수행하여 백업 세트에서 볼륨을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="0a32e-133">백업 세트에서 복원하려면</span><span class="sxs-lookup"><span data-stu-id="0a32e-133">To restore from a backup set</span></span>
1. <span data-ttu-id="0a32e-134">StorSimple 관리자 서비스 페이지에서 **백업 카탈로그** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![백업 카탈로그](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="0a32e-136">백업 세트를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="0a32e-137">해당 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="0a32e-138">드롭다운 목록에서 선택하려는 백업에 대 한 볼륨 또는 백업 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="0a32e-139">시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-139">Specify the time range.</span></span>
   4. <span data-ttu-id="0a32e-140">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="0a32e-140">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="0a32e-142">을 클릭하여 이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-142">to execute this query.</span></span>
      
      <span data-ttu-id="0a32e-143">선택한 볼륨와 연결된 백업을 또는 백업 정책이 백업 세트의 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="0a32e-144">백업 세트를 확장하여 연결된 볼륨을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="0a32e-145">이 볼륨은 복원하려면 호스트와 장치에서 오프라인 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="0a32e-146">[볼륨을 오프라인으로 전환](storsimple-manage-volumes.md#take-a-volume-offline)단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0a32e-147">해당 볼륨을 오프 라인으로 전환하기 전에, 먼저 호스트에서 해당 볼륨을 오프라인으로 전환했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="0a32e-148">호스트에서 볼륨을 오프라인으로 전환하지 않은 경우 잠재적으로 데이터가 손상될 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="0a32e-149">백업 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-149">Select a backup set.</span></span> <span data-ttu-id="0a32e-150">페이지의 맨 아래에서 **복원** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="0a32e-151">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-151">You will be prompted for confirmation.</span></span> 
   
    ![확인 페이지](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="0a32e-153">복원 정보를 검토하고 확인 아이콘 ![확인 아이콘](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png)단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="0a32e-154">그러면 **작업** 페이지에 액세스하여 볼 수 있는 복원 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="0a32e-155">복원이 완료되면 볼륨의 내용을 백업의 볼륨으로 바뀌는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="0a32e-156">![동영상 사용 가능](./media/storsimple-restore-from-backup-set/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="0a32e-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="0a32e-157">StorSimple에서 복제 및 복원 기능을 사용하여 삭제된 파일을 복구하는 방법을 보여 주는 동영상을 시청하려면 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="0a32e-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a32e-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a32e-158">Next steps</span></span>
* <span data-ttu-id="0a32e-159">[StorSimple 볼륨을 관리](storsimple-manage-volumes.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="0a32e-160">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a32e-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

