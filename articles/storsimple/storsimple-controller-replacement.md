---
title: "StorSimple 장치 컨트롤러 교체 | Microsoft Docs"
description: "StorSimple 장치에서 하나 또는 두 개의 컨트롤러 모듈을 모두 꺼내고 교체하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e25b52b7-60f5-47f3-bffc-6c157d57ab5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/03/2017
ms.author: alkohli
ms.openlocfilehash: 5dd5ffc7c08fcc9263b91ca5ac86de5163f91657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a><span data-ttu-id="11176-103">StorSimple 장치의 컨트롤러 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="11176-103">Replace a controller module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="11176-104">개요</span><span class="sxs-lookup"><span data-stu-id="11176-104">Overview</span></span>
<span data-ttu-id="11176-105">이 자습서에서는 StorSimple 장치에서 하나 또는 두 개의 컨트롤러 모듈을 모두 꺼내고 교체하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-105">This tutorial explains how to remove and replace one or both controller modules in a StorSimple device.</span></span> <span data-ttu-id="11176-106">단일 및 이중 컨트롤러 교체 시나리오에 대한 기본 논리에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-106">It also discusses the underlying logic for the single and dual controller replacement scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="11176-107">컨트롤러 교체를 수행하기 전에 항상 컨트롤러 펌웨어를 최신 버전으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-107">Prior to performing a controller replacement, we recommend that you always update your controller firmware to the latest version.</span></span>
> 
> <span data-ttu-id="11176-108">StorSimple 장치의 손상을 방지하려면 LED가 다음 중 하나로 표시될 때까지 컨트롤러를 꺼내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="11176-108">To prevent damage to your StorSimple device, do not eject the controller until the LEDs are showing as one of the following:</span></span>
> 
> * <span data-ttu-id="11176-109">모든 표시등이 OFF입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-109">All lights are OFF.</span></span>
> * <span data-ttu-id="11176-110">LED 3, ![녹색 확인 표시 아이콘](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), ![빨간색 십자 아이콘](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) 이 깜박이고 LED 0 및 LED 7이 **켜짐**입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-110">LED 3, ![Green check icon](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), and ![Red cross icon](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) are flashing, and LED 0 and LED 7 are **ON**.</span></span>
> 
> 

<span data-ttu-id="11176-111">다음 표에서는 지원되는 컨트롤러 교체 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11176-111">The following table shows the supported controller replacement scenarios.</span></span>

