---
title: "미리 구성된 Azure IoT 솔루션 | Microsoft Docs"
description: "미리 구성된 Azure IoT 솔루션에 대한 솔루션 및 추가 리소스에 대한 링크와 해당 아키텍처에 대한 설명입니다."
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
ms.openlocfilehash: d66dece63d2ba944c8f3828ba68c6202485d47e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="what-are-the-azure-iot-suite-preconfigured-solutions"></a><span data-ttu-id="e9ca1-103">미리 구성된 Azure IoT Suite 솔루션은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e9ca1-103">What are the Azure IoT Suite preconfigured solutions?</span></span>

<span data-ttu-id="e9ca1-104">미리 구성된 Azure IoT Suite 솔루션은 구독을 사용하여 Azure에 배포할 수 있는 일반적인 IoT 솔루션 패턴의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-104">The Azure IoT Suite preconfigured solutions are implementations of common IoT solution patterns that you can deploy to Azure using your subscription.</span></span> <span data-ttu-id="e9ca1-105">미리 구성된 솔루션을 다음으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-105">You can use the preconfigured solutions:</span></span>

* <span data-ttu-id="e9ca1-106">사용자 고유의 IoT 솔루션에 대한 시작점.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-106">As a starting point for your own IoT solutions.</span></span>
* <span data-ttu-id="e9ca1-107">IoT 솔루션 설계 및 개발에서 일반적인 패턴에 대해 알아보려면</span><span class="sxs-lookup"><span data-stu-id="e9ca1-107">To learn about common patterns in IoT solution design and development.</span></span>

<span data-ttu-id="e9ca1-108">미리 구성된 각 솔루션은 시뮬레이션된 장치를 사용하여 원격 분석을 생성하는 완전한 종단 간 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-108">Each preconfigured solution is a complete, end-to-end implementation that uses simulated devices to generate telemetry.</span></span>

<span data-ttu-id="e9ca1-109">전체 소스 코드를 다운로드하여 특정 IoT 요구 사항에 맞게 솔루션을 사용자 지정 및 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-109">You can download the complete source code to customize and extend the solution to meet your specific IoT requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="e9ca1-110">미리 구성된 솔루션 중 하나를 배포하려면 [Microsoft Azure IoT Suite][lnk-azureiotsuite]를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-110">To deploy one of the preconfigured solutions, visit [Microsoft Azure IoT Suite][lnk-azureiotsuite].</span></span> <span data-ttu-id="e9ca1-111">[미리 구성된 IoT 솔루션 시작][lnk-getstarted-preconfigured] 문서에서는 솔루션 중 하나를 배포 및 실행하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-111">The article [Get started with the IoT preconfigured solutions][lnk-getstarted-preconfigured] provides more information about how to deploy and run one of the solutions.</span></span>

<span data-ttu-id="e9ca1-112">다음 표에서 솔루션을 특정 IoT 기능에 매핑하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-112">The following table shows how the solutions map to specific IoT features:</span></span>

