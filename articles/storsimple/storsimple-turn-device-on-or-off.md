---
title: "StorSimple 8000 시리즈 장치 켜기 또는 끄기 | Microsoft Docs"
description: "새 StorSimple 장치를 켜고, 종료되었거나 전원이 손실된 장치를 켜고, 실행 중인 장치를 끄는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0577c837e0c47ba37a4f586603b0f5b951f1b549
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a><span data-ttu-id="f8ff1-103">StorSimple 8000 시리즈 장치 켜기 또는 끄기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-103">Turn on or turn off your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="f8ff1-104">개요</span><span class="sxs-lookup"><span data-stu-id="f8ff1-104">Overview</span></span>
<span data-ttu-id="f8ff1-105">Microsoft Azure StorSimple 장치 종료는 정상적인 시스템 작업의 일환으로 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-105">Shutting down a Microsoft Azure StorSimple device is not required as a part of normal system operation.</span></span> <span data-ttu-id="f8ff1-106">그러나 새 장치 또는 종료할 장치의 전원을 켜야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-106">However, you may need to turn on a new device or a device that had to be shut down.</span></span> <span data-ttu-id="f8ff1-107">일반적으로 오류가 발생한 하드웨어를 교체, 물리적으로 장치를 이동하거나 장치의 서비스를 중단해야 하는 경우 종료가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-107">Generally, a shutdown is required in cases in which you must replace failed hardware, physically move a unit, or take a device out of service.</span></span> <span data-ttu-id="f8ff1-108">이 자습서는 다양한 시나리오에서 StorSimple 장치를 켜고 종료하는데 필요한 절차에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-108">This tutorial describes the required procedure for turning on and shutting down your StorSimple device in different scenarios.</span></span>

## <a name="turn-on-a-new-device"></a><span data-ttu-id="f8ff1-109">새 장치 켜기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-109">Turn on a new device</span></span>
<span data-ttu-id="f8ff1-110">처음으로 StorSimple 장치를 켜는 단계는 장치가 8100인지 8600 모델인지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-110">The steps for turning on a StorSimple device for the first time differ depending on whether the device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="f8ff1-111">8100에는 단일 기본 엔클로저가 있는 반면 8600은 기본 엔클로저와 EBOD 엔클로저가 있는 이중 엔클로저 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-111">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="f8ff1-112">두 모델에 대한 자세한 단계는 다음 섹션에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-112">The detailed steps for both models are covered in the following sections.</span></span>

