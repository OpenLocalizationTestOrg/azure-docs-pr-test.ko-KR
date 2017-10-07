---
title: "aaaAzure IoT 솔루션 미리 구성 | Microsoft Docs"
description: "Azure IoT hello에 대 한 설명을 솔루션 및 해당 아키텍처 링크 tooadditional 리소스와 미리 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a><span data-ttu-id="26a96-103">Hello 미리 구성 된 Azure IoT Suite 솔루션은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="26a96-103">What are hello Azure IoT Suite preconfigured solutions?</span></span>

<span data-ttu-id="26a96-104">hello 미리 구성 된 Azure IoT Suite 솔루션은 tooAzure 구독을 사용 하 여 배포할 수 있음을 일반적인 IoT 솔루션 패턴의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-104">hello Azure IoT Suite preconfigured solutions are implementations of common IoT solution patterns that you can deploy tooAzure using your subscription.</span></span> <span data-ttu-id="26a96-105">Hello 미리 구성 된 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-105">You can use hello preconfigured solutions:</span></span>

* <span data-ttu-id="26a96-106">사용자 고유의 IoT 솔루션에 대한 시작점.</span><span class="sxs-lookup"><span data-stu-id="26a96-106">As a starting point for your own IoT solutions.</span></span>
* <span data-ttu-id="26a96-107">IoT 솔루션 디자인 및 개발에서 일반적인 패턴에 대 한 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-107">toolearn about common patterns in IoT solution design and development.</span></span>

<span data-ttu-id="26a96-108">미리 구성 된 각 솔루션에 사용 하 여 장치 toogenerate 원격 분석을 시뮬레이션할 완전 한 종단 간 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-108">Each preconfigured solution is a complete, end-to-end implementation that uses simulated devices toogenerate telemetry.</span></span>

<span data-ttu-id="26a96-109">Hello 전체 소스 코드 toocustomize 다운로드 하 고 hello 솔루션 toomeet 특정 IoT 요구 사항을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-109">You can download hello complete source code toocustomize and extend hello solution toomeet your specific IoT requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="26a96-110">솔루션을 미리 구성 된 hello의 toodeploy 하나, 방문 [Microsoft Azure IoT Suite][lnk-azureiotsuite]합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-110">toodeploy one of hello preconfigured solutions, visit [Microsoft Azure IoT Suite][lnk-azureiotsuite].</span></span> <span data-ttu-id="26a96-111">hello 문서 [hello 미리 구성 된 IoT 솔루션 시작] [ lnk-getstarted-preconfigured] 방법 중 하나를 실행된 하 고 toodeploy hello 솔루션에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-111">hello article [Get started with hello IoT preconfigured solutions][lnk-getstarted-preconfigured] provides more information about how toodeploy and run one of hello solutions.</span></span>

<span data-ttu-id="26a96-112">hello 다음 표에 나와 hello 솔루션 toospecific IoT 기능:</span><span class="sxs-lookup"><span data-stu-id="26a96-112">hello following table shows how hello solutions map toospecific IoT features:</span></span>