| <span data-ttu-id="e9ca1-113">해결 방법</span><span class="sxs-lookup"><span data-stu-id="e9ca1-113">Solution</span></span> | <span data-ttu-id="e9ca1-114">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="e9ca1-114">Data ingestion</span></span> | <span data-ttu-id="e9ca1-115">장치 ID</span><span class="sxs-lookup"><span data-stu-id="e9ca1-115">Device identity</span></span> | <span data-ttu-id="e9ca1-116">장치 관리</span><span class="sxs-lookup"><span data-stu-id="e9ca1-116">Device management</span></span> | <span data-ttu-id="e9ca1-117">명령 및 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e9ca1-117">Command and control</span></span> | <span data-ttu-id="e9ca1-118">규칙 및 동작</span><span class="sxs-lookup"><span data-stu-id="e9ca1-118">Rules and actions</span></span> | <span data-ttu-id="e9ca1-119">예측 분석</span><span class="sxs-lookup"><span data-stu-id="e9ca1-119">Predictive analytics</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e9ca1-120">[원격 모니터링][lnk-getstarted-preconfigured]</span><span class="sxs-lookup"><span data-stu-id="e9ca1-120">[Remote monitoring][lnk-getstarted-preconfigured]</span></span> |<span data-ttu-id="e9ca1-121">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-121">Yes</span></span> |<span data-ttu-id="e9ca1-122">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-122">Yes</span></span> |<span data-ttu-id="e9ca1-123">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-123">Yes</span></span> |<span data-ttu-id="e9ca1-124">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-124">Yes</span></span> |<span data-ttu-id="e9ca1-125">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-125">Yes</span></span> |- |
| <span data-ttu-id="e9ca1-126">[예측 유지 관리][lnk-predictive-maintenance]</span><span class="sxs-lookup"><span data-stu-id="e9ca1-126">[Predictive maintenance][lnk-predictive-maintenance]</span></span> |<span data-ttu-id="e9ca1-127">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-127">Yes</span></span> |<span data-ttu-id="e9ca1-128">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-128">Yes</span></span> |- |<span data-ttu-id="e9ca1-129">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-129">Yes</span></span> |<span data-ttu-id="e9ca1-130">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-130">Yes</span></span> |<span data-ttu-id="e9ca1-131">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-131">Yes</span></span> |
| <span data-ttu-id="e9ca1-132">[연결된 공장][lnk-getstarted-factory]</span><span class="sxs-lookup"><span data-stu-id="e9ca1-132">[Connected factory][lnk-getstarted-factory]</span></span> |<span data-ttu-id="e9ca1-133">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-133">Yes</span></span> |<span data-ttu-id="e9ca1-134">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-134">Yes</span></span> |<span data-ttu-id="e9ca1-135">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-135">Yes</span></span> |<span data-ttu-id="e9ca1-136">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-136">Yes</span></span> |<span data-ttu-id="e9ca1-137">예</span><span class="sxs-lookup"><span data-stu-id="e9ca1-137">Yes</span></span> |- |

* <span data-ttu-id="e9ca1-138">*데이터 수집*: 클라우드에 대한 대규모 데이터의 수신입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-138">*Data ingestion*: Ingress of data at scale to the cloud.</span></span>
* <span data-ttu-id="e9ca1-139">*장치 ID*: 고유한 장치 ID를 관리하고 솔루션에 대한 장치 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-139">*Device identity*: Manage unique device identities and control device access to the solution.</span></span>
* <span data-ttu-id="e9ca1-140">*장치 관리*: 장치 메타데이터를 관리하고 장치 재부팅 및 펌웨어 업그레이드 등의 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-140">*Device management*: Manage device metadata and perform operations such as device reboots and firmware upgrades.</span></span>
* <span data-ttu-id="e9ca1-141">*명령 및 컨트롤*: 장치가 작업을 수행하도록 하기 위해 클라우드에서 장치에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-141">*Command and control*: To cause the device to take an action, send messages to a device from the cloud.</span></span>
* <span data-ttu-id="e9ca1-142">*규칙 및 동작*: 특정 장치-클라우드 데이터에서 작동하도록 하기 위해 솔루션 백 엔드가 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-142">*Rules and actions*: To act on specific device-to-cloud data, the solution back end uses rules.</span></span>
* <span data-ttu-id="e9ca1-143">*예측 분석*: 솔루션 백 엔드는 장치-클라우드 데이터를 분석하여 특정 작업이 수행될 때를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-143">*Predictive analytics*: The solution back end analyzes device-to-cloud data to predict when specific actions should take place.</span></span> <span data-ttu-id="e9ca1-144">예를 들어 항공기 엔진 원격 분석을 분석하여 엔진 유지 관리가 만료될 때를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-144">For example, analyzing aircraft engine telemetry to determine when engine maintenance is due.</span></span>

## <a name="remote-monitoring-preconfigured-solution-overview"></a><span data-ttu-id="e9ca1-145">미리 구성된 원격 모니터링 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="e9ca1-145">Remote Monitoring preconfigured solution overview</span></span>

<span data-ttu-id="e9ca1-146">이 문서에서는 다른 솔루션에서 공유하는 여러 가지 일반적인 디자인 요소를 보여주는 미리 구성된 원격 모니터링 솔루션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-146">We have chosen to discuss the remote monitoring preconfigured solution in this article because it illustrates many common design elements that the other solutions share.</span></span>

