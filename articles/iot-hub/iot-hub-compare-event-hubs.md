---
title: "이벤트 허브 aaaCompare Azure IoT Hub tooAzure | Microsoft Docs"
description: "Hello IoT Hub 및 이벤트 허브 Azure 서비스 기능 차이 및 사용 사례를 강조 표시 비교 합니다. 지원 되는 프로토콜, 장치 관리, 모니터링을 포함 하는 hello 비교 하 고 파일 업로드 합니다."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Azure IoT Hub 및 Azure Event Hubs의 비교
IoT Hub에 대 한 hello 주요 사용 사례 중 하나에 장치에서 toogather 원격 분석입니다. 이러한 이유로 IoT Hub는 종종 비교 너무[Azure 이벤트 허브][Azure Event Hubs]합니다. IoT Hub와 같은 이벤트 허브는 이벤트 처리 서비스 이벤트 및 원격 분석 수신을 사용 하도록 설정 하는 낮은 대기 시간과 높은 안정성 대규모로 toohello 클라우드입니다.

그러나 hello 서비스는 다음 표에 hello에 자세히 설명 되어 있는 많은 차이점이 있습니다.

| 영역 | IoT 허브 | Event Hubs |
| --- | --- | --- |
| 통신 패턴 | [장치-클라우드 통신][lnk-d2c-guidance](메시징, 파일 업로드 및 reported 속성) 및 [클라우드-장치 통신][lnk-c2d-guidance](직접 메서드, desired 속성, 메시징)을 사용합니다. |이벤트 수신만(일반적으로 장치-클라우드 시나리오에 대해 고려됨)만 가능합니다. |
| 장치 상태 정보 | [장치 쌍][lnk-twins]은 장치 상태 정보를 저장하고 쿼리할 수 있습니다. | 어떤 장치 상태 정보도 저장할 수 없습니다. |
| 장치 프로토콜 지원 |MQTT, WebSocket을 통한 MQTT, AMQP, WebSocket을 통한 AMQP 및 HTTP를 지원합니다. IoT Hub hello로 작동 하는 또한 [Azure IoT 프로토콜 게이트웨이][lnk-azure-protocol-gateway], 한 사용자 지정 가능한 프로토콜 게이트웨이 구현 toosupport 사용자 지정 프로토콜입니다. |AMQP, WebSocket을 통한 AMQP 및 HTTP를 지원합니다. |
| 보안 |장치 단위 ID 및 취소 가능한 액세스 제어를 제공합니다. Hello 참조 [hello IoT 허브 개발자 가이드의 보안 섹션]합니다. |[게시자의 정책][Event Hubs publisher policies]을 통해 제한된 해지 지원을 포함하는 Event Hubs 전반의 [공유 액세스 정책][Event Hubs - security]을 제공합니다. IoT 솔루션은 필요한 tooimplement는 사용자 지정 솔루션 toosupport 장치 자격 증명 및 스푸핑 방지 측정값 경우가 많습니다. |
| 작업 모니터링 |IoT 솔루션 toosubscribe tooa 다양을 한 개별 장치 인증 오류, 제한 및 잘못 된 형식의 예외와 같은 장치 identity 관리 및 연결 이벤트 수 있습니다. 이러한 이벤트를 사용 하면 tooquickly hello 개별 장치 수준에서 연결 문제를 식별 합니다. |집계 메트릭만 표시합니다. |
| 확장 |최적화 된 toosupport 수백만 개의 동시에 연결 된 장치입니다. |미터 hello 당으로 연결 [Azure 이벤트 허브 할당량][Azure Event Hubs quotas]합니다. Hello 반면에, 이벤트 허브를 사용 하면 보낸 각 메시지에 대 한 toospecify hello 파티션 합니다. |
| 장치 SDK |제공 [장치 Sdk] [ Azure IoT SDKs] 다양 한 플랫폼 및 추가 toodirect MQTT, AMQP 및 HTTP Api에서 언어에 대 한 합니다. |또한 tooAMQP 및 HTTP 송신 인터페이스에서.NET, Java 및 C에서 지원 됩니다. |
| 파일 업로드 |IoT 장치 toohello 클라우드 솔루션 tooupload 파일 수 있습니다. 워크플로 통합에 대한 파일 알림 끝점과 디버깅 지원에 대한 작업 모니터링 범주를 포함합니다. | 지원되지 않습니다. |
| 경로는 toomultiple 끝점 메시지 | 사용자 지정 끝점은 too10까지 지원 됩니다. 규칙은 메시지 toocustom 라우트된 끝점에는 방법을 결정 합니다. 자세한 내용은 [IoT Hub를 통해 메시지 보내고 받기][lnk-devguide-messaging]를 참조하세요. | 작성 하 고 메시지 디스패치를 위한 호스트 추가 코드 toobe가 필요 합니다. |

요약 하자면, hello만 사용 사례는 장치-클라우드 원격 분석 수신 하는 경우에 IoT Hub는 서비스를 제공 설계 된 IoT 장치 연결에 대 한 합니다. Tooexpand hello 가치 제안 IoT와 관련 된 기능을 사용 하 여 이러한 시나리오를 계속합니다. 이벤트 허브는 대규모 데이터 센터 간 및 내부 데이터 센터 시나리오의 hello 컨텍스트에서 모두 이벤트 수신 하도록 설계 되었습니다.

일반적이 지 않은 toouse 없으면 IoT Hub 및 이벤트 허브에 모두 동일한 솔루션 hello 합니다. 이벤트 허브 실시간 처리 엔진에 이후 단계 이벤트 수신 처리 및 IoT Hub hello 장치-클라우드 통신을 처리 합니다.

### <a name="next-steps"></a>다음 단계
IoT Hub 배포 계획에 대해 자세히 toolearn 참조 [배율, HA, 및 DR][lnk-scaling]합니다.

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[hello IoT 허브 개발자 가이드의 보안 섹션]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
