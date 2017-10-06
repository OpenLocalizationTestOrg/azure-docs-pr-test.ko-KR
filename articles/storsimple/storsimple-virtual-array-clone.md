---
title: "StorSimple 가상 배열 백업 aaaClone | Microsoft Docs"
description: "자세한 방법을 tooclone 백업 및 StorSimple 가상 배열에서 파일을 복구 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a><span data-ttu-id="612e8-103">StorSimple 가상 배열의 백업에서 복제</span><span class="sxs-lookup"><span data-stu-id="612e8-103">Clone from a backup of your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="612e8-104">개요</span><span class="sxs-lookup"><span data-stu-id="612e8-104">Overview</span></span>

<span data-ttu-id="612e8-105">이 문서에서는 단계별 방법을 tooclone 하 여 백업 세트 공유 또는 볼륨의 Microsoft Azure StorSimple 가상 배열에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-105">This article describes step-by-step how tooclone a backup set of your shares or volumes on your Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="612e8-106">hello 복제 된 백업을 사용 하는 toorecover 삭제 또는 손상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-106">hello cloned backup is used toorecover a deleted or lost file.</span></span> <span data-ttu-id="612e8-107">hello 문서에는 StorSimple 가상 배열에는 항목 수준 복구는 파일 서버로 구성 하는 자세한 단계 tooperform도를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-107">hello article also includes detailed steps tooperform an item-level recovery on your StorSimple Virtual Array configured as a file server.</span></span>

## <a name="clone-shares-from-a-backup-set"></a><span data-ttu-id="612e8-108">백업 세트에서 공유 복제</span><span class="sxs-lookup"><span data-stu-id="612e8-108">Clone shares from a backup set</span></span>

