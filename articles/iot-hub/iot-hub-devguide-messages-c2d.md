---
title: "Azure IoT Hub 클라우드-장치 aaaUnderstand 메시징 | Microsoft Docs"
description: "개발자 가이드-어떻게 toouse 클라우드-장치 IoT Hub와 메시징입니다. Hello 메시지 수명 주기 및 구성 옵션에 대 한 정보가 포함 됩니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>IoT Hub에서 클라우드-장치 메시지 보내기

toosend 단방향 알림 toohello 장치 응용 프로그램 솔루션 백 엔드에서 IoT 허브 tooyour 장치에서 클라우드-장치 메시지를 보냅니다. IoT Hub가 지원하는 다른 클라우드-장치 옵션에 대한 설명은 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.

서비스 지향 끝점(**/messages/devicebound**)을 통해 클라우드-장치 메시지를 보냅니다. 장치를 장치 특정 끝점을 통해 hello 메시지 받습니다 (**/devices/ {deviceId} / 메시지/devicebound**).

각 클라우드-장치 메시지 대상으로 하는 단일 장치 hello 설정 하 여 **를** 속성 너무**/devices/ {deviceId} / 메시지/devicebound**합니다.

각 장치 큐는 클라우드-장치 메시지를 최대 50개까지 보유합니다. 더 많은 메시지 toohello toosend 시도 같은 장치는 오류가 발생 합니다.

## <a name="hello-cloud-to-device-message-lifecycle"></a>hello 클라우드-장치 메시지 수명 주기

IoT Hub tooguarantee에서-최소 1 회 메시지 배달을 장치 단위 큐에 있는 클라우드-장치 메시지를 유지합니다. 장치를 명시적으로 승인 해야 *완료* 큐 hello에서 IoT Hub tooremove에 대 한 합니다. 이 방법은 연결 및 장치 오류로부터 복원력을 보장합니다.

hello 다음 다이어그램 그래프를 보여 줍니다 hello 수명 주기 상태 클라우드-장치 메시지에 대 한 IoT Hub에 있습니다.

![클라우드-장치 메시지 수명 주기][img-lifecycle]

IoT Hub 서비스 hello 메시지 tooa 장치, hello 서비스를 보낼 때 설정 하는 hello 메시지 상태 너무**큐에 대기 된**합니다. 장치가 너무 경우*수신* 메시지가 IoT Hub *잠금* hello 메시지 (너무 hello 상태를 설정 하 여**보이지 않는**), 다른 스레드에서 hello 장치 toostart에서 허용 하는 다른 메시지를 수신 합니다. 장치 스레드 hello 메시지 처리를 완료 하 여 IoT Hub 알립니다 *완료* hello 메시지입니다. IoT Hub 다음 상태를 설정 hello 너무**Completed**합니다.

장치는 다음을 선택할 수도 있습니다.

* *거부* hello 메시지를 IoT Hub tooset 것 toohello **배달 못한 메시지로 분류** 상태입니다. Hello MQTT 프로토콜을 통해 연결 하는 장치는 클라우드-장치 메시지를 거부할 수 없습니다.
* *중단* hello 메시지를 IoT Hub tooput hello 메시지 hello 큐에 다시 hello 상태 너무 설정 하 여**큐에 대기 된**합니다.

스레드는 tooprocess 메시지가 IoT Hub에 게 알리지 않고 실패할 수 있습니다. 이 경우 메시지를 자동으로 hello에서 전환을 **보이지 않는** 상태 백 toohello **큐에 대기 된** 후 상태는 *표시 유형 (또는 잠금) 시간 초과*합니다. 이 시간 제한의 hello 기본 값은 1 분입니다.

메시지 hello 간에 전환할 수 **큐에 대기 된** 및 **보이지 않는** 에 대 한 상태에는 기껏해야 hello에 지정 된 횟수 만큼 hello **최대 배달 횟수** IoT 허브에서 속성입니다. IoT Hub 해당 전환 횟수 후 hello 메시지의 hello 상태 너무 설정**배달 못한 메시지로 분류**합니다. 마찬가지로, IoT 허브 상태를 설정 hello 메시지의 너무**배달 못한 메시지로 분류** 만료 시간 이후 (참조 [시간 toolive][lnk-ttl]).

hello [IoT Hub와 toosend 클라우드-장치 메시지 방법을] [ lnk-c2d-tutorial] hello에서 클라우드-장치 메시지 toosend 클라우드 하 고 장치에서 수신 하는 방법을 보여줍니다.

일반적으로 장치는 hello hello 메시지의 영향을 주지 않습니다 hello 응용 프로그램 논리 경우 클라우드-장치 메시지를 완료 합니다. 예를 들어 때 hello hello 메시지 콘텐츠를 로컬로 지속에 장치나 작업 처리가 성공적으로 실행 합니다. hello 메시지 인 손실 hello hello 응용 프로그램의 기능에 영향을 주지는 일시적인 정보를 수행할 수도 수입니다. 경우에 따라 장기 실행 작업에 대 한 צ ְ ײ hello 클라우드-장치 메시지를 유지 한 후 hello 로컬 저장소에 대 한 작업 설명입니다. 그런 다음 hello 작업의 진행률의 여러 단계에서 하나 이상의 장치-클라우드 메시지와 함께 hello 솔루션 백 엔드에 알릴 수 있습니다.

## <a name="message-expiration-time-toolive"></a>메시지 만료 (toolive 시간)

