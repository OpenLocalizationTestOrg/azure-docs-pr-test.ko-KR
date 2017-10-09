---
title: "aaaDeactivate StorSimple 8000 시리즈 장치를 삭제 하 고 | Microsoft Docs"
description: "설명 방법을 tooremove StorSimple 장치에서 서비스를 먼저 비활성화 한 후이 삭제 합니다."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a><span data-ttu-id="7d188-103">StorSimple 장치 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="7d188-103">Deactivate and delete a StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="7d188-104">개요</span><span class="sxs-lookup"><span data-stu-id="7d188-104">Overview</span></span>

<span data-ttu-id="7d188-105">이 문서에서는 설명 방법을 toodeactivate StorSimple 장치에 연결 된 tooa StorSimple 장치 관리자 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-105">This article describes how toodeactivate and delete a StorSimple device that is connected tooa StorSimple Device Manager service.</span></span> <span data-ttu-id="7d188-106">이 문서에 대 한 hello 지침 hello StorSimple 클라우드 어플라이언스에 포함 하 여 tooStorSimple 8000 시리즈 장치 에서만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-106">hello guidance in this article applies only tooStorSimple 8000 series devices including hello StorSimple Cloud Appliances.</span></span> <span data-ttu-id="7d188-107">StorSimple 가상 배열을 사용 하는 경우 이동 하 여 너무[비활성화 및 삭제는 StorSimple 가상 배열](storsimple-virtual-array-deactivate-and-delete-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-107">If you are using a StorSimple Virtual Array, then go too[Deactivate and delete a StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md).</span></span>

<span data-ttu-id="7d188-108">비활성화 서버 hello 장치와 StorSimple 장치 관리자 서비스를 해당 하는 hello hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-108">Deactivation severs hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="7d188-109">(예를 들어 교체 하거나 장치를 업그레이드 하는 경우 또는 StorSimple 더 이상 사용 하는 경우) 서비스에서 StorSimple 장치 tootake을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-109">You may wish tootake a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="7d188-110">이 경우 있어야만 toodeactivate hello 장치를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-110">If so, you need toodeactivate hello device before you can delete it.</span></span>

<span data-ttu-id="7d188-111">장치를 비활성화 하면 hello 장치에서 로컬로 저장 된 모든 데이터에는 더 이상 액세스할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-111">When you deactivate a device, any data that was stored locally on hello device is no longer accessible.</span></span> <span data-ttu-id="7d188-112">Hello 클라우드에 저장 된 hello 장치와 연결 된 hello 데이터만 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-112">Only hello data associated with hello device that was stored in hello cloud can be recovered.</span></span>

> [!WARNING]
> <span data-ttu-id="7d188-113">비활성화는 영구 작업이며 실행 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-113">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="7d188-114">비활성화 된 장치 toofactory 기본값 다시 설정 하지 않은 hello StorSimple 장치 관리자 서비스에 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-114">A deactivated device cannot be registered with hello StorSimple Device Manager service unless it is reset toofactory defaults.</span></span>
>
> <span data-ttu-id="7d188-115">hello 공장 기본 장치에서 로컬로 저장 된 모든 hello 데이터 프로세스 삭제를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-115">hello factory reset process deletes all hello data that was stored locally on your device.</span></span> <span data-ttu-id="7d188-116">따라서 장치를 비활성화하기 전에 모든 데이터의 클라우드 스냅숏을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-116">Therefore, you must take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="7d188-117">이 클라우드 스냅숏을 사용 하면 toorecover 이후 단계에서 데이터를 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-117">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

<span data-ttu-id="7d188-118">이 자습서를 읽은 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-118">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="7d188-119">장치 비활성화 하 고 hello 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-119">Deactivate a device and delete hello data.</span></span>
* <span data-ttu-id="7d188-120">장치 비활성화를 hello 데이터를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-120">Deactivate a device and retain hello data.</span></span>

> [!NOTE]
> <span data-ttu-id="7d188-121">StorSimple의 물리적 장치 또는 클라우드 어플라이언스를 비활성화하려면 먼저 해당 장치에 의존하는 클라이언트와 호스트를 중지하거나 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-121">Before you deactivate a StorSimple physical device or cloud appliance, stop or delete clients and hosts that depend on that device.</span></span>


## <a name="deactivate-and-delete-data"></a><span data-ttu-id="7d188-122">데이터 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="7d188-122">Deactivate and delete data</span></span>

<span data-ttu-id="7d188-123">Hello 장치를 완전히 삭제 하 고 hello 장치에 tooretain hello 데이터 하지 않을 경우 다음 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-123">If you are interested in deleting hello device completely and do not want tooretain hello data on hello device, then complete hello following steps.</span></span>

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a><span data-ttu-id="7d188-124">toodeactivate hello 장치 및 delete hello 데이터</span><span class="sxs-lookup"><span data-stu-id="7d188-124">toodeactivate hello device and delete hello data</span></span>

1. <span data-ttu-id="7d188-125">장치를 비활성화 하기 전에 모든 hello 볼륨 컨테이너 (및 hello 볼륨) hello 장치와 연결 된 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-125">Before you deactivate a device, you must delete all hello volume containers (and hello volumes) associated with hello device.</span></span> <span data-ttu-id="7d188-126">연결 된 hello 백업을 삭제 한 후에 볼륨 컨테이너를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-126">You can delete volume containers only after you have deleted hello associated backups.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d188-127">StorSimple 물리적 장치 또는 클라우드 어플라이언스에 비활성화 하기 전에 삭제 hello 볼륨 컨테이너에서 hello 데이터 hello 장치에서 실제로 삭제 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-127">Before you deactivate a StorSimple physical device or cloud appliance, ensure that hello data from hello deleted volume container is actually deleted from hello device.</span></span> <span data-ttu-id="7d188-128">Hello 클라우드 소비 차트를 모니터링할 수 있습니다 및 hello 클라우드 사용량 삭제 한 hello 백업으로 인해 삭제를 보면 toodeactivate hello 장치를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-128">You can monitor hello cloud consumption charts and when you see hello cloud usage drop because of hello backups you have deleted, then you can proceed toodeactivate hello device.</span></span> <span data-ttu-id="7d188-129">전에 hello 장치를 비활성화 하면이 놓기를 수행 hello 데이터 hello 저장소 계정에 잘못 할당 된 및 요금이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-129">If you deactivate hello device before this drop occurs, hello data is stranded in hello storage account and accrues charges.</span></span>

2. <span data-ttu-id="7d188-130">다음과 같이 hello 장치를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-130">Deactivate hello device as follows:</span></span>
   
   1. <span data-ttu-id="7d188-131">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-131">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="7d188-132">Hello에 **장치** 블레이드, toodeactivate 마우스 오른쪽 단추를 클릭 한 다음 원하는 선택 hello 장치 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-132">In hello **Devices** blade, select hello device that you wish toodeactivate, right-click, and then click **Deactivate**.</span></span>

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="7d188-134">Hello에 **비활성화** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-134">In hello **Deactivate** blade, type hello device name tooconfirm and then click **Deactivate**.</span></span> <span data-ttu-id="7d188-135">hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-135">hello deactivate process starts and takes a few minutes toocomplete.</span></span>

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. <span data-ttu-id="7d188-137">비활성화 한 후 hello 장치를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-137">After deactivation, you can delete hello device completely.</span></span> <span data-ttu-id="7d188-138">장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-138">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="7d188-139">그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-139">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="7d188-140">다음 단계 toodelete hello 장치 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-140">Use hello following steps toodelete hello device:</span></span>
   
   1. <span data-ttu-id="7d188-141">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-141">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="7d188-142">Hello에 **장치** 블레이드, toodelete 마우스 오른쪽 단추를 클릭 한 다음 원하는 비활성화 선택 hello 장치 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-142">In hello **Devices** blade, select hello deactivated device that you wish toodelete, right-click, and then click **Delete**.</span></span>

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="7d188-144">Hello에 **삭제** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-144">In hello **Delete** blade, type hello device name tooconfirm and then click **Delete**.</span></span> <span data-ttu-id="7d188-145">hello 삭제는 몇 분 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-145">hello deletion takes a few minutes toocomplete.</span></span>

        ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="7d188-147">Hello 삭제 성공적으로 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-147">After hello deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="7d188-148">hello 장치 목록도 tooreflect hello 삭제를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-148">hello device list also updates tooreflect hello deletion.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="7d188-149">데이터 비활성화 및 보존</span><span class="sxs-lookup"><span data-stu-id="7d188-149">Deactivate and retain data</span></span>

<span data-ttu-id="7d188-150">관심 있는 hello 장치를 삭제 해도 tooretain hello 데이터를 원하는 경우 다음 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-150">If you are interested in deleting hello device but want tooretain hello data, then complete hello following steps:</span></span>

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a><span data-ttu-id="7d188-151">장치 toodeactivate hello 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-151">toodeactivate a device and retain hello data</span></span>
1. <span data-ttu-id="7d188-152">Hello 장치를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-152">Deactivate hello device.</span></span> <span data-ttu-id="7d188-153">모든 볼륨 컨테이너를 hello 및 hello 장치의 hello 스냅숏은 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-153">All hello volume containers and hello snapshots of hello device remain.</span></span>
   
   1. <span data-ttu-id="7d188-154">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-154">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="7d188-155">Hello에 **장치** 블레이드, toodeactivate 마우스 오른쪽 단추를 클릭 한 다음 원하는 선택 hello 장치 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-155">In hello **Devices** blade, select hello device that you wish toodeactivate, right-click, and then click **Deactivate**.</span></span>

         ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="7d188-157">Hello에 **비활성화** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-157">In hello **Deactivate** blade, type hello device name tooconfirm and then click **Deactivate**.</span></span> <span data-ttu-id="7d188-158">hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-158">hello deactivate process starts and takes a few minutes toocomplete.</span></span>

         ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. <span data-ttu-id="7d188-160">이제 hello 볼륨 컨테이너와 연결 된 hello 스냅숏을 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-160">You can now fail over hello volume containers and hello associated snapshots.</span></span> <span data-ttu-id="7d188-161">너무 절차를 보려면[StorSimple 장치에 대 한 장애 조치 및 재해 복구](storsimple-8000-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-161">For procedures, go too[Failover and disaster recovery for your StorSimple device](storsimple-8000-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="7d188-162">비활성화 및 장애 조치 후 hello 장치를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-162">After deactivation and failover, you can delete hello device completely.</span></span> <span data-ttu-id="7d188-163">장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-163">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="7d188-164">그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-164">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="7d188-165">다음 단계 완료 hello toodelete hello 장치:</span><span class="sxs-lookup"><span data-stu-id="7d188-165">toodelete hello device, complete hello following steps:</span></span>
   
   1. <span data-ttu-id="7d188-166">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-166">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="7d188-167">Hello에 **장치** 블레이드, toodelete 마우스 오른쪽 단추를 클릭 한 다음 원하는 비활성화 선택 hello 장치 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-167">In hello **Devices** blade, select hello deactivated device that you wish toodelete, right-click, and then click **Delete**.</span></span>

       ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="7d188-169">Hello에 **삭제** 블레이드에서 hello 장치 이름 tooconfirm를 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-169">In hello **Delete** blade, type hello device name tooconfirm and then click **Delete**.</span></span> <span data-ttu-id="7d188-170">hello 삭제는 몇 분 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-170">hello deletion takes a few minutes toocomplete.</span></span>

       ![StorSimple 장치 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="7d188-172">Hello 삭제 성공적으로 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-172">After hello deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="7d188-173">hello 장치 목록도 tooreflect hello 삭제를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-173">hello device list also updates tooreflect hello deletion.</span></span>

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a><span data-ttu-id="7d188-174">클라우드 어플라이언스 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="7d188-174">Deactivate and delete a cloud appliance</span></span>

<span data-ttu-id="7d188-175">StorSimple 클라우드 장비에 대 한 hello 포털에서 비활성화 할당을 취소 하 고 hello 가상 컴퓨터 및 프로 비전 된 경우 생성 된 hello 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-175">For a StorSimple Cloud Appliance, deactivation from hello portal deallocates and deletes hello virtual machine, and hello resources created when it was provisioned.</span></span> <span data-ttu-id="7d188-176">일 수 없습니다 hello 클라우드 어플라이언스에 비활성화 된 후 tooits 이전 상태로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-176">After hello cloud appliance is deactivated, it cannot be restored tooits previous state.</span></span>

![StorSimple Cloud Appliance 비활성화](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

<span data-ttu-id="7d188-178">작업을 수행 하는 hello에 비활성화 결과:</span><span class="sxs-lookup"><span data-stu-id="7d188-178">Deactivation results in hello following actions:</span></span>

* <span data-ttu-id="7d188-179">StorSimple 클라우드 어플라이언스에 hello hello 서비스에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-179">hello StorSimple Cloud Appliance is removed from hello service.</span></span>
* <span data-ttu-id="7d188-180">StorSimple 클라우드 어플라이언스에 hello에 대 한 hello 가상 컴퓨터가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-180">hello virtual machine for hello StorSimple Cloud Appliance is deleted.</span></span>
* <span data-ttu-id="7d188-181">hello OS 디스크 및 StorSimple 클라우드 어플라이언스에 hello에 대 한 만든 데이터 디스크 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-181">hello OS disk and data disks created for hello StorSimple Cloud Appliance are removed.</span></span>
* <span data-ttu-id="7d188-182">hello 호스팅된 서비스 및 가상 네트워크를 프로 비전 중에 만들어진 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-182">hello hosted service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="7d188-183">이러한 엔터티를 사용하지 않는 경우 수동으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-183">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="7d188-184">StorSimple 클라우드 어플라이언스에 hello에서 만든 클라우드 스냅숏은 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-184">Cloud snapshots created by hello StorSimple Cloud Appliance are retained.</span></span>

<span data-ttu-id="7d188-185">Hello 클라우드 어플라이언스에 비활성화 된 후에 hello 장치 목록에서 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-185">After hello cloud appliance is deactivated, you can delete it from hello list of devices.</span></span> <span data-ttu-id="7d188-186">장치, 마우스 클릭 한 다음 선택 hello 비활성화 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-186">Select hello deactivated device, right-click, and then click **Delete**.</span></span> <span data-ttu-id="7d188-187">StorSimple는 hello 장치를 삭제 하 고 장치 업데이트 목록이 hello 되 면이 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-187">StorSimple notifies you once hello device is deleted and hello list of devices updates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d188-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d188-188">Next steps</span></span>

* <span data-ttu-id="7d188-189">toorestore 비활성화 된 장치 toofactory 기본값 hello, 너무 이동[hello 장치 toofactory 기본 설정으로 초기화](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-189">toorestore hello deactivated device toofactory defaults, go too[Reset hello device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="7d188-190">기술 지원을 받으려면 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="7d188-190">For technical assistance, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="7d188-191">toouse hello StorSimple 장치 관리자 서비스 너무 이동 하는 방법에 대해 더 알아봅니다을 toolearn[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d188-191">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

