---
title: "백업에서 StorSimple 볼륨 aaaRestore | Microsoft Docs"
description: "어떻게 toouse hello StorSimple 관리자 서비스 백업 카탈로그 페이지 toorestore 백업 세트에서 StorSimple 볼륨에 설명 합니다."
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
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="5399c-103">백업 세트에서 StorSimple 볼륨 복원</span><span class="sxs-lookup"><span data-stu-id="5399c-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="5399c-104">개요</span><span class="sxs-lookup"><span data-stu-id="5399c-104">Overview</span></span>
<span data-ttu-id="5399c-105">hello **백업 카탈로그** 페이지 수동 또는 자동 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="5399c-106">이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![백업 카탈로그 페이지](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="5399c-108">이 자습서에 설명 어떻게 toouse hello **백업 카탈로그** 페이지 toorestore 백업 세트에서 장치에 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="5399c-109">어떻게 toouse hello 백업 카탈로그</span><span class="sxs-lookup"><span data-stu-id="5399c-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="5399c-110">hello **백업 카탈로그** 페이지에서는 백업 세트 선택 toonarrow는 데 도움이 되는 쿼리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="5399c-111">Hello 백업 세트를 검색 하는 hello 매개 변수 뒤에 따라 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="5399c-112">**장치** – hello 장치는 hello에 백업 세트 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="5399c-113">**백업 정책** 또는 **볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="5399c-114">**** 및 **를** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="5399c-115">hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:</span><span class="sxs-lookup"><span data-stu-id="5399c-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="5399c-116">**이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="5399c-117">**크기** – hello hello 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="5399c-118">**만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="5399c-119">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="5399c-120">로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="5399c-121">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="5399c-122">**에 의해 시작** – hello 백업을 tooa 일정에 따라 자동으로 시작 될 수 있습니다 또는 사용자가 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="5399c-123">(백업 정책 tooschedule 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="5399c-124">Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 대화형 백업.)</span><span class="sxs-lookup"><span data-stu-id="5399c-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="5399c-125">어떻게 toorestore 백업에서 StorSimple 볼륨</span><span class="sxs-lookup"><span data-stu-id="5399c-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="5399c-126">Hello를 사용할 수 있습니다 **백업 카탈로그** toorestore 특정 백업에서 StorSimple 볼륨 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="5399c-127">백업에서 복원 hello hello 백업에서 기존 볼륨이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="5399c-128">Hello 백업을 수행한 후에 기록 된 모든 데이터의 손실을 hello 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="5399c-129">볼륨에서 복원을 시작 하기 전에 hello 볼륨이 오프 라인 상태 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="5399c-130">다음 장치를 hello 쿼리하고 먼저 tootake hello 볼륨을 오프 hello 호스트에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="5399c-131">Hello 단계에 따라 [볼륨을 오프 라인](storsimple-manage-volumes.md#take-a-volume-offline)합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="5399c-132">Hello 단계 toorestore 볼륨 백업 세트에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="5399c-133">백업 세트에서 toorestore</span><span class="sxs-lookup"><span data-stu-id="5399c-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="5399c-134">Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![백업 카탈로그](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="5399c-136">백업 세트를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="5399c-137">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="5399c-138">Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="5399c-139">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="5399c-140">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-140">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="5399c-142">tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="5399c-143">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="5399c-144">Hello 백업 세트 tooview hello 연결 된 볼륨을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="5399c-145">이러한 볼륨을 복구 하기 전에 hello 호스트와 장치에서 오프 라인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="5399c-146">Hello 단계에 따라 [볼륨을 오프 라인](storsimple-manage-volumes.md#take-a-volume-offline)합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5399c-147">수행 하 여 hello 호스트의 hello 볼륨을 오프 라인으로 먼저 hello 장치에서 hello 볼륨을 오프 라인으로 수행 하기 전에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="5399c-148">Hello 호스트에서 오프 라인으로 hello 볼륨을 사용 하지 않는 경우 toodata 손상이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="5399c-149">백업 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-149">Select a backup set.</span></span> <span data-ttu-id="5399c-150">클릭 **복원** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="5399c-151">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-151">You will be prompted for confirmation.</span></span> 
   
    ![확인 페이지](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="5399c-153">Hello 복원 정보를 검토 hello 확인 아이콘을 클릭 하 여 ![확인 아이콘](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="5399c-154">Hello에 액세스 하 여 볼 수 있는 복원 작업 시작 **작업** 페이지.</span><span class="sxs-lookup"><span data-stu-id="5399c-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="5399c-155">Hello 복원이 완료 되 면 사용자 볼륨의 hello 내용을 hello 백업에서 볼륨으로 바뀌는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="5399c-156">![동영상 사용 가능](./media/storsimple-restore-from-backup-set/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="5399c-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="5399c-157">toowatch hello 복제를 사용 하 여 StorSimple 삭제 toorecover 파일의 기능을 복원 하는 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5399c-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5399c-158">Next steps</span></span>
* <span data-ttu-id="5399c-159">너무 방법에 대해 알아봅니다[관리 StorSimple 볼륨](storsimple-manage-volumes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="5399c-160">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5399c-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

