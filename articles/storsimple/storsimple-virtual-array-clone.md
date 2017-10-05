---
title: "StorSimple Virtual Array 백업 복제 | Microsoft Docs"
description: "StorSimple 가상 배열에서 백업을 복제하고 파일을 복구하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 768c9a1c906999f4690c9c8f7d075743ab1678ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a><span data-ttu-id="90012-103">StorSimple 가상 배열의 백업에서 복제</span><span class="sxs-lookup"><span data-stu-id="90012-103">Clone from a backup of your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="90012-104">개요</span><span class="sxs-lookup"><span data-stu-id="90012-104">Overview</span></span>

<span data-ttu-id="90012-105">이 문서에서는 Microsoft Azure StorSimple 가상 배열에서 일련의 공유 또는 볼륨의 백업을 복제하는 방법을 단계별로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-105">This article describes step-by-step how to clone a backup set of your shares or volumes on your Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="90012-106">복제된 백업은 삭제 또는 손상 파일을 복구하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-106">The cloned backup is used to recover a deleted or lost file.</span></span> <span data-ttu-id="90012-107">또한 이 문서에서는 파일 서버로 구성된 StorSimple 가상 배열에서 항목 수준 복원을 일어나는 자세한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-107">The article also includes detailed steps to perform an item-level recovery on your StorSimple Virtual Array configured as a file server.</span></span>

## <a name="clone-shares-from-a-backup-set"></a><span data-ttu-id="90012-108">백업 세트에서 공유 복제</span><span class="sxs-lookup"><span data-stu-id="90012-108">Clone shares from a backup set</span></span>

