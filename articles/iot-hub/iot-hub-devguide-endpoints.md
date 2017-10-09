---
title: "aaaUnderstand Azure IoT Hub 끝점 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub 장치 지향 및 서비스 지향 끝점에 대한 참조 정보"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>참조 - IoT Hub 끝점

## <a name="iot-hub-names"></a>IoT Hub 이름

Hello hello 포털에 끝점을 호스팅하는 hello IoT 허브의 hello 이름을 찾을 수 있습니다 **개요** 블레이드입니다. 기본적으로 IoT hub의 hello DNS 이름을 다음과 같은: `{your iot hub name}.azure-devices.net`합니다.

Azure DNS toocreate IoT 허브에 대 한 사용자 지정 DNS 이름을 사용할 수 있습니다. 자세한 내용은 참조 [Azure 서비스에 대 한 Azure DNS를 사용 하 여 tooprovide 사용자 지정 도메인 설정을](../dns/dns-custom-domain.md#azure-iot)합니다.

## <a name="list-of-built-in-iot-hub-endpoints"></a>기본 제공 IoT Hub 끝점 목록

Azure IoT Hub는 해당 기능 toovarious 행위자를 노출 하는 다중 테 넌 트 서비스입니다. hello 다음 그림에 hello IoT Hub를 노출 하는 다양 한 끝점입니다.

![IoT Hub 끝점][img-endpoints]

다음 목록 hello hello 끝점을 설명 합니다.

* **리소스 공급자**. hello IoT 허브 리소스 공급자가 노출 된 [Azure 리소스 관리자] [ lnk-arm] 인터페이스입니다. 이 인터페이스는 Azure 구독 소유자 toocreate 있으며 IoT hub 및 tooupdate IoT 허브 속성을 삭제 합니다. IoT Hub 속성 제어 [허브 수준 보안 정책은][lnk-accesscontrol]toodevice 액세스 제어 및 클라우드-장치 및 장치-클라우드 메시지에 대 한 기능 옵션을 반대로 합니다. hello IoT 허브 리소스 공급자 사용 하면 수도 너무[장치 id를 내보내기][lnk-importexport]합니다.
* **장치 ID 관리**. HTTP REST 끝점 toomanage 장치 id 집합을 노출 하는 각 IoT 허브 (만들기, 검색, 업데이트 및 삭제) 합니다. [장치 ID][lnk-device-identities]는 장치 인증 및 액세스 제어에 사용됩니다.
* **장치 쌍 관리**. 서비스에 연결 되어 있고 HTTP REST 끝점 tooquery 업데이트 집합을 노출 하는 각 IoT 허브 [장치 트윈스] [ lnk-twins] (태그 및 속성 업데이트) 합니다.
* **작업 관리**. 각 IoT 허브 서비스 지향 HTTP REST 끝점 tooquery의 집합을 노출 하 고 관리 [작업][lnk-jobs]합니다.
* **장치 끝점**. Hello id 레지스트리에 각 장치에 대 한 IoT Hub 끝점 집합에 노출합니다.

  * *장치-클라우드 메시지 보내기*. 장치는이 끝점을 너무 사용[장치-클라우드 메시지를 보낼][lnk-d2c]합니다.
  * *클라우드-장치 메시지 받기*. 장치를 대상으로이 끝점 tooreceive 사용 [클라우드-장치 메시지][lnk-c2d]합니다.
  * *파일 업로드를 시작합니다*. 장치 사용이 끝점 tooreceive IoT 허브에서 Azure 저장소 SAS URI 너무[파일 업로드][lnk-upload]합니다.
  * *장치 쌍 속성 검색 및 업데이트*. 이 끝점 tooaccess 장치를 사용 하는 [장치로 이중][lnk-twins]의 속성입니다.
  * *직접 메서드 요청 수신*. 장치 사용에 대 한이 끝점 toolisten [직접적인 방법][lnk-methods]의 요청 합니다.

    이러한 끝점은 [MQTT v3.1.1][lnk-mqtt], HTTP 1.1 및 [AMQP 1.0][lnk-amqp] 프로토콜을 사용하여 공개됩니다. AMQP는 포트 443의 [WebSockets][lnk-websockets]를 통해서도 사용할 수 있습니다.

    hello 장치 트윈스 메서드와 끝점은 사용할 수 있는 hello를 사용 하는 경우에 [MQTT v3.1.1] [ lnk-mqtt] 프로토콜입니다.

* **서비스 끝점**. 각 IoT 허브에서 장치 집합 솔루션 백 엔드 toocommunicate에 대 한 끝점을 노출합니다. 단,이 끝점에만 표시 됩니다 hello를 사용 하 여 [AMQP] [ lnk-amqp] 프로토콜입니다. hello 메서드 호출 끝점 hello HTTP 프로토콜을 통해 노출 됩니다.
  
  * *장치-클라우드 메시지 받기*. 이 끝점은 [Azure Event Hubs][lnk-event-hubs]와 호환됩니다. 백 엔드 서비스 tooread hello 사용할 수 [장치-클라우드 메시지] [ lnk-d2c] 장치에서 전송 합니다. 또한 toothis 기본 제공 끝점에서 IoT 허브에서 사용자 지정 끝점을 만들 수 있습니다.
  * *클라우드-장치 메시지를 보내고 배달 승인 받기*. 이러한 끝점을 사용 하 여 솔루션 백 엔드 toosend 신뢰할 수 있는 [클라우드-장치 메시지][lnk-c2d], tooreceive hello 해당 배달 또는 만료 승인 하 고 있습니다.
  * *파일 알림을 받습니다*. 이 메시징 끝점이 있습니다 tooreceive 알림을 장치에 파일을 성공적으로 업로드 하는 경우. 
  * *직접 메서드 호출*. 이 끝점을 통해 백 엔드 서비스 tooinvoke 있습니다는 [직접적인 방법] [ lnk-methods] 장치에 있습니다.
  * *작업 모니터링 이벤트를 수신합니다*. 이 끝점 작업을 허용 하면 tooreceive 모니터링 이벤트 허브가 프로그램 IoT tooemit 구성 된 경우 해당 합니다. 자세한 내용은 [IoT Hub 작업 모니터링][lnk-operations-mon]을 참조하세요.

hello [Azure IoT Sdk] [ lnk-sdks] 문서에서는 설명 hello 다양 한 방법으로 tooaccess 이러한 끝점입니다.

Hello를 사용 하는 모든 IoT Hub 끝점 [TLS] [ lnk-tls] 프로토콜과 끝점이 적이 암호화 되지 않은 상태로 보안 되지 않은 채널에 노출 됩니다.

## <a name="custom-endpoints"></a>사용자 지정 끝점

메시지 라우팅에 대 한 끝점으로 프로그램 구독 tooyour IoT 허브 tooact에 기존 Azure 서비스를 연결할 수 있습니다. 이러한 끝점은 서비스 끝점 역할을 하며 메시지 경로에 대한 싱크로 사용됩니다. 장치 쓸 수 없습니다 직접 toohello 추가 끝점. 메시지 경로 대해 자세히 toolearn에 hello 개발자 가이드 항목 참조 [IoT hub와 메시지 송신 및 수신][lnk-devguide-messaging]합니다.

IoT Hub는 현재 추가 끝점으로 Azure 서비스를 수행 하는 hello를 지원 합니다.

* Event Hubs
* Service Bus 큐
* Service Bus 토픽

IoT Hub 메시지 라우팅 toowork toothese 서비스 끝점을 쓰기 권한이 필요합니다. Hello Azure 포털을 통해 끝점을 구성 하는 경우 필요한 권한이 hello 추가 됩니다. 서비스 toosupport hello 예상 처리량을 구성 해야 합니다. 하면 IoT 솔루션을 처음 구성할 때 필요한 toomonitor 추가 끝점 수 고 hello 실제 작업 부하에 대 한 필요한 부분을 수정할 수 있습니다.

메시지가 모든 toohello 가리키는지 여러 경로 일치 하는 경우 동일한 끝점 IoT Hub 제공 메시지 toothat 끝점 한 번만 합니다. 따라서 작업을 수행한 서비스 버스 큐 또는 항목에 tooconfigure 중복을 필요 합니다. 분할된 큐에서 파티션 선호도는 메시지 순서를 보장합니다.

> [!NOTE]
> IoT Hub으로 사용되는 Service Bus 큐 및 토픽에는 **세션** 또는 **중복 검색**이 사용하도록 설정되어 있어서는 안 됩니다. Hello 끝점으로 표시 되는 이러한 옵션 중 하나를 사용할 수 있으면 **연결할 수 없는** hello Azure 포털의에서.

Hello 다양 한 끝점을 추가할 수 있습니다에 hello 제한을 참조 [할당량 및 제한][lnk-devguide-quotas]합니다.

## <a name="field-gateways"></a>현장 게이트웨이

IoT 솔루션에서 *필드 게이트웨이*는 장치와 IoT Hub 끝점 사이에 위치하며 일반적으로 닫기 tooyour 장치는 장치는 hello 장치별으로 지원 되는 프로토콜을 사용 하 여 hello 필드 게이트웨이와 직접 통신 합니다. hello 필드 게이트웨이 tooan IoT 허브에서 지원 되는 프로토콜을 사용 하 여 IoT Hub 끝점을 연결 합니다. 필드 게이트웨이는 전용 하드웨어 장치이거나 사용자 지정 게이트웨이 소프트웨어를 실행하는 저전력 컴퓨터일 수 있습니다.

사용할 수 있습니다 [Azure IoT 가장자리] [ lnk-iot-edge] tooimplement 필드 게이트웨이 합니다. Hello에 여러 장치 로부터의 통신을 멀티플렉싱 하기 등의 기능을 제공 하는 IoT 가장자리 같은 IoT 허브 연결입니다.

## <a name="next-steps"></a>다음 단계

이 IoT Hub 개발자 가이드의 다른 참조 자료:

* [장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어][lnk-devguide-query]
* [할당량 및 제한][lnk-devguide-quotas]
* [IoT Hub MQTT 지원][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
