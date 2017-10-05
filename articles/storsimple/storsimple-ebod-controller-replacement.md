---
title: "StorSimple EBOD 컨트롤러 교체 | Microsoft Docs"
description: "StorSimple 8600 장치에서 하나 또는 두 개의 EBOD 컨트롤러를 모두 꺼내고 교체하는 방법을 설명합니다."
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
ms.openlocfilehash: 23d819ddc3bbcbaf2847cdcc9191407ead0ff43d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="172d7-103">StorSimple 장치의 EBOD 컨트롤러 교체</span><span class="sxs-lookup"><span data-stu-id="172d7-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="172d7-104">개요</span><span class="sxs-lookup"><span data-stu-id="172d7-104">Overview</span></span>
<span data-ttu-id="172d7-105">이 자습서에서는 Microsoft Azure StorSimple 장치에서 결함이 있는 EBOD 컨트롤러 모듈을 교체하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="172d7-106">EBOD 컨트롤러 모듈을 교체하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="172d7-107">결함이 있는 EBOD 컨트롤러 꺼내기</span><span class="sxs-lookup"><span data-stu-id="172d7-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="172d7-108">새 EBOD 컨트롤러 설치</span><span class="sxs-lookup"><span data-stu-id="172d7-108">Install a new EBOD controller</span></span>

