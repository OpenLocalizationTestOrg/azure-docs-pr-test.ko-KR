---
title: "Azure IoT 허브 MQTT 지원 aaaUnderstand | Microsoft Docs"
description: "개발자 가이드-장치에서 사용 하 여 IoT Hub 장치 쪽 끝점 tooan 연결 hello MQTT 프로토콜에 대 한 지원. Azure IoT 장치 Sdk hello에 기본 제공 MQTT 지원에 대 한 정보를 포함 합니다."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Hello MQTT 프로토콜을 사용 하 여 IoT 허브와 통신

IoT Hub hello를 사용 하 여 hello IoT Hub 장치 끝점을 장치 toocommunicate 있습니다 [MQTT v3.1.1] [ lnk-mqtt-org] 8883 포트 또는 포트 443에서 WebSocket 프로토콜을 통해 MQTT v3.1.1에서 프로토콜입니다. IoT Hub는 TLS/SSL을 사용 하 여 보안 하는 모든 장치 통신 toobe 필요 (따라서 IoT Hub 지원 하지 않습니다 비보안 연결 1883 포트를 통해).

## <a name="connecting-tooiot-hub"></a>TooIoT 허브 연결

장치 צ ְ ײ hello MQTT 프로토콜 tooconnect tooan IoT hub hello에서 hello 라이브러리를 사용 하 여 [Azure IoT Sdk] [ lnk-device-sdks] 또는 직접 hello MQTT 프로토콜을 사용 하 여 합니다.

## <a name="using-hello-device-sdks"></a>Hello 장치 Sdk를 사용 하 여

[장치 Sdk] [ lnk-device-sdks] 해당 지원 hello MQTT 프로토콜은 Java, Node.js, C, C#, 및 Python에 사용할 수 있습니다. hello 장치 Sdk hello 표준 IoT 허브 연결 문자열 tooestablish 연결 tooan IoT 허브를 사용 합니다. toouse hello MQTT 프로토콜 hello 클라이언트 프로토콜 매개 변수 설정 해야 너무**MQTT**합니다. IoT Hub tooan hello로 hello 장치 Sdk 기본적으로 연결 **CleanSession** 플래그가 설정 너무**0** 사용 하 여 **QoS 1** hello IoT hub와 메시지 교환에 대 한 합니다.

장치가 IoT 허브 연결된 tooan 면 hello 장치 Sdk tooand IoT 허브에서 메시지를 수신 하는 hello 장치 toosend 메시지를 사용할 수 있는 메서드를 제공 합니다.

hello 다음 표에 포함 되어 링크 toocode 샘플 각 지원 되는 언어 및 hello 매개 변수 toouse tooestablish 연결 tooIoT 허브 지정에 대 한 hello MQTT 프로토콜을 사용 합니다.

| 언어 | 프로토콜 매개 변수 |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>AMQP tooMQTT에서 장치 응용 프로그램 마이그레이션

Hello를 사용 하는 경우 [장치 Sdk][lnk-device-sdks], AMQP를 사용 하 여 전환 tooMQTT 필요 앞서 설명한 것 처럼 hello 클라이언트 초기화에 hello 프로토콜 매개 변수를 변경 합니다.

이렇게 할 경우 다음 항목 toocheck hello를 있는지 확인 합니다.

* AMQP은 MQTT hello 연결을 종료 하는 동안 많은 조건에 대 한 오류를 반환 합니다. 결과적으로 예외 처리 논리를 일부 변경해야 합니다.
* MQTT hello를 지원 하지 않습니다 *거부* 를 받을 때 작업 [클라우드-장치 메시지][lnk-messaging]합니다. 백 엔드 앱 tooreceive hello 장치 앱의 응답을 필요한 경우 사용 하 여 고려 [메서드를 직접][lnk-methods]합니다.

## <a name="using-hello-mqtt-protocol-directly"></a>직접 hello MQTT 프로토콜을 사용 하 여
장치 hello 장치 Sdk를 사용할 수 없는 경우 toohello 공용 장치 끝점 hello MQTT 프로토콜을 사용 하 여 8883 포트에서 계속 연결할 수 있습니다. Hello에 **연결** 패킷 hello 장치는 다음 값에는 hello를 사용 해야 합니다.

