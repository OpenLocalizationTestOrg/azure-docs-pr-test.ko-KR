---
title: "aaaUnderstand Azure IoT Hub 메시지 형식 | Microsoft Docs"
description: "개발자 가이드-구형 hello 예상의 형식과 내용을 IoT Hub 메시지입니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>IoT Hub 메시지 만들기 및 읽기

프로토콜을 통해 완전 한 상호 운용성 toosupport IoT Hub에 장치에 연결 하는 모든 프로토콜에 대 한 일반적인 메시지 형식을 정의합니다. 이 메시지 형식은 [장치-클라우드][lnk-d2c] 및 [클라우드-장치][lnk-c2d] 메시지 둘 다에 사용됩니다. [IoT Hub 메시지][lnk-messaging]는 다음으로 구성됩니다.

* *시스템 속성*집합. IoT Hub가 해석하거나 설정하는 속성입니다. 이 집합은 미리 결정됩니다.
* *응용 프로그램 속성*집합. Hello 응용 프로그램을 정의할 수 있는 문자열 속성 및 toodeserialize hello 메시지 본문 없이 액세스의 사전입니다. IoT Hub는 절대로 이러한 속성을 수정하지 않습니다.
* 불투명한 이진 본문.

속성 이름과 값은 다음과 같은 경우에 ASCII 영숫자 문자와 ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}``를 포함할 수 있습니다.

* Hello HTTP 프로토콜을 사용 하 여 장치-클라우드 메시지를 보냅니다.
* 클라우드-장치 메시지를 보냅니다.

방법에 대 한 자세한 내용은 tooencode 서로 다른 프로토콜을 사용 하 여 보낸 메시지를 디코딩할 참조 및 [Azure IoT Sdk][lnk-sdks]합니다.

다음 표에 hello hello 메시지 IoT 허브에서에서 시스템 속성 집합을 나열 합니다.

| 속성 | 설명 |
| --- | --- |
| MessageId |요청-회신 패턴에 사용 되는 hello 메시지에 대 한 사용자 설정 식별자입니다. 형식: 대/소문자 구분 문자열 (위쪽 too128 자)는 영숫자 ASCII 7 비트 + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`합니다. |
| 시퀀스 번호 |고유한 장치 큐가 할당 한 번호 IoT Hub tooeach 클라우드-장치 메시지입니다. |
| 너무|[클라우드-장치][lnk-c2d] 메시지에 지정된 대상입니다. |
| ExpiryTimeUtc |메시지 만료 날짜 및 시간입니다. |
| EnqueuedTime |날짜 및 시간 hello [클라우드-장치] [ lnk-c2d] IoT 허브에서 메시지를 받았습니다. |
| CorrelationId |일반적으로 요청-회신 패턴의 hello 요청 MessageId hello를 포함 하는 응답 메시지에 사용 되는 문자열 속성입니다. |
| UserId |ID는 toospecify hello 원본 메시지를 사용 합니다. 너무 설정 메시지가 IoT 허브에 의해 생성 되 면`{iot hub name}`합니다. |
| Ack |피드백 메시지 생성기입니다. 이 속성은 hello 장치별 hello 메시지의 hello 소비로 인해 클라우드-장치 메시지 toorequest IoT Hub toogenerate 피드백 메시지에 사용 됩니다. 가능한 값: **none** (기본값): 없음 피드백 메시지가 생성 되 **양의**: hello 메시지 완료 된 경우 피드백 메시지가 **음수**: 수신는 피드백 메시지 hello 메시지는 만료 되었습니다 (또는 최대 배달 횟수에 도달 했습니다) hello 장치에 의해 완료 되 고 없는 경우 또는 **전체**: 긍정 및 부정 합니다. 자세한 내용은 [메시지 피드백][lnk-feedback]을 참조하세요. |
| ConnectionDeviceId |IoT Hub에서 장치-클라우드 메시지에 설정하는 ID입니다. Hello 포함 되어 **deviceId** hello 메시지를 보낸 hello 장치의 합니다. |
| ConnectionDeviceGenerationId |IoT Hub에서 장치-클라우드 메시지에 설정하는 ID입니다. Hello 포함 되어 **generationId** (기준으로 [장치 id 속성][lnk-device-properties]) hello 메시지를 보낸 hello 장치의 합니다. |
| ConnectionAuthMethod |IoT Hub에서 장치-클라우드 메시지에 설정하는 인증 방법입니다. 이 속성 hello 메시지를 보내는 hello 인증 사용 하는 방법 tooauthenticate hello 장치에 대 한 정보를 포함 합니다. 자세한 내용은 참조 [장치 toocloud 스푸핑 방지][lnk-antispoofing]합니다. |

## <a name="message-size"></a>메시지 크기

IoT Hub 측정만 hello 실제 페이로드를 고려 프로토콜을 알 수 없는 방식으로 메시지 크기입니다. hello 크기 (바이트) hello 다음의 hello 합계로 계산 됩니다.

* hello 본문 크기 (바이트)입니다.
* hello hello 메시지 시스템 속성의 모든 hello 값의 바이트 크기입니다.
* 모든 사용자 속성 이름 및 값의 바이트 hello 크기입니다.

속성 이름 및 값은 제한 tooASCII 문자 hello hello 문자열 길이 크기를 바이트 단위로 hello와 같습니다.

## <a name="next-steps"></a>다음 단계

IoT Hub의 메시지 크기 제한에 대한 자세한 내용은 [IoT Hub 할당량 및 제한][lnk-quotas]을 참조하세요.

toolearn toocreate 및 다양 한 프로그래밍 언어의 읽기 IoT Hub 메시지를 확인 하려면 어떻게 hello [시작] [ lnk-get-started] 자습서입니다.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