| <span data-ttu-id="26a96-113">해결 방법</span><span class="sxs-lookup"><span data-stu-id="26a96-113">Solution</span></span> | <span data-ttu-id="26a96-114">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="26a96-114">Data ingestion</span></span> | <span data-ttu-id="26a96-115">장치 ID</span><span class="sxs-lookup"><span data-stu-id="26a96-115">Device identity</span></span> | <span data-ttu-id="26a96-116">장치 관리</span><span class="sxs-lookup"><span data-stu-id="26a96-116">Device management</span></span> | <span data-ttu-id="26a96-117">명령 및 컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a96-117">Command and control</span></span> | <span data-ttu-id="26a96-118">규칙 및 동작</span><span class="sxs-lookup"><span data-stu-id="26a96-118">Rules and actions</span></span> | <span data-ttu-id="26a96-119">예측 분석</span><span class="sxs-lookup"><span data-stu-id="26a96-119">Predictive analytics</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="26a96-120">[원격 모니터링][lnk-getstarted-preconfigured]</span><span class="sxs-lookup"><span data-stu-id="26a96-120">[Remote monitoring][lnk-getstarted-preconfigured]</span></span> |<span data-ttu-id="26a96-121">예</span><span class="sxs-lookup"><span data-stu-id="26a96-121">Yes</span></span> |<span data-ttu-id="26a96-122">예</span><span class="sxs-lookup"><span data-stu-id="26a96-122">Yes</span></span> |<span data-ttu-id="26a96-123">예</span><span class="sxs-lookup"><span data-stu-id="26a96-123">Yes</span></span> |<span data-ttu-id="26a96-124">예</span><span class="sxs-lookup"><span data-stu-id="26a96-124">Yes</span></span> |<span data-ttu-id="26a96-125">예</span><span class="sxs-lookup"><span data-stu-id="26a96-125">Yes</span></span> |- |
| <span data-ttu-id="26a96-126">[예측 유지 관리][lnk-predictive-maintenance]</span><span class="sxs-lookup"><span data-stu-id="26a96-126">[Predictive maintenance][lnk-predictive-maintenance]</span></span> |<span data-ttu-id="26a96-127">예</span><span class="sxs-lookup"><span data-stu-id="26a96-127">Yes</span></span> |<span data-ttu-id="26a96-128">예</span><span class="sxs-lookup"><span data-stu-id="26a96-128">Yes</span></span> |- |<span data-ttu-id="26a96-129">예</span><span class="sxs-lookup"><span data-stu-id="26a96-129">Yes</span></span> |<span data-ttu-id="26a96-130">예</span><span class="sxs-lookup"><span data-stu-id="26a96-130">Yes</span></span> |<span data-ttu-id="26a96-131">예</span><span class="sxs-lookup"><span data-stu-id="26a96-131">Yes</span></span> |
| <span data-ttu-id="26a96-132">[연결된 공장][lnk-getstarted-factory]</span><span class="sxs-lookup"><span data-stu-id="26a96-132">[Connected factory][lnk-getstarted-factory]</span></span> |<span data-ttu-id="26a96-133">예</span><span class="sxs-lookup"><span data-stu-id="26a96-133">Yes</span></span> |<span data-ttu-id="26a96-134">예</span><span class="sxs-lookup"><span data-stu-id="26a96-134">Yes</span></span> |<span data-ttu-id="26a96-135">예</span><span class="sxs-lookup"><span data-stu-id="26a96-135">Yes</span></span> |<span data-ttu-id="26a96-136">예</span><span class="sxs-lookup"><span data-stu-id="26a96-136">Yes</span></span> |<span data-ttu-id="26a96-137">예</span><span class="sxs-lookup"><span data-stu-id="26a96-137">Yes</span></span> |- |

* <span data-ttu-id="26a96-138">*데이터 수집*: toohello 클라우드 눈금에서의 데이터는 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-138">*Data ingestion*: Ingress of data at scale toohello cloud.</span></span>
* <span data-ttu-id="26a96-139">*장치 id*: 고유한 장치 id를 관리 하 고 장치 액세스 toohello 솔루션을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-139">*Device identity*: Manage unique device identities and control device access toohello solution.</span></span>
* <span data-ttu-id="26a96-140">*장치 관리*: 장치 메타데이터를 관리하고 장치 재부팅 및 펌웨어 업그레이드 등의 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-140">*Device management*: Manage device metadata and perform operations such as device reboots and firmware upgrades.</span></span>
* <span data-ttu-id="26a96-141">*명령 및 제어*: toocause hello 장치 tootake 있는 동작을 hello 클라우드에서 tooa 장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-141">*Command and control*: toocause hello device tootake an action, send messages tooa device from hello cloud.</span></span>
* <span data-ttu-id="26a96-142">*규칙 및 동작*: tooact hello 솔루션 백 엔드 특정 장치-클라우드 데이터에 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-142">*Rules and actions*: tooact on specific device-to-cloud data, hello solution back end uses rules.</span></span>
* <span data-ttu-id="26a96-143">*예측 분석*: hello 솔루션 백 엔드 특정 작업이 수행 해야 하는 경우 toopredict 장치-클라우드 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-143">*Predictive analytics*: hello solution back end analyzes device-to-cloud data toopredict when specific actions should take place.</span></span> <span data-ttu-id="26a96-144">예를 들어 엔진 유지 관리 기간이 때 비행기 엔진 원격 분석 toodetermine를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-144">For example, analyzing aircraft engine telemetry toodetermine when engine maintenance is due.</span></span>

