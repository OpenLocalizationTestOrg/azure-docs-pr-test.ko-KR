---
title: "Azure IoT Hub 작업 모니터링 | Microsoft 문서"
description: "IoT Hub 작업 모니터링을 사용하여 실시간으로 IoT Hub에 대한 작업의 상태를 모니터링하는 방법입니다."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="68e9f-103">IoT Hub 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="68e9f-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="68e9f-104">IoT Hub 작업 모니터링을 사용하면 실시간으로 IoT Hub에 대한 작업의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="68e9f-105">IoT Hub는 몇 가지 작업 범주에 걸쳐 이벤트를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="68e9f-106">하나 이상의 범주에서 IoT hub의 끝점으로 처리할 이벤트를 보내도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="68e9f-107">데이터에 오류가 있는지 모니터링하거나 데이터 패턴을 기반으로 좀 더 복잡한 처리를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="68e9f-108">IoT Hub는 다음 여섯 가지 범주의 이벤트를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="68e9f-109">장치 ID 작업</span><span class="sxs-lookup"><span data-stu-id="68e9f-109">Device identity operations</span></span>
* <span data-ttu-id="68e9f-110">장치 원격 분석</span><span class="sxs-lookup"><span data-stu-id="68e9f-110">Device telemetry</span></span>
* <span data-ttu-id="68e9f-111">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="68e9f-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="68e9f-112">연결</span><span class="sxs-lookup"><span data-stu-id="68e9f-112">Connections</span></span>
* <span data-ttu-id="68e9f-113">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="68e9f-113">File uploads</span></span>
* <span data-ttu-id="68e9f-114">메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="68e9f-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="68e9f-115">작업 모니터링을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="68e9f-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="68e9f-116">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-116">Create an IoT hub.</span></span> <span data-ttu-id="68e9f-117">IoT Hub를 만드는 방법에 관한 지침은 [시작][lnk-get-started] 가이드에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="68e9f-118">IoT Hub의 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="68e9f-119">여기에서 **작업 모니터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-119">From there, click **Operations monitoring**.</span></span>

    ![포털의 작업 모니터링 구성 액세스][1]

1. <span data-ttu-id="68e9f-121">모니터링하고자 하는 모니터링 범주를 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="68e9f-122">이벤트는 **모니터링 설정**에 나열된 이벤트 허브 호환 끝점에서 읽어오는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="68e9f-123">IoT Hub 끝점은 `messages/operationsmonitoringevents`라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![IoT hub에서 작업 모니터링 구성][2]

> [!NOTE]
> <span data-ttu-id="68e9f-125">**연결** 범주에 대한 **자세한 정보 표시** 모니터링을 선택하면 IoT Hub가 추가 진단 메시지를 생성하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="68e9f-126">다른 모든 범주의 경우 **자세한 정보 표시** 설정으로 인해 각 오류 메시지에서 IoT Hub가 포함하는 정보량이 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="68e9f-127">이벤트 범주 및 사용 방법</span><span class="sxs-lookup"><span data-stu-id="68e9f-127">Event categories and how to use them</span></span>

<span data-ttu-id="68e9f-128">각 작업 모니터링 범주는 IoT Hub와의 여러 상호 작용 유형을 추적하고 각 모니터링 범주에는 해당 범주의 이벤트가 어떻게 구성되는지를 정의하는 스키마가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="68e9f-129">장치 ID 작업</span><span class="sxs-lookup"><span data-stu-id="68e9f-129">Device identity operations</span></span>

<span data-ttu-id="68e9f-130">장치 ID 작업 범주는 IoT Hub ID 레지스트리의 항목을 만들거나, 업데이트하거나 삭제하려고 할 때 발생하는 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="68e9f-131">이 범주를 추적하는 것은 프로비전 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="68e9f-132">장치 원격 분석</span><span class="sxs-lookup"><span data-stu-id="68e9f-132">Device telemetry</span></span>

<span data-ttu-id="68e9f-133">장치 원격 분석 범주는 IoT Hub에서 발생하고 원격 분석 파이프라인에 관련된 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="68e9f-134">이 범주에는 원격 분석 이벤트를 보내고(예: 제한) 원격 분석 이벤트를 수신할 때(예: 무단된 판독기) 발생하는 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="68e9f-135">이 범주는 장치 자체에서 실행되는 코드에 의해 발생한 오류를 포착할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-135">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="68e9f-136">클라우드-장치 명령</span><span class="sxs-lookup"><span data-stu-id="68e9f-136">Cloud-to-device commands</span></span>

<span data-ttu-id="68e9f-137">클라우드-장치 명령 범주는 IoT Hub에서 발생하고 클라우드-장치 메시지 파이프라인에 관련된 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="68e9f-138">이 범주에는 클라우드-장치 메시지를 보낼 때(예: 권한이 없는 보낸 사람), 클라우드-장치 메시지를 받을 때(예: 전달 수 초과), 그리고 클라우드-장치 메시지 피드백을 받을 때(예: 피드백 만료) 발생하는 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="68e9f-139">이 범주는 클라우드-장치 메시지가 성공적으로 전달된 경우 클라우드-장치 메시지가 부적절하게 처리하는 장치로부터 오류를 포착하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="68e9f-140">연결</span><span class="sxs-lookup"><span data-stu-id="68e9f-140">Connections</span></span>

