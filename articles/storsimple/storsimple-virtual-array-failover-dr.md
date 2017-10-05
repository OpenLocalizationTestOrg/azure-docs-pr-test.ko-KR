---
title: "StorSimple Virtual Array 재해 복구 및 장치 장애 조치 | Microsoft Docs"
description: "StorSimple 가상 배열 장애 조치 방법에 대해 자세히 알아봅니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12079f8dbc409afe5acc274fa08bda878c90b76e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a><span data-ttu-id="6d6aa-103">Azure Portal을 통해 StorSimple 가상 배열에 대한 재해 복구 및 장치 장애 조치</span><span class="sxs-lookup"><span data-stu-id="6d6aa-103">Disaster recovery and device failover for your StorSimple Virtual Array via Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="6d6aa-104">개요</span><span class="sxs-lookup"><span data-stu-id="6d6aa-104">Overview</span></span>
<span data-ttu-id="6d6aa-105">이 문서에서는 다른 가상 배열에 장애 조치하는 자세한 단계를 포함하여 Microsoft Azure StorSimple 가상 배열에 대한 재해 복구를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-105">This article describes the disaster recovery for your Microsoft Azure StorSimple Virtual Array including the detailed steps to fail over to another virtual array.</span></span> <span data-ttu-id="6d6aa-106">장애 조치를 사용하면 데이터를 데이터 센터의 *원본* 장치에서 *대상* 장치로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-106">A failover allows you to move your data from a *source* device in the datacenter to a *target* device.</span></span> <span data-ttu-id="6d6aa-107">대상 장치는 동일하거나 다른 지리적 위치에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-107">The target device may be located in the same or a different geographical location.</span></span> <span data-ttu-id="6d6aa-108">장치 장애 조치는 전체 장치를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-108">The device failover is for the entire device.</span></span> <span data-ttu-id="6d6aa-109">장애 조치를 수행하는 동안 원본 장치의 클라우드 데이터는 대상 장치의 그것으로 소유권이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-109">During failover, the cloud data for the source device changes ownership to that of the target device.</span></span>

