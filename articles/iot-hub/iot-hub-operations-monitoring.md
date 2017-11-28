---
title: "aaaAzure IoT 허브 작업 모니터링 | Microsoft Docs"
description: "어떻게 toomonitor 모니터링 toouse Azure IoT 허브 작업 hello 실시간으로 IoT 허브에 대 한 작업의 상태입니다."
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
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="a1a27-103">IoT Hub 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="a1a27-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="a1a27-104">IoT Hub 작업 모니터링 toomonitor hello 상태를를 실시간으로 IoT 허브에 대 한 작업의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="a1a27-105">IoT Hub는 몇 가지 작업 범주에 걸쳐 이벤트를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="a1a27-106">하나 이상의 범주 tooan 끝점의 처리를 위해 IoT 허브에서 이벤트를 전송으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="a1a27-107">오류에 대 한 hello 데이터를 모니터링 하거나 데이터 패턴을 기반으로 하는 복잡 한 처리를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="a1a27-108">IoT Hub는 다음 여섯 가지 범주의 이벤트를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="a1a27-109">장치 ID 작업</span><span class="sxs-lookup"><span data-stu-id="a1a27-109">Device identity operations</span></span>
* <span data-ttu-id="a1a27-110">장치 원격 분석</span><span class="sxs-lookup"><span data-stu-id="a1a27-110">Device telemetry</span></span>
* <span data-ttu-id="a1a27-111">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="a1a27-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="a1a27-112">연결</span><span class="sxs-lookup"><span data-stu-id="a1a27-112">Connections</span></span>
* <span data-ttu-id="a1a27-113">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="a1a27-113">File uploads</span></span>
* <span data-ttu-id="a1a27-114">메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="a1a27-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="a1a27-115">어떻게 tooenable 작업 모니터링</span><span class="sxs-lookup"><span data-stu-id="a1a27-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="a1a27-116">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-116">Create an IoT hub.</span></span> <span data-ttu-id="a1a27-117">방법에 지침을 찾을 수 toocreate hello에서 IoT hub [시작] [ lnk-get-started] 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="a1a27-118">IoT hub의 hello 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="a1a27-119">여기에서 **작업 모니터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-119">From there, click **Operations monitoring**.</span></span>

    ![Hello 포털에서 구성을 모니터링 하는 액세스 작업][1]

1. <span data-ttu-id="a1a27-121">모니터링 toomonitor를 선택 하 고 클릭 범주 선택 hello **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="a1a27-122">hello 사용할 수 있는 이벤트에 나열 된 이벤트 허브 호환 hello 끝점에서 읽는 **모니터링 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="a1a27-123">hello IoT Hub 끝점 이라고 `messages/operationsmonitoringevents`합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![IoT hub에서 작업 모니터링 구성][2]

> [!NOTE]
> <span data-ttu-id="a1a27-125">선택 하면 **Verbose** hello에 대 한 모니터링 **연결** 범주로 인해 IoT Hub toogenerate 추가 진단 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="a1a27-126">다른 모든 범주에 대 한 hello **Verbose** 설정 변경 사항을 IoT Hub 정보의 hello 수량 각 오류 메시지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="a1a27-127">이벤트 범주 및 방법을 toouse에</span><span class="sxs-lookup"><span data-stu-id="a1a27-127">Event categories and how toouse them</span></span>

<span data-ttu-id="a1a27-128">각 작업 모니터링 범주는 IoT Hub와의 여러 상호 작용 유형을 추적하고 각 모니터링 범주에는 해당 범주의 이벤트가 어떻게 구성되는지를 정의하는 스키마가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="a1a27-129">장치 ID 작업</span><span class="sxs-lookup"><span data-stu-id="a1a27-129">Device identity operations</span></span>

<span data-ttu-id="a1a27-130">toocreate 시도할 때 발생 하는 오류를 추적 하는 hello 장치 id 작업 범주, 업데이트 또는 IoT 허브의 identity 레지스트리에 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="a1a27-131">이 범주를 추적하는 것은 프로비전 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="a1a27-132">장치 원격 분석</span><span class="sxs-lookup"><span data-stu-id="a1a27-132">Device telemetry</span></span>

<span data-ttu-id="a1a27-133">hello 장치 원격 분석 범주 관련된 toohello 원격 분석 파이프라인은 hello IoT 허브에서 발생 하는 오류를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="a1a27-134">이 범주에는 원격 분석 이벤트를 보내고(예: 제한) 원격 분석 이벤트를 수신할 때(예: 무단된 판독기) 발생하는 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="a1a27-135">이 범주는 hello 장치 자체에서 실행 되는 코드에 의해 발생 한 오류를 catch 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="a1a27-136">클라우드-장치 명령</span><span class="sxs-lookup"><span data-stu-id="a1a27-136">Cloud-to-device commands</span></span>

<span data-ttu-id="a1a27-137">hello 클라우드-장치 명령 범주 관련된 toohello 클라우드-장치 메시지 파이프라인 되며 hello IoT 허브에서 발생 하는 오류를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="a1a27-138">이 범주에는 클라우드-장치 메시지를 보낼 때(예: 권한이 없는 보낸 사람), 클라우드-장치 메시지를 받을 때(예: 전달 수 초과), 그리고 클라우드-장치 메시지 피드백을 받을 때(예: 피드백 만료) 발생하는 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="a1a27-139">이 범주는 hello 클라우드-장치 메시지를 성공적으로 배달할 경우 부적절 하 게 클라우드-장치 메시지를 처리 하는 장치에서 오류를 catch 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="a1a27-140">연결</span><span class="sxs-lookup"><span data-stu-id="a1a27-140">Connections</span></span>

