---
title: "장애 조치 aaaStorSimple 재해 복구 tooa StorSimple 8000 시리즈 실제 장치 | Microsoft Docs"
description: "자세한 방법을 StorSimple 8000 시리즈 실제 장치 tooanother 물리적 장치를 통해 toofail 합니다."
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
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a><span data-ttu-id="def17-103">장애 조치 tooa StorSimple 8000 시리즈 실제 장치</span><span class="sxs-lookup"><span data-stu-id="def17-103">Fail over tooa StorSimple 8000 series physical device</span></span>

## <a name="overview"></a><span data-ttu-id="def17-104">개요</span><span class="sxs-lookup"><span data-stu-id="def17-104">Overview</span></span>

<span data-ttu-id="def17-105">이 자습서에서는 재해가 경우 hello 단계 필요한 toofail StorSimple 8000 시리즈 실제 장치 tooanother StorSimple 물리적 장치를 통해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooanother StorSimple physical device if there is a disaster.</span></span> <span data-ttu-id="def17-106">StorSimple 물리적 장치를 tooanother hello 데이터 센터에서 원본 물리적 장치의 hello 장치 장애 조치 기능 toomigrate 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="def17-107">이 자습서의 지침에 hello tooStorSimple 8000 시리즈 실제 실행 하는 장치 소프트웨어 버전 업데이트 3 이상 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def17-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="def17-108">장치 장애 조치 및 재해를 사용 하는 toorecover는 방법에 대해 자세히 toolearn 너무 이동[StorSimple 8000 시리즈 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="def17-109">StorSimple 물리적 장치 tooa StorSimple 클라우드 어플라이언스를 통해 toofail 너무 이동[tooa StorSimple 클라우드 어플라이언스에 장애 조치할](storsimple-8000-device-failover-cloud-appliance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-109">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span> <span data-ttu-id="def17-110">물리적 장치 tooitself 통해 toofail 너무 이동[장애 조치 toohello 동일 StorSimple 물리적 장치용](storsimple-8000-device-failover-same-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-110">toofail over a physical device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="def17-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="def17-111">Prerequisites</span></span>

- <span data-ttu-id="def17-112">장치 장애 조치에 대 한 hello 고려 사항 검토 했음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="def17-113">자세한 내용은 이동 너무[장치 장애 조치에 대 한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="def17-114">Hello 데이터 센터에 배포 하는 StorSimple 8000 시리즈 실제 장치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-114">You must have a StorSimple 8000 series physical device deployed in hello datacenter.</span></span> <span data-ttu-id="def17-115">hello 장치 업데이트 3 또는 이후 소프트웨어 버전을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-115">hello device must run Update 3 or later software version.</span></span> <span data-ttu-id="def17-116">자세한 내용은 이동 너무[온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-116">For more information, go too[Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>


## <a name="steps-toofail-over-tooa-physical-device"></a><span data-ttu-id="def17-117">Tooa 물리적 장치를 통해 단계 toofail</span><span class="sxs-lookup"><span data-stu-id="def17-117">Steps toofail over tooa physical device</span></span>

<span data-ttu-id="def17-118">다음 단계 toorestore hello 장치 tooa 대상 물리적 장치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-118">Perform hello following steps toorestore your device tooa target physical device.</span></span>

1. <span data-ttu-id="def17-119">통해 toofail 하려는 해당 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-119">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="def17-120">자세한 내용은 이동 너무[StorSimple 장치 관리자를 사용 하 여 서비스 toocreate 백업은](storsimple-8000-manage-backup-policies-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-120">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="def17-121">StorSimple 장치 관리자 tooyour 이동한 다음 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-121">Go tooyour StorSimple Device Manager and then click **Devices**.</span></span> <span data-ttu-id="def17-122">Hello에 **장치** 블레이드, 서비스와 연결 된 장치 이동 toohello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="def17-122">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="def17-123">![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="def17-123">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span></span>
3. <span data-ttu-id="def17-124">원본 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-124">Select and click your source device.</span></span> <span data-ttu-id="def17-125">hello 원본 장치를 통해 toofail 하려는 hello 볼륨 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def17-125">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="def17-126">너무 이동**설정 > 볼륨 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-126">Go too**Settings > Volume Containers**.</span></span>
4. <span data-ttu-id="def17-127">싶다는 의사를 toofail tooanother 장치에 대 한 볼륨 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-127">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="def17-128">이 컨테이너 내의 볼륨 hello 볼륨 컨테이너 toodisplay hello 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-128">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="def17-129">볼륨, 마우스 클릭 선택 **오프 라인으로 전환** tootake hello 볼륨을 오프 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-129">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span> <span data-ttu-id="def17-130">Hello 볼륨 컨테이너에서 모든 hello 볼륨에 대해이 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-130">Repeat this process for all hello volumes in hello volume container.</span></span>
5. <span data-ttu-id="def17-131">이전 단계를 반복 hello toofail tooanother 장치를 통해 하려는 모든 볼륨 컨테이너를 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-131">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>
6. <span data-ttu-id="def17-132">Toohello 돌아가서 **장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="def17-132">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="def17-133">Hello 명령 모음에서 클릭 **장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-133">From hello command bar, click **Fail over**.</span></span>
    <span data-ttu-id="def17-134">![장애 조치(failover) 클릭](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span><span class="sxs-lookup"><span data-stu-id="def17-134">![Click fail over](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span></span>
    
7. <span data-ttu-id="def17-135">Hello에 **장애 조치** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-135">In hello **Fail over** blade, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="def17-136">**원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-136">Click **Source**.</span></span> <span data-ttu-id="def17-137">볼륨에 연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def17-137">hello volume containers with volumes associated with cloud snapshots are displayed.</span></span> <span data-ttu-id="def17-138">표시 된 hello 컨테이너에만 장애 조치에 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def17-138">Only hello containers displayed are eligible for failover.</span></span> <span data-ttu-id="def17-139">볼륨 컨테이너의 hello 목록에서 원하는 toofail 통해 hello 볼륨 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-139">In hello list of volume containers, select hello volume containers you would like toofail over.</span></span> <span data-ttu-id="def17-140">**연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너를 hello만 하 고 오프 라인 볼륨이 표시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="def17-140">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>

       ![원본 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. <span data-ttu-id="def17-142">**대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-142">Click **Target**.</span></span> <span data-ttu-id="def17-143">Hello 이전 단계에서 선택한 hello 볼륨 컨테이너에 대 한 사용 가능한 장치 hello 드롭 다운 목록에서 대상 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-143">For hello volume containers selected in hello previous step, select a target device from hello drop-down list of available devices.</span></span> <span data-ttu-id="def17-144">충분 한 용량 tooaccommodate 원본 볼륨 컨테이너에 있는 hello 장치만 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def17-144">Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.</span></span>

        ![대상 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. <span data-ttu-id="def17-146">마지막으로 아래에서 모든 hello 장애 조치 설정을 검토 **요약**합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-146">Finally, review all hello failover settings under **Summary**.</span></span> <span data-ttu-id="def17-147">Hello 설정을 검토 한 후에 hello 확인란을 선택한 볼륨 컨테이너에서 hello 볼륨이 오프 라인 인지 나타내는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-147">After you have reviewed hello settings, select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> <span data-ttu-id="def17-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-148">Click **OK**.</span></span>

       ![장애 조치(failover) 설정 검토](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. <span data-ttu-id="def17-150">StorSimple은 장애 조치 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="def17-150">StorSimple creates a failover job.</span></span> <span data-ttu-id="def17-151">Hello 알림 toomonitor hello 장애 조치 작업을 통해 hello 클릭 **작업** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="def17-151">Click hello job notification toomonitor hello failover job via hello **Jobs** blade.</span></span>

    <span data-ttu-id="def17-152">그런 다음 장애 조치 hello 볼륨 컨테이너에 볼륨이 로컬 각 로컬 볼륨 (하지 계층화 된 볼륨) hello 컨테이너에에 대 한 개별 복원 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="def17-152">If hello volume container that you failed over has local volumes, then you see individual restore jobs for each local volume (not for tiered volumes) in hello container.</span></span> <span data-ttu-id="def17-153">이러한 복원 작업 시간 toocomplete 다소 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def17-153">These restore jobs may take quite some time toocomplete.</span></span> <span data-ttu-id="def17-154">되었을 hello 장애 조치 작업 이전에 완료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def17-154">It is likely that hello failover job may complete earlier.</span></span> <span data-ttu-id="def17-155">Hello 복원 작업이 완료 된 후에 이러한 볼륨에서 로컬 보장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-155">These volumes will have local guarantees only after hello restore jobs are complete.</span></span>

    ![장애 조치(failover) 작업 모니터링](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. <span data-ttu-id="def17-157">Hello 장애 조치가 완료 된 후 이동 toohello **장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="def17-157">After hello failover is completed, go toohello **Devices** blade.</span></span>
   
   1. <span data-ttu-id="def17-158">Hello 장애 조치 프로세스에 대 한 hello 대상 장치로 사용 했던 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-158">Select hello device that was used as hello target device for hello failover process.</span></span>

       ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. <span data-ttu-id="def17-160">Toohello 이동 **볼륨 컨테이너** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="def17-160">Go toohello **Volume Containers** blade.</span></span> <span data-ttu-id="def17-161">Hello hello 이전 장치의 볼륨과 함께 모든 hello 볼륨 컨테이너를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-161">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       ![대상 볼륨 컨테이너 보기](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a><span data-ttu-id="def17-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="def17-163">Next steps</span></span>

* <span data-ttu-id="def17-164">장애 조치를 수행한 후 해야 너무[비활성화 또는 삭제 StorSimple 장치](storsimple-8000-deactivate-and-delete-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-164">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="def17-165">Toouse StorSimple 장치 관리자 hello 하는 방법에 대 한 정보에 대 한 서비스, 너무 이동[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="def17-165">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

