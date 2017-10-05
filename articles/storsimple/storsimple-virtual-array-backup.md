---
title: "Microsoft Azure StorSimple 가상 배열 백업 자습서 | Microsoft Docs"
description: "StorSimple 가상 배열 공유 및 볼륨을 백업하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="25b72-103">StorSimple 가상 배열에서 공유 또는 볼륨 백업</span><span class="sxs-lookup"><span data-stu-id="25b72-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="25b72-104">개요</span><span class="sxs-lookup"><span data-stu-id="25b72-104">Overview</span></span>

<span data-ttu-id="25b72-105">StorSimple 가상 배열은 파일 서버 또는 iSCSI 서버로 구성할 수 있는 하이브리드 클라우드 저장소 온-프레미스 가상 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="25b72-106">가상 배열을 사용하면 사용자가 장치에서 모든 공유 또는 볼륨의 예약된 백업과 수동 백업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="25b72-107">파일 서버로 구성하면 항목 수준 복구도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="25b72-108">이 자습서에서는 예약된 백업과 수동 백업을 만들고 가상 배열에서 삭제된 파일을 복원하는 항목 수준 복구를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="25b72-109">이 자습서는 StorSimple 가상 배열만에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="25b72-110">8000 시리즈에 대한 내용은 [8000 시리즈 장치에 대한 백업 만들기](storsimple-manage-backup-policies-u2.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="25b72-111">공유 및 볼륨 백업</span><span class="sxs-lookup"><span data-stu-id="25b72-111">Back up shares and volumes</span></span>

<span data-ttu-id="25b72-112">백업은 지정 시간 보호 기능을 제공하고, 복구 기능을 개선하며, 공유 및 볼륨의 복원 시간을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="25b72-113">StorSimple 장치에서 공유 또는 볼륨을 두 가지 방법(**예약** 또는 **수동**)으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="25b72-114">각 메서드는 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="25b72-115">백업 시작 시간 변경</span><span class="sxs-lookup"><span data-stu-id="25b72-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="25b72-116">이 릴리스에서 예약된 백업은 매일 지정된 시간에 실행되고 장치의 모든 공유 또는 볼륨을 백업하는 기본 정책에 따라 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="25b72-117">지금은 예약된 백업에 대한 사용자 지정 정책을 만드는 것이 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="25b72-118">StorSimple 가상 배열에는 하루 중 지정된 시간(22:30)에 시작하여 장치의 모든 공유 또는 볼륨을 하루에 한 번 백업하는 기본 백업 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="25b72-119">백업이 시작되는 시간은 변경할 수 있지만, 빈도 및 보존(보존할 백업의 수를 지정하는)은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="25b72-120">이러한 백업 중에 전체 가상 장치가 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="25b72-121">그러면 잠재적으로 장치의 성능에 영향을 주고 장치에 배포된 워크로드에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="25b72-122">따라서 사용량이 적은 시간에 이러한 백업을 예약하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="25b72-123">기본 백업 시작 시간을 변경하려면 [Azure Portal](https://portal.azure.com/)에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="25b72-124">기본 백업 정책의 시작 시간을 변경하려면</span><span class="sxs-lookup"><span data-stu-id="25b72-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="25b72-125">**장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-125">Go to **Devices**.</span></span> <span data-ttu-id="25b72-126">StorSimple 장치 관리자 서비스에 등록된 장치 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![장치로 이동](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="25b72-128">장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-128">Select and click your device.</span></span> <span data-ttu-id="25b72-129">**설정** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="25b72-130">**관리 > 백업 정책**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-130">Go to **Manage > Backup policies**.</span></span>
   
    ![장치 선택](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="25b72-132">**백업 정책** 블레이드에서 기본 시작 시간은 22시 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="25b72-133">장치 표준 시간대의 일별 일정에 새로운 시작 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![백업 정책으로 이동](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="25b72-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="25b72-136">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="25b72-136">Take a manual backup</span></span>

<span data-ttu-id="25b72-137">예약된 백업뿐만 아니라 장치 데이터의 수동(주문형) 백업도 언제든 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="25b72-138">수동 백업을 만들려면</span><span class="sxs-lookup"><span data-stu-id="25b72-138">To create a manual backup</span></span>

1. <span data-ttu-id="25b72-139">**장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-139">Go to **Devices**.</span></span> <span data-ttu-id="25b72-140">장치를 선택하고 선택한 행의 오른쪽 끝에 있는 **...**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="25b72-141">상황에 맞는 메뉴에서 **백업 수행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-141">From the context menu, select **Take backup**.</span></span>
   
    ![백업 수행으로 이동](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="25b72-143">**백업 수행** 블레이드에서 **백업 수행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="25b72-144">그러면 파일 서버의 모든 공유 또는 iSCSI 서버의 모든 볼륨을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![백업 시작](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="25b72-146">요청 시 백업이 시작되면 백업 작업이 시작되었다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![백업 시작](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="25b72-148">작업이 성공적으로 완료되면 다시 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="25b72-149">그러면 백업 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-149">The backup process then starts.</span></span>
   
    ![백업 작업 생성됨](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="25b72-151">백업 진행 상황을 추적하고 작업 세부 정보를 확인하려면 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="25b72-152">그러면 **작업 세부 정보**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-152">This takes you to  **Job details**.</span></span>
   
     ![백업 작업 세부 정보](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="25b72-154">백업이 완료되면 **관리 > 백업 카탈로그**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="25b72-155">장치에서 모든 공유 또는 볼륨의 클라우드 스냅숏을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![백업 완료됨](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="25b72-157">기존 백업 확인</span><span class="sxs-lookup"><span data-stu-id="25b72-157">View existing backups</span></span>
<span data-ttu-id="25b72-158">기존 백업을 보려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="25b72-159">기존 백업을 보려면</span><span class="sxs-lookup"><span data-stu-id="25b72-159">To view existing backups</span></span>

1. <span data-ttu-id="25b72-160">**장치** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-160">Go to **Devices** blade.</span></span> <span data-ttu-id="25b72-161">장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-161">Select and click your device.</span></span> <span data-ttu-id="25b72-162">**설정** 블레이드에서 **관리 > 백업 카탈로그**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![백업 카탈로그로 이동](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="25b72-164">필터링에 사용할 다음 기준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="25b72-165">**시간 범위** – **지난 1시간**, **지난 24시간**, **지난 7일**, **지난 30일**, **지난 해** 및 **사용자 지정 날짜**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="25b72-166">**장치** – StorSimple 장치 관리자 서비스에 등록된 파일 서버 또는 iSCSI 서버 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="25b72-167">**시작** – 백업 정책에 의해 자동으로 **예약**되거나 사용자에 의해 **수동으로** 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![필터 백업](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="25b72-169">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-169">Click **Apply**.</span></span> <span data-ttu-id="25b72-170">필터링된 백업 목록은 **백업 카탈로그** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="25b72-171">100개의 백업 요소만이 지정된 시간에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![업데이트된 백업 카탈로그](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="25b72-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25b72-173">Next steps</span></span>

<span data-ttu-id="25b72-174">[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25b72-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

