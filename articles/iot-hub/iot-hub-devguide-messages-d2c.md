---
title: "aaaUnderstand Azure IoT Hub 장치-클라우드 메시징 | Microsoft Docs"
description: "개발자 가이드-어떻게 toouse 장치-클라우드 IoT Hub와 메시징입니다. 원격 분석 및 비 telemtry 모두 데이터를 보내고 라우팅 toodeliver 메시지를 사용 하는 방법에 대 한 정보가 포함 됩니다."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>장치-클라우드 메시지 tooIoT 허브 보내기

toosend 시계열 원격 분석 및 경고 프로그램 장치 tooyour 솔루션 백 엔드를 장치 tooyour IoT 허브에서 장치-클라우드 메시지를 전송 합니다. IoT Hub에서 지원하는 기타 장치-클라우드 옵션에 대한 설명은 [장치-클라우드 통신 지침][lnk-d2c-guidance]을 참조하세요.

장치 지향 끝점(**/devices/{deviceId}/messages/events**)을 통해 장치-클라우드 메시지를 보냅니다. 라우팅 규칙 다음 hello 웹 서비스 끝점에 메시지 tooone IoT 허브에 라우트 합니다. Hello 헤더와 본문 허브 toodetermine를 통해 흐르는 hello 장치-클라우드 메시지의 라우팅 규칙에 사용 하 여 여기서 tooroute 해당 합니다. 기본적으로 메시지는 라우트된 toohello 기본 제공 서비스 연결 끝점 (**이벤트 메시지/**), 즉 호환 [이벤트 허브][lnk-event-hubs]합니다. 따라서 표준을 사용할 수 있습니다 [이벤트 허브 통합 및 Sdk] [ lnk-compatible-endpoint] 솔루션에서 장치-클라우드 메시지 tooreceive 백 엔드 합니다.

IoT Hub는 스트리밍 메시징 패턴을 사용하여 장치-클라우드 메시징을 구현합니다. IoT Hub 장치-클라우드 메시지와 더 비슷하게는 [이벤트 허브] [ lnk-event-hubs] *이벤트* 보다 [서비스 버스] [ lnk-servicebus] *메시지* 많은 양의 여러 판독기가 읽을 수 있는 hello 서비스를 통해 전달 되는 이벤트는 합니다.

장치-클라우드 IoT Hub와 메시징 hello 특성 뒤에 있습니다.

* 장치-클라우드 메시지는 영 속 IoT 허브의 기본 보존 **이벤트메시지/** tooseven 일 구성에 대 한 끝점입니다.
* 장치-클라우드 메시지 256KB 최대 있어야 하 고 toooptimize 전송 하는 일괄 처리로 그룹화 할 수 있습니다. 배치는 최대 256KB가 될 수 있습니다.
* Hello에 설명 된 대로 [컨트롤 액세스 tooIoT 허브] [ lnk-devguide-security] 섹션에서 IoT Hub-장치 인증 및 액세스 제어를 사용 하면 됩니다.
* IoT Hub too10 사용자 지정 끝점을 toocreate가 있습니다. 메시지가는 IoT hub에 구성 된 경로에 따라 toohello 끝점 배달 됩니다. 자세한 내용은 [라우팅 규칙](#routing-rules)을 참조하세요.
* IoT Hub를 사용하면 수백만 대의 장치를 동시에 연결할 수 있습니다([할당량 및 제한][lnk-quotas] 참조).
* IoT Hub는 임의 분할을 허용하지 않습니다. 장치-클라우드 메시지는 원래 **deviceId**와 관련하여 분할됩니다.

Hello 차이 hello IoT Hub 및 이벤트 허브 서비스에 대 한 자세한 내용은 참조 [Azure IoT Hub 비교 및 Azure 이벤트 허브][lnk-comparison]합니다.

## <a name="send-non-telemetry-traffic"></a>비-원격 분석 트래픽 보내기

메시지를 별도 실행 및 hello 솔루션 백 엔드의 처리를 필요로 하는 요청 장치 보내고 종종는 또한 tootelemetry 데이터 요소, 합니다. 예를 들어 hello에서 특정 동작을 트리거해야 하는 중요 한 알림 백 엔드 합니다. 쉽게 작성할 수는 [라우팅 규칙] [ lnk-devguide-custom] toosend 이러한 유형의 메시지 tooan 끝점 전용 hello 메시지에 헤더 또는 hello 메시지 본문의 값에 따라 tootheir 처리 합니다.

Hello 가장 좋은 방법은 tooprocess이 메시지의 종류에 대 한 자세한 내용은 참조 hello [자습서: 어떻게 tooprocess IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서입니다.

## <a name="route-device-to-cloud-messages"></a>장치-클라우드 메시지 라우팅

라우팅 장치-클라우드 메시지 tooyour 백 엔드 응용 프로그램에 대 한 두 가지 옵션이 있습니다.

* 기본 제공 hello를 사용 하 여 [호환 이벤트 허브 끝점] [ lnk-compatible-endpoint] tooenable 백 엔드 앱 tooread hello 장치-클라우드 메시지 hello 허브에서 수신 합니다. toolearn hello 기본 제공 하는 이벤트 허브 호환 끝점에 대 한 참조 [hello 기본 제공 끝점에서 장치-클라우드 메시지를 읽은][lnk-devguide-builtin]합니다.
* IoT hub에서 라우팅 규칙 toosend 메시지 toocustom 끝점을 사용 합니다. 사용자 지정 끝점을 이벤트 허브, 서비스 버스 큐 또는 Service Bus 항목을 사용 하 여 백 엔드 앱 tooread 장치-클라우드 메시지를 사용 하도록 설정 합니다. 라우팅 및 사용자 지정 끝점에 대 한 toolearn 참조 [장치-클라우드 메시지에 대 한 사용자 지정 끝점 및 라우팅 규칙을 사용 하 여][lnk-devguide-custom]합니다.

## <a name="anti-spoofing-properties"></a>스푸핑 방지 속성

IoT Hub는 장치-클라우드 메시지에 스탬프 hello 다음 속성이 있는 모든 메시지를 스푸핑 tooavoid 장치:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

hello 처음 두 개의 포함 hello **deviceId** 및 **generationId** 의 장치를 기준으로 발생 하는 hello [장치 id 속성][lnk-device-properties]합니다.

hello **ConnectionAuthMethod** 속성 다음과 같은 속성 hello로 JSON으로 직렬화 된 개체를 포함 합니다.

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>다음 단계

Hello Sdk에 대 한 내용은 toosend 장치-클라우드 메시지를 사용 하 여, 참조 수 [Azure IoT Sdk][lnk-sdks]합니다.

hello [시작] [ lnk-get-started] 보여 주는 자습서 시뮬레이션 및 실제 장치에서 toosend 장치-클라우드 메시지 방법을 합니다. 자세한 정보를 얻기 위해 hello 참조 [경로 사용 하 여 프로세스 IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서입니다.

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
