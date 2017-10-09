---
title: "IoT Hub 클라우드-장치 aaaAzure 옵션 | Microsoft Docs"
description: "개발자 가이드-toouse 메서드, 장치로 이중 원하는 속성 또는 클라우드-장치 통신에 대 한 클라우드-장치 메시지를 전송 하는 경우에 대 한 지침입니다."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>클라우드-장치 통신 지침
IoT Hub 장치 앱 tooexpose 기능 tooa 백 엔드 응용 프로그램에 대 한 세 가지 옵션을 제공합니다.

* [메서드를 직접] [ lnk-methods] hello 결과의 즉시 확인 해야 하는 통신에 대 한 합니다. 대화형 장치 제어(예: 선풍기 켜기)에 대해 직접 메서드를 자주 사용합니다.
* [로 이중 원하는 속성의] [ lnk-twins] 장기 실행 명령을 의도 tooput hello 장치 특정를 원하는 상태에 대 한 합니다. 예를 들어 hello 원격 분석 보내기 간격 too30 (분)을 설정 합니다.
* [클라우드-장치 메시지] [ lnk-c2d] 단방향 알림 toohello 장치 응용 프로그램에 대 한 합니다.

여기의 hello 자세히 비교 하려면 다양 한 클라우드-장치 통신 옵션입니다.

|  | 직접 메서드 | 쌍의 desired 속성 | 클라우드-장치 메시지 |
| ---- | ------- | ---------- | ---- |
| 시나리오 | 즉각적인 확인이 필요한 명령(예: 팬 작동) | 장기 실행 명령을 특정을 원하는 상태로 tooput hello 장치를 위한 것입니다. 예를 들어 hello 원격 분석 보내기 간격 too30 (분)을 설정 합니다. | 단방향 알림 toohello 장치는 응용 프로그램. |
| 데이터 흐름 | 양방향. hello 장치 앱 toohello 메서드를 즉시 응답할 수 있습니다. hello 솔루션 백 엔드 컨텍스트에 hello 결과 받는 toohello 요청 합니다. | 단방향. hello 장치 응용 프로그램에는 hello 속성 변경 알림을 받습니다. | 단방향. hello 메시지를 수신 하는 hello 장치 앱
| 내구성 | 연결이 끊긴 장치는 연결되지 않습니다. hello 솔루션 백 엔드에서 해당 hello 장치가 연결 되지 않은 알림이 전송 됩니다. | 속성 값은 hello 장치로 이중에서 유지 됩니다. 다음에 다시 연결할 때 장치에서 이 알림을 읽습니다. 속성 값은 검색할 수 있는 hello [IoT Hub 쿼리 언어][lnk-query]합니다. | Too48 시간에 대 한 IoT Hub에서 메시지를 보존할 수 있습니다. |
| 대상 | **deviceId**를 사용하는 단일 장치 또는 [jobs][lnk-jobs]를 사용하는 여러 장치 | **deviceId**를 사용하는 단일 장치 또는 [jobs][lnk-jobs]를 사용하는 여러 장치 | **deviceId**를 사용하는 단일 장치 |
| 크기 | too8KB 요청과 8KB 응답 합니다. | 최대 desired 속성 크기는 8KB입니다. | Too64KB 메시지입니다. |
| Frequency(빈도) | 높음. 자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요. | 중간. 자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요. | 낮음. 자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요. |
| 프로토콜 | 현재 MQTT를 사용할 때만 사용할 수 있습니다. | 현재 MQTT를 사용할 때만 사용할 수 있습니다. | 모든 프로토콜에서 사용할 수 있습니다. HTTP를 사용할 경우 장치에서 폴링해야 합니다. |

Toouse hello 자습서 뒤의 메서드, 원하는 속성 및 클라우드-장치 메시지를 직접 방법에 대해 설명 합니다.

* [직접 메서드 사용][lnk-methods-tutorial]
* [원하는 속성 tooconfigure 장치를 사용 하 여][lnk-twin-properties]장치로 이중 속성; 필요한의 대 한 
* [클라우드-장치 메시지 보내기][lnk-c2d-tutorial]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
