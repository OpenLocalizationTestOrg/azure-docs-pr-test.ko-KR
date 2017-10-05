---
title: "StorSimple 8000 시리즈 실제 장치로 StorSimple 장애 조치(failover), 재해 복구 | Microsoft Docs"
description: "다른 실제 장치로 StorSimple 8000 시리즈 실제 장치를 장애 조치(failover)하는 방법에 대해 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: f3ac9545a341fc24ca12c9f2547805d6956cd98a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-a-storsimple-8000-series-physical-device"></a><span data-ttu-id="82310-103">StorSimple 8000 시리즈 실제 장치에 장애 조치</span><span class="sxs-lookup"><span data-stu-id="82310-103">Fail over to a StorSimple 8000 series physical device</span></span>

## <a name="overview"></a><span data-ttu-id="82310-104">개요</span><span class="sxs-lookup"><span data-stu-id="82310-104">Overview</span></span>

<span data-ttu-id="82310-105">이 자습서에서는 재해가 발생하는 경우 StorSimple 8000 시리즈 실제 장치를 다른 StorSimple 실제 장치로 장애 조치(failover)하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to another StorSimple physical device if there is a disaster.</span></span> <span data-ttu-id="82310-106">StorSimple에서는 장치 장애 조치(failover) 기능을 사용하여 데이터 센터의 원본 물리적 장치에서 다른 물리적 장치로 데이터를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="82310-107">이 자습서의 지침은 소프트웨어 버전 업데이트 3 이상을 실행하는 StorSimple 8000 시리즈 물리적 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="82310-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="82310-108">장치 장애 조치(failover) 및 재해 복구에 사용되는 방법에 대해 자세히 알아보려면 [StorSimple 8000 시리즈 장치에 대한 장애 조치(failover) 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="82310-109">StorSimple 물리적 장치를 StorSimple Cloud Appliance로 장애 조치(failover)하려면 [StorSimple Cloud Appliance로 장애 조치(failover)](storsimple-8000-device-failover-cloud-appliance.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-109">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span> <span data-ttu-id="82310-110">실제 장치를 자체 장치로 장애 조치(failover)하려면 [동일한 StorSimple 물리적 장치로 장애 조치(failover)](storsimple-8000-device-failover-same-device.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-110">To fail over a physical device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="82310-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="82310-111">Prerequisites</span></span>

- <span data-ttu-id="82310-112">장치 장애 조치(failover)에 대한 고려 사항을 검토했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="82310-113">자세한 내용을 보려면 [장치 장애 조치(failover)에 대한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="82310-114">데이터 센터에서 배포된 StorSimple 8000 시리즈 실제 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-114">You must have a StorSimple 8000 series physical device deployed in the datacenter.</span></span> <span data-ttu-id="82310-115">장치는 업데이트 3 이후 소프트웨어 버전을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-115">The device must run Update 3 or later software version.</span></span> <span data-ttu-id="82310-116">자세한 내용은 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-116">For more information, go to [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>


## <a name="steps-to-fail-over-to-a-physical-device"></a><span data-ttu-id="82310-117">실제 장치로 장애 조치하는 단계</span><span class="sxs-lookup"><span data-stu-id="82310-117">Steps to fail over to a physical device</span></span>

<span data-ttu-id="82310-118">대상 실제 장치에 장치를 복원하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-118">Perform the following steps to restore your device to a target physical device.</span></span>

1. <span data-ttu-id="82310-119">장애 조치하려는 볼륨 컨테이너에 연결된 클라우드 스냅숏이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-119">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="82310-120">자세한 내용을 보려면 [StorSimple 장치 관리자 서비스를 사용하여 백업 만들기](storsimple-8000-manage-backup-policies-u2.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-120">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="82310-121">StorSimple 장치 관리자로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-121">Go to your StorSimple Device Manager and then click **Devices**.</span></span> <span data-ttu-id="82310-122">**장치** 블레이드에서 서비스와 연결된 장치 목록으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-122">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="82310-123">![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="82310-123">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span></span>
3. <span data-ttu-id="82310-124">원본 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-124">Select and click your source device.</span></span> <span data-ttu-id="82310-125">원본 장치에는 장애 조치(failover)하려는 볼륨 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82310-125">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="82310-126">**설정 > 볼륨 컨테이너**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-126">Go to **Settings > Volume Containers**.</span></span>
4. <span data-ttu-id="82310-127">다른 장치에 장애 조치하려는 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-127">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="82310-128">볼륨 컨테이너를 클릭하여 이 컨테이너 내에 볼륨의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-128">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="82310-129">볼륨을 선택하고 마우스 오른쪽 단추를 클릭한 다음, **오프라인으로 전환**을 클릭하여 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-129">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span> <span data-ttu-id="82310-130">볼륨 컨테이너의 모든 볼륨에 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-130">Repeat this process for all the volumes in the volume container.</span></span>
5. <span data-ttu-id="82310-131">다른 장치에 장애 조치하려는 모든 볼륨 컨테이너에 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-131">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>
6. <span data-ttu-id="82310-132">**장치** 블레이드로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-132">Go back to the **Devices** blade.</span></span> <span data-ttu-id="82310-133">명령 모음에서 **장애 조치(failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-133">From the command bar, click **Fail over**.</span></span>
    <span data-ttu-id="82310-134">![장애 조치(failover) 클릭](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span><span class="sxs-lookup"><span data-stu-id="82310-134">![Click fail over](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span></span>
    
7. <span data-ttu-id="82310-135">**장애 조치(failover)** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-135">In the **Fail over** blade, perform the following steps:</span></span>
   
   1. <span data-ttu-id="82310-136">**원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-136">Click **Source**.</span></span> <span data-ttu-id="82310-137">클라우드 스냅숏과 연결된 볼륨이 있는 볼륨 컨테이너가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82310-137">The volume containers with volumes associated with cloud snapshots are displayed.</span></span> <span data-ttu-id="82310-138">표시된 컨테이너만이 장애 조치의 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82310-138">Only the containers displayed are eligible for failover.</span></span> <span data-ttu-id="82310-139">볼륨 컨테이너 목록에서 장애 조치할 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-139">In the list of volume containers, select the volume containers you would like to fail over.</span></span> <span data-ttu-id="82310-140">**클라우드 스냅숏과 연결된 볼륨 컨테이너와 오프라인 볼륨만 표시됩니다.**</span><span class="sxs-lookup"><span data-stu-id="82310-140">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>

       ![원본 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. <span data-ttu-id="82310-142">**대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-142">Click **Target**.</span></span> <span data-ttu-id="82310-143">이전 단계에서 선택한 볼륨 컨테이너의 경우 사용 가능한 장치의 드롭다운 목록에서 대상 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-143">For the volume containers selected in the previous step, select a target device from the drop-down list of available devices.</span></span> <span data-ttu-id="82310-144">원본 볼륨 컨테이너를 수용할 수용작업량이 충분한 장치만 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82310-144">Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.</span></span>

        ![대상 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. <span data-ttu-id="82310-146">마지막으로 **요약**에서 모든 장애 조치 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-146">Finally, review all the failover settings under **Summary**.</span></span> <span data-ttu-id="82310-147">설정을 검토한 후에 선택한 볼륨 컨테이너의 볼륨이 오프라인 상태임을 나타내는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-147">After you have reviewed the settings, select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> <span data-ttu-id="82310-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-148">Click **OK**.</span></span>

       ![장애 조치(failover) 설정 검토](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. <span data-ttu-id="82310-150">StorSimple은 장애 조치 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82310-150">StorSimple creates a failover job.</span></span> <span data-ttu-id="82310-151">**작업** 블레이드를 통해 장애 조치(failover) 작업을 모니터링하려면 작업 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-151">Click the job notification to monitor the failover job via the **Jobs** blade.</span></span>

    <span data-ttu-id="82310-152">장애 조치된 볼륨 컨테이너에 로컬 볼륨이 있는 경우 컨테이너에서 (계층화된 볼륨이 아닌) 각 로컬 볼륨에 대한 개별 복원 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82310-152">If the volume container that you failed over has local volumes, then you see individual restore jobs for each local volume (not for tiered volumes) in the container.</span></span> <span data-ttu-id="82310-153">이러한 복원 작업을 완료하려면 상당한 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82310-153">These restore jobs may take quite some time to complete.</span></span> <span data-ttu-id="82310-154">장애 조치 작업이 이전에 완료될 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82310-154">It is likely that the failover job may complete earlier.</span></span> <span data-ttu-id="82310-155">이러한 볼륨은 복원 작업이 완료된 후에 로컬 보장을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="82310-155">These volumes will have local guarantees only after the restore jobs are complete.</span></span>

    ![장애 조치(failover) 작업 모니터링](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. <span data-ttu-id="82310-157">장애 조치를 완료한 후 **장치** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-157">After the failover is completed, go to the **Devices** blade.</span></span>
   
   1. <span data-ttu-id="82310-158">장애 조치 프로세스에 대한 대상 장치로 사용된 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-158">Select the device that was used as the target device for the failover process.</span></span>

       ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. <span data-ttu-id="82310-160">**볼륨 컨테이너** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82310-160">Go to the **Volume Containers** blade.</span></span> <span data-ttu-id="82310-161">이전 장치의 볼륨과 함께 모든 볼륨 컨테이너가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="82310-161">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       ![대상 볼륨 컨테이너 보기](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a><span data-ttu-id="82310-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82310-163">Next steps</span></span>

* <span data-ttu-id="82310-164">장애 조치(failover)를 수행한 후에 [StorSimple 장치 비활성화 또는 삭제](storsimple-8000-deactivate-and-delete-device.md)를 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82310-164">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="82310-165">StorSimple 장치 관리자 서비스를 사용하는 방법에 대한 자세한 내용을 보려면 [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md)(StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 관리)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="82310-165">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

