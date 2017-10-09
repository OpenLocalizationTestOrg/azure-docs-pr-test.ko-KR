---
title: "aaaManage StorSimple 백업 카탈로그 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 백업 카탈로그 페이지 toolist toouse hello를 선택 하 고 백업 세트를 삭제 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="f28d2-103">사용 하 여 hello StorSimple 장치 관리자 서비스 toomanage 백업 카탈로그</span><span class="sxs-lookup"><span data-stu-id="f28d2-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="f28d2-104">개요</span><span class="sxs-lookup"><span data-stu-id="f28d2-104">Overview</span></span>
<span data-ttu-id="f28d2-105">StorSimple 장치 관리자 서비스 hello **백업 카탈로그** 블레이드 수동 또는 예약 된 백업을 만들 때 만들어진 모든 hello 백업 세트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="f28d2-106">이 페이지 toolist를 모든 hello 백업을 사용 하 여 백업 정책 또는 볼륨을 선택 또는 백업, 삭제 하거나 사용 하거나 수 있습니다 백업 toorestore 볼륨을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="f28d2-107">이 자습서에서는 방법 toolist, select 및 삭제 하 여 백업 세트를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="f28d2-108">toolearn 어떻게 toorestore 백업에서 장치 이동 너무[장치 백업 세트에서 복원](storsimple-8000-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="f28d2-109">볼륨을 tooclone 너무 이동 toolearn[StorSimple 볼륨을 복제](storsimple-8000-clone-volume-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![백업 카탈로그](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="f28d2-111">hello **백업 카탈로그** 블레이드 쿼리 toonarrow 백업 세트 선택 항목을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="f28d2-112">Hello 매개 변수 뒤에 따라 검색 되는 hello 백업 세트를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="f28d2-113">**장치** – hello 장치는 hello에 백업 세트 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="f28d2-114">**백업 정책 또는 볼륨** –이 백업 세트와 연결 된 볼륨 또는 백업 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="f28d2-115">**From 및 To** – hello 백업 세트를 만들 때 날짜 및 시간 범위를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="f28d2-116">hello 필터링 된 백업 세트는 표 형식으로 표시 hello 특성 다음에 따라:</span><span class="sxs-lookup"><span data-stu-id="f28d2-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="f28d2-117">**이름** – hello hello 백업 정책 또는 hello 백업 세트와 연결 된 볼륨의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="f28d2-118">**크기** – hello hello 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="f28d2-119">**만든** hello 날짜 및 시간 hello 백업의 만들었을 당시의 – 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="f28d2-120">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="f28d2-121">로컬 스냅숏은 반면 클라우드 스냅숏은 hello 클라우드에 상주 하는 볼륨 데이터의 백업 toohello hello 장치에 로컬로 저장 된 모든 볼륨 데이터의 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="f28d2-122">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="f28d2-123">**시작한 사람** – 일정에 따라 또는 사용자가 수동으로 hello 백업을 자동으로 시작 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="f28d2-124">백업 정책 tooschedule 백업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="f28d2-125">Hello 또는 사용할 수 있습니다 **백업을** 옵션 tootake 수동 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="f28d2-126">백업 정책에 대한 백업 세트 나열</span><span class="sxs-lookup"><span data-stu-id="f28d2-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="f28d2-127">백업 정책에 대 한 모든 hello 백업을 hello 단계 toolist 다음을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="f28d2-128">toolist 백업 세트</span><span class="sxs-lookup"><span data-stu-id="f28d2-128">toolist backup sets</span></span>
1. <span data-ttu-id="f28d2-129">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="f28d2-130">다음과 같이 필터 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="f28d2-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="f28d2-131">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="f28d2-132">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="f28d2-133">기준으로 필터링 **백업 정책** tooview hello 해당 hello 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="f28d2-134">Hello 백업 정책 드롭다운 목록에서 선택 **모든** tooview 선택한 hello에 대 한 백업을 hello 모든 장치.</span><span class="sxs-lookup"><span data-stu-id="f28d2-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="f28d2-135">클릭 **적용** tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="f28d2-136">선택한 hello 백업 정책과 연결 하는 hello 백업이 백업 세트의 hello 목록에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="f28d2-138">백업 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-138">Select a backup set</span></span>
<span data-ttu-id="f28d2-139">다음 단계 tooselect 볼륨 또는 백업 정책에 대 한 하 여 백업 세트 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="f28d2-140">tooselect 백업 세트</span><span class="sxs-lookup"><span data-stu-id="f28d2-140">tooselect a backup set</span></span>
1. <span data-ttu-id="f28d2-141">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="f28d2-142">다음과 같이 필터 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="f28d2-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="f28d2-143">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="f28d2-144">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="f28d2-145">원하는 tooselect hello 백업에 대 한 볼륨 또는 백업 정책에 의해 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="f28d2-146">클릭 **적용** tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="f28d2-147">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="f28d2-149">백업 세트를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-149">Select and expand a backup set.</span></span> <span data-ttu-id="f28d2-150">이제 hello 백업 세트를 포함 하는 hello 볼륨에 따라 구분을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="f28d2-151">hello **복원** 및 **삭제** 옵션이 hello hello 백업 세트에 대 한 상황에 맞는 메뉴 (오른쪽 클릭)을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="f28d2-152">선택한 백업 세트를 hello에 이러한 작업 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="f28d2-154">백업 세트 삭제</span><span class="sxs-lookup"><span data-stu-id="f28d2-154">Delete a backup set</span></span>
<span data-ttu-id="f28d2-155">연관 된 tooretain hello 데이터를 더 이상 원하는 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="f28d2-156">Hello 단계 toodelete 백업 세트 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="f28d2-157">toodelete 백업 세트</span><span class="sxs-lookup"><span data-stu-id="f28d2-157">toodelete a backup set</span></span>
 <span data-ttu-id="f28d2-158">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="f28d2-159">다음과 같이 필터 hello 선택:</span><span class="sxs-lookup"><span data-stu-id="f28d2-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="f28d2-160">Hello 시간 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="f28d2-161">Hello 적절 한 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="f28d2-162">원하는 tooselect hello 백업에 대 한 볼륨 또는 백업 정책에 의해 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="f28d2-163">클릭 **적용** tooexecute이이 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="f28d2-164">hello hello 선택한 볼륨 또는 백업 정책과 연결 된 백업 목록에 표시 되어야 hello 백업 세트입니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="f28d2-166">백업 세트를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-166">Select and expand a backup set.</span></span> <span data-ttu-id="f28d2-167">이제 hello 백업 세트를 포함 하는 hello 볼륨에 따라 구분을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="f28d2-168">hello **복원** 및 **삭제** 옵션이 hello hello 백업 세트에 대 한 상황에 맞는 메뉴 (오른쪽 클릭)을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="f28d2-169">Hello 선택한 백업 세트를 마우스 오른쪽 단추로 클릭 하 고 hello 상황에 맞는 메뉴에서 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="f28d2-171">확인 메시지가 표시 되 면 hello 표시 정보를 검토 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="f28d2-172">hello 선택한 백업이 영구적으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-172">hello selected backup is deleted permanently.</span></span>

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="f28d2-174">Hello 삭제가 진행에서 되 고 성공적으로 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="f28d2-175">Hello 삭제를 완료 한 후이 페이지에 hello 쿼리를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="f28d2-176">백업 세트를 삭제 하는 hello hello 백업 세트 목록에 더 이상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Toobackup 카탈로그 이동](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="f28d2-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f28d2-178">Next steps</span></span>
* <span data-ttu-id="f28d2-179">너무 방법에 대해 알아봅니다[사용 하 여 백업 세트에서 장치를 백업 카탈로그 toorestore hello](storsimple-8000-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="f28d2-180">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f28d2-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

