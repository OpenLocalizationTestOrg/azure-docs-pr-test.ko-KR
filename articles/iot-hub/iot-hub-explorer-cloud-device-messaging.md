---
title: "iothub 탐색기와 메시징 aaaManage Azure IoT Hub 클라우드 장치 | Microsoft Docs"
description: "Toouse iothub 탐색기 CLI 도구 toomonitor 장치 toocloud (D2C) 메시지 hello 및 Azure IoT Hub에서 클라우드 toodevice (C2D) 메시지를 보낼 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iothub 탐색기, 메시징, 클라우드 장치 iot 허브 클라우드 toodevice 클라우드 toodevice 메시징"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="3a1d5-104">Iothub 탐색기 toosend를 사용 하 고 사용자의 장치 및 IoT Hub 간에 메시지 송수신</span><span class="sxs-lookup"><span data-stu-id="3a1d5-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="3a1d5-106">[iothub-explorer](https://github.com/azure/iothub-explorer)에는 IoT Hub를 더 쉽게 관리할 수 있는 몇 가지 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="3a1d5-107">이 자습서는 방법에 대해 toouse iothub 탐색기 toosend 및 IoT 허브와 장치 간에 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3a1d5-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="3a1d5-108">What you will learn</span></span>

<span data-ttu-id="3a1d5-109">배웁니다 어떻게 toouse iothub 탐색기 toomonitor 장치-클라우드 메시지와 toosend 클라우드-장치 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="3a1d5-110">장치-클라우드 메시지에는 장치를 수집 하 고 다음 tooyour IoT 허브를 보냅니다 센서 데이터가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="3a1d5-111">클라우드-장치 메시지 명령을 IoT hub 보내는 연결 된 tooyour 장치가 LED tooyour 장치 tooblink는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3a1d5-112">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="3a1d5-112">What you will do</span></span>

- <span data-ttu-id="3a1d5-113">Iothub 탐색기 toomonitor 장치-클라우드 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="3a1d5-114">Iothub 탐색기 toosend 클라우드-장치 메시지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3a1d5-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="3a1d5-115">What you need</span></span>

- <span data-ttu-id="3a1d5-116">자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="3a1d5-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="3a1d5-118">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3a1d5-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="3a1d5-119">메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="3a1d5-120">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="3a1d5-120">iothub-explorer.</span></span> <span data-ttu-id="3a1d5-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="3a1d5-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="3a1d5-122">장치-클라우드 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="3a1d5-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="3a1d5-123">toomonitor 전송 된 메시지를 장치 tooyour IoT 허브에서 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="3a1d5-124">콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-124">Open a console window.</span></span>
1. <span data-ttu-id="3a1d5-125">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="3a1d5-126">IoT Hub에서 `<device-id>`과 `<IoTHubConnectionString>`을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="3a1d5-127">확인 hello 이전 자습서 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="3a1d5-128">Toouse 시도할 수 있습니다 또는 `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` 있으면 `HostName`, `SharedAccessKeyName` 및 `SharedAccessKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="3a1d5-129">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="3a1d5-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="3a1d5-130">toosend 메시지가 IoT hub tooyour 장치에서 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="3a1d5-131">콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-131">Open a console window.</span></span>
1. <span data-ttu-id="3a1d5-132">Hello 다음 명령을 실행 하 여 IoT 허브에서 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="3a1d5-133">Hello 다음 명령을 실행 하 여 메시지 tooyour 장치 보내기:</span><span class="sxs-lookup"><span data-stu-id="3a1d5-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="3a1d5-134">hello 명령 하는 연결 된 tooyour 장치 고 hello 메시지 tooyour 장치 전송 hello led가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="3a1d5-135">Hello 메시지를 받을 때 별도 ack 명령 백 tooyour IoT 허브는 hello 장치 toosend 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a1d5-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a1d5-136">Next steps</span></span>

<span data-ttu-id="3a1d5-137">Toomonitor 장치-클라우드 메시지 하 고 IoT 장치와 Azure IoT Hub 간의 클라우드-장치 메시지를 송신 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="3a1d5-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
