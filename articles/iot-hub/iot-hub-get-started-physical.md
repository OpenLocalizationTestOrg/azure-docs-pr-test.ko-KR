---
title: "물리적 장치 tooAzure IoT 허브 연결을 시작 하려면 | Microsoft Docs"
description: "자세한 내용은 방법 tooconnect 물리적 장치와 보드 tooAzure IoT 허브입니다. 장치가는 IoT 허브 및 허브 원격 분석 tooIoT 모니터링 하 고 장치를 관리할 수에 보낼 수 있습니다."
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
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="20d90-105">실제 장치로 시작하는 Azure IoT Hub 자습서</span><span class="sxs-lookup"><span data-stu-id="20d90-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="20d90-106">이 자습서는 tooAzure IoT Hub 및 hello 장치 Sdk 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="20d90-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="20d90-107">hello 자습서 IoT 허브의 일반적인 IoT 시나리오 toodemonstrate hello 기능을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="20d90-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="20d90-108">hello 자습서도 방법을 toocombine IoT Hub 다른 azure 서비스와 설명 toobuild 더 tools 강력한 IoT 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="20d90-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="20d90-109">hello에 나열 된 자습서 안녕하세요 테이블 표시 다음 방법을 toocreate 물리적 IoT 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="20d90-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="20d90-110">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="20d90-110">IoT device</span></span>                       | <span data-ttu-id="20d90-111">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="20d90-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="20d90-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="20d90-112">Raspberry Pi</span></span>                    | <span data-ttu-id="20d90-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="20d90-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="20d90-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="20d90-114">IoT DevKit</span></span>                      | <span data-ttu-id="20d90-115">[VSCode의 Arduino][DevKit]</span><span class="sxs-lookup"><span data-stu-id="20d90-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="20d90-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="20d90-116">Intel Edison</span></span>                    | <span data-ttu-id="20d90-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="20d90-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="20d90-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="20d90-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="20d90-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="20d90-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="20d90-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="20d90-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="20d90-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="20d90-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="20d90-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="20d90-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="20d90-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="20d90-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="20d90-124">또한 IoT 가장자리 게이트웨이 tooenable 장치 tooconnect tooyour IoT hub를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20d90-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="20d90-125">게이트웨이 장치</span><span class="sxs-lookup"><span data-stu-id="20d90-125">Gateway device</span></span>               | <span data-ttu-id="20d90-126">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="20d90-126">Programming language</span></span> | <span data-ttu-id="20d90-127">플랫폼</span><span class="sxs-lookup"><span data-stu-id="20d90-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="20d90-128">Intel NUC(모델 DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="20d90-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="20d90-129">C</span><span class="sxs-lookup"><span data-stu-id="20d90-129">C</span></span>                    | <span data-ttu-id="20d90-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="20d90-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