모든 클라우드-장치 메시지에는 만료 시간이 있습니다. 이 이번 hello 서비스에 의해 설정 됩니다 (hello에 **ExpiryTimeUtc** 속성), 또는 기본 hello를 사용 하 여 IoT 허브 *시간 toolive* IoT Hub 속성으로 지정 합니다. [클라우드-장치 구성 옵션][lnk-c2d-configuration]을 참조하세요.

일반적인 방식으로 tootake 장점은 만료 메시지 및 toodisconnected 장치 메시지를 전송 하지 않도록, tooset toolive 짧은 시간 값이 있습니다. 이 방법은 hello 보다 효율적인 하면서 hello 장치 연결 상태를 유지 관리와 같은 결과 얻을 수 있습니다. 메시지 승인이 요청 하는 경우 장치는 수 tooreceive 메시지 이며 어떤 장치가 온라인 상태 인지 실패 한 IoT Hub 알립니다.

## <a name="message-feedback"></a>메시지 피드백

클라우드-장치 메시지를 보내면 hello 서비스는 hello 메시지의 최종 상태에 대 한 메시지 피드백의 hello 배달을 요청할 수 있습니다.

| Ack 속성 | 동작 |
| ------------ | -------- |
| **positive** | IoT Hub 피드백 메시지를 생성 하 고 hello 클라우드-장치 메시지 hello에 도달한 경우에 **Completed** 상태입니다. |
| **negative** | IoT Hub 및 경우에, hello 클라우드-장치 메시지 큐에 도달 hello 피드백 메시지를 생성 **배달 못한 메시지로 분류** 상태입니다. |
| **full**     | IoT Hub는 어떤 경우든 피드백 메시지를 생성합니다. |

경우 **Ack** 은 **전체**, 및 피드백 메시지가, 해당 hello 피드백 메시지 만료 된 것을 의미 합니다. hello 서비스 어떤 발생 했습니다 toohello 원본 메시지를 알 수 없습니다. 실제로 서비스는 만료 되기 전에 hello 피드백을 처리할 수 있도록 확인 해야 합니다. hello 최대 만료 시간은 2 일 수 있는 충분 한 시간 tooget hello 서비스를 다시 실행 오류가 발생 합니다.

[끝점][lnk-endpoints]에 설명된 대로 IoT Hub는 서비스 지향 끝점(**/messages/servicebound/feedback**)을 통해 피드백을 메시지로 전달합니다. hello 의미 체계 의견을 받기 위한 클라우드-장치 메시지의 경우와 동일는 hello와 같은 hello가 [메시지 수명 주기][lnk-lifecycle]합니다. 가능 하면 항상 피드백 메시지 일괄 처리 되는 단일 메시지에서 형식에 따라 hello로:

| 속성     | 설명 |
| ------------ | ----------- |
| EnqueuedTime | Hello 메시지를 만들 때를 나타내는 타임 스탬프입니다. |
| UserId       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

hello 본문은 다음과 같은 속성 hello로 각 레코드의 JSON 직렬화 된 배열:

| 속성           | 설명 |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | Hello 메시지의 hello 결과 발생 한 시기를 나타내는 타임 스탬프입니다. 예를 들어 완료 하는 장치를 hello 또는 hello 메시지는 만료 되었습니다. |
| OriginalMessageId  | **MessageId** hello 클라우드-장치 메시지 toowhich의이 사용자 의견 정보를 연결 합니다. |
| StatusCode         | 필수 문자열 IoT Hub에 의해 생성된 피드백 메시지에서 사용됩니다. <br/> 'Success' <br/> 'Expired' <br/> 'DeliveryCountExceeded' <br/> 'Rejected' <br/> 'Purged' |
| 설명        | **StatusCode**에 대한 문자열 값입니다. |
| deviceId           | **DeviceId** hello 클라우드-장치 메시지 toowhich의 hello 대상 장치의 피드백의이 부분 연결 합니다. |
| DeviceGenerationId | **DeviceGenerationId** hello 클라우드-장치 메시지 toowhich의 hello 대상 장치의 피드백의이 부분 연결 합니다. |

hello 서비스 지정 해야 합니다는 **MessageId** hello 클라우드-장치 메시지 toobe 수 toocorrelate 해당 피드백 hello 원본 메시지에 대 한 합니다.

hello 다음 예제에서는 hello 피드백 메시지 본문

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>클라우드-장치 구성 옵션

각 IoT 허브는 hello 다음 클라우드-장치 메시징에 대 한 구성 옵션을 제공 합니다.

| 속성                  | 설명 | 범위 및 기본값 |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | 클라우드-장치 메시지에 대한 기본 TTL | Too2D ISO_8601 간격 (최소 1 분)입니다. 기본값은 1시간입니다. |
| maxDeliveryCount          | 클라우드-장치 장치 단위 큐에 대한 최대 전달 수입니다. | 1 too100 합니다. 기본값은 10입니다. |
| feedback.ttlAsIso8601     | 서비스 바인딩 피드백 메시지에 대한 보존 기간입니다. | Too2D ISO_8601 간격 (최소 1 분)입니다. 기본값은 1시간입니다. |
| feedback.maxDeliveryCount |피드백 큐에 대한 최대 전달 수입니다. | 1 too100 합니다. 기본값은 100입니다. |

Tooset 이러한 구성 옵션을 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [만들 IoT hub][lnk-portal]합니다.

## <a name="next-steps"></a>다음 단계

Hello Sdk에 대 한 내용은 tooreceive 클라우드-장치 메시지를 사용 하 여, 참조 수 [Azure IoT Sdk][lnk-sdks]합니다.

클라우드-장치 메시지를 받는 아웃 tootry 참조 hello [클라우드-장치 보내기] [ lnk-c2d-tutorial] 자습서입니다.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
