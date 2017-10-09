---
title: "IoT Hub 통신 aaaAzure 프로토콜 및 포트 | Microsoft Docs"
description: "개발자 가이드-장치-클라우드 및 클라우드-장치 통신 및 열려 있어야 하는 hello 포트 번호에 대 한 지원 hello 통신 프로토콜을 설명 합니다."
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
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# 참조 - 통신 프로토콜 선택

IoT 허브를 사용 하면 장치 toouse [MQTT][lnk-mqtt], MQTT Websocket 통해 [AMQP][lnk-amqp], 장치 측에 대 한 Websocket, 및 HTTP를 통해 AMQP 프로토콜 통신 합니다. 이러한 프로토콜이 특정 IoT Hub 기능을 지원하는 방식에 대한 내용은 [장치-클라우드 통신 지침][lnk-d2c-guidance] 및 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.

hello 다음 표에서 hello 고급 권장 사항을 선택에 대 한 프로토콜의 합니다.

| 프로토콜 | 이 프로토콜을 선택해야 하는 경우 |
| --- | --- |
| MQTT <br> WebSocket을 통한 MQTT |Hello를 통해 여러 장치 (각각 고유한 장치 자격 증명)를 tooconnect 필요 하지 않은 모든 장치에서 사용 같은 TLS 연결 합니다. |
| AMQP <br> WebSocket을 통한 AMQP |필드 및 클라우드 게이트웨이 tootake 활용 멀티플렉싱 장치 간의 연결에 사용 합니다. |
| HTTP |다른 프로토콜을 지원할 수 없는 장치에 사용됩니다. |

장치 측 통신에 대 한 프로토콜을 선택 하는 경우 지점 뒤에 hello를 고려 합니다.

* **클라우드-장치 패턴**. HTTP는 효율적인 방법을 tooimplement 서버 푸시를 없습니다. 이와 같이 HTTP를 사용하는 경우 장치는 클라우드-장치 메시지에 IoT Hub를 폴링합니다. 이 방법은 hello 장치와 IoT 허브에 대 한 효율적인 하지 않습니다. 현재 HTTP 지침에 따르면 각 장치는 25분 이상 간격으로 메시지를 폴링해야 합니다. 다른 손 hello, MQTT 및 AMQP 클라우드-장치 메시지를 받을 때 서버 푸시를 지원 합니다. IoT Hub toohello 장치에서 메시지의 즉시 푸시 수 있습니다. 배달 대기 시간 문제가 되 MQTT 또는 AMQP hello 최상의 프로토콜 toouse 됩니다. 드물게 연결되는 장치의 경우 HTTP도 작동합니다.
* **현장 게이트웨이**. 여러 장치 (각각 고유한 장치 자격 증명)를 연결할 수 없는 MQTT 및 HTTP를 사용할 때 동일한 TLS 연결 hello를 사용 하 여 합니다. 따라서 [게이트웨이 시나리오 필드][lnk-azure-gateway-guidance], 각 장치 연결 된 toohello 필드 게이트웨이에 대해 hello 필드 게이트웨이 및 IoT 허브에서 하나의 TLS 연결 필요 하기 때문에 이러한 프로토콜은 만족 스 럽 지 합니다.
* **낮은 리소스 장치**. hello MQTT 및 HTTP 라이브러리 hello AMQP 라이브러리 보다 적은 사용을 했습니다. 경우 hello, 따라서 장치에 제한 된 리소스 (예를 들어 1 MB RAM 보다 작음), 이러한 프로토콜 hello 유일한 프로토콜 구현을 사용할 수 있습니다.
* **네트워크 통과**. hello 표준 AMQP 프로토콜 MQTT 닫힌된 toonon HTTP 프로토콜에 있는 네트워크에서 문제가 발생할 수 있는 8883, 포트에서 수신 하는 동안 포트 5671을 사용 합니다. Websocket 통해 MQTT, WebSockets, 및 HTTP를 통해 AMQP는 사용할 수 있는 toobe이이 시나리오에 사용 합니다.
* **페이로드 크기**. MQTT 및 AMQP는 바이너리 프로토콜로, HTTP보다 더 많이 압축된 페이로드를 발생합니다.

> [!WARNING]
> HTTP를 사용하는 경우 각 장치는 25분 이상마다 클라우드-장치에 대해 폴링합니다. 그러나 개발 하는 동안 되기 허용 toopoll 25 분 보다 더 자주 있습니다.

## 포트 번호

장치는 다양한 프로토콜을 사용하여 Azure에서 IoT Hub와 통신할 수 있습니다. 일반적으로 프로토콜 hello 선택 hello hello 솔루션의 특정 요구 사항에 의해 이루어집니다. hello 다음 표에 장치 toobe 수 toouse 특정 프로토콜에 대 한 열려 있어야 하는 hello 아웃 바운드 포트.

| 프로토콜 | 포트 |
| --- | --- |
| MQTT |8883 |
| WebSocket을 통한 MQTT |443 |
| AMQP |5671 |
| Websocket 통한 AMQP |443 |
| HTTP |443 |

Azure 지역에서 IoT hub를 만든 후 hello IoT 허브 유지 hello 동일한 IP 주소 hello 수명의 해당 IoT 허브에 대 한 합니다. 그러나 toomaintain 품질의 서비스를 Microsoft 이면 hello IoT 허브 tooa 다른 배율 단위를 이동 하는 경우 새 IP 주소를 할당 됩니다.


## 다음 단계

IoT Hub hello MQTT 프로토콜을 구현 하는 방법에 대해 자세히 toolearn 참조 [hello MQTT 프로토콜을 사용 하 여 IoT 허브와 통신][lnk-mqtt-support]합니다.

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
