---
title: "aaaAzure IoT 프로토콜 게이트웨이 | Microsoft Docs"
description: "어떻게 toouse Azure IoT 프로토콜 게이트웨이 tooextend IoT 허브 특성 및 고유 하 게 IoT Hub에서 지원 되지 않습니다 프로토콜을 사용 하 여 프로토콜 지원 tooenable 장치 tooconnect tooyour 허브 사용 합니다."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# IoT Hub에 대한 추가 프로토콜 지원
기본적으로 azure IoT Hub hello MQTT, AMQP 및 HTTP 프로토콜을 통한 통신을 지원 합니다. 경우에 따라 장치 또는 필드 게이트웨이 이러한 표준 프로토콜 중 하나는 수 toouse 수 있으며 프로토콜 조정 해야 합니다. 이러한 경우 사용자 지정 게이트웨이를 사용할 수 있습니다. 사용자 지정 게이트웨이 메워 hello 트래픽 tooand IoT 허브에서 IoT Hub 끝점에 대 한 프로토콜 조정을 가능 합니다. Hello를 사용할 수 있습니다 [Azure IoT 프로토콜 게이트웨이](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) IoT 허브에 대 한 사용자 지정 게이트웨이 tooenable 프로토콜 조정으로 합니다.

## Azure IoT 프로토콜 게이트웨이
hello Azure IoT 프로토콜 게이트웨이 확장성이 뛰어난, IoT Hub와 양방향 장치 통신을 위해 디자인 된 프로토콜 적응 위한 프레임 워크입니다. hello 프로토콜 게이트웨이 특정 프로토콜을 통한 장치 연결을 수락 하는 통과 구성 요소입니다. AMQP 1.0을 통해 hello 트래픽 tooIoT 허브를 연결 합니다. hello Azure IoT 프로토콜 게이트웨이 다양 한 프로토콜 및 프로토콜 버전에 대 한 지원을 추가 하기 위한 오픈 소스 소프트웨어 프로젝트 tooprovide 유연성으로 사용할 수 있습니다.

Azure Service Fabric, Azure 클라우드 서비스 작업자 역할 또는 Windows 가상 컴퓨터를 사용 하 여 확장성이 뛰어난 방식으로 Azure의 hello 프로토콜 게이트웨이 배포할 수 있습니다. 또한 필드 게이트웨이 등의 온-프레미스 환경에서는 hello 프로토콜 게이트웨이 배포할 수 있습니다.

hello Azure IoT 프로토콜 게이트웨이 있습니다 toocustomize hello MQTT 프로토콜 동작이 필요한 경우 사용 하도록 설정 하는 MQTT 프로토콜 어댑터를 포함 합니다. IoT Hub에 hello MQTT v3.1.1 프로토콜에 대 한 기본 제공 지원을 제공 하므로 사용자 지정 프로토콜 또는 추가 기능에 대 한 특정 요구 사항이 필요한 경우 hello MQTT 프로토콜 어댑터를 사용 하 여를 고려해 야 합니다.

hello MQTT 어댑터에는 또한 다른 프로토콜에 대 한 프로토콜 어댑터를 작성 하기 위한 프로그래밍 모델을 hello 보여 줍니다. 또한 hello Azure IoT 프로토콜 게이트웨이 프로그래밍 모델에서는 tooplug에 대 한 사용자 지정 구성 요소에서 특수화 된 사용자 지정 인증, 메시지 변환, 압축/압축 풀기 또는 트래픽 암호화/암호 해독 같은 처리 hello 장치와 IoT 허브입니다.

유연성을 hello 프로토콜 게이트웨이와 MQTT 구현 오픈 소스 소프트웨어 프로젝트에 제공 됩니다. 이렇게 하면 필요에 따라 toocustomize hello 구현이 있습니다.

## 다음 단계
toolearn hello Azure IoT 프로토콜 게이트웨이에 대 한 자세한 방법과 toouse 하면 IoT 솔루션의 일부로 배포를 참조 하세요.

* [GitHub에서 Azure IoT 프로토콜 게이트웨이 리포지토리](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Azure IoT 프로토콜 게이트웨이 개발자 가이드](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

IoT Hub 배포 계획에 대해 자세히 toolearn 참조:

* [Event Hubs와 비교][lnk-compare]
* [크기 조정, HA 및 DR][lnk-scaling]
* [IoT Hub 개발자 가이드][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