<span data-ttu-id="612e8-109">**Tooclone 공유를 시도 하기 전에 충분 한 공간이 있는지 hello 장치 toocomplete에이 작업을 확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="612e8-109">**Before you try tooclone shares, ensure that you have sufficient space on hello device toocomplete this operation.**</span></span> <span data-ttu-id="612e8-110">hello에 백업에서 tooclone [Azure 포털](https://portal.azure.com/), hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-110">tooclone from a backup, in hello [Azure portal](https://portal.azure.com/), perform hello following steps.</span></span>

#### <a name="tooclone-a-share"></a><span data-ttu-id="612e8-111">tooclone 공유</span><span class="sxs-lookup"><span data-stu-id="612e8-111">tooclone a share</span></span>

1. <span data-ttu-id="612e8-112">너무 찾아보기**장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-112">Browse too**Devices** blade.</span></span> <span data-ttu-id="612e8-113">장치를 선택하고 클릭한 다음 **공유**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-113">Select and click your device and then click **Shares**.</span></span> <span data-ttu-id="612e8-114">Tooclone를 마우스 오른쪽 단추로 클릭 hello 공유 tooinvoke hello 상황에 맞는 메뉴 hello 공유를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-114">Select hello share that you want tooclone, right-click hello share tooinvoke hello context menu.</span></span> <span data-ttu-id="612e8-115">**복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-115">Select **Clone**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. <span data-ttu-id="612e8-117">Hello에 **복제** 블레이드에서 클릭 **백업 > 선택** 수행가 다음를 hello 다음 및:</span><span class="sxs-lookup"><span data-stu-id="612e8-117">In hello **Clone** blade, click **Backup > Select** and then do hello following:</span></span> 
   
   <span data-ttu-id="612e8-118">a.</span><span class="sxs-lookup"><span data-stu-id="612e8-118">a.</span></span>    <span data-ttu-id="612e8-119">Hello 시간 범위에 따라이 장치에서 백업을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-119">Filter a backup on this device based on hello time range.</span></span> <span data-ttu-id="612e8-120">**지난 7일**, **지난 30일** 및 **지난 해** 중에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-120">You can choose from **Past 7 days**, **Past 30 days**, and **Past year**.</span></span>
   
   <span data-ttu-id="612e8-121">b.</span><span class="sxs-lookup"><span data-stu-id="612e8-121">b.</span></span>    <span data-ttu-id="612e8-122">표시 되는 필터링 된 백업 hello 목록에서 백업 tooclone를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-122">In hello list of filtered backups displayed, select a backup tooclone from.</span></span>
   
   <span data-ttu-id="612e8-123">c.</span><span class="sxs-lookup"><span data-stu-id="612e8-123">c.</span></span>    <span data-ttu-id="612e8-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-124">Click **OK**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. <span data-ttu-id="612e8-126">Hello에 **복제** 블레이드에서 클릭 **설정을 대상** 수행가 다음를 hello 다음 및:</span><span class="sxs-lookup"><span data-stu-id="612e8-126">In hello **Clone** blade, click **Target settings** and then do hello following:</span></span>
   
   <span data-ttu-id="612e8-127">a.</span><span class="sxs-lookup"><span data-stu-id="612e8-127">a.</span></span>    <span data-ttu-id="612e8-128">공유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-128">Provide a share name.</span></span> <span data-ttu-id="612e8-129">hello 공유 이름은 3 ~ 127 자 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-129">hello share name must contain 3-127 characters.</span></span>
   
   <span data-ttu-id="612e8-130">b.</span><span class="sxs-lookup"><span data-stu-id="612e8-130">b.</span></span>    <span data-ttu-id="612e8-131">필요에 따라 hello 복제 된 공유에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-131">Optionally provide a description for hello cloned share.</span></span>
   
   <span data-ttu-id="612e8-132">c.</span><span class="sxs-lookup"><span data-stu-id="612e8-132">c.</span></span>    <span data-ttu-id="612e8-133">복원 하는 hello 공유의 hello 유형을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-133">You cannot change hello type of hello share you are restoring to.</span></span> <span data-ttu-id="612e8-134">계층화된 공유는 계층화된 공유로 복제되고 로컬로 고정된 공유는 로컬로 고정된 공유로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-134">A tiered share is cloned as a tiered and a locally pinned share as locally pinned.</span></span>
   
   <span data-ttu-id="612e8-135">d.</span><span class="sxs-lookup"><span data-stu-id="612e8-135">d.</span></span>    <span data-ttu-id="612e8-136">hello 용량에서 복제 하는 hello 공유의 같은 toohello 크기로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-136">hello capacity is set as equal toohello size of hello share you are cloning from.</span></span>
   
   <span data-ttu-id="612e8-137">e.</span><span class="sxs-lookup"><span data-stu-id="612e8-137">e.</span></span>    <span data-ttu-id="612e8-138">이 공유에 대 한 hello 관리자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-138">Assign hello administrators for this share.</span></span> <span data-ttu-id="612e8-139">Hello 복제를 완료 한 후 파일 탐색기를 통해 수 toomodify hello 공유 속성을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-139">You will be able toomodify hello share properties via File Explorer after hello clone is complete.</span></span>
   
   <span data-ttu-id="612e8-140">f.</span><span class="sxs-lookup"><span data-stu-id="612e8-140">f.</span></span>    <span data-ttu-id="612e8-141">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-141">Click **OK**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. <span data-ttu-id="612e8-143">클릭 **복제** toostart 한 복제 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-143">Click **Clone** toostart a clone job.</span></span> <span data-ttu-id="612e8-144">Hello 작업이 완료 되 면 hello 복제 작업 시작 하 고 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-144">After hello job is complete, hello clone operation starts and you are notified.</span></span> <span data-ttu-id="612e8-145">이동 toohello toomonitor hello 진행률 **작업** 블레이드에 대 한 클릭 hello 작업 tooview 작업 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-145">toomonitor hello progress of clone, go toohello **Jobs** blade and click hello job tooview job details.</span></span>
5. <span data-ttu-id="612e8-146">Hello 복제본을 성공적으로 만든 후 뒤로 toohello 이동 **공유** 블레이드 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-146">After hello clone is successfully created, navigate back toohello **Shares** blade on your device.</span></span>
6. <span data-ttu-id="612e8-147">장치에서 공유 hello 목록에서 새 복제 된 공유 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-147">You can now view hello new cloned share in hello list of shares on your device.</span></span> <span data-ttu-id="612e8-148">계층화된 공유는 계층화된 공유로 복제되고 로컬로 고정된 공유는 로컬로 고정된 공유로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-148">A tiered share is cloned as tiered and a locally pinned share as a locally pinned share.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a><span data-ttu-id="612e8-150">백업 세트에서 볼륨 복제</span><span class="sxs-lookup"><span data-stu-id="612e8-150">Clone volumes from a backup set</span></span>

<span data-ttu-id="612e8-151">hello Azure 포털에서에서 백업에서 tooclone 한 tooperform 단계 비슷한 toohello 것을 공유 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-151">tooclone from a backup, in hello Azure portal, you have tooperform steps similar toohello ones when cloning a share.</span></span> <span data-ttu-id="612e8-152">hello에 hello 백업 tooa 새 볼륨을 복제 하는 hello 복제 작업이 동일한 가상 장치 tooa 다른 장치를 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-152">hello clone operation clones hello backup tooa new volume on hello same virtual device; you cannot clone tooa different device.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="612e8-153">tooclone 볼륨</span><span class="sxs-lookup"><span data-stu-id="612e8-153">tooclone a volume</span></span>

1. <span data-ttu-id="612e8-154">너무 찾아보기**장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-154">Browse too**Devices** blade.</span></span> <span data-ttu-id="612e8-155">장치를 선택하고 클릭한 다음 **볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-155">Select and click your device and then click **Volumes**.</span></span> <span data-ttu-id="612e8-156">문자열 hello 볼륨 tooclone, 원하는 단추로 hello 볼륨 tooinvoke hello 상황에 맞는 메뉴를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-156">Selec hello volume that you want tooclone, right-click hello volume tooinvoke hello context menu.</span></span> <span data-ttu-id="612e8-157">**복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-157">Select **Clone**.</span></span>
   
   ![볼륨 복제](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. <span data-ttu-id="612e8-159">Hello에 **복제** 블레이드에서 클릭 **백업** 수행가 다음를 hello 다음 및:</span><span class="sxs-lookup"><span data-stu-id="612e8-159">In hello **Clone** blade, click **Backup** and then do hello following:</span></span> 
   
   <span data-ttu-id="612e8-160">a.</span><span class="sxs-lookup"><span data-stu-id="612e8-160">a.</span></span>    <span data-ttu-id="612e8-161">Hello 시간 범위에 따라이 장치에서 백업을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-161">Filter a backup on this device based on hello time range.</span></span> <span data-ttu-id="612e8-162">**지난 7일**, **지난 30일** 및 **지난 해** 중에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-162">You can choose from **Past 7 days**, **Past 30 days**, and **Past year**.</span></span> 
   
   <span data-ttu-id="612e8-163">b.</span><span class="sxs-lookup"><span data-stu-id="612e8-163">b.</span></span>    <span data-ttu-id="612e8-164">표시 되는 필터링 된 백업 hello 목록에서 백업 tooclone를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-164">In hello list of filtered backups displayed, select a backup tooclone from.</span></span>
   
   <span data-ttu-id="612e8-165">c.</span><span class="sxs-lookup"><span data-stu-id="612e8-165">c.</span></span>    <span data-ttu-id="612e8-166">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-166">Click **OK**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. <span data-ttu-id="612e8-168">Hello에 **복제** 블레이드에서 클릭 **대상 볼륨 설정** 수행가 다음를 hello 다음 고::</span><span class="sxs-lookup"><span data-stu-id="612e8-168">In hello **Clone** blade, click **Target volume settings** and then do hello following::</span></span>
   
   <span data-ttu-id="612e8-169">a.</span><span class="sxs-lookup"><span data-stu-id="612e8-169">a.</span></span> <span data-ttu-id="612e8-170">hello 장치 이름이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-170">hello device name is automatically populated.</span></span>
   
   <span data-ttu-id="612e8-171">b.</span><span class="sxs-lookup"><span data-stu-id="612e8-171">b.</span></span> <span data-ttu-id="612e8-172">Hello에 대 한 볼륨 이름을 제공 **볼륨을 복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-172">Provide a volume name for hello **cloned volume**.</span></span> <span data-ttu-id="612e8-173">hello 볼륨 이름에는 3 too127 문자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-173">hello volume name must contain 3 too127 characters.</span></span>
   
   <span data-ttu-id="612e8-174">c.</span><span class="sxs-lookup"><span data-stu-id="612e8-174">c.</span></span> <span data-ttu-id="612e8-175">hello 볼륨 종류가 toohello 원래 볼륨을 자동으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-175">hello volume type is automatically set toohello original volume.</span></span> <span data-ttu-id="612e8-176">계층화된 볼륨은 계층화된 볼륨으로 복제되고 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-176">A tiered volume is cloned as tiered and a locally pinned volume as locally pinned.</span></span>
   
   <span data-ttu-id="612e8-177">d.</span><span class="sxs-lookup"><span data-stu-id="612e8-177">d.</span></span> <span data-ttu-id="612e8-178">Hello에 대 한 **호스트 연결**, 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-178">For hello **Connected hosts**, click **Select**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. <span data-ttu-id="612e8-180">Hello에 **호스트 연결** 블레이드에서 기존 ACR에서 선택 하거나 새 ACR을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-180">In  hello **Connected hosts** blade, select from an existing ACR or add a new ACR.</span></span> <span data-ttu-id="612e8-181">새 ACR을 tooadd tooprovide ACR 이름 및 IQN hello 호스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-181">tooadd a new ACR, you will need tooprovide an ACR name and hello host IQN.</span></span> <span data-ttu-id="612e8-182">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-182">Click **Select**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. <span data-ttu-id="612e8-184">클릭 **복제** toolaunch 한 복제 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-184">Click **Clone** toolaunch a clone job.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. <span data-ttu-id="612e8-186">Hello 복제 작업을 만든 후 복제 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-186">After hello clone job is created, cloning will start.</span></span> <span data-ttu-id="612e8-187">Hello 복제본을 만든 후 장치에 볼륨 블레이드 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-187">Once hello clone is created, it is displayed on hello Volumes blade on your device.</span></span> <span data-ttu-id="612e8-188">계층화된 볼륨은 계층화된 볼륨으로 복제되고 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-188">Note that a tiered volume is cloned as tiered and a locally pinned volume is cloned as a locally pinned volume.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. <span data-ttu-id="612e8-190">Hello 볼륨 온라인 볼륨의 hello 목록에 표시 될 때, hello 볼륨은 사용 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-190">Once hello volume appears online on hello list of volumes, hello volume is available for use.</span></span> <span data-ttu-id="612e8-191">Hello iSCSI 초기자 호스트에서 iSCSI 초기자 속성 창에서 대상 hello 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-191">On hello iSCSI initiator host, refresh hello list of targets in iSCSI initiator properties window.</span></span> <span data-ttu-id="612e8-192">Hello 복제 볼륨 이름을 포함 하는 새 대상 hello 상태 열에서 '비활성'으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-192">A new target that contains hello cloned volume name should appear as 'inactive' under hello status column.</span></span>
8. <span data-ttu-id="612e8-193">Hello 대상을 선택 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-193">Select hello target and click **Connect**.</span></span> <span data-ttu-id="612e8-194">Hello 초기자가 연결 된 toohello 대상, hello 상태 너무 변경 해야**연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-194">After hello initiator is connected toohello target, hello status should change too**Connected**.</span></span>
9. <span data-ttu-id="612e8-195">Hello에 **디스크 관리** 창 hello 탑재 된 볼륨이 표시 hello 다음 그림에에서 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-195">In hello **Disk Management** window, hello mounted volumes appear as shown in hello following illustration.</span></span> <span data-ttu-id="612e8-196">발견 된 hello 볼륨을 마우스 오른쪽 단추로 클릭 (hello 디스크 이름 클릭)를 클릭 하 고 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-196">Right-click hello discovered volume (click hello disk name), and then click **Online**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="612e8-197">Hello 복제 작업이 실패 하면 볼륨 또는 백업 세트에서 공유 tooclone 시도, 대상 볼륨 또는 공유의 여전히 있습니다 때 hello 포털에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-197">When trying tooclone a volume or a share from a backup set, if hello clone job fails, a target volume or share may still be created in hello portal.</span></span> <span data-ttu-id="612e8-198">이 대상 볼륨을 삭제 하거나이 요소에서 발생 하는 모든 향후 문제 hello 포털 toominimize에서 공유 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-198">It is important that you delete this target volume or share in hello portal toominimize any future issues arising from this element.</span></span>
> 
> 

## <a name="item-level-recovery-ilr"></a><span data-ttu-id="612e8-199">항목 수준 복구(ILR)</span><span class="sxs-lookup"><span data-stu-id="612e8-199">Item-level recovery (ILR)</span></span>

<span data-ttu-id="612e8-200">이 릴리스에 hello 항목 수준 복구를 (ILR) 파일 서버로 구성 하는 StorSimple 가상 배열에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-200">This release introduces hello item-level recovery (ILR) on a StorSimple Virtual Array configured as a file server.</span></span> <span data-ttu-id="612e8-201">hello 기능 hello StorSimple 장치에서 모든 hello 공유의 클라우드 백업에서 파일 및 폴더의 toodo 세분화 된 복구를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-201">hello feature allows you toodo granular recovery of files and folders from a cloud backup of all hello shares on hello StorSimple device.</span></span> <span data-ttu-id="612e8-202">셀프 서비스 모델을 사용하여 최근 백업에서 삭제된 파일을 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-202">You can retrieve deleted files from recent backups using a self-service model.</span></span>

<span data-ttu-id="612e8-203">모든 공유에는 *.backups* hello 가장 최근 백업이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-203">Every share has a *.backups* folder that contains hello most recent backups.</span></span> <span data-ttu-id="612e8-204">원하는 백업 toohello를 탐색 하 고, hello 백업에서 관련 파일 및 폴더를 복사 하 고, 복원할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-204">You can navigate toohello desired backup, copy relevant files and folders from hello backup and restore them.</span></span> <span data-ttu-id="612e8-205">이 기능은 백업에서 복원할 수 있도록 tooadministrators 호출을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-205">This feature eliminates calls tooadministrators for restoring files from backups.</span></span>

1. <span data-ttu-id="612e8-206">Hello ILR를 수행 하는 경우 파일 탐색기를 통해 hello 백업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-206">When performing hello ILR, you can view hello backups through File Explorer.</span></span> <span data-ttu-id="612e8-207">에 대 한 hello 백업에서 toolook 원하는 hello 특정 공유를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-207">Click hello specific share that you want toolook at hello backup for.</span></span> <span data-ttu-id="612e8-208">표시 됩니다는 *.backups* 모든 hello 백업을 저장 하는 hello 공유에 만들어지는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-208">You will see a *.backups* folder created under hello share that stores all hello backups.</span></span> <span data-ttu-id="612e8-209">Hello 확장 *.backups* 폴더 tooview hello 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-209">Expand hello *.backups* folder tooview hello backups.</span></span> <span data-ttu-id="612e8-210">hello 폴더의 전체 백업 계층 hello hello 분해 된 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-210">hello folder shows hello exploded view of hello entire backup hierarchy.</span></span> <span data-ttu-id="612e8-211">이 보기에는 몇 초 toocreate는 대개와 요청 시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-211">This view is created on-demand and usually takes only a couple of seconds toocreate.</span></span>
   
   <span data-ttu-id="612e8-212">hello 마지막 다섯 개 백업 이러한 방식으로 표시 되 고 사용 하는 tooperform 항목 수준 복구 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-212">hello last five backups are displayed in this way and can be used tooperform an item-level recovery.</span></span> <span data-ttu-id="612e8-213">hello 최근 5 개의 백업을 동시에 포함 될 기본 예약 hello 및 수동 백업을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-213">hello five recent backups include both hello default scheduled and hello manual backups.</span></span>
   
   * <span data-ttu-id="612e8-214">**예약된 백업**의 이름은 &lt;장치 이름&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-214">**Scheduled backups** named as &lt;Device name&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC.</span></span>
   * <span data-ttu-id="612e8-215">**수동 백업** 의 이름은 Ad-hoc-YYYYMMDD-HHMMSS-UTC로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-215">**Manual backups** named as Ad-hoc-YYYYMMDD-HHMMSS-UTC.</span></span>
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. <span data-ttu-id="612e8-216">Hello hello 삭제할 파일의 최신 버전을 포함 하는 hello 백업을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-216">Identify hello backup containing hello most recent version of hello deleted file.</span></span> <span data-ttu-id="612e8-217">Hello 폴더 이름 각 hello의 경우 앞에 UTC 타임 스탬프가 들어 있지만 hello는 hello 폴더를 만든 시간은 hello 실제 장치 hello 백업 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-217">Though hello folder name contains a UTC timestamp in each of hello preceding cases, hello time at which hello folder was created is hello actual device time when hello backup started.</span></span> <span data-ttu-id="612e8-218">폴더 타임 스탬프 toolocate hello를 사용 하 고 hello 백업을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-218">Use hello folder timestamp toolocate and identify hello backups.</span></span>

3. <span data-ttu-id="612e8-219">Hello 폴더나 hello 이전 단계에서 식별 된 hello 백업에 toorestore 원하는 hello 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-219">Locate hello folder or hello file that you want toorestore in hello backup that you identified in hello previous step.</span></span> <span data-ttu-id="612e8-220">Note hello 파일 또는 폴더에 권한을 가진 사용자를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-220">Note you can only view hello files or folders that you have permissions for.</span></span> <span data-ttu-id="612e8-221">특정 파일이나 폴더에 액세스할 수 없는 경우 공유 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="612e8-221">If you cannot access certain files or folders, contact a share administrator.</span></span> <span data-ttu-id="612e8-222">관리자에 게는 파일 탐색기 tooedit hello 공유 사용 권한을 사용 하 고 액세스 toohello 특정 파일 또는 폴더 제공 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-222">hello administrator can use File Explorer tooedit hello share permissions and give you access toohello specific file or folder.</span></span> <span data-ttu-id="612e8-223">권장된 모범 사례입니다 hello 공유 관리자는 단일 사용자가 아니라 사용자 그룹 이며</span><span class="sxs-lookup"><span data-stu-id="612e8-223">It is a recommended best practice that hello share administrator is a user group instead of a single user.</span></span>

4. <span data-ttu-id="612e8-224">Hello 파일 또는 hello 폴더 toohello StorSimple 파일 서버에 적절 한 공유에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-224">Copy hello file or hello folder toohello appropriate share on your StorSimple file server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="612e8-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="612e8-225">Next steps</span></span>

<span data-ttu-id="612e8-226">너무 방법에 대 한 자세한[hello 로컬 웹 UI를 사용 하 여 StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="612e8-226">Learn more about how too[administer your StorSimple Virtual Array using hello local web UI](storsimple-ova-web-ui-admin.md).</span></span>

