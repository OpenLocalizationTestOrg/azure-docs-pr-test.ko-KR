---
title: "aaaDeactivate 및 Microsoft Azure StorSimple 가상 배열 delete | Microsoft Docs"
description: "설명 방법을 tooremove StorSimple 장치에서 서비스를 먼저 비활성화 한 후이 삭제 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="201a8-103">StorSimple 가상 배열 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="201a8-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="201a8-104">개요</span><span class="sxs-lookup"><span data-stu-id="201a8-104">Overview</span></span>

<span data-ttu-id="201a8-105">StorSimple 가상 배열을 비활성화 하면 hello 장치와 StorSimple 장치 관리자 서비스를 해당 하는 hello hello 연결도를 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="201a8-106">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="201a8-107">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="201a8-107">Deactivate a device</span></span> 
* <span data-ttu-id="201a8-108">비활성화된 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="201a8-108">Delete a deactivated device</span></span>

<span data-ttu-id="201a8-109">이 문서의 정보 hello tooStorSimple 가상 배열만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="201a8-110">8000 시리즈에 대 한 내용은 toohow을 너무 이동[비활성화 또는 장치를 삭제](storsimple-deactivate-and-delete-device.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="201a8-111">때 toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="201a8-111">When toodeactivate?</span></span>

<span data-ttu-id="201a8-112">비활성화는 영구 작업이며 실행 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="201a8-113">StorSimple 장치 관리자 서비스 hello로 비활성화 된 장치 다시 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="201a8-114">Toodeactivate 필요 하 고 hello 다음 시나리오에에서는 StorSimple 가상 배열 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="201a8-115">**계획 된 장애 조치** : 장치가 온라인 상태이 고 장치를 통해 toofail를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="201a8-116">Tooupgrade tooa 큰 장치를 계획 하는 경우 장치를 통해 toofail을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="201a8-117">Hello 데이터 소유권은 전송 hello 장애 조치가 완료 후 자동 hello 원본 장치가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="201a8-118">**계획 되지 않은 장애 조치** : 장치가 오프 라인 상태 이며 hello 장치를 통해 toofail 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="201a8-119">이 시나리오는 hello 데이터 센터에서 중단 되 고 다운 기본 장치는 재해 발생 시 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="201a8-120">Hello 장치 tooa 보조 장치를 통해 toofail를 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="201a8-121">Hello 데이터 소유권은 전송 hello 장애 조치가 완료 후 자동 hello 원본 장치가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="201a8-122">**서비스 해제** : toodecommission hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="201a8-123">이 옵션을 toofirst hello 장치를 비활성화 한 다음 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="201a8-124">장치를 비활성화하면 로컬로 저장된 데이터에 더 이상 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="201a8-125">액세스 및 복구 hello 데이터만 hello 클라우드에 저장을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="201a8-126">비활성화 후 tookeep hello 장치 데이터를 계획 하는 경우 장치를 비활성화 하기 전에 모든 데이터의 클라우드 스냅숏을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="201a8-127">이 클라우드 스냅숏을 사용 하면 toorecover 이후 단계에서 데이터를 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="201a8-128">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="201a8-128">Deactivate a device</span></span>

<span data-ttu-id="201a8-129">toodeactivate 장치 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="201a8-130">toodeactivate hello 장치</span><span class="sxs-lookup"><span data-stu-id="201a8-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="201a8-131">서비스에 이동 너무**관리 > 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="201a8-132">Hello에 **장치** 블레이드, 클릭 및 선택 hello 장치 toodeactivate 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![장치 toodeactivate 선택](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="201a8-134">사용자 **장치 대시보드** 블레이드에서 클릭 **중... 더 많은** hello 목록에서 선택 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![비활성화 클릭](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="201a8-136">Hello에 **비활성화** 블레이드, 형식 hello 장치 이름 및 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![비활성화 확인](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="201a8-138">hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![진행 중인 비활성화](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="201a8-140">비활성화 한 후 장치의 hello 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![비활성화 완료](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="201a8-142">이제 이 장치를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="201a8-143">Hello 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="201a8-143">Delete hello device</span></span>

<span data-ttu-id="201a8-144">장치에 첫 번째 비활성화 toodelete toobe 것입니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="201a8-145">장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="201a8-146">그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="201a8-147">그러나 hello 장치와 연결 된 hello 데이터 hello 클라우드 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="201a8-148">그러면 이 데이터를 사용하는 데 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-148">This data then accrues charges.</span></span>

<span data-ttu-id="201a8-149">toodelete hello 장치 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="201a8-150">toodelete hello 장치</span><span class="sxs-lookup"><span data-stu-id="201a8-150">toodelete hello device</span></span>

1. <span data-ttu-id="201a8-151">StorSimple 장치 관리자 프로그램 너무 이동**관리 > 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="201a8-152">Hello에 **장치** 블레이드에서 원하는 toodelete 비활성화 된 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="201a8-153">Hello에 **장치 대시보드** 블레이드에서 클릭 **중... 더 많은** 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![장치 toodelete 선택](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="201a8-155">Hello에 **삭제** 블레이드, 형식 hello 이름을 클릭 하 여 장치 tooconfirm hello 삭제 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="201a8-156">삭제 hello 장치 hello 장치와 연결 된 hello 클라우드 데이터를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![삭제 확인](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="201a8-158">hello 삭제 시작 되 고 몇 분 toocomplete를 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![진행 중인 삭제](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="201a8-160">Hello 장치를 삭제 한 후 장치의 hello 업데이트 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="201a8-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="201a8-161">Next steps</span></span>

* <span data-ttu-id="201a8-162">방법에 대 한 조치 toofail 너무 이동[StorSimple 가상 배열의 장애 조치 및 재해 복구](storsimple-virtual-array-failover-dr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="201a8-163">toouse hello StorSimple 장치 관리자 서비스 너무 이동 하는 방법에 대해 더 알아봅니다을 toolearn[사용 하 여 hello StorSimple 장치 관리자 서비스 tooadminister StorSimple 가상 배열](storsimple-virtual-array-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="201a8-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