## <a name="remote-monitoring-preconfigured-solution-overview"></a><span data-ttu-id="26a96-145">미리 구성된 원격 모니터링 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="26a96-145">Remote Monitoring preconfigured solution overview</span></span>

<span data-ttu-id="26a96-146">Toodiscuss hello 다른 솔루션 공유 하는 많은 일반적인 디자인 요소에 설명 하기 때문에이 문서에서 원격 모니터링 미리 구성 된 솔루션을 hello 했습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-146">We have chosen toodiscuss hello remote monitoring preconfigured solution in this article because it illustrates many common design elements that hello other solutions share.</span></span>

<span data-ttu-id="26a96-147">hello 다음 다이어그램에서는 hello hello 원격 모니터링 솔루션의 주요 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-147">hello following diagram illustrates hello key elements of hello remote monitoring solution.</span></span> <span data-ttu-id="26a96-148">hello 다음 섹션에서는 이러한 요소에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="26a96-148">hello following sections provide more information about these elements.</span></span>

![미리 구성된 원격 모니터링 솔루션 아키텍처][img-remote-monitoring-arch]

## <a name="devices"></a><span data-ttu-id="26a96-150">장치</span><span class="sxs-lookup"><span data-stu-id="26a96-150">Devices</span></span>

<span data-ttu-id="26a96-151">Hello 원격 모니터링 미리 구성 된 솔루션을 배포 하면 4 개의 시뮬레이션 된 장치는 냉각 장치를 시뮬레이션 하는 hello 솔루션에서 사전 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-151">When you deploy hello remote monitoring preconfigured solution, four simulated devices are pre-provisioned in hello solution that simulate a cooling device.</span></span> <span data-ttu-id="26a96-152">이러한 시뮬레이션된 장치에는 원격 분석을 내보내는 기본 제공 온도 및 습도 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-152">These simulated devices have a built-in temperature and humidity model that emits telemetry.</span></span> <span data-ttu-id="26a96-153">이러한 시뮬레이션된 장치에 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-153">These simulated devices are included to:</span></span>

- <span data-ttu-id="26a96-154">Hello 솔루션을 통해 데이터의 hello 종단 간 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-154">Illustrate hello end-to-end flow of data through hello solution.</span></span>
- <span data-ttu-id="26a96-155">원격 분석의 편리한 원본을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-155">Provide a convenient source of telemetry.</span></span>
- <span data-ttu-id="26a96-156">시작 지점으로 hello 솔루션을 사용 하 여 사용자 지정 구현에 대 한 백 엔드 개발자의 경우 대상 메서드 또는 명령에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-156">Provide a target for methods or commands if you are a back-end developer using hello solution as a starting point for a custom implementation.</span></span>

<span data-ttu-id="26a96-157">hello 솔루션에 hello 시뮬레이션 된 장치는 클라우드-장치 통신 다음 toohello를 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-157">hello simulated devices in hello solution can respond toohello following cloud-to-device communications:</span></span>

