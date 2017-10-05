---
title: "Microsoft Azure StorSimple 장치의 배터리 교체 | Microsoft Docs"
description: "StorSimple 장치의 백업 배터리 모듈을 꺼내고 교체 및 유지 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="2c53e-103">StorSimple 장치의 백업 배터리 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="2c53e-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="2c53e-104">개요</span><span class="sxs-lookup"><span data-stu-id="2c53e-104">Overview</span></span>
<span data-ttu-id="2c53e-105">Microsoft Azure StorSimple 장치의 기본 엔클로저 PCM(전원 및 냉각 모듈)에는 추가 배터리 팩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="2c53e-106">이 팩은 기본 엔클로저에 대한 AC 전원이 끊어질 경우 StorSimple 장치가 데이터를 저장할 수 있도록 전원을 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="2c53e-107">이 배터리 팩을 *백업 배터리 모듈*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="2c53e-108">백업 배터리 모듈은 StorSimple 장치의 기본 엔클로저에만 있습니다(EBOD 엔클로저에는 백업 배터리 모듈이 없음).</span><span class="sxs-lookup"><span data-stu-id="2c53e-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="2c53e-109">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="2c53e-110">백업 배터리 모듈 꺼내기</span><span class="sxs-lookup"><span data-stu-id="2c53e-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="2c53e-111">새 백업 배터리 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="2c53e-111">Install a new backup battery module</span></span>
* <span data-ttu-id="2c53e-112">백업 배터리 모듈 유지 관리</span><span class="sxs-lookup"><span data-stu-id="2c53e-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c53e-113">백업 배터리 모듈을 꺼내고 교체하기 전에 [StorSimple 하드웨어 구성 요소 교체 소개](storsimple-hardware-component-replacement.md)에서 안전 정보를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="2c53e-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="2c53e-114">백업 배터리 모듈 꺼내기</span><span class="sxs-lookup"><span data-stu-id="2c53e-114">Remove the backup battery module</span></span>
<span data-ttu-id="2c53e-115">StorSimple 장치에 대한 백업 배터리 모듈은 FRU(현장 교체 장치)입니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="2c53e-116">PCM에 설치하기 전에는 원래 포장 안에 배터리 모듈을 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="2c53e-117">백업 배터리를 꺼내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="2c53e-118">백업 배터리 모듈을 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="2c53e-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="2c53e-119">Azure 클래식 포털에서 **장치** > **유지 관리** > **하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="2c53e-120">**공유 구성 요소**아래에서 배터리 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="2c53e-121">배터리에서 오류가 발생한 PCM을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="2c53e-122">그림 1은 StorSimple 장치의 뒷면의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="2c53e-124">**그림 1** PCM 및 컨트롤러 모듈을 표시하는 기본 장치 뒷면</span><span class="sxs-lookup"><span data-stu-id="2c53e-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="2c53e-125">레이블</span><span class="sxs-lookup"><span data-stu-id="2c53e-125">Label</span></span> | <span data-ttu-id="2c53e-126">설명</span><span class="sxs-lookup"><span data-stu-id="2c53e-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2c53e-127">1</span><span class="sxs-lookup"><span data-stu-id="2c53e-127">1</span></span> |<span data-ttu-id="2c53e-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="2c53e-128">PCM 0</span></span> |
   | <span data-ttu-id="2c53e-129">2</span><span class="sxs-lookup"><span data-stu-id="2c53e-129">2</span></span> |<span data-ttu-id="2c53e-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="2c53e-130">PCM 1</span></span> |
   | <span data-ttu-id="2c53e-131">3</span><span class="sxs-lookup"><span data-stu-id="2c53e-131">3</span></span> |<span data-ttu-id="2c53e-132">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="2c53e-132">Controller 0</span></span> |
   | <span data-ttu-id="2c53e-133">4</span><span class="sxs-lookup"><span data-stu-id="2c53e-133">4</span></span> |<span data-ttu-id="2c53e-134">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="2c53e-134">Controller 1</span></span> |
   
    <span data-ttu-id="2c53e-135">그림 2의 번호 3과 같이 **배터리 결함** 에 해당하는 PCM 0의 모니터링 표시기 LED가 켜져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="2c53e-137">**그림 2** 모니터링 표시기 LED를 표시하는 PCM 뒷면</span><span class="sxs-lookup"><span data-stu-id="2c53e-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="2c53e-138">레이블</span><span class="sxs-lookup"><span data-stu-id="2c53e-138">Label</span></span> | <span data-ttu-id="2c53e-139">설명</span><span class="sxs-lookup"><span data-stu-id="2c53e-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2c53e-140">1</span><span class="sxs-lookup"><span data-stu-id="2c53e-140">1</span></span> |<span data-ttu-id="2c53e-141">AC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="2c53e-141">AC power failure</span></span> |
   | <span data-ttu-id="2c53e-142">2</span><span class="sxs-lookup"><span data-stu-id="2c53e-142">2</span></span> |<span data-ttu-id="2c53e-143">팬 오류</span><span class="sxs-lookup"><span data-stu-id="2c53e-143">Fan failure</span></span> |
   | <span data-ttu-id="2c53e-144">3</span><span class="sxs-lookup"><span data-stu-id="2c53e-144">3</span></span> |<span data-ttu-id="2c53e-145">배터리 결함</span><span class="sxs-lookup"><span data-stu-id="2c53e-145">Battery fault</span></span> |
   | <span data-ttu-id="2c53e-146">4</span><span class="sxs-lookup"><span data-stu-id="2c53e-146">4</span></span> |<span data-ttu-id="2c53e-147">PCM 정상</span><span class="sxs-lookup"><span data-stu-id="2c53e-147">PCM OK</span></span> |
   | <span data-ttu-id="2c53e-148">5</span><span class="sxs-lookup"><span data-stu-id="2c53e-148">5</span></span> |<span data-ttu-id="2c53e-149">DC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="2c53e-149">DC power failure</span></span> |
   | <span data-ttu-id="2c53e-150">6</span><span class="sxs-lookup"><span data-stu-id="2c53e-150">6</span></span> |<span data-ttu-id="2c53e-151">배터리 정상</span><span class="sxs-lookup"><span data-stu-id="2c53e-151">Battery healthy</span></span> |
