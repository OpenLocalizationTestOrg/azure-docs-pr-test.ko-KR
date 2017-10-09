---
title: "StorSimple 장치에서 PCM aaaReplace | Microsoft Docs"
description: "어떻게 tooremove 및 바꾸기 hello 전원 및 냉각 모듈 (PCM) StorSimple 장치에 설명"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="0de52-103">StorSimple 장치의 전원 및 냉각 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="0de52-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="0de52-104">개요</span><span class="sxs-lookup"><span data-stu-id="0de52-104">Overview</span></span>
<span data-ttu-id="0de52-105">hello 전원 및 냉각 모듈 (PCM)에서 Microsoft Azure StorSimple 장치에 전원 공급 장치 및 냉각 팬 hello 기본 인클로저와 EBOD 인클로저를 통해 제어 되는 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="0de52-106">각 엔클로저마다 인증된 PCM 모델 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="0de52-107">hello 기본 인클로저는 764w PCM에 대 한 인증 및 hello EBOD 인클로저는 580w PCM에 대해 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="0de52-108">Hello 기본 인클로저와 EBOD 인클로저 hello에 대 한 hello Pcm이 서로 다르기는 하지만 hello 교체 절차는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="0de52-109">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="0de52-110">PCM 꺼내기</span><span class="sxs-lookup"><span data-stu-id="0de52-110">Remove a PCM</span></span>
* <span data-ttu-id="0de52-111">교체 PCM 설치</span><span class="sxs-lookup"><span data-stu-id="0de52-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0de52-112">제거 하 고는 PCM을 교체 hello 보안 정보를 검토 하기 전에 [StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="0de52-113">PCM을 교체하기 전에</span><span class="sxs-lookup"><span data-stu-id="0de52-113">Before you replace a PCM</span></span>
<span data-ttu-id="0de52-114">PCM을 교체 하기 전에 중요 한 문제를 따라 hello 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="0de52-115">Hello 전원 공급을 하는 경우 hello PCM에 오류가 발생 하면 hello 결함이 있는 모듈은 설치 된 가지만 hello 전원 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="0de52-116">hello 팬 hello 인클로저에서 tooreceive 전원 고 tooprovide 적절 한 냉각을 계속 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="0de52-117">Hello 팬에 오류가 발생 하는 경우 즉시 바뀝니다 toobe hello PCM에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="0de52-118">Hello PCM을 제거 하기 전에 hello 기본 스위치 (있는 경우) 해제 하 여 또는 hello 전원 코드를 물리적으로 제거 하 여 hello 전원을 hello PCM에서에서 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="0de52-119">이 전원 공급이 중단 임박 임을 경고 tooyour 시스템을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="0de52-120">있는지 확인 하십시오 다른 PCM이 작동 하는 hello 결함이 있는 PCM hello 교체 하기 전에 시스템 작업을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="0de52-121">가능한 한 빨리 결함이 있는 PCM을 완벽하게 작동하는 PCM으로 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="0de52-122">PCM 모듈 교체만 몇 분 toocomplete, 걸리지만 제거 하지 못했습니다 hello PCM tooprevent 과열 10 분 내에 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="0de52-123">Note hello 대체 764 PCM 모듈 hello 공장에서 출고 hello 백업 배터리 모듈에 포함 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="0de52-124">결함이 있는 PCM에서 tooremove hello 배터리 필요한 쿼리하고 hello 교체 모듈 이전 tooperforming hello 교체에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="0de52-125">자세한 내용은 참조 방법을 너무[제거 하 고 백업 배터리 모듈을 삽입](storsimple-battery-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-125">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="0de52-126">PCM 꺼내기</span><span class="sxs-lookup"><span data-stu-id="0de52-126">Remove a PCM</span></span>
<span data-ttu-id="0de52-127">Microsoft Azure StorSimple 장치에서 준비 tooremove 전원 및 냉각 모듈 (PCM) 있을 때는 다음이 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0de52-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="0de52-128">PCM을 제거 하기 전에 올바른 교체품 (764w 기본 인클로저 hello) 또는 EBOD 인클로저의 hello에 대 한 580w 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>
> 
> 

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="0de52-129">tooremove pcm 분리</span><span class="sxs-lookup"><span data-stu-id="0de52-129">tooremove a PCM</span></span>
1. <span data-ttu-id="0de52-130">Hello Azure 클래식 포털에서에서 클릭 **장치** > **유지 관리** > **하드웨어 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-130">In hello Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="0de52-131">Hello PCM 구성 요소에서의 hello 상태를 확인 **공유 구성 요소의** tooidentify PCM 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-131">Check hello status of hello PCM components under **Shared Components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="0de52-132">PCM 0의에서 전원 공급 장치에 실패 한 경우의 상태를 hello **PCM 0의에서 전원 공급 장치** 빨강으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="0de52-133">PCM 1의 전원 공급 장치에 실패 한 경우의 상태를 hello **PCM 1의 전원 공급 장치** 빨강으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="0de52-134">PCM 1의 hello 팬에 실패 한 경우의 상태를 hello **0 PCM 0의 냉각** 또는 **PCM 0의 냉각 1** 빨강으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="0de52-135">Hello를 hello 기본 인클로저의 백업 hello에 오류가 발생 한 PCM을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="0de52-136">8600 모델을 실행 하는 경우 hello hello 전면 패널 LED 디스플레이에 표시 된 시스템 장치 식별 번호를 확인 하 여 hello 기본 인클로저를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="0de52-137">기본 장치 ID hello 기본 인클로저에 표시 되는 hello **00**, hello 기본 단위 ID EBOD 인클로저 hello에 표시 되는 반면, **01**합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="0de52-138">hello 다음 다이어그램과 테이블 설명 hello LED 디스플레이의 전면 패널 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![전면 OPS 패널의 시스템 ID](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="0de52-140">**그림 1** hello 장치의 전면 패널</span><span class="sxs-lookup"><span data-stu-id="0de52-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="0de52-141">레이블</span><span class="sxs-lookup"><span data-stu-id="0de52-141">Label</span></span> | <span data-ttu-id="0de52-142">설명</span><span class="sxs-lookup"><span data-stu-id="0de52-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0de52-143">1</span><span class="sxs-lookup"><span data-stu-id="0de52-143">1</span></span> |<span data-ttu-id="0de52-144">음소거 단추</span><span class="sxs-lookup"><span data-stu-id="0de52-144">Mute button</span></span> |
   | <span data-ttu-id="0de52-145">2</span><span class="sxs-lookup"><span data-stu-id="0de52-145">2</span></span> |<span data-ttu-id="0de52-146">시스템 전원</span><span class="sxs-lookup"><span data-stu-id="0de52-146">System power</span></span> |
   | <span data-ttu-id="0de52-147">3</span><span class="sxs-lookup"><span data-stu-id="0de52-147">3</span></span> |<span data-ttu-id="0de52-148">모듈 결함</span><span class="sxs-lookup"><span data-stu-id="0de52-148">Module fault</span></span> |
   | <span data-ttu-id="0de52-149">4</span><span class="sxs-lookup"><span data-stu-id="0de52-149">4</span></span> |<span data-ttu-id="0de52-150">논리적 결함</span><span class="sxs-lookup"><span data-stu-id="0de52-150">Logical fault</span></span> |
   | <span data-ttu-id="0de52-151">5</span><span class="sxs-lookup"><span data-stu-id="0de52-151">5</span></span> |<span data-ttu-id="0de52-152">장치 ID 디스플레이</span><span class="sxs-lookup"><span data-stu-id="0de52-152">Unit ID display</span></span> |
3. <span data-ttu-id="0de52-153">모니터링 표시기 Led hello hello 기본 인클로저 후면의 hello는 tooidentify hello 결함이 있는 PCM 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="0de52-154">Hello 다음 다이어그램 및 toounderstand 어떻게 테이블을 참조 toouse hello Led toolocate hello 결함이 있는 PCM 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="0de52-155">예를 들어 경우 hello 초래한 해당 toohello **팬 오류** 가 켜지 면 hello 팬 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="0de52-156">마찬가지로, 경우 hello 초래한 너무 해당**AC 오류** 가 켜지 면 전원 공급 장치 hello 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![장치 PCM 모니터링 표시기 LED의 백플레인](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="0de52-158">**그림 2** 표시기 LED가 있는 PCM 뒷면</span><span class="sxs-lookup"><span data-stu-id="0de52-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="0de52-159">레이블</span><span class="sxs-lookup"><span data-stu-id="0de52-159">Label</span></span> | <span data-ttu-id="0de52-160">설명</span><span class="sxs-lookup"><span data-stu-id="0de52-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0de52-161">1</span><span class="sxs-lookup"><span data-stu-id="0de52-161">1</span></span> |<span data-ttu-id="0de52-162">AC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="0de52-162">AC power failure</span></span> |
   | <span data-ttu-id="0de52-163">2</span><span class="sxs-lookup"><span data-stu-id="0de52-163">2</span></span> |<span data-ttu-id="0de52-164">팬 오류</span><span class="sxs-lookup"><span data-stu-id="0de52-164">Fan failure</span></span> |
   | <span data-ttu-id="0de52-165">3</span><span class="sxs-lookup"><span data-stu-id="0de52-165">3</span></span> |<span data-ttu-id="0de52-166">배터리 결함</span><span class="sxs-lookup"><span data-stu-id="0de52-166">Battery fault</span></span> |
   | <span data-ttu-id="0de52-167">4</span><span class="sxs-lookup"><span data-stu-id="0de52-167">4</span></span> |<span data-ttu-id="0de52-168">PCM 정상</span><span class="sxs-lookup"><span data-stu-id="0de52-168">PCM OK</span></span> |
   | <span data-ttu-id="0de52-169">5</span><span class="sxs-lookup"><span data-stu-id="0de52-169">5</span></span> |<span data-ttu-id="0de52-170">DC 전원 오류</span><span class="sxs-lookup"><span data-stu-id="0de52-170">DC power failure</span></span> |
   | <span data-ttu-id="0de52-171">6</span><span class="sxs-lookup"><span data-stu-id="0de52-171">6</span></span> |<span data-ttu-id="0de52-172">배터리 정상</span><span class="sxs-lookup"><span data-stu-id="0de52-172">Battery healthy</span></span> |
4. <span data-ttu-id="0de52-173">Toohello hello hello StorSimple 장치 toolocate 실패 hello PCM 모듈 뒷면의 다이어그램을 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0de52-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="0de52-174">PCM 0 hello 왼쪽에 있고 PCM 1은 오른쪽 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="0de52-175">hello 표는 hello 모듈에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-175">hello table that follows explains hello modules.</span></span>
   
     ![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="0de52-177">**그림 3** 플러그 인 모듈이 있는 장치 뒷면</span><span class="sxs-lookup"><span data-stu-id="0de52-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="0de52-178">레이블</span><span class="sxs-lookup"><span data-stu-id="0de52-178">Label</span></span> | <span data-ttu-id="0de52-179">설명</span><span class="sxs-lookup"><span data-stu-id="0de52-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0de52-180">1</span><span class="sxs-lookup"><span data-stu-id="0de52-180">1</span></span> |<span data-ttu-id="0de52-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="0de52-181">PCM 0</span></span> |
   | <span data-ttu-id="0de52-182">2</span><span class="sxs-lookup"><span data-stu-id="0de52-182">2</span></span> |<span data-ttu-id="0de52-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="0de52-183">PCM 1</span></span> |
   | <span data-ttu-id="0de52-184">3</span><span class="sxs-lookup"><span data-stu-id="0de52-184">3</span></span> |<span data-ttu-id="0de52-185">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="0de52-185">Controller 0</span></span> |
   | <span data-ttu-id="0de52-186">4</span><span class="sxs-lookup"><span data-stu-id="0de52-186">4</span></span> |<span data-ttu-id="0de52-187">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="0de52-187">Controller 1</span></span> |
5. <span data-ttu-id="0de52-188">설정 해제 결함이 있는 PCM hello 및 hello 전원 공급 장치 코드를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="0de52-189">이제 PCM hello를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="0de52-190">엄지와 집게, PCM을 처리 하는 hello의 hello 래치 및 hello 잡고 함께 tooopen hello 핸들에 동시에 누르면 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![PCM 핸들 열기](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="0de52-192">**그림 4** Opening hello PCM 처리</span><span class="sxs-lookup"><span data-stu-id="0de52-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="0de52-193">Hello 핸들을 잡고 PCM hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![장치 PCM 꺼내기](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="0de52-195">**그림 5** PCM 제거 하는 hello</span><span class="sxs-lookup"><span data-stu-id="0de52-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="0de52-196">교체 PCM 설치</span><span class="sxs-lookup"><span data-stu-id="0de52-196">Install a replacement PCM</span></span>
<span data-ttu-id="0de52-197">이러한 지침은 tooinstall StorSimple 장치에서 PCM을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="0de52-198">Hello 백업 배터리 모듈 이전 tooinstalling hello 교체 PCM (too764 W Pcm만 적용 됨)를 삽입 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="0de52-199">자세한 내용은 참조 방법을 너무[제거 하 고 백업 배터리 모듈을 삽입](storsimple-battery-replacement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-199">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="0de52-200">tooinstall pcm 분리</span><span class="sxs-lookup"><span data-stu-id="0de52-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="0de52-201">Hello 올바른 교체용 PCM이 인클로저의 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0de52-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="0de52-202">hello 기본 인클로저는 764w PCM 되어야 하며 hello EBOD 인클로저는 580w PCM 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="0de52-203">Toouse 해서는 안 hello 580w PCM hello 기본 인클로저에서 또는 EBOD 인클로저 hello에 764w PCM 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="0de52-204">다음 이미지는 hello hello에 대 한이 정보 즉 레이블을 tooidentify toohello PCM을 추가 하는 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![장치 PCM 레이블](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="0de52-206">**그림 6** PCM 레이블</span><span class="sxs-lookup"><span data-stu-id="0de52-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="0de52-207">손상 toohello 인클로저, 특히 주의 toohello 커넥터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0de52-208">**구부러진 핀이 있는 경우에 hello 모듈을 설치 하지 마십시오.**</span><span class="sxs-lookup"><span data-stu-id="0de52-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="0de52-209">Hello에 PCM을 처리 하는 hello 위치, 슬라이드 hello 모듈 hello 인클로저도을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![장치 PCM 설치](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="0de52-211">**그림 7** 설치 hello PCM</span><span class="sxs-lookup"><span data-stu-id="0de52-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="0de52-212">수동으로 hello PCM 핸들을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="0de52-213">Hello 핸들 래치가 맞물릴 때 처럼 한 번의 클릭을 들려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-213">You should hear a click as hello handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0de52-214">커넥터 핀 hello tooensure 있습니다 부드럽게 잡아당겨 보면 hello 핸들 hello 래치를 해제 하지 않고 참여 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="0de52-215">Hello PCM이 빼내 참여 하는 hello 커넥터 하기 전에 해당 hello 래치 닫혔습니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="0de52-216">Hello 전원 케이블 toohello 전원과 PCM toohello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="0de52-217">릴리프 베일을 고정 hello 부담을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-217">Secure hello strain relief bales.</span></span> 
7. <span data-ttu-id="0de52-218">Hello PCM 켭니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="0de52-219">Hello 교체에 성공 했는지 확인: hello StorSimple 관리자 서비스의 Azure 클래식 포털에서에서 탐색 너무**장치** > **유지 관리**  >  **하드웨어 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-219">Verify that hello replacement was successful: in hello Azure classic portal of your StorSimple Manager service, navigate too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="0de52-220">아래 **공유 구성 요소의**, hello PCM의 hello 상태가 녹색으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-220">Under **Shared Components**, hello status of hello PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0de52-221">Hello 교체 PCM toocompletely initialize 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="0de52-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0de52-222">Next steps</span></span>
<span data-ttu-id="0de52-223">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0de52-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