* [<span data-ttu-id="f8ff1-113">기본 인클로저만 있는 새 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-113">New device with primary enclosure only</span></span>](#new-device-with-primary-enclosure-only)
* [<span data-ttu-id="f8ff1-114">EBOD 인클로저가 있는 새 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-114">New device with EBOD enclosure</span></span>](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a><span data-ttu-id="f8ff1-115">기본 인클로저만 있는 새 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-115">New device with primary enclosure only</span></span>
<span data-ttu-id="f8ff1-116">StorSimple 8100 모델은 단일 인클로저 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-116">The StorSimple 8100 model is a single enclosure device.</span></span> <span data-ttu-id="f8ff1-117">장치에는 예비 전원 및 냉각 모듈(PCM)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-117">Your device includes redundant Power and Cooling Modules (PCMs).</span></span> <span data-ttu-id="f8ff1-118">두 PCM을 모두 설치하고 다른 전원 공급 장치에 연결하여 높은 가용성을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-118">Both PCMs must be installed and connected to different power sources to ensure high availability.</span></span>

<span data-ttu-id="f8ff1-119">다음 단계를 수행하여 케이블로 장치를 전원에 연결하세요.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-119">Perform the following steps to cable your device for power.</span></span>

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> <span data-ttu-id="f8ff1-120">장치 설정 완료 및 케이블 연결 지침은 [StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-120">For complete device setup and cabling instructions, go to [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md).</span></span> <span data-ttu-id="f8ff1-121">지침을 정확하게 따르고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-121">Make sure that you follow the instructions exactly.</span></span>
> 
> 

### <a name="new-device-with-ebod-enclosure"></a><span data-ttu-id="f8ff1-122">EBOD 인클로저가 있는 새 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-122">New device with EBOD enclosure</span></span>
<span data-ttu-id="f8ff1-123">StorSimple 8600 모델에는 기본 인클로저 및 EBOD 인클로저가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-123">The StorSimple 8600 model has both a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="f8ff1-124">장치를 Serial Attached SCSI(SAS) 연결 및 전원에 모두 케이블 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-124">This requires the units to be cabled together for Serial Attached SCSI (SAS) connectivity and power.</span></span>

<span data-ttu-id="f8ff1-125">처음으로 이 장치를 설정할 때 SAS 케이블 연결을 먼저 수행한 다음 전원 케이블 연결에 대한 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-125">When setting up this device for the first time, perform the steps for SAS cabling first and then complete the steps for power cabling.</span></span>

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> <span data-ttu-id="f8ff1-126">장치 설정 완료 및 케이블 연결 지침은 [StorSimple 8600 장치 설치](storsimple-8600-hardware-installation.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-126">For complete device setup and cabling instructions, go to [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span> <span data-ttu-id="f8ff1-127">지침을 정확하게 따르고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-127">Make sure that you follow the instructions exactly.</span></span>

## <a name="turn-on-a-device-after-shutdown"></a><span data-ttu-id="f8ff1-128">종료 후 장치 켜기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-128">Turn on a device after shutdown</span></span>
<span data-ttu-id="f8ff1-129">StorSimple 장치가 종료된 후에 켜는 단계는 장치가 8100인지 8600 모델인지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-129">The steps for turning on a StorSimple device after it has been shut down are different depending on whether the device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="f8ff1-130">8100에는 단일 기본 엔클로저가 있는 반면 8600은 기본 엔클로저와 EBOD 엔클로저가 있는 이중 엔클로저 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-130">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

* [<span data-ttu-id="f8ff1-131">기본 인클로저만 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-131">Device with primary enclosure only</span></span>](#device-with-primary-enclosure-only)
* [<span data-ttu-id="f8ff1-132">EBOD 인클로저가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-132">Device with EBOD enclosure</span></span>](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a><span data-ttu-id="f8ff1-133">기본 인클로저만 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-133">Device with primary enclosure only</span></span>
<span data-ttu-id="f8ff1-134">종료 후 기본 인클로저가 있고 EBOD 인클로저가 없는 StorSimple 장치를 켜려면 다음 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-134">After a shutdown, use the following procedure to turn on a StorSimple device with a primary enclosure and no EBOD enclosure.</span></span>

#### <a name="to-turn-on-a-device-with-a-primary-enclosure-only"></a><span data-ttu-id="f8ff1-135">기본 인클로저만 있는 장치 켜기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-135">To turn on a device with a primary enclosure only</span></span>
1. <span data-ttu-id="f8ff1-136">두 PCM(전원 및 냉각 모듈)의 전원 스위치가 OFF 위치에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-136">Make sure that the power switches on both Power and Cooling Modules (PCMs) are in the OFF position.</span></span> <span data-ttu-id="f8ff1-137">스위치가 OFF 위치에 없는 경우 OFF 위치로 밀고 표시등이 꺼질 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-137">If the switches are not in the OFF position, then flip them to the OFF position and wait for the lights to go off.</span></span>
2. <span data-ttu-id="f8ff1-138">양쪽 PCM 상의 전원 스위치를 ON 위치로 밀어 장치의 전원을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-138">Turn on the device by flipping the power switches on both PCMs to the ON position.</span></span> <span data-ttu-id="f8ff1-139">장치를 켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-139">The device should turn on.</span></span>
3. <span data-ttu-id="f8ff1-140">다음을 확인하여 장치가 완전히 켜졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-140">Check the following to verify that the device is fully on:</span></span>
   
   1. <span data-ttu-id="f8ff1-141">두 PCM 모듈의 OK LED가 녹색입니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-141">The OK LEDs on both PCM modules are green.</span></span>
   2. <span data-ttu-id="f8ff1-142">두 컨트롤러의 상태 LED가 녹색으로 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-142">The status LEDs on both controllers are solid green.</span></span>
   3. <span data-ttu-id="f8ff1-143">컨트롤러 중 하나의 파란색 LED가 깜박이는 것은 컨트롤러 활성화되어 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-143">The blue LED on one of the controllers is blinking, which indicates that the controller is active.</span></span>
      
      <span data-ttu-id="f8ff1-144">이러한 조건 중 하나라도 충족되지 않은 경우 장치가 정상이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-144">If any of these conditions are not met, then your device is not healthy.</span></span> <span data-ttu-id="f8ff1-145">[Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-145">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="device-with-ebod-enclosure"></a><span data-ttu-id="f8ff1-146">EBOD 인클로저가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-146">Device with EBOD enclosure</span></span>
<span data-ttu-id="f8ff1-147">종료 후 기본 인클로저와 EBOD 인클로저가 있는 StorSimple 장치를 켜려면 다음 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-147">After a shutdown, use the following procedure to turn on a StorSimple device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="f8ff1-148">설명한대로 정확하게 각 단계를 순서대로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-148">Perform each step in sequence exactly as described.</span></span> <span data-ttu-id="f8ff1-149">이렇게 하지 않으면 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-149">Failure to do so could result in data loss.</span></span>

#### <a name="to-turn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a><span data-ttu-id="f8ff1-150">기본 및 EBOD 인클로저가 있는 장치 켜기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-150">To turn on a device with a primary and an EBOD enclosure</span></span>
1. <span data-ttu-id="f8ff1-151">EBOD 인클로저가 기본 인클로저에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-151">Make sure that the EBOD enclosure is connected to the primary enclosure.</span></span> <span data-ttu-id="f8ff1-152">자세한 내용은 [StorSimple 8600 장치 설치](storsimple-8600-hardware-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-152">For more information, see [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="f8ff1-153">EBOD 및 기본 인클로저의 PCM(전원 및 냉각 모듈)이 OFF 위치에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-153">Make sure that the Power and Cooling Modules (PCMs) on both the EBOD and primary enclosures are in the OFF position.</span></span> <span data-ttu-id="f8ff1-154">스위치가 OFF 위치에 없는 경우 OFF 위치로 밀고 표시등이 꺼질 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-154">If the switches are not in the OFF position, then flip them to the OFF position and wait for the lights to go off.</span></span>
3. <span data-ttu-id="f8ff1-155">양쪽 PCM 상의 전원 스위치를 ON 위치로 밀어 EBOD 인클로저의 전원을 먼저 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-155">Turn on the EBOD enclosure first by flipping the power switches on both PCMs to the ON position.</span></span> <span data-ttu-id="f8ff1-156">PCM LED가 녹색이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-156">The PCM LEDs should be green.</span></span> <span data-ttu-id="f8ff1-157">이 장치의 녹색 EBOD 컨트롤러 LED는 EBOD 인클로저가 켜져 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-157">A green EBOD controller LED on this unit indicates that the EBOD enclosure is on.</span></span>
4. <span data-ttu-id="f8ff1-158">양쪽 PCM 상의 전원 스위치를 ON 위치로 밀어 기본 인클로저의 전원을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-158">Turn on the primary enclosure by flipping the power switches on both PCMs to the ON position.</span></span> <span data-ttu-id="f8ff1-159">이제 전체 시스템이 켜져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-159">The entire system should now be on.</span></span>
5. <span data-ttu-id="f8ff1-160">EBOD 인클로저 및 기본 인클로저 간의 연결이 좋은지를 나타내는 SAS LED가 녹색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-160">Verify that the SAS LEDs are green, which ensures that the connection between the EBOD enclosure and the primary enclosure is good.</span></span>

## <a name="turn-on-a-device-after-a-power-loss"></a><span data-ttu-id="f8ff1-161">전원 손실 후 장치 켜기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-161">Turn on a device after a power loss</span></span>
<span data-ttu-id="f8ff1-162">정전 또는 전원 중단으로 StorSimple 장치가 종료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-162">A power outage or interruption can shut down a StorSimple device.</span></span> <span data-ttu-id="f8ff1-163">전원 공급 장치 중 하나 또는 두 전원 공급 장치에서 정전이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-163">The power outage can happen on one of the power supplies or both power supplies.</span></span> <span data-ttu-id="f8ff1-164">복구 단계는 장치가 8100 또는 8600 모델인지 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-164">The recovery steps are different depending on whether the device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="f8ff1-165">8100에는 단일 기본 엔클로저가 있는 반면 8600은 기본 엔클로저와 EBOD 엔클로저가 있는 이중 엔클로저 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-165">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="f8ff1-166">이 섹션에서는 각 시나리오에 대한 복구 절차를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-166">This section describes the recovery procedure for each scenario.</span></span>

* [<span data-ttu-id="f8ff1-167">기본 인클로저만 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-167">Device with primary enclosure only</span></span>](#8100)
* [<span data-ttu-id="f8ff1-168">EBOD 인클로저가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-168">Device with EBOD enclosure</span></span>](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a><span data-ttu-id="f8ff1-169">기본 인클로저만 있는 장치 <a name="8100"></span><span class="sxs-lookup"><span data-stu-id="f8ff1-169">Device with primary enclosure only <a name="8100"></span></span>
<span data-ttu-id="f8ff1-170">전원 공급 장치 중 하나에 전원 손실이 발생하는 경우 시스템은 일반적인 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-170">The system can continue its normal operation if there is power loss to one of its power supplies.</span></span> <span data-ttu-id="f8ff1-171">하지만 장치의 고가용성을 보장하려면 가능한 빨리 전원 공급 장치에 전원을 복원하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-171">However, to ensure high availability of the device, restore power to the power supply as soon as possible.</span></span>

<span data-ttu-id="f8ff1-172">전원 공급 장치 모두에서 정전 또는 전원 중단이 있는 경우 시스템이 순차적이고 제어된 방식으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-172">If there is a power outage or power interruption on both power supplies, the system will shut down in an orderly and controlled manner.</span></span> <span data-ttu-id="f8ff1-173">전원이 복원되면 시스템이 자동으로 켜집니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-173">When the power is restored, the system will automatically turn on.</span></span>

### <a name="device-with-ebod-enclosure-a-name8600"></a><span data-ttu-id="f8ff1-174">EBOD 인클로저가 있는 장치 <a name="8600"></span><span class="sxs-lookup"><span data-stu-id="f8ff1-174">Device with EBOD enclosure <a name="8600"></span></span>
#### <a name="power-loss-on-one-power-supply"></a><span data-ttu-id="f8ff1-175">하나의 전원 공급 장치에서 전원 손실</span><span class="sxs-lookup"><span data-stu-id="f8ff1-175">Power loss on one power supply</span></span>
<span data-ttu-id="f8ff1-176">기본 인클로저 또는 EBOD 인클로저의 전원 공급 장치 중 하나에 전원 손실이 발생하는 경우 시스템은 일반적인 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-176">The system can continue its normal operation if there is power loss to one of its power supplies on the primary enclosure or the EBOD enclosure.</span></span> <span data-ttu-id="f8ff1-177">하지만 장치의 고가용성을 보장하려면 가능한 빨리 전원 공급 장치에 전원을 복원하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-177">However, to ensure high availability of the device, please restore power to the power supply as soon as possible.</span></span>

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a><span data-ttu-id="f8ff1-178">기본 및 EBOD 인클로저의 두 전원 공급 장치에서 전원 손실</span><span class="sxs-lookup"><span data-stu-id="f8ff1-178">Power loss on both power supplies on primary and EBOD enclosures</span></span>
<span data-ttu-id="f8ff1-179">전원 공급 장치 모두에서 정전 또는 전원 중단이 있는 경우 EBOD 인클로저는 즉시 종료되고 기본 인클로저는 순차적이고 제어된 방식으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-179">If there is a power outage or power interruption on both power supplies, the EBOD enclosure will shut down immediately and the primary enclosure will shut down in an orderly and controlled manner.</span></span> <span data-ttu-id="f8ff1-180">전원이 복원되면 기기가 자동으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-180">When power is restored, the appliance will start automatically.</span></span>

<span data-ttu-id="f8ff1-181">전원이 수동으로 꺼진 경우 다음 단계를 따라 시스템의 전원을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-181">If the power is switched off manually, then take the following steps to restore power to the system.</span></span>

1. <span data-ttu-id="f8ff1-182">EBOD 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-182">Turn on the EBOD enclosure.</span></span>
2. <span data-ttu-id="f8ff1-183">EBOD 인클로저의 전원이 켜진 후 기본 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-183">After the EBOD enclosure is on, turn on the primary enclosure.</span></span>

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a><span data-ttu-id="f8ff1-184">EBOD 인클로저의 두 전원 공급 장치에서 전원 손실</span><span class="sxs-lookup"><span data-stu-id="f8ff1-184">Power loss on both power supplies on EBOD enclosure</span></span>
<span data-ttu-id="f8ff1-185">케이블을 설정할 때 EBOD가 별도 PDU에 단독 연결되지 않도록 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-185">When you set up your cables, you must ensure that the EBOD is never connected alone to a separate PDU.</span></span> <span data-ttu-id="f8ff1-186">EBOD 및 기본 인클로저가 동시에 실패하는 경우 시스템이 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-186">If the EBOD and primary enclosure fail at the same time, the system will recover.</span></span>

<span data-ttu-id="f8ff1-187">EBOD 인클로저의 두 전원 공급 장치가 실패한 경우 시스템이 자동으로 복구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-187">If only the EBOD enclosure fails on both power supplies, the system will not automatically recover.</span></span> <span data-ttu-id="f8ff1-188">다음 단계를 수행하여 시스템의 전원을 켜고 정상 상태로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-188">Take the following steps to turn on the system and restore it to a healthy state:</span></span>

1. <span data-ttu-id="f8ff1-189">기본 인클로저가 켜져 있는 경우 두 PCM(전원 및 냉각 모듈)을 모두 끕니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-189">If the primary enclosure is turned on, switch off both Power and Cooling Modules (PCMs).</span></span>
2. <span data-ttu-id="f8ff1-190">시스템이 종료될 때까지 몇 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-190">Wait for a few minutes for the system to shut down.</span></span>
3. <span data-ttu-id="f8ff1-191">EBOD 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-191">Turn on the EBOD enclosure.</span></span>
4. <span data-ttu-id="f8ff1-192">EBOD 인클로저의 전원이 켜진 후 기본 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-192">After the EBOD enclosure is on, turn on the primary enclosure.</span></span>

## <a name="turn-on-a-device-after-the-primary-and-ebod-enclosure-connection-is-lost"></a><span data-ttu-id="f8ff1-193">기본 및 EBOD 인클로저 연결 손실 후 장치 켜기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-193">Turn on a device after the primary and EBOD enclosure connection is lost</span></span>
<span data-ttu-id="f8ff1-194">대기 컨트롤러와 해당 EBOD 컨트롤러 간의 연결이 끊어진 경우 장치가 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-194">If the connection is lost between the standby controller and the corresponding EBOD controller, the device continues to work.</span></span> <span data-ttu-id="f8ff1-195">시스템 활성 컨트롤러와 해당 EBOD 컨트롤러 간의 연결이 끊어진 경우 장애 조치가 발생해야 하며 장치는 계속 정상적으로 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-195">If the connection between the system active controller and the corresponding EBOD controller is lost, failover should occur and the device should continue to work as normal.</span></span>

<span data-ttu-id="f8ff1-196">두 SAS(Serial Attached SCSI) 케이블이 제거되거나 EBOD 인클로저와 기본 인클로저 간의 연결이 단절되는 경우 장치의 작동이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-196">When both Serial Attached SCSI (SAS) cables are removed or the connection between the EBOD enclosure and the primary enclosure is severed, the device will stop working.</span></span> <span data-ttu-id="f8ff1-197">이때 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-197">At this point, perform the following steps.</span></span>

### <a name="to-turn-on-the-device-after-connection-is-lost"></a><span data-ttu-id="f8ff1-198">연결이 끊어진 후 장치를 켜려면</span><span class="sxs-lookup"><span data-stu-id="f8ff1-198">To turn on the device after connection is lost</span></span>
1. <span data-ttu-id="f8ff1-199">장치의 뒷면에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-199">Access the back of the device.</span></span>
2. <span data-ttu-id="f8ff1-200">EBOD 인클로저와 기본 인클로저 간의 SAS 케이블 연결이 중단되는 경우 EBOD 인클로저의 모든 SAS 레인 LED가 꺼집니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-200">If the SAS cable connection between the EBOD enclosure and the primary enclosure is broken, all SAS lane LEDs on the EBOD enclosure will be off.</span></span>
3. <span data-ttu-id="f8ff1-201">EBOD 인클로저 및 기본 인클로저의 두 PCM(전원 및 냉각 모듈)을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-201">Shut down both Power and Cooling Modules (PCMs) on the EBOD enclosure and the primary enclosure.</span></span>
4. <span data-ttu-id="f8ff1-202">두 인클로저의 뒷면에 있는 모든 표시등이 꺼질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-202">Wait until all the lights on the back of both the enclosures turn off.</span></span>
5. <span data-ttu-id="f8ff1-203">SAS 케이블을 다시 삽입하고 EBOD 인클로저와 기본 인클로저 간의 연결이 양호한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-203">Reinsert the SAS cables, and ensure that there is a good connection between the EBOD enclosure and the primary enclosure.</span></span>
6. <span data-ttu-id="f8ff1-204">두 PCM 스위치를 ON 위치로 밀어 EBOD 인클로저의 전원을 먼저 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-204">Turn on the EBOD enclosure first by flipping both PCM switches to the ON position.</span></span>
7. <span data-ttu-id="f8ff1-205">녹색 LED가 ON인지 확인하여 EBOD 인클로저가 켜졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-205">Ensure that the EBOD enclosure is on by checking that the green LED is ON.</span></span>
8. <span data-ttu-id="f8ff1-206">기본 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-206">Turn on the primary enclosure.</span></span>
9. <span data-ttu-id="f8ff1-207">컨트롤러 녹색 LED가 ON인지 확인하여 기본 인클로저가 켜졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-207">Ensure that the primary enclosure is on by checking that the controller green LED is ON.</span></span>
10. <span data-ttu-id="f8ff1-208">SAS 레인 LED(EBOD 컨트롤러당 4개)가 모두 ON인지 확인하여 EBOD 인클로저와 기본 인클로저의 연결이 양호한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-208">Verify that the EBOD enclosure connection with the primary enclosure is good by checking that the SAS lane LEDs (four per EBOD controller) are all ON.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8ff1-209">SAS 케이블이 결함이 있거나 EBOD 인클로저와 기본 인클로저 간의 연결이 좋지 않은 경우 시스템을 켜면 복구 모드로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-209">If the SAS cables are defective or the connection between the EBOD enclosure and the primary enclosure is not good, when you turn on the system, it will go into recovery mode.</span></span> <span data-ttu-id="f8ff1-210">이 경우 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-210">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) if this happens.</span></span>


## <a name="turn-off-a-running-device"></a><span data-ttu-id="f8ff1-211">실행 중인 장치 끄기</span><span class="sxs-lookup"><span data-stu-id="f8ff1-211">Turn off a running device</span></span>
<span data-ttu-id="f8ff1-212">실행 중인 StorSimple 장치를 이동 중이거나 서비스를 받지 못하거나 교체가 필요한 오작동하는 구성 요소가 있는 경우 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-212">A running StorSimple device may need to be shut down if it is being moved, taken out of service, or has a malfunctioning component that needs to be replaced.</span></span> <span data-ttu-id="f8ff1-213">단계는 StorSimple 장치가 8100 또는 8600 모델인지 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-213">The steps are different depending on whether the StorSimple device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="f8ff1-214">8100에는 단일 기본 엔클로저가 있는 반면 8600은 기본 엔클로저와 EBOD 엔클로저가 있는 이중 엔클로저 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-214">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="f8ff1-215">이 섹션에서는 실행 중인 장치를 종료하는 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-215">This section details the steps to shut down a running device.</span></span>

* [<span data-ttu-id="f8ff1-216">기본 인클로저가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-216">Device with primary enclosure</span></span>](#8100a)
* [<span data-ttu-id="f8ff1-217">EBOD 인클로저가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="f8ff1-217">Device with EBOD enclosure</span></span>](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a><span data-ttu-id="f8ff1-218">기본 인클로저가 있는 장치 <a name="8100a"></span><span class="sxs-lookup"><span data-stu-id="f8ff1-218">Device with primary enclosure <a name="8100a"></span></span>
<span data-ttu-id="f8ff1-219">제어된 방식으로 올바른 순서에 따라 장치를 종료하려는 경우 Azure 클래식 포털 또는 StorSimple용 Windows PowerShell을 통해 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-219">To shut down the device in an orderly and controlled manner, you can do it through the Azure classic portal or via the Windows PowerShell for StorSimple.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f8ff1-220">장치 뒷면의 전원 단추를 사용하여 실행 중인 장치를 종료하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-220">Do not shut down a running device by using the power button on the back of the device.</span></span>
> 
> <span data-ttu-id="f8ff1-221">장치를 종료하기 전에 모든 장치 구성 요소가 올바르게 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-221">Before shutting down the device, make sure that all the device components are healthy.</span></span> <span data-ttu-id="f8ff1-222">Azure 클래식 포털에서 **장치** > **유지 관리** > **하드웨어 상태**로 이동한 다음, 모든 구성 요소의 상태가 녹색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-222">In the Azure classic portal, navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that status of all the components is green.</span></span> <span data-ttu-id="f8ff1-223">양호한 시스템에 대해서만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-223">This is true only for a healthy system.</span></span> <span data-ttu-id="f8ff1-224">시스템이 종료되어 작동하지 않는 구성 요소를 교체하는 경우 **하드웨어 상태**의 해당 구성 요소에 실패(빨간색) 또는 성능 저하(노란색) 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-224">If the system is being shut down to replace a malfunctioning component, you will see a failed (red) or degraded (yellow) status for the respective component in the **Hardware Status**.</span></span>
> 
> 

<span data-ttu-id="f8ff1-225">StorSimple용 Windows PowerShell 또는 Azure 클래식 포털에 액세스한 후 [StorSimple 장치 종료](storsimple-manage-device-controller.md#shut-down-a-storsimple-device)의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-225">After you access the Windows PowerShell for StorSimple or the Azure classic portal, follow the steps in [shut down a StorSimple device](storsimple-manage-device-controller.md#shut-down-a-storsimple-device).</span></span> 

### <a name="device-with-ebod-enclosure-a-name8600a"></a><span data-ttu-id="f8ff1-226">EBOD 인클로저가 있는 장치 <a name="8600a"></span><span class="sxs-lookup"><span data-stu-id="f8ff1-226">Device with EBOD enclosure <a name="8600a"></span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8ff1-227">기본 인클로저 및 EBOD 인클로저를 종료 기 전에 모든 장치 구성 요소가 정상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-227">Before shutting down the primary enclosure and the EBOD enclosure, ensure that all the device components are healthy.</span></span> <span data-ttu-id="f8ff1-228">Azure Portal에서 **장치** > **모니터** > **하드웨어 상태**로 이동한 다음, 모든 구성 요소의 상태가 정상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-228">In the Azure portal, navigate to **Devices** > **Monitor** > **Hardware health**, and verify that all the components are healthy.</span></span>


#### <a name="to-shut-down-a-running-device-with-ebod-enclosure"></a><span data-ttu-id="f8ff1-229">EBOD 인클로저가 있는 실행 중인 장치를 종료하려면</span><span class="sxs-lookup"><span data-stu-id="f8ff1-229">To shut down a running device with EBOD enclosure</span></span>
1. <span data-ttu-id="f8ff1-230">기본 엔클로저에 대해 [StorSimple 장치 종료](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) 에 나와 있는 모든 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-230">Follow all the steps listed in [shut down a StorSimple device](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) for the primary enclosure.</span></span>
2. <span data-ttu-id="f8ff1-231">기본 인클로저가 종료된 후 두 PCM(전원 및 냉각 모듈) 스위치를 꺼 EBOD를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-231">After the primary enclosure is shut down, shut down the EBOD by flipping off both Power and Cooling Module (PCM) switches.</span></span>
3. <span data-ttu-id="f8ff1-232">EBOD가 종료되었는지 확인하려면 EBOD 인클로저의 뒷면에 있는 모든 표시등이 꺼졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-232">To verify that the EBOD has shut down, check that all lights on the back of the EBOD enclosure are off.</span></span>

> [!NOTE]
> <span data-ttu-id="f8ff1-233">EBOD 인클로저를 기본 인클로저에 연결하는데 사용되는 SAS 케이블을 시스템이 종료된 후까지 제거하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-233">The SAS cables that are used to connect the EBOD enclosure to the primary enclosure should not be removed until after the system is shut down.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8ff1-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8ff1-234">Next steps</span></span>
<span data-ttu-id="f8ff1-235">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8ff1-235">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) if you encounter problems when turning on or shutting down a StorSimple device.</span></span>

