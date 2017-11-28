---
title: "aaaDeep을 심층적으로 자동차를 움직일 상태를 예측 하 고 습관-Azure | Microsoft Docs"
description: "습관 지원 하 고 차량 상태에 대해 Cortana 인텔리전스 toogain 실시간 및 예측 insights hello 기능을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="2b19e-103">자동차를 움직일 원격 분석 분석 솔루션 플레이 북: hello 솔루션으로 심층 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="2b19e-104">이 **메뉴** 이 플레이 북의 toohello 섹션 링크:</span><span class="sxs-lookup"><span data-stu-id="2b19e-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="2b19e-105">이 섹션으로 드릴 다운 각 hello 솔루션 아키텍처 지침 및 사용자 지정에 대 한 포인터에에서 표시 된 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="2b19e-106">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="2b19e-106">Data Sources</span></span>
<span data-ttu-id="2b19e-107">hello 솔루션에서는 두 개의 서로 다른 데이터 소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="2b19e-108">**시뮬레이션된 차량 신호 및 진단 데이터 집합** 및</span><span class="sxs-lookup"><span data-stu-id="2b19e-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="2b19e-109">**차량 카탈로그**</span><span class="sxs-lookup"><span data-stu-id="2b19e-109">**vehicle catalog**</span></span>