<span data-ttu-id="e9ca1-147">다음 다이어그램에서는 원격 모니터링 솔루션의 핵심 요소를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-147">The following diagram illustrates the key elements of the remote monitoring solution.</span></span> <span data-ttu-id="e9ca1-148">다음 섹션에서는 이러한 요소에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-148">The following sections provide more information about these elements.</span></span>

![미리 구성된 원격 모니터링 솔루션 아키텍처][img-remote-monitoring-arch]

## <a name="devices"></a><span data-ttu-id="e9ca1-150">장치</span><span class="sxs-lookup"><span data-stu-id="e9ca1-150">Devices</span></span>

<span data-ttu-id="e9ca1-151">원격 모니터링 미리 구성 된 솔루션을 배포하는 경우, 4개의 시뮬레이션된 장치가 냉각 장치를 시뮬레이션하는 솔루션에 미리 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-151">When you deploy the remote monitoring preconfigured solution, four simulated devices are pre-provisioned in the solution that simulate a cooling device.</span></span> <span data-ttu-id="e9ca1-152">이러한 시뮬레이션된 장치에는 원격 분석을 내보내는 기본 제공 온도 및 습도 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-152">These simulated devices have a built-in temperature and humidity model that emits telemetry.</span></span> <span data-ttu-id="e9ca1-153">이러한 시뮬레이션된 장치에 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-153">These simulated devices are included to:</span></span>

- <span data-ttu-id="e9ca1-154">솔루션을 통해 데이터의 종단 간 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-154">Illustrate the end-to-end flow of data through the solution.</span></span>
- <span data-ttu-id="e9ca1-155">원격 분석의 편리한 원본을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-155">Provide a convenient source of telemetry.</span></span>
- <span data-ttu-id="e9ca1-156">사용자 지정 구현을 위해 시작 지점으로 솔루션을 사용하는 백 엔드 개발자인 경우 메서드 또는 명령에 대한 대상을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-156">Provide a target for methods or commands if you are a back-end developer using the solution as a starting point for a custom implementation.</span></span>

<span data-ttu-id="e9ca1-157">솔루션에서 시뮬레이션된 장치는 다음과 같은 클라우드-장치 통신에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-157">The simulated devices in the solution can respond to the following cloud-to-device communications:</span></span>

- <span data-ttu-id="e9ca1-158">*메서드([직접 메서드][lnk-direct-methods])*: 연결된 장치가 즉시 응답하도록 예상되는 양방향 통신 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-158">*Methods ([direct methods][lnk-direct-methods])*: A two-way communication method where a connected device is expected to respond immediately.</span></span>
- <span data-ttu-id="e9ca1-159">*명령(클라우드-장치 메시지)*: 장치가 지속형 큐에서 명령을 검색하는 단방향 통신 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-159">*Commands (cloud-to-device messages)*: A one-way communication method where a device retrieves the command from a durable queue.</span></span>

<span data-ttu-id="e9ca1-160">서로 다른 방법에 대한 비교는 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-160">For a comparison of these different approaches, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

<span data-ttu-id="e9ca1-161">장치를 미리 구성된 솔루션에 있는 IoT Hub에 처음으로 연결하는 경우, 허브에 장치 정보 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-161">When a device first connects to IoT Hub in the preconfigured solution, it sends a device information message to the hub.</span></span> <span data-ttu-id="e9ca1-162">이 메시지는 장치가 응답할 수 메서드를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-162">This message enumerates the methods the device can respond to.</span></span> <span data-ttu-id="e9ca1-163">미리 구성된 원격 모니터링 솔루션에서 시뮬레이션된 장치는 이러한 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-163">In the remote monitoring preconfigured solution, simulated devices support these methods:</span></span>

* <span data-ttu-id="e9ca1-164">*펌웨어 업데이트 시작*: 이 메서드는 장치에서 비동기 작업을 시작하여 펌웨어 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-164">*Initiate Firmware Update*: this method initiates an asynchronous task on the device to perform a firmware update.</span></span> <span data-ttu-id="e9ca1-165">비동기 작업은 reported 속성을 사용하여 솔루션 대시보드에 상태 업데이트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-165">The asynchronous task uses reported properties to deliver status updates to the solution dashboard.</span></span>
* <span data-ttu-id="e9ca1-166">*다시 부팅*: 이 메서드를 사용하면 시뮬레이션된 장치가 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-166">*Reboot*: this method causes the simulated device to reboot.</span></span>
* <span data-ttu-id="e9ca1-167">*FactoryReset*: 이 메서드는 시뮬레이션된 장치에서 공장 재설정을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-167">*FactoryReset*: this method triggers a factory reset on the simulated device.</span></span>

