---
title: "aaaPredictive 유지 관리 연습 | Microsoft Docs"
description: "Hello Azure IoT 예측 유지 관리의 연습 미리 솔루션을 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a><span data-ttu-id="82146-103">미리 구성된 예측 유지 관리 솔루션 연습</span><span class="sxs-lookup"><span data-stu-id="82146-103">Predictive maintenance preconfigured solution walkthrough</span></span>

<span data-ttu-id="82146-104">hello 미리 구성 하는 예측 유지 관리 솔루션은 문제일 가능성이 toooccur이 있는 hello 지점을 예측 하는 비즈니스 시나리오에 대 한 종단 간 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-104">hello predictive maintenance preconfigured solution is an end-to-end solution for a business scenario that predicts hello point at which a failure is likely toooccur.</span></span> <span data-ttu-id="82146-105">유지 관리를 최적화하는 등의 작업에 미리 구성된 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82146-105">You can use this preconfigured solution proactively for activities such as optimizing maintenance.</span></span> <span data-ttu-id="82146-106">hello 솔루션은 스트림 분석, IoT Hub와 같은 핵심 Azure IoT Suite 서비스를 결합 및 [Azure 기계 학습] [ lnk-machine-learning] 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-106">hello solution combines key Azure IoT Suite services, such as IoT Hub, Stream analytics, and an [Azure Machine Learning][lnk-machine-learning] workspace.</span></span> <span data-ttu-id="82146-107">이 작업 영역에는 공용 샘플 데이터 집합, toopredict hello 남은 연수 (RUL) 비행기 엔진을 기반으로 모델을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-107">This workspace contains a model, based on a public sample data set, toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="82146-108">완전히 hello 솔루션 tooplan 하기 위한 시작 지점으로 hello IoT 비즈니스 시나리오를 구현 하 고 사용자의 특정 비즈니스 요구 사항을 충족 하는 솔루션을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-108">hello solution fully implements hello IoT business scenario as a starting point for you tooplan and implement a solution that meets your own specific business requirements.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="82146-109">논리 아키텍처</span><span class="sxs-lookup"><span data-stu-id="82146-109">Logical architecture</span></span>

<span data-ttu-id="82146-110">다음 다이어그램 hello hello hello 미리 구성 된 솔루션의 논리적 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-110">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![][img-architecture]

<span data-ttu-id="82146-111">파란색 hello 항목은 미리 구성 하는 hello 솔루션을 배포한 hello 영역에 사용자를 프로 비전 하는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-111">hello blue items are Azure services provisioned in hello region where you deployed hello preconfigured solution.</span></span> <span data-ttu-id="82146-112">hello에 hello 목록 hello 미리 구성 된 솔루션을 배포할 수 있는 영역에 표시 됩니다. [프로 비전 페이지][lnk-azureiotsuite]합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-112">hello list of regions where you can deploy hello preconfigured solution displays on hello [provisioning page][lnk-azureiotsuite].</span></span>

<span data-ttu-id="82146-113">녹색 hello 항목은 시뮬레이션 된 장치 비행기 엔진을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-113">hello green item is a simulated device that represents an aircraft engine.</span></span> <span data-ttu-id="82146-114">Hello 다음 섹션에서에서 이러한 시뮬레이션 된 장치에 대해 자세히 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="82146-114">You can learn more about these simulated devices in hello following section.</span></span>

<span data-ttu-id="82146-115">hello 회색 항목 구성 요소를 나타내는 구현 하는 *장치 관리* 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-115">hello gray items represent components that implement *device management* capabilities.</span></span> <span data-ttu-id="82146-116">hello hello 미리 구성 하는 예측 유지 관리 솔루션의 현재 릴리스에서 이러한 리소스를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82146-116">hello current release of hello predictive maintenance preconfigured solution does not provision these resources.</span></span> <span data-ttu-id="82146-117">장치 관리에 대해 자세히 toolearn 참조 toohello [미리 구성 된 솔루션 모니터링 원격][lnk-remote-monitoring]합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-117">toolearn more about device management, refer toohello [remote monitoring pre-configured solution][lnk-remote-monitoring].</span></span>

## <a name="simulated-devices"></a><span data-ttu-id="82146-118">시뮬레이션된 장치</span><span class="sxs-lookup"><span data-stu-id="82146-118">Simulated devices</span></span>

