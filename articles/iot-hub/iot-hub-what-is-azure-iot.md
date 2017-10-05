---
title: "사물 인터넷을 위한 Azure 솔루션(IoT Suite) | Microsoft Docs"
description: "샘플 IoT 솔루션 아키텍처의 개요 및 장치에 연결된 방법, Azure IoT Hub 서비스, Azure IoT 장치 SDK, Azure IoT 서비스 SDK 및 기타 Azure 서비스입니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="fd977-103">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd977-103">Next steps</span></span>

<span data-ttu-id="fd977-104">Azure IoT Hub는 솔루션 백 엔드와 수백 만개의 장치 간에 안정적이고 신뢰할 수 있는 양방향 통신이 가능하도록 해주는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="fd977-105">이것을 사용하면 솔루션 백 엔드에서 다음 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="fd977-106">장치로부터 대규모 원격 분석을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="fd977-107">장치에서 스트림 이벤트 프로세서로 데이터를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="fd977-108">장치로부터 파일 업로드를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="fd977-109">특정 장치에 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="fd977-110">사용자 고유의 솔루션 백 엔드를 구현하기 위해 IoT Hub를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="fd977-111">또한 IoT Hub에는 장치, 보안 자격 증명, IoT Hub에 연결하는 권한을 프로비전하는 데 사용된 장치 ID 레지스트리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="fd977-112">IoT Hub에 대해 자세히 알아보려면 [IoT Hub란?][lnk-iot-hub]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd977-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="fd977-113">Azure IoT Hub를 사용하여 표준 기반 장치 관리를 통해 원격으로 장치를 관리, 구성, 업데이트할 수 있는 방법을 알아보려면 [IoT Hub를 사용한 장치 관리의 개요][lnk-device-management]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd977-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="fd977-114">다양한 장치 하드웨어 플랫폼과 운영 체제에서 클라이언트 응용 프로그램을 구현하기 위해 Azure IoT 장치 SDK를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="fd977-115">장치 SDK에는 IoT Hub에 대한 원격 분석 전송 및 클라우드-장치 메시지 수신을 용이하게 하는 라이브러리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="fd977-116">장치 SDK를 사용하면 몇 가지 네트워크 프로토콜 중에서 선택하여 IoT Hub와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="fd977-117">자세한 내용은 [장치 SDK에 대한 정보][lnk-device-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd977-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="fd977-118">일부 코드를 작성하고 몇 가지 샘플을 실행하기 시작하려면 [IoT Hub 시작][lnk-getstarted] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd977-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="fd977-119">또한 미리 구성된 솔루션의 컬렉션인 [Azure IoT Suite][lnk-iot-suite]에 관심이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="fd977-120">IoT Suite를 사용하면 원격 모니터링, 자산 관리 및 예측 유지 관리와 같은 일반적인 IoT 시나리오를 해결하기 위해 IoT 프로젝트의 크기를 조정하고 빠르게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd977-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