* Hello에 대 한 **ClientId** 필드의 경우 hello 사용 **deviceId**합니다.
* Hello에 대 한 **Username** 필드의 경우 사용 `{iothubhostname}/{device_id}/api-version=2016-11-14`, 여기서 {iothubhostname} hello IoT 허브의 전체 CName hello 됩니다.

    예를 들어 hello IoT 허브의 이름인 **contoso.azure devices.net** hello 장치 이름이 경우 **MyDevice01**, 전체 hello **Username** 필드에 포함 되어야 `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Hello에 대 한 **암호** 필드의 경우 SAS 토큰을 사용 합니다. SAS 토큰은 hello hello 형식의 hello HTTP 및 AMQP 프로토콜을 모두의 경우와 동일 hello:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`

    방법에 대 한 자세한 내용은 toogenerate SAS 토큰의 hello 장치 섹션을 참조 [IoT 허브를 사용 하 여 보안 토큰][lnk-sas-tokens]합니다.

    을 테스트할 때 사용할 수도 있습니다 hello [장치 탐색기] [ lnk-device-explorer] 도구 tooquickly 복사 하 고 사용자 고유의 코드에 붙여 넣을 수 있는 SAS 토큰을 생성 합니다.

  1. Toohello 이동 **관리** 탭에서 **장치 탐색기**합니다.
  2. **SAS 토큰** (오른쪽 위)을 클릭합니다.
  3. **SASTokenForm**, hello에 장치를 선택 합니다. **DeviceID** 드롭 다운 합니다. **TTL**을 설정합니다.
  4. 클릭 **생성** toocreate 토큰입니다.

     hello 생성 되는 SAS 토큰에이 구조: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`합니다.

     이 토큰 toouse hello로의 일부 hello **암호** MQTT를 사용 하 여 필드 tooconnect은: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`합니다.

MQTT에 대 한 연결 및 분리 패킷, IoT Hub 발급 hello에 대 한 이벤트 **Operations 모니터링** tootroubleshoot 연결 문제 도움이 되는 추가 정보를 사용 하 여 채널입니다.

### <a name="sending-device-to-cloud-messages"></a>장치-클라우드 메시지 보내기

성공적으로 연결한 후 장치를 사용 하 여 메시지 tooIoT 허브 보낼 수 `devices/{device_id}/messages/events/` 또는 `devices/{device_id}/messages/events/{property_bag}` 로 **주제 이름**합니다. hello `{property_bag}` 요소를 사용 하면 추가 속성을 url로 인코딩된 형식으로 hello 장치 toosend 메시지입니다. 예:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> 이 `{property_bag}` 요소 hello HTTP 프로토콜에 쿼리 문자열의 경우와 같은 인코딩을 사용 하 여 hello 합니다.
>
>

hello 장치 앱 ´ ï ´ `devices/{device_id}/messages/events/{property_bag}` hello로 **가 항목 이름을** toodefine *가 메시지를* toobe 원격 분석 메시지로 전달 합니다.

- IoT Hub에서는 QoS 2 메시지를 지원하지 않습니다. 장치 응용 프로그램으로 메시지를 게시 하는 경우 **QoS 2**, IoT Hub hello 네트워크 연결을 닫습니다.
- IoT Hub에서는 보관 메시지가 지속되지 않습니다. 장치 hello로 메시지를 보내는 경우 **RETAIN** 플래그가 설정 too1, IoT Hub 추가 hello **x-opt-유지** 응용 프로그램 속성 toohello 메시지입니다. 이 경우 대신 지속 hello 메시지를 보관, IoT Hub toohello 백 엔드 응용 프로그램 전달 합니다.
- IoT Hub는 장치 당 하나의 활성 MQTT 연결만을 지원합니다. 모든 새 MQTT 연결 hello를 대신 하 여 동일한 장치 ID로 인해 IoT Hub toodrop hello에 대 한 기존 연결 합니다.

자세한 내용은 [메시징 개발자 가이드][lnk-messaging]를 참조하세요.

### <a name="receiving-cloud-to-device-messages"></a>클라우드-장치 메시지 수신

IoT Hub에서 tooreceive 메시지, 장치가 가입 되어 있어야 사용 하 여 `devices/{device_id}/messages/devicebound/#` 로 **항목 필터**합니다. 여러 수준의 와일드 카드 hello  **#**  hello에 항목 필터 tooallow hello 장치 tooreceive 추가 속성 hello 항목 이름에만 사용 됩니다. IoT Hub hello의 hello 사용 하지 못하도록  **#**  또는 **?** 하위 토픽의 필터링을 위한 와일드카드 IoT Hub 범용 게시-구독 메시징 브로커 아니므로 문서화 hello 항목 이름 및 항목 필터를 지원 합니다.