<span data-ttu-id="82146-119">시뮬레이션된 된 장치는 미리 구성 하는 hello 솔루션에서 비행기 엔진을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="82146-119">In hello preconfigured solution, a simulated device represents an aircraft engine.</span></span> <span data-ttu-id="82146-120">hello 솔루션 tooa 단일 비행기를 매핑하는 두 개의 엔진으로 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82146-120">hello solution is provisioned with two engines that map tooa single aircraft.</span></span> <span data-ttu-id="82146-121">각 엔진에서 네 가지 유형의 원격 분석: 센서 9, 센서 11, 센서 14 및 15의 센서 hello 엔진에 대 한 hello 기계 학습 모델 toocalculate hello RUL에 필요한 hello 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-121">Each engine emits four types of telemetry: Sensor 9, Sensor 11, Sensor 14, and Sensor 15 provide hello data necessary for hello Machine Learning model toocalculate hello RUL for hello engine.</span></span> <span data-ttu-id="82146-122">메시지 tooIoT 허브 원격 분석을 수행 하는 hello를 전송 하는 각 시뮬레이션 된 장치:</span><span class="sxs-lookup"><span data-stu-id="82146-122">Each simulated device sends hello following telemetry messages tooIoT Hub:</span></span>

<span data-ttu-id="82146-123">*계수 주기*.</span><span class="sxs-lookup"><span data-stu-id="82146-123">*Cycle count*.</span></span> <span data-ttu-id="82146-124">주기는 2시간에서 10시간 사이의 기간으로 완료된 비행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="82146-124">A cycle represents a completed flight with a duration between two and ten hours.</span></span> <span data-ttu-id="82146-125">Hello 비행 중 원격 분석 데이터는 30 분 마다 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="82146-125">During hello flight, telemetry data is captured every half hour.</span></span>

<span data-ttu-id="82146-126">*원격 분석*.</span><span class="sxs-lookup"><span data-stu-id="82146-126">*Telemetry*.</span></span> <span data-ttu-id="82146-127">엔진 특성을 나타내는 4가지 센서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82146-127">There are four sensors that represent engine attributes.</span></span> <span data-ttu-id="82146-128">센서 9, 센서 11, 센서 14 및 15의 센서 hello 센서는 일반적으로 레이블이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82146-128">hello sensors are generically labeled Sensor 9, Sensor 11, Sensor 14, and Sensor 15.</span></span> <span data-ttu-id="82146-129">이러한 네 가지 센서 hello RUL 모델에서 충분 한 원격 분석 tooobtain 유용한 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="82146-129">These four sensors represent telemetry sufficient tooobtain useful results from hello RUL model.</span></span> <span data-ttu-id="82146-130">미리 구성 하는 hello 솔루션에 사용 되는 hello 모델은 실제 엔진 센서 데이터를 포함 하는 공용 데이터 집합에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="82146-130">hello model used in hello preconfigured solution is created from a public data set that includes real engine sensor data.</span></span> <span data-ttu-id="82146-131">Hello 원래 데이터 집합에서 모델 hello를 생성 하는 방법에 대 한 자세한 내용은 참조 hello [Cortana Intelligence 갤러리 예측 유지 관리 템플릿][lnk-cortana-analytics]합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-131">For more information on how hello model was created from hello original data set, see hello [Cortana Intelligence Gallery Predictive Maintenance Template][lnk-cortana-analytics].</span></span>

<span data-ttu-id="82146-132">시뮬레이션 된 hello 장치 hello 다음 hello 솔루션의 hello IoT 허브에서 전송 되는 명령을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82146-132">hello simulated devices can handle hello following commands sent from hello IoT hub in hello solution:</span></span>

| <span data-ttu-id="82146-133">명령</span><span class="sxs-lookup"><span data-stu-id="82146-133">Command</span></span> | <span data-ttu-id="82146-134">설명</span><span class="sxs-lookup"><span data-stu-id="82146-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82146-135">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="82146-135">StartTelemetry</span></span> |<span data-ttu-id="82146-136">컨트롤 hello hello 시뮬레이션의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-136">Controls hello state of hello simulation.</span></span><br/><span data-ttu-id="82146-137">원격 분석 보내기 시작 hello 장치</span><span class="sxs-lookup"><span data-stu-id="82146-137">Starts hello device sending telemetry</span></span> |
| <span data-ttu-id="82146-138">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="82146-138">StopTelemetry</span></span> |<span data-ttu-id="82146-139">컨트롤 hello hello 시뮬레이션의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-139">Controls hello state of hello simulation.</span></span><br/><span data-ttu-id="82146-140">중지 hello 장치 원격 분석 보내기</span><span class="sxs-lookup"><span data-stu-id="82146-140">Stops hello device sending telemetry</span></span> |