<span data-ttu-id="172d7-109">시작하기 전에 다음 정보를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="172d7-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="172d7-110">사용하지 않은 모든 슬롯에 빈 EBOD 모듈을 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="172d7-111">슬롯이 열려 있으면 엔클로저가 제대로 냉각되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="172d7-112">EBOD 컨트롤러는 핫 스왑이 가능하며 꺼내거나 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="172d7-113">교체가 있을 때까지 오류가 발생한 모듈을 꺼내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="172d7-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="172d7-114">교체 프로세스를 시작하는 경우 10분 내에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="172d7-115">StorSimple 구성 요소를 제거하거나 교체하기 전에 [안전성 아이콘 표시 규칙](storsimple-safety.md#safety-icon-conventions) 및 기타 [안전 주의 사항](storsimple-safety.md)을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="172d7-116">EBOD 컨트롤러 꺼내기</span><span class="sxs-lookup"><span data-stu-id="172d7-116">Remove an EBOD controller</span></span>
<span data-ttu-id="172d7-117">StorSimple 장치에서 오류가 발생한 EBOD 컨트롤러 모듈을 교체하기 전에 다른 EBOD 컨트롤러 모듈이 활성화되어 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="172d7-118">다음 절차와 표에서는 EBOD 컨트롤러 모듈을 꺼내는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="172d7-119">EBOD 모듈을 꺼내려면</span><span class="sxs-lookup"><span data-stu-id="172d7-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="172d7-120">Azure 클래식 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="172d7-121">**장치** > **유지 관리** > **하드웨어 상태**로 이동한 다음 활성 EBOD 컨트롤러 모듈의 LED 상태가 녹색이고 오류가 발생한 EBOD 컨트롤러 모듈의 LED가 빨간색인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="172d7-122">장치 뒷면에서 오류가 발생한 EBOD 컨트롤러 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="172d7-123">시스템에서 EBOD 모듈을 꺼내기 전에 EBOD 컨트롤러 모듈을 컨트롤러에 연결하는 케이블을 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="172d7-124">컨트롤러에 연결된 EBOD 컨트롤러 모듈의 SAS 포트를 정확하게 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="172d7-125">EBOD 모듈을 교체한 후 시스템을 이 구성으로 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="172d7-126">일반적으로 포트 A이며, 다음 다이어그램에서는 **호스트 인** 으로 레이블이 붙어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![EBOD 컨트롤러의 백플레인](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="172d7-128">**그림 1** EBOD 모듈 뒷면</span><span class="sxs-lookup"><span data-stu-id="172d7-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="172d7-129">레이블</span><span class="sxs-lookup"><span data-stu-id="172d7-129">Label</span></span> | <span data-ttu-id="172d7-130">설명</span><span class="sxs-lookup"><span data-stu-id="172d7-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="172d7-131">1</span><span class="sxs-lookup"><span data-stu-id="172d7-131">1</span></span> |<span data-ttu-id="172d7-132">오류 LED</span><span class="sxs-lookup"><span data-stu-id="172d7-132">Fault LED</span></span> |
   | <span data-ttu-id="172d7-133">2</span><span class="sxs-lookup"><span data-stu-id="172d7-133">2</span></span> |<span data-ttu-id="172d7-134">전원 LED</span><span class="sxs-lookup"><span data-stu-id="172d7-134">Power LED</span></span> |
   | <span data-ttu-id="172d7-135">3</span><span class="sxs-lookup"><span data-stu-id="172d7-135">3</span></span> |<span data-ttu-id="172d7-136">SAS 커넥터</span><span class="sxs-lookup"><span data-stu-id="172d7-136">SAS connectors</span></span> |
   | <span data-ttu-id="172d7-137">4</span><span class="sxs-lookup"><span data-stu-id="172d7-137">4</span></span> |<span data-ttu-id="172d7-138">SAS LED</span><span class="sxs-lookup"><span data-stu-id="172d7-138">SAS LEDs</span></span> |
   | <span data-ttu-id="172d7-139">5</span><span class="sxs-lookup"><span data-stu-id="172d7-139">5</span></span> |<span data-ttu-id="172d7-140">팩터리 전용 직렬 포트</span><span class="sxs-lookup"><span data-stu-id="172d7-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="172d7-141">6</span><span class="sxs-lookup"><span data-stu-id="172d7-141">6</span></span> |<span data-ttu-id="172d7-142">포트 A(호스트 인)</span><span class="sxs-lookup"><span data-stu-id="172d7-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="172d7-143">7</span><span class="sxs-lookup"><span data-stu-id="172d7-143">7</span></span> |<span data-ttu-id="172d7-144">포트 B(호스트 아웃)</span><span class="sxs-lookup"><span data-stu-id="172d7-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="172d7-145">8</span><span class="sxs-lookup"><span data-stu-id="172d7-145">8</span></span> |<span data-ttu-id="172d7-146">포트 C(팩터리 전용)</span><span class="sxs-lookup"><span data-stu-id="172d7-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="172d7-147">새 EBOD 컨트롤러 설치</span><span class="sxs-lookup"><span data-stu-id="172d7-147">Install a new EBOD controller</span></span>
<span data-ttu-id="172d7-148">다음 절차와 표에서는 StorSimple 장치에 EBOD 컨트롤러 모듈을 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="172d7-149">EBOD 컨트롤러를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="172d7-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="172d7-150">EBOD 장치에서 특히 인터페이스 커넥터에 손상된 부분이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="172d7-151">핀이 구부러진 경우 새 EBOD 컨트롤러를 설치하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="172d7-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="172d7-152">래치를 열린 위치에 놓고 래치가 걸릴 때까지 모듈을 엔클로저에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![EBOD 컨트롤러 설치](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="172d7-154">**그림 2** EBOD 컨트롤러 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="172d7-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="172d7-155">래치를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-155">Close the latch.</span></span> <span data-ttu-id="172d7-156">래치가 걸리면 딸깍하는 소리가 들립니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-156">You should hear a click as the latch engages.</span></span>
   
    ![EBOD 래치 해제](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="172d7-158">**그림 3** EBOD 모듈 래치 닫기</span><span class="sxs-lookup"><span data-stu-id="172d7-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="172d7-159">케이블을 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-159">Reconnect the cables.</span></span> <span data-ttu-id="172d7-160">교체 전에 있던 구성을 정확하게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="172d7-161">케이블을 연결하는 방법에 대한 자세한 내용은 다음 다이어그램과 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="172d7-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![전원에 4U 장치를 케이블로 연결](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="172d7-163">**그림 4**.</span><span class="sxs-lookup"><span data-stu-id="172d7-163">**Figure 4**.</span></span> <span data-ttu-id="172d7-164">케이블 다시 연결</span><span class="sxs-lookup"><span data-stu-id="172d7-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="172d7-165">레이블</span><span class="sxs-lookup"><span data-stu-id="172d7-165">Label</span></span> | <span data-ttu-id="172d7-166">설명</span><span class="sxs-lookup"><span data-stu-id="172d7-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="172d7-167">1</span><span class="sxs-lookup"><span data-stu-id="172d7-167">1</span></span> |<span data-ttu-id="172d7-168">기본 인클로저</span><span class="sxs-lookup"><span data-stu-id="172d7-168">Primary enclosure</span></span> |
   | <span data-ttu-id="172d7-169">2</span><span class="sxs-lookup"><span data-stu-id="172d7-169">2</span></span> |<span data-ttu-id="172d7-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="172d7-170">PCM 0</span></span> |
   | <span data-ttu-id="172d7-171">3</span><span class="sxs-lookup"><span data-stu-id="172d7-171">3</span></span> |<span data-ttu-id="172d7-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="172d7-172">PCM 1</span></span> |
   | <span data-ttu-id="172d7-173">4</span><span class="sxs-lookup"><span data-stu-id="172d7-173">4</span></span> |<span data-ttu-id="172d7-174">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="172d7-174">Controller 0</span></span> |
   | <span data-ttu-id="172d7-175">5</span><span class="sxs-lookup"><span data-stu-id="172d7-175">5</span></span> |<span data-ttu-id="172d7-176">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="172d7-176">Controller 1</span></span> |
   | <span data-ttu-id="172d7-177">6</span><span class="sxs-lookup"><span data-stu-id="172d7-177">6</span></span> |<span data-ttu-id="172d7-178">EBOD 컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="172d7-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="172d7-179">7</span><span class="sxs-lookup"><span data-stu-id="172d7-179">7</span></span> |<span data-ttu-id="172d7-180">EBOD 컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="172d7-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="172d7-181">8</span><span class="sxs-lookup"><span data-stu-id="172d7-181">8</span></span> |<span data-ttu-id="172d7-182">EBOD 인클로저</span><span class="sxs-lookup"><span data-stu-id="172d7-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="172d7-183">9</span><span class="sxs-lookup"><span data-stu-id="172d7-183">9</span></span> |<span data-ttu-id="172d7-184">전력 분배 장치</span><span class="sxs-lookup"><span data-stu-id="172d7-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="172d7-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="172d7-185">Next steps</span></span>
<span data-ttu-id="172d7-186">[StorSimple 하드웨어 구성 요소 교체](storsimple-hardware-component-replacement.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="172d7-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

