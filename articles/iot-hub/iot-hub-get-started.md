---
title: "Azure IoT Hub - 클라우드에 IoT 장치 연결 시작 | Microsoft Docs"
description: "Azure IoT Hub에 IoT 보드 및 시작 키트를 연결하는 방법을 알아봅니다. 장치는 원격 분석을 IoT Hub로 전송할 수 있고 Iot Hub는 사용자 장치를 모니터링하고 관리할 수 있습니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Azure IoT Hub 자습서"
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 45016e6383761ffe78f13ccef1112ab3d9753498
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="5a89f-105">Azure IoT Hub 시작 자습서</span><span class="sxs-lookup"><span data-stu-id="5a89f-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="5a89f-106">Azure IoT Hub 및 Azure IoT 장치 SDK를 사용하여 IoT(사물 인터넷) 솔루션을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-106">You can use Azure IoT Hub and the Azure IoT device SDKs to build Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="5a89f-107">Azure IoT Hub는 IoT 장치를 안전하게 연결하고, 모니터링하고, 관리하는 클라우드의 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-107">Azure IoT Hub is a fully managed service in the cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="5a89f-108">Azure IoT 장치 SDK를 사용하여 IoT 장치를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-108">Use the Azure IoT Device SDKs to implement your IoT devices.</span></span>
* <span data-ttu-id="5a89f-109">보다 복잡한 IoT 시나리오에서는 IoT 게이트웨이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="5a89f-110">레거시 장치, 대역폭 비용, 보안 및 개인 정보 보호 정책 또는 Edge 데이터 처리 등의 요소를 고려해야 하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-110">For example, where you need to consider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="5a89f-111">이러한 시나리오에서는 Azure IoT Edge를 사용하여 장치를 IoT Hub에 연결하는 게이트웨이를 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-111">In these scenarios, you use Azure IoT Edge to implement a gateway that connects devices to your IoT hub.</span></span>

## <a name="what-the-tutorials-cover"></a><span data-ttu-id="5a89f-112">자습서에 포함된 내용</span><span class="sxs-lookup"><span data-stu-id="5a89f-112">What the tutorials cover</span></span>

<span data-ttu-id="5a89f-113">이러한 자습서는 Azure IoT Hub 및 장치 SDK를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-113">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="5a89f-114">이 자습서에서는 IoT Hub의 기능을 설명하기 위한 일반적인 IoT 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-114">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="5a89f-115">또한 IoT Hub를 다른 Azure 서비스 및 도구와 결합하여 좀 더 강력한 IoT 솔루션을 구축하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-115">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="5a89f-116">이 자습서에서는 시뮬레이트된 IoT 장치 또는 실제 IoT 장치를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-116">In the tutorials, you can choose to use either simulated or real IoT devices.</span></span> <span data-ttu-id="5a89f-117">또한 게이트웨이를 사용하여 장치를 IoT Hub에 연결하는 방법도 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-117">In addition, you can learn how to use a gateway to enable devices to connect to your IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="5a89f-118">장치 설정</span><span class="sxs-lookup"><span data-stu-id="5a89f-118">Set up your device</span></span>

<span data-ttu-id="5a89f-119">IoT 장치 또는 게이트웨이를 Azure IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-119">Connect an IoT device or gateway to Azure IoT Hub.</span></span> <span data-ttu-id="5a89f-120">시작하려면 실제 또는 시뮬레이트된 장치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-120">You can choose a physical or simulated device to get started:</span></span>

| <span data-ttu-id="5a89f-121">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="5a89f-121">IoT device</span></span>                       | <span data-ttu-id="5a89f-122">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="5a89f-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="5a89f-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="5a89f-123">Raspberry Pi</span></span>                     | <span data-ttu-id="5a89f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="5a89f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="5a89f-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="5a89f-125">IoT DevKit</span></span>                       | <span data-ttu-id="5a89f-126">[VSCode의 Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="5a89f-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="5a89f-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="5a89f-127">Intel Edison</span></span>                     | <span data-ttu-id="5a89f-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="5a89f-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="5a89f-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="5a89f-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="5a89f-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="5a89f-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="5a89f-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="5a89f-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="5a89f-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="5a89f-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="5a89f-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="5a89f-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="5a89f-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="5a89f-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="5a89f-135">PC의 시뮬레이션된 장치</span><span class="sxs-lookup"><span data-stu-id="5a89f-135">Simulated device on PC</span></span>           | <span data-ttu-id="5a89f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="5a89f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="5a89f-137">온라인 장치 시뮬레이터</span><span class="sxs-lookup"><span data-stu-id="5a89f-137">Online device simulator</span></span>         | <span data-ttu-id="5a89f-138">[Raspberry Pi(Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="5a89f-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="5a89f-139">또한 IoT Edge 게이트웨이를 사용하여 장치를 IoT Hub에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a89f-139">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub:</span></span>

| <span data-ttu-id="5a89f-140">게이트웨이 장치</span><span class="sxs-lookup"><span data-stu-id="5a89f-140">Gateway device</span></span>               | <span data-ttu-id="5a89f-141">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="5a89f-141">Programming language</span></span> | <span data-ttu-id="5a89f-142">플랫폼</span><span class="sxs-lookup"><span data-stu-id="5a89f-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="5a89f-143">Intel NUC(모델 DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="5a89f-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="5a89f-144">C</span><span class="sxs-lookup"><span data-stu-id="5a89f-144">C</span></span>                    | <span data-ttu-id="5a89f-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="5a89f-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="5a89f-146">시뮬레이트된 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="5a89f-146">Simulated gateway</span></span>            | <span data-ttu-id="5a89f-147">C</span><span class="sxs-lookup"><span data-stu-id="5a89f-147">C</span></span>                    | <span data-ttu-id="5a89f-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="5a89f-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
