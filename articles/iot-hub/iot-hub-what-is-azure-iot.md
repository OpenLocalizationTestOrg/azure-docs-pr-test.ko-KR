---
title: "사물 인터넷 (IoT Suite)에 대 한 aaaAzure 솔루션 | Microsoft Docs"
description: "샘플 IoT 솔루션 아키텍처 및 toodevices, 관계의 개요에는 Azure IoT 허브 서비스, Azure IoT 장치 Sdk, Azure IoT 서비스 Sdk 및 기타 Azure 서비스 hello 합니다."
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
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="4185e-103">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4185e-103">Next steps</span></span>

<span data-ttu-id="4185e-104">Azure IoT Hub는 솔루션 백 엔드와 수백 만개의 장치 간에 안정적이고 신뢰할 수 있는 양방향 통신이 가능하도록 해주는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="4185e-105">Hello 솔루션 백 엔드를를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="4185e-106">장치로부터 대규모 원격 분석을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="4185e-107">사용자 장치 tooa 스트림 이벤트 프로세서에서 경로 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="4185e-108">장치로부터 파일 업로드를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="4185e-109">Toospecific 장치 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="4185e-110">IoT Hub tooimplement 종료 하는 사용자 고유의 솔루션을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="4185e-111">또한 IoT 허브는 identity 사용 되는 레지스트리 tooprovision 장치, 해당 보안 자격 증명 및 해당 권한 tooconnect toohello IoT 허브를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="4185e-112">IoT 허브에 대해 자세히 toolearn 참조 [IoT Hub 란?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="4185e-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="4185e-113">toolearn Azure IoT Hub tooremotely 있습니다 관리, 구성 및 장치에 업데이트에 대 한 표준 기반 장치 관리를 사용 하면 참조 [IoT Hub와 장치 관리의 개요][lnk-device-management]합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="4185e-114">tooimplement 클라이언트 장치 하드웨어 플랫폼 및 운영 체제의 다양 한 응용 프로그램, Azure IoT 장치 hello Sdk를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="4185e-115">hello 장치 Sdk 원격 분석 tooan IoT 허브 및 수신 클라우드-장치 메시지를 보낼 수 있는 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="4185e-116">Hello 장치 Sdk를 사용 하면 IoT Hub와 여러 네트워크 프로토콜 toocommunicate에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="4185e-117">toolearn hello을 더 참조 [장치 Sdk에 대 한 정보][lnk-device-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="4185e-118">일부 코드를 작성 하 고 일부 샘플 실행을 시작 하는 tooget 참조 hello [IoT 허브 시작] [ lnk-getstarted] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="4185e-119">또한 미리 구성된 솔루션의 컬렉션인 [Azure IoT Suite][lnk-iot-suite]에 관심이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="4185e-120">IoT Suite tooget 신속 하 게 시작 있으며 특정 IoT 프로젝트 tooaddress IoT 등 일반적인 시나리오-원격 모니터링, 자산 관리 및 예측 유지 관리를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4185e-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