<span data-ttu-id="e9ca1-168">장치를 미리 구성된 솔루션에 있는 IoT Hub에 처음으로 연결하는 경우, 허브에 장치 정보 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-168">When a device first connects to IoT Hub in the preconfigured solution, it sends a device information message to the hub.</span></span> <span data-ttu-id="e9ca1-169">이 메시지는 장치가 응답할 수 명령을 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-169">This message enumerates the commands the device can respond to.</span></span> <span data-ttu-id="e9ca1-170">미리 구성된 원격 모니터링 솔루션에서 시뮬레이션된 장치는 이러한 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-170">In the remote monitoring preconfigured solution, simulated devices support these commands:</span></span>

* <span data-ttu-id="e9ca1-171">*Ping 장치*: 장치가 승인을 사용하여 이 명령에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-171">*Ping Device*: The device responds to this command with an acknowledgement.</span></span> <span data-ttu-id="e9ca1-172">이 명령은 장치가 여전히 활성 상태로 수신하고 있는지 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-172">This command is useful for checking that the device is still active and listening.</span></span>
* <span data-ttu-id="e9ca1-173">*원격 분석 시작*: 장치가 원격 분석 보내기를 시작하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-173">*Start Telemetry*: Instructs the device to start sending telemetry.</span></span>
* <span data-ttu-id="e9ca1-174">*원격 분석 중지*: 장치가 원격 분석 보내기를 중지하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-174">*Stop Telemetry*: Instructs the device to stop sending telemetry.</span></span>
* <span data-ttu-id="e9ca1-175">*설정 지점 온도 변경*: 장치가 전송하는 시뮬레이션된 온도 원격 분석 값을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-175">*Change Set Point Temperature*: Controls the simulated temperature telemetry values the device sends.</span></span> <span data-ttu-id="e9ca1-176">이 명령은 백 엔드 논리를 테스트하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-176">This command is useful for testing back-end logic.</span></span>
* <span data-ttu-id="e9ca1-177">*진단 원격 분석*: 장치가 외부 온도를 원격 분석으로 보내야 할지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-177">*Diagnostic Telemetry*: Controls if the device should send the external temperature as telemetry.</span></span>
* <span data-ttu-id="e9ca1-178">*장치 상태 변경*.: 장치가 보고하는 장치 상태 메타데이터 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-178">*Change Device State*: Sets the device state metadata property that the device reports.</span></span> <span data-ttu-id="e9ca1-179">이 명령은 백 엔드 논리를 테스트하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-179">This command is useful for testing back-end logic.</span></span>

<span data-ttu-id="e9ca1-180">동일한 원격 분석을 내보내고 동일한 메서드 및 명령에 응답하는 솔루션에 시뮬레이션된 장치를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-180">You can add more simulated devices to the solution that emit the same telemetry and respond to the same methods and commands.</span></span>

<span data-ttu-id="e9ca1-181">명령 및 메서드에 응답하는 것 외에도 솔루션은 [장치 쌍][lnk-device-twin]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-181">In addition to responding to commands and methods, the solution uses [device twins][lnk-device-twin].</span></span> <span data-ttu-id="e9ca1-182">장치는 장치 쌍을 사용하여 솔루션 백 엔드에 속성 값을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-182">Devices use device twins to report property values to the solution back end.</span></span> <span data-ttu-id="e9ca1-183">솔루션 대시보드는 장치 쌍을 사용하여 장치에 새로운 desired 속성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-183">The solution dashboard uses device twins to set to new desired property values on devices.</span></span> <span data-ttu-id="e9ca1-184">예를 들어 펌웨어 업데이트 프로세스 동안 시뮬레이션된 장치는 reported 속성을 사용하여 업데이트의 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-184">For example, during the firmware update process the simulated device reports the status of the update using reported properties.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="e9ca1-185">IoT 허브</span><span class="sxs-lookup"><span data-stu-id="e9ca1-185">IoT Hub</span></span>