hello 장치는 메시지를 받지 못하게 IoT 허브에서 hello 나타내는 tooits 장치별 끝점에서 성공적으로 구독 될 때까지 `devices/{device_id}/messages/devicebound/#` 항목 필터입니다. 성공한 구독 설정 된 후 hello 장치 tooit hello 구독의 hello 시간 이후에 보낸만으로 클라우드-장치 메시지를 받기 시작 합니다. Hello 장치가 연결 된 **CleanSession** 플래그가 설정 너무**0**, hello 구독 다른 세션 간에 유지 됩니다. 이 경우 다음으로 연결할 때 hello **CleanSession 0** hello 장치에서 보낸 tooit 끊어져 동안 해결 되지 않은 메시지를 수신 합니다. Hello 장치를 사용 하는 경우 **CleanSession** 플래그가 설정 너무**1** 하지만 수신 되지 않으면 모든 메시지가 IoT 허브에서 tooits 장치 끝점을 등록 될 때까지 합니다.

IoT Hub hello로 메시지를 배달 **주제 이름** `devices/{device_id}/messages/devicebound/`, 또는 `devices/{device_id}/messages/devicebound/{property_bag}` 모든 메시지 속성이 있는 경우. `{property_bag}` 에는 메시지 속성의 URL 인코딩된 키/값 쌍이 있습니다. 응용 프로그램 속성 및 사용자 설정 시스템 속성 (같은 **messageId** 또는 **correlationId**) hello propertybag에 포함 됩니다. 시스템 속성 이름은 hello 접두사가  **$** , 응용 프로그램 속성 접두사가 없는 원래 속성 이름 hello를 사용 합니다.

장치 앱 tooa 항목을 구독 하는 경우 **QoS 2**, IoT Hub 부여 hello에 최대 QoS 수준 1 **SUBACK** 패킷 합니다. 그 후 IoT 허브는 QoS 1을 사용 하 여 메시지 toohello 장치를 제공 합니다.

### <a name="retrieving-a-device-twins-properties"></a>장치 쌍 속성 검색

첫째, 장치가 구독 너무`$iothub/twin/res/#`, tooreceive hello 작업 응답 합니다. 그런 다음 빈 메시지 tootopic 보내는 `$iothub/twin/GET/?$rid={request id}`에 지정된 된 값이 있는 **요청 id**. hello 서비스 hello 장치로 이중 데이터 항목에 포함 된 응답 메시지를 보냅니다 `$iothub/twin/res/{status}/?$rid={request id}`, 동일 hello를 사용 하 여  **요청 id** hello 요청으로 합니다.

request id는 [IoT Hub 메시징 개발자 가이드][lnk-messaging]에 따라 메시지 속성 값에 대한 유효한 값이며 status는 정수로 확인됩니다.
hello 응답 본문의 hello 장치로 이중 hello 속성 섹션에 포함:

hello 본문 hello identity 레지스트리 항목의 예를 들어 toohello "속성" 멤버를 제한:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

hello 가능한 상태 코드는.

|가동 상태 | 설명 |
| ----- | ----------- |
| 200 | 성공 |
| 429 | 너무 많은 요청(제한됨), [IoT Hub 제한][lnk-quotas] 참조 |
| 5** | 서버 오류 |

자세한 내용은 [장치 쌍 개발자 가이드][lnk-devguide-twin]를 참조하세요.

### <a name="update-device-twins-reported-properties"></a>장치 쌍의 reported 속성 업데이트

hello 다음 시퀀스에 설명 장치 hello를 업데이트 하는 방식은 hello 장치로 이중 IoT 허브에서의 속성을 보고 합니다.

1. 장치 toohello 먼저 구독 해야 `$iothub/twin/res/#` IoT 허브에서 항목 tooreceive hello 작업 응답 합니다.

1. Hello 장치로 이중 업데이트 toohello 포함 된 메시지를 전송 하는 장치는 `$iothub/twin/PATCH/properties/reported/?$rid={request id}` 항목입니다. 이 메시지는 **요청 ID** 값을 포함합니다.

