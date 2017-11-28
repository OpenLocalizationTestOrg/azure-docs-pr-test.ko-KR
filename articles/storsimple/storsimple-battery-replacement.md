---
title: "Microsoft Azure StorSimple 장치에서 배터리 aaaReplace | Microsoft Docs"
description: "Tooremove, 대체를 하 고 StorSimple 장치에서 백업 배터리 모듈 hello를 유지 관리 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="5058d-103">StorSimple 장치에서 hello 백업 배터리 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="5058d-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="5058d-104">개요</span><span class="sxs-lookup"><span data-stu-id="5058d-104">Overview</span></span>
<span data-ttu-id="5058d-105">hello 기본 인클로저 전원 및 냉각 모듈 (PCM) Microsoft Azure StorSimple 장치에는 추가적인 배터리 팩을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="5058d-106">이 팩 hello StorSimple 장치 저장할 수 있도록 데이터의 기본 인클로저를 toohello AC 전원 손실이 발생 해도 power를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="5058d-107">이 배터리 팩은 참조 tooas hello *백업 배터리 모듈*합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="5058d-108">hello 백업 배터리 모듈 hello 기본 인클로저 StorSimple 장치에만 존재 하므로 (EBOD 인클로저 hello 백업 배터리 모듈을 포함 되지 않은).</span><span class="sxs-lookup"><span data-stu-id="5058d-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="5058d-109">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="5058d-110">Hello 백업 배터리 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="5058d-111">새 백업 배터리 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="5058d-111">Install a new backup battery module</span></span>
* <span data-ttu-id="5058d-112">Hello 백업 배터리 모듈을 유지 관리</span><span class="sxs-lookup"><span data-stu-id="5058d-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5058d-113">분리 및 교체 백업 배터리 모듈 hello hello 보안 정보를 검토 하기 전에 [소개 tooStorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="5058d-114">Hello 백업 배터리 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-114">Remove hello backup battery module</span></span>
<span data-ttu-id="5058d-115">StorSimple 장치에 대 한 hello 백업 배터리 모듈은 현장 교체 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="5058d-116">Hello PCM에에서 설치 하기 전에 hello 배터리 모듈 원래 패키지에 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="5058d-117">Hello 단계 tooremove hello 백업 배터리 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="5058d-118">tooremove hello 백업 배터리 모듈</span><span class="sxs-lookup"><span data-stu-id="5058d-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="5058d-119">Hello Azure 클래식 포털에서 너무 이동**장치** > **유지 관리** > **하드웨어 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="5058d-120">아래 **공유 구성 요소의**, hello hello 배터리 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="5058d-121">배터리는 hello에 실패 했습니다 hello PCM을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="5058d-122">그림 1 hello hello StorSimple 장치의 후면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="5058d-124">**그림 1** PCM 및 컨트롤러 모듈을 표시하는 기본 장치 뒷면</span><span class="sxs-lookup"><span data-stu-id="5058d-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="5058d-125">레이블</span><span class="sxs-lookup"><span data-stu-id="5058d-125">Label</span></span> | <span data-ttu-id="5058d-126">설명</span><span class="sxs-lookup"><span data-stu-id="5058d-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5058d-127">1</span><span class="sxs-lookup"><span data-stu-id="5058d-127">1</span></span> |<span data-ttu-id="5058d-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="5058d-128">PCM 0</span></span> |
   | <span data-ttu-id="5058d-129">2</span><span class="sxs-lookup"><span data-stu-id="5058d-129">2</span></span> |<span data-ttu-id="5058d-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="5058d-130">PCM 1</span></span> |
   | <span data-ttu-id="5058d-131">3</span><span class="sxs-lookup"><span data-stu-id="5058d-131">3</span></span> |<span data-ttu-id="5058d-132">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="5058d-132">Controller 0</span></span> |
   | <span data-ttu-id="5058d-133">4</span><span class="sxs-lookup"><span data-stu-id="5058d-133">4</span></span> |<span data-ttu-id="5058d-134">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="5058d-134">Controller 1</span></span> |
   
    <span data-ttu-id="5058d-135">표시기를 모니터링 하는 hello 너무 해당 하는 PCM 0에서 LED를 hello 그림 2에서에서 번호 3으로 표시 된 것과 같이**배터리 결함** 켜져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="5058d-137">**그림 2** PCM의 후면 보여 주는 hello 모니터링 표시기 Led</span><span class="sxs-lookup"><span data-stu-id="5058d-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="5058d-138">레이블</span><span class="sxs-lookup"><span data-stu-id="5058d-138">Label</span></span> | <span data-ttu-id="5058d-139">설명</span><span class="sxs-lookup"><span data-stu-id="5058d-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5058d-140">1</span><span class="sxs-lookup"><span data-stu-id="5058d-140">1</span></span> |<span data-ttu-id="5058d-141">AC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="5058d-141">AC power failure</span></span> |
   | <span data-ttu-id="5058d-142">2</span><span class="sxs-lookup"><span data-stu-id="5058d-142">2</span></span> |<span data-ttu-id="5058d-143">팬 오류</span><span class="sxs-lookup"><span data-stu-id="5058d-143">Fan failure</span></span> |
   | <span data-ttu-id="5058d-144">3</span><span class="sxs-lookup"><span data-stu-id="5058d-144">3</span></span> |<span data-ttu-id="5058d-145">배터리 결함</span><span class="sxs-lookup"><span data-stu-id="5058d-145">Battery fault</span></span> |
   | <span data-ttu-id="5058d-146">4</span><span class="sxs-lookup"><span data-stu-id="5058d-146">4</span></span> |<span data-ttu-id="5058d-147">PCM 정상</span><span class="sxs-lookup"><span data-stu-id="5058d-147">PCM OK</span></span> |
   | <span data-ttu-id="5058d-148">5</span><span class="sxs-lookup"><span data-stu-id="5058d-148">5</span></span> |<span data-ttu-id="5058d-149">DC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="5058d-149">DC power failure</span></span> |
   | <span data-ttu-id="5058d-150">6</span><span class="sxs-lookup"><span data-stu-id="5058d-150">6</span></span> |<span data-ttu-id="5058d-151">배터리 정상</span><span class="sxs-lookup"><span data-stu-id="5058d-151">Battery healthy</span></span> |
3. <span data-ttu-id="5058d-152">실패 한 배터리 tooremove hello PCM에서 다음과 같이 hello [PCM 제거](storsimple-power-cooling-module-replacement.md#remove-a-pcm)합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="5058d-153">PCM 제거 hello, 리프트 및 회전 hello 배터리 모듈 hello 다음 그림에에서 표시 된 대로 위쪽으로 처리 하 고 tooremove hello 배터리 꺼내 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![PCM에서 배터리 꺼내기](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="5058d-155">**그림 3** hello PCM에서에서 배터리 hello 제거</span><span class="sxs-lookup"><span data-stu-id="5058d-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="5058d-156">Hello 현장 교체 장치 패키지에 hello 모듈을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="5058d-157">적절 한 수리와 처리에 대 한 hello 결함 있는 장치 tooMicrosoft를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="5058d-158">새 백업 배터리 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="5058d-158">Install a new backup battery module</span></span>
<span data-ttu-id="5058d-159">Hello 단계 tooinstall hello 교체 배터리 모듈 hello 기본 인클로저 StorSimple 장치에 PCM hello에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="5058d-160">tooinstall hello 배터리 모듈</span><span class="sxs-lookup"><span data-stu-id="5058d-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="5058d-161">Hello PCM에서에서 적절 한 방향을 hello에 hello 백업 배터리 모듈을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="5058d-162">케이블 hello 배터리 모듈을 눌러 모든 hello 방식으로 tooseat hello 커넥터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="5058d-163">대체 hello 지침에 따라 hello 기본 인클로저에서 PCM hello [StorSimple 장치에서 전원 및 냉각 모듈 교체](storsimple-power-cooling-module-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="5058d-164">Hello 교체가 완료 되 면 후 너무 이동**장치** > **유지 관리** > **하드웨어 상태** hello Azure 클래식 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="5058d-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="5058d-165">Hello 상태의 hello 배터리 toomake hello 설치가 제대로 수행 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="5058d-166">녹색 상태 hello 배터리 정상 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="5058d-167">Hello 백업 배터리 모듈을 유지 관리</span><span class="sxs-lookup"><span data-stu-id="5058d-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="5058d-168">StorSimple 장치 hello 백업 배터리 모듈 전원 손실 이벤트가 발생 하는 동안 전원 toohello 컨트롤러를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="5058d-169">제어 된 방식으로 hello StorSimple 장치 toosave 중요 한 데이터가 이전 tooshutting을 아래로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="5058d-170">Hello Pcm의에서 완전히 충전 된 배터리 두 hello 시스템 두 개의 연속 된 손실 이벤트를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="5058d-171">Hello Azure 클래식 포털에서에서 hello **하드웨어 상태** hello에 **유지 관리** 페이지 hello 배터리가 오작동 하거나 hello 수명 끝에 도달 하 고 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="5058d-172">hello 배터리 상태를 나타냅니다 **PCM 0의에서 배터리** 또는 **PCM 1의 배터리** 아래 **공유 구성 요소의**합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="5058d-173">이 페이지에서 사용 기간 종료가 임박한 경우 **DEGRADED** 상태가 표시되고 사용 기간이 종료된 경우 **FAILED** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="5058d-174">hello 배터리를 보고할 수 **실패** 단순히 청구 toobe 필요 경우.</span><span class="sxs-lookup"><span data-stu-id="5058d-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="5058d-175">경우 hello **DEGRADED** 상태가 나타나면 다음 조치 hello 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="5058d-176">hello 시스템 최근 전원 손실이 발생 했을 수 있습니다 또는 hello 배터리에서 정기적으로 유지 관리 모드로 전환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="5058d-177">계속 하기 전에 12 시간 동안 hello 시스템을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="5058d-178">Hello 상태가 여전히 **DEGRADED** 배터리 교체 toobe 필요한 hello 사용 하 여 지속적으로 연결 tooAC 전원 12 시간 컨트롤러와 pcm을 실행 하면서 다음 hello 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="5058d-179">교체 백업 배터리 모듈에 대해서는 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="5058d-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="5058d-180">12 시간 후 정상 hello 상태가 되 면 hello 배터리가 정상적으로 작동 하 고 유지 관리 비용이 청구만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="5058d-181">발생 되지 않은 경우는 관련된 AC 전원 손실과 hello PCM 켜져 있고 연결 tooAC 전원, hello 배터리 교체 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="5058d-182">[Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) tooorder 교체 백업 배터리 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5058d-183">Hello의 dispose toonational 및 지역 규정에 따라 배터리에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5058d-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5058d-184">Next steps</span></span>
<span data-ttu-id="5058d-185">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5058d-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

