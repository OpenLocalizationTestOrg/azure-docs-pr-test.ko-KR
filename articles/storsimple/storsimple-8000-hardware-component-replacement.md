---
title: "StorSimple 8000 시리즈 하드웨어 구성 요소 교체 | Microsoft Docs"
description: "StorSimple 장치의 PCM, 배터리, 컨트롤러 모듈, EBOD 컨트롤러, 디스크 드라이브 및 섀시를 안전하게 교체하는 방법을 설명합니다."
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
ms.custom: 
ms.openlocfilehash: 6de50c5031db59176bdf17ecc69b934559220f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a><span data-ttu-id="ca383-103">StorSimple 8000 시리즈 장치에서 하드웨어 구성 요소 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-103">Replace a hardware component on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="ca383-104">개요</span><span class="sxs-lookup"><span data-stu-id="ca383-104">Overview</span></span>
<span data-ttu-id="ca383-105">하드웨어 구성 요소 교체 자습서에서는 Microsoft Azure StorSimple 8000 시리즈 장치의 하드웨어 구성 요소 및 구성 요소를 꺼내고 교체하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-105">The hardware component replacement tutorials describe the hardware components of your Microsoft Azure StorSimple 8000 series device and the steps necessary to remove and replace them.</span></span> <span data-ttu-id="ca383-106">이 문서에서는 안전 아이콘을 설명하고, 자세한 자습서에 대한 포인터를 제공하고, 교체 가능한 구성 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-106">This article describes the safety icons, provides pointers to the detailed tutorials, and lists the components that are replaceable.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca383-107">StorSimple 구성 요소를 제거하거나 교체하기 전에 [안전성 아이콘 표시 규칙](#safety-icon-conventions) 및 기타 [안전 주의 사항](storsimple-safety.md)을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-107">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>


### <a name="safety-icon-conventions"></a><span data-ttu-id="ca383-108">안전성 아이콘 표시 규칙</span><span class="sxs-lookup"><span data-stu-id="ca383-108">Safety icon conventions</span></span>
<span data-ttu-id="ca383-109">다음 표에서는 이러한 자습서에서 사용된 안전성 아이콘에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-109">The following table describes the safety icons used in these tutorials.</span></span> <span data-ttu-id="ca383-110">장치 구성 요소를 꺼내고 교체하는 단계를 진행할 때 이러한 안전성 아이콘에 각별히 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="ca383-110">Pay close attention to these safety icons as you go through the steps to remove and replace device components.</span></span>