<span data-ttu-id="e9ca1-186">미리 구성된 솔루션에서 IoT Hub 인스턴스는 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]의 *클라우드 게이트웨이*에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-186">In this preconfigured solution, the IoT Hub instance corresponds to the *Cloud Gateway* in a typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

<span data-ttu-id="e9ca1-187">IoT hub는 단일 끝점의 장치에서 원격 분석을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-187">An IoT hub receives telemetry from the devices at a single endpoint.</span></span> <span data-ttu-id="e9ca1-188">또한 IoT hub는 각 장치가 보내 명령을 검색할 수 있는 장치 특정 끝점을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-188">An IoT hub also maintains device-specific endpoints where each device can retrieve the commands that are sent to it.</span></span>

<span data-ttu-id="e9ca1-189">IoT hub를 사용하면 서비스 쪽 원격 분석 읽기 끝점을 통해 수신한 원격 분석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-189">The IoT hub makes the received telemetry available through the service-side telemetry read endpoint.</span></span>

<span data-ttu-id="e9ca1-190">IoT Hub의 장치 관리 기능을 통해 다음과 같은 작업을 수행하는 솔루션 포털 및 일정 작업에서 장치 속성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-190">The device management capability of IoT Hub enables you to manage your device properties from the solution portal and schedule jobs that perform operations such as:</span></span>

- <span data-ttu-id="e9ca1-191">장치 재부팅</span><span class="sxs-lookup"><span data-stu-id="e9ca1-191">Rebooting devices</span></span>
- <span data-ttu-id="e9ca1-192">장치 상태 변경</span><span class="sxs-lookup"><span data-stu-id="e9ca1-192">Changing device states</span></span>
- <span data-ttu-id="e9ca1-193">펌웨어 업데이트</span><span class="sxs-lookup"><span data-stu-id="e9ca1-193">Firmware updates</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="e9ca1-194">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e9ca1-194">Azure Stream Analytics</span></span>

<span data-ttu-id="e9ca1-195">미리 구성된 솔루션은 세 가지 [Azure Stream Analytics][lnk-asa](ASA) 작업을 사용하여 장치에서 원격 분석 스트림을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-195">The preconfigured solution uses three [Azure Stream Analytics][lnk-asa] (ASA) jobs to filter the telemetry stream from the devices:</span></span>

* <span data-ttu-id="e9ca1-196">*DeviceInfo 작업* - 솔루션 장치 레지스트리에 장치 등록 특정 메시지를 라우팅하는 이벤트 허브에 데이터를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-196">*DeviceInfo job* - outputs data to an Event hub that routes device registration-specific messages to the solution device registry.</span></span> <span data-ttu-id="e9ca1-197">이 장치 레지스트리는 Azure Cosmos DB 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-197">This device registry is an Azure Cosmos DB database.</span></span> <span data-ttu-id="e9ca1-198">장치를 처음으로 연결하거나 **장치 상태 변경** 명령에 대한 응답으로 이 메시지가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-198">These messages are sent when a device first connects or in response to a **Change device state** command.</span></span>
* <span data-ttu-id="e9ca1-199">*원격 분석 작업* - 콜드 저장소용 Azure Blob Storage에 모든 원시 원격 분석을 보내고 솔루션 대시보드에 표시하는 원격 분석 집계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-199">*Telemetry job* - sends all raw telemetry to Azure blob storage for cold storage and calculates telemetry aggregations that display in the solution dashboard.</span></span>
* <span data-ttu-id="e9ca1-200">*규칙 작업* - 규칙 임계값을 초과하는 값에 대해 원격 분석 스트림을 필터링하고 이벤트 허브에 대한 데이터를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-200">*Rules job* - filters the telemetry stream for values that exceed any rule thresholds and outputs the data to an Event hub.</span></span> <span data-ttu-id="e9ca1-201">규칙이 실행되면 솔루션 포털 대시보드 뷰는 경보 기록 테이블에 새 행으로 이 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-201">When a rule fires, the solution portal dashboard view displays this event as a new row in the alarm history table.</span></span> <span data-ttu-id="e9ca1-202">이러한 규칙은 솔루션 포털의 **규칙** 및 **작업** 뷰에서 정의된 설정에 따라 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-202">These rules can also trigger an action based on the settings defined on the **Rules** and **Actions** views in the solution portal.</span></span>

