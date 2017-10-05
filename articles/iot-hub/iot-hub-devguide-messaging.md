---
title: "Azure IoT Hub 메시징 이해 | Microsoft 문서"
description: "개발자 가이드 - IoT Hub를 사용한 장치-클라우드 및 클라우드-장치 메시징 메시지 형식 및 지원되는 통신 프로토콜에 대한 정보가 포함됩니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="7474f-104">IoT Hub를 사용한 장치-클라우드 및 클라우드-장치 메시징</span><span class="sxs-lookup"><span data-stu-id="7474f-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="7474f-105">IoT Hub 메시징을 사용하여 다음과 같은 방법으로 장치와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="7474f-106">장치에서 솔루션 백 엔드로 [장치-클라우드][lnk-d2c] 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="7474f-107">솔루션 백 엔드에서 장치로 [클라우드-장치][lnk-c2d] 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="7474f-108">IoT Hub 메시징 기능의 핵심 속성은 메시지의 안정성 및 내구성입니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="7474f-109">이 속성을 사용하여 장치 쪽에서 일시적인 연결 및 클라우드 쪽에서 이벤트 처리에 급증한 부하를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="7474f-110">IoT Hub는 장치-클라우드 및 클라우드-장치 메시징 모두에 대해 *한 번 이상* 전달 보증을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="7474f-111">IoT Hub 기능에 대한 소개는 [Azure 및 사물 인터넷][lnk-azure-iot]과 [Azure IoT Hub 서비스 개요][lnk-iot-hub-overview] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7474f-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="7474f-112">IoT Hub 메시징을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="7474f-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="7474f-113">장치 앱에서 시계열 원격 분석 및 경고를 보내려면 장치-클라우드 메시지를 사용하고 장치 앱에 단방향 알림을 보내려면 클라우드-장치 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="7474f-114">장치-클라우드 메시지, reported 속성 또는 파일 업로드 사용에 대해 궁금한 점이 있으면 [장치-클라우드 통신 지침][lnk-d2c-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7474f-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="7474f-115">클라우드-장치 메시지, desired 속성 또는 직접 메서드 사용에 대해 궁금한 점이 있으면 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7474f-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7474f-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7474f-116">Next steps</span></span>

* <span data-ttu-id="7474f-117">IoT Hub [장치-클라우드 메시징][lnk-d2c]에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="7474f-118">IoT Hub [클라우드-장치 메시징][lnk-c2d]에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7474f-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md