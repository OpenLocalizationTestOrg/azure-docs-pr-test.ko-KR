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
# <a name="iot-hub-operations-monitoring"></a>IoT Hub 작업 모니터링

IoT Hub 작업 모니터링 toomonitor hello 상태를를 실시간으로 IoT 허브에 대 한 작업의 있습니다. IoT Hub는 몇 가지 작업 범주에 걸쳐 이벤트를 추적합니다. 하나 이상의 범주 tooan 끝점의 처리를 위해 IoT 허브에서 이벤트를 전송으로 선택할 수 있습니다. 오류에 대 한 hello 데이터를 모니터링 하거나 데이터 패턴을 기반으로 하는 복잡 한 처리를 설정할 수 있습니다.

IoT Hub는 다음 여섯 가지 범주의 이벤트를 모니터링합니다.

* 장치 ID 작업
* 장치 원격 분석
* 클라우드-장치 메시지
* 연결
* 파일 업로드
* 메시지 라우팅

## <a name="how-tooenable-operations-monitoring"></a>어떻게 tooenable 작업 모니터링

1. IoT Hub를 만듭니다. 방법에 지침을 찾을 수 toocreate hello에서 IoT hub [시작] [ lnk-get-started] 가이드입니다.

1. IoT hub의 hello 블레이드를 엽니다. 여기에서 **작업 모니터링**을 클릭합니다.

    ![Hello 포털에서 구성을 모니터링 하는 액세스 작업][1]

1. 모니터링 toomonitor를 선택 하 고 클릭 범주 선택 hello **저장**합니다. hello 사용할 수 있는 이벤트에 나열 된 이벤트 허브 호환 hello 끝점에서 읽는 **모니터링 설정**합니다. hello IoT Hub 끝점 이라고 `messages/operationsmonitoringevents`합니다.

    ![IoT hub에서 작업 모니터링 구성][2]

> [!NOTE]
> 선택 하면 **Verbose** hello에 대 한 모니터링 **연결** 범주로 인해 IoT Hub toogenerate 추가 진단 메시지입니다. 다른 모든 범주에 대 한 hello **Verbose** 설정 변경 사항을 IoT Hub 정보의 hello 수량 각 오류 메시지에 포함 됩니다.

## <a name="event-categories-and-how-toouse-them"></a>이벤트 범주 및 방법을 toouse에

각 작업 모니터링 범주는 IoT Hub와의 여러 상호 작용 유형을 추적하고 각 모니터링 범주에는 해당 범주의 이벤트가 어떻게 구성되는지를 정의하는 스키마가 있습니다.

### <a name="device-identity-operations"></a>장치 ID 작업

toocreate 시도할 때 발생 하는 오류를 추적 하는 hello 장치 id 작업 범주, 업데이트 또는 IoT 허브의 identity 레지스트리에 항목을 삭제 합니다. 이 범주를 추적하는 것은 프로비전 시나리오에 유용합니다.

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

### <a name="device-telemetry"></a>장치 원격 분석

hello 장치 원격 분석 범주 관련된 toohello 원격 분석 파이프라인은 hello IoT 허브에서 발생 하는 오류를 추적 합니다. 이 범주에는 원격 분석 이벤트를 보내고(예: 제한) 원격 분석 이벤트를 수신할 때(예: 무단된 판독기) 발생하는 오류가 포함됩니다. 이 범주는 hello 장치 자체에서 실행 되는 코드에 의해 발생 한 오류를 catch 할 수 없습니다.

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

### <a name="cloud-to-device-commands"></a>클라우드-장치 명령

hello 클라우드-장치 명령 범주 관련된 toohello 클라우드-장치 메시지 파이프라인 되며 hello IoT 허브에서 발생 하는 오류를 추적 합니다. 이 범주에는 클라우드-장치 메시지를 보낼 때(예: 권한이 없는 보낸 사람), 클라우드-장치 메시지를 받을 때(예: 전달 수 초과), 그리고 클라우드-장치 메시지 피드백을 받을 때(예: 피드백 만료) 발생하는 오류가 포함됩니다. 이 범주는 hello 클라우드-장치 메시지를 성공적으로 배달할 경우 부적절 하 게 클라우드-장치 메시지를 처리 하는 장치에서 오류를 catch 하지 않습니다.

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

### <a name="connections"></a>연결

hello 연결 범주 장치 연결 또는 IoT hub에서 연결을 끊을 때 발생 하는 오류를 추적 합니다. 이 범주를 추적하는 것은 무단 연결 시도를 식별하고 연결 상태가 좋지 않은 영역에서 장치의 연결이 끊어졌을 때 추적하는 데 유용합니다.

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

