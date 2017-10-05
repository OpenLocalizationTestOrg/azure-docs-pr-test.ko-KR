---
title: "StorSimple 8000 시리즈 장치의 PCM 교체 | Microsoft Docs"
description: "StorSimple 장치의 PCM(전원 및 냉각 모듈)을 꺼내고 교체하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 7d181e6e434c998573dbea4b541cfacf7a28ee66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="12c59-103">StorSimple 장치의 전원 및 냉각 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="12c59-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="12c59-104">개요</span><span class="sxs-lookup"><span data-stu-id="12c59-104">Overview</span></span>
<span data-ttu-id="12c59-105">Microsoft Azure StorSimple 장치의 PCM(전원 및 냉각 모듈)은 기본 및 EBOD 엔클로저를 통해 제어되는 전원 공급 장치 및 냉각 팬으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="12c59-106">각 엔클로저마다 인증된 PCM 모델 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="12c59-107">기본 엔클로저는 764W PCM에 대해 인증되고 EBOD 엔클로저는 580W PCM에 대해 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="12c59-108">기본 엔클로저와 EBOD 엔클로저의 PCM은 서로 다르지만 교체 절차는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="12c59-109">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="12c59-110">PCM 꺼내기</span><span class="sxs-lookup"><span data-stu-id="12c59-110">Remove a PCM</span></span>
* <span data-ttu-id="12c59-111">교체 PCM 설치</span><span class="sxs-lookup"><span data-stu-id="12c59-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12c59-112">PCM을 꺼내고 교체하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에서 안전 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="12c59-113">PCM을 교체하기 전에</span><span class="sxs-lookup"><span data-stu-id="12c59-113">Before you replace a PCM</span></span>
<span data-ttu-id="12c59-114">PCM을 교체하기 전에 다음과 같은 중요한 문제에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="12c59-115">PCM의 전원 공급 장치에서 오류가 발생할 경우 결함이 있는 모듈을 설치된 상태로 두고 전원 코드를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="12c59-116">팬이 엔클로저에서 계속 전원을 받고 적절한 냉각을 계속 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="12c59-117">팬에서 오류가 발생할 경우 PCM을 즉시 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="12c59-118">PCM을 꺼내기 전에 주 스위치(있는 경우)를 끄거나 전원 코드를 물리적으로 분리하여 PCM에서 전원을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="12c59-119">전원이 곧 종료된다는 경고가 시스템에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="12c59-120">결함이 있는 PCM을 교체하기 전에 지속적인 시스템 작동을 위해 다른 PCM이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="12c59-121">가능한 한 빨리 결함이 있는 PCM을 완벽하게 작동하는 PCM으로 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="12c59-122">PCM 모듈 교체를 완료하는 데 몇 분밖에 걸리지 않지만 과열을 방지하기 위해 오류가 발생한 PCM을 꺼내고 10분 내에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="12c59-123">공장에서 출고된 교체 764 W PCM 모듈에는 백업 배터리 모듈이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="12c59-124">교체하기 전에 결함이 있는 PCM에서 배터리를 제거하고 교체 모듈에 이를 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="12c59-125">자세한 내용은 [백업 배터리 모듈 제거 및 삽입](storsimple-8000-battery-replacement.md)방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-125">For more information, see how to [remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="12c59-126">PCM 꺼내기</span><span class="sxs-lookup"><span data-stu-id="12c59-126">Remove a PCM</span></span>
<span data-ttu-id="12c59-127">Microsoft Azure StorSimple 장치에서 PCM(전원 및 냉각 모듈)을 꺼낼 준비가 되면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="12c59-128">PCM을 꺼내기 전에 올바른 교체(기본 엔클로저의 경우 764W, EBOD 엔클로저의 경우 580W)가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="12c59-129">PCM을 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="12c59-129">To remove a PCM</span></span>
1. <span data-ttu-id="12c59-130">Azure 클래식 포털에서 **설정 > 모니터 > 하드웨어 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-130">In the Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="12c59-131">**공유 구성 요소** 아래에서 PCM 구성 요소의 상태를 확인하여 오류가 발생한 PCM을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-131">Check the status of the PCM components under **Shared components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="12c59-132">PCM 0의 전원 공급 장치에서 오류가 발생한 경우 **PCM 0의 전원 공급 장치** 상태가 빨강으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="12c59-133">PCM 1의 전원 공급 장치에서 오류가 발생한 경우 **PCM 1의 전원 공급 장치** 상태가 빨강으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="12c59-134">PCM 1의 팬에서 오류가 발생한 경우 **PCM 0의 냉각 0** 또는 **PCM 0의 냉각 1** 상태가 빨강으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="12c59-135">기본 엔클로저 뒷면에서 오류가 발생한 PCM을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="12c59-136">8600 모델을 실행하는 경우 전면 패널 LED 디스플레이에 표시된 시스템 장치 식별 번호를 확인하여 기본 엔클로저를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="12c59-137">기본 엔클로저에 표시되는 기본 장치 ID는 **00**인 반면, EBOD 엔클로저에 표시되는 기본 장치 ID는 **01**입니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="12c59-138">다음 다이어그램과 표에서는 LED 디스플레이의 전면 패널에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![전면 OPS 패널의 시스템 ID](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="12c59-140">**그림 1** 장치의 전면 패널</span><span class="sxs-lookup"><span data-stu-id="12c59-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="12c59-141">레이블</span><span class="sxs-lookup"><span data-stu-id="12c59-141">Label</span></span> | <span data-ttu-id="12c59-142">설명</span><span class="sxs-lookup"><span data-stu-id="12c59-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="12c59-143">1</span><span class="sxs-lookup"><span data-stu-id="12c59-143">1</span></span> |<span data-ttu-id="12c59-144">음소거 단추</span><span class="sxs-lookup"><span data-stu-id="12c59-144">Mute button</span></span> |
   | <span data-ttu-id="12c59-145">2</span><span class="sxs-lookup"><span data-stu-id="12c59-145">2</span></span> |<span data-ttu-id="12c59-146">시스템 전원</span><span class="sxs-lookup"><span data-stu-id="12c59-146">System power</span></span> |
   | <span data-ttu-id="12c59-147">3</span><span class="sxs-lookup"><span data-stu-id="12c59-147">3</span></span> |<span data-ttu-id="12c59-148">모듈 결함</span><span class="sxs-lookup"><span data-stu-id="12c59-148">Module fault</span></span> |
   | <span data-ttu-id="12c59-149">4</span><span class="sxs-lookup"><span data-stu-id="12c59-149">4</span></span> |<span data-ttu-id="12c59-150">논리적 결함</span><span class="sxs-lookup"><span data-stu-id="12c59-150">Logical fault</span></span> |
   | <span data-ttu-id="12c59-151">5</span><span class="sxs-lookup"><span data-stu-id="12c59-151">5</span></span> |<span data-ttu-id="12c59-152">장치 ID 디스플레이</span><span class="sxs-lookup"><span data-stu-id="12c59-152">Unit ID display</span></span> |
3. <span data-ttu-id="12c59-153">기본 엔클로저 뒷면의 모니터링 표시기 LED를 사용하여 결함이 있는 PCM을 식별할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="12c59-154">LED를 사용하여 결함이 있는 PCM을 찾는 방법을 이해하려면 다음 다이어그램과 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="12c59-155">예를 들어 **팬 오류** 에 해당하는 LED가 켜지면 팬에서 오류가 발생한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="12c59-156">마찬가지로, **AC 오류** 에 해당하는 LED가 켜지면 전원 공급 장치에서 오류가 발생한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="12c59-158">**그림 2** 표시기 LED가 있는 PCM 뒷면</span><span class="sxs-lookup"><span data-stu-id="12c59-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="12c59-159">레이블</span><span class="sxs-lookup"><span data-stu-id="12c59-159">Label</span></span> | <span data-ttu-id="12c59-160">설명</span><span class="sxs-lookup"><span data-stu-id="12c59-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="12c59-161">1</span><span class="sxs-lookup"><span data-stu-id="12c59-161">1</span></span> |<span data-ttu-id="12c59-162">AC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="12c59-162">AC power failure</span></span> |
   | <span data-ttu-id="12c59-163">2</span><span class="sxs-lookup"><span data-stu-id="12c59-163">2</span></span> |<span data-ttu-id="12c59-164">팬 오류</span><span class="sxs-lookup"><span data-stu-id="12c59-164">Fan failure</span></span> |
   | <span data-ttu-id="12c59-165">3</span><span class="sxs-lookup"><span data-stu-id="12c59-165">3</span></span> |<span data-ttu-id="12c59-166">배터리 결함</span><span class="sxs-lookup"><span data-stu-id="12c59-166">Battery fault</span></span> |
   | <span data-ttu-id="12c59-167">4</span><span class="sxs-lookup"><span data-stu-id="12c59-167">4</span></span> |<span data-ttu-id="12c59-168">PCM 정상</span><span class="sxs-lookup"><span data-stu-id="12c59-168">PCM OK</span></span> |
   | <span data-ttu-id="12c59-169">5</span><span class="sxs-lookup"><span data-stu-id="12c59-169">5</span></span> |<span data-ttu-id="12c59-170">DC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="12c59-170">DC power failure</span></span> |
   | <span data-ttu-id="12c59-171">6</span><span class="sxs-lookup"><span data-stu-id="12c59-171">6</span></span> |<span data-ttu-id="12c59-172">배터리 정상</span><span class="sxs-lookup"><span data-stu-id="12c59-172">Battery healthy</span></span> |
4. <span data-ttu-id="12c59-173">StorSimple 장치 뒷면의 다음 다이어그램을 참조하여 오류가 발생한 PCM 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="12c59-174">PCM 0은 왼쪽에 있고 PCM 1은 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="12c59-175">뒤에 나오는 표에서는 모듈에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-175">The table that follows explains the modules.</span></span>
   
     ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="12c59-177">**그림 3** 플러그 인 모듈이 있는 장치 뒷면</span><span class="sxs-lookup"><span data-stu-id="12c59-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="12c59-178">레이블</span><span class="sxs-lookup"><span data-stu-id="12c59-178">Label</span></span> | <span data-ttu-id="12c59-179">설명</span><span class="sxs-lookup"><span data-stu-id="12c59-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="12c59-180">1</span><span class="sxs-lookup"><span data-stu-id="12c59-180">1</span></span> |<span data-ttu-id="12c59-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="12c59-181">PCM 0</span></span> |
   | <span data-ttu-id="12c59-182">2</span><span class="sxs-lookup"><span data-stu-id="12c59-182">2</span></span> |<span data-ttu-id="12c59-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="12c59-183">PCM 1</span></span> |
   | <span data-ttu-id="12c59-184">3</span><span class="sxs-lookup"><span data-stu-id="12c59-184">3</span></span> |<span data-ttu-id="12c59-185">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="12c59-185">Controller 0</span></span> |
   | <span data-ttu-id="12c59-186">4</span><span class="sxs-lookup"><span data-stu-id="12c59-186">4</span></span> |<span data-ttu-id="12c59-187">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="12c59-187">Controller 1</span></span> |
5. <span data-ttu-id="12c59-188">결함이 있는 PCM을 끄고 전원 공급 장치 코드를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="12c59-189">이제 PCM을 꺼낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="12c59-190">엄지와 집게 손가락으로 PCM 핸들의 래치와 측면을 잡고 눌러서 핸들을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![PCM 핸들 열기](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="12c59-192">**그림 4** PCM 핸들 열기</span><span class="sxs-lookup"><span data-stu-id="12c59-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="12c59-193">핸들을 잡고 PCM을 꺼냅니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-193">Grip the handle and remove the PCM.</span></span>
   
    ![장치 PCM 꺼내기](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="12c59-195">**그림 5** PCM 꺼내기</span><span class="sxs-lookup"><span data-stu-id="12c59-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="12c59-196">교체 PCM 설치</span><span class="sxs-lookup"><span data-stu-id="12c59-196">Install a replacement PCM</span></span>
<span data-ttu-id="12c59-197">StorSimple 장치에 PCM을 설치하려면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="12c59-198">교체 PCM을 설치하기 전에 백업 배터리 모듈을 삽입했는지 확인합니다(764 W PCM에만 적용).</span><span class="sxs-lookup"><span data-stu-id="12c59-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="12c59-199">자세한 내용은 [백업 배터리 모듈 제거 및 삽입](storsimple-8000-battery-replacement.md)방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c59-199">For more information, see how to [remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="12c59-200">PCM을 설치하려면</span><span class="sxs-lookup"><span data-stu-id="12c59-200">To install a PCM</span></span>
1. <span data-ttu-id="12c59-201">이 엔클로저에 적합한 교체 PCM이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="12c59-202">기본 엔클로저에는 764W PCM이 필요하고 EBOD 엔클로저에는 580W PCM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="12c59-203">기본 엔클로저에 580W PCM을 사용하거나 EBOD 엔클로저에 764W PCM을 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="12c59-204">다음 그림은 PCM에 부착된 레이블에서 이 정보를 식별할 수 있는 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![장치 PCM 레이블](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="12c59-206">**그림 6** PCM 레이블</span><span class="sxs-lookup"><span data-stu-id="12c59-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="12c59-207">커넥터에 특히 주의해서 엔클로저에 손상된 부분이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="12c59-208">**커넥터 핀이 구부러진 경우 모듈을 설치하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="12c59-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="12c59-209">PCM 핸들을 열린 위치에 놓고 모듈을 엔클로저에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![장치 PCM 설치](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="12c59-211">**그림 7** PCM 설치</span><span class="sxs-lookup"><span data-stu-id="12c59-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="12c59-212">수동으로 PCM 핸들을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-212">Manually close the PCM handle.</span></span> <span data-ttu-id="12c59-213">핸들 래치가 걸리면 딸깍하는 소리가 들립니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-213">You should hear a click as the handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12c59-214">커넥터 핀이 걸리도록 래치를 해제하지 않고 핸들을 부드럽게 잡아당길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="12c59-215">PCM이 밖으로 밀리면 커넥터가 걸리기 전에 래치가 닫힌 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   
5. <span data-ttu-id="12c59-216">전원과 PCM에 전원 케이블을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="12c59-217">변형 방지 묶음을 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-217">Secure the strain relief bales.</span></span>
7. <span data-ttu-id="12c59-218">PCM을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="12c59-219">교체에 성공했는지 확인합니다. StorSimple 장치 관리자 서비스의 Azure Portal에서 장치로 이동한 후 **설정 > 모니터 > 하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-219">Verify that the replacement was successful: in the Azure portal of your StorSimple Device Manager service, navigate to your device and then to **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="12c59-220">**공유 구성 요소** 아래에서 PCM 상태가 녹색이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-220">Under the **Shared components**, the status of the PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12c59-221">교체 PCM이 완전히 초기화되는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c59-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12c59-222">Next steps</span></span>
<span data-ttu-id="12c59-223">[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c59-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

