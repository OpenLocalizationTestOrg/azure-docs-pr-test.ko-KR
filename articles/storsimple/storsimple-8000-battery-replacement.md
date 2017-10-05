---
title: "Microsoft Azure StorSimple 8000 시리즈 장치의 배터리 교체 | Microsoft Docs"
description: "StorSimple 장치의 백업 배터리 모듈을 꺼내고 교체 및 유지 관리하는 방법을 설명합니다."
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 174a3163082594ea6a49b7f5a78857848f8f0566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="abede-103">StorSimple 장치의 백업 배터리 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="abede-103">Replace the backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="abede-104">개요</span><span class="sxs-lookup"><span data-stu-id="abede-104">Overview</span></span>
<span data-ttu-id="abede-105">Microsoft Azure StorSimple 장치의 기본 엔클로저 PCM(전원 및 냉각 모듈)에는 추가 배터리 팩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="abede-106">이 팩은 기본 엔클로저에 대한 AC 전원이 끊어질 경우 StorSimple 장치가 데이터를 저장할 수 있도록 전원을 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="abede-107">이 배터리 팩을 *백업 배터리 모듈*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="abede-108">백업 배터리 모듈은 StorSimple 장치의 기본 엔클로저에만 있습니다(EBOD 엔클로저에는 백업 배터리 모듈이 없음).</span><span class="sxs-lookup"><span data-stu-id="abede-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="abede-109">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="abede-110">백업 배터리 모듈 꺼내기</span><span class="sxs-lookup"><span data-stu-id="abede-110">Remove the backup battery module</span></span>
* <span data-ttu-id="abede-111">새 백업 배터리 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="abede-111">Install a new backup battery module</span></span>
* <span data-ttu-id="abede-112">백업 배터리 모듈 유지 관리</span><span class="sxs-lookup"><span data-stu-id="abede-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abede-113">백업 배터리 모듈을 꺼내고 교체하기 전에 [StorSimple 하드웨어 구성 요소 교체 소개](storsimple-8000-hardware-component-replacement.md)에서 안전 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="abede-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="abede-114">백업 배터리 모듈 꺼내기</span><span class="sxs-lookup"><span data-stu-id="abede-114">Remove the backup battery module</span></span>
<span data-ttu-id="abede-115">StorSimple 장치에 대한 백업 배터리 모듈은 FRU(현장 교체 장치)입니다.</span><span class="sxs-lookup"><span data-stu-id="abede-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="abede-116">PCM에 설치하기 전에는 원래 포장 안에 배터리 모듈을 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="abede-117">백업 배터리를 꺼내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="abede-118">백업 배터리 모듈을 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="abede-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="abede-119">Azure Portal에서 StorSimple 장치 관리자 서비스 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-119">In the Azure portal, go to your StorSimple Device Manager service blade.</span></span> <span data-ttu-id="abede-120">**장치**로 이동한 후 장치 목록에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-120">Go to **Devices** and then select your device from the list of devices.</span></span> <span data-ttu-id="abede-121">**모니터** > **하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-121">Navigate to **Monitor** > **Hardware health**.</span></span> <span data-ttu-id="abede-122">**공유 구성 요소**아래에서 배터리 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-122">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="abede-123">배터리에서 오류가 발생한 PCM을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-123">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="abede-124">그림 1은 StorSimple 장치의 뒷면의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abede-124">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="abede-126">**그림 1** PCM 및 컨트롤러 모듈을 표시하는 기본 장치 뒷면</span><span class="sxs-lookup"><span data-stu-id="abede-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="abede-127">레이블</span><span class="sxs-lookup"><span data-stu-id="abede-127">Label</span></span> | <span data-ttu-id="abede-128">설명</span><span class="sxs-lookup"><span data-stu-id="abede-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="abede-129">1</span><span class="sxs-lookup"><span data-stu-id="abede-129">1</span></span> |<span data-ttu-id="abede-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="abede-130">PCM 0</span></span> |
   | <span data-ttu-id="abede-131">2</span><span class="sxs-lookup"><span data-stu-id="abede-131">2</span></span> |<span data-ttu-id="abede-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="abede-132">PCM 1</span></span> |
   | <span data-ttu-id="abede-133">3</span><span class="sxs-lookup"><span data-stu-id="abede-133">3</span></span> |<span data-ttu-id="abede-134">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="abede-134">Controller 0</span></span> |
   | <span data-ttu-id="abede-135">4</span><span class="sxs-lookup"><span data-stu-id="abede-135">4</span></span> |<span data-ttu-id="abede-136">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="abede-136">Controller 1</span></span> |
   
    <span data-ttu-id="abede-137">그림 2의 번호 3과 같이 **배터리 결함** 에 해당하는 PCM 0의 모니터링 표시기 LED가 켜져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-137">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="abede-139">**그림 2** 모니터링 표시기 LED를 표시하는 PCM 뒷면</span><span class="sxs-lookup"><span data-stu-id="abede-139">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="abede-140">레이블</span><span class="sxs-lookup"><span data-stu-id="abede-140">Label</span></span> | <span data-ttu-id="abede-141">설명</span><span class="sxs-lookup"><span data-stu-id="abede-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="abede-142">1</span><span class="sxs-lookup"><span data-stu-id="abede-142">1</span></span> |<span data-ttu-id="abede-143">AC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="abede-143">AC power failure</span></span> |
   | <span data-ttu-id="abede-144">2</span><span class="sxs-lookup"><span data-stu-id="abede-144">2</span></span> |<span data-ttu-id="abede-145">팬 오류</span><span class="sxs-lookup"><span data-stu-id="abede-145">Fan failure</span></span> |
   | <span data-ttu-id="abede-146">3</span><span class="sxs-lookup"><span data-stu-id="abede-146">3</span></span> |<span data-ttu-id="abede-147">배터리 결함</span><span class="sxs-lookup"><span data-stu-id="abede-147">Battery fault</span></span> |
   | <span data-ttu-id="abede-148">4</span><span class="sxs-lookup"><span data-stu-id="abede-148">4</span></span> |<span data-ttu-id="abede-149">PCM 정상</span><span class="sxs-lookup"><span data-stu-id="abede-149">PCM OK</span></span> |
   | <span data-ttu-id="abede-150">5</span><span class="sxs-lookup"><span data-stu-id="abede-150">5</span></span> |<span data-ttu-id="abede-151">DC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="abede-151">DC power failure</span></span> |
   | <span data-ttu-id="abede-152">6</span><span class="sxs-lookup"><span data-stu-id="abede-152">6</span></span> |<span data-ttu-id="abede-153">배터리 정상</span><span class="sxs-lookup"><span data-stu-id="abede-153">Battery healthy</span></span> |