- <span data-ttu-id="26a96-158">*메서드 ([메서드를 직접][lnk-direct-methods])*: 여기서 연결된 된 장치는 예상된 toorespond 즉시 양방향 통신 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-158">*Methods ([direct methods][lnk-direct-methods])*: A two-way communication method where a connected device is expected toorespond immediately.</span></span>
- <span data-ttu-id="26a96-159">*명령 (클라우드-장치 메시지)*: 장치에서 지 속성 큐 hello 명령을 검색 하는 단방향 통신 메서드.</span><span class="sxs-lookup"><span data-stu-id="26a96-159">*Commands (cloud-to-device messages)*: A one-way communication method where a device retrieves hello command from a durable queue.</span></span>

<span data-ttu-id="26a96-160">서로 다른 방법에 대한 비교는 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26a96-160">For a comparison of these different approaches, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

<span data-ttu-id="26a96-161">장치에서 먼저 hello 미리 구성 된 솔루션의 tooIoT 허브를 연결 된 장치 정보 메시지 toohello 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-161">When a device first connects tooIoT Hub in hello preconfigured solution, it sends a device information message toohello hub.</span></span> <span data-ttu-id="26a96-162">이 메시지에 hello 장치에 응답할 수 hello 메서드를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-162">This message enumerates hello methods hello device can respond to.</span></span> <span data-ttu-id="26a96-163">Hello 원격 미리 구성 된 솔루션 모니터링, 시뮬레이션 된 장치는 이러한 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-163">In hello remote monitoring preconfigured solution, simulated devices support these methods:</span></span>

* <span data-ttu-id="26a96-164">*펌웨어 업데이트 시작*:이 메서드는 hello 장치 tooperform 펌웨어 업데이트에는 비동기 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-164">*Initiate Firmware Update*: this method initiates an asynchronous task on hello device tooperform a firmware update.</span></span> <span data-ttu-id="26a96-165">hello 비동기 작업 보고 속성 toodeliver 상태 업데이트 toohello 솔루션 대시보드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-165">hello asynchronous task uses reported properties toodeliver status updates toohello solution dashboard.</span></span>
* <span data-ttu-id="26a96-166">*다시 부팅*:이 메서드를 사용 하면 장치 tooreboot hello 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-166">*Reboot*: this method causes hello simulated device tooreboot.</span></span>
* <span data-ttu-id="26a96-167">*FactoryReset*:이 메서드는 hello 시뮬레이션 된 장치에서 공장 재설정을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-167">*FactoryReset*: this method triggers a factory reset on hello simulated device.</span></span>

<span data-ttu-id="26a96-168">장치에서 먼저 hello 미리 구성 된 솔루션의 tooIoT 허브를 연결 된 장치 정보 메시지 toohello 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-168">When a device first connects tooIoT Hub in hello preconfigured solution, it sends a device information message toohello hub.</span></span> <span data-ttu-id="26a96-169">이 메시지 hello 장치에 응답할 수 hello 명령을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-169">This message enumerates hello commands hello device can respond to.</span></span> <span data-ttu-id="26a96-170">Hello 원격 미리 구성 된 솔루션 모니터링, 시뮬레이션 된 장치는 이러한 명령을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-170">In hello remote monitoring preconfigured solution, simulated devices support these commands:</span></span>

