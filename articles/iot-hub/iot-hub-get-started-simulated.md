---
title: "Azure IoT Hub에 시뮬레이션된 장치 연결 시작 | Microsoft Docs"
description: "시뮬레이션된 IoT 장치를 만들고 Azure IoT Hub에 연결하는 방법을 알아봅니다. 장치는 원격 분석을 IoT Hub로 전송할 수 있고 IoT Hub는 사용자 장치를 모니터링하고 관리할 수 있습니다."
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
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="ba446-105">시뮬레이션된 장치로 시작하는 Azure IoT Hub 자습서</span><span class="sxs-lookup"><span data-stu-id="ba446-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="ba446-106">이러한 자습서는 Azure IoT Hub 및 장치 SDK를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="ba446-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="ba446-107">이 자습서에서는 IoT Hub의 기능을 설명하기 위한 일반적인 IoT 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="ba446-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="ba446-108">또한 IoT Hub를 다른 Azure 서비스 및 도구와 결합하여 좀 더 강력한 IoT 솔루션을 구축하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba446-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="ba446-109">다음 표에 나열된 자습서는 시뮬레이션된 IoT 장치를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba446-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="ba446-110">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="ba446-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="ba446-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="ba446-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="ba446-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="ba446-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="ba446-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="ba446-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="ba446-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="ba446-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="ba446-115">또한 IoT Edge 게이트웨이를 사용하여 시뮬레이션된 장치를 IoT Hub에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba446-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="ba446-116">프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="ba446-116">Programming language</span></span> | <span data-ttu-id="ba446-117">플랫폼</span><span class="sxs-lookup"><span data-stu-id="ba446-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="ba446-118">C</span><span class="sxs-lookup"><span data-stu-id="ba446-118">C</span></span>                    | <span data-ttu-id="ba446-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="ba446-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="ba446-120">C</span><span class="sxs-lookup"><span data-stu-id="ba446-120">C</span></span>                    | <span data-ttu-id="ba446-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="ba446-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