<span data-ttu-id="e9ca1-203">미리 구성된 솔루션에서 ASA 작업은 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]에서 **IoT 솔루션 백 엔드**의 일부를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-203">In this preconfigured solution, the ASA jobs form part of to the **IoT solution back end** in a typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

## <a name="event-processor"></a><span data-ttu-id="e9ca1-204">이벤트 프로세서</span><span class="sxs-lookup"><span data-stu-id="e9ca1-204">Event processor</span></span>

<span data-ttu-id="e9ca1-205">미리 구성된 솔루션에서 이벤트 프로세서는 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]에서 **IoT 솔루션 백 엔드**의 일부를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-205">In this preconfigured solution, the event processor forms part of the **IoT solution back end** in a typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

<span data-ttu-id="e9ca1-206">**DeviceInfo** 및 **규칙** ASA 작업은 다른 백 엔드 서비스에 배달하기 위해 Event Hubs에 해당 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-206">The **DeviceInfo** and **Rules** ASA jobs send their output to Event hubs for delivery to other back-end services.</span></span> <span data-ttu-id="e9ca1-207">솔루션은 [WebJob][lnk-web-job]에서 실행 중인 [EventProcessorHost][lnk-event-processor] 인스턴스를 사용하여 이러한 Event hubs에서 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-207">The solution uses an [EventProcessorHost][lnk-event-processor] instance, running in a [WebJob][lnk-web-job], to read the messages from these Event hubs.</span></span> <span data-ttu-id="e9ca1-208">**EventProcessorHost**는 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-208">The **EventProcessorHost** uses:</span></span>
- <span data-ttu-id="e9ca1-209">Cosmos DB 데이터베이스에서 장치 데이터를 업데이트하는 **DeviceInfo** 데이터.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-209">The **DeviceInfo** data to update the device data in the Cosmos DB database.</span></span>
- <span data-ttu-id="e9ca1-210">솔루션 포털에서 논리 앱을 호출하고 경고 표시를 업데이트하는 **규칙** 데이터.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-210">The **Rules** data to invoke the Logic app and update the alerts display in the solution portal.</span></span>

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a><span data-ttu-id="e9ca1-211">장치 ID 레지스트리, 장치 쌍 및 Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e9ca1-211">Device identity registry, device twin, and Cosmos DB</span></span>

<span data-ttu-id="e9ca1-212">모든 IoT Hub는 장치 키를 저장하는 [장치 ID 레지스트리][lnk-identity-registry]를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-212">Every IoT hub includes a [device identity registry][lnk-identity-registry] that stores device keys.</span></span> <span data-ttu-id="e9ca1-213">IoT Hub는 이 정보를 사용하여 장치를 인증하며 허브에 연결하려면 장치를 등록해야 하고 유효한 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-213">IoT Hub uses this information authenticate devices - a device must be registered and have a valid key before it can connect to the hub.</span></span>

<span data-ttu-id="e9ca1-214">[장치 쌍][lnk-device-twin]은 IoT Hub에서 관리하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-214">A [device twin][lnk-device-twin] is a JSON document managed by the IoT Hub.</span></span> <span data-ttu-id="e9ca1-215">장치에 대한 장치 쌍은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-215">A device twin for a device contains:</span></span>

- <span data-ttu-id="e9ca1-216">장치에서 허브에 보낸 Reported 속성.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-216">Reported properties sent by the device to the hub.</span></span> <span data-ttu-id="e9ca1-217">솔루션 포털에서 이러한 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-217">You can view these properties in the solution portal.</span></span>
- <span data-ttu-id="e9ca1-218">장치에 전송하려는 Desired 속성.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-218">Desired properties that you want to send to the device.</span></span> <span data-ttu-id="e9ca1-219">솔루션 포털에서 이러한 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-219">You can set these properties in the solution portal.</span></span>
- <span data-ttu-id="e9ca1-220">장치가 아닌 장치 쌍에만 존재하는 태그.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-220">Tags that exist only in the device twin and not on the device.</span></span> <span data-ttu-id="e9ca1-221">이러한 태그를 사용하여 솔루션 포털에서 장치 목록을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-221">You can use these tags to filter lists of devices in the solution portal.</span></span>