<span data-ttu-id="a1a27-141">hello 연결 범주 장치 연결 또는 IoT hub에서 연결을 끊을 때 발생 하는 오류를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="a1a27-142">이 범주를 추적하는 것은 무단 연결 시도를 식별하고 연결 상태가 좋지 않은 영역에서 장치의 연결이 끊어졌을 때 추적하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="a1a27-143">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="a1a27-143">File uploads</span></span>

<span data-ttu-id="a1a27-144">hello 파일 업로드 범주 hello IoT 허브에서 발생 하는 관련된 toofile 기능으로 업로드 하는 오류를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="a1a27-145">이 범주에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-145">This category includes:</span></span>

* <span data-ttu-id="a1a27-146">예 전에 장치 업로드 완료의 hello 허브를에 알립니다. 인증서 만료: hello SAS URI로 발생 하는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="a1a27-147">Hello 장치가 보고 업로드 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="a1a27-148">IoT Hub 알림 메시지 생성 중 저장소에서 파일을 찾을 수 없는 경우 발생하는 오류.</span><span class="sxs-lookup"><span data-stu-id="a1a27-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="a1a27-149">이 범주는 직접 hello 장치 파일 toostorage를 업로드 하는 동안 발생 하는 오류를 catch 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="a1a27-150">메시지 라우팅</span><span class="sxs-lookup"><span data-stu-id="a1a27-150">Message routing</span></span>

<span data-ttu-id="a1a27-151">hello 메시지 라우팅 범주 메시지 경로 평가 및 끝점 상태 IoT 허브에서 인식 하는 동안 발생 하는 오류를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="a1a27-152">이 범주는 규칙 값이 너무 "undefined" 이면 때 IoT Hub 끝점을로 표시, 배달 및 수신 끝점에서 다른 오류와 같은 이벤트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="a1a27-153">이 범주는 hello "장치 원격 분석" 범주 아래 보고 hello 메시지 (예: 장치 제한 오류), 자체에 대 한 특정 오류를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="a1a27-154">이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="a1a27-154">View events</span></span>

<span data-ttu-id="a1a27-155">Hello를 사용할 수 있습니다 *iothub 탐색기* 도구 tooquickly IoT hub 모니터링 이벤트를 생성 하는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="a1a27-156">tooinstall hello 도구 hello에 hello 지침을 참조 하십시오 [iothub 탐색기] [ lnk-iothub-explorer] GitHub 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="a1a27-157">있는지 hello 확인 **연결** 너무 설정 범주 모니터링**Verbose** hello 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="a1a27-158">명령 프롬프트에서 hello 명령 tooread hello 모니터링 끝점에서에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="a1a27-159">다른 명령 프롬프트에서 다음 명령을 toosimulate hello 장치-클라우드 메시지를 보내는 장치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="a1a27-160">IoT hub tooyour hello 시뮬레이션 된 장치 연결 하는 hello 첫 번째 명령 프롬프트 hello 모니터링 이벤트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="a1a27-161">모니터링 끝점 toohello 연결</span><span class="sxs-lookup"><span data-stu-id="a1a27-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="a1a27-162">IoT hub 끝점을 모니터링 하는 hello 호환 이벤트 허브 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="a1a27-163">이 끝점에서 이벤트 허브 tooread 모니터링 메시지와 함께 작동 하는 메커니즘을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="a1a27-164">hello 다음 예제에서는 만듭니다 처리량이 높은 배포에 적합 하지 않은 기본 판독기입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="a1a27-165">이벤트 허브에서 tooprocess 메시지 하는 방법에 대 한 자세한 내용은 참조 hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="a1a27-166">tooconnect toohello 모니터링 끝점 연결 문자열 및 hello 끝점 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="a1a27-167">단계를 수행 하는 hello toofind hello 포털에서 필요한 값을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="a1a27-168">Hello 포털에서 tooyour IoT 허브 리소스 블레이드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="a1a27-169">선택 **작업 모니터링**, hello 기록 **이벤트 허브와 호환 가능한 이름** 및 **호환 이벤트 허브 끝점** 값:</span><span class="sxs-lookup"><span data-stu-id="a1a27-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![이벤트 허브 호환 끝점 값][img-endpoints]

1. <span data-ttu-id="a1a27-171">**공유 액세스 정책**을 선택하고 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="a1a27-172">Hello 메모 **기본 키** 값:</span><span class="sxs-lookup"><span data-stu-id="a1a27-172">Make a note of hello **Primary key** value:</span></span>

    ![서비스 공유 액세스 정책 기본 키][img-service-key]

<span data-ttu-id="a1a27-174">hello 다음 C# 코드 샘플에서에서 가져온 것 Visual Studio **클래식 Windows 데스크톱** C# 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="a1a27-175">hello 프로젝트에 hello **WindowsAzure.ServiceBus** NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="a1a27-176">Hello를 사용 하는 연결 문자열 hello 연결 문자열 자리 표시자를 바꿉니다 **호환 이벤트 허브 끝점** 및 서비스 **기본 키** hello 다음과 같이 이전에 기록한 값 예:</span><span class="sxs-lookup"><span data-stu-id="a1a27-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="a1a27-177">Hello로 끝점 이름 자리 표시자를 모니터링 하는 hello 대체 **이벤트 허브와 호환 가능한 이름** 앞에서 설명 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a1a27-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="a1a27-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1a27-178">Next steps</span></span>
<span data-ttu-id="a1a27-179">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a1a27-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a1a27-180">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a1a27-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a1a27-181">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a1a27-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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