1. 포함 된 응답 메시지에 대 한 ETag 값을 새 hello 보냅니다 hello 보고 properties 컬렉션 항목에 대 한 다음 서비스 hello `$iothub/twin/res/{status}/?$rid={request id}`합니다. 이 응답 메시지를 사용 하 여 hello 동일 **요청 id** hello 요청으로 합니다.

hello 요청 메시지 본문에는 보고 속성 (기타 속성이 나 메타 데이터를 수정할 수 있음)에 대 한 새 값을 제공 하는 JSON 문서를 포함 합니다.
Hello JSON 문서에 있는 각 멤버를 업데이트 하거나 hello 장치로 이중의 문서에 hello 해당 멤버를 추가 합니다. 구성원 설정 너무`null`, 삭제 hello 개체를 포함 하는 hello에서 멤버입니다. 예:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

hello 가능한 상태 코드는.

|가동 상태 | 설명 |
| ----- | ----------- |
| 200 | 성공 |
| 400 | 잘못된 요청. 형식이 잘못된 JSON |
| 429 | 너무 많은 요청(제한됨), [IoT Hub 제한][lnk-quotas] 참조 |
| 5** | 서버 오류 |

자세한 내용은 [장치 쌍 개발자 가이드][lnk-devguide-twin]를 참조하세요.

### <a name="receiving-desired-properties-update-notifications"></a>desired 속성 업데이트 알림 수신

IoT Hub 장치가 연결 된 알림 toohello 항목 보냅니다 `$iothub/twin/PATCH/properties/desired/?$version={new version}`, hello 솔루션 백 엔드 수행한 hello 업데이트의 hello 콘텐츠를 포함 하는 합니다. 예:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

속성 업데이트와 `null` hello JSON 값은 개체 멤버를 삭제 하는 중입니다.


> [!IMPORTANT] 
> IoT Hub는 장치가 연결된 경우에만 변경 알림을 생성하여 있는지 tooimplement hello 확인 [장치 다시 연결 흐름] [ lnk-devguide-twin-reconnection] tookeep hello 원하는 속성 IoT Hub와 hello 장치 응용 프로그램 간에 동기화 합니다.

자세한 내용은 [장치 쌍 개발자 가이드][lnk-devguide-twin]를 참조하세요.

### <a name="respond-tooa-direct-method"></a>응답 tooa 직접적인 방법

첫째, 장치가 toosubscribe 너무`$iothub/methods/POST/#`합니다. IoT Hub 보냅니다 메서드 요청 toohello 항목 `$iothub/methods/POST/{method name}/?$rid={request id}`, 유효한 JSON 또는 본문이 비어 있습니다.

hello 장치 toorespond, 유효한 JSON 또는 빈 본문 toohello 항목으로 메시지를 보내는 `$iothub/methods/res/{status}/?$rid={request id}`여기서 **요청 id** toomatch hello 요청 메시지에서 hello에 및 **상태** toobe 정수에 .

자세한 내용은 [직접 메서드 개발자 가이드][lnk-methods]를 참조하세요.

### <a name="additional-considerations"></a>추가 고려 사항

최종 고려 사항으로 toocustomize hello MQTT 프로토콜 동작 hello 클라우드 쪽에서는 필요한 경우 검토 해야 hello [Azure IoT 프로토콜 게이트웨이] [ lnk-azure-protocol-gateway] 수 있게 해 주는 toodeploy 성능 우선 IoT Hub와 직접 상호 작용 하는 사용자 지정 프로토콜 게이트웨이. hello Azure IoT 프로토콜 게이트웨이 있습니다 toocustomize hello 장치 프로토콜 tooaccommodate brownfield MQTT 배포 또는 기타 사용자 지정 프로토콜을 활성화합니다. 그렇지만 이 방법을 사용하는 경우 사용자 지정 프로토콜 게이트웨이를 실행하고 작동해야 합니다.

## <a name="next-steps"></a>다음 단계

hello MQTT 프로토콜에 대해 자세히 toolearn 참조 hello [MQTT 설명서][lnk-mqtt-docs]합니다.

IoT Hub 배포 계획에 대해 자세히 toolearn 참조:

* [IoT용 Azure Certified 장치 카탈로그][lnk-devices]
* [추가 프로토콜 지원][lnk-protocols]
* [Event Hubs와 비교][lnk-compare]
* [크기 조정, HA 및 DR][lnk-scaling]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