* <span data-ttu-id="26a96-171">*Ping 장치*: hello 장치 승인을 toothis 명령에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-171">*Ping Device*: hello device responds toothis command with an acknowledgement.</span></span> <span data-ttu-id="26a96-172">이 명령은 해당 hello 장치는 여전히 활성 상태이 고 수신 대기를 검사 하는 것에 대 한 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-172">This command is useful for checking that hello device is still active and listening.</span></span>
* <span data-ttu-id="26a96-173">*원격 분석을 시작*: hello 장치 toostart 원격 분석을 전송 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-173">*Start Telemetry*: Instructs hello device toostart sending telemetry.</span></span>
* <span data-ttu-id="26a96-174">*원격 분석을 중지*: hello 장치 toostop 원격 분석을 전송 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-174">*Stop Telemetry*: Instructs hello device toostop sending telemetry.</span></span>
* <span data-ttu-id="26a96-175">*변경 집합 지점 온도*: 컨트롤 hello 시뮬레이션된 온도 값 hello 장치 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-175">*Change Set Point Temperature*: Controls hello simulated temperature telemetry values hello device sends.</span></span> <span data-ttu-id="26a96-176">이 명령은 백 엔드 논리를 테스트하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-176">This command is useful for testing back-end logic.</span></span>
* <span data-ttu-id="26a96-177">*진단 원격 분석*: hello 장치 원격 분석으로 hello 외부 온도 보내야 하는 경우를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-177">*Diagnostic Telemetry*: Controls if hello device should send hello external temperature as telemetry.</span></span>
* <span data-ttu-id="26a96-178">*장치 상태 변경*: 장치 보고서 hello 하 hello 장치 상태 메타 데이터 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-178">*Change Device State*: Sets hello device state metadata property that hello device reports.</span></span> <span data-ttu-id="26a96-179">이 명령은 백 엔드 논리를 테스트하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-179">This command is useful for testing back-end logic.</span></span>

<span data-ttu-id="26a96-180">Hello를 생성 하는 시뮬레이션 된 장치 toohello 솔루션을 더 추가할 수 있습니다는 동일한 원격 분석 및 응답 toohello 동일한 메서드 및 명령.</span><span class="sxs-lookup"><span data-stu-id="26a96-180">You can add more simulated devices toohello solution that emit hello same telemetry and respond toohello same methods and commands.</span></span>

<span data-ttu-id="26a96-181">또한 tooresponding toocommands 및 메서드 hello 솔루션에서는 [장치 트윈스][lnk-device-twin]합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-181">In addition tooresponding toocommands and methods, hello solution uses [device twins][lnk-device-twin].</span></span> <span data-ttu-id="26a96-182">장치는 장치 트윈스 tooreport 속성 값 toohello 솔루션 백 엔드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-182">Devices use device twins tooreport property values toohello solution back end.</span></span> <span data-ttu-id="26a96-183">hello 솔루션 대시보드는 장치에서 장치 트윈스 tooset 원하는 toonew 속성 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-183">hello solution dashboard uses device twins tooset toonew desired property values on devices.</span></span> <span data-ttu-id="26a96-184">예를 들어 hello 펌웨어 업데이트 프로세스를 시뮬레이션 하는 hello 장치 보고서 중 hello의 hello 상태 업데이트 보고 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-184">For example, during hello firmware update process hello simulated device reports hello status of hello update using reported properties.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="26a96-185">IoT 허브</span><span class="sxs-lookup"><span data-stu-id="26a96-185">IoT Hub</span></span>

<span data-ttu-id="26a96-186">이 미리 구성 된 솔루션에서는 hello IoT Hub 인스턴스에 해당 toohello *클라우드 게이트웨이* 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-186">In this preconfigured solution, hello IoT Hub instance corresponds toohello *Cloud Gateway* in a typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

<span data-ttu-id="26a96-187">IoT hub는 단일 끝점에서 hello 장치에서 원격 분석을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-187">An IoT hub receives telemetry from hello devices at a single endpoint.</span></span> <span data-ttu-id="26a96-188">IoT hub에 장치 관련 끝점 각 장치 tooit 전송 하는 hello 명령을 검색할 수 있는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-188">An IoT hub also maintains device-specific endpoints where each device can retrieve hello commands that are sent tooit.</span></span>

<span data-ttu-id="26a96-189">hello IoT 허브를 사용 하면 수신 hello 원격 분석 끝점 읽을 hello 서비스 측 원격 분석을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-189">hello IoT hub makes hello received telemetry available through hello service-side telemetry read endpoint.</span></span>

<span data-ttu-id="26a96-190">IoT Hub의 hello 장치 관리 기능이 있습니다 toomanage hello 솔루션 포털 및 일정 작업에서 작업을 수행 하 여 장치 속성을 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="26a96-190">hello device management capability of IoT Hub enables you toomanage your device properties from hello solution portal and schedule jobs that perform operations such as:</span></span>