3. <span data-ttu-id="abede-154">오류가 발생한 배터리가 있는 PCM을 꺼내려면 [PCM 꺼내기](storsimple-power-cooling-module-replacement.md#remove-a-pcm)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="abede-154">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="abede-155">PCM을 꺼낸 후 다음 그림과 같이 배터리 모듈 핸들을 들고 위로 회전해서 당겨 배터리를 꺼냅니다.</span><span class="sxs-lookup"><span data-stu-id="abede-155">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![PCM에서 배터리 꺼내기](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="abede-157">**그림 3** PCM에서 배터리 꺼내기</span><span class="sxs-lookup"><span data-stu-id="abede-157">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="abede-158">FRU(현장 교체 장치) 포장 안에 모듈을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-158">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="abede-159">적절한 서비스 및 처리를 위해 결함이 있는 장치를 Microsoft에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-159">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="abede-160">새 백업 배터리 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="abede-160">Install a new backup battery module</span></span>
<span data-ttu-id="abede-161">StorSimple 장치의 기본 엔클로저의 PCM에 교체 배터리 모듈을 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="abede-161">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="abede-162">배터리 모듈을 설치하려면</span><span class="sxs-lookup"><span data-stu-id="abede-162">To install the battery module</span></span>
1. <span data-ttu-id="abede-163">백업 배터리 모듈을 PCM에 올바른 방향으로 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-163">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="abede-164">배터리 모듈 핸들을 아래로 완전히 눌러 커넥터를 장착합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-164">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="abede-165">[StorSimple 장치의 전원 및 냉각 모듈 교체](storsimple-power-cooling-module-replacement.md)의 지침에 따라 기본 엔클로저의 PCM을 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-165">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="abede-166">바꾸기가 완료되면 Azure Portal에서 장치로 이동한 후 **모니터** > **하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-166">After the replacement is complete, go to your device and then go to **Monitor** > **Hardware health** in the Azure portal.</span></span> <span data-ttu-id="abede-167">설치가 성공적으로 수행되었는지 확인하려면 배터리 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-167">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="abede-168">녹색 상태는 배터리가 정상임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abede-168">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="abede-169">백업 배터리 모듈 유지 관리</span><span class="sxs-lookup"><span data-stu-id="abede-169">Maintain the backup battery module</span></span>
<span data-ttu-id="abede-170">StorSimple 장치에서 백업 배터리 모듈은 전원 손실 이벤트가 발생하는 동안 컨트롤러에 전원을 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-170">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="abede-171">StorSimple 장치가 종료되기 전에 제어된 방식으로 중요한 데이터를 저장할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-171">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="abede-172">PCM에 완전히 충전된 두 개의 배터리가 있으면 시스템이 두 번의 연속된 손실 이벤트를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-172">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="abede-173">Azure Portal에서 **모니터** 블레이드의 **하드웨어 상태**는 배터리가 오작동하는지 또는 사용 기간 종료가 임박하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="abede-173">In the Azure portal, the **Hardware health** under the **Monitor** blade indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="abede-174">배터리 상태는 **공유 구성 요소**에서 **PCM 0의 배터리** 또는 **PCM 1의 배터리**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="abede-174">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="abede-175">이 블레이드에서 사용 기간 종료가 임박한 경우 **DEGRADED** 상태가 표시되고 사용 기간이 종료된 경우 **FAILED** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="abede-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="abede-176">단순히 충전이 필요한 경우 배터리에서 **FAILED** 를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-176">The battery can report **FAILED** when it simply needs to be charged.</span></span>


<span data-ttu-id="abede-177">**DEGRADED** 상태가 표시되는 경우 다음 작업을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-177">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="abede-178">시스템에서 최근에 전원 손실이 발생했거나 배터리 정기 유지 관리가 진행 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abede-178">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="abede-179">계속 진행하기 전에 12시간 동안 시스템을 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-179">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="abede-180">컨트롤러와 PCM을 실행하여 AC 전원에 12시간 동안 연속해서 연결된 후에도 상태가 여전히 **DEGRADED** 이면 배터리를 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-180">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="abede-181">교체 백업 배터리 모듈에 대해서는 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="abede-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="abede-182">12시간 후 정상 상태가 되면 배터리가 작동하는 것이며 유지 관리 충전만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abede-182">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="abede-183">연결된 AC 전원 손실이 없으며 PCM이 켜져 있고 AC 전원에 연결된 경우 배터리를 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-183">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="abede-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="abede-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abede-185">국가 및 지역 규정에 따라 오류가 발생한 배터리를 폐기합니다.</span><span class="sxs-lookup"><span data-stu-id="abede-185">Dispose of the failed battery according to national and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abede-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="abede-186">Next steps</span></span>
<span data-ttu-id="abede-187">[StorSimple 하드웨어 구성 요소 교체](storsimple-8000-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="abede-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

