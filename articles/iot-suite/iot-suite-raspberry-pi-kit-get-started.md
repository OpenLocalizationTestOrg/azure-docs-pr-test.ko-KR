---
title: "Raspberry Pi를 Azure IoT Suite에 연결 | Microsoft Docs"
description: "Node.js 또는 C를 사용하여 Raspberry Pi 3용 Microsoft Azure IoT 스타터 키트 및 IoT Suite 원격 모니터링 솔루션을 사용하는 방법을 배우도록 도와주는 자습서입니다. 원격 분석을 시뮬레이트하거나, 실제 센서를 사용하거나, 원격 펌웨어 업데이트를 사용하도록 설정하는 자습서를 선택할 수 있습니다."
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
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="3bcd3-104">Microsoft Azure IoT Raspberry Pi 3 스타터 키트를 원격 모니터링 솔루션에 연결</span><span class="sxs-lookup"><span data-stu-id="3bcd3-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="3bcd3-105">이 섹션의 자습서에서는 원격 모니터링 솔루션에 Raspberry Pi 3 장치를 연결하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="3bcd3-106">원하는 프로그래밍 언어 및 Raspberry Pi에서 센서 하드웨어를 함께 사용할 수 있는지 여부에 따라 자습서를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="3bcd3-107">자습서</span><span class="sxs-lookup"><span data-stu-id="3bcd3-107">The tutorials</span></span>

| <span data-ttu-id="3bcd3-108">자습서</span><span class="sxs-lookup"><span data-stu-id="3bcd3-108">Tutorial</span></span> | <span data-ttu-id="3bcd3-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3bcd3-109">Notes</span></span> | <span data-ttu-id="3bcd3-110">언어</span><span class="sxs-lookup"><span data-stu-id="3bcd3-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="3bcd3-111">시뮬레이트된 원격 분석(기본)</span><span class="sxs-lookup"><span data-stu-id="3bcd3-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="3bcd3-112">센서 데이터를 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-112">Simulates sensor data.</span></span> <span data-ttu-id="3bcd3-113">독립 실행형 Raspberry Pi를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="3bcd3-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="3bcd3-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="3bcd3-115">실제 센서(중간)</span><span class="sxs-lookup"><span data-stu-id="3bcd3-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="3bcd3-116">Raspberry Pi에 연결된 BME280 센서의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="3bcd3-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="3bcd3-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="3bcd3-118">펌웨어 업데이트 구현(고급)</span><span class="sxs-lookup"><span data-stu-id="3bcd3-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="3bcd3-119">Raspberry Pi에 연결된 BME280 센서의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="3bcd3-120">Raspberry Pi에서 원격 펌웨어 업데이트를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="3bcd3-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="3bcd3-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3bcd3-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3bcd3-122">Next steps</span></span>

<span data-ttu-id="3bcd3-123">Azure IoT에 대한 추가 샘플 및 설명서를 보려면 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="3bcd3-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md