### <a name="file-uploads"></a>파일 업로드

hello 파일 업로드 범주 hello IoT 허브에서 발생 하는 관련된 toofile 기능으로 업로드 하는 오류를 추적 합니다. 이 범주에는 다음이 포함됩니다.

* 예 전에 장치 업로드 완료의 hello 허브를에 알립니다. 인증서 만료: hello SAS URI로 발생 하는 오류가 발생 했습니다.
* Hello 장치가 보고 업로드 하지 못했습니다.
* IoT Hub 알림 메시지 생성 중 저장소에서 파일을 찾을 수 없는 경우 발생하는 오류.

이 범주는 직접 hello 장치 파일 toostorage를 업로드 하는 동안 발생 하는 오류를 catch 할 수 없습니다.

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

### <a name="message-routing"></a>메시지 라우팅

hello 메시지 라우팅 범주 메시지 경로 평가 및 끝점 상태 IoT 허브에서 인식 하는 동안 발생 하는 오류를 추적 합니다. 이 범주는 규칙 값이 너무 "undefined" 이면 때 IoT Hub 끝점을로 표시, 배달 및 수신 끝점에서 다른 오류와 같은 이벤트가 포함 됩니다. 이 범주는 hello "장치 원격 분석" 범주 아래 보고 hello 메시지 (예: 장치 제한 오류), 자체에 대 한 특정 오류를 포함 하지 않습니다.

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

## <a name="view-events"></a>이벤트 보기

Hello를 사용할 수 있습니다 *iothub 탐색기* 도구 tooquickly IoT hub 모니터링 이벤트를 생성 하는지 테스트 합니다. tooinstall hello 도구 hello에 hello 지침을 참조 하십시오 [iothub 탐색기] [ lnk-iothub-explorer] GitHub 리포지토리 합니다.

1. 있는지 hello 확인 **연결** 너무 설정 범주 모니터링**Verbose** hello 포털에서 합니다.

1. 명령 프롬프트에서 hello 명령 tooread hello 모니터링 끝점에서에서 다음을 실행 합니다.

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. 다른 명령 프롬프트에서 다음 명령을 toosimulate hello 장치-클라우드 메시지를 보내는 장치를 실행 합니다.

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. IoT hub tooyour hello 시뮬레이션 된 장치 연결 하는 hello 첫 번째 명령 프롬프트 hello 모니터링 이벤트를 보여 줍니다.

## <a name="connect-toohello-monitoring-endpoint"></a>모니터링 끝점 toohello 연결

IoT hub 끝점을 모니터링 하는 hello 호환 이벤트 허브 끝점입니다. 이 끝점에서 이벤트 허브 tooread 모니터링 메시지와 함께 작동 하는 메커니즘을 사용할 수 있습니다. hello 다음 예제에서는 만듭니다 처리량이 높은 배포에 적합 하지 않은 기본 판독기입니다. 이벤트 허브에서 tooprocess 메시지 하는 방법에 대 한 자세한 내용은 참조 hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] 자습서입니다.

tooconnect toohello 모니터링 끝점 연결 문자열 및 hello 끝점 이름이 필요 합니다. 단계를 수행 하는 hello toofind hello 포털에서 필요한 값을 hello 하는 방법을 보여 줍니다.

1. Hello 포털에서 tooyour IoT 허브 리소스 블레이드를 탐색 합니다.

1. 선택 **작업 모니터링**, hello 기록 **이벤트 허브와 호환 가능한 이름** 및 **호환 이벤트 허브 끝점** 값:

    ![이벤트 허브 호환 끝점 값][img-endpoints]

1. **공유 액세스 정책**을 선택하고 **서비스**를 선택합니다. Hello 메모 **기본 키** 값:

    ![서비스 공유 액세스 정책 기본 키][img-service-key]

hello 다음 C# 코드 샘플에서에서 가져온 것 Visual Studio **클래식 Windows 데스크톱** C# 콘솔 응용 프로그램입니다. hello 프로젝트에 hello **WindowsAzure.ServiceBus** NuGet 패키지를 설치 합니다.

* Hello를 사용 하는 연결 문자열 hello 연결 문자열 자리 표시자를 바꿉니다 **호환 이벤트 허브 끝점** 및 서비스 **기본 키** hello 다음과 같이 이전에 기록한 값 예:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Hello로 끝점 이름 자리 표시자를 모니터링 하는 hello 대체 **이벤트 허브와 호환 가능한 이름** 앞에서 설명 된 값입니다.

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

## <a name="next-steps"></a>다음 단계
toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

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