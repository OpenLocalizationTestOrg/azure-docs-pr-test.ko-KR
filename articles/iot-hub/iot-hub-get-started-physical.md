---
title: "Azure IoT Hub에 실제 장치 연결 시작 | Microsoft Docs"
description: "물리적 장치와 보드를 Azure IoT Hub에 연결하는 방법을 알아봅니다. 장치는 원격 분석을 IoT Hub로 전송할 수 있고 Iot Hub는 사용자 장치를 모니터링하고 관리할 수 있습니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Azure IoT Hub 자습서"
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: f4128b6b049aa876e170c56dcf2e40720644dc3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="888da-105">실제 장치로 시작하는 Azure IoT Hub 자습서</span><span class="sxs-lookup"><span data-stu-id="888da-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="888da-106">이러한 자습서는 Azure IoT Hub 및 장치 SDK를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="888da-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="888da-107">이 자습서에서는 IoT Hub의 기능을 설명하기 위한 일반적인 IoT 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="888da-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="888da-108">또한 IoT Hub를 다른 Azure 서비스 및 도구와 결합하여 좀 더 강력한 IoT 솔루션을 구축하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="888da-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="888da-109">다음 테이블에 나열된 자습서는 실제 IoT 장치를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="888da-109">The tutorials listed in the following table show you how to create physical IoT devices.</span></span>

| <span data-ttu-id="888da-110">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="888da-110">IoT device</span></span>                       | <span data-ttu-id="888da-111">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="888da-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="888da-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="888da-112">Raspberry Pi</span></span>                    | <span data-ttu-id="888da-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="888da-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="888da-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="888da-114">IoT DevKit</span></span>                      | <span data-ttu-id="888da-115">[VSCode의 Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="888da-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="888da-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="888da-116">Intel Edison</span></span>                    | <span data-ttu-id="888da-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="888da-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="888da-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="888da-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="888da-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="888da-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="888da-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="888da-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="888da-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="888da-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="888da-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="888da-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="888da-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="888da-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="888da-124">또한 IoT Edge 게이트웨이를 사용하여 장치를 IoT Hub에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="888da-124">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="888da-125">게이트웨이 장치</span><span class="sxs-lookup"><span data-stu-id="888da-125">Gateway device</span></span>               | <span data-ttu-id="888da-126">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="888da-126">Programming language</span></span> | <span data-ttu-id="888da-127">플랫폼</span><span class="sxs-lookup"><span data-stu-id="888da-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="888da-128">Intel NUC(모델 DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="888da-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="888da-129">C</span><span class="sxs-lookup"><span data-stu-id="888da-129">C</span></span>                    | <span data-ttu-id="888da-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="888da-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
