---
title: "iothub-explorer를 사용하여 Azure IoT 장치 관리 | Microsoft Docs"
description: "Direct 메서드와 Twin의 desired 속성 관리 옵션을 제공하는 iothub-explorer CLI 도구를 사용하여 Azure IoT Hub 장치를 관리합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IoT 장치 관리, Azure IoT Hub 장치 관리, 장치 관리 IoT, IoT Hub 장치 관리"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="3daf6-104">iothub-explorer를 사용하여 Azure IoT Hub 장치 관리</span><span class="sxs-lookup"><span data-stu-id="3daf6-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="3daf6-106">[iothub-explorer](https://github.com/azure/iothub-explorer)는 호스트 컴퓨터에서 실행하여 IoT Hub 레지스트리의 장치 ID를 관리하는 CLI 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="3daf6-107">다양한 작업을 수행하는 데 사용할 수 있는 관리 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="3daf6-108">관리 옵션</span><span class="sxs-lookup"><span data-stu-id="3daf6-108">Management option</span></span>          | <span data-ttu-id="3daf6-109">작업</span><span class="sxs-lookup"><span data-stu-id="3daf6-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3daf6-110">직접 메서드</span><span class="sxs-lookup"><span data-stu-id="3daf6-110">Direct methods</span></span>             | <span data-ttu-id="3daf6-111">메시지 보내기 시작 또는 중지, 장치 다시 부팅 등의 장치 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="3daf6-112">Twin desired 속성</span><span class="sxs-lookup"><span data-stu-id="3daf6-112">Twin desired properties</span></span>    | <span data-ttu-id="3daf6-113">장치를 특정 상태(예: LED를 녹색으로 설정 또는 원격 분석 전송 간격을 30 분으로 설정)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="3daf6-114">Twin reported 속성</span><span class="sxs-lookup"><span data-stu-id="3daf6-114">Twin reported properties</span></span>   | <span data-ttu-id="3daf6-115">장치의 보고된 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-115">Get the reported state of a device.</span></span> <span data-ttu-id="3daf6-116">예를 들어 장치에서 지금 LED가 깜박이고 있다고 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="3daf6-117">Twin tags</span><span class="sxs-lookup"><span data-stu-id="3daf6-117">Twin tags</span></span>                  | <span data-ttu-id="3daf6-118">클라우드에서 장치 전용 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="3daf6-119">예를 들어 자동 판매기의 배포 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="3daf6-120">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="3daf6-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="3daf6-121">장치에 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-121">Send notifications to a device.</span></span> <span data-ttu-id="3daf6-122">예를 들어 "오늘 비가 올 가능성이 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="3daf6-123">반드시 우산을 챙기세요."</span><span class="sxs-lookup"><span data-stu-id="3daf6-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="3daf6-124">장치 쌍 쿼리</span><span class="sxs-lookup"><span data-stu-id="3daf6-124">Device twin queries</span></span>        | <span data-ttu-id="3daf6-125">모든 장치 쌍을 쿼리하여 사용할 수 있는 장치를 식별하는 등 임의의 조건에 해당하는 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="3daf6-126">이러한 옵션을 사용하는 방법에 대한 차이점과 지침에 대한 자세한 내용은 [장치-클라우드 통신 지침](iot-hub-devguide-d2c-guidance.md) 및 [클라우드-장치 통신 지침](iot-hub-devguide-c2d-guidance.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3daf6-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3daf6-127">장치 쌍은 장치의 상태 정보(메타데이터, 상태 및 조건)를 저장하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="3daf6-128">IoT Hub는 여기에 연결하는 각 장치에 대해 하나의 장치 쌍을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="3daf6-129">장치 쌍에 대한 자세한 내용은 [장치 쌍 시작](iot-hub-node-node-twin-getstarted.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3daf6-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3daf6-130">학습 내용</span><span class="sxs-lookup"><span data-stu-id="3daf6-130">What you learn</span></span>

<span data-ttu-id="3daf6-131">배포 컴퓨터에서 다양한 관리 옵션으로 iothub-explorer를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3daf6-132">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="3daf6-132">What you do</span></span>

<span data-ttu-id="3daf6-133">다양한 관리 옵션으로 iothub-explorer를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3daf6-134">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="3daf6-134">What you need</span></span>

- <span data-ttu-id="3daf6-135">다음 요구 사항을 다루는 자습서 [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료:</span><span class="sxs-lookup"><span data-stu-id="3daf6-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="3daf6-136">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3daf6-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="3daf6-137">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3daf6-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="3daf6-138">메시지를 Azure IoT Hub로 보내는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3daf6-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="3daf6-139">이 자습서를 진행하는 동안 장치가 클라이언트 응용 프로그램을 사용해서 실행되고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="3daf6-140">iothub-explorer, 개발 컴퓨터에 [iothub-explorer를 설치](https://github.com/azure/iothub-explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="3daf6-141">IoT Hub에 연결</span><span class="sxs-lookup"><span data-stu-id="3daf6-141">Connect to your IoT hub</span></span>

<span data-ttu-id="3daf6-142">다음 명령을 실행하여 IoT Hub에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="3daf6-143">직접 메서드로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="3daf6-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="3daf6-144">다음 명령으로 장치 앱에서 `start` 메서드를 호출하여 IoT Hub로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="3daf6-145">다음 명령으로 장치 앱에서 `stop` 메서드를 호출하여 IoT Hub로의 메시지 전송을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="3daf6-146">twin의 desired 속성으로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="3daf6-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="3daf6-147">다음 명령을 실행하여 desired 속성의 간격(interval = 3000)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="3daf6-148">이 속성은 장치에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="3daf6-149">twin의 reported 속성으로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="3daf6-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="3daf6-150">다음 명령을 실행하여 장치의 reported 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="3daf6-151">속성 중 하나인 $metadata.$lastUpdated는 이 장치에서 메시지를 보내거나 받은 마지막 시간을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="3daf6-152">twin의 tags로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="3daf6-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="3daf6-153">다음 명령을 실행하여 장치의 태그와 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="3daf6-154">다음 명령을 실행하여 장치에 역할(role = temperature&humidity) 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="3daf6-155">클라우드-장치 메시지로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="3daf6-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="3daf6-156">다음 명령을 실행하여 장치에 "Hello World" 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="3daf6-157">이 명령을 사용하는 실제 시나리오는 [iothub-explorer를 사용하여 장치와 IoT Hub 간에 메시지 보내기 및 받기](iot-hub-explorer-cloud-device-messaging.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3daf6-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="3daf6-158">장치 쌍 쿼리로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="3daf6-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="3daf6-159">다음 명령을 실행하여 role = 'temperature & humidity' 태그가 있는 장치를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="3daf6-160">다음 명령을 실행하여 role = 'temperature & humidity' 태그가 있는 장치를 제외한 모든 장치를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="3daf6-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3daf6-161">Next steps</span></span>

<span data-ttu-id="3daf6-162">다양한 관리 옵션으로 iothub-explorer를 사용하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3daf6-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
