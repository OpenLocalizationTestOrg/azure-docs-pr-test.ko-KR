---
title: "Azure IoT 가장자리의 aaaOverview | Microsoft Docs"
description: "Hello 아키텍처의 주요 개념 Azure IoT 가장자리 게이트웨이, 모듈 및 브로커 등을 설명합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Azure IoT Edge 아키텍처 개념

모든 샘플 코드를 검사 하거나 IoT 가장자리를 사용 하 여 사용자 고유의 필드 게이트웨이 만들 하기 전에 IoT 가장자리의 hello 아키텍처를 지 원하는 hello 주요 개념을 이해 해야 합니다.

## <a name="iot-edge-modules"></a>IoT Edge 모듈

*IoT Edge 모듈*을 만들고 조합하여 Azure IoT Edge를 통해 게이트웨이를 빌드합니다. 모듈에 사용 하 여 *메시지* tooexchange 서로 데이터를 합니다. 메시지를 수신 하에 작업을 수행할 필요에 따라 새 메시지로 변환를 다음 다른 모듈 tooprocess에 대 한 게시 하는 모듈입니다. 일부 모듈은 새 메시지만 생성하고, 들어오는 메시지를 전혀 처리하지 않습니다. 모듈의 체인 해당 파이프라인의 한 지점 hello 데이터에 변환을 수행 하는 각 모듈 사용 데이터 처리 파이프라인을 만듭니다.

![Azure IoT Edge로 만든 게이트웨이의 모듈 체인][1]

IoT 가장자리 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.

* 일반 게이트웨이 기능을 수행하는 미리 작성된 모듈.
* 개발자는 hello 인터페이스 toowrite 사용자 지정 모듈을 사용할 수 있습니다.
* 인프라 필요한 toodeploy hello 하 고 모듈의 집합을 실행 합니다.

hello SDK를 사용 하면 주는 추상화 계층 toobuild 게이트웨이 toorun 다양 한 운영 체제 및 플랫폼에서 제공 합니다.

![Azure IoT Edge 추상화 계층][2]

## <a name="messages"></a>메시지

메시지 tooeach 다른 방법 게이트웨이 작동 하는 편리한 방법을 tooconceptualize은 전달 하는 모듈에 대 한 생각이 있지만 반영 하지 않습니다 정확 하 게 수행 되는 작업. IoT 가장자리 모듈 서로 브로커 toocommunicate를 사용합니다. 모듈 (예: 버스, 또는 게시/구독 메시징 패턴을 사용 하 여) 메시지 toohello 브로커를 게시 한 hello broker 경로 hello 메시지 toohello 모듈 연결 된 tooit 하 게 하 합니다.

모듈 hello를 사용 하 여 **Broker_Publish** toopublish 메시지 toohello 브로커 작동 합니다. hello 브로커는 콜백 함수를 호출 하 여 메시지 tooa 모듈을 제공 합니다. 메시지는 키/값 속성 및 메모리 블록으로 전달되는 콘텐츠의 집합으로 구성됩니다.

![hello Azure IoT 가장자리의 Broker의 hello 역할][3]

## <a name="message-routing-and-filtering"></a>메시지 라우팅 및 필터링

두 가지가 toodirect 메시지 toohello 올바른 IoT 가장자리 모듈:

* 링크의 집합을 전달할 수 있습니다 hello 브로커 hello 원본 및 싱크 각 모듈에 대 한 알 수 있도록 toohello broker 전달 수 있습니다.
* 모듈은 hello 메시지의 hello 속성에서 필터링 할 수 있습니다.

모듈은 hello 메시지 위한 하는 경우에 메시지에 작동 해야 합니다. 링크 및 메시지 필터링은 메시지 파이프라인을 효과적으로 만듭니다.

## <a name="next-steps"></a>다음 단계

toosee 실행할 수 있습니다 이러한 개념 샘플에 적용 된 참조 [Azure IoT 가장자리 탐색 아키텍처][lnk-hello-world]합니다.

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md