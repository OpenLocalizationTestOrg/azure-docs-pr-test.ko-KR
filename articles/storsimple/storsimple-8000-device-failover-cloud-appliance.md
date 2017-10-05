---
title: "StorSimple Cloud Appliance로 StorSimple 장애 조치(failover), 재해 복구 | Microsoft Docs"
description: "클라우드 어플라이언스로 StorSimple 8000 시리즈 물리적 장치를 장애 조치(failover)하는 방법에 대해 알아봅니다."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="57a6d-103">StorSimple Cloud Appliance로 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="57a6d-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="57a6d-104">개요</span><span class="sxs-lookup"><span data-stu-id="57a6d-104">Overview</span></span>

<span data-ttu-id="57a6d-105">이 자습서에서는 재해가 발생하는 경우 StorSimple 8000 시리즈 물리적 장치를 StorSimple Cloud Appliance로 장애 조치(failover)하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="57a6d-106">StorSimple에서는 장치 장애 조치(failover) 기능을 사용하여 데이터 센터의 원본 물리적 장치로부터 Azure에서 실행 중인 클라우드 어플라이언스로 데이터를 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="57a6d-107">이 자습서의 지침은 StorSimple 8000 시리즈 물리적 장치 및 소프트웨어 버전 업데이트 3 이상을 실행하는 클라우드 어플라이언스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="57a6d-108">장치 장애 조치(failover) 및 재해 복구에 사용되는 방법에 대해 자세히 알아보려면 [StorSimple 8000 시리즈 장치에 대한 장애 조치(failover) 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="57a6d-109">StorSimple 물리적 장치를 다른 물리적 장치로 장애 조치(failover)하려면 [StorSimple 물리적 장치로 장애 조치(failover)](storsimple-8000-device-failover-physical-device.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="57a6d-110">장치를 자체 장치로 장애 조치(failover)하려면 [동일한 StorSimple 물리적 장치로 장애 조치(failover)](storsimple-8000-device-failover-same-device.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57a6d-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="57a6d-111">Prerequisites</span></span>

- <span data-ttu-id="57a6d-112">장치 장애 조치(failover)에 대한 고려 사항을 검토했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="57a6d-113">자세한 내용을 보려면 [장치 장애 조치(failover)에 대한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="57a6d-114">이 절차를 수행하기에 앞서 StorSimple Cloud Appliance를 먼저 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="57a6d-115">업데이트 3 이상의 소프트웨어 버전을 실행하고 있는 경우 DR에 8020 클라우드 어플라이언스 사용을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="57a6d-116">8020 모델은 64TB이며 Premium Storage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="57a6d-117">자세한 내용을 보려면 [StorSimple Cloud Appliance 배포 및 관리](storsimple-8000-cloud-appliance-u2.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="57a6d-118">클라우드 어플라이언스로 장애 조치(failover)하는 단계</span><span class="sxs-lookup"><span data-stu-id="57a6d-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="57a6d-119">대상 StorSimple Cloud Appliance에 장치를 복원하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="57a6d-120">장애 조치하려는 볼륨 컨테이너에 연결된 클라우드 스냅숏이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="57a6d-121">자세한 내용을 보려면 [StorSimple 장치 관리자 서비스를 사용하여 백업 만들기](storsimple-8000-manage-backup-policies-u2.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="57a6d-122">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="57a6d-123">**장치** 블레이드에서 서비스와 연결된 장치 목록으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="57a6d-124">![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="57a6d-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="57a6d-125">원본 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-125">Select and click your source device.</span></span> <span data-ttu-id="57a6d-126">원본 장치에는 장애 조치(failover)하려는 볼륨 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="57a6d-127">**설정 > 볼륨 컨테이너**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-127">Go to **Settings > Volume Containers**.</span></span>

    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="57a6d-129">다른 장치에 장애 조치하려는 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="57a6d-130">볼륨 컨테이너를 클릭하여 이 컨테이너 내에 볼륨의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="57a6d-131">볼륨을 선택하고 마우스 오른쪽 단추를 클릭한 다음, **오프라인으로 전환**을 클릭하여 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="57a6d-133">볼륨 컨테이너의 모든 볼륨에 이 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="57a6d-135">다른 장치에 장애 조치하려는 모든 볼륨 컨테이너에 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="57a6d-136">**장치** 블레이드로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="57a6d-137">명령 모음에서 **장애 조치(failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-137">From the command bar, click **Fail over**.</span></span>

    ![장애 조치(failover) 클릭](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="57a6d-139">**장애 조치(failover)** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="57a6d-140">**원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-140">Click **Source**.</span></span> <span data-ttu-id="57a6d-141">장애 조치(failover)할 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="57a6d-142">**클라우드 스냅숏과 연결된 볼륨 컨테이너와 오프라인 볼륨만 표시됩니다.**</span><span class="sxs-lookup"><span data-stu-id="57a6d-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="57a6d-143">![원본 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="57a6d-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="57a6d-144">**대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-144">Click **Target**.</span></span> <span data-ttu-id="57a6d-145">사용 가능한 장치 드롭다운 목록에서 대상 클라우드 어플라이언스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="57a6d-146">**원본 볼륨 컨테이너를 수용할 용량이 충분한 장치만 목록에 표시됩니다.**</span><span class="sxs-lookup"><span data-stu-id="57a6d-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![대상 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="57a6d-148">**요약**에서 장애 조치(failover) 설정을 검토하고 선택한 볼륨 컨테이너의 볼륨이 오프라인 상태임을 나타내는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![장애 조치(failover) 설정 검토](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="57a6d-150">장애 조치(failover) 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-150">A failover job is created.</span></span> <span data-ttu-id="57a6d-151">장애 조치(failover) 작업을 모니터링하려면 작업 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-151">To monitor the failover job, click the job notification.</span></span>

    ![장애 조치(failover) 작업 모니터링](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="57a6d-153">장애 조치(failover)를 완료한 후 **장치** 블레이드로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="57a6d-154">장애 조치(failover) 대상으로 사용된 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-154">Select the device that was used as the target for the failover.</span></span>

       ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="57a6d-156">**볼륨 컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-156">Click **Volume Containers**.</span></span> <span data-ttu-id="57a6d-157">이전 장치의 볼륨과 함께 모든 볼륨 컨테이너가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="57a6d-158">장애 조치(failover)한 볼륨 컨테이너에 로컬로 고정된 볼륨이 있는 경우 이러한 볼륨은 계층화된 볼륨으로 장애 조치(failover)됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="57a6d-159">StorSimple Cloud Appliance에서는 로컬로 고정된 볼륨이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![대상 볼륨 컨테이너 보기](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="57a6d-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57a6d-161">Next steps</span></span>

* <span data-ttu-id="57a6d-162">장애 조치(failover)를 수행한 후에 [StorSimple 장치 비활성화 또는 삭제](storsimple-8000-deactivate-and-delete-device.md)를 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a6d-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="57a6d-163">StorSimple 장치 관리자 서비스를 사용하는 방법에 대한 자세한 내용을 보려면 [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md)(StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 관리)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="57a6d-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

