---
title: "StorSimple EBOD 컨트롤러 aaaReplace | Microsoft Docs"
description: "에 대해 설명 방법을 tooremove StorSimple 8600 장치의 EBOD 컨트롤러를 하나 또는 둘 다를 바꿉니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="929a7-103">StorSimple 장치의 EBOD 컨트롤러 교체</span><span class="sxs-lookup"><span data-stu-id="929a7-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="929a7-104">개요</span><span class="sxs-lookup"><span data-stu-id="929a7-104">Overview</span></span>
<span data-ttu-id="929a7-105">이 자습서에 설명 방법을 tooreplace Microsoft Azure StorSimple 장치에서 결함이 있는 EBOD 컨트롤러 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="929a7-106">EBOD 컨트롤러 모듈 tooreplace 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="929a7-107">Hello 결함이 있는 EBOD 컨트롤러 제거</span><span class="sxs-lookup"><span data-stu-id="929a7-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="929a7-108">새 EBOD 컨트롤러 설치</span><span class="sxs-lookup"><span data-stu-id="929a7-108">Install a new EBOD controller</span></span>

<span data-ttu-id="929a7-109">Hello를 시작 하기 전에 다음 정보를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="929a7-110">사용하지 않은 모든 슬롯에 빈 EBOD 모듈을 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="929a7-111">슬롯을 남겨 둘지 hello 인클로저가 제대로 식 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="929a7-112">hello EBOD 컨트롤러는 핫 스왑 가능한 제거 하거나 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="929a7-113">교체가 있을 때까지 오류가 발생한 모듈을 꺼내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="929a7-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="929a7-114">Hello 교체 프로세스를 시작 하면 10 분 내에 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="929a7-115">Tooremove 시도 하기 전에 모든 StorSimple 구성 요소 교체, hello 검토 해야 또는 [안전 아이콘 규칙](storsimple-safety.md#safety-icon-conventions) 및 기타 [안전 조치](storsimple-safety.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="929a7-116">EBOD 컨트롤러 꺼내기</span><span class="sxs-lookup"><span data-stu-id="929a7-116">Remove an EBOD controller</span></span>
<span data-ttu-id="929a7-117">전에 hello을 바꾸지 못했으므로 StorSimple 장치에 EBOD 컨트롤러 모듈, 있어야 해당 hello 다른 EBOD 컨트롤러 모듈이 활성화 되어 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="929a7-118">hello 다음 절차와 테이블에 설명 tooremove EBOD 컨트롤러 모듈을 hello 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="929a7-119">tooremove EBOD 모듈</span><span class="sxs-lookup"><span data-stu-id="929a7-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="929a7-120">Azure 클래식 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="929a7-121">너무 이동**장치** > **유지 관리** > **하드웨어 상태**, hello의 hello 상태에 대 한 원인이 있는지 확인 하 고 활성 EBOD hello 컨트롤러는 녹색 하 고 실패 hello EBOD 컨트롤러 모듈에 대 한 hello LED가 빨간색입니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="929a7-122">Hello hello 장치 뒷면에서 실패 하는 hello EBOD 컨트롤러 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="929a7-123">Hello EBOD 모듈 hello 시스템 꺼내기 전에 EBOD 컨트롤러 모듈 toohello 컨트롤러 hello를 연결 하는 hello 케이블을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="929a7-124">연결 된 toohello 컨트롤러 hello EBOD 컨트롤러 모듈의 hello 정확한 SAS 포트를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="929a7-125">Hello EBOD 모듈을 교체한 후 필요한 toorestore hello 시스템 toothis 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="929a7-126">일반적으로 포트 A로 표시 된 됩니다 **에서 호스팅할** hello 다이어그램 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![EBOD 컨트롤러의 백플레인](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="929a7-128">**그림 1** EBOD 모듈 뒷면</span><span class="sxs-lookup"><span data-stu-id="929a7-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="929a7-129">레이블</span><span class="sxs-lookup"><span data-stu-id="929a7-129">Label</span></span> | <span data-ttu-id="929a7-130">설명</span><span class="sxs-lookup"><span data-stu-id="929a7-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="929a7-131">1</span><span class="sxs-lookup"><span data-stu-id="929a7-131">1</span></span> |<span data-ttu-id="929a7-132">오류 LED</span><span class="sxs-lookup"><span data-stu-id="929a7-132">Fault LED</span></span> |
   | <span data-ttu-id="929a7-133">2</span><span class="sxs-lookup"><span data-stu-id="929a7-133">2</span></span> |<span data-ttu-id="929a7-134">전원 LED</span><span class="sxs-lookup"><span data-stu-id="929a7-134">Power LED</span></span> |
   | <span data-ttu-id="929a7-135">3</span><span class="sxs-lookup"><span data-stu-id="929a7-135">3</span></span> |<span data-ttu-id="929a7-136">SAS 커넥터</span><span class="sxs-lookup"><span data-stu-id="929a7-136">SAS connectors</span></span> |
   | <span data-ttu-id="929a7-137">4</span><span class="sxs-lookup"><span data-stu-id="929a7-137">4</span></span> |<span data-ttu-id="929a7-138">SAS LED</span><span class="sxs-lookup"><span data-stu-id="929a7-138">SAS LEDs</span></span> |
   | <span data-ttu-id="929a7-139">5</span><span class="sxs-lookup"><span data-stu-id="929a7-139">5</span></span> |<span data-ttu-id="929a7-140">팩터리 전용 직렬 포트</span><span class="sxs-lookup"><span data-stu-id="929a7-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="929a7-141">6</span><span class="sxs-lookup"><span data-stu-id="929a7-141">6</span></span> |<span data-ttu-id="929a7-142">포트 A(호스트 인)</span><span class="sxs-lookup"><span data-stu-id="929a7-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="929a7-143">7</span><span class="sxs-lookup"><span data-stu-id="929a7-143">7</span></span> |<span data-ttu-id="929a7-144">포트 B(호스트 아웃)</span><span class="sxs-lookup"><span data-stu-id="929a7-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="929a7-145">8</span><span class="sxs-lookup"><span data-stu-id="929a7-145">8</span></span> |<span data-ttu-id="929a7-146">포트 C(팩터리 전용)</span><span class="sxs-lookup"><span data-stu-id="929a7-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="929a7-147">새 EBOD 컨트롤러 설치</span><span class="sxs-lookup"><span data-stu-id="929a7-147">Install a new EBOD controller</span></span>
