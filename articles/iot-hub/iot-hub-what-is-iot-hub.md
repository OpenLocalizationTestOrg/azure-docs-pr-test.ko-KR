---
title: "IoT Hub 개요 aaaAzure | Microsoft Docs"
description: "Hello Azure IoT 허브 서비스의 개요: IoT Hub, 장치 연결, 인터넷 가지 통신 패턴, 게이트웨이 및 hello 서비스 기반 통신 패턴의 란"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Hello Azure IoT 허브 서비스의 개요

IoT Hub tooAzure를 시작 합니다. 이 문서에서는 Azure IoT 허브에 대해 간략하게 설명 하 고이 서비스 tooimplement 인터넷 IoT (사물) 솔루션을 사용 해야 하는 이유를 설명 합니다. Azure IoT Hub는 수백만의 IoT 장치와 솔루션 백 엔드 간에서 안정적이고 안전한 양방향 통신이 가능하도록 완전히 관리되는 서비스입니다. Azure IoT Hub

* 단방향 메시징, 파일 전송 및 요청-회신 메서드를 포함하여 여러 장치-클라우드 및 클라우드-장치 간 통신 옵션을 제공합니다.
* 기본 제공 선언적 메시지 라우팅 tooother Azure 서비스를 제공합니다.
* 장치 메타데이터와 동기화된 상태 정보에 대한 쿼리 가능한 저장소를 제공합니다.
* 장치 단위 보안 키 또는 X.509 인증서를 사용하여 통신 및 액세스 제어를 보호합니다.
* 장치 연결 및 장치 ID 관리 이벤트에 대한 포괄적인 모니터링을 제공합니다.
* Hello 가장 인기 있는 언어 및 플랫폼에 대 한 장치 라이브러리를 포함합니다.

hello 문서 [비교의 IoT Hub 및 이벤트 허브] [ lnk-compare] hello 이들 두 서비스 간의 주요 차이점에 설명 하 고 IoT 허브를 사용 하 여 IoT 솔루션에서의 hello 이점을 강조 표시 합니다.

어떻게 Azure와 IoT Hub를 보호 하면 IoT 솔루션에 대 한 자세한 내용은 참조 하십시오. [hello 접지에서 사물 인터넷 보안][lnk-security-ground-up]합니다.

![사물 인터넷 솔루션에서 클라우드 게이트웨이인 Azure IoT Hub][img-architecture]

> [!NOTE]
> IoT 아키텍처는 대 한 자세한 내용은 참조 hello [Microsoft Azure IoT 참조 아키텍처][lnk-refarch]합니다.

## <a name="iot-device-connectivity-challenges"></a>IoT 장치 연결 과제

IoT Hub 및 hello 장치 라이브러리 도움말 방법의 toomeet hello 과제 tooreliably 장치 toohello 솔루션에 대 한 백 엔드를 안전 하 게 연결 합니다. IoT 장치:

* 운영자가 없는 내장 시스템인 경우가 많습니다.
* 물리적 액세스에 많은 비용이 드는 원격 위치에 있을 수 있습니다.
* Hello 솔루션 백 엔드를 통해 도달할 수 있습니다.
* 전원 및 리소스 처리 제한이 있을 수 있습니다.
* 일시적이거나 느리거나 비용이 많이 드는 네트워크 연결이 있을 수 있습니다.
* Toouse 소유, 사용자 지정 또는 업계 관련 응용 프로그램 프로토콜을 지정 해야 합니다.
* 널리 사용되는 다양한 하드웨어 및 소프트웨어 플랫폼을 사용하여 만들 수 있습니다.

또한 toohello 위의 요구 사항은, 모든 IoT 솔루션도 배달 해야 배율, 보안 및 안정성 합니다. hello 결과 연결 요구 사항 집합이 하드 및 시간 소요 정도가 tooimplement 웹 컨테이너 및 메시징 브로커과 같은 기존 기술을 사용 하는 경우.

## <a name="why-use-azure-iot-hub"></a>Azure IoT Hub를 사용하는 이유

또한 tooa 풍부한 집합이 [장치-클라우드] [ lnk-d2c-guidance] 및 [클라우드-장치] [ lnk-c2d-guidance] 통신 옵션, 메시지를 포함 하 여 파일 전송 및 요청-회신 메서드, Azure IoT Hub 주소 hello 같은 방법으로 다음의 장치 연결 과제 hello:

* **장치 쌍**. [장치 쌍][lnk-twins]을 사용하여 장치 메타데이터 및 상태 정보를 저장, 동기화 및 쿼리할 수 있습니다. 장치 쌍은 장치의 상태 정보(메타데이터, 상태 및 조건)를 저장하는 JSON 문서입니다. IoT Hub tooIoT 허브에 연결 해야 하는 각 장치에 대 한 장치로 이중을 유지 합니다.

* **장치별 인증 및 보안 연결**. 고유의 각 장치를 프로 비전 할 수 [보안 키] [ lnk-devguide-security] tooenable 것 tooconnect tooIoT 허브입니다. hello [IoT Hub id 레지스트리에] [ lnk-devguide-identityregistry] 솔루션에서 장치 id 및 키를 저장 합니다. 솔루션 백 엔드 tooallow 개별 장치를 추가 하거나 목록 tooenable 완벽 하 게 제어 장치 액세스를 거부할 수 있습니다.

* **경로 장치-클라우드 메시지 선언적 규칙에 따라 tooAzure 서비스**합니다. IoT Hub 있습니다 toodefine 경로에 따라 메시지를 라우팅 규칙 toocontrol 허브에서 장치-클라우드 메시지를 전송 하는 위치 수 있습니다. 라우팅 규칙 있습니다 toowrite 모든 코드가 필요 하지 않은 및 사용자 지정 후 수집 메시지 디스패처의 hello 수행 될 수 있습니다.

* **장치 연결 작업에 대한 모니터링**. 장치 ID 관리 작업 및 장치 연결 이벤트에 대한 자세한 작업 로그를 받을 수 있습니다. 이 모니터링 기능 tooconnect 잘못 된 자격 증명을 사용 하는 장치 메시지 너무 자주 보내거나 거부 모든 클라우드-장치 메시지와 같은 하면 IoT 솔루션 tooidentify 연결 문제를 수 있습니다.

* **광범위한 장치 라이브러리 집합**. [Azure IoT 장치 SDK][lnk-device-sdks]는 사용 가능하며 다양한 언어 및 플랫폼(여러 Linux 배포판, Windows 및 실시간 운영 체제에 대한 C)에 대해 지원됩니다. 또한 Azure IoT 장치 SDK에서는 C#, Java 및 JavaScript와 같은 관리된 언어를 지원합니다.

* **IoT 프로토콜 및 확장성**. 솔루션 hello 장치 라이브러리를 사용할 수 없는 경우 IoT Hub 장치 toonatively 사용 하 여 hello MQTT v3.1.1, HTTP 1.1 또는 AMQP 1.0 프로토콜을 사용 하는 공용 프로토콜을 노출 합니다. 사용자 지정 프로토콜에 대 한 IoT Hub toosupport를 확장할 수 있습니다.

  * 필드 게이트웨이를 만드는 [Azure IoT 가장자리] [ lnk-iot-edge] hello 프로토콜 이해 IoT 허브에서의 사용자 지정 프로토콜 tooone 사용자를 변환 하 합니다.
  * 사용자 지정 hello [Azure IoT 프로토콜 게이트웨이][protocol-gateway], hello 클라우드에서 실행 되는 오픈 소스 구성 요소입니다.

* **확장**. Azure IoT Hub toomillions 동시에 연결 된 장치 및 초당 이벤트의 수백만 조정합니다.

## <a name="gateways"></a>게이트웨이

IoT 솔루션에서 게이트웨이 일반적으로 하나는 [프로토콜 게이트웨이] [ lnk-iotedge] hello 클라우드에 배포 된 또는 [필드 게이트웨이] [ lnk-field-gateway] 즉 장치 로컬 배포. 프로토콜 게이트웨이 MQTT tooAMQP 예의 프로토콜 변환을 수행합니다. 필드 게이트웨이 수 hello 가장자리에 분석을 실행할 tooreduce 대기 시간이 중요 한 결정을 내릴, 장치 관리 서비스를 제공, 보안 및 개인 정보 보호 제약 조건 적용 및 프로토콜 변환을 수행할 수도 있습니다. 두 유형의 게이트웨이는 장치와 loT Hub 간의 중개자 역할을 합니다.