<span data-ttu-id="e9ca1-222">이 솔루션은 장치 쌍을 사용하여 장치 메타데이터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-222">This solution uses device twins to manage device metadata.</span></span> <span data-ttu-id="e9ca1-223">또한 솔루션은 Cosmos DB 데이터베이스를 사용하여 각 장치 및 명령 기록에서 지원하는 명령과 같은 추가 솔루션 특정 장치 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-223">The solution also uses a Cosmos DB database to store additional solution-specific device data such as the commands supported by each device and the command history.</span></span>

<span data-ttu-id="e9ca1-224">또한 솔루션은 Cosmos DB 데이터베이스의 콘텐츠로 동기화된 장치 ID 레지스트리에 정보를 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-224">The solution must also keep the information in the device identity registry synchronized with the contents of the Cosmos DB database.</span></span> <span data-ttu-id="e9ca1-225">**EventProcessorHost**는 **DeviceInfo** Stream Analytics 작업의 데이터를 사용하여 동기화를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-225">The **EventProcessorHost** uses the data from **DeviceInfo** stream analytics job to manage the synchronization.</span></span>

## <a name="solution-portal"></a><span data-ttu-id="e9ca1-226">솔루션 포털</span><span class="sxs-lookup"><span data-stu-id="e9ca1-226">Solution portal</span></span>

![솔루션 포털][img-dashboard]

<span data-ttu-id="e9ca1-228">솔루션 포털은 미리 구성된 솔루션의 일부로 클라우드에 배포된 웹 기반 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-228">The solution portal is a web-based UI that is deployed to the cloud as part of the preconfigured solution.</span></span> <span data-ttu-id="e9ca1-229">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-229">It enables you to:</span></span>

* <span data-ttu-id="e9ca1-230">대시보드에서 원격 분석 및 경보 기록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-230">View telemetry and alarm history in a dashboard.</span></span>
* <span data-ttu-id="e9ca1-231">새 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-231">Provision new devices.</span></span>
* <span data-ttu-id="e9ca1-232">장치를 관리 및 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-232">Manage and monitor devices.</span></span>
* <span data-ttu-id="e9ca1-233">특정 장치에 명령을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-233">Send commands to specific devices.</span></span>
* <span data-ttu-id="e9ca1-234">특정 장치에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-234">Invoke methods on specific devices.</span></span>
* <span data-ttu-id="e9ca1-235">규칙 및 작업을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-235">Manage rules and actions.</span></span>
* <span data-ttu-id="e9ca1-236">하나 이상의 장치에서 실행할 작업을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-236">Schedule jobs to run on one or more devices.</span></span>

<span data-ttu-id="e9ca1-237">미리 구성된 솔루션에서 솔루션 포털은 **IoT 솔루션 백 엔드**의 일부와 일반적인 [IoT 솔루션 아키텍처][lnk-what-is-azure-iot]에서 **프로세스 및 비즈니스 연결**의 일부를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-237">In this preconfigured solution, the solution portal forms part of the **IoT solution back end** and part of the **Processing and business connectivity** in the typical [IoT solution architecture][lnk-what-is-azure-iot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9ca1-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9ca1-238">Next steps</span></span>

<span data-ttu-id="e9ca1-239">IoT 솔루션 아키텍처에 대한 자세한 내용은 [Microsoft Azure IoT 서비스: 참조 아키텍처][lnk-refarch]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-239">For more information about IoT solution architectures, see [Microsoft Azure IoT services: Reference Architecture][lnk-refarch].</span></span>

<span data-ttu-id="e9ca1-240">이제 미리 구성된 솔루션을 알 수 있으므로 미리 구성된 *원격 모니터링* 솔루션: [미리 구성된 솔루션 시작][lnk-getstarted-preconfigured]을 배포하여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9ca1-240">Now you know what a preconfigured solution is, you can get started by deploying the *remote monitoring* preconfigured solution: [Get started with the preconfigured solutions][lnk-getstarted-preconfigured].</span></span>

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