<span data-ttu-id="929a7-148">hello 다음 절차와 테이블에 설명 방법을 tooinstall StorSimple 장치에 EBOD 컨트롤러 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="929a7-149">EBOD 컨트롤러 tooinstall</span><span class="sxs-lookup"><span data-stu-id="929a7-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="929a7-150">Hello EBOD 장치를 특히 toohello 인터페이스 커넥터 손상 되지 않았는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="929a7-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="929a7-151">구부러진 핀 하는 경우에 hello 새 EBOD 컨트롤러를 설치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="929a7-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="929a7-152">Hello에 hello 래치 위치, 슬라이드 hello 모듈 hello 인클로저 hello 맞물릴 때까지으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![EBOD 컨트롤러 설치](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="929a7-154">**그림 2** hello EBOD 컨트롤러 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="929a7-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="929a7-155">래치 닫기 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-155">Close hello latch.</span></span> <span data-ttu-id="929a7-156">Hello 래치가 맞물릴 때 처럼 한 번의 클릭을 들려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-156">You should hear a click as hello latch engages.</span></span>
   
    ![EBOD 래치 해제](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="929a7-158">**그림 3** hello EBOD 모듈 래치 닫기</span><span class="sxs-lookup"><span data-stu-id="929a7-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="929a7-159">Hello 케이블 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-159">Reconnect hello cables.</span></span> <span data-ttu-id="929a7-160">Hello hello 교체 하기 전에 있었던 정확한 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="929a7-161">Hello 다이어그램을 다음 참조 및 방법에 대 한 세부 정보에 대 한 테이블 tooconnect hello 케이블 합니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![전원에 4U 장치를 케이블로 연결](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="929a7-163">**그림 4**.</span><span class="sxs-lookup"><span data-stu-id="929a7-163">**Figure 4**.</span></span> <span data-ttu-id="929a7-164">케이블 다시 연결</span><span class="sxs-lookup"><span data-stu-id="929a7-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="929a7-165">레이블</span><span class="sxs-lookup"><span data-stu-id="929a7-165">Label</span></span> | <span data-ttu-id="929a7-166">설명</span><span class="sxs-lookup"><span data-stu-id="929a7-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="929a7-167">1</span><span class="sxs-lookup"><span data-stu-id="929a7-167">1</span></span> |<span data-ttu-id="929a7-168">기본 인클로저</span><span class="sxs-lookup"><span data-stu-id="929a7-168">Primary enclosure</span></span> |
   | <span data-ttu-id="929a7-169">2</span><span class="sxs-lookup"><span data-stu-id="929a7-169">2</span></span> |<span data-ttu-id="929a7-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="929a7-170">PCM 0</span></span> |
   | <span data-ttu-id="929a7-171">3</span><span class="sxs-lookup"><span data-stu-id="929a7-171">3</span></span> |<span data-ttu-id="929a7-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="929a7-172">PCM 1</span></span> |
   | <span data-ttu-id="929a7-173">4</span><span class="sxs-lookup"><span data-stu-id="929a7-173">4</span></span> |<span data-ttu-id="929a7-174">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="929a7-174">Controller 0</span></span> |
   | <span data-ttu-id="929a7-175">5</span><span class="sxs-lookup"><span data-stu-id="929a7-175">5</span></span> |<span data-ttu-id="929a7-176">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="929a7-176">Controller 1</span></span> |
   | <span data-ttu-id="929a7-177">6</span><span class="sxs-lookup"><span data-stu-id="929a7-177">6</span></span> |<span data-ttu-id="929a7-178">EBOD 컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="929a7-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="929a7-179">7</span><span class="sxs-lookup"><span data-stu-id="929a7-179">7</span></span> |<span data-ttu-id="929a7-180">EBOD 컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="929a7-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="929a7-181">8</span><span class="sxs-lookup"><span data-stu-id="929a7-181">8</span></span> |<span data-ttu-id="929a7-182">EBOD 인클로저</span><span class="sxs-lookup"><span data-stu-id="929a7-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="929a7-183">9</span><span class="sxs-lookup"><span data-stu-id="929a7-183">9</span></span> |<span data-ttu-id="929a7-184">전력 분배 장치</span><span class="sxs-lookup"><span data-stu-id="929a7-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="929a7-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="929a7-185">Next steps</span></span>
<span data-ttu-id="929a7-186">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="929a7-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

