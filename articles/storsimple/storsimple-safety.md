---
title: "StorSimple 장치에 대한 안정성 | Microsoft Docs"
description: "안전성 규칙, 지침 및 고려 사항을 설명하고 StorSimple 장치를 안전하게 설치하고 작동하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: dae6d535-1ca2-4d2b-b221-6819043aa068
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: a178e8880bcbcada9d66eaacf5ccbdb7c55957cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="safely-install-and-operate-your-storsimple-device"></a><span data-ttu-id="09422-103">StorSimple 장치의 안전한 설치 및 작동</span><span class="sxs-lookup"><span data-stu-id="09422-103">Safely install and operate your StorSimple device</span></span>
<span data-ttu-id="09422-104">![경고 아이콘](./media/storsimple-safety/IC740879.png)
![안전성 고지 읽기 아이콘](./media/storsimple-safety/IC740885.png) **안전성 및 상태 정보 읽기**</span><span class="sxs-lookup"><span data-stu-id="09422-104">![Warning Icon](./media/storsimple-safety/IC740879.png)
![Read Safety Notice Icon](./media/storsimple-safety/IC740885.png) **READ SAFETY AND HEALTH INFORMATION**</span></span>

<span data-ttu-id="09422-105">이 문서에서 Microsoft Azure StorSimple 장치에 적용되는 모든 안전성 및 상태 정보를 읽으십시오</span><span class="sxs-lookup"><span data-stu-id="09422-105">Read all the safety and health information in this article that applies to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="09422-106">나중에 참조할 수 있도록 StorSimple 장치와 함께 제공되는 모든 인쇄된 가이드를 보관하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-106">Keep all the printed guides shipped with your StorSimple device for future reference.</span></span> <span data-ttu-id="09422-107">지침을 따르지 않고 이 제품을 적절하게 설정, 사용 및 관리하지 않으면 심각한 부상 또는 사망 위험이 증가하거나 장치가 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-107">Failure to follow instructions and properly set up, use, and care for this product can increase the risk of serious injury or death, or damage to the device or devices.</span></span> <span data-ttu-id="09422-108">[이 가이드의 다운로드할 수 있는 버전](http://www.microsoft.com/download/details.aspx?id=44233)도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09422-108">A [downloadable version of this guide](http://www.microsoft.com/download/details.aspx?id=44233) is also available.</span></span>

## <a name="safety-icon-conventions"></a><span data-ttu-id="09422-109">안전성 아이콘 표시 규칙</span><span class="sxs-lookup"><span data-stu-id="09422-109">Safety icon conventions</span></span>
<span data-ttu-id="09422-110">다음은 Microsoft Azure StorSimple 장치를 설정 및 실행할 때 관찰되는 안전 주의 사항을 검토할 때 표시되는 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="09422-110">Here are the icons that you will find when you review the safety precautions to be observed when setting up and running your Microsoft Azure StorSimple device.</span></span>

| <span data-ttu-id="09422-111">아이콘</span><span class="sxs-lookup"><span data-stu-id="09422-111">Icon</span></span> | <span data-ttu-id="09422-112">설명</span><span class="sxs-lookup"><span data-stu-id="09422-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="09422-113">![위험 아이콘](./media/storsimple-safety/IC740879.png) **위험!**</span><span class="sxs-lookup"><span data-stu-id="09422-113">![Danger Icon](./media/storsimple-safety/IC740879.png) **DANGER!**</span></span> |<span data-ttu-id="09422-114">피하지 않을 경우 사망 또는 심각한 부상을 당하는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="09422-114">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="09422-115">이 위험도 표시는 가장 극단적인 상황으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="09422-115">This signal word is to be limited to the most extreme situations.</span></span> |
| <span data-ttu-id="09422-116">![경고 아이콘](./media/storsimple-safety/IC740879.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-116">![Warning Icon](./media/storsimple-safety/IC740879.png) **WARNING!**</span></span> |<span data-ttu-id="09422-117">피하지 않을 경우 사망 또는 심각한 부상을 당할 수 있는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="09422-117">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| <span data-ttu-id="09422-118">![경고 아이콘](./media/storsimple-safety/IC740879.png) **주의!**</span><span class="sxs-lookup"><span data-stu-id="09422-118">![Warning Icon](./media/storsimple-safety/IC740879.png) **CAUTION!**</span></span> |<span data-ttu-id="09422-119">피하지 않을 경우 최소 또는 보통 수준의 부상을 당할 수 있는 위험한 상황을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="09422-119">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| <span data-ttu-id="09422-120">![참고 아이콘](./media/storsimple-safety/IC740881.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="09422-120">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span> |<span data-ttu-id="09422-121">중요하지만 위험과 관련되지 않은 것으로 간주되는 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="09422-121">Indicates information considered important, but not hazard-related.</span></span> |
| <span data-ttu-id="09422-122">![감전 아이콘](./media/storsimple-safety/IC740882.png) **감전 위험**</span><span class="sxs-lookup"><span data-stu-id="09422-122">![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **Electrical Shock Hazard**</span></span> |<span data-ttu-id="09422-123">높은 전압</span><span class="sxs-lookup"><span data-stu-id="09422-123">High voltage</span></span> |
| <span data-ttu-id="09422-124">![무거운 무게 아이콘](./media/storsimple-safety/IC740883.png) **무거운 무게**</span><span class="sxs-lookup"><span data-stu-id="09422-124">![Heavy Weight Icon](./media/storsimple-safety/IC740883.png) **Heavy Weight**</span></span> | |
| <span data-ttu-id="09422-125">![사용자 서비스 가능 부품 없음 아이콘](./media/storsimple-safety/IC740879.png) **사용자 서비스 가능 부품 없음**</span><span class="sxs-lookup"><span data-stu-id="09422-125">![No User Serviceable Parts Icon](./media/storsimple-safety/IC740879.png) **No User Serviceable Parts**</span></span> |<span data-ttu-id="09422-126">제대로 교육을 받지 않은 경우 액세스하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="09422-126">Do not access unless properly trained.</span></span> |
| <span data-ttu-id="09422-127">![안전성 고지 읽기 아이콘](./media/storsimple-safety/IC740885.png)**먼저 모든 지침 읽기**</span><span class="sxs-lookup"><span data-stu-id="09422-127">![Read Safety Notice Icon](./media/storsimple-safety/IC740885.png)**Read All Instructions First**</span></span> | |
| <span data-ttu-id="09422-128">![기울어짐 위험 아이콘](./media/storsimple-safety/IC740886.png) **기울어짐 위험**</span><span class="sxs-lookup"><span data-stu-id="09422-128">![Tip Hazard Icon](./media/storsimple-safety/IC740886.png) **Tip Hazard**</span></span> | |

## <a name="handling-precautions"></a><span data-ttu-id="09422-129">취급 주의 사항</span><span class="sxs-lookup"><span data-stu-id="09422-129">Handling precautions</span></span>
<span data-ttu-id="09422-130">![경고 아이콘](./media/storsimple-safety/IC740879.png) ![무거운 무게 아이콘](./media/storsimple-safety/IC740883.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-130">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Heavy Weight Icon](./media/storsimple-safety/IC740883.png) **WARNING!**</span></span> 

<span data-ttu-id="09422-131">부상 위험을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-131">To reduce the risk of injury:</span></span>

* <span data-ttu-id="09422-132">완전히 구성된 인클로저의 최고 무게는 32kg(70lbs)입니다. 혼자 들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-132">A fully configured enclosure can weigh up to 32 kg (70 lbs); do not try to lift it by yourself.</span></span>
* <span data-ttu-id="09422-133">인클로저를 이동하기 전에 항상 두 사람이 무게를 지탱하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-133">Before moving the enclosure, always ensure that two people are available to handle the weight.</span></span> <span data-ttu-id="09422-134">한 사람이 이 무게를 들어 올릴 경우 부상을 당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-134">Be aware that one person attempting to lift this weight can sustain injuries.</span></span>
* <span data-ttu-id="09422-135">장치의 뒷면에 있는 전원 및 냉각 모듈(PCM)의 핸들로 인클로저를 들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-135">Do not lift the enclosure by the handles on the Power and Cooling Modules (PCMs) located at the rear of the unit.</span></span> <span data-ttu-id="09422-136">무게를 지탱하도록 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-136">These are not designed to take the weight.</span></span>

## <a name="connection-precautions"></a><span data-ttu-id="09422-137">연결 주의 사항</span><span class="sxs-lookup"><span data-stu-id="09422-137">Connection precautions</span></span>
<span data-ttu-id="09422-138">![경고 아이콘](./media/storsimple-safety/IC740879.png) ![감전 아이콘](./media/storsimple-safety/IC740882.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-138">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="09422-139">부상, 감전 또는 사망 가능성을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-139">To reduce the likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="09422-140">여러 AC 전원에서 전기를 공급받는 경우 완전한 격리를 위해 모든 전원의 연결을 해제하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-140">When powered by multiple AC sources, disconnect all supply power for complete isolation.</span></span>
* <span data-ttu-id="09422-141">이동하기 전이나 어떤 방식으로든 손상될 것이라고 판단되는 장치 플러그를 영구적으로 뽑으십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-141">Permanently unplug the unit before you move it or if you think it has become damaged in any way.</span></span>
* <span data-ttu-id="09422-142">전원 공급 코드에 안전한 전기 접지 연결을 제공하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-142">Provide a safe electrical earth connection to the power supply cords.</span></span> <span data-ttu-id="09422-143">전원을 공급하기 전에 인클로저의 접지가 국가 및 지역 요구 사항을 충족하는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-143">Verify that the grounding of the enclosure meets the national and local requirements before applying power.</span></span>
* <span data-ttu-id="09422-144">인클로저에서 PCM을 제거하기 전에 항상 전원 연결을 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-144">Ensure that the power connection is always disconnected prior to the removal of a PCM from the enclosure.</span></span>
* <span data-ttu-id="09422-145">전원 공급 장치 코드의 플러그가 기본 차단 장치라면, 소켓 콘센트가 장비 근처에 있고 쉽게 액세스할 수 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-145">Given that the plug on the power supply cord is the main disconnect device, ensure that the socket outlets are located near the equipment and are easily accessible.</span></span>

<span data-ttu-id="09422-146">![경고 아이콘](./media/storsimple-safety/IC740879.png) ![감전 아이콘](./media/storsimple-safety/IC740882.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-146">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="09422-147">전기 연결에서 과열 또는 화재 가능성을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-147">To reduce the likelihood of overheating or fire from the electrical connections:</span></span>

* <span data-ttu-id="09422-148">기술 사양에 상세히 기술된 요구 사항을 충족하기 위해 전기 과부하 보호 기능과 함께 적합한 전원을 제공하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-148">Provide a suitable power source with electrical overload protection to meet the requirements detailed in the technical specification.</span></span>
* <span data-ttu-id="09422-149">두 갈래의 전원 코드("Y" 리드)를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-149">Do not use bifurcated power cords (“Y” leads).</span></span>
* <span data-ttu-id="09422-150">해당 안전, 배기 가스 및 열 요구 사항을 준수하기 위해 커버를 제거하지 말고 모든 베이를 플러그인 모듈 또는 드라이브 블랭크로 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-150">To comply with applicable safety, emission, and thermal requirements, no covers should be removed and all bays must be populated with plug-in modules or drive blanks.</span></span>
* <span data-ttu-id="09422-151">장비가 제조업체에서 지정한 방식으로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-151">Ensure that the equipment is used in a manner specified by the manufacturer.</span></span> <span data-ttu-id="09422-152">제조업체에서 지정하지 않은 방식으로 이 장비를 사용할 경우 장비에서 제공하는 보호 기능이 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-152">If this equipment is used in a manner not specified by the manufacturer, the protection provided by the equipment may be impaired.</span></span>

<span data-ttu-id="09422-153">![참고 아이콘](./media/storsimple-safety/IC740881.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="09422-153">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="09422-154">장비의 적절한 작동 및 제품 손상을 막으려면:</span><span class="sxs-lookup"><span data-stu-id="09422-154">For the proper operation of your equipment and to prevent product damage:</span></span>

* <span data-ttu-id="09422-155">장치의 뒷면에 있는 RJ45 포트는 이더넷 연결 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="09422-155">The RJ45 ports at the back of the device are for an Ethernet connection only.</span></span> <span data-ttu-id="09422-156">원격 통신 네트워크에 연결해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09422-156">These must not be connected to a telecommunications network.</span></span>
* <span data-ttu-id="09422-157">앞-뒤 냉각 설계를 수용할 수 있는 랙에 장치를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-157">Be sure to install the device in a rack that can accommodate a front-to-back cooling design.</span></span>
* <span data-ttu-id="09422-158">모든 플러그인 모듈 및 블랭크 판은 시스템 인클로저의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="09422-158">All plug-in modules and blank plates are part of the system enclosure.</span></span> <span data-ttu-id="09422-159">교체품을 즉시 추가할 수 있을 때만 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-159">These must only be removed when a replacement can be immediately added.</span></span> <span data-ttu-id="09422-160">시스템은 모든 모듈 또는 블랭크가 장착된 상태에서만 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-160">The system must not be run without all modules or blanks in place.</span></span>

## <a name="rack-system-precautions"></a><span data-ttu-id="09422-161">랙 시스템 주의 사항</span><span class="sxs-lookup"><span data-stu-id="09422-161">Rack system precautions</span></span>
<span data-ttu-id="09422-162">랙 캐비닛에 장치를 탑재할 때는 다음 안전 요구 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-162">The following safety requirements must be considered when you mount the device in a rack cabinet.</span></span>

<span data-ttu-id="09422-163">![경고 아이콘](./media/storsimple-safety/IC740879.png) ![기울어짐 위험 아이콘](./media/storsimple-safety/IC740886.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-163">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Tip Hazard Icon](./media/storsimple-safety/IC740886.png) **WARNING!**</span></span>

<span data-ttu-id="09422-164">전복되어 발생하는 부상 가능성을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-164">To reduce the likelihood of injury from a tip over:</span></span>

* <span data-ttu-id="09422-165">랙 설계는 설치된 인클로저의 총 무게를 지탱해야 하며 설치 또는 정상적인 사용 중에 랙이 기울어 넘어지거나 밀어 넘어지지 않도록 안정화 기능을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-165">The rack design should support the total weight of the installed enclosures and should incorporate stabilizing features suitable to prevent the rack from tipping or being pushed over during installation or normal use.</span></span>
* <span data-ttu-id="09422-166">랙을 로드할 때는 아래에서 위로 랙을 채우고 위에서 아래로 비우십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-166">When loading a rack, fill the rack from the bottom up and empty from the top down.</span></span>
* <span data-ttu-id="09422-167">두 개 이상의 인클로저를 랙 바깥쪽으로 동시에 밀지 마십시오. 랙이 넘어질 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-167">Do not slide more than one enclosure out of the rack at a time to avoid the danger of the rack toppling over.</span></span>

<span data-ttu-id="09422-168">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-168">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="09422-169">부상, 감전 또는 사망 가능성을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-169">To reduce the likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="09422-170">랙은 안전한 배전 시스템을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-170">The rack should have a safe electrical distribution system.</span></span> <span data-ttu-id="09422-171">인클로저에 과전류 보호 기능을 제공해야 하며 설치된 인클로저 총 수에 의해 과부하되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09422-171">It must provide over-current protection for the enclosure and must not be overloaded by the total number of enclosures installed.</span></span> <span data-ttu-id="09422-172">명판에 표시된 정격 소비 전력을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-172">The electrical power consumption rating shown on the nameplate should be observed.</span></span>
* <span data-ttu-id="09422-173">배전 시스템에서는 랙에 있는 각 인클로저에 신뢰할 수 있는 접지를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-173">The electrical distribution system must provide a reliable ground for each enclosure in the rack.</span></span>
* <span data-ttu-id="09422-174">배전 시스템의 설계에서는 모든 인클로저의 모든 전원 공급 장치로부터 나오는 전체 접지 누설 전류를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-174">The design of the electrical distribution system must take into consideration the total ground leakage current from all power supplies in all enclosures.</span></span> <span data-ttu-id="09422-175">각 인클로저의 각 전원 공급 장치에는 60Hz, 264볼트에서 최대 1.0mA의 접지 누설 전류를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-175">Note that each power supply in each enclosure has a ground leakage current of 1.0 mA maximum at 60 Hz, 264 volts.</span></span> <span data-ttu-id="09422-176">랙에 “누설 전류 높음.</span><span class="sxs-lookup"><span data-stu-id="09422-176">The rack may require labeling with “HIGH LEAKAGE CURRENT.</span></span> <span data-ttu-id="09422-177">전기를 연결하기 전에 접지(어스) 연결이 필요합니다."라는 레이블이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-177">Ground (earth) connection is essential before connecting a supply.”</span></span>
* <span data-ttu-id="09422-178">인클로저와 함께 구성된 랙은 UL 60950-1 및 IEC 60950-1/EN 60950-1의 안전 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-178">The rack, when configured with the enclosures, must meet the safety requirements of UL 60950-1 and IEC 60950-1/EN 60950-1.</span></span>

<span data-ttu-id="09422-179">![참고 아이콘](./media/storsimple-safety/IC740881.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="09422-179">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="09422-180">랙 시스템의 적절한 냉각을 위해:</span><span class="sxs-lookup"><span data-stu-id="09422-180">For the proper cooling of your rack system:</span></span>

* <span data-ttu-id="09422-181">랙 설계 시 섭씨 35도(화씨 95도)의 인클로저 작동을 위한 최대 주변 온도를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-181">Ensure that the rack design takes into consideration the maximum enclosure operating ambient temperature of 35 degrees Celsius (95 degrees Fahrenheit).</span></span>
* <span data-ttu-id="09422-182">시스템은 저압의 후면 배기 설치에서 작동합니다(랙 도어에서 발생하는 배압 및 장애물이 5파스칼[0.5mm 수면계]을 초과하지 않음).</span><span class="sxs-lookup"><span data-stu-id="09422-182">The system is operated with low-pressure, rear-exhaust installation (back pressure created by rack doors and obstacles not to exceed 5 Pascal [0.5 mm water gauge]).</span></span>

## <a name="power-cooling-module-pcm-precautions"></a><span data-ttu-id="09422-183">PCM(전원 냉각 모듈) 주의 사항</span><span class="sxs-lookup"><span data-stu-id="09422-183">Power Cooling Module (PCM) precautions</span></span>
<span data-ttu-id="09422-184">장치는 두 개의 PCM과 함께 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-184">The device is designed to operate with two PCMs.</span></span> <span data-ttu-id="09422-185">각 PCM에는 전원 공급 장치와 이중 축 팬이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-185">Each of the PCMs has a power supply and a dual-axis fan.</span></span> <span data-ttu-id="09422-186">임계 조건에서 시스템은 한 대의 전원 공급 장치에 오류가 발생해도 정상적인 작동을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-186">During a critical condition, the system allows for a failure of one power supply while continuing normal operations.</span></span> <span data-ttu-id="09422-187">항상 두 PCM(및 전원 공급 장치)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-187">Two PCMs (and hence power supplies) must always be installed.</span></span> <span data-ttu-id="09422-188">PCM 하나로는 예비 전력을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-188">A single PCM does not provide redundant power.</span></span> <span data-ttu-id="09422-189">따라서 하나의 PCM만 고장나도 가동 중지 시간 또는 데이터 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-189">Therefore, the failure of even one PCM can result in downtime or possible data loss.</span></span>

<span data-ttu-id="09422-190">![경고 아이콘](./media/storsimple-safety/IC740879.png) ![감전 아이콘](./media/storsimple-safety/IC740882.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-190">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="09422-191">부상, 감전 또는 사망 가능성을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-191">To reduce the likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="09422-192">PCM에서 커버를 제거하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-192">Do not remove the covers from the PCM.</span></span> <span data-ttu-id="09422-193">내부 감전 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-193">There is a danger of electric shock inside.</span></span> <span data-ttu-id="09422-194">PCM을 반환하고 교체하려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="09422-194">To return the PCM and obtain a replacement, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

<span data-ttu-id="09422-195">![참고 아이콘](./media/storsimple-safety/IC740881.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="09422-195">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="09422-196">장비의 적절한 작동 및 제품 손상을 막으려면:</span><span class="sxs-lookup"><span data-stu-id="09422-196">For the proper operation of your equipment and to prevent product damage:</span></span>

* <span data-ttu-id="09422-197">실패한 PCM은 24시간 이내 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-197">You must replace the failed PCM within 24 hours.</span></span> <span data-ttu-id="09422-198">교체할 PCM을 제거한 후 제거 시점부터 10분이내 교체를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-198">After a PCM is removed for replacement, the replacement must be completed within 10 minutes after removal.</span></span>
* <span data-ttu-id="09422-199">교체품을 즉시 설치할 수 없는 경우 PCM을 제거하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-199">Do not remove a PCM unless a replacement can be installed immediately.</span></span> <span data-ttu-id="09422-200">모든 모듈이 장착된 상태에서만 인클로저를 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-200">The enclosure must not be operated without all modules in place.</span></span>

## <a name="electrostatic-discharge-esd-precautions"></a><span data-ttu-id="09422-201">정전기 방전(ESD) 주의 사항</span><span class="sxs-lookup"><span data-stu-id="09422-201">Electrostatic discharge (ESD) precautions</span></span>
<span data-ttu-id="09422-202">![참고 아이콘](./media/storsimple-safety/IC740881.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="09422-202">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="09422-203">다음 ESD 관련 주의 상태를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="09422-203">Observe the following ESD-related precautions.</span></span>

* <span data-ttu-id="09422-204">적절한 방전 손목 또는 발목 스트랩을 착용했는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-204">Ensure that you have installed and checked a suitable antistatic wrist or ankle strap.</span></span>
* <span data-ttu-id="09422-205">모듈 및 구성 요소를 취급할 때는 모든 기본적인 ESD 주의 사항을 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-205">Observe all conventional ESD precautions when handling modules and components.</span></span>
* <span data-ttu-id="09422-206">백플레인 구성 요소 및 모듈 커넥터에 닿지 않도록 하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-206">Avoid contact with backplane components and module connectors.</span></span>
* <span data-ttu-id="09422-207">ESD 손상 시 보증이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-207">ESD damage is not covered by warranty.</span></span>

## <a name="battery-disposal-precautions"></a><span data-ttu-id="09422-208">배터리 폐기 주의 사항</span><span class="sxs-lookup"><span data-stu-id="09422-208">Battery disposal precautions</span></span>
<span data-ttu-id="09422-209">전원 공급 장치는 일시적인 단기 정전 중에 메모리 내용을 보호하는 특수 배터리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-209">The power supply uses a special battery to protect the contents of memory during temporary, short-term power outages.</span></span> <span data-ttu-id="09422-210">이 배터리는 PCM에 장착되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-210">The battery is seated in the PCM.</span></span> <span data-ttu-id="09422-211">배터리에 대한 다음 정보를 숙지하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-211">Keep the following information in mind about the battery.</span></span>

<span data-ttu-id="09422-212">![경고 아이콘](./media/storsimple-safety/IC740879.png) **경고!**</span><span class="sxs-lookup"><span data-stu-id="09422-212">![Warning Icon](./media/storsimple-safety/IC740879.png) **WARNING!**</span></span>

<span data-ttu-id="09422-213">누전, 화재, 폭발, 부상 또는 사망 위험을 줄이려면:</span><span class="sxs-lookup"><span data-stu-id="09422-213">To reduce the risk of shorts, fire, explosion, injury, or death:</span></span>

* <span data-ttu-id="09422-214">국가/지역 규정에 따라 사용한 배터리를 폐기하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-214">Dispose of used batteries in accordance with national/regional regulations.</span></span>
* <span data-ttu-id="09422-215">분해하거나 충격을 가하거나 섭씨 60도(화씨 140도)가 넘게 가열하거나 소각하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-215">Do not disassemble, crush, or heat above 60 degrees Celsius (140 degrees Fahrenheit) or incinerate.</span></span> <span data-ttu-id="09422-216">PCM 배터리는 제공된 배터리로만 교체하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-216">Replace the PCM battery with a supplied battery only.</span></span> <span data-ttu-id="09422-217">다른 배터리를 사용할 경우 화재 또는 폭발 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09422-217">Use of another battery may present a risk of fire or explosion.</span></span>
* <span data-ttu-id="09422-218">전원 공급 장치에서 제거하는 경우 배터리에 보호용 끝 캡을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="09422-218">Use protective end caps on the batteries if these are removed from the power supply.</span></span>

<span data-ttu-id="09422-219">![참고 아이콘](./media/storsimple-safety/IC740881.png) **고지:**</span><span class="sxs-lookup"><span data-stu-id="09422-219">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="09422-220">배터리를 선적하거나 항공편으로 달리 운송하는 경우 IATA 리튬 배터리 지침 문서( [http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)</span><span class="sxs-lookup"><span data-stu-id="09422-220">When shipping or otherwise transporting the batteries by air, follow the IATA Lithium Battery Guidance document available at [http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)</span></span>

<span data-ttu-id="09422-221">이 보안 공지를 검토한 후 다음 단계에서는 장치를 개봉하고 랙 및 케이블을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-221">After you have reviewed these safety notices, the next steps are to unpack, rack and cable your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09422-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09422-222">Next steps</span></span>
* <span data-ttu-id="09422-223">8100 장치의 경우 [StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-223">For an 8100 device, go to [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md).</span></span>
* <span data-ttu-id="09422-224">8600 장치의 경우 [StorSimple 8600 장치 설치](storsimple-8600-hardware-installation.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09422-224">For an 8600 device, go to [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>