| <span data-ttu-id="11176-112">사례</span><span class="sxs-lookup"><span data-stu-id="11176-112">Case</span></span> | <span data-ttu-id="11176-113">교체 시나리오</span><span class="sxs-lookup"><span data-stu-id="11176-113">Replacement scenario</span></span> | <span data-ttu-id="11176-114">해당 절차</span><span class="sxs-lookup"><span data-stu-id="11176-114">Applicable procedure</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="11176-115">1</span><span class="sxs-lookup"><span data-stu-id="11176-115">1</span></span> |<span data-ttu-id="11176-116">한 컨트롤러는 실패 상태이고 다른 컨트롤러는 정상 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-116">One controller is in a failed state, the other controller is healthy and active.</span></span> |<span data-ttu-id="11176-117">[단일 컨트롤러 교체를 지원하는 논리](#single-controller-replacement-logic) 및 [교체 단계](#single-controller-replacement-steps)를 설명하는 [단일 컨트롤러 교체](#replace-a-single-controller)입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-117">[Single controller replacement](#replace-a-single-controller), which describes the [logic behind a single controller replacement](#single-controller-replacement-logic), as well as the [replacement steps](#single-controller-replacement-steps).</span></span> |
| <span data-ttu-id="11176-118">2</span><span class="sxs-lookup"><span data-stu-id="11176-118">2</span></span> |<span data-ttu-id="11176-119">두 컨트롤러에서 모두 오류가 발생했으며 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-119">Both the controllers have failed and require replacement.</span></span> <span data-ttu-id="11176-120">섀시, 디스크 및 디스크 엔클로저는 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-120">The chassis, disks, and disk enclosure are healthy.</span></span> |<span data-ttu-id="11176-121">[이중 컨트롤러 교체를 지원하는 논리](#dual-controller-replacement-logic) 및 [교체 단계](#dual-controller-replacement-steps)를 설명하는 [이중 컨트롤러 교체](#replace-both-controllers)입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-121">[Dual controller replacement](#replace-both-controllers), which describes the [logic behind a dual controller replacement](#dual-controller-replacement-logic), as well as the [replacement steps](#dual-controller-replacement-steps).</span></span> |
| <span data-ttu-id="11176-122">3</span><span class="sxs-lookup"><span data-stu-id="11176-122">3</span></span> |<span data-ttu-id="11176-123">동일한 장치 또는 서로 다른 장치의 컨트롤러를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-123">Controllers from the same device or from different devices are swapped.</span></span> <span data-ttu-id="11176-124">섀시, 디스크 및 디스크 엔클로저는 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-124">The chassis, disks, and disk enclosures are healthy.</span></span> |<span data-ttu-id="11176-125">슬롯 불일치 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-125">A slot mismatch alert message will appear.</span></span> |
| <span data-ttu-id="11176-126">4</span><span class="sxs-lookup"><span data-stu-id="11176-126">4</span></span> |<span data-ttu-id="11176-127">한 컨트롤러는 없고 다른 컨트롤러에서는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-127">One controller is missing and the other controller fails.</span></span> |<span data-ttu-id="11176-128">[이중 컨트롤러 교체를 지원하는 논리](#dual-controller-replacement-logic) 및 [교체 단계](#dual-controller-replacement-steps)를 설명하는 [이중 컨트롤러 교체](#replace-both-controllers)입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-128">[Dual controller replacement](#replace-both-controllers), which describes the [logic behind a dual controller replacement](#dual-controller-replacement-logic), as well as the [replacement steps](#dual-controller-replacement-steps).</span></span> |
| <span data-ttu-id="11176-129">5</span><span class="sxs-lookup"><span data-stu-id="11176-129">5</span></span> |<span data-ttu-id="11176-130">하나 또는 두 개의 컨트롤러에서 모두 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-130">One or both controllers have failed.</span></span> <span data-ttu-id="11176-131">직렬 콘솔 또는 Windows PowerShell 원격을 통해 장치에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-131">You cannot access the device through the serial console or Windows PowerShell remoting.</span></span> |<span data-ttu-id="11176-132">수동 컨트롤러 교체 절차는 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-132">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) for a manual controller replacement procedure.</span></span> |
| <span data-ttu-id="11176-133">6</span><span class="sxs-lookup"><span data-stu-id="11176-133">6</span></span> |<span data-ttu-id="11176-134">컨트롤러의 빌드 버전이 서로 다르며, 다음과 같은 이유 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-134">The controllers have a different build version, which may be due to:</span></span><ul><li><span data-ttu-id="11176-135">컨트롤러에는 다양한 소프트웨어 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-135">Controllers have a different software version.</span></span></li><li><span data-ttu-id="11176-136">컨트롤러에는 다양한 펌웨어 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-136">Controllers have a different firmware version.</span></span></li></ul> |<span data-ttu-id="11176-137">컨트롤러 소프트웨어 버전이 서로 다른 경우 교체 논리에서 이를 감지하고 교체 컨트롤러의 소프트웨어 버전을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-137">If the controller software versions are different, the replacement logic detects that and updates the software version on the replacement controller.</span></span><br><br><span data-ttu-id="11176-138">컨트롤러 펌웨어 버전이 서로 다르고 이전 펌웨어 버전을 자동으로 업그레이드할 수 **없는** 경우 Azure 클래식 포털에 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-138">If the controller firmware versions are different and the old firmware version is **not** automatically upgradeable, an alert message will appear in the Azure classic portal.</span></span> <span data-ttu-id="11176-139">업데이트를 검색하고 펌웨어 업데이트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-139">You should scan for updates and install the firmware updates.</span></span></br></br><span data-ttu-id="11176-140">컨트롤러 펌웨어 버전이 서로 다르고 이전 펌웨어 버전을 자동으로 업그레이드할 수 있는 경우 컨트롤러 교체 논리에서 이를 감지하고 컨트롤러가 시작된 후 펌웨어가 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-140">If the controller firmware versions are different and the old firmware version is automatically upgradeable, the controller replacement logic will detect this, and after the controller starts, the firmware will be automatically updated.</span></span> |

<span data-ttu-id="11176-141">오류가 발생한 경우 컨트롤러 모듈을 꺼내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-141">You need to remove a controller module if it has failed.</span></span> <span data-ttu-id="11176-142">하나 또는 두 개의 컨트롤러 모듈에서 모두 오류가 발생할 수 있으며, 단일 컨트롤러 교체 또는 이중 컨트롤러 교체가 요구될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-142">One or both the controller modules can fail, which can result in a single controller replacement or dual controller replacement.</span></span> <span data-ttu-id="11176-143">교체 절차 및 지원 논리는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-143">For replacement procedures and the logic behind them, see the following:</span></span>

* [<span data-ttu-id="11176-144">단일 컨트롤러 교체</span><span class="sxs-lookup"><span data-stu-id="11176-144">Replace a single controller</span></span>](#replace-a-single-controller)
* [<span data-ttu-id="11176-145">두 컨트롤러 모두 교체</span><span class="sxs-lookup"><span data-stu-id="11176-145">Replace both controllers</span></span>](#replace-both-controllers)
* [<span data-ttu-id="11176-146">컨트롤러 꺼내기</span><span class="sxs-lookup"><span data-stu-id="11176-146">Remove a controller</span></span>](#remove-a-controller)
* [<span data-ttu-id="11176-147">컨트롤러 삽입</span><span class="sxs-lookup"><span data-stu-id="11176-147">Insert a controller</span></span>](#insert-a-controller)
* [<span data-ttu-id="11176-148">장치의 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-148">Identify the active controller on your device</span></span>](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> <span data-ttu-id="11176-149">컨트롤러를 꺼내고 교체하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에서 안전 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-149">Before removing and replacing a controller, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="replace-a-single-controller"></a><span data-ttu-id="11176-150">단일 컨트롤러 교체</span><span class="sxs-lookup"><span data-stu-id="11176-150">Replace a single controller</span></span>
<span data-ttu-id="11176-151">Microsoft Azure StorSimple 장치의 두 컨트롤러 중 하나에서 오류가 발생했거나 오작동하거나 없는 경우 단일 컨트롤러를 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-151">When one of the two controllers on the Microsoft Azure StorSimple device has failed, is malfunctioning, or is missing, you need to replace a single controller.</span></span> 

### <a name="single-controller-replacement-logic"></a><span data-ttu-id="11176-152">단일 컨트롤러 교체 논리</span><span class="sxs-lookup"><span data-stu-id="11176-152">Single controller replacement logic</span></span>
<span data-ttu-id="11176-153">단일 컨트롤러 교체에서는 오류가 발생한 컨트롤러를 먼저 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-153">In a single controller replacement, you should first remove the failed controller.</span></span> <span data-ttu-id="11176-154">(장치의 나머지 컨트롤러가 활성 컨트롤러가 됩니다.) 교체 컨트롤러를 삽입하면 다음 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-154">(The remaining controller in the device is the active controller.) When you insert the replacement controller, the following actions occur:</span></span>

1. <span data-ttu-id="11176-155">교체 컨트롤러가 즉시 StorSimple 장치와 통신을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-155">The replacement controller immediately starts communicating with the StorSimple device.</span></span>
2. <span data-ttu-id="11176-156">활성 컨트롤러에 대한 VHD(가상 하드 디스크)의 스냅숏이 교체 컨트롤러에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-156">A snapshot of the virtual hard disk (VHD) for the active controller is copied on the replacement controller.</span></span>
3. <span data-ttu-id="11176-157">교체 컨트롤러가 이 VHD에서 시작될 때 대기 컨트롤러로 인식되도록 스냅숏이 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-157">The snapshot is modified so that when the replacement controller starts from this VHD, it will be recognized as a standby controller.</span></span>
4. <span data-ttu-id="11176-158">수정이 완료되면 교체 컨트롤러가 대기 컨트롤러로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-158">When the modifications are complete, the replacement controller will start as the standby controller.</span></span>
5. <span data-ttu-id="11176-159">두 컨트롤러가 모두 실행되고 있으면 클러스터가 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-159">When both the controllers are running, the cluster comes online.</span></span>

### <a name="single-controller-replacement-steps"></a><span data-ttu-id="11176-160">단일 컨트롤러 교체 단계</span><span class="sxs-lookup"><span data-stu-id="11176-160">Single controller replacement steps</span></span>
<span data-ttu-id="11176-161">Microsoft Azure StorSimple 장치의 컨트롤러 중 하나에서 오류가 발생하는 경우 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="11176-161">Complete the following steps if one of the controllers in your Microsoft Azure StorSimple device fails.</span></span> <span data-ttu-id="11176-162">(다른 컨트롤러는 활성화되고 실행 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-162">(The other controller must be active and running.</span></span> <span data-ttu-id="11176-163">두 컨트롤러에서 모두 오류가 발생하거나 오작동하는 경우 [이중 컨트롤러 교체 단계](#dual-controller-replacement-steps)로 이동합니다.)</span><span class="sxs-lookup"><span data-stu-id="11176-163">If both controllers fail or malfunction, go to [dual controller replacement steps](#dual-controller-replacement-steps).)</span></span>

> [!NOTE]
> <span data-ttu-id="11176-164">컨트롤러가 다시 시작되고 단일 컨트롤러 교체 절차에서 완전히 복구되는 데 30-45분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-164">It can take 30 – 45 minutes for the controller to restart and completely recover from the single controller replacement procedure.</span></span> <span data-ttu-id="11176-165">케이블 연결을 포함하여 전체 절차의 총 시간은 약 2시간입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-165">The total time for the entire procedure, including attaching the cables, is approximately 2 hours.</span></span>
> 
> 

#### <a name="to-remove-a-single-failed-controller-module"></a><span data-ttu-id="11176-166">오류가 발생한 단일 컨트롤러 모듈을 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="11176-166">To remove a single failed controller module</span></span>
1. <span data-ttu-id="11176-167">Azure 클래식 포털에서 StorSimple Manager 서비스로 이동하고 **장치** 탭을 클릭한 다음 모니터링하려는 장치의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-167">In the Azure classic portal, go to the StorSimple Manager service, click the **Devices** tab, and then click the name of the device that you want to monitor.</span></span>
2. <span data-ttu-id="11176-168">**유지 관리 > 하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-168">Go to **Maintenance > Hardware Status**.</span></span> <span data-ttu-id="11176-169">컨트롤러 0 또는 컨트롤러 1의 상태가 오류를 나타내는 빨강이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-169">The status of either Controller 0 or Controller 1 should be red, which indicates a failure.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="11176-170">단일 컨트롤러 교체에서 오류가 발생한 컨트롤러는 항상 대기 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-170">The failed controller in a single controller replacement is always a standby controller.</span></span>
   > 
   > 
3. <span data-ttu-id="11176-171">그림 1과 다음 표를 사용하여 오류가 발생한 컨트롤러 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-171">Use Figure 1 and the following table to locate the failed controller module.</span></span>  
   
    ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-controller-replacement/IC740994.png)
   
    <span data-ttu-id="11176-173">**그림 1** StorSimple 장치 뒷면</span><span class="sxs-lookup"><span data-stu-id="11176-173">**Figure 1** Back of StorSimple device</span></span>
   
   | <span data-ttu-id="11176-174">레이블</span><span class="sxs-lookup"><span data-stu-id="11176-174">Label</span></span> | <span data-ttu-id="11176-175">설명</span><span class="sxs-lookup"><span data-stu-id="11176-175">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="11176-176">1</span><span class="sxs-lookup"><span data-stu-id="11176-176">1</span></span> |<span data-ttu-id="11176-177">PCM 0</span><span class="sxs-lookup"><span data-stu-id="11176-177">PCM 0</span></span> |
   | <span data-ttu-id="11176-178">2</span><span class="sxs-lookup"><span data-stu-id="11176-178">2</span></span> |<span data-ttu-id="11176-179">PCM 1</span><span class="sxs-lookup"><span data-stu-id="11176-179">PCM 1</span></span> |
   | <span data-ttu-id="11176-180">3</span><span class="sxs-lookup"><span data-stu-id="11176-180">3</span></span> |<span data-ttu-id="11176-181">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="11176-181">Controller 0</span></span> |
   | <span data-ttu-id="11176-182">4</span><span class="sxs-lookup"><span data-stu-id="11176-182">4</span></span> |<span data-ttu-id="11176-183">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="11176-183">Controller 1</span></span> |
4. <span data-ttu-id="11176-184">오류가 발생한 컨트롤러의 데이터 포트에서 연결된 네트워크 케이블을 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-184">On the failed controller, remove all the connected network cables from the data ports.</span></span> <span data-ttu-id="11176-185">8600 모델을 사용하는 경우 컨트롤러를 EBOD 컨트롤러에 연결하는 SAS 케이블를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-185">If you are using an 8600 model, also remove the SAS cables that connect the controller to the EBOD controller.</span></span>
5. <span data-ttu-id="11176-186">[컨트롤러 제거](#remove-a-controller)의 단계에 따라 오류가 발생한 컨트롤러를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-186">Follow the steps in [remove a controller](#remove-a-controller) to remove the failed controller.</span></span> 
6. <span data-ttu-id="11176-187">오류가 발생한 컨트롤러를 제거한 슬롯과 동일한 슬롯에 팩터리 교체를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-187">Install the factory replacement in the same slot from which the failed controller was removed.</span></span> <span data-ttu-id="11176-188">이렇게 하면 단일 컨트롤러 교체 논리가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-188">This triggers the single controller replacement logic.</span></span> <span data-ttu-id="11176-189">자세한 내용은 [단일 컨트롤러 교체 논리](#single-controller-replacement-logic)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-189">For more information, see [single controller replacement logic](#single-controller-replacement-logic).</span></span>
7. <span data-ttu-id="11176-190">단일 컨트롤러 교체 논리가 백그라운드에서 진행되는 동안 케이블을 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-190">While the single controller replacement logic progresses in the background, reconnect the cables.</span></span> <span data-ttu-id="11176-191">교체 전에 연결된 것과 동일한 방식으로 모든 케이블을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-191">Take care to connect all the cables exactly the same way that they were connected before the replacement.</span></span>
8. <span data-ttu-id="11176-192">컨트롤러가 다시 시작된 후 Azure 클래식 포털에서 **컨트롤러 상태** 및 **클러스터 상태**를 검사하여 컨트롤러가 다시 정상 상태로 돌아갔으며 대기 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-192">After the controller restarts, check the **Controller status** and the **Cluster status** in the Azure classic portal to verify that the controller is back to a healthy state and is in standby mode.</span></span>

> [!NOTE]
> <span data-ttu-id="11176-193">직렬 콘솔을 통해 장치를 모니터링하는 경우 컨트롤러가 교체 절차에서 복구되는 동안 여러 번 다시 시작되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-193">If you are monitoring the device through the serial console, you may see multiple restarts while the controller is recovering from the replacement procedure.</span></span> <span data-ttu-id="11176-194">직렬 콘솔 메뉴가 표시되면 교체가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-194">When the serial console menu is presented, then you know that the replacement is complete.</span></span> <span data-ttu-id="11176-195">컨트롤러 교체를 시작한 후 2시간 내에 메뉴가 표시되지 않는 경우 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-195">If the menu does not appear within two hours of starting the controller replacement, please [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
>
> <span data-ttu-id="11176-196">업데이트 4부터는 장치의 Windows PowerShell 인터페이스에서 cmdlet `Get-HCSControllerReplacementStatus`를 사용하여 컨트롤러 대체 프로세스의 상태를 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-196">Starting Update 4, you can also use the cmdlet `Get-HCSControllerReplacementStatus` in the Windows PowerShell interface of the device to monitor the status of the controller replacement process.</span></span>
> 

## <a name="replace-both-controllers"></a><span data-ttu-id="11176-197">두 컨트롤러 모두 교체</span><span class="sxs-lookup"><span data-stu-id="11176-197">Replace both controllers</span></span>
<span data-ttu-id="11176-198">Microsoft Azure StorSimple 장치의 두 컨트롤러에서 모두 오류가 발생했거나 오작동하거나 없는 경우 두 컨트롤러를 모두 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-198">When both controllers on the Microsoft Azure StorSimple device have failed, are malfunctioning, or are missing, you need to replace both controllers.</span></span> 

### <a name="dual-controller-replacement-logic"></a><span data-ttu-id="11176-199">이중 컨트롤러 교체 논리</span><span class="sxs-lookup"><span data-stu-id="11176-199">Dual controller replacement logic</span></span>
<span data-ttu-id="11176-200">이중 컨트롤러 교체에서는 먼저 오류가 발생한 두 컨트롤러를 모두 제거하고 교체를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-200">In a dual controller replacement, you first remove both failed controllers and then insert replacements.</span></span> <span data-ttu-id="11176-201">두 교체 컨트롤러를 삽입하면 다음 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-201">When the two replacement controllers are inserted, the following actions occur:</span></span>

1. <span data-ttu-id="11176-202">슬롯 0의 교체 컨트롤러가 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-202">The replacement controller in slot 0 checks the following:</span></span>
   
   1. <span data-ttu-id="11176-203">최신 버전의 펌웨어 및 소프트웨어를 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="11176-203">Is it using current versions of the firmware and software?</span></span>
   2. <span data-ttu-id="11176-204">클러스터의 일부인가요?</span><span class="sxs-lookup"><span data-stu-id="11176-204">Is it a part of the cluster?</span></span>
   3. <span data-ttu-id="11176-205">피어 컨트롤러가 실행 중이며 클러스터되었나요?</span><span class="sxs-lookup"><span data-stu-id="11176-205">Is the peer controller running and is it clustered?</span></span>
      
      <span data-ttu-id="11176-206">이러한 조건이 모두 true가 아니면 컨트롤러가 최근 매일 백업을 찾습니다(S 드라이브의 **nonDOMstorage**에 있음).</span><span class="sxs-lookup"><span data-stu-id="11176-206">If none of these conditions are true, the controller looks for the latest daily backup (located in the **nonDOMstorage** on drive S).</span></span> <span data-ttu-id="11176-207">컨트롤러가 백업에서 VHD의 최신 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-207">The controller copies the latest snapshot of the VHD from the backup.</span></span>
2. <span data-ttu-id="11176-208">슬롯 0의 컨트롤러가 스냅숏을 사용하여 자체 이미지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-208">The controller in slot 0 uses the snapshot to image itself.</span></span>
3. <span data-ttu-id="11176-209">한편, 슬롯 1의 컨트롤러는 컨트롤러 0이 이미징을 완료하고 시작될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="11176-209">Meanwhile, the controller in slot 1 waits for controller 0 to complete the imaging and start.</span></span>
4. <span data-ttu-id="11176-210">컨트롤러 0이 시작된 후 컨트롤러 1이 컨트롤러 0에서 만든 클러스터를 검색하며, 이로 인해 단일 컨트롤러 교체 논리가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-210">After controller 0 starts, controller 1 detects the cluster created by controller 0, which triggers the single controller replacement logic.</span></span> <span data-ttu-id="11176-211">자세한 내용은 [단일 컨트롤러 교체 논리](#single-controller-replacement-logic)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-211">For more information, see [single controller replacement logic](#single-controller-replacement-logic).</span></span>
5. <span data-ttu-id="11176-212">그 후에는 두 컨트롤러가 모두 실행되고 클러스터가 온라인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-212">Afterwards, both controllers will be running and the cluster will come online.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11176-213">이중 컨트롤러 교체 다음에는 StorSimple 장치가 구성된 후 반드시 장치를 수동으로 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-213">Following a dual controller replacement, after the StorSimple device is configured, it is essential that you take a manual backup of the device.</span></span> <span data-ttu-id="11176-214">24시간이 경과할 때까지 일별 장치 구성 백업이 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-214">Daily device configuration backups are not triggered until after 24 hours have elapsed.</span></span> <span data-ttu-id="11176-215">[Microsoft 지원](storsimple-contact-microsoft-support.md)의 도움을 받아 장치를 수동으로 백업하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-215">Work with [Microsoft Support](storsimple-contact-microsoft-support.md) to make a manual backup of your device.</span></span>
> 
> 

### <a name="dual-controller-replacement-steps"></a><span data-ttu-id="11176-216">이중 컨트롤러 교체 단계</span><span class="sxs-lookup"><span data-stu-id="11176-216">Dual controller replacement steps</span></span>
<span data-ttu-id="11176-217">이 워크플로는 Microsoft Azure StorSimple 장치의 두 컨트롤러에서 모두 오류가 발생한 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-217">This workflow is required when both of the controllers in your Microsoft Azure StorSimple device have failed.</span></span> <span data-ttu-id="11176-218">이러한 상황은 냉각 시스템 작동이 중지되어 짧은 기간 내에 두 컨트롤러에서 모두 오류가 발생하는 데이터 센터에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-218">This could happen in a datacenter in which the cooling system stops working, and as a result, both the controllers fail within a short period of time.</span></span> <span data-ttu-id="11176-219">StorSimple 장치가 켜져 있는지 여부 및 8600 또는 8100 모델을 사용하는지에 따라 다른 일련의 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-219">Depending on whether the StorSimple device is turned off or on, and whether you are using an 8600 or an 8100 model, a different set of steps is required.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11176-220">컨트롤러가 다시 시작되고 이중 컨트롤러 교체 절차에서 완전히 복구되는 데 45분-1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-220">It can take 45 minutes to 1 hour for the controller to restart and completely recover from a dual controller replacement procedure.</span></span> <span data-ttu-id="11176-221">케이블 연결을 포함하여 전체 절차의 총 시간은 약 2.5시간입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-221">The total time for the entire procedure, including attaching the cables, is approximately 2.5 hours.</span></span>
> 
> 

#### <a name="to-replace-both-controller-modules"></a><span data-ttu-id="11176-222">두 컨트롤러 모듈을 모두 교체하려면</span><span class="sxs-lookup"><span data-stu-id="11176-222">To replace both controller modules</span></span>
1. <span data-ttu-id="11176-223">장치가 꺼져 있는 경우 이 단계를 건너뛰고 다음 단계로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-223">If the device is turned off, skip this step and proceed to the next step.</span></span> <span data-ttu-id="11176-224">장치가 켜져 있는 경우 장치를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="11176-224">If the device is turned on, turn off the device.</span></span>
   
   1. <span data-ttu-id="11176-225">8600 모델을 사용하는 경우 기본 엔클로저를 먼저 끈 다음 EBOD 엔클로저를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="11176-225">If you are using an 8600 model, turn off the primary enclosure first, and then turn off the EBOD enclosure.</span></span>
   2. <span data-ttu-id="11176-226">장치가 완전히 종료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="11176-226">Wait until the device has shut down completely.</span></span> <span data-ttu-id="11176-227">장치 뒷면의 모든 LED가 꺼집니다.</span><span class="sxs-lookup"><span data-stu-id="11176-227">All the LEDs in the back of the device will be off.</span></span>
2. <span data-ttu-id="11176-228">데이터 포트에 연결된 모든 네트워크 케이블을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-228">Remove all the network cables that are connected to the data ports.</span></span> <span data-ttu-id="11176-229">8600 모델을 사용하는 경우 기본 엔클로저를 EBOD 엔클로저에 연결하는 SAS 케이블도 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-229">If you are using an 8600 model, also remove the SAS cables that connect the primary enclosure to the EBOD enclosure.</span></span>
3. <span data-ttu-id="11176-230">StorSimple 장치에서 두 컨트롤러를 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-230">Remove both controllers from the StorSimple device.</span></span> <span data-ttu-id="11176-231">자세한 내용은 [컨트롤러 제거](#remove-a-controller)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-231">For more information, see [remove a controller](#remove-a-controller).</span></span>
4. <span data-ttu-id="11176-232">컨트롤러 0에 대한 팩터리 교체를 먼저 삽입하고 컨트롤러 1을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-232">Insert the factory replacement for Controller 0 first, and then insert Controller 1.</span></span> <span data-ttu-id="11176-233">자세한 내용은 [컨트롤러 삽입](#insert-a-controller)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-233">For more information, see [insert a controller](#insert-a-controller).</span></span> <span data-ttu-id="11176-234">이렇게 하면 이중 컨트롤러 교체 논리가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-234">This triggers the dual controller replacement logic.</span></span> <span data-ttu-id="11176-235">자세한 내용은 [이중 컨트롤러 교체 논리](#dual-controller-replacement-logic)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-235">For more information, see [dual controller replacement logic](#dual-controller-replacement-logic).</span></span>
5. <span data-ttu-id="11176-236">컨트롤러 교체 논리가 백그라운드에서 진행되는 동안 케이블을 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-236">While the controller replacement logic progresses in the background, reconnect the cables.</span></span> <span data-ttu-id="11176-237">교체 전에 연결된 것과 동일한 방식으로 모든 케이블을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-237">Take care to connect all the cables exactly the same way that they were connected before the replacement.</span></span> <span data-ttu-id="11176-238">[StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [StorSimple 8600 장치 설치](storsimple-8600-hardware-installation.md)의 장치를 케이블로 연결 섹션에서 모델에 대한 자세한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-238">See the detailed instructions for your model in the Cable your device section of [install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
6. <span data-ttu-id="11176-239">StorSimple 장치를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="11176-239">Turn on the StorSimple device.</span></span> <span data-ttu-id="11176-240">8600 모델을 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="11176-240">If you are using an 8600 model:</span></span>
   
   1. <span data-ttu-id="11176-241">EBOD 엔클로저가 먼저 켜지는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-241">Make sure that the EBOD enclosure is turned on first.</span></span>
   2. <span data-ttu-id="11176-242">EBOD 엔클로저가 실행될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="11176-242">Wait until the EBOD enclosure is running.</span></span>
   3. <span data-ttu-id="11176-243">기본 엔클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="11176-243">Turn on the primary enclosure.</span></span>
   4. <span data-ttu-id="11176-244">첫 번째 컨트롤러가 다시 시작되고 정상 상태이면 시스템이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-244">After the first controller restarts and is in a healthy state, the system will be running.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="11176-245">직렬 콘솔을 통해 장치를 모니터링하는 경우 컨트롤러가 교체 절차에서 복구되는 동안 여러 번 다시 시작되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-245">If you are monitoring the device through the serial console, you may see multiple restarts while the controller is recovering from the replacement procedure.</span></span> <span data-ttu-id="11176-246">직렬 콘솔 메뉴가 표시되면 교체가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="11176-246">When the serial console menu appears, then you know that the replacement is complete.</span></span> <span data-ttu-id="11176-247">컨트롤러 교체를 시작한 후 2.5시간 내에 메뉴가 표시되지 않는 경우 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="11176-247">If the menu does not appear within 2.5 hours of starting the controller replacement, please [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
      > 
      > 

## <a name="remove-a-controller"></a><span data-ttu-id="11176-248">컨트롤러 꺼내기</span><span class="sxs-lookup"><span data-stu-id="11176-248">Remove a controller</span></span>
<span data-ttu-id="11176-249">StorSimple 장치에서 결함이 있는 컨트롤러 모듈을 꺼내려면 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="11176-249">Use the following procedure to remove a faulty controller module from your StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="11176-250">다음 그림은 컨트롤러 0에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-250">The following illustrations are for controller 0.</span></span> <span data-ttu-id="11176-251">컨트롤러 1의 경우 반대가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-251">For controller 1, these would be reversed.</span></span>
> 
> 

#### <a name="to-remove-a-controller-module"></a><span data-ttu-id="11176-252">컨트롤러 모듈을 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="11176-252">To remove a controller module</span></span>
1. <span data-ttu-id="11176-253">엄지와 집게 손가락으로 모듈 래치를 잡습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-253">Grasp the module latch between your thumb and forefinger.</span></span>
2. <span data-ttu-id="11176-254">엄지와 집게 손가락을 부드럽게 눌러 컨트롤러 래치를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-254">Gently squeeze your thumb and forefinger together to release the controller latch.</span></span>
   
    ![컨트롤러 래치 해제](./media/storsimple-controller-replacement/IC741047.png)
   
    <span data-ttu-id="11176-256">**그림 2** 컨트롤러 래치 해제</span><span class="sxs-lookup"><span data-stu-id="11176-256">**Figure 2** Releasing controller latch</span></span>
3. <span data-ttu-id="11176-257">래치를 핸들로 사용하여 컨트롤러를 섀시 밖으로 밉니다.</span><span class="sxs-lookup"><span data-stu-id="11176-257">Use the latch as a handle to slide the controller out of the chassis.</span></span>
   
    ![섀시 밖으로 컨트롤러 밀기](./media/storsimple-controller-replacement/IC741048.png)
   
    <span data-ttu-id="11176-259">**그림 3** 섀시 밖으로 컨트롤러 밀기</span><span class="sxs-lookup"><span data-stu-id="11176-259">**Figure 3** Sliding the controller out of the chassis</span></span>

## <a name="insert-a-controller"></a><span data-ttu-id="11176-260">컨트롤러 삽입</span><span class="sxs-lookup"><span data-stu-id="11176-260">Insert a controller</span></span>
<span data-ttu-id="11176-261">StorSimple 장치에서 결함이 있는 모듈을 꺼낸 후 팩터리 제공 컨트롤러 모듈을 설치하려면 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="11176-261">Use the following procedure to install a factory-supplied controller module after you remove a faulty module from your StorSimple device.</span></span>

#### <a name="to-install-a-controller-module"></a><span data-ttu-id="11176-262">컨트롤러 모듈을 설치하려면</span><span class="sxs-lookup"><span data-stu-id="11176-262">To install a controller module</span></span>
1. <span data-ttu-id="11176-263">인터페이스 커넥터에 손상된 부분이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-263">Check to see if there is any damage to the interface connectors.</span></span> <span data-ttu-id="11176-264">커넥터 핀이 손상되었거나 구부러진 경우 모듈을 설치하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="11176-264">Do not install the module if any of the connector pins are damaged or bent.</span></span>
2. <span data-ttu-id="11176-265">래치가 완전히 해제된 동안 컨트롤러 모듈을 섀시에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-265">Slide the controller module into the chassis while the latch is fully released.</span></span> 
   
    ![섀시 안으로 컨트롤러 밀기](./media/storsimple-controller-replacement/IC741053.png)
   
    <span data-ttu-id="11176-267">**그림 4** 섀시에 컨트롤러 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="11176-267">**Figure 4** Sliding controller into the chassis</span></span>
3. <span data-ttu-id="11176-268">컨트롤러 모듈을 삽입한 후 컨트롤러 모듈을 섀시 안으로 계속 누르면서 래치를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-268">With the controller module inserted, begin closing the latch while continuing to push the controller module into the chassis.</span></span> <span data-ttu-id="11176-269">래치가 걸려 컨트롤러를 제자리로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-269">The latch will engage to guide the controller into place.</span></span>
   
    ![컨트롤러 래치 닫기](./media/storsimple-controller-replacement/IC741054.png)
   
    <span data-ttu-id="11176-271">**그림 5** 컨트롤러 래치 닫기</span><span class="sxs-lookup"><span data-stu-id="11176-271">**Figure 5** Closing the controller latch</span></span>
4. <span data-ttu-id="11176-272">래치가 제자리에 놓이면 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-272">You're done when the latch snaps into place.</span></span> <span data-ttu-id="11176-273">이제 **OK** LED가 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="11176-273">The **OK** LED should now be on.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="11176-274">컨트롤러 및 LED가 활성화되는 데 최대 5분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-274">It can take up to 5 minutes for the controller and the LED to activate.</span></span>
   > 
   > 
5. <span data-ttu-id="11176-275">교체에 성공했는지 확인하려면 Azure 클래식 포털에서 **장치** > **유지 관리** > **하드웨어 상태**로 이동한 다음 컨트롤러 0과 컨트롤러 1이 모두 정상(녹색 상태)인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-275">To verify that the replacement is successful, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**, and make sure that both controller 0 and controller 1 are healthy (status is green).</span></span>

## <a name="identify-the-active-controller-on-your-device"></a><span data-ttu-id="11176-276">장치의 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-276">Identify the active controller on your device</span></span>
<span data-ttu-id="11176-277">처음 장치를 등록하거나 컨트롤러를 교체하는 경우와 같이 StorSimple 장치에서 활성 컨트롤러를 찾아야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-277">There are many situations, such as first-time device registration or controller replacement, that require you to locate the active controller on a StorSimple device.</span></span> <span data-ttu-id="11176-278">활성 컨트롤러는 모든 디스크 펌웨어 및 네트워킹 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-278">The active controller processes all the disk firmware and networking operations.</span></span> <span data-ttu-id="11176-279">다음 방법 중 하나를 사용하여 활성 컨트롤러를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-279">You can use any of the following methods to identify the active controller:</span></span>

* [<span data-ttu-id="11176-280">Azure 클래식 포털을 사용하여 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-280">Use the Azure classic portal to identify the active controller</span></span>](#use-the-azure-classic-portal-to-identify-the-active-controller)
* [<span data-ttu-id="11176-281">StorSimple용 Windows PowerShell을 사용하여 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-281">Use Windows PowerShell for StorSimple to identify the active controller</span></span>](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [<span data-ttu-id="11176-282">물리적 장치를 검사하여 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-282">Check the physical device to identify the active controller</span></span>](#check-the-physical-device-to-identify-the-active-controller)

<span data-ttu-id="11176-283">아래에서는 이러한 각 절차에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-283">Each of these procedures is described next.</span></span>

### <a name="use-the-azure-classic-portal-to-identify-the-active-controller"></a><span data-ttu-id="11176-284">Azure 클래식 포털을 사용하여 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-284">Use the Azure classic portal to identify the active controller</span></span>
<span data-ttu-id="11176-285">Azure 클래식 포털에서 **장치** > **유지 관리**로 이동한 다음 **컨트롤러** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-285">In the Azure classic portal, navigate to **Devices** > **Maintenance**, and scroll to the **Controllers** section.</span></span> <span data-ttu-id="11176-286">여기서 활성 컨트롤러를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-286">Here you can verify which controller is active.</span></span>

![Azure 클래식 포털에서 활성 컨트롤러 식별](./media/storsimple-controller-replacement/IC752072.png)

<span data-ttu-id="11176-288">**그림 6** 활성 컨트롤러를 보여 주는 Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="11176-288">**Figure 6** Azure classic portal showing the active controller</span></span>

### <a name="use-windows-powershell-for-storsimple-to-identify-the-active-controller"></a><span data-ttu-id="11176-289">StorSimple용 Windows PowerShell을 사용하여 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-289">Use Windows PowerShell for StorSimple to identify the active controller</span></span>
<span data-ttu-id="11176-290">직렬 콘솔을 통해 장치에 액세스하는 경우 배너 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11176-290">When you access your device through the serial console, a banner message is presented.</span></span> <span data-ttu-id="11176-291">배너 메시지에는 모델, 이름, 설치된 소프트웨어 버전 및 액세스 중인 컨트롤러의 상태와 같은 기본 장치 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-291">The banner message contains basic device information such as the model, name, installed software version, and status of the controller you are accessing.</span></span> <span data-ttu-id="11176-292">다음 그림은 배너 메시지의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11176-292">The following image shows an example of a banner message:</span></span>

![직렬 배너 메시지](./media/storsimple-controller-replacement/IC741098.png)

<span data-ttu-id="11176-294">**그림 7** 컨트롤러 0을 활성으로 표시하는 배너 메시지</span><span class="sxs-lookup"><span data-stu-id="11176-294">**Figure 7** Banner message showing controller 0 as Active</span></span>

<span data-ttu-id="11176-295">배너 메시지를 사용하여 연결된 컨트롤러가 활성 또는 수동인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-295">You can use the banner message to determine whether the controller you are connected to is active or passive.</span></span>

### <a name="check-the-physical-device-to-identify-the-active-controller"></a><span data-ttu-id="11176-296">물리적 장치를 검사하여 활성 컨트롤러 식별</span><span class="sxs-lookup"><span data-stu-id="11176-296">Check the physical device to identify the active controller</span></span>
<span data-ttu-id="11176-297">장치의 활성 컨트롤러를 식별하려면 기본 엔클로저 뒷면에서 DATA 5 포트 위의 파란색 LED를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-297">To identify the active controller on your device, locate the blue LED above the DATA 5 port on the back of the primary enclosure.</span></span>

<span data-ttu-id="11176-298">이 LED가 깜박이면 컨트롤러가 활성 상태이며 다른 컨트롤러는 대기 모드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11176-298">If this LED is blinking, the controller is active and the other controller is in standby mode.</span></span> <span data-ttu-id="11176-299">다음 다이어그램과 표를 보조 도구로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11176-299">Use the following diagram and table as an aid.</span></span>

![데이터 포트가 있는 장치 기본 인클로저 백플레인](./media/storsimple-controller-replacement/IC741055.png)

<span data-ttu-id="11176-301">**그림 8** 데이터 포트와 모니터링 LED가 있는 기본 엔클로저 뒷면</span><span class="sxs-lookup"><span data-stu-id="11176-301">**Figure 8** Back of primary enclosure with data ports and monitoring LEDs</span></span>

| <span data-ttu-id="11176-302">레이블</span><span class="sxs-lookup"><span data-stu-id="11176-302">Label</span></span> | <span data-ttu-id="11176-303">설명</span><span class="sxs-lookup"><span data-stu-id="11176-303">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="11176-304">1-6</span><span class="sxs-lookup"><span data-stu-id="11176-304">1-6</span></span> |<span data-ttu-id="11176-305">DATA 0 - 5 네트워크 포트</span><span class="sxs-lookup"><span data-stu-id="11176-305">DATA 0 – 5 network ports</span></span> |
| <span data-ttu-id="11176-306">7</span><span class="sxs-lookup"><span data-stu-id="11176-306">7</span></span> |<span data-ttu-id="11176-307">파란색 LED</span><span class="sxs-lookup"><span data-stu-id="11176-307">Blue LED</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11176-308">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11176-308">Next steps</span></span>
<span data-ttu-id="11176-309">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11176-309">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