- <span data-ttu-id="26a96-191">장치 재부팅</span><span class="sxs-lookup"><span data-stu-id="26a96-191">Rebooting devices</span></span>
- <span data-ttu-id="26a96-192">장치 상태 변경</span><span class="sxs-lookup"><span data-stu-id="26a96-192">Changing device states</span></span>
- <span data-ttu-id="26a96-193">펌웨어 업데이트</span><span class="sxs-lookup"><span data-stu-id="26a96-193">Firmware updates</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="26a96-194">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26a96-194">Azure Stream Analytics</span></span>

<span data-ttu-id="26a96-195">hello 미리 구성 된 솔루션 사용 하 여 세 개의 [Azure 스트림 분석] [ lnk-asa] (ASA) 작업 toofilter hello 원격 분석 스트림 hello 장치에서:</span><span class="sxs-lookup"><span data-stu-id="26a96-195">hello preconfigured solution uses three [Azure Stream Analytics][lnk-asa] (ASA) jobs toofilter hello telemetry stream from hello devices:</span></span>

* <span data-ttu-id="26a96-196">*DeviceInfo 작업* -장치 등록 별 메시지 toohello 솔루션 장치 레지스트리 경로 조정 하는 출력 데이터 tooan 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-196">*DeviceInfo job* - outputs data tooan Event hub that routes device registration-specific messages toohello solution device registry.</span></span> <span data-ttu-id="26a96-197">이 장치 레지스트리는 Azure Cosmos DB 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-197">This device registry is an Azure Cosmos DB database.</span></span> <span data-ttu-id="26a96-198">이러한 메시지는 장치를 처음으로 연결할 때 또는 응답 tooa **장치 상태 변경** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-198">These messages are sent when a device first connects or in response tooa **Change device state** command.</span></span>
* <span data-ttu-id="26a96-199">*원격 분석 작업* -콜드 저장소에 대 한 모든 원시 원격 분석 tooAzure blob 저장소를 전송 하 고 hello 솔루션 대시보드를 표시 하는 원격 분석 집계를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-199">*Telemetry job* - sends all raw telemetry tooAzure blob storage for cold storage and calculates telemetry aggregations that display in hello solution dashboard.</span></span>
* <span data-ttu-id="26a96-200">*규칙 작업* -필터 규칙 임계값을 초과 하는 값에 대 한 원격 분석 스트림을 hello 및 출력 hello 데이터 tooan 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-200">*Rules job* - filters hello telemetry stream for values that exceed any rule thresholds and outputs hello data tooan Event hub.</span></span> <span data-ttu-id="26a96-201">규칙을 발생 시키면 hello 솔루션 포털 대시보드 보기 hello 경보 기록 테이블에 새 행으로이 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-201">When a rule fires, hello solution portal dashboard view displays this event as a new row in hello alarm history table.</span></span> <span data-ttu-id="26a96-202">이러한 규칙 hello에 정의 된 hello 설정을 기반으로 작업을 트리거할 수도 **규칙** 및 **동작** hello 솔루션 포털에서 보기.</span><span class="sxs-lookup"><span data-stu-id="26a96-202">These rules can also trigger an action based on hello settings defined on hello **Rules** and **Actions** views in hello solution portal.</span></span>

<span data-ttu-id="26a96-203">이 미리 구성 된 솔루션에서는 hello ASA 작업 toohello의 일부가 **IoT 솔루션 백 엔드** 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-203">In this preconfigured solution, hello ASA jobs form part of toohello **IoT solution back end** in a typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

## <a name="event-processor"></a><span data-ttu-id="26a96-204">이벤트 프로세서</span><span class="sxs-lookup"><span data-stu-id="26a96-204">Event processor</span></span>

