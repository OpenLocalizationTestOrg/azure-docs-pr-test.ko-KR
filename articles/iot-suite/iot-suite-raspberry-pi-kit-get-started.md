---
title: "aaaConnect 라스베리 Pi tooAzure IoT Suite | Microsoft Docs"
description: "Node.js 또는 C toohelp 하는 방법을 배웁니다 toouse hello 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트 hello IoT Suite 모니터링 솔루션 원격 hello를 사용 하 여 자습서입니다. 원격 분석을 시뮬레이트하거나, 실제 센서를 사용하거나, 원격 펌웨어 업데이트를 사용하도록 설정하는 자습서를 선택할 수 있습니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: a085967ea63e3b0abfe5d10579ba181273a0502c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-toohello-remote-monitoring-solution"></a><span data-ttu-id="aed0d-104">Microsoft Azure IoT 라스베리 Pi 3 시작 키트 toohello 원격 모니터링 솔루션 연결</span><span class="sxs-lookup"><span data-stu-id="aed0d-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit toohello remote monitoring solution</span></span>

<span data-ttu-id="aed0d-105">이 섹션의 자습서에서는 hello 문의할 어떻게 tooconnect는 라스베리 Pi 3 장치 toohello 원격 모니터링 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-105">hello tutorials in this section help you learn how tooconnect a Raspberry Pi 3 device toohello remote monitoring solution.</span></span> <span data-ttu-id="aed0d-106">Hello 자습서 적절 한 tooyour 기본 프로그래밍 언어 및 hello 라스베리 Pi와 함께 사용할 수 있는 hello 센서 하드웨어 toouse 했는지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-106">Choose hello tutorial appropriate tooyour preferred programming language and hello whether you have hello sensor hardware available toouse with your Raspberry Pi.</span></span>

## <a name="hello-tutorials"></a><span data-ttu-id="aed0d-107">hello 자습서</span><span class="sxs-lookup"><span data-stu-id="aed0d-107">hello tutorials</span></span>

| <span data-ttu-id="aed0d-108">자습서</span><span class="sxs-lookup"><span data-stu-id="aed0d-108">Tutorial</span></span> | <span data-ttu-id="aed0d-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="aed0d-109">Notes</span></span> | <span data-ttu-id="aed0d-110">언어</span><span class="sxs-lookup"><span data-stu-id="aed0d-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="aed0d-111">시뮬레이트된 원격 분석(기본)</span><span class="sxs-lookup"><span data-stu-id="aed0d-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="aed0d-112">센서 데이터를 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-112">Simulates sensor data.</span></span> <span data-ttu-id="aed0d-113">독립 실행형 Raspberry Pi를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="aed0d-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="aed0d-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="aed0d-115">실제 센서(중간)</span><span class="sxs-lookup"><span data-stu-id="aed0d-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="aed0d-116">BME280 센서에서 사용 하 여 데이터 tooyour 라스베리 Pi를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-116">Uses data from a BME280 sensor connected tooyour Raspberry Pi.</span></span> | <span data-ttu-id="aed0d-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="aed0d-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="aed0d-118">펌웨어 업데이트 구현(고급)</span><span class="sxs-lookup"><span data-stu-id="aed0d-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="aed0d-119">BME280 센서에서 사용 하 여 데이터 tooyour 라스베리 Pi를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-119">Uses data from a BME280 sensor connected tooyour Raspberry Pi.</span></span> <span data-ttu-id="aed0d-120">Raspberry Pi에서 원격 펌웨어 업데이트를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="aed0d-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="aed0d-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aed0d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aed0d-122">Next steps</span></span>

<span data-ttu-id="aed0d-123">Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="aed0d-123">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md