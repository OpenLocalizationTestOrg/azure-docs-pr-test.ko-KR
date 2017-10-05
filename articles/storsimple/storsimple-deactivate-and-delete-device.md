---
title: "StorSimple 장치 비활성화 및 삭제 | Microsoft Docs"
description: "먼저 StorSimple 장치를 비활성화한 후 삭제하여 서비스에서 제거하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c000a642aa088ac80cc7077453b87e9a47f96900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a><span data-ttu-id="9cc01-103">StorSimple Manager 서비스를 통해 StorSimple 8000 시리즈 장치 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="9cc01-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span></span>
## <a name="overview"></a><span data-ttu-id="9cc01-104">개요</span><span class="sxs-lookup"><span data-stu-id="9cc01-104">Overview</span></span>
<span data-ttu-id="9cc01-105">StorSimple 장치 서비스를 중단하고 싶을 수 있습니다(예: 장치를 교체 또는 업그레이드하거나 더 이상 StorSimple을 사용하지 않는 경우).</span><span class="sxs-lookup"><span data-stu-id="9cc01-105">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="9cc01-106">그런 경우 장치를 비활성화한 다음 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-106">If this is the case, you will need to deactivate the device before you can delete it.</span></span> <span data-ttu-id="9cc01-107">비활성화하면 장치 및 해당 StorSimple Manager 서비스 간의 연결이 끊깁니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-107">Deactivating severs the connection between the device and the corresponding StorSimple Manager service.</span></span> <span data-ttu-id="9cc01-108">이 자습서에서는 StorSimple 장치를 먼저 비활성화한 후 삭제하여 서비스에서 제거하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-108">This tutorial explains how to remove a StorSimple device from service by first deactivating it and then deleting it.</span></span> 

<span data-ttu-id="9cc01-109">장치를 비활성화하면 장치에 로컬로 저장된 데이터에 더 이상 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-109">When you deactivate a device, any data that was stored locally on the device will no longer be accessible.</span></span> <span data-ttu-id="9cc01-110">클라우드에 저장된 장치와 연결된 데이터만 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-110">Only the data associated with the device that was stored in the cloud can be recovered.</span></span>  

> [!WARNING]
> <span data-ttu-id="9cc01-111">비활성화는 영구 작업이며 실행 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-111">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="9cc01-112">먼저 기본 팩터리 설정에서 장치를 재설정해야 비활성화된 장치를 StorSimple Manager 서비스에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-112">A deactivated device cannot be registered with the StorSimple Manager service unless it is first reset to the default factory settings.</span></span> 
> 
> <span data-ttu-id="9cc01-113">공장 재설정 프로세스는 장치에 로컬로 저장된 모든 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-113">The factory reset process deletes all the data that was stored locally on your device.</span></span> <span data-ttu-id="9cc01-114">따라서 반드시 장치를 비장치를 비활성화하기 전에 모든 데이터의 클라우드 스냅숏을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="9cc01-115">이렇게 하면 이후 단계에서 모든 데이터를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-115">This will allow you to recover all the data at a later stage.</span></span>
> 
> 

<span data-ttu-id="9cc01-116">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-116">This tutorial explains how to:</span></span>

* <span data-ttu-id="9cc01-117">장치 비활성화 및 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="9cc01-117">Deactivate a device and delete the data</span></span>
* <span data-ttu-id="9cc01-118">장치 비활성화 및 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="9cc01-118">Deactivate a device and retain the data</span></span>

<span data-ttu-id="9cc01-119">StorSimple 가상 장치에서 비활성화 및 삭제가 어떻게 작동하는지도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc01-120">StorSimple 물리적 장치 또는 가상 장치를 비활성화하기 전에 장치에 의존하는 클라이언트와 호스트를 중지하거나 삭제했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-120">Before you deactivate a StorSimple physical or virtual device, make sure to stop or delete clients and hosts that depend on that device.</span></span>
> 
> 

## <a name="deactivate-and-delete-data"></a><span data-ttu-id="9cc01-121">데이터 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="9cc01-121">Deactivate and delete data</span></span>
<span data-ttu-id="9cc01-122">장치를 완전히 삭제하고 장치의 데이터를 보존하지 않으려는 경우 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-122">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span></span>

#### <a name="to-deactivate-the-device-and-delete-the-data"></a><span data-ttu-id="9cc01-123">장치를 비활성화하고 데이터를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="9cc01-123">To deactivate the device and delete the data</span></span>
1. <span data-ttu-id="9cc01-124">장치를 비활성화하기 전에 장치와 연결된 모든 볼륨 컨테이너(및 볼륨)를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-124">Prior to deactivating a device, you must delete all the volume containers (and the volumes) associated with the device.</span></span> <span data-ttu-id="9cc01-125">연결된 백업을 삭제한 후에만 볼륨 컨테이너를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-125">You can delete volume containers only after you have deleted the associated backups.</span></span>
2. <span data-ttu-id="9cc01-126">다음과 같이 장치를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-126">Deactivate the device as follows:</span></span>
   
   1. <span data-ttu-id="9cc01-127">StorSimple Manager 서비스 **장치** 페이지에서 비활성화할 장치를 선택하고 페이지 하단에서 **비활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-127">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="9cc01-128">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-128">A confirmation message will appear.</span></span> <span data-ttu-id="9cc01-129">**예** 를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-129">Click **Yes** to continue.</span></span> <span data-ttu-id="9cc01-130">비활성화 프로세스가 시작되고 완료하는 데 몇 분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-130">The deactivate process will start and take a few minutes to complete.</span></span>