<span data-ttu-id="26a96-205">이 미리 구성 된 솔루션에서는 hello 이벤트 프로세서 hello의 일부를 형성 **IoT 솔루션 백 엔드** 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-205">In this preconfigured solution, hello event processor forms part of hello **IoT solution back end** in a typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

<span data-ttu-id="26a96-206">hello **DeviceInfo** 및 **규칙** ASA 작업 보낼 배달에 대 한 해당 출력 tooEvent 허브 tooother 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-206">hello **DeviceInfo** and **Rules** ASA jobs send their output tooEvent hubs for delivery tooother back-end services.</span></span> <span data-ttu-id="26a96-207">hello 솔루션에서 사용 하는 [EventProcessorHost] [ lnk-event-processor] 에서 실행 중인 인스턴스는 [WebJob][lnk-web-job], 이러한 이벤트 허브에서 tooread hello 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-207">hello solution uses an [EventProcessorHost][lnk-event-processor] instance, running in a [WebJob][lnk-web-job], tooread hello messages from these Event hubs.</span></span> <span data-ttu-id="26a96-208">hello **EventProcessorHost** 사용:</span><span class="sxs-lookup"><span data-stu-id="26a96-208">hello **EventProcessorHost** uses:</span></span>
- <span data-ttu-id="26a96-209">hello **DeviceInfo** hello Cosmos DB 데이터베이스의 데이터 tooupdate hello 장치 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-209">hello **DeviceInfo** data tooupdate hello device data in hello Cosmos DB database.</span></span>
- <span data-ttu-id="26a96-210">hello **규칙** 데이터 tooinvoke hello 논리 앱 및 업데이트 hello 경고 hello 솔루션 포털에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-210">hello **Rules** data tooinvoke hello Logic app and update hello alerts display in hello solution portal.</span></span>

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a><span data-ttu-id="26a96-211">장치 ID 레지스트리, 장치 쌍 및 Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="26a96-211">Device identity registry, device twin, and Cosmos DB</span></span>

<span data-ttu-id="26a96-212">모든 IoT Hub는 장치 키를 저장하는 [장치 ID 레지스트리][lnk-identity-registry]를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-212">Every IoT hub includes a [device identity registry][lnk-identity-registry] that stores device keys.</span></span> <span data-ttu-id="26a96-213">IoT Hub이이 정보를 사용 하 여 장치 인증-장치를 등록 해야 하 고 toohello 허브에 연결할 수 있으려면 유효한 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-213">IoT Hub uses this information authenticate devices - a device must be registered and have a valid key before it can connect toohello hub.</span></span>

<span data-ttu-id="26a96-214">A [장치로 이중] [ lnk-device-twin] hello IoT 허브에서 관리 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-214">A [device twin][lnk-device-twin] is a JSON document managed by hello IoT Hub.</span></span> <span data-ttu-id="26a96-215">장치에 대한 장치 쌍은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-215">A device twin for a device contains:</span></span>

- <span data-ttu-id="26a96-216">Hello 장치 toohello 허브에서 보낸 보고 된 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-216">Reported properties sent by hello device toohello hub.</span></span> <span data-ttu-id="26a96-217">Hello 솔루션 포털에서 이러한 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-217">You can view these properties in hello solution portal.</span></span>
- <span data-ttu-id="26a96-218">원하는 속성을 원하는 toosend toohello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-218">Desired properties that you want toosend toohello device.</span></span> <span data-ttu-id="26a96-219">Hello 솔루션 포털에서 이러한 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-219">You can set these properties in hello solution portal.</span></span>
- <span data-ttu-id="26a96-220">Hello 장치에 없는 hello 장치로 이중에만 존재 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-220">Tags that exist only in hello device twin and not on hello device.</span></span> <span data-ttu-id="26a96-221">Hello 솔루션 포털에서 이러한 태그 toofilter 목록 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-221">You can use these tags toofilter lists of devices in hello solution portal.</span></span>

