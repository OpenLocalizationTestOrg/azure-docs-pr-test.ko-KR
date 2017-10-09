---
title: "Azure IoT 허브에 대 한 aaaDeveloper 가이드 | Microsoft Docs"
description: "hello Azure IoT 허브 개발자 가이드에는 끝점, 보안, hello id 레지스트리에, 장치 관리, 직접 메서드, 장치 트윈스, 파일 업로드, 작업, hello IoT Hub 쿼리 언어 및 메시징에 대해 포함 되어 있습니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Azure IoT Hub 개발자 가이드

Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.

Azure IoT Hub는 다음을 제공합니다.

* 장치 단위 보안 자격 증명 및 액세스 제어를 사용하여 보안 통신을 제공합니다.
* 다수의 장치-클라우드 및 클라우드-장치 하이퍼스케일(hyper-scale) 통신 옵션.
* 장치별 상태 정보 및 메타데이터를 쿼리할 수 있는 저장소
* Hello 가장 인기 있는 언어 및 플랫폼에 대 한 장치 라이브러리와 쉽게 장치 연결 합니다.

이 IoT 허브 개발자 가이드 문서 다음 hello를 포함 되어 있습니다.

* [장치-클라우드 통신 지침][lnk-d2c-guidance] - 장치-클라우드 메시지, 장치 쌍의 reported 속성, 파일 업로드 중에 하나를 선택하도록 도와줍니다.
* [클라우드-장치 통신 지침][lnk-c2d-guidance] - 직접 메서드, 장치 쌍의 desired 속성, 클라우드-장치 메시지 중 하나를 선택할 수 있도록 도움을 줍니다.
* [장치-클라우드 및 클라우드-장치 IoT Hub와 메시징] [ devguide-messaging] hello 메시징 기능 (장치-클라우드 및 클라우드-장치)에 IoT Hub 노출에 대해 설명 합니다.
  * [장치-클라우드 메시지 tooIoT 허브 보내기][devguide-messages-d2c]합니다.
  * [Hello 기본 제공 끝점에서 장치-클라우드 메시지를 읽은][devguide-builtin]합니다.
  * [장치-클라우드 메시지에 대한 사용자 지정 끝점 및 라우팅 규칙 사용][devguide-custom]
  * [IoT Hub에서 클라우드-장치 메시지 보내기][devguide-messages-c2d]
  * [IoT Hub 메시지 만들기 및 읽기][devguide-format]
* [장치에서 파일 업로드][devguide-upload] - 장치에서 파일을 업로드하는 방법을 설명합니다. hello 문서에는 알림을 hello 업로드 프로세스를 보낼 수 hello 같은 항목에 대 한 정보도 포함 됩니다.
* [IoT Hub에서 장치 ID 관리][devguide-identities] - 각 IoT Hub의 ID 레지스트리에 어떤 정보가 저장되고 이것을 어떻게 액세스하고 수정할 수 있는지 설명합니다.
* [액세스 tooIoT 허브 제어] [ devguide-security] 기능에 설명 hello 보안 사용 되는 모델 toogrant 액세스 tooIoT 허브 장치와 클라우드 구성 요소에 대 한 합니다. hello 문서에는 토큰 및 X.509 인증서 및 hello 사용 권한 부여할 수의 세부 정보를 사용 하는 방법에 대 한 정보가 포함 됩니다.
* [장치 트윈스 toosynchronize 상태 및 구성을 사용 하 여] [ devguide-device-twins] hello 설명 *장치로 이중* 장치와 해당 장치를 동기화 하는 등 노출 하는 개념 및 hello 기능 로 이중 합니다. hello 문서 장치로 이중에 저장 된 hello 데이터에 대 한 정보를 제공 합니다.
* [장치에서 직접 메서드를 호출] [ devguide-directmethods] hello 수명 주기는 직접적인 방법 tooinvoke 메서드 백 엔드 응용 프로그램 및 핸들 hello에서 장치에 장치에서 메서드를 지시 하는 방법에 대 한 정보를 설명 합니다.
* [여러 장치에서 작업 예약][devguide-jobs] - 여러 장치에서 작업을 예약하는 방법을 설명합니다. hello 문서에서는 설명 방법을 toosubmit 작업 하는 장치로 이중을 사용 하 여 장치 업데이트 직접 메서드를 실행 하 고 작업을 수행 합니다. 또한 tooquery 작업의 상태를 hello 하는 방법을 설명 합니다.
* [참조-통신 프로토콜 선택] [ devguide-protocol] hello 통신 프로토콜 IoT Hub 장치 통신에 대 한 지원 및 목록 hello이 열려 있어야 하는 포트에 설명 합니다.
* [IoT Hub 끝점 참조-] [ devguide-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다. hello 대해서도 설명 하 고 IoT 허브에서 추가 끝점을 만들 수 있습니다 방법 toouse 필드 게이트웨이 tooenable 장치 연결 tooyour IoT Hub 비표준 시나리오에서 끝점입니다.
* [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어 참조-] [ devguide-query] 장치 트윈스 및 작업에 대 한 허브에서 tooretrieve 정보 수 있는 해당 IoT Hub 쿼리 언어에 설명 합니다.
* [참조-할당량 및 제한] [ devguide-quotas] hello IoT 허브 서비스와 조정 된 할당량을 초과 하면 toosee 기대할 수 있는 동작 hello에서 설정 된 hello 할당량 요약 되어 있습니다.
* [참조-가격] [ devguide-pricing] 다른 Sku 및 IoT Hub 및 IoT Hub에서 IoT Hub에 다양 한 기능으로 요금이 부과 되며 hello 메시지 하는 방법을 대 한 세부 정보에 대 한 가격 책정에 일반 정보를 제공 합니다.
* [참조-장치 및 서비스 Sdk] [ devguide-sdks] 목록 hello Azure IoT Sdk toodevelop를 사용할 수 있습니다 IoT hub와 상호 작용 하는 장치 및 서비스 둘 다 응용 프로그램입니다. hello 문서 링크 tooonline API 설명서를 제공합니다.
* [참조-IoT 허브 MQTT 지원] [ devguide-mqtt] IoT Hub hello MQTT 프로토콜을 지 원하는 방법에 대 한 자세한 정보를 제공 합니다. hello 문서 hello MQTT 프로토콜 기본 제공 toohello Azure IoT Sdk에 대 한 hello 지원에 설명 하 고 직접 hello MQTT 프로토콜을 사용 하는 방법에 대 한 정보를 제공 합니다.
* [용어집][devguide-glossary] - 일반적인 IoT Hub 관련 용어 목록입니다.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