3. <span data-ttu-id="9cc01-131">비활성화한 후 장치를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-131">After deactivation, you can delete the device completely.</span></span> <span data-ttu-id="9cc01-132">장치를 삭제하면 서비스에 연결된 장치 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-132">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="9cc01-133">그러면 서비스에서 삭제된 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-133">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="9cc01-134">장치를 삭제하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-134">Use the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="9cc01-135">StorSimple Manager 서비스 **장치** 페이지에서 삭제할 비활성화된 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-135">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="9cc01-136">페이지 맨 아래에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-136">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="9cc01-137">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-137">You will be prompted for confirmation.</span></span> <span data-ttu-id="9cc01-138">**예** 를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-138">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="9cc01-139">장치를 삭제하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-139">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="9cc01-140">데이터 비활성화 및 보존</span><span class="sxs-lookup"><span data-stu-id="9cc01-140">Deactivate and retain data</span></span>
<span data-ttu-id="9cc01-141">장치를 삭제하지만 데이터를 보존하고 싶은 경우 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-141">If you are interested in deleting the device but want to retain the data, then complete the following steps.</span></span>

#### <a name="to-deactivate-a-device-and-retain-the-data"></a><span data-ttu-id="9cc01-142">장치를 비활성화하고 데이터를 유지하려면</span><span class="sxs-lookup"><span data-stu-id="9cc01-142">To deactivate a device and retain the data</span></span>
1. <span data-ttu-id="9cc01-143">장치를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-143">Deactivate the device.</span></span> <span data-ttu-id="9cc01-144">장치의 모든 볼륨 컨테이너 및 스냅숏은 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-144">All the volume containers and the snapshots of the device will remain.</span></span>
   
   1. <span data-ttu-id="9cc01-145">StorSimple Manager 서비스 **장치** 페이지에서 비활성화할 장치를 선택하고 페이지 하단에서 **비활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-145">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="9cc01-146">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-146">A confirmation message will appear.</span></span> <span data-ttu-id="9cc01-147">**예** 를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-147">Click **Yes** to continue.</span></span> <span data-ttu-id="9cc01-148">비활성화 프로세스가 시작되고 완료하는 데 몇 분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-148">The deactivate process will start and take a few minutes to complete.</span></span>
2. <span data-ttu-id="9cc01-149">이제 볼륨 컨테이너와 연결된 스냅숏을 장애 조치(Failover)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-149">You can now fail over the volume containers and the associated snapshots.</span></span> <span data-ttu-id="9cc01-150">이에 대한 절차를 보려면 [StorSimple 장치에 대한 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc01-150">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="9cc01-151">비활성화 및 장애 조치(failover) 후 장치를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-151">After deactivation and failover, you can delete the device completely.</span></span> <span data-ttu-id="9cc01-152">장치를 삭제하면 서비스에 연결된 장치 목록에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-152">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="9cc01-153">그러면 서비스에서 삭제된 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-153">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="9cc01-154">장치를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-154">Complete the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="9cc01-155">StorSimple Manager 서비스 **장치** 페이지에서 삭제할 비활성화된 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-155">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="9cc01-156">페이지 맨 아래에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-156">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="9cc01-157">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-157">You will be prompted for confirmation.</span></span> <span data-ttu-id="9cc01-158">**예** 를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-158">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="9cc01-159">장치를 삭제하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-159">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-delete-a-virtual-device"></a><span data-ttu-id="9cc01-160">가상 장치 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="9cc01-160">Deactivate and delete a virtual device</span></span>
<span data-ttu-id="9cc01-161">StorSimple 가상 컴퓨터에 대한 비활성화는 가상 장치의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-161">For a StorSimple virtual device, deactivation deallocates the virtual machine.</span></span> <span data-ttu-id="9cc01-162">그런 다음 가상 컴퓨터가 프로비전되었을 때 만든 리소스와 가상 컴퓨터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-162">You can then delete the virtual machine and the resources created when it was provisioned.</span></span> <span data-ttu-id="9cc01-163">가상 장치가 비활성화된 후 이전 상태로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-163">After the virtual device is deactivated, it cannot be restored to its previous state.</span></span> 

<span data-ttu-id="9cc01-164">비활성화하면 다음 작업이 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-164">Deactivation results in the following actions:</span></span>

* <span data-ttu-id="9cc01-165">StorSimple 가상 장치가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-165">The StorSimple virtual device is removed.</span></span>
* <span data-ttu-id="9cc01-166">OS 디스크 및 StorSimple 가상 장치에 대해 만든 데이터 디스크가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-166">The OSDisk and Data Disks created for the StorSimple virtual device are removed.</span></span>
* <span data-ttu-id="9cc01-167">프로비전 중 호스티드 서비스 및 가상 네트워크가 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-167">The Hosted Service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="9cc01-168">이러한 엔터티를 사용하지 않는 경우 수동으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-168">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="9cc01-169">StorSimple 가상 장치에서 만든 클라우드 스냅숏은 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-169">Cloud snapshots created by the StorSimple virtual device are retained.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc01-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cc01-170">Next steps</span></span>
* <span data-ttu-id="9cc01-171">비활성화된 장치를 공장 기본 설정으로 복원하려면 [장치를 공장 기본 설정으로 초기화](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc01-171">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="9cc01-172">기술 지원을 받으려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc01-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="9cc01-173">StorSimple Manager 서비스를 사용하는 방법을 자세히 알아보려면 [StorSimple Manager 서비스를 사용하여 StorSimple 장치 관리](storsimple-manager-service-administration.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc01-173">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span> 