<span data-ttu-id="6d6aa-110">이 문서는 StorSimple 가상 배열에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-110">This article is applicable to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="6d6aa-111">8000 시리즈 장치에 장애 조치를 하려면 [StorSimple 장치에 대한 장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-111">To fail over an 8000 series device, go to [Device failover and disaster recovery of your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>

## <a name="what-is-disaster-recovery-and-device-failover"></a><span data-ttu-id="6d6aa-112">재해 복구 및 장치 장애 조치(Failover)란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6d6aa-112">What is disaster recovery and device failover?</span></span>

<span data-ttu-id="6d6aa-113">DR(재해 복구) 시나리오에서 기본 장치가 작동을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-113">In a disaster recovery (DR) scenario, the primary device stops functioning.</span></span> <span data-ttu-id="6d6aa-114">이 시나리오에서는 실패한 장치와 연결된 클라우드 데이터를 다른 장치로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-114">In this scenario, you can move the cloud data associated with the failed device to another device.</span></span> <span data-ttu-id="6d6aa-115">기본 장치를 *원본*으로 사용하고 다른 장치를 *대상*으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-115">You can use the primary device as the *source* and specify another device as the *target*.</span></span> <span data-ttu-id="6d6aa-116">이 프로세스는 *장애 조치*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-116">This process is referred to as the *failover*.</span></span> <span data-ttu-id="6d6aa-117">장애 조지 중에는 원본 장치의 모든 볼륨 또는 공유가 소유권을 변경하고 대상 장치로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-117">During failover, all the volumes or the shares from the source device change ownership and are transferred to the target device.</span></span> <span data-ttu-id="6d6aa-118">데이터에 대한 필터링은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-118">No filtering of the data is allowed.</span></span>

<span data-ttu-id="6d6aa-119">DR은 열 지도 기반 계층화 및 추적을 사용하여 전체 장치 복원으로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-119">DR is modeled as a full device restore using the heat map–based tiering and tracking.</span></span> <span data-ttu-id="6d6aa-120">열 지도는 읽기 및 쓰기 패턴을 기반으로 데이터에 열 값을 할당하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-120">A heat map is defined by assigning a heat value to the data based on read and write patterns.</span></span> <span data-ttu-id="6d6aa-121">이 열 지도는 높은 열(가장 많이 사용되는) 데이터 청크는 로컬 계층에 유지하면서, 최저 열 데이터 청크를 클라우드에 우선 계층화합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-121">This heat map then tiers the lowest heat data chunks to the cloud first while keeping the high heat (most used) data chunks in the local tier.</span></span> <span data-ttu-id="6d6aa-122">DR 중에 StorSimple은 클라우드로부터 데이터를 복원하고 리하이드레이션하는 데 열 지도를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-122">During a DR, StorSimple uses the heat map to restore and rehydrate the data from the cloud.</span></span> <span data-ttu-id="6d6aa-123">장치는 최신의 마지막 백업(내부적으로 확인된)에서 모든 볼륨/공유를 가져와서 해당 백업으로부터 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-123">The device fetches all the volumes/shares in the last recent backup (as determined internally) and performs a restore from that backup.</span></span> <span data-ttu-id="6d6aa-124">가상 배열은 전체 DR 프로세스를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-124">The virtual array orchestrates the entire DR process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d6aa-125">원본 장치가 장치 장애 조치 후에 삭제되고 따라서 장애 복구가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-125">The source device is deleted at the end of device failover and hence a failback is not supported.</span></span>
> 
> 

<span data-ttu-id="6d6aa-126">재해 복구는 장치 장애 조치 기능을 통해 조정되며 **장치** 블레이드에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-126">Disaster recovery is orchestrated via the device failover feature and is initiated from the **Devices** blade.</span></span> <span data-ttu-id="6d6aa-127">이 블레이드는 StorSimple 장치 관리자 서비스에 연결된 모든 StorSimple 장치를 표로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-127">This blade tabulates all the StorSimple devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6d6aa-128">각 장치에 대해 친숙한 이름, 상태, 프로비전된 용량 및 최대 용량, 유형 및 모델이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-128">For each device, you can see the friendly name, status, provisioned and maximum capacity, type, and model.</span></span>

## <a name="prerequisites-for-device-failover"></a><span data-ttu-id="6d6aa-129">장치 장애 조치에 대한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d6aa-129">Prerequisites for device failover</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6d6aa-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d6aa-130">Prerequisites</span></span>

<span data-ttu-id="6d6aa-131">모든 장치 장애 조치에 대해 다음과 같은 필수 조건을 충족했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-131">For a device failover, ensure that the following prerequisites are satisfied:</span></span>

* <span data-ttu-id="6d6aa-132">원본 장치는 **비활성화됨** 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-132">The source device needs to be in a **Deactivated** state.</span></span>
* <span data-ttu-id="6d6aa-133">대상 장치는 Azure Portal에 **설정할 준비 완료**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-133">The target device needs to show up as **Ready to set up** in the Azure portal.</span></span> <span data-ttu-id="6d6aa-134">용량이 동일하거나 더 높은 대상 가상 배열을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-134">Provision a target virtual array of the same or higher capacity.</span></span> <span data-ttu-id="6d6aa-135">그 후 로컬 웹 UI를 사용하여 대상 가상 배열을 구성하고 등록을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-135">Use the local web UI to configure and successfully register the target virtual array.</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="6d6aa-136">서비스를 통해 등록된 가상 장치를 구성하려고 시도하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-136">Do not attempt to configure the registered virtual device through the service.</span></span> <span data-ttu-id="6d6aa-137">이 서비스를 통해 장치 구성을 수행하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-137">No device configuration should be performed through the service.</span></span>
  > 
  > 
* <span data-ttu-id="6d6aa-138">대상 장치는 원본 장치와 동일한 이름을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-138">The target device cannot have the same name as the source device.</span></span>
* <span data-ttu-id="6d6aa-139">원본 및 대상 장치는 같은 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-139">The source and target device have to be the same type.</span></span> <span data-ttu-id="6d6aa-140">파일 서버로 구성된 가장 배열에서는 또 다른 파일 서버로만 장애 조치를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-140">You can only fail over a virtual array configured as a file server to another file server.</span></span> <span data-ttu-id="6d6aa-141">iSCSI 서버에도 같은 내용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-141">The same is true for an iSCSI server.</span></span>
* <span data-ttu-id="6d6aa-142">파일 서버 DR의 경우 대상 장치를 원본과 동일한 도메인에 조인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-142">For a file server DR, we recommend that you join the target device to the same domain as the source.</span></span> <span data-ttu-id="6d6aa-143">이 구성을 통해 공유 사용 권한을 자동으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-143">This configuration ensures that the share permissions are automatically resolved.</span></span> <span data-ttu-id="6d6aa-144">같은 도메인에 있는 대상 장치에 대한 장애 조치만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-144">Only the failover to a target device in the same domain.</span></span>
* <span data-ttu-id="6d6aa-145">DR에 사용할 수 있는 대상 장치는 원본 장치와 용량이 같거나 더 큰 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-145">The available target devices for DR are devices that have the same or larger capacity compared to the source device.</span></span> <span data-ttu-id="6d6aa-146">서비스에 연결되어 있지만 충분한 공간 조건을 충족하지 않는 장치는 대상 장치로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-146">The devices that are connected to your service but do not meet the criteria of sufficient space are not available as target devices.</span></span>

### <a name="other-considerations"></a><span data-ttu-id="6d6aa-147">기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6d6aa-147">Other considerations</span></span>

* <span data-ttu-id="6d6aa-148">계획된 장애 조치(Failover)의 경우</span><span class="sxs-lookup"><span data-stu-id="6d6aa-148">For a planned failover</span></span> 
  
  * <span data-ttu-id="6d6aa-149">원본 장치의 모든 볼륨 또는 공유를 오프라인으로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-149">We recommend that you take all the volumes or shares on the source device offline.</span></span>
  * <span data-ttu-id="6d6aa-150">데이터 손실을 최소화하기 위해 장치의 백업을 수행한 후에 장애 조치를 진행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-150">We recommend that you take a backup of the device and then proceed with the failover to minimize data loss.</span></span> 
* <span data-ttu-id="6d6aa-151">계획되지 않은 장애 조치의 경우 장치에서는 가장 최근 백업을 사용하여 데이터를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-151">For an unplanned failover, the device uses the most recent backup to restore the data.</span></span>

### <a name="device-failover-prechecks"></a><span data-ttu-id="6d6aa-152">장치 장애 조치 사전 검사</span><span class="sxs-lookup"><span data-stu-id="6d6aa-152">Device failover prechecks</span></span>

<span data-ttu-id="6d6aa-153">DR이 시작되기 전에 장치에서는 사전 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-153">Before the DR begins, the device performs prechecks.</span></span> <span data-ttu-id="6d6aa-154">이러한 검사는 DR이 시작된 후 오류가 발생하지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-154">These checks help ensure that no errors occur when DR commences.</span></span> <span data-ttu-id="6d6aa-155">사전 검사에는 다음 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-155">The prechecks include:</span></span>

* <span data-ttu-id="6d6aa-156">저장소 계정 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="6d6aa-156">Validating the storage account.</span></span>
* <span data-ttu-id="6d6aa-157">Azure에 대한 클라우드 연결 확인</span><span class="sxs-lookup"><span data-stu-id="6d6aa-157">Checking the cloud connectivity to Azure.</span></span>
* <span data-ttu-id="6d6aa-158">대상 장치의 사용 가능한 공간 확인</span><span class="sxs-lookup"><span data-stu-id="6d6aa-158">Checking available space on the target device.</span></span>
* <span data-ttu-id="6d6aa-159">iSCSI 서버 원본 장치 볼륨에 다음 항목이 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="6d6aa-159">Checking if an iSCSI server source device volume has</span></span>
  
  * <span data-ttu-id="6d6aa-160">유효한 ACR 이름</span><span class="sxs-lookup"><span data-stu-id="6d6aa-160">valid ACR names.</span></span>
  * <span data-ttu-id="6d6aa-161">유효한 IQN(220자를 초과하지 않음)</span><span class="sxs-lookup"><span data-stu-id="6d6aa-161">valid IQN (not exceeding 220 characters).</span></span>
  * <span data-ttu-id="6d6aa-162">유효한 CHAP 암호(12-16자 길이)</span><span class="sxs-lookup"><span data-stu-id="6d6aa-162">valid CHAP passwords (12-16 characters long).</span></span>

<span data-ttu-id="6d6aa-163">앞서 사전 검사 중 하나라도 실패하면 DR을 진행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-163">If any of the preceding prechecks fail, you cannot proceed with the DR.</span></span> <span data-ttu-id="6d6aa-164">해당 문제를 해결한 후 DR을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-164">Resolve those issues and then retry DR.</span></span>

<span data-ttu-id="6d6aa-165">DR이 성공적으로 완료된 후에는, 원본 장치에 있는 클라우드 데이터의 소유권이 대상 장치로 이전됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-165">After the DR is successfully completed, the ownership of the cloud data on the source device is transferred to the target device.</span></span> <span data-ttu-id="6d6aa-166">그 후 원본 장치는 포털에서 더 이상 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-166">The source device is then no longer available in the portal.</span></span> <span data-ttu-id="6d6aa-167">원본 장치의 모든 볼륨/공유에 대한 액세스가 차단되고 대상 장치가 활성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-167">Access to all the volumes/shares on the source device is blocked and the target device becomes active.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d6aa-168">장치를 더 이상 사용할 수 없지만, 호스트 시스템에서 프로비전한 가상 컴퓨터는 여전히 자원을 소비합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-168">Though the device is no longer available, the virtual machine that you provisioned on the host system is still consuming resources.</span></span> <span data-ttu-id="6d6aa-169">DR이 성공적으로 완료되고 나면 이 가상 컴퓨터를 호스트 시스템에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-169">Once the DR is successfully complete, you can delete this virtual machine from your host system.</span></span>
> 
> 

## <a name="fail-over-to-a-virtual-array"></a><span data-ttu-id="6d6aa-170">가상 배열에 대한 장애 조치</span><span class="sxs-lookup"><span data-stu-id="6d6aa-170">Fail over to a virtual array</span></span>

<span data-ttu-id="6d6aa-171">이 절차를 실행하기 전에 StorSimple 장치 관리자 서비스에 다른 StorSimple 가상 배열을 프로비전, 구성 및 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-171">We recommend that you provision, configure, and register another StorSimple Virtual Array with your StorSimple Device Manager service before you run this procedure.</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="6d6aa-172">StorSimple 8000 시리즈 장치에서 1200 가상 장치로 장애 조치(failover)할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-172">You cannot fail over from a StorSimple 8000 series device to a 1200 virtual device.</span></span>
> * <span data-ttu-id="6d6aa-173">FIPS(Federal Information Processing Standard) 사용 가상 장치에서 정부 포털에서 배포된 FIPS 사용 장치 또는 FIPS가 아닌 장치로 장애 조치(failover)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-173">You can fail over from a Federal Information Processing Standard (FIPS) enabled virtual device to another FIPS enabled device or to a non-FIPS device deployed in the Government portal.</span></span>


<span data-ttu-id="6d6aa-174">대상 StorSimple 가상 장치에 장치를 복원하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-174">Perform the following steps to restore the device to a target StorSimple virtual device.</span></span>

1. <span data-ttu-id="6d6aa-175">[장치 장애 조치에 대한 필수 구성 요소](#prerequisites)를 충족하는 대상 장치를 프로비전하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-175">Provision and configure a target device that meets the [prerequisites for device failover](#prerequisites).</span></span> <span data-ttu-id="6d6aa-176">로컬 웹 UI를 통해 장치 구성을 완료하고 해당 당치를 StorSimple 장치 관리자 서비스에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-176">Complete the device configuration via the local web UI and register it to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6d6aa-177">파일 서버를 만드는 경우 [파일 서버로 설정](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)의 1단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-177">If creating a file server, go to step 1 of [set up as file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span> <span data-ttu-id="6d6aa-178">iSCSI 서버를 만드는 경우 [iSCSI 서버로 설정](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)의 1단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-178">If creating an iSCSI server, go to step 1 of [set up as iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span>

2. <span data-ttu-id="6d6aa-179">호스트에서 볼륨/공유를 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-179">Take volumes/shares offline on the host.</span></span> <span data-ttu-id="6d6aa-180">볼륨/공유 오프라인으로 전환하려면 호스트에 관한 운영 체제별 지침을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-180">To take the volumes/shares offline, refer to the operating system–specific instructions for the host.</span></span> <span data-ttu-id="6d6aa-181">오프라인 상태가 아니면 다음을 수행하여 장치에서 모든 볼륨/공유를 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-181">If not already offline, you need to take all the volumes/shares offline on the device by doing the following.</span></span>
   
    1. <span data-ttu-id="6d6aa-182">**장치** 블레이드로 이동하고 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-182">Go to **Devices** blade and select your device.</span></span>
   
    2. <span data-ttu-id="6d6aa-183">**설정 > 관리 > 공유**(또는 **설정 > 관리 > 볼륨**)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-183">Go to **Settings > Manage > Shares** (or **Settings > Manage > Volumes**).</span></span> 
   
    3. <span data-ttu-id="6d6aa-184">공유/볼륨을 선택하고 **오프라인으로 전환**을 마우스 오른쪽 단추로 클릭하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-184">Select a share/volume, right click and select **Take offline**.</span></span> 
   
    4. <span data-ttu-id="6d6aa-185">확인을 위한 메시지가 나타나면 **이 공유를 오프라인으로 전환하는 영향을 이해합니다.**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-185">When prompted for confirmation, check **I understand the impact of taking this share offline.**</span></span> 
   
    5. <span data-ttu-id="6d6aa-186">**오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-186">Click **Take offline**.</span></span>

3. <span data-ttu-id="6d6aa-187">StorSimple 장치 관리자 서비스에서 **관리 > 장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-187">In your StorSimple Device Manager service, go to **Management > Devices**.</span></span> <span data-ttu-id="6d6aa-188">**장치** 블레이드에서 원본 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-188">In the **Devices** blade, select and click your source device.</span></span>

4. <span data-ttu-id="6d6aa-189">**장치 대시보드** 블레이드에서 **비활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-189">In your **Device dashboard** blade, click **Deactivate**.</span></span>

5. <span data-ttu-id="6d6aa-190">**비활성화** 블레이드에서 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-190">In the **Deactivate** blade, you are prompted for confirmation.</span></span> <span data-ttu-id="6d6aa-191">장치 비활성화는 *영구적인* 프로세스이며 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-191">Device deactivation is a *permanent* process that cannot be undone.</span></span> <span data-ttu-id="6d6aa-192">호스트의 공유/볼륨을 오프라인으로 전환하라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-192">You are also reminded to take your shares/volumes offline on the host.</span></span> <span data-ttu-id="6d6aa-193">장치 이름을 입력하여 **비활성화**를 확인하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-193">Type the device name to confirm and click **Deactivate**.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. <span data-ttu-id="6d6aa-194">비활성화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-194">The deactivation starts.</span></span> <span data-ttu-id="6d6aa-195">비활성화가 성공적으로 완료된 후에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-195">You will receive a notification after the deactivation is successfully completed.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. <span data-ttu-id="6d6aa-196">장치 페이지의 장치 상태가 이제 **비활성화됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-196">On the Devices page, the device state will now change to **Deactivated**.</span></span>
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. <span data-ttu-id="6d6aa-197">**장치** 블레이드에서 장애 조치(failover)를 위한 비활성화된 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-197">In the **Devices** blade, select and click the deactivated source device for failover.</span></span> 
9. <span data-ttu-id="6d6aa-198">**장치 대시보드** 블레이드에서 **장애 조치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-198">In the **Device dashboard** blade, click **Fail over**.</span></span> 
10. <span data-ttu-id="6d6aa-199">**장치 장애 조치** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-199">In the **Fail over device** blade, do the following:</span></span>
    
    1. <span data-ttu-id="6d6aa-200">원본 장치 필드가 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-200">The source device field is automatically populated.</span></span> <span data-ttu-id="6d6aa-201">원본 장치의 전체 데이터 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-201">Note the total data size for the source device.</span></span> <span data-ttu-id="6d6aa-202">데이터 크기는 대상 장치에서 사용 가능한 용량 보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-202">The data size should be lesser than the available capacity on the target device.</span></span> <span data-ttu-id="6d6aa-203">장치 이름, 총 용량, 장애 조치를 수행할 공유의 이름을 비롯한 원본 장치와 관련된 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-203">Review the details associated with the source device such as device name, total capacity, and the names of the shares that are failed over.</span></span>

    2. <span data-ttu-id="6d6aa-204">사용 가능한 장치 드롭다운 목록에서 **대상 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-204">From the dropdown list of available devices, choose a **Target device**.</span></span> <span data-ttu-id="6d6aa-205">충분한 용량이 있는 장치만 드롭다운 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-205">Only the devices that have sufficient capacity are displayed in the dropdown list.</span></span>

    3. <span data-ttu-id="6d6aa-206">**이 작업이 대상 장치에 대한 데이터를 장애 조치한다는 것을 이해합니다.**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-206">Check that **I understand that this operation will fail over data to the target device**.</span></span> 

    4. <span data-ttu-id="6d6aa-207">**장애 조치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-207">Click **Fail over**.</span></span>
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. <span data-ttu-id="6d6aa-208">장애 조치 작업을 시작하면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-208">A failover job initiates and you receive a notification.</span></span> <span data-ttu-id="6d6aa-209">**장치 > 작업**을 이동하여 장애 조치를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-209">Go to **Devices > Jobs** to monitor the failover.</span></span>
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. <span data-ttu-id="6d6aa-210">**작업** 블레이드에 원본 장치에 대해 만들어진 장애 조치(failover) 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-210">In the **Jobs** blade, you see a failover job created for the source device.</span></span> <span data-ttu-id="6d6aa-211">이 작업이 DR 사전 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-211">This job performs the DR prechecks.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     <span data-ttu-id="6d6aa-212">DR 사전 검사가 성공적으로 완료된 후에, 장애 조치 작업은 원본 장치에 존재하는 각 공유/볼륨에 대한 복원 작업을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-212">After the DR prechecks are successful, the failover job will spawn restore jobs for each share/volume that exists on your source device.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. <span data-ttu-id="6d6aa-213">장애 조치를 완료한 후 **장치** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-213">After the failover is complete, go to the **Devices** blade.</span></span>
    
    1. <span data-ttu-id="6d6aa-214">장애 조치 프로세스에 대한 대상 장치로 사용된 StorSimple 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-214">Select and click the StorSimple device that was used as the target device for the failover process.</span></span>
    2. <span data-ttu-id="6d6aa-215">**설정 > 관리 > 공유**(또는 iSCSI 서버의 경우 **볼륨**)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-215">Go to **Settings > Management > Shares** (or **Volumes** if iSCSI server).</span></span> <span data-ttu-id="6d6aa-216">**공유** 블레이드의 예전 장치에서 모든 공유(볼륨)를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-216">In the **Shares** blade, you can view all the shares (volumes) from the old device.</span></span>
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. <span data-ttu-id="6d6aa-217">연결하려는 모든 응용 프로그램이 새 장치에 리디렉션되도록 [DNS 별칭을 만들](https://support.microsoft.com/kb/168322)어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-217">You will need to [create a DNS alias](https://support.microsoft.com/kb/168322) so that all the applications that are trying to connect can get redirected to the new device.</span></span>

## <a name="errors-during-dr"></a><span data-ttu-id="6d6aa-218">DR 중 오류</span><span class="sxs-lookup"><span data-stu-id="6d6aa-218">Errors during DR</span></span>

<span data-ttu-id="6d6aa-219">**DR 중 클라우드 연결 중단**</span><span class="sxs-lookup"><span data-stu-id="6d6aa-219">**Cloud connectivity outage during DR**</span></span>

<span data-ttu-id="6d6aa-220">DR이 시작된 후와 장치 복원이 완료되기 전에 클라우드 연결이 중단되면, DR이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-220">If the cloud connectivity is disrupted after DR has started and before the device restore is complete, the DR will fail.</span></span> <span data-ttu-id="6d6aa-221">장애 조치 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-221">You receive a failore notification.</span></span> <span data-ttu-id="6d6aa-222">DR에 대한 대상 장치는 *사용할 수 없음*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-222">The target device for DR is marked as *unusable.*</span></span> <span data-ttu-id="6d6aa-223">동일한 대상 장치를 향후 DR에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-223">You cannot use the same target device for future DRs.</span></span>

<span data-ttu-id="6d6aa-224">**호환되는 대상 장치 없음**</span><span class="sxs-lookup"><span data-stu-id="6d6aa-224">**No compatible target devices**</span></span>

<span data-ttu-id="6d6aa-225">사용 가능한 대상 장치에 충분한 공간이 없으면 호환되는 대상 장치가 없다는 내용의 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-225">If the available target devices do not have sufficient space, you see an error to the effect that there are no compatible target devices.</span></span>

<span data-ttu-id="6d6aa-226">**사전 검사 실패**</span><span class="sxs-lookup"><span data-stu-id="6d6aa-226">**Precheck failures**</span></span>

<span data-ttu-id="6d6aa-227">사전 검사 중 하나가 충족되지 않으면 사전 검사 실패가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-227">If one of the prechecks is not satisfied, then you see precheck failures.</span></span>

## <a name="business-continuity-disaster-recovery-bcdr"></a><span data-ttu-id="6d6aa-228">비즈니스 연속성 재해 복구(BCDR)</span><span class="sxs-lookup"><span data-stu-id="6d6aa-228">Business continuity disaster recovery (BCDR)</span></span>

<span data-ttu-id="6d6aa-229">비즈니스 연속성 재해 복구(BCDR) 시나리오는 전체 Azure 데이터 센터의 작동이 중지되는 경우 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-229">A business continuity disaster recovery (BCDR) scenario occurs when the entire Azure datacenter stops functioning.</span></span> <span data-ttu-id="6d6aa-230">StorSimple 장치 관리자 서비스 및 연결된 StorSimple 장치에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-230">This can affect your StorSimple Device Manager service and the associated StorSimple devices.</span></span>

<span data-ttu-id="6d6aa-231">재해가 발생하기 직전에 등록된 StorSimple 장치가 있으면 해당 StorSimple 장치를 삭제해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-231">If there are StorSimple devices that were registered just before a disaster occurred, then these StorSimple devices may need to be deleted.</span></span> <span data-ttu-id="6d6aa-232">재해가 끝난 후에 해당 장치를 다시 만들고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-232">After the disaster, you can recreate and configure those devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d6aa-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d6aa-233">Next steps</span></span>

<span data-ttu-id="6d6aa-234">[로컬 웹 UI를 사용하여 StorSimple 가상 배열을 관리](storsimple-ova-web-ui-admin.md)하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d6aa-234">Learn more about how to [administer your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span></span>

