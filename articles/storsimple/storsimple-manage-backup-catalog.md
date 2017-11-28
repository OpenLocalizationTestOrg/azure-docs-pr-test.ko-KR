---
title: "aaaManage StorSimple 백업 카탈로그 | Microsoft Docs"
description: "Toouse hello StorSimple Manager 서비스 백업 카탈로그 페이지 toolist를 선택 하 고 볼륨에 대 한 백업 세트를 삭제 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="93c8d-103">사용 하 여 hello StorSimple 관리자 서비스 toomanage 백업 카탈로그</span><span class="sxs-lookup"><span data-stu-id="93c8d-103">Use hello StorSimple Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="93c8d-104">개요</span><span class="sxs-lookup"><span data-stu-id="93c8d-104">Overview</span></span>
<span data-ttu-id="93c8d-105">StorSimple Manager 서비스 hello **백업 카탈로그** 페이지 수동 또는 예약 된 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="93c8d-106">이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="93c8d-107">이 자습서에서는 방법 toolist, select 및 삭제 하 여 백업 세트를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="93c8d-108">toolearn 어떻게 toorestore 백업에서 장치 이동 너무[장치 백업 세트에서 복원](storsimple-restore-from-backup-set.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="93c8d-109">볼륨을 tooclone 너무 이동 toolearn[StorSimple 볼륨을 복제](storsimple-clone-volume.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![백업 카탈로그](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="93c8d-111">hello **백업 카탈로그** 페이지 쿼리 toonarrow 백업 세트 선택 항목을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-111">hello **Backup Catalog** page provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="93c8d-112">Hello 매개 변수 뒤에 따라 검색 되는 hello 백업 세트를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="93c8d-113">**장치** – hello 장치는 hello에 백업 세트 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="93c8d-114">**백업 정책 또는 볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-114">**Backup Policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="93c8d-115">**From 및 To** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="93c8d-116">hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:</span><span class="sxs-lookup"><span data-stu-id="93c8d-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="93c8d-117">**이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="93c8d-118">**크기** – hello hello 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="93c8d-119">**만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="93c8d-120">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="93c8d-121">로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="93c8d-122">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="93c8d-123">**시작한 사람** – 일정에 따라 또는 사용자가 수동으로 hello 백업을 자동으로 시작 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="93c8d-124">백업 정책 tooschedule 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="93c8d-125">Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 수동 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="93c8d-126">볼륨에 대한 목록 백업 세트</span><span class="sxs-lookup"><span data-stu-id="93c8d-126">List backup sets for a volume</span></span>
<span data-ttu-id="93c8d-127">다음 단계 toolist hello 볼륨에 대 한 모든 hello 백업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-127">Complete hello following steps toolist all hello backups for a volume.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="93c8d-128">toolist 백업 세트</span><span class="sxs-lookup"><span data-stu-id="93c8d-128">toolist backup sets</span></span>
1. <span data-ttu-id="93c8d-129">Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-129">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="93c8d-130">다음과 같이 필터 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="93c8d-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="93c8d-131">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-131">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="93c8d-132">Hello 드롭 다운 목록에서 볼륨 tooview hello 해당 hello 백업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-132">In hello drop-down list, choose a volume tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="93c8d-133">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-133">Specify hello time range.</span></span>
   4. <span data-ttu-id="93c8d-134">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-134">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="93c8d-136">tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-136">tooexecute this query.</span></span>
      
      <span data-ttu-id="93c8d-137">hello 백업을 선택 하는 hello 볼륨와 관련 된 백업 세트의 hello 목록에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-137">hello backups associated with hello selected volume should appear in hello list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="93c8d-138">백업 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-138">Select a backup set</span></span>
<span data-ttu-id="93c8d-139">다음 단계 tooselect 볼륨 또는 백업 정책에 대 한 하 여 백업 세트 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="93c8d-140">tooselect 백업 세트</span><span class="sxs-lookup"><span data-stu-id="93c8d-140">tooselect a backup set</span></span>
1. <span data-ttu-id="93c8d-141">Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-141">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="93c8d-142">다음과 같이 필터 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="93c8d-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="93c8d-143">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-143">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="93c8d-144">Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-144">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="93c8d-145">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-145">Specify hello time range.</span></span>
   4. <span data-ttu-id="93c8d-146">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-146">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="93c8d-148">tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-148">tooexecute this query.</span></span>
      
      <span data-ttu-id="93c8d-149">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-149">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="93c8d-150">백업 세트를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-150">Select and expand a backup set.</span></span> <span data-ttu-id="93c8d-151">hello **복원** 및 **삭제** 옵션이 hello hello 페이지 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-151">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="93c8d-152">선택한 백업 세트를 hello에 이러한 작업 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-152">You can perform either of these actions on hello backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="93c8d-153">백업 세트 삭제</span><span class="sxs-lookup"><span data-stu-id="93c8d-153">Delete a backup set</span></span>
<span data-ttu-id="93c8d-154">연관 된 tooretain hello 데이터를 더 이상 원하는 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-154">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="93c8d-155">Hello 단계 toodelete 백업 세트 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-155">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="93c8d-156">toodelete 백업 세트</span><span class="sxs-lookup"><span data-stu-id="93c8d-156">toodelete a backup set</span></span>
1. <span data-ttu-id="93c8d-157">Hello StorSimple 관리자 서비스 페이지에서 클릭 hello **백업 카탈로그 탭**합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-157">On hello StorSimple Manager service page, click hello **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="93c8d-158">다음과 같이 필터 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="93c8d-158">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="93c8d-159">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-159">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="93c8d-160">Hello 드롭 다운 목록에서 원하는 tooselect hello 백업에 대 한 hello 볼륨 또는 백업 정책을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-160">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="93c8d-161">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-161">Specify hello time range.</span></span>
   4. <span data-ttu-id="93c8d-162">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-162">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="93c8d-164">tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-164">tooexecute this query.</span></span>
      
      <span data-ttu-id="93c8d-165">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-165">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="93c8d-166">백업 세트를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-166">Select and expand a backup set.</span></span> <span data-ttu-id="93c8d-167">hello **복원** 및 **삭제** 옵션이 hello hello 페이지 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-167">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="93c8d-168">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-168">Click **Delete**.</span></span>
4. <span data-ttu-id="93c8d-169">Hello 삭제가 진행에서 되 고 성공적으로 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-169">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="93c8d-170">Hello 삭제를 완료 한 후이 페이지에 hello 쿼리를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-170">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="93c8d-171">백업 세트를 삭제 하는 hello hello 백업 세트 목록에 더 이상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-171">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93c8d-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93c8d-172">Next steps</span></span>
* <span data-ttu-id="93c8d-173">너무 방법에 대해 알아봅니다[사용 하 여 백업 세트에서 장치를 백업 카탈로그 toorestore hello](storsimple-restore-from-backup-set.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-173">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="93c8d-174">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93c8d-174">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