현장 게이트웨이는 일반적으로 솔루션에서 액세스 및 정보 흐름을 관리하는 실제 역할을 수행하므로 단순한 트래픽 라우팅 장치(예: 네트워크 주소 변환 장치 또는 방화벽)와는 다릅니다.

솔루션에는 프로토콜과 필드 게이트웨이가 모두 포함될 수 있습니다.

## <a name="how-does-iot-hub-work"></a>IoT Hub는 어떻게 작동하나요?

Azure IoT Hub 구현 hello [서비스 기반 통신] [ lnk-service-assisted-pattern] 패턴 toomediate hello 상호 작용 하는 장치 및 솔루션 간의 백 엔드 합니다. hello 서비스 기반 통신의 목적은 IoT Hub 및 신뢰할 수 없는 물리적 공간에 배포 되는 특수 한 용도의 장치 등의 제어 시스템 간의 tooestablish 신뢰할 수 있는, 양방향 통신 경로입니다. hello 패턴 hello를 원칙에 따라 다릅니다.

* 보안이 다른 모든 기능보다 우선합니다.

* 장치는 요청하지 않은 네트워크 정보를 허용하지 않습니다. 장치에서 아웃바운드 전용 방식으로 모든 연결 및 경로를 설정합니다. 장치 tooreceive hello 솔루션 백 엔드를 명령에 대 한 hello 장치에 대 한 모든 보류 중인 명령 tooprocess 연결 toocheck를 정기적으로 시작 해야 합니다.

* 장치 연결 해야 tooor IoT Hub와 같은, 겹치기는 경로 toowell 알려진 서비스를 설정 합니다.

* 장치 및 서비스 간의 또는 장치와 게이트웨이 hello 통신 경로 hello 응용 프로그램 프로토콜 계층에서 보호 됩니다.

* 시스템 수준 권한 부여 및 인증은 장치 ID를 기반으로 하며 액세스 자격 증명 및 권한은 즉시 취소 가능합니다.

* 산발적으로 장애가 due toopower 또는 연결 문제를 연결 하는 장치에 대 한 양방향 통신 명령 및 장치 알림 장치 tooreceive 연결 될 때까지 보유 하 여 촉진 됩니다 하 합니다. IoT Hub에 장치 관련 큐 보내는 hello 명령에 대 한 유지 관리 합니다.

* 응용 프로그램 페이로드 데이터 게이트웨이 tooa 특정 서비스를 통해 보호 된 전송에 대해 개별적으로 보호 됩니다.

hello 모바일 업계가 사용 hello 서비스 기반 통신 패턴에서 눈금 막대 한 tooimplement 푸시 알림 서비스와 같은 [Windows 푸시 알림 서비스][lnk-wns], [Google Cloud Messaging][lnk-google-messaging], 및 [Apple 푸시 알림 서비스][lnk-apple-push]합니다.

IoT Hub는 ExpressRoute의 공용 피어링 경로를 통해 지원됩니다.

## <a name="next-steps"></a>다음 단계

toolearn toosend 장치에서 메시지 방법과 tooconfigure 메시지 라우팅하 하는 방법 뿐만 아니라 IoT 허브에서 받을 참조 [IoT Hub와 메시지를 주고받을][lnk-send-messages]합니다.

toolearn IoT Hub tooremotely 있습니다 관리, 구성 및 장치에 업데이트에 대 한 표준 기반 장치 관리를 사용 하면 참조 [IoT Hub와 장치 관리의 개요][lnk-device-management]합니다.

tooimplement 클라이언트 장치 하드웨어 플랫폼 및 운영 체제의 다양 한 응용 프로그램, Azure IoT 장치 hello Sdk를 사용할 수 있습니다. hello 장치 Sdk 원격 분석 tooan IoT 허브 및 수신 클라우드-장치 메시지를 보낼 수 있는 라이브러리를 포함 합니다. Hello 장치 Sdk를 사용 하면 IoT Hub와 다양 한 네트워크 프로토콜 toocommunicate에서 선택할 수 있습니다. toolearn hello을 더 참조 [장치 Sdk에 대 한 정보][lnk-device-sdks]합니다.

일부 코드를 작성 하 고 일부 샘플 실행을 시작 하는 tooget 참조 hello [IoT 허브 시작] [ lnk-get-started] 자습서입니다.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "서비스 지원 통신, Clemens vasters의 블로그 게시물"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