<span data-ttu-id="82146-141">IoT Hub는 장치 명령 승인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-141">IoT Hub provides device command acknowledgment.</span></span>

## <a name="azure-stream-analytics-job"></a><span data-ttu-id="82146-142">Azure Stream Analytics 작업</span><span class="sxs-lookup"><span data-stu-id="82146-142">Azure Stream Analytics job</span></span>

<span data-ttu-id="82146-143">**작업: 원격 분석** hello 들어오는 장치 원격 분석 스트림에 두 문을 사용 하 여에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-143">**Job: Telemetry** operates on hello incoming device telemetry stream using two statements:</span></span>

* <span data-ttu-id="82146-144">먼저 hello는 hello 장치에서 모든 원격 분석을 선택 하 고이 데이터 tooblob 저장소를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="82146-144">hello first selects all telemetry from hello devices and sends this data tooblob storage.</span></span> <span data-ttu-id="82146-145">여기에서 hello 웹 응용 프로그램에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-145">From here, it is visualized in hello web app.</span></span>
* <span data-ttu-id="82146-146">hello 평균 센서 2 분 슬라이딩 윈도우를 통해 값을 이벤트 허브 tooan hello 통해이 데이터를 보내는 두 번째 계산 **이벤트 프로세서**합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-146">hello second computes average sensor values over a two-minute sliding window and sends this data through hello Event hub tooan **event processor**.</span></span>

## <a name="event-processor"></a><span data-ttu-id="82146-147">이벤트 프로세서</span><span class="sxs-lookup"><span data-stu-id="82146-147">Event processor</span></span>
<span data-ttu-id="82146-148">hello **이벤트 프로세서 호스트** Azure 웹 작업에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-148">hello **event processor host** runs in an Azure Web Job.</span></span> <span data-ttu-id="82146-149">hello **이벤트 프로세서** 완료 주기에 대 한 hello 센서 평균 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-149">hello **event processor** takes hello average sensor values for a completed cycle.</span></span> <span data-ttu-id="82146-150">그런 다음 해당 값 tooan toocalculate hello RUL는 엔진에 대 한 학습 된 모델을 노출 하는 API에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-150">It then passes those values tooan API that exposes trained model toocalculate hello RUL for an engine.</span></span> <span data-ttu-id="82146-151">hello API hello 솔루션의 일부로 제공 되는 기계 학습 작업 영역에 의해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82146-151">hello API is exposed by a Machine Learning workspace that is provisioned as part of hello solution.</span></span>

## <a name="machine-learning"></a><span data-ttu-id="82146-152">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="82146-152">Machine Learning</span></span>
<span data-ttu-id="82146-153">hello 기계 학습 구성 요소는 실제 비행기 엔진에서 수집 된 데이터에서 파생 된 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82146-153">hello Machine Learning component uses a model derived from data collected from real aircraft engines.</span></span> <span data-ttu-id="82146-154">Hello에 hello 타일에서 toohello 기계 학습 작업 영역을 탐색할 수 [azureiotsuite.com] [ lnk-azureiotsuite] 프로 비전 된 솔루션에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-154">You can navigate toohello Machine Learning workspace from hello tile on hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="82146-155">hello 타일은 사용할 수 있는 hello 솔루션은 hello 때 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-155">hello tile is available when hello solution is in hello **Ready** state.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82146-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82146-156">Next steps</span></span>
<span data-ttu-id="82146-157">Toocustomize 경우가 hello 미리 구성 하는 예측 유지 관리 솔루션의 주요 구성 요소 hello 살펴보았습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="82146-157">Now you've seen hello key components of hello predictive maintenance preconfigured solution, you may want toocustomize it.</span></span> <span data-ttu-id="82146-158">[미리 구성된 솔루션 사용자 지정에 대한 지침][lnk-customize]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82146-158">See [Guidance on customizing preconfigured solutions][lnk-customize].</span></span>

<span data-ttu-id="82146-159">탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:</span><span class="sxs-lookup"><span data-stu-id="82146-159">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="82146-160">[IoT Suite에 대한 질문과 대답][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="82146-160">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="82146-161">[Hello 접지에서 IoT 보안][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="82146-161">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/