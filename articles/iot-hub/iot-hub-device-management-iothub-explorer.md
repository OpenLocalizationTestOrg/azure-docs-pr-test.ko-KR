---
title: "aaaAzure iothub 탐색기를 사용 하 여 IoT 장치 관리 | Microsoft Docs"
description: "Hello iothub 탐색기 CLI 도구를 사용 하 여 hello 직접 메서드 및 hello로 이중 원하는 속성 관리 옵션, Azure IoT Hub 장치 관리에 대 한 합니다."
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
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="b8b6e-104">iothub-explorer를 사용하여 Azure IoT Hub 장치 관리</span><span class="sxs-lookup"><span data-stu-id="b8b6e-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="b8b6e-106">[iothub 탐색기](https://github.com/azure/iothub-explorer) IoT 허브 레지스트리에서 호스트 컴퓨터 toomanage 장치 id에서 실행 하는 CLI 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="b8b6e-107">다양 한 작업 tooperform를 사용할 수 있는 관리 옵션을 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="b8b6e-108">관리 옵션</span><span class="sxs-lookup"><span data-stu-id="b8b6e-108">Management option</span></span>          | <span data-ttu-id="b8b6e-109">작업</span><span class="sxs-lookup"><span data-stu-id="b8b6e-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b8b6e-110">직접 메서드</span><span class="sxs-lookup"><span data-stu-id="b8b6e-110">Direct methods</span></span>             | <span data-ttu-id="b8b6e-111">역할 시작 또는 중지 메시지를 보내거나 hello 장치를 다시 부팅 등 장치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="b8b6e-112">Twin desired 속성</span><span class="sxs-lookup"><span data-stu-id="b8b6e-112">Twin desired properties</span></span>    | <span data-ttu-id="b8b6e-113">장치는 LED toogreen를 설정 하는 등의 특정 상태를 전환 하거나 간격 too30 (분)을 보낼 hello 원격 분석 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="b8b6e-114">Twin reported 속성</span><span class="sxs-lookup"><span data-stu-id="b8b6e-114">Twin reported properties</span></span>   | <span data-ttu-id="b8b6e-115">가져오기 hello는 장치의 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-115">Get hello reported state of a device.</span></span> <span data-ttu-id="b8b6e-116">예를 들어 hello 장치는 이제 LED가 깜박입니다. hello를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="b8b6e-117">Twin tags</span><span class="sxs-lookup"><span data-stu-id="b8b6e-117">Twin tags</span></span>                  | <span data-ttu-id="b8b6e-118">Hello 클라우드에서 장치 관련 메타 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="b8b6e-119">예를 들어 hello 배포의 위치는 판매기입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="b8b6e-120">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="b8b6e-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="b8b6e-121">Tooa 장치를 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-121">Send notifications tooa device.</span></span> <span data-ttu-id="b8b6e-122">예를 들어 "오늘은 가능성이 매우 toorain 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="b8b6e-123">반드시 toobring는 포괄적인 합니다. "</span><span class="sxs-lookup"><span data-stu-id="b8b6e-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="b8b6e-124">장치 쌍 쿼리</span><span class="sxs-lookup"><span data-stu-id="b8b6e-124">Device twin queries</span></span>        | <span data-ttu-id="b8b6e-125">사용 하기 위해 사용할 수 있는 hello 장치를 식별 하는 등의 임의 조건을 가진 모든 장치 트윈스 tooretrieve를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="b8b6e-126">Hello 그 차이에 대 한 설명 및 이러한 옵션을 사용 하는 방법과 자세한 [장치-클라우드 통신 지침](iot-hub-devguide-d2c-guidance.md) 및 [클라우드-장치 통신 지침](iot-hub-devguide-c2d-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b8b6e-127">장치 쌍은 장치의 상태 정보(메타데이터, 상태 및 조건)를 저장하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="b8b6e-128">IoT Hub tooit 연결 하는 각 장치에 대 한 장치로 이중을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="b8b6e-129">장치 쌍에 대한 자세한 내용은 [장치 쌍 시작](iot-hub-node-node-twin-getstarted.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b8b6e-130">학습 내용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-130">What you learn</span></span>

<span data-ttu-id="b8b6e-131">배포 컴퓨터에서 다양한 관리 옵션으로 iothub-explorer를 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b8b6e-132">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="b8b6e-132">What you do</span></span>

<span data-ttu-id="b8b6e-133">다양한 관리 옵션으로 iothub-explorer를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b8b6e-134">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="b8b6e-134">What you need</span></span>

- <span data-ttu-id="b8b6e-135">자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="b8b6e-136">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="b8b6e-137">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b8b6e-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b8b6e-138">메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="b8b6e-139">이 자습서에서 hello 클라이언트 응용 프로그램 실행 하는 장치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="b8b6e-140">iothub-explorer, 개발 컴퓨터에 [iothub-explorer를 설치](https://github.com/azure/iothub-explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="b8b6e-141">Tooyour IoT 허브 연결</span><span class="sxs-lookup"><span data-stu-id="b8b6e-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="b8b6e-142">Hello 다음 명령을 실행 하 여 tooyour IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="b8b6e-143">직접 메서드로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="b8b6e-144">Hello 호출 `start` hello 장치 앱 toosend 메시지 tooyour IoT 허브에서 hello 다음 명령을 실행 하 여 메서드:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="b8b6e-145">Hello 호출 `stop` hello 장치 앱 toostop 보내는 메서드 hello 다음 명령을 실행 하 여 tooyour IoT hub 메시지:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="b8b6e-146">twin의 desired 속성으로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="b8b6e-147">원하는 속성 간격 설정 hello 다음 명령을 실행 하 여 3000 =:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="b8b6e-148">이 속성은 장치에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="b8b6e-149">twin의 reported 속성으로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="b8b6e-150">가져오기 hello hello를 실행 하 여 hello 장치의 속성을 보고 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="b8b6e-151">$Metadata hello 속성 중 하나입니다.는 hello 마지막으로이 장치 $lastUpdated 보내거나 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="b8b6e-152">twin의 tags로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="b8b6e-153">Hello 다음 명령을 실행 하 여 hello 태그 및 hello 장치의 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="b8b6e-154">필드 역할 추가 hello 다음 명령을 실행 하 여 온도 및 습도 toohello 장치 =:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="b8b6e-155">클라우드-장치 메시지로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="b8b6e-156">"Hello World" 메시지 toohello 장치를 hello 다음 명령을 실행 하 여 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="b8b6e-157">참조 [toosend iothub 탐색기를 사용 하 고 사용자의 장치 및 IoT Hub 간에 메시지 송수신](iot-hub-explorer-cloud-device-messaging.md) 이 명령을 사용 하 여 실제 시나리오에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="b8b6e-158">장치 쌍 쿼리로 iothub-explorer 사용</span><span class="sxs-lookup"><span data-stu-id="b8b6e-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="b8b6e-159">역할의 태그를 사용 하 여 장치를 쿼리할 '온도 및 습도' hello 다음 명령을 실행 하 여 =:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="b8b6e-160">역할의 태그와 제외 하 고 모든 장치를 쿼리할 '온도 및 습도' hello 다음 명령을 실행 하 여 =:</span><span class="sxs-lookup"><span data-stu-id="b8b6e-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="b8b6e-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8b6e-161">Next steps</span></span>

<span data-ttu-id="b8b6e-162">지금까지 학습 방법을 다양 한 관리 옵션으로 toouse iothub 탐색기.</span><span class="sxs-lookup"><span data-stu-id="b8b6e-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