3. <span data-ttu-id="2c53e-152">오류가 발생한 배터리가 있는 PCM을 꺼내려면 [PCM 꺼내기](storsimple-power-cooling-module-replacement.md#remove-a-pcm)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2c53e-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="2c53e-153">PCM을 꺼낸 후 다음 그림과 같이 배터리 모듈 핸들을 들고 위로 회전해서 당겨 배터리를 꺼냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![PCM에서 배터리 꺼내기](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="2c53e-155">**그림 3** PCM에서 배터리 꺼내기</span><span class="sxs-lookup"><span data-stu-id="2c53e-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="2c53e-156">FRU(현장 교체 장치) 포장 안에 모듈을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="2c53e-157">적절한 서비스 및 처리를 위해 결함이 있는 장치를 Microsoft에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="2c53e-158">새 백업 배터리 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="2c53e-158">Install a new backup battery module</span></span>
<span data-ttu-id="2c53e-159">StorSimple 장치의 기본 엔클로저의 PCM에 교체 배터리 모듈을 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2c53e-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="2c53e-160">배터리 모듈을 설치하려면</span><span class="sxs-lookup"><span data-stu-id="2c53e-160">To install the battery module</span></span>
1. <span data-ttu-id="2c53e-161">백업 배터리 모듈을 PCM에 올바른 방향으로 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="2c53e-162">배터리 모듈 핸들을 아래로 완전히 눌러 커넥터를 장착합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="2c53e-163">[StorSimple 장치의 전원 및 냉각 모듈 교체](storsimple-power-cooling-module-replacement.md)의 지침에 따라 기본 엔클로저의 PCM을 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="2c53e-164">교체가 완료되면 Azure 클래식 포털에서 **장치** > **유지 관리** > **하드웨어 상태**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="2c53e-165">설치가 성공적으로 수행되었는지 확인하려면 배터리 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="2c53e-166">녹색 상태는 배터리가 정상임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="2c53e-167">백업 배터리 모듈 유지 관리</span><span class="sxs-lookup"><span data-stu-id="2c53e-167">Maintain the backup battery module</span></span>
<span data-ttu-id="2c53e-168">StorSimple 장치에서 백업 배터리 모듈은 전원 손실 이벤트가 발생하는 동안 컨트롤러에 전원을 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="2c53e-169">StorSimple 장치가 종료되기 전에 제어된 방식으로 중요한 데이터를 저장할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="2c53e-170">PCM에 완전히 충전된 두 개의 배터리가 있으면 시스템이 두 번의 연속된 손실 이벤트를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="2c53e-171">Azure 클래식 포털에서 **유지 관리** 페이지의 **하드웨어 상태**는 배터리가 오작동하는지 또는 사용 기간 종료가 임박하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="2c53e-172">배터리 상태는 **공유 구성 요소**에서 **PCM 0의 배터리** 또는 **PCM 1의 배터리**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="2c53e-173">이 페이지에서 사용 기간 종료가 임박한 경우 **DEGRADED** 상태가 표시되고 사용 기간이 종료된 경우 **FAILED** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="2c53e-174">단순히 충전이 필요한 경우 배터리에서 **FAILED** 를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="2c53e-175">**DEGRADED** 상태가 표시되는 경우 다음 작업을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="2c53e-176">시스템에서 최근에 전원 손실이 발생했거나 배터리 정기 유지 관리가 진행 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="2c53e-177">계속 진행하기 전에 12시간 동안 시스템을 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="2c53e-178">컨트롤러와 PCM을 실행하여 AC 전원에 12시간 동안 연속해서 연결된 후에도 상태가 여전히 **DEGRADED** 이면 배터리를 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="2c53e-179">교체 백업 배터리 모듈에 대해서는 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="2c53e-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="2c53e-180">12시간 후 정상 상태가 되면 배터리가 작동하는 것이며 유지 관리 충전만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="2c53e-181">연결된 AC 전원 손실이 없으며 PCM이 켜져 있고 AC 전원에 연결된 경우 배터리를 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="2c53e-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="2c53e-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c53e-183">국가 및 지역 규정에 따라 오류가 발생한 배터리를 폐기합니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2c53e-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c53e-184">Next steps</span></span>
<span data-ttu-id="2c53e-185">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2c53e-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

