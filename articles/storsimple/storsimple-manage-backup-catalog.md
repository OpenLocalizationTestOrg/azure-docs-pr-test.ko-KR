---
title: "StorSimple 백업 카탈로그 관리 | Microsoft Docs"
description: "StorSimple 관리자 서비스 백업 카탈로그 페이지를 사용하여 볼륨에 대한 백업 세트를 나열, 선택 및 삭제하는 방법을 설명합니다."
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
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="4c6d4-103">StorSimple 관리자 서비스를 사용하여 백업 카탈로그 관리</span><span class="sxs-lookup"><span data-stu-id="4c6d4-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="4c6d4-104">개요</span><span class="sxs-lookup"><span data-stu-id="4c6d4-104">Overview</span></span>
<span data-ttu-id="4c6d4-105">StorSimple 관리자 서비스 **백업 카탈로그** 페이지는 수동 또는 예약된 백업을 수행할 때 생성되는 모든 백업 세트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="4c6d4-106">이 페이지를 사용하여 백업 정책 또는 볼륨에 대한 모든 백업을 나열하거나, 백업을 선택 또는 삭제하거나 백업을 사용하여 볼륨을 복원 또는 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="4c6d4-107">이 자습서에서는 백업 세트를 표시하고 선택하고 삭제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="4c6d4-108">백업에서 장치를 복원하는 방법을 알아보려면 [백업 세트에서 장치 복원](storsimple-restore-from-backup-set.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="4c6d4-109">볼륨 복제 방법을 알아보려면 [StorSimple 볼륨 복제](storsimple-clone-volume.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![백업 카탈로그](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="4c6d4-111">**백업 카탈로그** 페이지는 백업 세트 선택 범위를 좁힐 수 있는 쿼리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="4c6d4-112">다음 매개 변수를 기반으로 검색되는 백업 세트를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="4c6d4-113">**장치** – 백업 세트를 만든 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="4c6d4-114">**백업 정책 또는 볼륨** – 백업 정책 또는 이 백업 세트와 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="4c6d4-115">**시작 및 종료** – 백업 세트를 만든 날짜 및 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="4c6d4-116">그런 다음 필터링된 백업 세트는 다음 특성을 기반으로 표로 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="4c6d4-117">**이름** – 백업 정책 또는 이 백업 세트와 연결된 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="4c6d4-118">**크기** – 백업 세트의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="4c6d4-119">**만든 날짜** – 백업이 만들어진 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="4c6d4-120">**유형** – 백업 세트는 로컬 스냅숏 또는 클라우드 스냅숏일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="4c6d4-121">로컬 스냅숏은 장치에 로컬로 저장된 모든 볼륨 데이터의 백업인 반면 클라우드 스냅숏은 클라우드에 상주하는 볼륨 데이터의 백업을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="4c6d4-122">로컬 스냅숏은 데이터 복구 기능으로 클라우드 스냅숏을 선택하는 반면 빠른 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="4c6d4-123">**시작 기준** – 일정에 따라 자동으로 또는 사용자가 수동으로 백업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="4c6d4-124">백업을 예약하기 위해 백업 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="4c6d4-125">또는 **백업 수행** 옵션을 사용하여 수동 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="4c6d4-126">볼륨에 대한 목록 백업 세트</span><span class="sxs-lookup"><span data-stu-id="4c6d4-126">List backup sets for a volume</span></span>
<span data-ttu-id="4c6d4-127">볼륨에 대한 모든 백업을 나열하려면 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="4c6d4-128">백업 세트를 나열하려면</span><span class="sxs-lookup"><span data-stu-id="4c6d4-128">To list backup sets</span></span>
1. <span data-ttu-id="4c6d4-129">StorSimple 관리자 서비스 페이지에서 **백업 카탈로그** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="4c6d4-130">다음과 같이 선택 항목을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="4c6d4-131">해당 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="4c6d4-132">드롭다운 목록에서 해당 볼륨을 선택하여 백업을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="4c6d4-133">시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-133">Specify the time range.</span></span>
   4. <span data-ttu-id="4c6d4-134">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="4c6d4-134">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="4c6d4-136">을 클릭하여 이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-136">to execute this query.</span></span>
      
      <span data-ttu-id="4c6d4-137">선택한 볼륨과 연결된 백업이 백업 세트의 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="4c6d4-138">백업 세트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-138">Select a backup set</span></span>
<span data-ttu-id="4c6d4-139">볼륨 또는 백업 정책에 백업 세트를 선택 하려면 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="4c6d4-140">백업 세트를 선택하려면</span><span class="sxs-lookup"><span data-stu-id="4c6d4-140">To select a backup set</span></span>
1. <span data-ttu-id="4c6d4-141">StorSimple 관리자 서비스 페이지에서 **백업 카탈로그** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="4c6d4-142">다음과 같이 선택 항목을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="4c6d4-143">해당 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="4c6d4-144">드롭다운 목록에서 선택하려는 백업에 대 한 볼륨 또는 백업 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="4c6d4-145">시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-145">Specify the time range.</span></span>
   4. <span data-ttu-id="4c6d4-146">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="4c6d4-146">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="4c6d4-148">을 클릭하여 이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-148">to execute this query.</span></span>
      
      <span data-ttu-id="4c6d4-149">선택한 볼륨와 연결된 백업을 또는 백업 정책이 백업 세트의 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="4c6d4-150">백업 세트를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-150">Select and expand a backup set.</span></span> <span data-ttu-id="4c6d4-151">**복원** 및 **삭제** 옵션이 페이지의 맨 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="4c6d4-152">선택한 백업 세트에 이러한 동작 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="4c6d4-153">백업 세트 삭제</span><span class="sxs-lookup"><span data-stu-id="4c6d4-153">Delete a backup set</span></span>
<span data-ttu-id="4c6d4-154">백업에 연결된 데이터를 더이상 보존하고 싶지 않은 경우 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="4c6d4-155">백업 세트를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="4c6d4-156">백업 세트를 삭제 하려면</span><span class="sxs-lookup"><span data-stu-id="4c6d4-156">To delete a backup set</span></span>
1. <span data-ttu-id="4c6d4-157">StorSimple 관리자 서비스 페이지에서 **백업 카탈로그**탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="4c6d4-158">다음과 같이 선택 항목을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="4c6d4-159">해당 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="4c6d4-160">드롭다운 목록에서 선택하려는 백업에 대 한 볼륨 또는 백업 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="4c6d4-161">시간 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-161">Specify the time range.</span></span>
   4. <span data-ttu-id="4c6d4-162">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="4c6d4-162">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="4c6d4-164">을 클릭하여 이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-164">to execute this query.</span></span>
      
      <span data-ttu-id="4c6d4-165">선택한 볼륨와 연결된 백업을 또는 백업 정책이 백업 세트의 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="4c6d4-166">백업 세트를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-166">Select and expand a backup set.</span></span> <span data-ttu-id="4c6d4-167">**복원** 및 **삭제** 옵션이 페이지의 맨 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="4c6d4-168">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-168">Click **Delete**.</span></span>
4. <span data-ttu-id="4c6d4-169">삭제가 진행 중일 때와 삭제가 완료되었을 때 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="4c6d4-170">삭제를 완료 한 후 이 페이지의 쿼리를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="4c6d4-171">삭제 된 백업 세트는 백업 세트의 목록에 더이상 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c6d4-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c6d4-172">Next steps</span></span>
* <span data-ttu-id="4c6d4-173">백업 카탈로그를 사용하여 [백업 세트에서 장치를 복원](storsimple-restore-from-backup-set.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="4c6d4-174">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c6d4-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