<span data-ttu-id="26a96-222">이 솔루션에서는 장치 트윈스 toomanage 장치 메타 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-222">This solution uses device twins toomanage device metadata.</span></span> <span data-ttu-id="26a96-223">또한 hello 솔루션 각 장치와 hello 명령 기록에서 지 원하는 hello 명령 같은 Cosmos DB 데이터베이스 toostore 추가 솔루션 별 장치 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-223">hello solution also uses a Cosmos DB database toostore additional solution-specific device data such as hello commands supported by each device and hello command history.</span></span>

<span data-ttu-id="26a96-224">또한 hello 솔루션 hello Cosmos DB 데이터베이스의 내용을 hello와 동기화 하는 hello 장치 id 레지스트리에서의 hello 정보를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-224">hello solution must also keep hello information in hello device identity registry synchronized with hello contents of hello Cosmos DB database.</span></span> <span data-ttu-id="26a96-225">hello **EventProcessorHost** 사용 하 여 데이터를 hello **DeviceInfo** stream analytics 작업 toomanage hello 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-225">hello **EventProcessorHost** uses hello data from **DeviceInfo** stream analytics job toomanage hello synchronization.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="26a96-226">솔루션 포털</span><span class="sxs-lookup"><span data-stu-id="26a96-226">Solution portal</span></span>

![솔루션 포털][img-dashboard]

<span data-ttu-id="26a96-228">hello 솔루션 포털은 웹 기반 UI를 hello 미리 구성 된 솔루션의 일부로 배포 된 모든 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-228">hello solution portal is a web-based UI that is deployed toohello cloud as part of hello preconfigured solution.</span></span> <span data-ttu-id="26a96-229">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-229">It enables you to:</span></span>

* <span data-ttu-id="26a96-230">대시보드에서 원격 분석 및 경보 기록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-230">View telemetry and alarm history in a dashboard.</span></span>
* <span data-ttu-id="26a96-231">새 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-231">Provision new devices.</span></span>
* <span data-ttu-id="26a96-232">장치를 관리 및 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-232">Manage and monitor devices.</span></span>
* <span data-ttu-id="26a96-233">Toospecific 장치는 명령을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-233">Send commands toospecific devices.</span></span>
* <span data-ttu-id="26a96-234">특정 장치에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-234">Invoke methods on specific devices.</span></span>
* <span data-ttu-id="26a96-235">규칙 및 작업을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-235">Manage rules and actions.</span></span>
* <span data-ttu-id="26a96-236">하나 이상의 장치에서 작업 toorun를 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-236">Schedule jobs toorun on one or more devices.</span></span>

<span data-ttu-id="26a96-237">이 미리 구성 된 솔루션에서는 hello 솔루션 포털 hello의 일부를 형성 **IoT 솔루션 백 엔드** hello의 일부인 **처리 및 비즈니스 연결** 일반적인 hello에 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]합니다.</span><span class="sxs-lookup"><span data-stu-id="26a96-237">In this preconfigured solution, hello solution portal forms part of hello **IoT solution back end** and part of hello **Processing and business connectivity** in hello typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="26a96-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26a96-238">Next steps</span></span>

<span data-ttu-id="26a96-239">IoT 솔루션 아키텍처에 대한 자세한 내용은 [Microsoft Azure IoT 서비스: 참조 아키텍처][lnk-refarch]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26a96-239">For more information about IoT solution architectures, see [Microsoft Azure IoT services: Reference Architecture][lnk-refarch].</span></span>

<span data-ttu-id="26a96-240">이제 미리 구성 된 솔루션은 hello를 배포 하 여 시작할 수 있습니다 *원격 모니터링* 솔루션 미리 구성 된: [hello 미리 구성 된 솔루션 시작] [ lnk-getstarted-preconfigured].</span><span class="sxs-lookup"><span data-stu-id="26a96-240">Now you know what a preconfigured solution is, you can get started by deploying hello *remote monitoring* preconfigured solution: [Get started with hello preconfigured solutions][lnk-getstarted-preconfigured].</span></span>

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
