---
title: "iothub-explorer로 Azure IoT Hub 클라우드 장치 메시지 관리 | Microsoft Docs"
description: "iothub-explorer CLI 도구를 사용하여 Azure IoT Hub에서 D2C(장치-클라우드) 메시지를 모니터링하고 C2D(클라우드-장치) 메시지를 보내는 방법에 대해 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iothub explorer, 클라우드 장치 메시지, IoT Hub 클라우드-장치 메시지, 클라우드-장치 메시지"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 30151b7bdc544bc36e959cc3528d37897198fc7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="50e6f-104">iothub-explorer를 사용하여 장치와 IoT Hub 간에 메시지 보내기 및 받기</span><span class="sxs-lookup"><span data-stu-id="50e6f-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="50e6f-106">[iothub-explorer](https://github.com/azure/iothub-explorer)에는 IoT Hub를 더 쉽게 관리할 수 있는 몇 가지 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="50e6f-107">이 자습서에서는 iothub-explorer를 사용하여 장치와 IoT Hub 간에 메시지를 보내고 받는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-107">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="50e6f-108">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="50e6f-108">What you will learn</span></span>

<span data-ttu-id="50e6f-109">iothub-explorer를 사용하여 장치-클라우드 메시지를 모니터링하고 클라우드-장치 메시지를 보내는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-109">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="50e6f-110">장치-클라우드 메시지는 장치에서 수집한 다음 IoT Hub로 보내는 센서 데이터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-110">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="50e6f-111">클라우드-장치 메시지는 IoT Hub에서 장치로 보내 사용자 장치에 연결된 LED를 깜박이는 명령일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-111">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="50e6f-112">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="50e6f-112">What you will do</span></span>

- <span data-ttu-id="50e6f-113">iothub-explorer를 사용하여 장치-클라우드 메시지를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-113">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="50e6f-114">iothub-explorer를 사용하여 클라우드-장치 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-114">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="50e6f-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="50e6f-115">What you need</span></span>

- <span data-ttu-id="50e6f-116">다음 요구 사항을 다루는 자습서 [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료:</span><span class="sxs-lookup"><span data-stu-id="50e6f-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="50e6f-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="50e6f-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="50e6f-118">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="50e6f-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="50e6f-119">메시지를 Azure IoT Hub로 보내는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="50e6f-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="50e6f-120">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="50e6f-120">iothub-explorer.</span></span> <span data-ttu-id="50e6f-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="50e6f-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="50e6f-122">장치-클라우드 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="50e6f-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="50e6f-123">장치에서 IoT Hub로 보낸 메시지를 모니터링하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-123">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="50e6f-124">콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-124">Open a console window.</span></span>
1. <span data-ttu-id="50e6f-125">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-125">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="50e6f-126">IoT Hub에서 `<device-id>`과 `<IoTHubConnectionString>`을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="50e6f-127">이전 자습서를 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-127">Make sure you've finished the previous tutorial.</span></span> <span data-ttu-id="50e6f-128">또는 `HostName`, `SharedAccessKeyName` 및 `SharedAccessKey`가 있는 경우 `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"`을(를) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-128">Or you can try to use `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="50e6f-129">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="50e6f-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="50e6f-130">IoT Hub에서 장치로 메시지를 보내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-130">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="50e6f-131">콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-131">Open a console window.</span></span>
1. <span data-ttu-id="50e6f-132">다음 명령을 실행하여 IoT Hub에서 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-132">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="50e6f-133">다음 명령을 실행하여 메시지를 장치로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-133">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="50e6f-134">이 명령은 장치에 연결된 LED를 깜박이고 메시지를 장치로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-134">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="50e6f-135">장치에서 메시지를 받는 즉시 별도의 ack 명령을 IoT Hub로 다시 보내지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-135">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50e6f-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50e6f-136">Next steps</span></span>

<span data-ttu-id="50e6f-137">IoT 장치와 Azure IoT Hub 간에 장치-클라우드 메시지를 모니터링하고 클라우드-장치 메시지를 보내는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="50e6f-137">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
