---
title: "Microsoft Azure StorSimple 가상 배열 비활성화 및 삭제 | Microsoft Docs"
description: "먼저 StorSimple 장치를 비활성화한 후 삭제하여 서비스에서 제거하는 방법을 설명합니다."
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
ms.openlocfilehash: 8dea36f92b034f8c6cdb6875634848d37f4c6606
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="cbc63-103">StorSimple 가상 배열 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="cbc63-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cbc63-104">개요</span><span class="sxs-lookup"><span data-stu-id="cbc63-104">Overview</span></span>

<span data-ttu-id="cbc63-105">StorSimple 가상 배열을 비활성화하면 장치 및 해당 StorSimple 장치 관리자 서비스 간의 연결이 끊깁니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-105">When you deactivate a StorSimple Virtual Array, you break the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="cbc63-106">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="cbc63-107">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="cbc63-107">Deactivate a device</span></span> 
* <span data-ttu-id="cbc63-108">비활성화된 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="cbc63-108">Delete a deactivated device</span></span>

<span data-ttu-id="cbc63-109">이 문서의 정보는 StorSimple 가상 배열에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-109">The information in this article applies to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="cbc63-110">8000 시리즈에 대한 내용은 [장치를 비활성화 또는 삭제](storsimple-deactivate-and-delete-device.md)하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc63-110">For information on 8000 series, go to how to [deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-to-deactivate"></a><span data-ttu-id="cbc63-111">비활성화하는 경우</span><span class="sxs-lookup"><span data-stu-id="cbc63-111">When to deactivate?</span></span>

<span data-ttu-id="cbc63-112">비활성화는 영구 작업이며 실행 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="cbc63-113">비활성화된 장치를 StorSimple 장치 관리자 서비스에 다시 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-113">You cannot register a deactivated device with the StorSimple Device Manager service again.</span></span> <span data-ttu-id="cbc63-114">다음과 같은 시나리오에서 StorSimple 가상 배열을 비활성화하고 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-114">You may need to deactivate and delete a StorSimple Virtual Array in the following scenarios:</span></span>

* <span data-ttu-id="cbc63-115">**계획된 장애조치**: 장치가 온라인 상태이고 이 장치를 장애 조치할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-115">**Planned failover** : Your device is online and you plan to fail over your device.</span></span> <span data-ttu-id="cbc63-116">더 큰 장치로 업그레이드하려는 경우 장치를 장애 조치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-116">If you are planning to upgrade to a larger device, you may need to fail over your device.</span></span> <span data-ttu-id="cbc63-117">데이터 소유권을 이전하고 장애 조치가 완료된 후에 원본 장치는 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-117">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="cbc63-118">**계획되지 않은 장애조치**: 장치가 오프라인 상태이고 이 장치를 장애 조치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-118">**Unplanned failover** : Your device is offline and you need to fail over the device.</span></span> <span data-ttu-id="cbc63-119">이 시나리오는 데이터 센터에서 중단이 발생하고 기본 장치가 중단되는 재해 발생 시 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-119">This scenario may occur during a disaster when there is an outage in the datacenter and your primary device is down.</span></span> <span data-ttu-id="cbc63-120">장치를 보조 장치로 장애 조치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-120">You plan to fail over the device to a secondary device.</span></span> <span data-ttu-id="cbc63-121">데이터 소유권을 이전하고 장애 조치가 완료된 후에 원본 장치는 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-121">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="cbc63-122">**서비스 해제**: 장치 서비스를 해제하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-122">**Decommission** : You want to decommission the device.</span></span> <span data-ttu-id="cbc63-123">이를 위해서는 먼저 장치를 비활성화한 다음 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-123">This requires you to first deactivate the device and then delete it.</span></span> <span data-ttu-id="cbc63-124">장치를 비활성화하면 로컬로 저장된 데이터에 더 이상 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="cbc63-125">클라우드에 저장된 데이터에 액세스하고 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-125">You can only access and recover the data stored in the cloud.</span></span> <span data-ttu-id="cbc63-126">비활성화 후 장치 데이터를 유지하려는 경우 장치를 비활성화하기 전에 모든 데이터의 클라우드 스냅숏을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-126">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="cbc63-127">이 클라우드 스냅숏을 사용하면 이후 단계에서 모든 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-127">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="cbc63-128">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="cbc63-128">Deactivate a device</span></span>

<span data-ttu-id="cbc63-129">장치를 비활성화하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-129">To deactivate your device, perform the following steps.</span></span>

#### <a name="to-deactivate-the-device"></a><span data-ttu-id="cbc63-130">장치를 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="cbc63-130">To deactivate the device</span></span>

1. <span data-ttu-id="cbc63-131">서비스에서 **관리 > 장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-131">In your service, go to **Management > Devices**.</span></span> <span data-ttu-id="cbc63-132">**장치** 블레이드에서 비활성화하려는 장치를 클릭하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-132">In the **Devices** blade, click and select the device that you wish to deactivate.</span></span>
   
    ![비활성화할 장치 선택](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="cbc63-134">**장치 대시보드** 블레이드의 목록에서 **... 추가**를 클릭하고 **비활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-134">In your **Device dashboard** blade, click **… More** and from the list, select **Deactivate**.</span></span>
   
    ![비활성화 클릭](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="cbc63-136">**비활성화** 블레이드에서 장치 이름을 입력한 다음 **비활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-136">In the **Deactivate** blade, type the device name and then click **Deactivate**.</span></span> 
   
    ![비활성화 확인](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="cbc63-138">비활성화 프로세스가 시작되고 완료하는 데 몇 분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-138">The deactivate process starts and takes a few minutes to complete.</span></span>
   
    ![진행 중인 비활성화](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="cbc63-140">비활성화한 후에 장치 목록이 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-140">After deactivation, the list of devices refreshes.</span></span>
   
    ![비활성화 완료](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="cbc63-142">이제 이 장치를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-142">You can now delete this device.</span></span>

## <a name="delete-the-device"></a><span data-ttu-id="cbc63-143">장치 삭제</span><span class="sxs-lookup"><span data-stu-id="cbc63-143">Delete the device</span></span>

<span data-ttu-id="cbc63-144">삭제하려면 먼저 장치를 비활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-144">A device has to be first deactivated to delete it.</span></span> <span data-ttu-id="cbc63-145">장치를 삭제하면 서비스에 연결된 장치 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-145">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="cbc63-146">그러면 서비스에서 삭제된 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-146">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="cbc63-147">그러나 장치와 연결된 데이터는 클라우드에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-147">The data associated with the device however remains in the cloud.</span></span> <span data-ttu-id="cbc63-148">그러면 이 데이터를 사용하는 데 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-148">This data then accrues charges.</span></span>

<span data-ttu-id="cbc63-149">장치를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-149">To delete the device, perform the following steps.</span></span>

#### <a name="to-delete-the-device"></a><span data-ttu-id="cbc63-150">장치를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="cbc63-150">To delete the device</span></span>

1. <span data-ttu-id="cbc63-151">StorSimple 장치 관리자에서 **관리 > 장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-151">In your StorSimple Device Manager, go to **Management > Devices**.</span></span> <span data-ttu-id="cbc63-152">**장치** 블레이드에서 삭제하려는 비활성화된 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-152">In the **Devices** blade, select a deactivated device that you wish to delete.</span></span>
2. <span data-ttu-id="cbc63-153">**장치 대시보드** 블레이드에서 **...추가**를 클릭한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-153">In the **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![삭제할 장치 선택](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="cbc63-155">**삭제** 블레이드에서 삭제를 확인하는 장치의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-155">In the **Delete** blade, type the name of your device to confirm the deletion and then click **Delete**.</span></span> <span data-ttu-id="cbc63-156">장치를 삭제하더라도 장치와 연결된 클라우드 데이터를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-156">Deleting the device does not delete the cloud data associated with the device.</span></span> 
   
   ![삭제 확인](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="cbc63-158">삭제 작업이 시작되고 완료하는 데 몇 분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-158">The deletion starts and takes a few minutes to complete.</span></span>
   
   ![진행 중인 삭제](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="cbc63-160">장치를 삭제한 후에 업데이트된 장치 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-160">After the device is deleted, you can view the updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbc63-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cbc63-161">Next steps</span></span>

* <span data-ttu-id="cbc63-162">장애 조치 방법에 대한 정보는 [StorSimple 가상 배열 장애 조치 및 재해 복구](storsimple-virtual-array-failover-dr.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cbc63-162">For information on how to fail over, go to [Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="cbc63-163">StorSimple 장치 관리자 서비스를 사용하는 방법을 자세히 알아보려면 [StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열 관리](storsimple-virtual-array-manager-service-administration.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="cbc63-163">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

