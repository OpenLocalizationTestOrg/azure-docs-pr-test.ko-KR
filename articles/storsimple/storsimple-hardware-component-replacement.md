---
title: "하드웨어 구성 요소 교체 aaaStorSimple | Microsoft Docs"
description: "Toosafely hello Pcm, 배터리, 컨트롤러 모듈, EBOD 컨트롤러, 디스크 드라이브 및 StorSimple 장치의 섀시 교체 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e8087ba7-0b66-4f59-8988-e53aad52ee21
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 472d9dc1c31b61550fe079cc9b9419510487db3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a><span data-ttu-id="36f16-103">StorSimple 8000 시리즈 장치에서 하드웨어 구성 요소 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-103">Replace a hardware component on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="36f16-104">개요</span><span class="sxs-lookup"><span data-stu-id="36f16-104">Overview</span></span>
<span data-ttu-id="36f16-105">hello 하드웨어 구성 요소 교체 자습서에 Microsoft Azure StorSimple 8000 시리즈 장치와 hello 단계 필요한 tooremove hello 하드웨어 구성 요소에 설명 하 고 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="36f16-105">hello hardware component replacement tutorials describe hello hardware components of your Microsoft Azure StorSimple 8000 series device and hello steps necessary tooremove and replace them.</span></span> <span data-ttu-id="36f16-106">이 문서에 hello 안전 아이콘에 설명 하는 팁을 제공 하 고 목록 hello는 교체 될 수 있는 구성 요소는 toohello 자세한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-106">This article describes hello safety icons, provides pointers toohello detailed tutorials, and lists hello components that are replaceable.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36f16-107">Tooremove 시도 하기 전에 모든 StorSimple 구성 요소 교체, hello 검토 해야 또는 [안전 아이콘 규칙](#safety-icon-conventions) 및 기타 [안전 조치](storsimple-safety.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-107">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

### <a name="safety-icon-conventions"></a><span data-ttu-id="36f16-108">안전성 아이콘 표시 규칙</span><span class="sxs-lookup"><span data-stu-id="36f16-108">Safety icon conventions</span></span>
<span data-ttu-id="36f16-109">hello 다음 표에 이러한 자습서에 사용 된 hello 안전 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-109">hello following table describes hello safety icons used in these tutorials.</span></span> <span data-ttu-id="36f16-110">살펴보아야 toothese 안전 아이콘 hello 단계 tooremove를 통해 이동 하 고 장치 구성 요소를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-110">Pay close attention toothese safety icons as you go through hello steps tooremove and replace device components.</span></span>

| <span data-ttu-id="36f16-111">아이콘</span><span class="sxs-lookup"><span data-stu-id="36f16-111">Icon</span></span> | <span data-ttu-id="36f16-112">텍스트</span><span class="sxs-lookup"><span data-stu-id="36f16-112">Text</span></span> | <span data-ttu-id="36f16-113">추가 정보</span><span class="sxs-lookup"><span data-stu-id="36f16-113">Additional information</span></span> |
|:--- |:--- |:--- |
| ![경고 아이콘](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="36f16-115">**위험!**</span><span class="sxs-lookup"><span data-stu-id="36f16-115">**DANGER!**</span></span> |<span data-ttu-id="36f16-116">피하지 않을 경우 사망 또는 심각한 부상을 당하는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-116">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="36f16-117">이 신호 단어는 제한 된 toohello 가장 극단적인 상황입니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-117">This signal word is limited toohello most extreme situations.</span></span> |
| ![경고 아이콘](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="36f16-119">**경고!**</span><span class="sxs-lookup"><span data-stu-id="36f16-119">**WARNING!**</span></span> |<span data-ttu-id="36f16-120">피하지 않을 경우 사망 또는 심각한 부상을 당할 수 있는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-120">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| ![주의 아이콘](./media/storsimple-hardware-component-replacement/Caution.png) |<span data-ttu-id="36f16-122">**주의!**</span><span class="sxs-lookup"><span data-stu-id="36f16-122">**CAUTION!**</span></span> |<span data-ttu-id="36f16-123">피하지 않을 경우 최소 또는 보통 수준의 부상을 당할 수 있는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-123">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| ![고지 아이콘](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |<span data-ttu-id="36f16-125">**고지:**</span><span class="sxs-lookup"><span data-stu-id="36f16-125">**NOTICE:**</span></span> |<span data-ttu-id="36f16-126">중요하지만 위험과 관련되지 않은 것으로 간주되는 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-126">Indicates information considered important, but not hazard-related.</span></span> |
| ![감전 아이콘](./media/storsimple-hardware-component-replacement/Electric.png) |<span data-ttu-id="36f16-128">**감전 위험**</span><span class="sxs-lookup"><span data-stu-id="36f16-128">**Electrical Shock Hazard**</span></span> |<span data-ttu-id="36f16-129">높은 전압을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-129">Indicates high voltage.</span></span> |
| ![무거운 무게 아이콘](./media/storsimple-hardware-component-replacement/Weight.png) |<span data-ttu-id="36f16-131">**무거운 무게**</span><span class="sxs-lookup"><span data-stu-id="36f16-131">**Heavy Weight**</span></span> | |
| ![사용자 서비스 가능 부품 없음 아이콘](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |<span data-ttu-id="36f16-133">**사용자 서비스 가능 부품 없음**</span><span class="sxs-lookup"><span data-stu-id="36f16-133">**No User Serviceable Parts**</span></span> |<span data-ttu-id="36f16-134">제대로 교육을 받지 않은 경우 액세스하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="36f16-134">Do not access unless properly trained.</span></span> |
| ![지침 읽기 아이콘](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |<span data-ttu-id="36f16-136">**먼저 모든 지침 읽기**</span><span class="sxs-lookup"><span data-stu-id="36f16-136">**Read All Instructions First**</span></span> | |
| ![기울어짐 위험 아이콘](./media/storsimple-hardware-component-replacement/TipHazard.png) |<span data-ttu-id="36f16-138">**기울어짐 위험**</span><span class="sxs-lookup"><span data-stu-id="36f16-138">**Tip Hazard**</span></span> | |

### <a name="before-you-begin"></a><span data-ttu-id="36f16-139">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="36f16-139">Before you begin</span></span>
<span data-ttu-id="36f16-140">이 자습서에 사용 하 여 장치 및 안전 아이콘에 대 한 hello 안전 정보를 숙지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-140">Familiarize yourself with hello safety information about your device and safety icons used in this tutorial.</span></span> <span data-ttu-id="36f16-141">너무 이동[안전 하 게 설치 하 고 StorSimple 장치를 작동](storsimple-safety.md) 완전 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-141">Go too[Safely install and operate your StorSimple device](storsimple-safety.md) for complete information.</span></span> <span data-ttu-id="36f16-142">수 있는지 tooreview hello [안전 조치](storsimple-safety.md#handling-precautions) StorSimple 장치를 처리 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="36f16-142">Be sure tooreview hello [Safety precautions](storsimple-safety.md#handling-precautions) before you handle your StorSimple device.</span></span> 

<span data-ttu-id="36f16-143">Tooreplace 구성 요소를 시도 하기 전에 hello 다음 정보를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-143">Before you attempt tooreplace a component, consider hello following information.</span></span>

<span data-ttu-id="36f16-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="36f16-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **WARNING!**</span></span> 

* <span data-ttu-id="36f16-145">StorSimple 장치의 모듈 및 구성 요소를 처리할 때 정전기 방전 또는 정전기 방지 매트를 사용하여 올바르게 접지합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-145">Ground yourself properly by using an electrostatic discharge or antistatic mat when handling modules and components of your StorSimple device.</span></span>
* <span data-ttu-id="36f16-146">회로를 만지지 마세요.</span><span class="sxs-lookup"><span data-stu-id="36f16-146">Do not touch any circuitry.</span></span> <span data-ttu-id="36f16-147">회로가 노출 되었을 수 있는 구성 요소를 처리 하는 동안 제공 된 hello 핸들 및 가이드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-147">Use hello supplied handles and guides while handling components that may have exposed circuitry.</span></span>

<span data-ttu-id="36f16-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="36f16-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **NOTICE:**</span></span>

<span data-ttu-id="36f16-149">모듈을 교체할 때 **hello hello 인클로저 후면에 빈 베이 두어서는 안**합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-149">When you replace a module, **NEVER leave an empty bay in hello rear of hello enclosure**.</span></span> <span data-ttu-id="36f16-150">Hello 문제가 있는 부품을 제거 하기 전에 교체 모듈 또는 빈 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-150">Obtain a replacement or blank module before removing hello problem part.</span></span>

## <a name="hardware-component-replacement-procedures"></a><span data-ttu-id="36f16-151">하드웨어 구성 요소 교체 절차</span><span class="sxs-lookup"><span data-stu-id="36f16-151">Hardware component replacement procedures</span></span>
<span data-ttu-id="36f16-152">여러 기본 hello에 플러그 인 모듈 및/또는 EBOD 인클로저 StorSimple 8000 시리즈 장치 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-152">Your StorSimple 8000 series device consists of several plug-in modules in hello primary and/or EBOD enclosures.</span></span> <span data-ttu-id="36f16-153">8100 hello는 hello 8600는 기본 인클로저와 EBOD 인클로저가 있는 이중 인클로저 장치 하는 반면는 단일 기본 인클로저가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-153">hello 8100 has a single primary enclosure, whereas hello 8600 is a dual enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

<span data-ttu-id="36f16-154">장치 hello 기본 하드웨어 구성 요소는 다음 표는 hello에 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-154">hello main hardware components in your device are summarized in hello following tables.</span></span> <span data-ttu-id="36f16-155">Hello hello 링크를 클릭 **교체 절차** 열 toogo toohello 자습서에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-155">Click hello link in hello **Replacement procedure** column toogo toohello associated tutorial.</span></span>

| <span data-ttu-id="36f16-156">구성 요소</span><span class="sxs-lookup"><span data-stu-id="36f16-156">Components</span></span> | <span data-ttu-id="36f16-157">현재 개수</span><span class="sxs-lookup"><span data-stu-id="36f16-157"># Present</span></span> | <span data-ttu-id="36f16-158">플러그 인 모듈 여부</span><span class="sxs-lookup"><span data-stu-id="36f16-158">Plug-in module?</span></span> | <span data-ttu-id="36f16-159">교체 절차</span><span class="sxs-lookup"><span data-stu-id="36f16-159">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="36f16-160">섀시</span><span class="sxs-lookup"><span data-stu-id="36f16-160">Chassis</span></span> |<span data-ttu-id="36f16-161">1</span><span class="sxs-lookup"><span data-stu-id="36f16-161">1</span></span> |<span data-ttu-id="36f16-162">아니요</span><span class="sxs-lookup"><span data-stu-id="36f16-162">No</span></span> |[<span data-ttu-id="36f16-163">StorSimple 장치에 hello 섀시 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-163">Replace hello chassis on your StorSimple device</span></span>](storsimple-chassis-replacement.md) |
| <span data-ttu-id="36f16-164">기본 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="36f16-164">Primary controllers</span></span> |<span data-ttu-id="36f16-165">2</span><span class="sxs-lookup"><span data-stu-id="36f16-165">2</span></span> |<span data-ttu-id="36f16-166">예</span><span class="sxs-lookup"><span data-stu-id="36f16-166">Yes</span></span> |[<span data-ttu-id="36f16-167">StorSimple 장치의 컨트롤러 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-167">Replace a controller module on your StorSimple device</span></span>](storsimple-controller-replacement.md) |
| <span data-ttu-id="36f16-168">764W PCM(전원 및 냉각 모듈)</span><span class="sxs-lookup"><span data-stu-id="36f16-168">764W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="36f16-169">2</span><span class="sxs-lookup"><span data-stu-id="36f16-169">2</span></span> |<span data-ttu-id="36f16-170">예</span><span class="sxs-lookup"><span data-stu-id="36f16-170">Yes</span></span> |[<span data-ttu-id="36f16-171">StorSimple 장치의 전원 및 냉각 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-171">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-power-cooling-module-replacement.md) |
| <span data-ttu-id="36f16-172">백업 배터리</span><span class="sxs-lookup"><span data-stu-id="36f16-172">Backup battery</span></span> |<span data-ttu-id="36f16-173">2</span><span class="sxs-lookup"><span data-stu-id="36f16-173">2</span></span> |<span data-ttu-id="36f16-174">예</span><span class="sxs-lookup"><span data-stu-id="36f16-174">Yes</span></span> |[<span data-ttu-id="36f16-175">StorSimple 장치에서 hello 백업 배터리 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-175">Replace hello backup battery module on your StorSimple device</span></span>](storsimple-battery-replacement.md) |
| <span data-ttu-id="36f16-176">디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="36f16-176">Disk drives</span></span> |<span data-ttu-id="36f16-177">12</span><span class="sxs-lookup"><span data-stu-id="36f16-177">12</span></span> |<span data-ttu-id="36f16-178">예</span><span class="sxs-lookup"><span data-stu-id="36f16-178">Yes</span></span> |[<span data-ttu-id="36f16-179">StorSimple 장치의 디스크 드라이브 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-179">Replace a disk drive on your StorSimple device</span></span>](storsimple-disk-drive-replacement.md) |

<span data-ttu-id="36f16-180">**표 1** hello 기본 인클로저의 하드웨어 구성 요소</span><span class="sxs-lookup"><span data-stu-id="36f16-180">**Table 1** Hardware components in hello primary enclosure</span></span>

<span data-ttu-id="36f16-181">I/O 모듈 hello 기본 인클로저와 EBOD 인클로저 hello 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-181">hello primary enclosure and hello EBOD enclosure differ in their I/O modules.</span></span> <span data-ttu-id="36f16-182">또한 hello Pcm 와트를 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-182">Additionally, hello PCMs have different wattage.</span></span> <span data-ttu-id="36f16-183">hello 기본 인클로저에서 hello Pcm은 764w, 백업 배터리 모듈에 인클로저 hello Pcm 기본 hello에 W. 580 hello EBOD 인클로저가 있는 반면도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-183">hello PCMs in hello primary enclosure are 764 W, whereas those in hello EBOD enclosure are 580 W. hello PCMs in hello primary enclosure also contain a backup battery module.</span></span>

| <span data-ttu-id="36f16-184">구성 요소</span><span class="sxs-lookup"><span data-stu-id="36f16-184">Components</span></span> | <span data-ttu-id="36f16-185">현재 개수</span><span class="sxs-lookup"><span data-stu-id="36f16-185"># Present</span></span> | <span data-ttu-id="36f16-186">플러그 인 모듈 여부</span><span class="sxs-lookup"><span data-stu-id="36f16-186">Plug-in module?</span></span> | <span data-ttu-id="36f16-187">교체 절차</span><span class="sxs-lookup"><span data-stu-id="36f16-187">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="36f16-188">섀시</span><span class="sxs-lookup"><span data-stu-id="36f16-188">Chassis</span></span> |<span data-ttu-id="36f16-189">1</span><span class="sxs-lookup"><span data-stu-id="36f16-189">1</span></span> |<span data-ttu-id="36f16-190">아니요</span><span class="sxs-lookup"><span data-stu-id="36f16-190">No</span></span> |[<span data-ttu-id="36f16-191">StorSimple 장치에 hello 섀시 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-191">Replace hello chassis on your StorSimple device</span></span>](storsimple-chassis-replacement.md) |
| <span data-ttu-id="36f16-192">EBOD 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="36f16-192">EBOD controllers</span></span> |<span data-ttu-id="36f16-193">2</span><span class="sxs-lookup"><span data-stu-id="36f16-193">2</span></span> |<span data-ttu-id="36f16-194">예</span><span class="sxs-lookup"><span data-stu-id="36f16-194">Yes</span></span> |[<span data-ttu-id="36f16-195">StorSimple 장치의 EBOD 컨트롤러 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-195">Replace an EBOD controller on your StorSimple device</span></span>](storsimple-ebod-controller-replacement.md) |
| <span data-ttu-id="36f16-196">580W PCM(전원 및 냉각 모듈)</span><span class="sxs-lookup"><span data-stu-id="36f16-196">580W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="36f16-197">2</span><span class="sxs-lookup"><span data-stu-id="36f16-197">2</span></span> |<span data-ttu-id="36f16-198">예</span><span class="sxs-lookup"><span data-stu-id="36f16-198">Yes</span></span> |[<span data-ttu-id="36f16-199">StorSimple 장치의 전원 및 냉각 모듈 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-199">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-power-cooling-module-replacement.md) |
| <span data-ttu-id="36f16-200">디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="36f16-200">Disk drives</span></span> |<span data-ttu-id="36f16-201">12</span><span class="sxs-lookup"><span data-stu-id="36f16-201">12</span></span> |<span data-ttu-id="36f16-202">예</span><span class="sxs-lookup"><span data-stu-id="36f16-202">Yes</span></span> |[<span data-ttu-id="36f16-203">StorSimple 장치의 디스크 드라이브 교체</span><span class="sxs-lookup"><span data-stu-id="36f16-203">Replace a disk drive on your StorSimple device</span></span>](storsimple-disk-drive-replacement.md) |

<span data-ttu-id="36f16-204">**표 2** hello EBOD 인클로저의 하드웨어 구성 요소</span><span class="sxs-lookup"><span data-stu-id="36f16-204">**Table 2** Hardware components in hello EBOD enclosure</span></span>

<span data-ttu-id="36f16-205">hello 장치에서 플러그 인 모듈이 hello hello 다음 전면 및 후면 다이어그램에에서 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-205">hello plug-in modules on hello device are highlighted in hello following front and rear diagrams.</span></span> <span data-ttu-id="36f16-206">대체 해야 하는 경우 다양 한 플러그 인 모듈의 hello 이러한 다이어그램 toodetermine hello 위치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-206">You can use these diagrams toodetermine hello location of hello various plug-in modules if a replacement is required.</span></span> <span data-ttu-id="36f16-207">hello 전면 다이어그램 보여줄 hello 디스크 드라이브 및 hello 후면 다이어그램의 hello EBOD 인클로저와 기본 인클로저 hello hello 플러그 인 모듈.</span><span class="sxs-lookup"><span data-stu-id="36f16-207">hello front diagram shows hello disk drives, and hello rear diagrams of hello EBOD enclosure and hello primary enclosure show hello plug-in modules.</span></span>

![디스크 드라이브가 있는 장치의 프런트플레인](./media/storsimple-hardware-component-replacement/IC741028.png)

<span data-ttu-id="36f16-209">**그림 1** hello 장치의 전면</span><span class="sxs-lookup"><span data-stu-id="36f16-209">**Figure 1** Front of hello device</span></span>

| <span data-ttu-id="36f16-210">레이블</span><span class="sxs-lookup"><span data-stu-id="36f16-210">Label</span></span> | <span data-ttu-id="36f16-211">설명</span><span class="sxs-lookup"><span data-stu-id="36f16-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="36f16-212">0 - 11</span><span class="sxs-lookup"><span data-stu-id="36f16-212">0 - 11</span></span> |<span data-ttu-id="36f16-213">디스크 드라이브(총 12개)</span><span class="sxs-lookup"><span data-stu-id="36f16-213">Disk drives (total of 12)</span></span> |

<span data-ttu-id="36f16-214">Hello 기본 인클로저 및 EBOD 인클로저 hello 둘 다 다 드라이브 캐리어 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-214">Both hello primary enclosure and hello EBOD enclosure have drive carrier modules.</span></span> <span data-ttu-id="36f16-215">hello 섀시 보관 12 개의 3.5 인치 디스크 드라이브에는 3 4 형식으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-215">hello chassis houses twelve 3.5" disk drives arranged in a 3 by 4 format.</span></span>

![장치 기본 엔클로저 모듈의 백플레인](./media/storsimple-hardware-component-replacement/IC740994.png)

<span data-ttu-id="36f16-217">**그림 2** hello 기본 엔클로저의 뒷면</span><span class="sxs-lookup"><span data-stu-id="36f16-217">**Figure 2** Back of hello primary enclosure</span></span>

| <span data-ttu-id="36f16-218">레이블</span><span class="sxs-lookup"><span data-stu-id="36f16-218">Label</span></span> | <span data-ttu-id="36f16-219">설명</span><span class="sxs-lookup"><span data-stu-id="36f16-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="36f16-220">1</span><span class="sxs-lookup"><span data-stu-id="36f16-220">1</span></span> |<span data-ttu-id="36f16-221">PCM 0</span><span class="sxs-lookup"><span data-stu-id="36f16-221">PCM 0</span></span> |
| <span data-ttu-id="36f16-222">2</span><span class="sxs-lookup"><span data-stu-id="36f16-222">2</span></span> |<span data-ttu-id="36f16-223">PCM 1</span><span class="sxs-lookup"><span data-stu-id="36f16-223">PCM 1</span></span> |
| <span data-ttu-id="36f16-224">3</span><span class="sxs-lookup"><span data-stu-id="36f16-224">3</span></span> |<span data-ttu-id="36f16-225">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="36f16-225">Controller 0</span></span> |
| <span data-ttu-id="36f16-226">4</span><span class="sxs-lookup"><span data-stu-id="36f16-226">4</span></span> |<span data-ttu-id="36f16-227">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="36f16-227">Controller 1</span></span> |

![장치 EBOD 엔클로저 플러그 인 모듈의 백플레인](./media/storsimple-hardware-component-replacement/IC769599.png)

<span data-ttu-id="36f16-229">**그림 3** hello EBOD 인클로저의 후면</span><span class="sxs-lookup"><span data-stu-id="36f16-229">**Figure 3** Back of hello EBOD enclosure</span></span>

| <span data-ttu-id="36f16-230">레이블</span><span class="sxs-lookup"><span data-stu-id="36f16-230">Label</span></span> | <span data-ttu-id="36f16-231">설명</span><span class="sxs-lookup"><span data-stu-id="36f16-231">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="36f16-232">1</span><span class="sxs-lookup"><span data-stu-id="36f16-232">1</span></span> |<span data-ttu-id="36f16-233">PCM 0</span><span class="sxs-lookup"><span data-stu-id="36f16-233">PCM 0</span></span> |
| <span data-ttu-id="36f16-234">2</span><span class="sxs-lookup"><span data-stu-id="36f16-234">2</span></span> |<span data-ttu-id="36f16-235">PCM 1</span><span class="sxs-lookup"><span data-stu-id="36f16-235">PCM 1</span></span> |
| <span data-ttu-id="36f16-236">3</span><span class="sxs-lookup"><span data-stu-id="36f16-236">3</span></span> |<span data-ttu-id="36f16-237">EBOD 컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="36f16-237">EBOD Controller 0</span></span> |
| <span data-ttu-id="36f16-238">4</span><span class="sxs-lookup"><span data-stu-id="36f16-238">4</span></span> |<span data-ttu-id="36f16-239">EBOD 컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="36f16-239">EBOD Controller 1</span></span> |

## <a name="field-replaceable-units"></a><span data-ttu-id="36f16-240">FRU(필드 교체 장치)</span><span class="sxs-lookup"><span data-stu-id="36f16-240">Field replaceable units</span></span>
<span data-ttu-id="36f16-241">다음 fru 교체 () hello StorSimple 장치에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-241">hello following field replaceable units (FRUs) are available for your StorSimple device:</span></span>

* <span data-ttu-id="36f16-242">섀시 (hello 통합된 운용 패널 포함)</span><span class="sxs-lookup"><span data-stu-id="36f16-242">Chassis (including hello integrated operations panel)</span></span>
* <span data-ttu-id="36f16-243">764 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="36f16-243">764 W AC PCM</span></span>
* <span data-ttu-id="36f16-244">580 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="36f16-244">580 W AC PCM</span></span>
* <span data-ttu-id="36f16-245">드라이브 캐리어 모듈이 있는 하드 디스크 드라이브</span><span class="sxs-lookup"><span data-stu-id="36f16-245">Hard disk drive with drive carrier module</span></span>
* <span data-ttu-id="36f16-246">컨트롤러 모듈</span><span class="sxs-lookup"><span data-stu-id="36f16-246">Controller module</span></span>
* <span data-ttu-id="36f16-247">EBOD 컨트롤러 모듈</span><span class="sxs-lookup"><span data-stu-id="36f16-247">EBOD controller module</span></span>
* <span data-ttu-id="36f16-248">백업 배터리 모듈</span><span class="sxs-lookup"><span data-stu-id="36f16-248">Backup battery module</span></span>
* <span data-ttu-id="36f16-249">랙 탑재 레일 키트</span><span class="sxs-lookup"><span data-stu-id="36f16-249">Rack mounting rail kit</span></span>

<span data-ttu-id="36f16-250">하십시오 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md) tooorder 이러한 교체 장비입니다.</span><span class="sxs-lookup"><span data-stu-id="36f16-250">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder any of these replacement units.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36f16-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36f16-251">Next steps</span></span>
<span data-ttu-id="36f16-252">모든 검토 [안전 정보](storsimple-safety.md) tooreplace StorSimple 하드웨어 구성 요소를 시도 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="36f16-252">Review all [safety information](storsimple-safety.md) before you attempt tooreplace a StorSimple hardware component.</span></span>