<span data-ttu-id="90012-109">**공유 복제를 시도하기 전에 작업을 완료하기에 충분한 공간이 장치에 있는지 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="90012-109">**Before you try to clone shares, ensure that you have sufficient space on the device to complete this operation.**</span></span> <span data-ttu-id="90012-110">백업에서 복제하려면 [Azure Portal](https://portal.azure.com/)에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-110">To clone from a backup, in the [Azure portal](https://portal.azure.com/), perform the following steps.</span></span>

#### <a name="to-clone-a-share"></a><span data-ttu-id="90012-111">공유를 복제하려면</span><span class="sxs-lookup"><span data-stu-id="90012-111">To clone a share</span></span>

1. <span data-ttu-id="90012-112">**장치** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-112">Browse to **Devices** blade.</span></span> <span data-ttu-id="90012-113">장치를 선택하고 클릭한 다음 **공유**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-113">Select and click your device and then click **Shares**.</span></span> <span data-ttu-id="90012-114">복제하려는 공유를 선택하고 공유를 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-114">Select the share that you want to clone, right-click the share to invoke the context menu.</span></span> <span data-ttu-id="90012-115">**복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-115">Select **Clone**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. <span data-ttu-id="90012-117">**복제** 블레이드에서 **백업 > 선택**을 클릭하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-117">In the **Clone** blade, click **Backup > Select** and then do the following:</span></span> 
   
   <span data-ttu-id="90012-118">a.</span><span class="sxs-lookup"><span data-stu-id="90012-118">a.</span></span>    <span data-ttu-id="90012-119">시간 범위에 따라 이 장치에서 백업을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-119">Filter a backup on this device based on the time range.</span></span> <span data-ttu-id="90012-120">**지난 7일**, **지난 30일** 및 **지난 해** 중에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-120">You can choose from **Past 7 days**, **Past 30 days**, and **Past year**.</span></span>
   
   <span data-ttu-id="90012-121">b.</span><span class="sxs-lookup"><span data-stu-id="90012-121">b.</span></span>    <span data-ttu-id="90012-122">표시되는 필터링된 백업 목록에서 복제할 백업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-122">In the list of filtered backups displayed, select a backup to clone from.</span></span>
   
   <span data-ttu-id="90012-123">c.</span><span class="sxs-lookup"><span data-stu-id="90012-123">c.</span></span>    <span data-ttu-id="90012-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-124">Click **OK**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. <span data-ttu-id="90012-126">**복제** 블레이드에서 **대상 설정**을 클릭하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-126">In the **Clone** blade, click **Target settings** and then do the following:</span></span>
   
   <span data-ttu-id="90012-127">a.</span><span class="sxs-lookup"><span data-stu-id="90012-127">a.</span></span>    <span data-ttu-id="90012-128">공유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-128">Provide a share name.</span></span> <span data-ttu-id="90012-129">공유 이름은 3자에서 127자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-129">The share name must contain 3-127 characters.</span></span>
   
   <span data-ttu-id="90012-130">b.</span><span class="sxs-lookup"><span data-stu-id="90012-130">b.</span></span>    <span data-ttu-id="90012-131">필요에 따라 복제된 공유에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-131">Optionally provide a description for the cloned share.</span></span>
   
   <span data-ttu-id="90012-132">c.</span><span class="sxs-lookup"><span data-stu-id="90012-132">c.</span></span>    <span data-ttu-id="90012-133">복원 중인 공유의 유형을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-133">You cannot change the type of the share you are restoring to.</span></span> <span data-ttu-id="90012-134">계층화된 공유는 계층화된 공유로 복제되고 로컬로 고정된 공유는 로컬로 고정된 공유로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-134">A tiered share is cloned as a tiered and a locally pinned share as locally pinned.</span></span>
   
   <span data-ttu-id="90012-135">d.</span><span class="sxs-lookup"><span data-stu-id="90012-135">d.</span></span>    <span data-ttu-id="90012-136">용량은 복제 중인 공유의 크기와 동일한 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-136">The capacity is set as equal to the size of the share you are cloning from.</span></span>
   
   <span data-ttu-id="90012-137">e.</span><span class="sxs-lookup"><span data-stu-id="90012-137">e.</span></span>    <span data-ttu-id="90012-138">이 공유의 관리자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-138">Assign the administrators for this share.</span></span> <span data-ttu-id="90012-139">복제가 완료되면 파일 탐색기를 통해 공유 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-139">You will be able to modify the share properties via File Explorer after the clone is complete.</span></span>
   
   <span data-ttu-id="90012-140">f.</span><span class="sxs-lookup"><span data-stu-id="90012-140">f.</span></span>    <span data-ttu-id="90012-141">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-141">Click **OK**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. <span data-ttu-id="90012-143">**복제**를 클릭하여 복제 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-143">Click **Clone** to start a clone job.</span></span> <span data-ttu-id="90012-144">작업이 완료되면 복제 작업이 시작되고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-144">After the job is complete, the clone operation starts and you are notified.</span></span> <span data-ttu-id="90012-145">복제본의 진행률을 모니터링하려면 **작업** 블레이드로 이동하고 작업을 클릭하여 작업 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="90012-145">To monitor the progress of clone, go to the **Jobs** blade and click the job to view job details.</span></span>
5. <span data-ttu-id="90012-146">복제본이 성공적으로 만들어지면 장치에서 **공유** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="90012-146">After the clone is successfully created, navigate back to the **Shares** blade on your device.</span></span>
6. <span data-ttu-id="90012-147">장치의 공유 목록에서 새로 복제된 공유를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-147">You can now view the new cloned share in the list of shares on your device.</span></span> <span data-ttu-id="90012-148">계층화된 공유는 계층화된 공유로 복제되고 로컬로 고정된 공유는 로컬로 고정된 공유로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-148">A tiered share is cloned as tiered and a locally pinned share as a locally pinned share.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a><span data-ttu-id="90012-150">백업 세트에서 볼륨 복제</span><span class="sxs-lookup"><span data-stu-id="90012-150">Clone volumes from a backup set</span></span>

<span data-ttu-id="90012-151">Azure Portal에서 백업을 복제하려면 공유를 복제하는 경우와 비슷한 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-151">To clone from a backup, in the Azure portal, you have to perform steps similar to the ones when cloning a share.</span></span> <span data-ttu-id="90012-152">복제 작업은 동일한 가상 장치의 새 볼륨에 백업을 복제합니다. 다른 장치에 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-152">The clone operation clones the backup to a new volume on the same virtual device; you cannot clone to a different device.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="90012-153">볼륨 복제하기</span><span class="sxs-lookup"><span data-stu-id="90012-153">To clone a volume</span></span>

1. <span data-ttu-id="90012-154">**장치** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-154">Browse to **Devices** blade.</span></span> <span data-ttu-id="90012-155">장치를 선택하고 클릭한 다음 **볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-155">Select and click your device and then click **Volumes**.</span></span> <span data-ttu-id="90012-156">복제하려는 볼륨을 선택하고 볼륨을 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-156">Selec the volume that you want to clone, right-click the volume to invoke the context menu.</span></span> <span data-ttu-id="90012-157">**복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-157">Select **Clone**.</span></span>
   
   ![볼륨 복제](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. <span data-ttu-id="90012-159">**복제** 블레이드에서 **백업**을 클릭하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-159">In the **Clone** blade, click **Backup** and then do the following:</span></span> 
   
   <span data-ttu-id="90012-160">a.</span><span class="sxs-lookup"><span data-stu-id="90012-160">a.</span></span>    <span data-ttu-id="90012-161">시간 범위에 따라 이 장치에서 백업을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-161">Filter a backup on this device based on the time range.</span></span> <span data-ttu-id="90012-162">**지난 7일**, **지난 30일** 및 **지난 해** 중에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-162">You can choose from **Past 7 days**, **Past 30 days**, and **Past year**.</span></span> 
   
   <span data-ttu-id="90012-163">b.</span><span class="sxs-lookup"><span data-stu-id="90012-163">b.</span></span>    <span data-ttu-id="90012-164">표시되는 필터링된 백업 목록에서 복제할 백업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-164">In the list of filtered backups displayed, select a backup to clone from.</span></span>
   
   <span data-ttu-id="90012-165">c.</span><span class="sxs-lookup"><span data-stu-id="90012-165">c.</span></span>    <span data-ttu-id="90012-166">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-166">Click **OK**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. <span data-ttu-id="90012-168">**복제** 블레이드에서 **대상 볼륨 설정**을 클릭하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-168">In the **Clone** blade, click **Target volume settings** and then do the following::</span></span>
   
   <span data-ttu-id="90012-169">a.</span><span class="sxs-lookup"><span data-stu-id="90012-169">a.</span></span> <span data-ttu-id="90012-170">장치 이름은 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="90012-170">The device name is automatically populated.</span></span>
   
   <span data-ttu-id="90012-171">b.</span><span class="sxs-lookup"><span data-stu-id="90012-171">b.</span></span> <span data-ttu-id="90012-172">**복제된 볼륨**의 볼륨 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-172">Provide a volume name for the **cloned volume**.</span></span> <span data-ttu-id="90012-173">볼륨 이름은 3자에서 127자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-173">The volume name must contain 3 to 127 characters.</span></span>
   
   <span data-ttu-id="90012-174">c.</span><span class="sxs-lookup"><span data-stu-id="90012-174">c.</span></span> <span data-ttu-id="90012-175">볼륨 유형은 원래 볼륨으로 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-175">The volume type is automatically set to the original volume.</span></span> <span data-ttu-id="90012-176">계층화된 볼륨은 계층화된 볼륨으로 복제되고 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-176">A tiered volume is cloned as tiered and a locally pinned volume as locally pinned.</span></span>
   
   <span data-ttu-id="90012-177">d.</span><span class="sxs-lookup"><span data-stu-id="90012-177">d.</span></span> <span data-ttu-id="90012-178">**연결된 호스트**에서 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-178">For the **Connected hosts**, click **Select**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. <span data-ttu-id="90012-180">**연결된 호스트** 블레이드에서 기존 ACR에서 선택하거나 새 ACR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-180">In  the **Connected hosts** blade, select from an existing ACR or add a new ACR.</span></span> <span data-ttu-id="90012-181">새 ACR을 추가하려면 ACR 이름 및 호스트 IQN을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-181">To add a new ACR, you will need to provide an ACR name and the host IQN.</span></span> <span data-ttu-id="90012-182">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-182">Click **Select**.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. <span data-ttu-id="90012-184">**복제**를 클릭하여 복제 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-184">Click **Clone** to launch a clone job.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. <span data-ttu-id="90012-186">복제 작업을 만든 후에 복제가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-186">After the clone job is created, cloning will start.</span></span> <span data-ttu-id="90012-187">복제본이 만들어지면 장치의 볼륨 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-187">Once the clone is created, it is displayed on the Volumes blade on your device.</span></span> <span data-ttu-id="90012-188">계층화된 볼륨은 계층화된 볼륨으로 복제되고 로컬로 고정된 볼륨은 로컬로 고정된 볼륨으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-188">Note that a tiered volume is cloned as tiered and a locally pinned volume is cloned as a locally pinned volume.</span></span>
   
   ![백업 복제](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. <span data-ttu-id="90012-190">볼륨 목록에 볼륨이 온라인 상태로 표시되면 볼륨을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-190">Once the volume appears online on the list of volumes, the volume is available for use.</span></span> <span data-ttu-id="90012-191">iSCSI 초기자 호스트에서 iSCSI 초기자 속성 창의 대상 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-191">On the iSCSI initiator host, refresh the list of targets in iSCSI initiator properties window.</span></span> <span data-ttu-id="90012-192">복제된 볼륨 이름이 포함된 새 대상은 상태 열 아래에 '비활성'으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-192">A new target that contains the cloned volume name should appear as 'inactive' under the status column.</span></span>
8. <span data-ttu-id="90012-193">대상을 선택하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-193">Select the target and click **Connect**.</span></span> <span data-ttu-id="90012-194">초기자가 대상에 연결되면 상태가 **연결됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-194">After the initiator is connected to the target, the status should change to **Connected**.</span></span>
9. <span data-ttu-id="90012-195">**디스크 관리** 창에 탑재된 볼륨이 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-195">In the **Disk Management** window, the mounted volumes appear as shown in the following illustration.</span></span> <span data-ttu-id="90012-196">검색된 볼륨을 마우스 오른쪽 단추로 클릭(디스크 이름 클릭)한 다음 **온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-196">Right-click the discovered volume (click the disk name), and then click **Online**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90012-197">백업 집합에서 볼륨 또는 공유를 복제할 때 복제 작업에 실패한 경우 포털에서 대상 볼륨 또는 공유를 계속 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-197">When trying to clone a volume or a share from a backup set, if the clone job fails, a target volume or share may still be created in the portal.</span></span> <span data-ttu-id="90012-198">향후 이 요소로 인해 발생하는 문제를 최소화하려면 포털에서 이 대상 볼륨 또는 공유를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-198">It is important that you delete this target volume or share in the portal to minimize any future issues arising from this element.</span></span>
> 
> 

## <a name="item-level-recovery-ilr"></a><span data-ttu-id="90012-199">항목 수준 복구(ILR)</span><span class="sxs-lookup"><span data-stu-id="90012-199">Item-level recovery (ILR)</span></span>

<span data-ttu-id="90012-200">이 릴리스는 파일 서버로 구성된 StorSimple 가상 배열의 항목 수준 복구(ILR)를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-200">This release introduces the item-level recovery (ILR) on a StorSimple Virtual Array configured as a file server.</span></span> <span data-ttu-id="90012-201">이 기능을 사용하여 StorSimple 장치에 있는 모든 공유의 클라우드 백업에서 파일과 폴더를 세부적으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-201">The feature allows you to do granular recovery of files and folders from a cloud backup of all the shares on the StorSimple device.</span></span> <span data-ttu-id="90012-202">셀프 서비스 모델을 사용하여 최근 백업에서 삭제된 파일을 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-202">You can retrieve deleted files from recent backups using a self-service model.</span></span>

<span data-ttu-id="90012-203">모든 공유에는 최신 백업을 포함하는 *.backups* 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-203">Every share has a *.backups* folder that contains the most recent backups.</span></span> <span data-ttu-id="90012-204">원하는 백업으로 이동하고, 백업에서 적절한 파일과 폴더를 복사하여 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-204">You can navigate to the desired backup, copy relevant files and folders from the backup and restore them.</span></span> <span data-ttu-id="90012-205">이 기능은 백업에서 파일을 복원하기 위해 관리자를 호출할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-205">This feature eliminates calls to administrators for restoring files from backups.</span></span>

1. <span data-ttu-id="90012-206">ILR을 수행할 때 파일 탐색기를 통해 백업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-206">When performing the ILR, you can view the backups through File Explorer.</span></span> <span data-ttu-id="90012-207">백업을 살펴보려면 특정 공유를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-207">Click the specific share that you want to look at the backup for.</span></span> <span data-ttu-id="90012-208">모든 백업을 저장하는 공유 아래에 만들어진 *.backups* 폴더를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-208">You will see a *.backups* folder created under the share that stores all the backups.</span></span> <span data-ttu-id="90012-209">백업을 보려면 *.backups* 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-209">Expand the *.backups* folder to view the backups.</span></span> <span data-ttu-id="90012-210">폴더는 전체 백업 계층 구조의 쪼개진 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90012-210">The folder shows the exploded view of the entire backup hierarchy.</span></span> <span data-ttu-id="90012-211">이 보기는 주문형으로 만들어지며 일반적으로 몇 초 안에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="90012-211">This view is created on-demand and usually takes only a couple of seconds to create.</span></span>
   
   <span data-ttu-id="90012-212">마지막 백업 5개가 이러한 방식으로 표시되며 항목 수준 복구를 수행하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-212">The last five backups are displayed in this way and can be used to perform an item-level recovery.</span></span> <span data-ttu-id="90012-213">최근 백업 5개에는 기본 예약된 백업 및 수동 백업이 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-213">The five recent backups include both the default scheduled and the manual backups.</span></span>
   
   * <span data-ttu-id="90012-214">**예약된 백업**의 이름은 &lt;장치 이름&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-214">**Scheduled backups** named as &lt;Device name&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC.</span></span>
   * <span data-ttu-id="90012-215">**수동 백업** 의 이름은 Ad-hoc-YYYYMMDD-HHMMSS-UTC로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="90012-215">**Manual backups** named as Ad-hoc-YYYYMMDD-HHMMSS-UTC.</span></span>
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. <span data-ttu-id="90012-216">삭제된 파일의 최신 버전을 포함하는 백업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-216">Identify the backup containing the most recent version of the deleted file.</span></span> <span data-ttu-id="90012-217">앞서 모든 경우에서 폴더 이름에 UTC 타임스탬프가 포함되며, 폴더가 만들어진 시간은 백업이 시작될 당시 장치의 실제 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="90012-217">Though the folder name contains a UTC timestamp in each of the preceding cases, the time at which the folder was created is the actual device time when the backup started.</span></span> <span data-ttu-id="90012-218">폴더 타임스탬프를 사용하여 백업을 찾고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-218">Use the folder timestamp to locate and identify the backups.</span></span>

3. <span data-ttu-id="90012-219">이전 단계에서 확인한 백업에서 복원하려는 폴더 또는 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-219">Locate the folder or the file that you want to restore in the backup that you identified in the previous step.</span></span> <span data-ttu-id="90012-220">사용 권한이 있는 파일 또는 폴더만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-220">Note you can only view the files or folders that you have permissions for.</span></span> <span data-ttu-id="90012-221">특정 파일이나 폴더에 액세스할 수 없는 경우 공유 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="90012-221">If you cannot access certain files or folders, contact a share administrator.</span></span> <span data-ttu-id="90012-222">관리자는 파일 탐색기를 사용하여 공유 사용 권한을 편집하고 특정 파일 또는 폴더에 대한 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-222">The administrator can use File Explorer to edit the share permissions and give you access to the specific file or folder.</span></span> <span data-ttu-id="90012-223">공유 관리자는 단일 사용자가 아닌 사용자 그룹이 되도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90012-223">It is a recommended best practice that the share administrator is a user group instead of a single user.</span></span>

4. <span data-ttu-id="90012-224">파일 또는 폴더를 StorSimple 파일 서버의 적절한 공유에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="90012-224">Copy the file or the folder to the appropriate share on your StorSimple file server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90012-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90012-225">Next steps</span></span>

<span data-ttu-id="90012-226">[로컬 웹 UI를 사용하여 StorSimple 가상 배열을 관리](storsimple-ova-web-ui-admin.md)하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="90012-226">Learn more about how to [administer your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span></span>

