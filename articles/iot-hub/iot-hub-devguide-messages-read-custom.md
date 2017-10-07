---
title: "aaaUnderstand Azure IoT 허브에 대 한 사용자 지정 끝점 | Microsoft Docs"
description: "개발자 가이드-tooroute 장치-클라우드 메시지 toocustom 끝점 규칙 라우팅을 사용 하 여 합니다."
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>장치-클라우드 메시지에 대해 메시지 라우팅 및 사용자 지정 끝점 사용

IoT 허브를 사용 하면 tooroute [장치-클라우드 메시지] [ lnk-device-to-cloud] tooIoT 허브 서비스 측 끝점 메시지 속성에 기초 합니다. Hello 없이 toogo 적시에 메시지 라우팅 규칙 지정 유연성 toosend hello tooprocess 메시지나 toowrite 추가 코드가 추가 서비스에 대 한 필요. 구성한 각 라우팅 규칙에는 다음과 같은 속성 hello:

| 속성      | 설명 |
| ------------- | ----------- |
| **Name**      | hello 규칙을 식별 하는 고유 이름 hello입니다. |
| **원본**    | hello hello 데이터 원본을 스트림 toobe 작업을 수행 합니다. 예를 들어 장치 원격 분석이 있습니다. |
| **Condition** | hello hello 메시지의 헤더 및 본문에 대해 실행 되 고 toodetermine를 사용 하 여 hello 끝점에 대 한 일치 하는 항목 인지 여부를 지정 하는 hello 라우팅 규칙에 대 한 쿼리 식입니다. 경로 조건 생성에 대 한 자세한 내용은 참조 hello [장치 트윈스 및 작업에 대 한 쿼리 언어 참조-][lnk-devguide-query-language]합니다. |
| **끝점**  | IoT Hub hello 조건과 일치 하는 메시지를 전송 하는 위치 hello 끝점의 hello 이름입니다. 끝점 hello에 있어야 합니다. hello IoT hub와 같은 지역의 그렇지 않으면 있습니다 요금이 청구 되 지역 간 작성에 대 한 합니다. |

단일 메시지에는 사례 IoT 허브는 hello 메시지 toohello 끝점과 연결 된 각 일치 규칙을 제공 하는 여러 라우팅 규칙에 hello 상태를 간주할 수 있습니다. IoT Hub는 자동으로 메시지 배달을 deduplicates 메시지가 일치 하는 경우 결합 된 여러 규칙을 가진 hello 되므로 동일한 대상 것만 toothat 대상 한 번씩 기록 됩니다.

IoT Hub에는 기본 [기본 제공 끝점][lnk-built-in]이 있습니다. 사용자 지정 끝점 tooroute 메시지 tooby 구독 toohello 허브의 다른 서비스 연결을 만들 수 있습니다. IoT Hub는 현재 사용자 지정 끝점으로 Event Hubs, Service Bus 큐 및 Service Bus 토픽을 지원합니다.

> [!WARNING]
> **세션** 또는 **중복 검색**이 사용하도록 설정된 Service Bus 큐 및 토픽은 사용자 지정 끝점으로 지원되지 않습니다.

IoT Hub에 사용자 지정 끝점을 만드는 방법에 대한 자세한 내용은 [IoT Hub 끝점][lnk-devguide-endpoints]을 참조하세요.

사용자 지정 끝점에서 읽는 방법에 대한 자세한 내용은 다음을 참조하세요.

* [Event Hubs][lnk-getstarted-eh]에서 읽기
* [Service Bus 큐][lnk-getstarted-queue]에서 읽기
* [Service Bus 토픽][lnk-getstarted-topic]에서 읽기

### <a name="next-steps"></a>다음 단계

IoT Hub 끝점에 대한 자세한 내용은 [IoT Hub 끝점][lnk-devguide-endpoints]을 참조하세요.

Hello 쿼리 언어에 대 한 자세한 내용은 toodefine 라우팅 규칙을 사용할 참조 [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어][lnk-devguide-query-language]합니다.

hello [경로 사용 하 여 프로세스 IoT Hub 장치-클라우드 메시지] [ lnk-d2c-tutorial] 자습서 toouse 라우팅 규칙 방식 및 표시 사용자 지정 끝점입니다.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
