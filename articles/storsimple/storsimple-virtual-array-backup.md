---
title: "aaaMicrosoft Azure StorSimple 가상 배열 백업 자습서 | Microsoft Docs"
description: "Tooback StorSimple 가상 배열을 공유 하는 방법 및 볼륨에 설명 합니다."
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
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="e10f7-103">StorSimple 가상 배열에서 공유 또는 볼륨 백업</span><span class="sxs-lookup"><span data-stu-id="e10f7-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="e10f7-104">개요</span><span class="sxs-lookup"><span data-stu-id="e10f7-104">Overview</span></span>

<span data-ttu-id="e10f7-105">hello StorSimple 가상 배열은 하이브리드 클라우드 저장소 온-프레미스 가상 장치는 파일 서버 또는 iSCSI 서버로 구성 될 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="e10f7-106">hello 가상 배열 hello 사용자 toocreate 모든 hello 공유 또는 볼륨의 예약 된 구성과 수동 백업을 hello 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="e10f7-107">파일 서버로 구성하면 항목 수준 복구도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="e10f7-108">이 자습서는 toocreate 예약 하는 방법 및 수동 백업에 설명 하 고 항목 수준의 복구 toorestore 가상 배열에 있는 삭제 된 파일을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="e10f7-109">이 자습서 toohello StorSimple 가상 배열만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="e10f7-110">8000 시리즈에 대 한 내용은 이동 너무[8000 시리즈 장치에 대 한 백업 만들기](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="e10f7-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="e10f7-111">공유 및 볼륨 백업</span><span class="sxs-lookup"><span data-stu-id="e10f7-111">Back up shares and volumes</span></span>

<span data-ttu-id="e10f7-112">백업은 지정 시간 보호 기능을 제공하고, 복구 기능을 개선하며, 공유 및 볼륨의 복원 시간을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="e10f7-113">StorSimple 장치에서 공유 또는 볼륨을 두 가지 방법(**예약** 또는 **수동**)으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="e10f7-114">Hello 메서드는 각각 hello 다음 섹션에서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="e10f7-115">Hello 백업 시작 시간 변경</span><span class="sxs-lookup"><span data-stu-id="e10f7-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="e10f7-116">이 릴리스에서 예약 된 백업은 지정된 시간에 매일 실행 하 고 hello 장치에서 모든 hello 공유 또는 볼륨을 백업 하는 기본 정책에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="e10f7-117">이 이번에 예약 된 백업에 대 한 사용자 지정 정책 가능한 toocreate 않습니다 것.</span><span class="sxs-lookup"><span data-stu-id="e10f7-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="e10f7-118">StorSimple 가상 배열 (22 시 30) 하루 중 지정된 된 시간에 시작 하 고 하루에 한 번 hello 장치에서 모든 hello 공유 또는 볼륨을 백업 하는 기본 백업 정책을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="e10f7-119">hello 백업 시작 하지만 hello 빈도 및 hello에 보존 (백업 tooretain hello 수를 지정)는를 변경할 수 없는 hello 시간을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="e10f7-120">이러한 백업 하는 동안 전체 가상 장치 hello 백업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="e10f7-121">잠재적으로 hello 장치의 hello 성능에 영향을 하 고 hello 장치에 배포 된 hello 워크 로드에 영향을 줄 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="e10f7-122">따라서 사용량이 적은 시간에 이러한 백업을 예약하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="e10f7-123">toochange hello 기본 백업 시작 시간, hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="e10f7-124">toochange hello 시작 hello 기본 백업 정책에 대 한 시간</span><span class="sxs-lookup"><span data-stu-id="e10f7-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="e10f7-125">너무 이동**장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-125">Go too**Devices**.</span></span> <span data-ttu-id="e10f7-126">StorSimple 장치 관리자 서비스에 등록 된 장치의 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![toodevices 이동](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="e10f7-128">장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-128">Select and click your device.</span></span> <span data-ttu-id="e10f7-129">hello **설정을** 블레이드를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="e10f7-130">너무 이동**관리 > 백업 정책이**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-130">Go too**Manage > Backup policies**.</span></span>
   
    ![장치 선택](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="e10f7-132">Hello에 **백업 정책이** 블레이드에서 hello 기본 시작 시간은 22 시 30입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="e10f7-133">장치 표준 시간대의 hello hello 일별 일정에 대 한 새 시작 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![toobackup 정책 이동](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="e10f7-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="e10f7-136">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="e10f7-136">Take a manual backup</span></span>

<span data-ttu-id="e10f7-137">또한 tooscheduled 백업을 언제 든 지 장치 데이터의 수동 (주문형) 백업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="e10f7-138">toocreate 수동 백업</span><span class="sxs-lookup"><span data-stu-id="e10f7-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="e10f7-139">너무 이동**장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-139">Go too**Devices**.</span></span> <span data-ttu-id="e10f7-140">장치를 선택 하 고 마우스 오른쪽 단추로 클릭 **중...**  hello 맨 오른쪽에 hello 선택 된 행에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="e10f7-141">Hello 상황에 맞는 메뉴에서 선택 **백업을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-141">From hello context menu, select **Take backup**.</span></span>
   
    ![tootake 백업 이동](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="e10f7-143">Hello에 **백업 수행** 블레이드에서 클릭 **백업을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="e10f7-144">그러면 hello 파일 서버의 모든 hello 공유 또는 iSCSI 서버에 있는 모든 hello 볼륨에 백업 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![백업 시작](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="e10f7-146">요청 시 백업이 시작되면 백업 작업이 시작되었다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![백업 시작](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="e10f7-148">Hello 작업이 성공적으로 완료 되 면 다시 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="e10f7-149">hello 백업 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-149">hello backup process then starts.</span></span>
   
    ![백업 작업 생성됨](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="e10f7-151">hello 백업과 hello 작업 세부 정보를 살펴보고 tootrack hello 진행률 hello 알림을 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e10f7-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="e10f7-152">이렇게 하면 너무 **작업 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-152">This takes you too **Job details**.</span></span>
   
     ![백업 작업 세부 정보](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="e10f7-154">Hello 백업이 완료 된 후 너무 이동**관리 > 백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="e10f7-155">장치에서 모든 hello 공유 (또는 볼륨)의 클라우드 스냅숏을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![백업 완료됨](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="e10f7-157">기존 백업 확인</span><span class="sxs-lookup"><span data-stu-id="e10f7-157">View existing backups</span></span>
<span data-ttu-id="e10f7-158">tooview hello 기존 백업 hello hello Azure 포털의에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="e10f7-159">tooview 기존 백업</span><span class="sxs-lookup"><span data-stu-id="e10f7-159">tooview existing backups</span></span>

1. <span data-ttu-id="e10f7-160">너무 이동**장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-160">Go too**Devices** blade.</span></span> <span data-ttu-id="e10f7-161">장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-161">Select and click your device.</span></span> <span data-ttu-id="e10f7-162">Hello에 **설정** 블레이드에서 너무 이동**관리 > 백업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Toobackup 카탈로그 이동](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="e10f7-164">필터링에 사용 되는 조건을 toobe 다음 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="e10f7-165">**시간 범위** – **지난 1시간**, **지난 24시간**, **지난 7일**, **지난 30일**, **지난 해** 및 **사용자 지정 날짜**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="e10f7-166">**장치** – 파일 서버 또는 StorSimple 장치 관리자 서비스에 등록 된 iSCSI 서버 hello 목록 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="e10f7-167">**시작** – 백업 정책에 의해 자동으로 **예약**되거나 사용자에 의해 **수동으로** 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![필터 백업](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="e10f7-169">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-169">Click **Apply**.</span></span> <span data-ttu-id="e10f7-170">hello 백업 필터링 된 목록에에서 표시 됩니다 hello **백업 카탈로그** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="e10f7-171">100개의 백업 요소만이 지정된 시간에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![업데이트된 백업 카탈로그](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="e10f7-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e10f7-173">Next steps</span></span>

<span data-ttu-id="e10f7-174">[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e10f7-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

