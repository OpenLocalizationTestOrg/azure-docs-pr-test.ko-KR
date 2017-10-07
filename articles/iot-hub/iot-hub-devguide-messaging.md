---
title: "aaaUnderstand Azure IoT Hub 메시징 | Microsoft Docs"
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="fb2b1-104">IoT Hub를 사용한 장치-클라우드 및 클라우드-장치 메시징</span><span class="sxs-lookup"><span data-stu-id="fb2b1-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="fb2b1-105">IoT Hub에서 장치에서 toocommunicate 메시징 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="fb2b1-106">보내는 [장치-클라우드] [ lnk-d2c] 메시지 장치 tooyour 솔루션에서 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="fb2b1-107">보내는 [클라우드-장치] [ lnk-c2d] hello 솔루션 다시에서 메시지 tooyour 장치를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="fb2b1-108">IoT Hub 메시징 기능의 핵심 속성은 hello 안정성 및 지 속성 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="fb2b1-109">복원 력 toointermittent 연결 hello 장치 쪽에서 이러한 속성을 사용 하 고 tooload hello 클라우드 쪽에서 처리 하는 이벤트의 급증 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="fb2b1-110">IoT Hub는 장치-클라우드 및 클라우드-장치 메시징 모두에 대해 *한 번 이상* 전달 보증을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="fb2b1-111">IoT Hub의 소개 toohello 기능 hello 문서를 참조 하십시오. [Azure 및 사물 인터넷] [ lnk-azure-iot] 및 [hello Azure IoT 허브 서비스의 개요] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="fb2b1-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="fb2b1-112">때 toouse IoT Hub 메시징</span><span class="sxs-lookup"><span data-stu-id="fb2b1-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="fb2b1-113">단방향 알림 tooyour 장치 응용 프로그램에 대 한 장치 앱에서 시간 시계열 원격 분석 및 경고를 보내기 위한 장치-클라우드 메시지와 클라우드-장치 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="fb2b1-114">너무 참조[장치-클라우드 통신 지침] [ lnk-d2c-guidance] 장치-클라우드 메시지, 보고 된 속성 또는 파일을 업로드 하 여 확실 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="fb2b1-115">너무 참조[클라우드-장치 통신 지침] [ lnk-c2d-guidance] 클라우드-장치 메시지, 원하는 속성 또는 메서드를 직접 사용할지 확실 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb2b1-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fb2b1-116">Next steps</span></span>

* <span data-ttu-id="fb2b1-117">IoT Hub [장치-클라우드 메시징][lnk-d2c]에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="fb2b1-118">IoT Hub [클라우드-장치 메시징][lnk-c2d]에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fb2b1-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md