<span data-ttu-id="68e9f-141">연결 범주는 장치가 IoT Hub에 연결되거나 연결이 해제될 때 발생하는 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="68e9f-142">이 범주를 추적하는 것은 무단 연결 시도를 식별하고 연결 상태가 좋지 않은 영역에서 장치의 연결이 끊어졌을 때 추적하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="68e9f-143">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="68e9f-143">File uploads</span></span>

<span data-ttu-id="68e9f-144">파일 업로드 범주는 IoT Hub에서 발생하고 파일 업로드 기능과 관련된 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="68e9f-145">이 범주에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-145">This category includes:</span></span>

* <span data-ttu-id="68e9f-146">SAS URI에서 발생하는 오류(예: 장치가 허브에 완료된 업로드를 알리기 전에 만료되는 경우).</span><span class="sxs-lookup"><span data-stu-id="68e9f-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="68e9f-147">장치에 의해 보고된 실패한 업로드.</span><span class="sxs-lookup"><span data-stu-id="68e9f-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="68e9f-148">IoT Hub 알림 메시지 생성 중 저장소에서 파일을 찾을 수 없는 경우 발생하는 오류.</span><span class="sxs-lookup"><span data-stu-id="68e9f-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="68e9f-149">이 범주는 장치가 저장소로 파일을 업로드하는 동안 직접 발생하는 오류를 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="68e9f-150">메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="68e9f-150">Message routing</span></span>

<span data-ttu-id="68e9f-151">메시지 라우팅 범주는 IoT Hub에서 감지하는 대로 메시지 경로 평가 및 끝점 상태 중에 발생한 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="68e9f-152">이 범주에는 규칙이 "undefined"로 평가되는 경우, IoT Hub가 끝점을 데드로 표시한 경우 및 다른 오류가 끝점에서 수신되는 경우와 같은 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="68e9f-153">이 범주는 메시지 자체에 대한 특정 오류(예: 장치 제한 오류)를 포함하지 않습니다. 해당 오류는 "장치 원격 분석" 범주 아래에서 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="68e9f-154">이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="68e9f-154">View events</span></span>

<span data-ttu-id="68e9f-155">*iothub-explorer* 도구를 사용하여 IoT Hub가 모니터링 이벤트를 생성하는지 빠르게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="68e9f-156">도구를 설치하려면 [iothub-explorer][lnk-iothub-explorer] GitHub 리포지토리의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68e9f-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="68e9f-157">포털에서 **연결** 모니터링 범주가 **자세한 정보 표시**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="68e9f-158">명령 프롬프트에서 다음 명령을 실행하여 모니터링 끝점에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="68e9f-159">또 다른 명령 프롬프트에서 다음 명령을 실행하여 장치-클라우드 메시지를 보내는 장치를 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="68e9f-160">첫 번째 명령 프롬프트에는 시뮬레이트된 장치가 IoT Hub에 연결될 때 모니터링 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="68e9f-161">모니터링 끝점에 연결</span><span class="sxs-lookup"><span data-stu-id="68e9f-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="68e9f-162">IoT Hub의 모니터링 끝점은 이벤트 허브와 호환되는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="68e9f-163">Event Hubs와 함께 작동하는 모든 메커니즘을 사용하여 이 끝점에서 모니터링 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="68e9f-164">다음 샘플은 처리량이 높은 배포용이 아닌 기본적인 판독기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="68e9f-165">Event Hubs에서 메시지를 처리하는 방법에 대한 자세한 내용은 [Event Hubs 시작][lnk-eventhubs-tutorial] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68e9f-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="68e9f-166">모니터링 끝점에 연결하려면 연결 문자열 및 끝점 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="68e9f-167">다음 단계에서는 포털에서 필요한 값을 찾는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="68e9f-168">포털에서 IoT Hub 리소스 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="68e9f-169">**작업 모니터링**을 선택하고 **이벤트 허브 호환 이름** 및 **이벤트 허브 호환 끝점** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![이벤트 허브 호환 끝점 값][img-endpoints]

1. <span data-ttu-id="68e9f-171">**공유 액세스 정책**을 선택하고 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="68e9f-172">**기본 키** 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-172">Make a note of the **Primary key** value:</span></span>

    ![서비스 공유 액세스 정책 기본 키][img-service-key]

<span data-ttu-id="68e9f-174">다음 C# 코드 샘플은 Visual Studio **Windows 클래식 데스크톱** C# 콘솔 앱에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="68e9f-175">프로젝트에는 **WindowsAzure.ServiceBus** NuGet 패키지가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="68e9f-176">다음 예제와 같이 연결 문자열 자리 표시자를 이전에 적어 둔 **이벤트 허브 호환 끝점** 및 서비스 **기본 키** 값을 사용하는 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="68e9f-177">모니터링 끝점 이름 자리 표시자를 이전에 적어 둔 **이벤트 허브 호환 이름** 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="68e9f-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="68e9f-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68e9f-178">Next steps</span></span>
<span data-ttu-id="68e9f-179">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68e9f-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="68e9f-180">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="68e9f-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="68e9f-181">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="68e9f-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md