<span data-ttu-id="2b19e-110">차량 텔레매틱스 시뮬레이터가 이 솔루션의 일부로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="2b19e-111">진단 정보를 내보냅니다 하 고 해당 toohello 상태 hello 차량와 시간에서 지정된 된 지점에서 패턴을 구동 toohello에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="2b19e-112">클릭 [차량 전자 통신 정보 시뮬레이터](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **차량 전자 통신 정보 시뮬레이터 Visual Studio 솔루션** 요구 사항에 따라 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="2b19e-113">hello 차량 카탈로그 VIN toomodel 매핑 사용 하 여 참조 데이터 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![차량 텔레매틱스 시뮬레이터](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="2b19e-115">*그림 1 – 차량 텔레매틱스 시뮬레이터*</span><span class="sxs-lookup"><span data-stu-id="2b19e-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="2b19e-116">Hello 다음 스키마를 포함 하는 JSON 형식의 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="2b19e-117">열</span><span class="sxs-lookup"><span data-stu-id="2b19e-117">Column</span></span> | <span data-ttu-id="2b19e-118">설명</span><span class="sxs-lookup"><span data-stu-id="2b19e-118">Description</span></span> | <span data-ttu-id="2b19e-119">값</span><span class="sxs-lookup"><span data-stu-id="2b19e-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b19e-120">VIN</span><span class="sxs-lookup"><span data-stu-id="2b19e-120">VIN</span></span> |<span data-ttu-id="2b19e-121">임의로 생성된 차량 식별 번호</span><span class="sxs-lookup"><span data-stu-id="2b19e-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="2b19e-122">10,000개의 임의로 생성된 차량 식별 번호의 마스터 목록에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="2b19e-123">외부 온도</span><span class="sxs-lookup"><span data-stu-id="2b19e-123">Outside temperature</span></span> |<span data-ttu-id="2b19e-124">hello 차량 운전는 온도 외부 hello</span><span class="sxs-lookup"><span data-stu-id="2b19e-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="2b19e-125">0-100까지의 임의로 생성된 번호</span><span class="sxs-lookup"><span data-stu-id="2b19e-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="2b19e-126">엔진 온도</span><span class="sxs-lookup"><span data-stu-id="2b19e-126">Engine temperature</span></span> |<span data-ttu-id="2b19e-127">hello 차량 hello 엔진 온도</span><span class="sxs-lookup"><span data-stu-id="2b19e-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="2b19e-128">0-500까지의 임의로 생성된 번호</span><span class="sxs-lookup"><span data-stu-id="2b19e-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="2b19e-129">속도</span><span class="sxs-lookup"><span data-stu-id="2b19e-129">Speed</span></span> |<span data-ttu-id="2b19e-130">hello 엔진 속도 hello에 자동차를 움직일 제어</span><span class="sxs-lookup"><span data-stu-id="2b19e-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="2b19e-131">0-100까지의 임의로 생성된 번호</span><span class="sxs-lookup"><span data-stu-id="2b19e-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="2b19e-132">연료</span><span class="sxs-lookup"><span data-stu-id="2b19e-132">Fuel</span></span> |<span data-ttu-id="2b19e-133">hello 자동차의 연료 수준 hello</span><span class="sxs-lookup"><span data-stu-id="2b19e-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="2b19e-134">0-100까지의 임의로 생성된 번호(연료 수준 비율을 나타냄)</span><span class="sxs-lookup"><span data-stu-id="2b19e-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="2b19e-135">엔진 오일</span><span class="sxs-lookup"><span data-stu-id="2b19e-135">EngineOil</span></span> |<span data-ttu-id="2b19e-136">hello 차량 hello 엔진 석유 수준</span><span class="sxs-lookup"><span data-stu-id="2b19e-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="2b19e-137">0-100까지의 임의로 생성된 번호(엔진 오일 수준 비율을 나타냄)</span><span class="sxs-lookup"><span data-stu-id="2b19e-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="2b19e-138">타이어 압력</span><span class="sxs-lookup"><span data-stu-id="2b19e-138">Tire pressure</span></span> |<span data-ttu-id="2b19e-139">hello 차량 hello tire 압력</span><span class="sxs-lookup"><span data-stu-id="2b19e-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="2b19e-140">0-50까지의 임의로 생성된 번호(타이어 압력 수준 비율을 나타냄)</span><span class="sxs-lookup"><span data-stu-id="2b19e-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="2b19e-141">주행 기록계</span><span class="sxs-lookup"><span data-stu-id="2b19e-141">Odometer</span></span> |<span data-ttu-id="2b19e-142">hello 차량 주행 기록 계 읽기 hello</span><span class="sxs-lookup"><span data-stu-id="2b19e-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="2b19e-143">0-200000까지의 임의로 생성된 번호</span><span class="sxs-lookup"><span data-stu-id="2b19e-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="2b19e-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="2b19e-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="2b19e-145">hello 차량 hello 가속기 페달 위치</span><span class="sxs-lookup"><span data-stu-id="2b19e-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="2b19e-146">0-100까지의 임의로 생성된 번호(가속기 수준 비율을 나타냄)</span><span class="sxs-lookup"><span data-stu-id="2b19e-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="2b19e-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="2b19e-147">Parking_brake_status</span></span> |<span data-ttu-id="2b19e-148">Hello 차량 파킹 되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="2b19e-149">True 또는 False</span><span class="sxs-lookup"><span data-stu-id="2b19e-149">True or False</span></span> |
| <span data-ttu-id="2b19e-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="2b19e-150">Headlamp_status</span></span> |<span data-ttu-id="2b19e-151">Hello headlamp 위치가에 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="2b19e-152">True 또는 False</span><span class="sxs-lookup"><span data-stu-id="2b19e-152">True or False</span></span> |
| <span data-ttu-id="2b19e-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="2b19e-153">Brake_pedal_status</span></span> |<span data-ttu-id="2b19e-154">Hello 브레이크 페달을 눌렀는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="2b19e-155">True 또는 False</span><span class="sxs-lookup"><span data-stu-id="2b19e-155">True or False</span></span> |
| <span data-ttu-id="2b19e-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="2b19e-156">Transmission_gear_position</span></span> |<span data-ttu-id="2b19e-157">hello 차량 hello 전송 기어 위치</span><span class="sxs-lookup"><span data-stu-id="2b19e-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="2b19e-158">상태: 1단, 2단, 3단, 4단, 5단, 6단, 7단, 8단</span><span class="sxs-lookup"><span data-stu-id="2b19e-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="2b19e-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="2b19e-159">Ignition_status</span></span> |<span data-ttu-id="2b19e-160">실행 중이거나 중지 된 hello 차량 인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="2b19e-161">True 또는 False</span><span class="sxs-lookup"><span data-stu-id="2b19e-161">True or False</span></span> |
| <span data-ttu-id="2b19e-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="2b19e-162">Windshield_wiper_status</span></span> |<span data-ttu-id="2b19e-163">Hello 차량의 바람막이 wiper 설정 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="2b19e-164">True 또는 False</span><span class="sxs-lookup"><span data-stu-id="2b19e-164">True or False</span></span> |
| <span data-ttu-id="2b19e-165">ABS</span><span class="sxs-lookup"><span data-stu-id="2b19e-165">ABS</span></span> |<span data-ttu-id="2b19e-166">ABS의 작동 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="2b19e-167">True 또는 False</span><span class="sxs-lookup"><span data-stu-id="2b19e-167">True or False</span></span> |
| <span data-ttu-id="2b19e-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2b19e-168">Timestamp</span></span> |<span data-ttu-id="2b19e-169">hello 데이터 요소를 만들 때 timestamp 안녕</span><span class="sxs-lookup"><span data-stu-id="2b19e-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="2b19e-170">Date</span><span class="sxs-lookup"><span data-stu-id="2b19e-170">Date</span></span> |
| <span data-ttu-id="2b19e-171">City</span><span class="sxs-lookup"><span data-stu-id="2b19e-171">City</span></span> |<span data-ttu-id="2b19e-172">hello 차량 hello 위치</span><span class="sxs-lookup"><span data-stu-id="2b19e-172">hello location of hello vehicle</span></span> |<span data-ttu-id="2b19e-173">이 솔루션의 경우 4개 도시: 벨뷰, 레드몬드, 사마미시, 시애틀</span><span class="sxs-lookup"><span data-stu-id="2b19e-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="2b19e-174">참조 데이터 집합을 모델 hello 차량 VIN toohello 모델 매핑을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="2b19e-175">VIN</span><span class="sxs-lookup"><span data-stu-id="2b19e-175">VIN</span></span> | <span data-ttu-id="2b19e-176">모델</span><span class="sxs-lookup"><span data-stu-id="2b19e-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="2b19e-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="2b19e-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="2b19e-178">세단</span><span class="sxs-lookup"><span data-stu-id="2b19e-178">Sedan</span></span> |
| <span data-ttu-id="2b19e-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="2b19e-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="2b19e-180">하이브리드</span><span class="sxs-lookup"><span data-stu-id="2b19e-180">Hybrid</span></span> |
| <span data-ttu-id="2b19e-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="2b19e-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="2b19e-182">가족용 승용차</span><span class="sxs-lookup"><span data-stu-id="2b19e-182">Family Saloon</span></span> |
| <span data-ttu-id="2b19e-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="2b19e-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="2b19e-184">세단</span><span class="sxs-lookup"><span data-stu-id="2b19e-184">Sedan</span></span> |
| <span data-ttu-id="2b19e-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="2b19e-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="2b19e-186">하이브리드</span><span class="sxs-lookup"><span data-stu-id="2b19e-186">Hybrid</span></span> |
| <span data-ttu-id="2b19e-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="2b19e-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="2b19e-188">가족용 승용차</span><span class="sxs-lookup"><span data-stu-id="2b19e-188">Family Saloon</span></span> |
| <span data-ttu-id="2b19e-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="2b19e-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="2b19e-190">세단</span><span class="sxs-lookup"><span data-stu-id="2b19e-190">Sedan</span></span> |
| <span data-ttu-id="2b19e-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="2b19e-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="2b19e-192">하이브리드</span><span class="sxs-lookup"><span data-stu-id="2b19e-192">Hybrid</span></span> |
| <span data-ttu-id="2b19e-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="2b19e-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="2b19e-194">가족용 승용차</span><span class="sxs-lookup"><span data-stu-id="2b19e-194">Family Saloon</span></span> |
| <span data-ttu-id="2b19e-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="2b19e-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="2b19e-196">컨버터블</span><span class="sxs-lookup"><span data-stu-id="2b19e-196">Convertible</span></span> |
| <span data-ttu-id="2b19e-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="2b19e-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="2b19e-198">스테이션 웨건</span><span class="sxs-lookup"><span data-stu-id="2b19e-198">Station Wagon</span></span> |
| <span data-ttu-id="2b19e-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="2b19e-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="2b19e-200">경차</span><span class="sxs-lookup"><span data-stu-id="2b19e-200">Compact Car</span></span> |
| <span data-ttu-id="2b19e-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="2b19e-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="2b19e-202">소형 SUV</span><span class="sxs-lookup"><span data-stu-id="2b19e-202">Small SUV</span></span> |
| <span data-ttu-id="2b19e-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="2b19e-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="2b19e-204">스포츠카</span><span class="sxs-lookup"><span data-stu-id="2b19e-204">Sports Car</span></span> |
| <span data-ttu-id="2b19e-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="2b19e-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="2b19e-206">중형 SUV</span><span class="sxs-lookup"><span data-stu-id="2b19e-206">Medium SUV</span></span> |
| <span data-ttu-id="2b19e-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="2b19e-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="2b19e-208">스테이션 웨건</span><span class="sxs-lookup"><span data-stu-id="2b19e-208">Station Wagon</span></span> |
| <span data-ttu-id="2b19e-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="2b19e-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="2b19e-210">대형 SUV</span><span class="sxs-lookup"><span data-stu-id="2b19e-210">Large SUV</span></span> |
| <span data-ttu-id="2b19e-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="2b19e-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="2b19e-212">대형 SUV</span><span class="sxs-lookup"><span data-stu-id="2b19e-212">Large SUV</span></span> |
| <span data-ttu-id="2b19e-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="2b19e-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="2b19e-214">쿠페</span><span class="sxs-lookup"><span data-stu-id="2b19e-214">Coupe</span></span> |
| <span data-ttu-id="2b19e-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="2b19e-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="2b19e-216">세단</span><span class="sxs-lookup"><span data-stu-id="2b19e-216">Sedan</span></span> |
| <span data-ttu-id="2b19e-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="2b19e-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="2b19e-218">하이브리드</span><span class="sxs-lookup"><span data-stu-id="2b19e-218">Hybrid</span></span> |
| <span data-ttu-id="2b19e-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="2b19e-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="2b19e-220">가족용 승용차</span><span class="sxs-lookup"><span data-stu-id="2b19e-220">Family Saloon</span></span> |
| <span data-ttu-id="2b19e-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="2b19e-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="2b19e-222">세단</span><span class="sxs-lookup"><span data-stu-id="2b19e-222">Sedan</span></span> |
| <span data-ttu-id="2b19e-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="2b19e-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="2b19e-224">하이브리드</span><span class="sxs-lookup"><span data-stu-id="2b19e-224">Hybrid</span></span> |
| <span data-ttu-id="2b19e-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="2b19e-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="2b19e-226">가족용 승용차</span><span class="sxs-lookup"><span data-stu-id="2b19e-226">Family Saloon</span></span> |
| <span data-ttu-id="2b19e-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="2b19e-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="2b19e-228">세단</span><span class="sxs-lookup"><span data-stu-id="2b19e-228">Sedan</span></span> |
| <span data-ttu-id="2b19e-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="2b19e-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="2b19e-230">하이브리드</span><span class="sxs-lookup"><span data-stu-id="2b19e-230">Hybrid</span></span> |
| <span data-ttu-id="2b19e-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="2b19e-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="2b19e-232">가족용 승용차</span><span class="sxs-lookup"><span data-stu-id="2b19e-232">Family Saloon</span></span> |
| <span data-ttu-id="2b19e-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="2b19e-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="2b19e-234">컨버터블</span><span class="sxs-lookup"><span data-stu-id="2b19e-234">Convertible</span></span> |
| <span data-ttu-id="2b19e-235">…….</span><span class="sxs-lookup"><span data-stu-id="2b19e-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="2b19e-236">참조</span><span class="sxs-lookup"><span data-stu-id="2b19e-236">References</span></span>
[<span data-ttu-id="2b19e-237">차량 텔레매틱스 시뮬레이터 Visual Studio 솔루션</span><span class="sxs-lookup"><span data-stu-id="2b19e-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="2b19e-238">Azure 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="2b19e-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="2b19e-239">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="2b19e-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="2b19e-240">수집</span><span class="sxs-lookup"><span data-stu-id="2b19e-240">Ingestion</span></span>
<span data-ttu-id="2b19e-241">Azure 이벤트 허브, 스트림 분석 및 데이터 팩터리의의 조합은 사용된 tooingest hello 차량 신호를 hello 진단 이벤트 및 실시간 분석을 일괄 처리 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="2b19e-242">이러한 구성 요소가 모두 생성 및 hello 솔루션 배포의 일부로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="2b19e-243">실시간 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-243">Real-time analysis</span></span>
<span data-ttu-id="2b19e-244">hello hello 차량 전자 통신 정보 시뮬레이터에 의해 생성 된 이벤트 게시 된 이벤트 허브 SDK hello toohello 이벤트 허브를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="2b19e-245">hello 스트림 분석 작업 hello 이벤트 허브에서에서 이러한 이벤트를 수집 하 고 프로세스의 실시간으로 tooanalyze hello 차량 상태 데이터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![이벤트 허브 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="2b19e-247">*그림 4 - 이벤트 허브 대시보드*</span><span class="sxs-lookup"><span data-stu-id="2b19e-247">*Figure 4 - Event Hub dashboard*</span></span>

![데이터를 처리 중인 Stream Analytics 작업](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="2b19e-249">*그림 5 - 데이터를 처리 중인 Stream Analytics 작업*</span><span class="sxs-lookup"><span data-stu-id="2b19e-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="2b19e-250">hello 스트림 분석 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="2b19e-251">hello 이벤트 허브에서에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="2b19e-252">hello 참조 데이터 toomap hello 차량 VIN toohello 해당 모델을 사용 하 여 연결을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="2b19e-253">충분한 일괄 분석을 위해 Azure Blob Storage에 유지</span><span class="sxs-lookup"><span data-stu-id="2b19e-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="2b19e-254">hello 다음 스트림 분석 쿼리는 Azure blob 저장소로 사용 되는 toopersist hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![데이터 수집을 위한 Stream Analytics 작업 쿼리](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="2b19e-256">*그림 6 - 데이터 수집을 위한 Stream Analytics 작업 쿼리*</span><span class="sxs-lookup"><span data-stu-id="2b19e-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="2b19e-257">일괄 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-257">Batch analysis</span></span>
<span data-ttu-id="2b19e-258">또한 더욱 충분한 일괄 분석을 위해 시뮬레이션된 차량 신호와 진단 데이터 집합의 추가 볼륨을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="2b19e-259">이 필수 tooensure 일괄 처리에 대 한 적절 한 대표 데이터 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="2b19e-260">이 작업을 위해 사용 하 여 "PrepareSampleDataPipeline" hello Azure Data Factory 워크플로 toogenerate에 이름이 지정 된 파이프라인 시뮬레이션 된 차량 신호 및 진단 데이터 집합에 1 년 동안의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="2b19e-261">클릭 [Data Factory 사용자 지정 활동](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello DotNet 활동을 사용자 지정 하는 데이터 팩터리. 사용자 지정을 위한 Visual Studio 솔루션 요구 사항에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![일괄 처리 워크플로를 위한 샘플 데이터 준비](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="2b19e-263">*그림 7 - 일괄 처리 워크플로를 위한 샘플 데이터 준비*</span><span class="sxs-lookup"><span data-stu-id="2b19e-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="2b19e-264">hello 파이프라인의 사용자 지정 ADF.Net 구성 됩니다. 작업을 여기에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline 작업](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="2b19e-266">*그림 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="2b19e-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="2b19e-267">Hello 파이프라인 성공적으로 실행 되 고 1 년 분량의 시뮬레이션 된 차량 신호 및 진단 "RawCarEventsTable" dataset "준비" 표시는 데이터는 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="2b19e-268">Hello 다음을 참조 폴더 및 hello "connectedcar" 컨테이너 아래에서 저장소 계정에서 만든 파일:</span><span class="sxs-lookup"><span data-stu-id="2b19e-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![PrepareSampleDataPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="2b19e-270">*그림 9 - PrepareSampleDataPipeline 출력*</span><span class="sxs-lookup"><span data-stu-id="2b19e-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="2b19e-271">참조</span><span class="sxs-lookup"><span data-stu-id="2b19e-271">References</span></span>
[<span data-ttu-id="2b19e-272">스트림 수집을 위한 Azure 이벤트 허브 SDK</span><span class="sxs-lookup"><span data-stu-id="2b19e-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="2b19e-273">[Azure Data Factory 데이터 이동 기능](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet 작업](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="2b19e-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="2b19e-274">샘플 데이터 준비를 위한 Azure 데이터 팩터리 DotNet 작업 Visual Studio 솔루션</span><span class="sxs-lookup"><span data-stu-id="2b19e-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="2b19e-275">데이터 집합을 분할 hello</span><span class="sxs-lookup"><span data-stu-id="2b19e-275">Partition hello dataset</span></span>
<span data-ttu-id="2b19e-276">hello 원시 반 구조화 된 차량 신호 및 진단 데이터 집합을 YEAR/MONTH 형식 hello 데이터 준비 단계에서 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="2b19e-277">다음 hello 첫 번째 계정으로 blob 하나 계정 toohello에서 장애 조치를 사용 하 여 확장 가능한 장기 저장소 꽉 차면 및 보다 효율적인 쿼리를 승격이 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="2b19e-278">Hello 솔루션의이 단계는 적용 가능한 유일한 toobatch 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="2b19e-279">입력 및 출력 데이터 데이터 관리:</span><span class="sxs-lookup"><span data-stu-id="2b19e-279">Input and output data data management:</span></span>

* <span data-ttu-id="2b19e-280">hello **출력 데이터** (레이블이 *PartitionedCarEventsTable*) toobe로 유지 되는 오랜 시간에 대 한 hello 기본 / "rawest" 형식의 "데이터 레이크" hello 고객의에서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="2b19e-281">hello **입력 데이터** toothis 파이프라인은 일반적으로 무시 hello 출력 데이터의 충실도 toohello 입력-(분할) 보다 잘 후속 사용 하기 위해 방금 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![자동차 이벤트 분할 워크플로](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="2b19e-283">*그림 10 - 자동차 이벤트 분할 워크플로*</span><span class="sxs-lookup"><span data-stu-id="2b19e-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="2b19e-284">hello 원시 데이터에서 "PartitionCarEventsPipeline" HDInsight Hive 활동을 사용 하 여 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="2b19e-285">1 년에 대해 1 단계에서 생성 된 hello 예제 데이터는 YEAR/MONTH로 분할 되므로</span><span class="sxs-lookup"><span data-stu-id="2b19e-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="2b19e-286">hello 파티션은 연도의 매월 (총 12 파티션)에 대 한 사용 되는 toogenerate 차량 신호 및 진단 데이터는입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline 작업](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="2b19e-288">*그림 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="2b19e-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="2b19e-289">***PartitionConnectedCarEvents 하이브 스크립트***</span><span class="sxs-lookup"><span data-stu-id="2b19e-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="2b19e-290">hello "partitioncarevents.hql" 이라는 다음 하이브 스크립트 분할에 사용 있고는 hello 다운로드 zip의 hello "\demo\src\connectedcar\scripts" 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="2b19e-291">Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![분할된 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="2b19e-293">*그림 12 - 분할된 출력*</span><span class="sxs-lookup"><span data-stu-id="2b19e-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="2b19e-294">hello 데이터 액세스에 최적화 된 이제는, 좀 더 관리 및 toogain 풍부한 일괄 처리 insights 추가 처리할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="2b19e-295">데이터 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-295">Data Analysis</span></span>
<span data-ttu-id="2b19e-296">이 섹션에서는 Azure 스트림 분석 toocombine, Azure 기계 학습, Azure 데이터 팩터리 및 풍부한에 대 한 Azure HDInsight의 고급 표시 분석 차량 상태 및 구동 습관입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="2b19e-297">다음과 같은 세 개의 하위 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-297">There are three subsections here:</span></span>

1. <span data-ttu-id="2b19e-298">**기계 학습**:이 하위 섹션에서는 유지 관리 및 차량 회수 toosafety 문제 때문에 필요한 서비스 필요한이 솔루션 toopredict 수단을 사용 했습니다 hello 비정상 탐지 실험에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="2b19e-299">**실시간 분석**:이 하위 섹션에 대 한 hello 실시간 분석 hello 기계 학습 작업 활용 및 hello 스트림 분석 쿼리 언어를 사용 하 여 사용자 지정 응용 프로그램을 사용 하 여 실시간으로에서 실험 하는 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="2b19e-300">**분석을 일괄 처리**:이 하위 섹션 hello Azure HDInsight 및 Azure 데이터 팩터리에서 병원 Azure 기계 학습을 사용 하 여 hello 일괄 처리 데이터를 처리 하 고 변환에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="2b19e-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2b19e-301">Machine Learning</span></span>
<span data-ttu-id="2b19e-302">우리의 목적은 유지 관리 또는 특정 heath 통계에 따라 회수 필요한 toopredict hello 수단입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="2b19e-303">Hello를 다음 가정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-303">We make hello following assumptions</span></span>

* <span data-ttu-id="2b19e-304">Hello 다음 세 가지 조건 중 하나에 해당할 경우 hello 차량 필요 **유지 관리 서비스**:</span><span class="sxs-lookup"><span data-stu-id="2b19e-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="2b19e-305">타이어 압력이 낮음</span><span class="sxs-lookup"><span data-stu-id="2b19e-305">Tire pressure is low</span></span>
  * <span data-ttu-id="2b19e-306">엔진 오일 수준이 낮음</span><span class="sxs-lookup"><span data-stu-id="2b19e-306">Engine oil level is low</span></span>
  * <span data-ttu-id="2b19e-307">엔진 온도가 높음</span><span class="sxs-lookup"><span data-stu-id="2b19e-307">Engine temperature is high</span></span>
* <span data-ttu-id="2b19e-308">Hello 다음 조건 중 하나에 해당할 경우에 hello 차량 있을 수는 **안전 문제** 필요 **회수**:</span><span class="sxs-lookup"><span data-stu-id="2b19e-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="2b19e-309">엔진 온도가 높지만 외부 온도는 낮음</span><span class="sxs-lookup"><span data-stu-id="2b19e-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="2b19e-310">엔진 온도가 낮지만 외부 온도는 높음</span><span class="sxs-lookup"><span data-stu-id="2b19e-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="2b19e-311">Hello 이전 요구 사항에 따라, 만들어져 차량 유지 관리 검색 및 차량 회수 검색에 대 한 두 개의 별도 모델 toodetect 예외.</span><span class="sxs-lookup"><span data-stu-id="2b19e-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="2b19e-312">이러한 두 모델 hello 기본 제공 보안 주체 PCA (주성분 분석) 알고리즘 이상 탐지에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="2b19e-313">**유지 관리 감지 모델**</span><span class="sxs-lookup"><span data-stu-id="2b19e-313">**Maintenance detection model**</span></span>

<span data-ttu-id="2b19e-314">각 조건에 맞는-tire 압력, 엔진 석유 또는 엔진 온도-세 표시기 중 하나 hello 유지 관리 탐지 모델은 비정상 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="2b19e-315">따라서 필요 tooconsider hello 모델 작성에 이러한 세 개의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="2b19e-316">Azure 기계 학습에서의 실험에서 처음 사용 하 여는 **데이터 집합의 열 선택** 모듈 tooextract 이러한 세 개의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="2b19e-317">그런 다음 hello PCA 기반 비정상 검색 모듈 toobuild hello 이상 탐지 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="2b19e-318">주 구성 요소 분석 PCA ()가 적용 된 toofeature 선택, 분류 및 변칙 검색 될 수 있는 기계 학습의 인정 받는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="2b19e-319">PCA는 가능하면 상관된 변수가 포함된 사례 집합을 주성분이라는 값 집합으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="2b19e-320">PCA 기반 모델링의 hello 핵심 아이디어는 기능 및 예외 보다 쉽게 식별할 수 있도록 차원 하위 공간으로 tooproject 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="2b19e-321">새로운 각 입력에는 너무 탐지 모델 hello에 대 한 hello 비정상 탐지기 hello 고유 벡터에 프로젝션으로 먼저 계산 하 고 계산 hello 표준화 재구성 오류.</span><span class="sxs-lookup"><span data-stu-id="2b19e-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="2b19e-322">이 정규화 된 오류는 hello 비정상 점수입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="2b19e-323">더 높은 hello 오류 hello hello 더 비정상적인 hello 인스턴스가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="2b19e-324">검색 문제를 유지 관리 하는 hello 각 레코드 좌표 tire 압력과 엔진 석유 엔진 온도에 정의 된 3 차원 공간에서 지점으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="2b19e-325">toocapture 이러한 비정상 PCA를 사용 하 여 2 차원 공간 hello hello 3 차원 공간에서 원래 데이터를 프로젝션 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="2b19e-326">따라서 hello 매개 변수 수가 구성 요소 toouse PCA toobe 2에서에서 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="2b19e-327">이 매개 변수는 PCA 기반 이상 감지를 적용하는 데 중요한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="2b19e-328">PCA를 사용하여 데이터를 표현하면 이러한 이상을 보다 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="2b19e-329">**이상 탐지 모델 회수** hello 회수 이상 탐지 모델을 사용 하 여 hello 데이터 집합과 PCA 기반 비정상 열 선택 비슷한 방법으로 검색 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="2b19e-330">처음 세 개의 변수-엔진 온도, 외부 기온, 기 속도-hello를 사용 하 여 추출할 특히 **데이터 집합의 열 선택** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="2b19e-331">또한 hello 속도 포함 변수 hello 엔진 온도 일반적으로 이므로 toohello 속도 상관 관계가 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="2b19e-332">그런 다음 PCA 기반 비정상 검색 모듈 tooproject hello 데이터를 사용 하 여 hello 3 차원 공간에서으로 2 차원 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="2b19e-333">충족 하는 hello 회수 조건을 이루어지며 하므로 hello 차량 회수 엔진 온도 및 외부 온도 부정적인 높은 상호 연결 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2b19e-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="2b19e-334">PCA 기반 비정상 검색 알고리즘을 사용 하 여 우리 PCA를 수행한 후 hello 변칙을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="2b19e-335">두 모델을 학습할 때 유지 관리 또는 회수 hello 입력된 데이터 tootrain hello PCA 기반 비정상 검색 모델으로 요구 하지 않는 toouse 일반 데이터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="2b19e-336">Hello 실험 점수 매기기, 유지 관리 또는 회수 hello 차량 필요 여부 hello 학습 된 비정상 검색 모델 toodetect을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="2b19e-337">실시간 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-337">Real-time analysis</span></span>
<span data-ttu-id="2b19e-338">스트림 분석 SQL 쿼리를 수행 하는 hello 사용 되는 모든 tooget hello 평균 hello 차량 속도, 연료 수준, 엔진 온도, 주행 기록 계 읽기, 타이어 압력, 엔진 석유 수준 및 다른 사용자와 같은 중요 한 차량 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="2b19e-339">hello 평균은 사용 되는 toodetect 예외 경고를 발생 하 고 확인 후 toodemographics로 서로 연결 하 고 특정 지역에서 작동 하는 자동차의 전반적인 상태 조건 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![실시간 처리를 위한 Stream Analytics 쿼리](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="2b19e-341">*그림 13 - 실시간 처리를 위한 Stream Analytics 쿼리*</span><span class="sxs-lookup"><span data-stu-id="2b19e-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="2b19e-342">모든 hello 평균 3 초 TumblingWindow에 대해 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="2b19e-343">이 경우 중복되지 않는 연속적인 시간 간격이 필요하므로 TubmlingWindow를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="2b19e-344">Azure 스트림 분석에서 모든 hello "Windowing" 기능에 대해 자세히 toolearn 클릭 [창 작업 (Azure 스트림 분석)](https://msdn.microsoft.com/library/azure/dn835019.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="2b19e-345">**실시간 예측**</span><span class="sxs-lookup"><span data-stu-id="2b19e-345">**Real-time prediction**</span></span>

<span data-ttu-id="2b19e-346">응용 프로그램은 실제 시간에서 hello 솔루션 toooperationalize hello 기계 학습 모델의 일부로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="2b19e-347">이 응용 프로그램 "RealTimeDashboardApp" 라는 만들어지고 hello 솔루션 배포의 일부로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="2b19e-348">hello 응용 프로그램에서는 hello 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="2b19e-349">여기서 스트림 분석은 이벤트를 게시 hello 패턴에서 지속적으로 tooan 이벤트 허브 인스턴스를 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="2b19e-350">![스트림 분석 쿼리 hello 데이터 게시를 위한](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *그림 14-hello 데이터 tooan 게시에 대 한 스트림 분석 쿼리 출력 이벤트 허브 인스턴스*</span><span class="sxs-lookup"><span data-stu-id="2b19e-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="2b19e-351">이 응용 프로그램이 수신하는 모든 이벤트에 대해 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="2b19e-352">시스템 학습 요청-응답 점수 매기기 (RR) 끝점을 사용 하 여 hello 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="2b19e-353">hello RR 끝점 hello 배포의 일부로 자동으로 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="2b19e-354">hello RR 출력은 hello 푸시 Api를 사용 하 여 게시 된 tooa Power BI 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="2b19e-355">이 패턴을 볼 toointegrate hello 실시간 분석 흐름에 따라 비즈니스 줄 (lob 기간 업무) 응용 프로그램 경고, 알림 및 메시징 등의 시나리오에 적용 가능한 tooscenarios 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="2b19e-356">클릭 [RealtimeDashboardApp 다운로드](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio 솔루션에 대 한 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="2b19e-357">**tooexecute hello 실시간 대시보드 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="2b19e-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="2b19e-358">로컬로 추출 및 저장 ![RealtimeDashboardApp 폴더](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *그림 16 - RealtimeDashboardApp 폴더*</span><span class="sxs-lookup"><span data-stu-id="2b19e-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="2b19e-359">Hello RealtimeDashboardApp.exe 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2b19e-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="2b19e-360">유효한 Power BI 자격 증명을 제공하고 로그인한 후 동의를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![실시간 대시보드 응용 프로그램 로그인 tooPower 비교 BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![실시간 대시보드 응용 프로그램 로그인 tooPower BI 마침](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="2b19e-363">*그림 17-RealtimeDashboardApp: 로그인 tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="2b19e-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="2b19e-364">Tooflush hello Power BI 데이터 집합을 원하는 경우 hello RealtimeDashboardApp hello "flushdata" 매개 변수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="2b19e-365">일괄 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-365">Batch analysis</span></span>
<span data-ttu-id="2b19e-366">hello 목적은 tooshow Contoso 모터 어떻게 활용 hello Azure 계산 기능 tooharness 빅 데이터 toogain 풍부한 인 사이트에 운전 패턴, 사용량 동작 및 차량 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="2b19e-367">이를 통해 다음이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-367">This makes it possible to:</span></span>

* <span data-ttu-id="2b19e-368">운전 습관 및 연료 효율적인 구동 동작에 통찰력을 제공 하 여 더 저렴 하 게 하는 hello 고객 환경 개선</span><span class="sxs-lookup"><span data-stu-id="2b19e-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="2b19e-369">고객 및 구동 패턴 toogovern 비즈니스 의사 결정의 사전 확인 하 고 hello를 가장 잘 클래스 제품 및 서비스에 제공</span><span class="sxs-lookup"><span data-stu-id="2b19e-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="2b19e-370">이 솔루션에서는 다음 메트릭을 hello 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="2b19e-371">**전체 업그레이드 동작을 구동**: hello hello 모델, 위치, 구동 조건 및 구동 적극적인 패턴에 대 한 hello 연도 toogain 통찰력의 시간 추세를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="2b19e-372">Contoso Motors는 마케팅 캠페인, 주행에 새롭게 개인 설정된 기능 및 사용 현황에 따른 보험에 이를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="2b19e-373">**효율적인 구동 동작 연료**: hello hello 모델, 위치, 구동 조건 및 연료 효율적인 구동 패턴에 대 한 hello 연도 toogain 통찰력 시간의 추세를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="2b19e-374">Contoso 모터 이러한 insights를 사용 마케팅 캠페인, 새로운 기능을 구동 하 고 보고 하는 사전 toohello 드라이버에 대 한 유효 및 환경 친숙 한 구동 습관 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="2b19e-375">**모델을 회수**: 회수 hello 변칙 검색 기계 학습 실험 작업 활용 하 여 필요한 모델 식별</span><span class="sxs-lookup"><span data-stu-id="2b19e-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="2b19e-376">이러한 메트릭의 각 hello 세부 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="2b19e-377">**공격적인 주행 패턴**</span><span class="sxs-lookup"><span data-stu-id="2b19e-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="2b19e-378">hello 차량 신호를 분할 하 고 진단 데이터는 처리 하이브 toodetermine hello 모델, 위치, 자동차를 사용 하 여 "AggresiveDrivingPatternPipeline" 라는 hello 파이프라인에서 구동 조건 및 다른 매개 변수를 보여 주는 적극적인 구동 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="2b19e-379">![적극적인 구동 패턴 워크플로](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
 *그림 18 - 적극적인 구동 패턴 워크플로*</span><span class="sxs-lookup"><span data-stu-id="2b19e-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="2b19e-380">***공격적인 주행 패턴 하이브 쿼리***</span><span class="sxs-lookup"><span data-stu-id="2b19e-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="2b19e-381">hello 라는 "aggresivedriving.hql" 적극적인 구동 조건 패턴 분석에 사용 된 Hive 스크립트는 hello 다운로드 zip의 "\demo\src\connectedcar\scripts" 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="2b19e-382">자동차의 전송 기어 위치, 브레이크 페달 상태 및 속도 toodetect 무모/적극적인 브레이크 빠른 속도로 패턴에 따라 동작을 구동의 hello 조합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="2b19e-383">Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![AggressiveDrivingPatternPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="2b19e-385">*그림 19 - AggressiveDrivingPatternPipeline 출력*</span><span class="sxs-lookup"><span data-stu-id="2b19e-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="2b19e-386">**연료 효율이 좋은 주행 패턴**</span><span class="sxs-lookup"><span data-stu-id="2b19e-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="2b19e-387">hello 차량 신호를 분할 하 고 진단 데이터는 "FuelEfficientDrivingPatternPipeline" 라는 hello 파이프라인에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="2b19e-388">하이브 사용 되는 toodetermine hello 모델, 위치, 자동차를 움직일, 운전 환경 및 연료 효율적인 구동 패턴을 제공 하는 기타 속성도입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![연료 효율이 좋은 주행 패턴](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="2b19e-390">*그림 20 - 연료 효율이 좋은 주행 패턴 워크플로*</span><span class="sxs-lookup"><span data-stu-id="2b19e-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="2b19e-391">***연료 효율이 좋은 주행 패턴 하이브 쿼리***</span><span class="sxs-lookup"><span data-stu-id="2b19e-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="2b19e-392">hello 라는 "fuelefficientdriving.hql" 적극적인 구동 조건 패턴 분석에 사용 된 Hive 스크립트는 hello 다운로드 zip의 "\demo\src\connectedcar\scripts" 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="2b19e-393">자동차의 전송 기어 위치, 페달 브레이크 상태, 속도 및 가속기 페달 위치 toodetect 연료 브레이크, 가속에 기반 하 여 효율적인 구동 동작 hello 조합을 사용 하 고 패턴 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="2b19e-394">Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![FuelEfficientDrivingPatternPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="2b19e-396">*그림 21 - FuelEfficientDrivingPatternPipeline 출력*</span><span class="sxs-lookup"><span data-stu-id="2b19e-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="2b19e-397">**회수 예측**</span><span class="sxs-lookup"><span data-stu-id="2b19e-397">**Recall Predictions**</span></span>

<span data-ttu-id="2b19e-398">hello 기계 학습 실험은 프로 비전 및 hello 솔루션 배포의 일부로 웹 서비스로 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="2b19e-399">hello 일괄 처리 끝점을 점수 매기기 데이터 팩터리에 연결 된 서비스로 등록 하 고 데이터 팩터리 일괄 처리 점수 매기기 활동을 사용 하 여 병원이 워크플로의 활용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Machine Learning 끝점](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="2b19e-401">*그림 22 - Data Factory의 연결된 서비스로 등록된 Machine Learning 끝점*</span><span class="sxs-lookup"><span data-stu-id="2b19e-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="2b19e-402">hello 등록 된 연결 된 서비스에에서 사용 됩니다 hello 이상 탐지 모델을 사용 하 여 hello DetectAnomalyPipeline tooscore hello 데이터.</span><span class="sxs-lookup"><span data-stu-id="2b19e-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Data Factory에서 Machine Learning 일괄 처리 점수 매기기 활동](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="2b19e-404">*그림 23 – Data Factory에서 Azure Machine Learning 일괄 처리 점수 매기기 활동*</span><span class="sxs-lookup"><span data-stu-id="2b19e-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="2b19e-405">웹 서비스를 평가 하는 hello 일괄 처리와 병원 될 수 있도록 데이터 준비에 대 한이 파이프라인에서 수행 하는 몇 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![회수가 필요한 차량을 예측하기 위한 DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="2b19e-407">*그림 24 - 회수가 필요한 차량을 예측하기 위한 DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="2b19e-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="2b19e-408">***변칙 검색 Hive 쿼리***</span><span class="sxs-lookup"><span data-stu-id="2b19e-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="2b19e-409">Hello 점수 매기기가 완료 되 면 사용 되는 tooprocess 및 비정상을 확률 점수로 0.60 이상의 hello 모델에 의해 분류 되는 집계 hello 데이터 HDInsight 활동은.</span><span class="sxs-lookup"><span data-stu-id="2b19e-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="2b19e-410">Hello 파이프라인 성공적으로 실행 되 면 hello hello "connectedcar" 컨테이너 아래에서 저장소 계정에 생성 된 파티션을 다음 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![DetectAnomalyPipeline 출력](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="2b19e-412">*그림 25 – DetectAnomalyPipeline 출력*</span><span class="sxs-lookup"><span data-stu-id="2b19e-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="2b19e-413">게시</span><span class="sxs-lookup"><span data-stu-id="2b19e-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="2b19e-414">실시간 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-414">Real-time analysis</span></span>
<span data-ttu-id="2b19e-415">Hello Stream Analytics 작업에서 hello 쿼리 중 하나 게시 hello 이벤트 tooan 출력 이벤트 허브 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="2b19e-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![스트림 분석 작업이 게시 tooan 출력 이벤트 허브 인스턴스](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="2b19e-417">*그림 26-스트림 분석 작업 게시 tooan 출력 이벤트 허브 인스턴스*</span><span class="sxs-lookup"><span data-stu-id="2b19e-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![스트림 분석 쿼리 toopublish toohello 출력 이벤트 허브 인스턴스](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="2b19e-419">*그림 27-스트림 분석 쿼리 toopublish toohello 출력 이벤트 허브 인스턴스*</span><span class="sxs-lookup"><span data-stu-id="2b19e-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="2b19e-420">이 이벤트 스트림의 RealTimeDashboardApp hello 솔루션에 포함 된 hello에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="2b19e-421">이 응용 프로그램 실시간 점수 매기기에 대 한 hello 컴퓨터 학습 요청-응답 웹 서비스를 활용 하며 hello 결과 데이터 tooa Power BI 데이터 집합에 사용 하기 위해 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="2b19e-422">일괄 분석</span><span class="sxs-lookup"><span data-stu-id="2b19e-422">Batch analysis</span></span>
<span data-ttu-id="2b19e-423">hello hello 일괄 처리 및 실시간 처리 결과가 소비에 대 한 게시 된 toohello Azure SQL 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="2b19e-424">hello Azure SQL Server, 데이터베이스 및 테이블 hello hello 설치 스크립트의 일부로 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![결과 처리 하는 일괄 처리 복사 toodata 마트 워크플로](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="2b19e-426">*그림 28-일괄 처리 결과 복사 toodata 마트 워크플로*</span><span class="sxs-lookup"><span data-stu-id="2b19e-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![스트림 분석 작업이 toodata 마트 게시](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="2b19e-428">*그림 29-스트림 분석 작업 toodata 마트 게시*</span><span class="sxs-lookup"><span data-stu-id="2b19e-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Stream Analytics 작업에서 데이터 마트 설정](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="2b19e-430">*그림 30 - Stream Analytics 작업에서 데이터 마트 설정*</span><span class="sxs-lookup"><span data-stu-id="2b19e-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="2b19e-431">사용</span><span class="sxs-lookup"><span data-stu-id="2b19e-431">Consume</span></span>
<span data-ttu-id="2b19e-432">Power BI는 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="2b19e-433">Hello Power BI 보고서 및 대시보드 hello 설정에 대 한 자세한 내용은 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="2b19e-434">hello 최종 대시보드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-434">hello final dashboard looks like this:</span></span>

![Power BI 대시보드](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="2b19e-436">*그림 31 - Power BI 대시보드*</span><span class="sxs-lookup"><span data-stu-id="2b19e-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="2b19e-437">요약</span><span class="sxs-lookup"><span data-stu-id="2b19e-437">Summary</span></span>
<span data-ttu-id="2b19e-438">이 문서에는 hello 차량 원격 분석 분석 솔루션의 자세한 드릴 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="2b19e-439">예측 및 동작과 함께 실시간 및 일괄 분석을 위한 람다 아키텍처 패턴을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="2b19e-440">이 패턴 tooa 다양 한 범위의 실행 부하 과다 경로 (실시간)를 필요로 하는 사용 사례를 적용 및 콜드 경로 (일괄 처리) 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b19e-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

