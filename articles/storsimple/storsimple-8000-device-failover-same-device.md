---
title: "8000 시리즈 장치에 대한 StorSimple 장애 조치(failover), 재해 복구 | Microsoft Docs"
description: "StorSimple 장치를 동일한 장치로 장애 조치(failover)하는 방법을 알아봅니다."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="3d721-103">StorSimple 물리적 장치를 동일한 장치로 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="3d721-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="3d721-104">개요</span><span class="sxs-lookup"><span data-stu-id="3d721-104">Overview</span></span>

<span data-ttu-id="3d721-105">이 자습서에서는 재해가 발생하는 경우 StorSimple 8000 시리즈 물리적 장치를 자체 장치로 장애 조치(failover)하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="3d721-106">StorSimple에서는 장치 장애 조치(failover) 기능을 사용하여 데이터 센터의 원본 물리적 장치에서 다른 물리적 장치로 데이터를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="3d721-107">이 자습서의 지침은 소프트웨어 버전 업데이트 3 이상을 실행하는 StorSimple 8000 시리즈 물리적 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="3d721-108">장치 장애 조치(failover) 및 재해 복구에 사용되는 방법에 대해 자세히 알아보려면 [StorSimple 8000 시리즈 장치에 대한 장애 조치(failover) 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="3d721-109">물리적 장치를 다른 물리적 장치로 장애 조치(failover)하려면 [동일한 StorSimple 물리적 장치로 장애 조치(failover)](storsimple-8000-device-failover-physical-device.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="3d721-110">StorSimple 물리적 장치를 StorSimple Cloud Appliance로 장애 조치(failover)하려면 [StorSimple Cloud Appliance로 장애 조치(failover)](storsimple-8000-device-failover-cloud-appliance.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3d721-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3d721-111">Prerequisites</span></span>

- <span data-ttu-id="3d721-112">장치 장애 조치(failover)에 대한 고려 사항을 검토했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="3d721-113">자세한 내용을 보려면 [장치 장애 조치(failover)에 대한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="3d721-114">동일한 장치로 장애 조치(failover)하는 단계</span><span class="sxs-lookup"><span data-stu-id="3d721-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="3d721-115">동일한 장치로 장애 조치(failover)해야 하는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="3d721-116">장치에서 모든 볼륨의 클라우드 스냅숏을 마련합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="3d721-117">자세한 내용을 보려면 [StorSimple 장치 관리자 서비스를 사용하여 백업 만들기](storsimple-8000-manage-backup-policies-u2.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="3d721-118">장치를 공장 기본값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="3d721-119">[StorSimple 장치를 공장 기본 설정으로 다시 설정하는 방법](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)의 자세한 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="3d721-120">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="3d721-121">**장치** 블레이드에서 이전 장치는 **오프라인**으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![오프라인 상태의 원본 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="3d721-123">장치를 구성하고 StorSimple 장치 관리자 서비스에 다시 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="3d721-124">새로 등록된 장치는 **Ready to set up**(설정 준비 완료)으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="3d721-125">새 장치의 장치 이름이 이전 장치와 동일하지만 장치가 공장 기본값으로 다시 설정되어 다시 등록되었음을 나타내는 숫자가 추가되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![설정 준비 완료 상태의 새로 등록된 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="3d721-127">새 장치의 경우 장치 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="3d721-128">자세한 내용을 보려면 [4단계: 최소 장치 설정 완료](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="3d721-129">**장치** 블레이드에서 장치의 상태가 **온라인**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3d721-130">**최소 구성을 먼저 완료하지 않으면 DR이 실패할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="3d721-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![온라인 상태의 새로 등록된 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="3d721-132">이전 장치(오프라인 상태)를 선택하고 명령 모음에서 **장애 조치(failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="3d721-133">**장애 조치(failover)** 블레이드에서 이전 장치를 원본으로 선택하고 대상 장치를 새로 등록된 장치로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![장애 조치(failover) 요약](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="3d721-135">자세한 지침은 [다른 실제 장치에 장애 조치](#fail-over-to-another-physical-device)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="3d721-136">**작업** 블레이드에서 모니터링할 수 있는 장치 복원 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="3d721-137">작업이 성공적으로 완료되면 새 장치에 액세스하고 **볼륨 컨테이너** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="3d721-138">이전 장치의 모든 볼륨 컨테이너가 새 장치로 마이그레이션되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![마이그레이션된 볼륨 컨테이너](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="3d721-140">장애 조치(failover)가 완료되면 포털에서 이전 장치를 비활성화하고 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="3d721-141">이전 장치(오프라인)를 선택하고 마우스 오른쪽 단추를 클릭한 다음, **비활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="3d721-142">장치가 비활성화되면 장치 상태가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![비활성화된 원본 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="3d721-144">비활성화된 장치를 선택하고 마우스 오른쪽 단추를 클릭한 다음, **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="3d721-145">이렇게 하면 장치 목록에서 장치가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-145">This deletes the device from the list of devices.</span></span>

    ![삭제된 원본 장치](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="3d721-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d721-147">Next steps</span></span>

* <span data-ttu-id="3d721-148">장애 조치(failover)를 수행한 후에 [StorSimple 장치 비활성화 또는 삭제](storsimple-8000-deactivate-and-delete-device.md)를 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d721-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="3d721-149">StorSimple 장치 관리자 서비스를 사용하는 방법에 대한 자세한 내용을 보려면 [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md)(StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 관리)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3d721-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

