---
title: "장애 조치 aaaStorSimple 재해 복구 tooa StorSimple 클라우드 어플라이언스에 | Microsoft Docs"
description: "어떻게 하면 StorSimple 8000 시리즈 실제 장치 tooa 통해 toofail 클라우드 어플라이언스에 알아봅니다."
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
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="65c59-103">장애 조치 tooyour 클라우드 StorSimple 어플라이언스</span><span class="sxs-lookup"><span data-stu-id="65c59-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="65c59-104">개요</span><span class="sxs-lookup"><span data-stu-id="65c59-104">Overview</span></span>

<span data-ttu-id="65c59-105">이 자습서에서는 재해가 경우 hello 단계 필요한 toofail StorSimple 8000 시리즈 실제 장치 tooa StorSimple 클라우드 어플라이언스를 통해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="65c59-106">StorSimple에서 hello 데이터 센터 tooa 클라우드 어플라이언스에 Azure에서 실행 되는 원본 물리적 장치에서 hello 장치 장애 조치 기능 toomigrate 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="65c59-107">이 자습서의 지침에 hello tooStorSimple 8000 시리즈 실제 장치 및 3 이상 소프트웨어 업데이트 버전을 실행 하는 클라우드 어플라이언스에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="65c59-108">장치 장애 조치 및 재해를 사용 하는 toorecover는 방법에 대해 자세히 toolearn 너무 이동[StorSimple 8000 시리즈 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="65c59-109">StorSimple 물리적 장치 tooanother 물리적 장치를 통해 toofail 너무 이동[tooa StorSimple 물리적 장치용 장애 조치할](storsimple-8000-device-failover-physical-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="65c59-110">장치 tooitself 통해 toofail 너무 이동[장애 조치 toohello 동일 StorSimple 물리적 장치용](storsimple-8000-device-failover-same-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65c59-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65c59-111">Prerequisites</span></span>

- <span data-ttu-id="65c59-112">장치 장애 조치에 대 한 hello 고려 사항 검토 했음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="65c59-113">자세한 내용은 이동 너무[장치 장애 조치에 대 한 일반적인 고려 사항](storsimple-8000-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="65c59-114">이 절차를 수행하기에 앞서 StorSimple Cloud Appliance를 먼저 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="65c59-115">실행 중인 소프트웨어 버전 3을 업데이트 하거나 나중에 대 한 8020 클라우드 어플라이언스에 사용 하는 것이 좋습니다 hello DR.</span><span class="sxs-lookup"><span data-stu-id="65c59-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="65c59-116">hello 8020 모델 64TB 개이고 프리미엄 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="65c59-117">자세한 내용은 이동 너무[배포 및 StorSimple 클라우드 어플라이언스에 관리](storsimple-8000-cloud-appliance-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="65c59-118">Tooa 클라우드 어플라이언스를 통해 단계 toofail</span><span class="sxs-lookup"><span data-stu-id="65c59-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="65c59-119">Hello 단계 toorestore hello 장치 tooa 대상 StorSimple 클라우드 어플라이언스에 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="65c59-120">통해 toofail 하려는 해당 hello 볼륨 컨테이너에 연결 된 클라우드 스냅숏이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="65c59-121">자세한 내용은 이동 너무[StorSimple 장치 관리자를 사용 하 여 서비스 toocreate 백업은](storsimple-8000-manage-backup-policies-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="65c59-122">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="65c59-123">Hello에 **장치** 블레이드, 서비스와 연결 된 장치 이동 toohello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="65c59-124">![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="65c59-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="65c59-125">원본 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-125">Select and click your source device.</span></span> <span data-ttu-id="65c59-126">hello 원본 장치를 통해 toofail 하려는 hello 볼륨 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="65c59-127">너무 이동**설정 > 볼륨 컨테이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-127">Go too**Settings > Volume Containers**.</span></span>

    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="65c59-129">싶다는 의사를 toofail tooanother 장치에 대 한 볼륨 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="65c59-130">이 컨테이너 내의 볼륨 hello 볼륨 컨테이너 toodisplay hello 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="65c59-131">볼륨, 마우스 클릭 선택 **오프 라인으로 전환** tootake hello 볼륨을 오프 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="65c59-133">Hello 볼륨 컨테이너에서 모든 hello 볼륨에 대해이 프로세스를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="65c59-135">이전 단계를 반복 hello toofail tooanother 장치를 통해 하려는 모든 볼륨 컨테이너를 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="65c59-136">Toohello 돌아가서 **장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="65c59-137">Hello 명령 모음에서 클릭 **장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-137">From hello command bar, click **Fail over**.</span></span>

    ![장애 조치(failover) 클릭](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="65c59-139">Hello에 **장애 조치** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="65c59-140">**원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-140">Click **Source**.</span></span> <span data-ttu-id="65c59-141">통해 볼륨 컨테이너 toofail hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="65c59-142">**연결 된 클라우드 스냅숏이 있는 볼륨 컨테이너를 hello만 하 고 오프 라인 볼륨이 표시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="65c59-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="65c59-143">![원본 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="65c59-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="65c59-144">**대상**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-144">Click **Target**.</span></span> <span data-ttu-id="65c59-145">대상 클라우드 어플라이언스에 hello 사용 가능한 장치 드롭다운 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="65c59-146">**충분 한 용량 tooaccommodate 원본 볼륨 컨테이너에 있는 hello 장치만 hello 목록에 표시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="65c59-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![대상 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="65c59-148">장애 조치 설정을 hello 검토 **요약** hello 확인란을 선택한 볼륨 컨테이너에서 hello 볼륨이 오프 라인 인지 나타내는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![장애 조치(failover) 설정 검토](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="65c59-150">장애 조치(failover) 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-150">A failover job is created.</span></span> <span data-ttu-id="65c59-151">toomonitor hello 장애 조치 작업를 작업 알림 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![장애 조치(failover) 작업 모니터링](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="65c59-153">Hello 장애 조치가 완료 되 면 toohello 돌아가서 **장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="65c59-154">Hello 장애 조치에 대 한 hello 대상으로 사용 된 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![장치 선택](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="65c59-156">**볼륨 컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-156">Click **Volume Containers**.</span></span> <span data-ttu-id="65c59-157">Hello hello 이전 장치의 볼륨과 함께 모든 hello 볼륨 컨테이너를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="65c59-158">장애 조치 hello 볼륨 컨테이너에 볼륨 고정 된 로컬로 하는 경우 이러한 볼륨은 장애 조치 계층화 된 볼륨으로.</span><span class="sxs-lookup"><span data-stu-id="65c59-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="65c59-159">StorSimple Cloud Appliance에서는 로컬로 고정된 볼륨이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![대상 볼륨 컨테이너 보기](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="65c59-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65c59-161">Next steps</span></span>

* <span data-ttu-id="65c59-162">장애 조치를 수행한 후 해야 너무[비활성화 또는 삭제 StorSimple 장치](storsimple-8000-deactivate-and-delete-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="65c59-163">Toouse StorSimple 장치 관리자 hello 하는 방법에 대 한 정보에 대 한 서비스, 너무 이동[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65c59-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