| <span data-ttu-id="ca383-111">아이콘</span><span class="sxs-lookup"><span data-stu-id="ca383-111">Icon</span></span> | <span data-ttu-id="ca383-112">텍스트</span><span class="sxs-lookup"><span data-stu-id="ca383-112">Text</span></span> | <span data-ttu-id="ca383-113">추가 정보</span><span class="sxs-lookup"><span data-stu-id="ca383-113">Additional information</span></span> |
|:--- |:--- |:--- |
| ![경고 아이콘](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="ca383-115">**위험!**</span><span class="sxs-lookup"><span data-stu-id="ca383-115">**DANGER!**</span></span> |<span data-ttu-id="ca383-116">피하지 않을 경우 사망 또는 심각한 부상을 당하는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-116">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="ca383-117">이 위험도 표시는 가장 극단적인 상황으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-117">This signal word is limited to the most extreme situations.</span></span> |
| ![경고 아이콘](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="ca383-119">**경고!**</span><span class="sxs-lookup"><span data-stu-id="ca383-119">**WARNING!**</span></span> |<span data-ttu-id="ca383-120">피하지 않을 경우 사망 또는 심각한 부상을 당할 수 있는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-120">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| ![주의 아이콘](./media/storsimple-hardware-component-replacement/Caution.png) |<span data-ttu-id="ca383-122">**주의!**</span><span class="sxs-lookup"><span data-stu-id="ca383-122">**CAUTION!**</span></span> |<span data-ttu-id="ca383-123">피하지 않을 경우 최소 또는 보통 수준의 부상을 당할 수 있는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-123">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| ![고지 아이콘](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |<span data-ttu-id="ca383-125">**고지:**</span><span class="sxs-lookup"><span data-stu-id="ca383-125">**NOTICE:**</span></span> |<span data-ttu-id="ca383-126">중요하지만 위험과 관련되지 않은 것으로 간주되는 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-126">Indicates information considered important, but not hazard-related.</span></span> |
| ![감전 아이콘](./media/storsimple-hardware-component-replacement/Electric.png) |<span data-ttu-id="ca383-128">**감전 위험**</span><span class="sxs-lookup"><span data-stu-id="ca383-128">**Electrical Shock Hazard**</span></span> |<span data-ttu-id="ca383-129">높은 전압을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-129">Indicates high voltage.</span></span> |
| ![무거운 무게 아이콘](./media/storsimple-hardware-component-replacement/Weight.png) |<span data-ttu-id="ca383-131">**무거운 무게**</span><span class="sxs-lookup"><span data-stu-id="ca383-131">**Heavy Weight**</span></span> | |
| ![사용자 서비스 가능 부품 없음 아이콘](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |<span data-ttu-id="ca383-133">**사용자 서비스 가능 부품 없음**</span><span class="sxs-lookup"><span data-stu-id="ca383-133">**No User Serviceable Parts**</span></span> |<span data-ttu-id="ca383-134">제대로 교육을 받지 않은 경우 액세스하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ca383-134">Do not access unless properly trained.</span></span> |
| ![지침 읽기 아이콘](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |<span data-ttu-id="ca383-136">**먼저 모든 지침 읽기**</span><span class="sxs-lookup"><span data-stu-id="ca383-136">**Read All Instructions First**</span></span> | |
| ![기울어짐 위험 아이콘](./media/storsimple-hardware-component-replacement/TipHazard.png) |<span data-ttu-id="ca383-138">**기울어짐 위험**</span><span class="sxs-lookup"><span data-stu-id="ca383-138">**Tip Hazard**</span></span> | |

### <a name="before-you-begin"></a><span data-ttu-id="ca383-139">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ca383-139">Before you begin</span></span>
<span data-ttu-id="ca383-140">이 자습서에서 사용된 안전성 아이콘 및 장치에 대한 안전성 정보를 숙지합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-140">Familiarize yourself with the safety information about your device and safety icons used in this tutorial.</span></span> <span data-ttu-id="ca383-141">자세한 내용을 보려면 [StorSimple 장치의 안전한 설치 및 작동](storsimple-safety.md) 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-141">Go to [Safely install and operate your StorSimple device](storsimple-safety.md) for complete information.</span></span> <span data-ttu-id="ca383-142">StorSimple 장치를 처리하기 전에 [안전 주의 사항](storsimple-safety.md#handling-precautions) 을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-142">Be sure to review the [Safety precautions](storsimple-safety.md#handling-precautions) before you handle your StorSimple device.</span></span>

<span data-ttu-id="ca383-143">구성 요소를 교체하기 전에 다음 정보를 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="ca383-143">Before you attempt to replace a component, consider the following information.</span></span>

<span data-ttu-id="ca383-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="ca383-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **WARNING!**</span></span>

* <span data-ttu-id="ca383-145">StorSimple 장치의 모듈 및 구성 요소를 처리할 때 정전기 방전 또는 정전기 방지 매트를 사용하여 올바르게 접지합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-145">Ground yourself properly by using an electrostatic discharge or antistatic mat when handling modules and components of your StorSimple device.</span></span>
* <span data-ttu-id="ca383-146">회로를 만지지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ca383-146">Do not touch any circuitry.</span></span> <span data-ttu-id="ca383-147">노출된 회로가 있을 수 있는 구성 요소를 처리할 때는 제공된 핸들 및 가이드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-147">Use the supplied handles and guides while handling components that may have exposed circuitry.</span></span>

<span data-ttu-id="ca383-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="ca383-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **NOTICE:**</span></span>

<span data-ttu-id="ca383-149">모듈을 교체하는 경우 **엔클로저 뒷면에 빈 베이를 남기지 마세요**.</span><span class="sxs-lookup"><span data-stu-id="ca383-149">When you replace a module, **NEVER leave an empty bay in the rear of the enclosure**.</span></span> <span data-ttu-id="ca383-150">문제 부품을 꺼내기 전에 교체 또는 빈 모듈을 구합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-150">Obtain a replacement or blank module before removing the problem part.</span></span>

## <a name="hardware-component-replacement-procedures"></a><span data-ttu-id="ca383-151">하드웨어 구성 요소 교체 절차</span><span class="sxs-lookup"><span data-stu-id="ca383-151">Hardware component replacement procedures</span></span>
<span data-ttu-id="ca383-152">StorSimple 8000 시리즈 장치는 기본 및/또는 EBOD 엔클로저의 여러 플러그 인 모듈로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-152">Your StorSimple 8000 series device consists of several plug-in modules in the primary and/or EBOD enclosures.</span></span> <span data-ttu-id="ca383-153">8100에는 단일 기본 엔클로저가 있는 반면 8600은 기본 엔클로저와 EBOD 엔클로저가 있는 이중 엔클로저 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-153">The 8100 has a single primary enclosure, whereas the 8600 is a dual enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

<span data-ttu-id="ca383-154">장치의 기본 하드웨어 구성 요소는 다음 표에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-154">The main hardware components in your device are summarized in the following tables.</span></span> <span data-ttu-id="ca383-155">**교체 절차** 열에 있는 링크를 클릭하면 연결된 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-155">Click the link in the **Replacement procedure** column to go to the associated tutorial.</span></span>

| <span data-ttu-id="ca383-156">구성 요소</span><span class="sxs-lookup"><span data-stu-id="ca383-156">Components</span></span> | <span data-ttu-id="ca383-157">현재 개수</span><span class="sxs-lookup"><span data-stu-id="ca383-157"># Present</span></span> | <span data-ttu-id="ca383-158">플러그 인 모듈 여부</span><span class="sxs-lookup"><span data-stu-id="ca383-158">Plug-in module?</span></span> | <span data-ttu-id="ca383-159">교체 절차</span><span class="sxs-lookup"><span data-stu-id="ca383-159">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ca383-160">섀시</span><span class="sxs-lookup"><span data-stu-id="ca383-160">Chassis</span></span> |<span data-ttu-id="ca383-161">1</span><span class="sxs-lookup"><span data-stu-id="ca383-161">1</span></span> |<span data-ttu-id="ca383-162">아니요</span><span class="sxs-lookup"><span data-stu-id="ca383-162">No</span></span> |[<span data-ttu-id="ca383-163">StorSimple 장치의 섀시 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-163">Replace the chassis on your StorSimple device</span></span>](storsimple-8000-chassis-replacement.md) |
| <span data-ttu-id="ca383-164">기본 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="ca383-164">Primary controllers</span></span> |<span data-ttu-id="ca383-165">2</span><span class="sxs-lookup"><span data-stu-id="ca383-165">2</span></span> |<span data-ttu-id="ca383-166">예</span><span class="sxs-lookup"><span data-stu-id="ca383-166">Yes</span></span> |[<span data-ttu-id="ca383-167">StorSimple 장치의 컨트롤러 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-167">Replace a controller module on your StorSimple device</span></span>](storsimple-8000-controller-replacement.md) |
| <span data-ttu-id="ca383-168">764W PCM(전원 및 냉각 모듈)</span><span class="sxs-lookup"><span data-stu-id="ca383-168">764W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="ca383-169">2</span><span class="sxs-lookup"><span data-stu-id="ca383-169">2</span></span> |<span data-ttu-id="ca383-170">예</span><span class="sxs-lookup"><span data-stu-id="ca383-170">Yes</span></span> |[<span data-ttu-id="ca383-171">StorSimple 장치의 전원 및 냉각 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-171">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-8000-power-cooling-module-replacement.md) |
| <span data-ttu-id="ca383-172">백업 배터리</span><span class="sxs-lookup"><span data-stu-id="ca383-172">Backup battery</span></span> |<span data-ttu-id="ca383-173">2</span><span class="sxs-lookup"><span data-stu-id="ca383-173">2</span></span> |<span data-ttu-id="ca383-174">예</span><span class="sxs-lookup"><span data-stu-id="ca383-174">Yes</span></span> |[<span data-ttu-id="ca383-175">StorSimple 장치의 백업 배터리 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-175">Replace the backup battery module on your StorSimple device</span></span>](storsimple-8000-battery-replacement.md) |
| <span data-ttu-id="ca383-176">디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="ca383-176">Disk drives</span></span> |<span data-ttu-id="ca383-177">12</span><span class="sxs-lookup"><span data-stu-id="ca383-177">12</span></span> |<span data-ttu-id="ca383-178">예</span><span class="sxs-lookup"><span data-stu-id="ca383-178">Yes</span></span> |[<span data-ttu-id="ca383-179">StorSimple 장치의 디스크 드라이브 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-179">Replace a disk drive on your StorSimple device</span></span>](storsimple-8000-disk-drive-replacement.md) |

<span data-ttu-id="ca383-180">**표 1** 기본 엔클로저의 하드웨어 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ca383-180">**Table 1** Hardware components in the primary enclosure</span></span>

<span data-ttu-id="ca383-181">기본 엔클로저와 EBOD 엔클로저는 해당 I/O 모듈이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-181">The primary enclosure and the EBOD enclosure differ in their I/O modules.</span></span> <span data-ttu-id="ca383-182">또한 PCM의 전력량이 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-182">Additionally, the PCMs have different wattage.</span></span> <span data-ttu-id="ca383-183">기본 엔클로저의 PCM은 764W인 반면, EBOD 엔클로저의 PCM은 580W입니다. 기본 엔클로저의 PCM에는 백업 배터리 모듈도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-183">The PCMs in the primary enclosure are 764 W, whereas those in the EBOD enclosure are 580 W. The PCMs in the primary enclosure also contain a backup battery module.</span></span>

| <span data-ttu-id="ca383-184">구성 요소</span><span class="sxs-lookup"><span data-stu-id="ca383-184">Components</span></span> | <span data-ttu-id="ca383-185">현재 개수</span><span class="sxs-lookup"><span data-stu-id="ca383-185"># Present</span></span> | <span data-ttu-id="ca383-186">플러그 인 모듈 여부</span><span class="sxs-lookup"><span data-stu-id="ca383-186">Plug-in module?</span></span> | <span data-ttu-id="ca383-187">교체 절차</span><span class="sxs-lookup"><span data-stu-id="ca383-187">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ca383-188">섀시</span><span class="sxs-lookup"><span data-stu-id="ca383-188">Chassis</span></span> |<span data-ttu-id="ca383-189">1</span><span class="sxs-lookup"><span data-stu-id="ca383-189">1</span></span> |<span data-ttu-id="ca383-190">아니요</span><span class="sxs-lookup"><span data-stu-id="ca383-190">No</span></span> |[<span data-ttu-id="ca383-191">StorSimple 장치의 섀시 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-191">Replace the chassis on your StorSimple device</span></span>](storsimple-8000-chassis-replacement.md) |
| <span data-ttu-id="ca383-192">EBOD 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="ca383-192">EBOD controllers</span></span> |<span data-ttu-id="ca383-193">2</span><span class="sxs-lookup"><span data-stu-id="ca383-193">2</span></span> |<span data-ttu-id="ca383-194">예</span><span class="sxs-lookup"><span data-stu-id="ca383-194">Yes</span></span> |[<span data-ttu-id="ca383-195">StorSimple 장치의 EBOD 컨트롤러 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-195">Replace an EBOD controller on your StorSimple device</span></span>](storsimple-8000-ebod-controller-replacement.md) |
| <span data-ttu-id="ca383-196">580W PCM(전원 및 냉각 모듈)</span><span class="sxs-lookup"><span data-stu-id="ca383-196">580W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="ca383-197">2</span><span class="sxs-lookup"><span data-stu-id="ca383-197">2</span></span> |<span data-ttu-id="ca383-198">예</span><span class="sxs-lookup"><span data-stu-id="ca383-198">Yes</span></span> |[<span data-ttu-id="ca383-199">StorSimple 장치의 전원 및 냉각 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-199">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-8000-power-cooling-module-replacement.md) |
| <span data-ttu-id="ca383-200">디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="ca383-200">Disk drives</span></span> |<span data-ttu-id="ca383-201">12</span><span class="sxs-lookup"><span data-stu-id="ca383-201">12</span></span> |<span data-ttu-id="ca383-202">예</span><span class="sxs-lookup"><span data-stu-id="ca383-202">Yes</span></span> |[<span data-ttu-id="ca383-203">StorSimple 장치의 디스크 드라이브 교체</span><span class="sxs-lookup"><span data-stu-id="ca383-203">Replace a disk drive on your StorSimple device</span></span>](storsimple-8000-disk-drive-replacement.md) |

<span data-ttu-id="ca383-204">**표 2** EBOD 엔클로저의 하드웨어 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ca383-204">**Table 2** Hardware components in the EBOD enclosure</span></span>

<span data-ttu-id="ca383-205">장치의 플러그 인 모듈은 다음 앞면 및 뒷면 다이어그램에서 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-205">The plug-in modules on the device are highlighted in the following front and rear diagrams.</span></span> <span data-ttu-id="ca383-206">교체가 필요한 경우 이러한 다이어그램을 사용하여 다양한 플러그 인 모듈의 위치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-206">You can use these diagrams to determine the location of the various plug-in modules if a replacement is required.</span></span> <span data-ttu-id="ca383-207">앞면 다이어그램에는 디스크 드라이브가 표시되고, EBOD 엔클로저 및 기본 엔클로저의 뒷면 다이어그램에는 플러그 인 모듈이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-207">The front diagram shows the disk drives, and the rear diagrams of the EBOD enclosure and the primary enclosure show the plug-in modules.</span></span>

![디스크 드라이브가 있는 장치의 프런트플레인](./media/storsimple-hardware-component-replacement/IC741028.png)

<span data-ttu-id="ca383-209">**그림 1** 장치 앞면</span><span class="sxs-lookup"><span data-stu-id="ca383-209">**Figure 1** Front of the device</span></span>

| <span data-ttu-id="ca383-210">레이블</span><span class="sxs-lookup"><span data-stu-id="ca383-210">Label</span></span> | <span data-ttu-id="ca383-211">설명</span><span class="sxs-lookup"><span data-stu-id="ca383-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ca383-212">0 - 11</span><span class="sxs-lookup"><span data-stu-id="ca383-212">0 - 11</span></span> |<span data-ttu-id="ca383-213">디스크 드라이브(총 12개)</span><span class="sxs-lookup"><span data-stu-id="ca383-213">Disk drives (total of 12)</span></span> |

<span data-ttu-id="ca383-214">기본 엔클로저와 EBOD 엔클로저에 모두 드라이브 캐리어 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-214">Both the primary enclosure and the EBOD enclosure have drive carrier modules.</span></span> <span data-ttu-id="ca383-215">섀시에는 3.5" 디스크 드라이브 12개가 3X4 형식으로 정렬되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-215">The chassis houses twelve 3.5" disk drives arranged in a 3 by 4 format.</span></span>

![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-hardware-component-replacement/IC740994.png)

<span data-ttu-id="ca383-217">**그림 2** 기본 엔클로저 뒷면</span><span class="sxs-lookup"><span data-stu-id="ca383-217">**Figure 2** Back of the primary enclosure</span></span>

| <span data-ttu-id="ca383-218">레이블</span><span class="sxs-lookup"><span data-stu-id="ca383-218">Label</span></span> | <span data-ttu-id="ca383-219">설명</span><span class="sxs-lookup"><span data-stu-id="ca383-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ca383-220">1</span><span class="sxs-lookup"><span data-stu-id="ca383-220">1</span></span> |<span data-ttu-id="ca383-221">PCM 0</span><span class="sxs-lookup"><span data-stu-id="ca383-221">PCM 0</span></span> |
| <span data-ttu-id="ca383-222">2</span><span class="sxs-lookup"><span data-stu-id="ca383-222">2</span></span> |<span data-ttu-id="ca383-223">PCM 1</span><span class="sxs-lookup"><span data-stu-id="ca383-223">PCM 1</span></span> |
| <span data-ttu-id="ca383-224">3</span><span class="sxs-lookup"><span data-stu-id="ca383-224">3</span></span> |<span data-ttu-id="ca383-225">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="ca383-225">Controller 0</span></span> |
| <span data-ttu-id="ca383-226">4</span><span class="sxs-lookup"><span data-stu-id="ca383-226">4</span></span> |<span data-ttu-id="ca383-227">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="ca383-227">Controller 1</span></span> |

![장치 EBOD 엔클로저 플러그 인 모듈의 백플레인](./media/storsimple-hardware-component-replacement/IC769599.png)

<span data-ttu-id="ca383-229">**그림 3** EBOD 엔클로저 뒷면</span><span class="sxs-lookup"><span data-stu-id="ca383-229">**Figure 3** Back of the EBOD enclosure</span></span>

| <span data-ttu-id="ca383-230">레이블</span><span class="sxs-lookup"><span data-stu-id="ca383-230">Label</span></span> | <span data-ttu-id="ca383-231">설명</span><span class="sxs-lookup"><span data-stu-id="ca383-231">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ca383-232">1</span><span class="sxs-lookup"><span data-stu-id="ca383-232">1</span></span> |<span data-ttu-id="ca383-233">PCM 0</span><span class="sxs-lookup"><span data-stu-id="ca383-233">PCM 0</span></span> |
| <span data-ttu-id="ca383-234">2</span><span class="sxs-lookup"><span data-stu-id="ca383-234">2</span></span> |<span data-ttu-id="ca383-235">PCM 1</span><span class="sxs-lookup"><span data-stu-id="ca383-235">PCM 1</span></span> |
| <span data-ttu-id="ca383-236">3</span><span class="sxs-lookup"><span data-stu-id="ca383-236">3</span></span> |<span data-ttu-id="ca383-237">EBOD 컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="ca383-237">EBOD Controller 0</span></span> |
| <span data-ttu-id="ca383-238">4</span><span class="sxs-lookup"><span data-stu-id="ca383-238">4</span></span> |<span data-ttu-id="ca383-239">EBOD 컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="ca383-239">EBOD Controller 1</span></span> |

## <a name="field-replaceable-units"></a><span data-ttu-id="ca383-240">FRU(필드 교체 장치)</span><span class="sxs-lookup"><span data-stu-id="ca383-240">Field replaceable units</span></span>
<span data-ttu-id="ca383-241">StorSimple 장치에 사용할 수 있는 FRU(필드 교체 장치)는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca383-241">The following field replaceable units (FRUs) are available for your StorSimple device:</span></span>

* <span data-ttu-id="ca383-242">섀시(통합 작업 패널 포함)</span><span class="sxs-lookup"><span data-stu-id="ca383-242">Chassis (including the integrated operations panel)</span></span>
* <span data-ttu-id="ca383-243">764 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="ca383-243">764 W AC PCM</span></span>
* <span data-ttu-id="ca383-244">580 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="ca383-244">580 W AC PCM</span></span>
* <span data-ttu-id="ca383-245">드라이브 캐리어 모듈이 있는 하드 디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="ca383-245">Hard disk drive with drive carrier module</span></span>
* <span data-ttu-id="ca383-246">컨트롤러 모듈</span><span class="sxs-lookup"><span data-stu-id="ca383-246">Controller module</span></span>
* <span data-ttu-id="ca383-247">EBOD 컨트롤러 모듈</span><span class="sxs-lookup"><span data-stu-id="ca383-247">EBOD controller module</span></span>
* <span data-ttu-id="ca383-248">백업 배터리 모듈</span><span class="sxs-lookup"><span data-stu-id="ca383-248">Backup battery module</span></span>
* <span data-ttu-id="ca383-249">랙 탑재 레일 키트</span><span class="sxs-lookup"><span data-stu-id="ca383-249">Rack mounting rail kit</span></span>

<span data-ttu-id="ca383-250">교체 장치를 주문하려면 [Microsoft 지원에 문의](storsimple-8000-contact-microsoft-support.md) 하세요.</span><span class="sxs-lookup"><span data-stu-id="ca383-250">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order any of these replacement units.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca383-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca383-251">Next steps</span></span>
<span data-ttu-id="ca383-252">StorSimple 하드웨어 구성 요소를 교체하기 전에 모든 [안전 정보](storsimple-safety.md) 를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="ca383-252">Review all [safety information](storsimple-safety.md) before you attempt to replace a StorSimple hardware component.</span></span>

