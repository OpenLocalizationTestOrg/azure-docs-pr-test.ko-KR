---
title: "Azure IoT Hub-IoT 장치 toohello 클라우드 연결 시작 | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect IoT 보드 및 시작 키트 tooAzure IoT 허브입니다. 장치가는 IoT 허브 및 허브 원격 분석 tooIoT 모니터링 하 고 장치를 관리할 수에 보낼 수 있습니다."
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
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="c6034-105">Azure IoT Hub 시작 자습서</span><span class="sxs-lookup"><span data-stu-id="c6034-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="c6034-106">Azure IoT Hub 및 hello Azure IoT 장치 Sdk toobuild 인터넷 IoT (사물) 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="c6034-107">Azure IoT Hub는 hello 클라우드에 안전 하 게 연결 하 고, 모니터링 및, IoT 장치를 관리 하는 완전히 관리 되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="c6034-108">Hello Azure IoT 장치 Sdk tooimplement IoT 장치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="c6034-109">보다 복잡한 IoT 시나리오에서는 IoT 게이트웨이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="c6034-110">예를 들어 해야 하는 레거시 장치, 대역폭 비용, 보안 및 개인 정보 보호 정책 또는 가장자리 데이터 처리와 같은 tooconsider 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="c6034-111">이러한 시나리오, Azure IoT 가장자리 tooimplement 장치 tooyour IoT 허브를 연결 하는 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="c6034-112">Hello 자습서에서 다루지 내용</span><span class="sxs-lookup"><span data-stu-id="c6034-112">What hello tutorials cover</span></span>

<span data-ttu-id="c6034-113">이 자습서는 tooAzure IoT Hub 및 hello 장치 Sdk 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="c6034-114">hello 자습서 IoT 허브의 일반적인 IoT 시나리오 toodemonstrate hello 기능을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="c6034-115">hello 자습서도 방법을 toocombine IoT Hub 다른 azure 서비스와 설명 toobuild 더 tools 강력한 IoT 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="c6034-116">Hello 자습서에서 toouse 시뮬레이션 또는 실제 IoT 장치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="c6034-117">또한 알아볼 수 있습니다 어떻게 toouse 게이트웨이 tooenable 장치 tooconnect tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="c6034-118">장치 설정</span><span class="sxs-lookup"><span data-stu-id="c6034-118">Set up your device</span></span>

<span data-ttu-id="c6034-119">IoT 장치 또는 게이트웨이 tooAzure IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="c6034-120">시작 하는 물리적 또는 시뮬레이션 된 장치 tooget을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="c6034-121">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="c6034-121">IoT device</span></span>                       | <span data-ttu-id="c6034-122">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="c6034-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="c6034-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c6034-123">Raspberry Pi</span></span>                     | <span data-ttu-id="c6034-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="c6034-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="c6034-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="c6034-125">IoT DevKit</span></span>                       | <span data-ttu-id="c6034-126">[VSCode의 Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="c6034-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="c6034-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="c6034-127">Intel Edison</span></span>                     | <span data-ttu-id="c6034-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="c6034-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="c6034-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="c6034-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="c6034-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="c6034-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="c6034-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="c6034-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="c6034-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="c6034-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="c6034-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="c6034-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="c6034-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="c6034-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="c6034-135">PC의 시뮬레이션된 장치</span><span class="sxs-lookup"><span data-stu-id="c6034-135">Simulated device on PC</span></span>           | <span data-ttu-id="c6034-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="c6034-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="c6034-137">온라인 장치 시뮬레이터</span><span class="sxs-lookup"><span data-stu-id="c6034-137">Online device simulator</span></span>         | <span data-ttu-id="c6034-138">[Raspberry Pi(Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="c6034-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="c6034-139">또한 IoT 가장자리 게이트웨이 tooenable 장치 tooconnect tooyour IoT hub를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6034-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="c6034-140">게이트웨이 장치</span><span class="sxs-lookup"><span data-stu-id="c6034-140">Gateway device</span></span>               | <span data-ttu-id="c6034-141">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="c6034-141">Programming language</span></span> | <span data-ttu-id="c6034-142">플랫폼</span><span class="sxs-lookup"><span data-stu-id="c6034-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="c6034-143">Intel NUC(모델 DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="c6034-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="c6034-144">C</span><span class="sxs-lookup"><span data-stu-id="c6034-144">C</span></span>                    | <span data-ttu-id="c6034-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="c6034-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="c6034-146">시뮬레이트된 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="c6034-146">Simulated gateway</span></span>            | <span data-ttu-id="c6034-147">C</span><span class="sxs-lookup"><span data-stu-id="c6034-147">C</span></span>                    | <span data-ttu-id="c6034-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="c6034-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

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
