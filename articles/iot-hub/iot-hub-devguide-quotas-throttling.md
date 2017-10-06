---
title: "aaaUnderstand Azure IoT Hub 할당량 및 제한 | Microsoft Docs"
description: "개발자 가이드-설명은 tooIoT 허브 및 hello 적용 되는 hello 할당량 제한 동작이 필요 합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>참조 - IoT Hub 할당량 및 제한

## <a name="quotas-and-throttling"></a>할당량 및 제한
각 Azure 구독은 IoT Hub 최대 10개와 무료 허브 최대 1개를 가질 수 있습니다.

각 IoT Hub는 특정 SKU에서 특정한 단위 수로 프로비전됩니다. 자세한 내용은 [Azure IoT Hub 가격 책정][lnk-pricing]을 참조하세요. hello SKU 및 단위 수가 결정 보낼 수 있는 메시지의 최대 일일 할당량 hello 합니다.

또한 hello SKU 조절 제한 IoT 허브에서 모든 작업을 적용 하는 hello를 결정 합니다.

## <a name="operation-throttles"></a>작업 제한
작업 스로틀은 hello 분 범위에 적용 되 고 있는 비율 제한이 tooavoid 남용을 위한 것입니다. IoT Hub tooavoid 가능 하면 항상 오류를 반환 하지만 hello 스로틀 너무 오랫동안 위반 되 면 예외를 반환 시작.

다음 테이블에서는 hello hello 스로틀을 적용 합니다. 값은 tooan 개별 허브를 참조합니다.

| 제한 | 무료 및 S1 허브 | S2 허브 | S3 허브 | 
| -------- | ------- | ------- | ------- |
| ID 레지스트리 작업(만들기, 검색, 나열, 업데이트 및 삭제) | 1.67/초/단위(100/분/단위) | 1.67/초/단위(100/분/단위) | 83.33/초/단위(5000/분/단위) |
| 장치 연결 | 최대 100/초 또는 12/초/단위 <br/> 예를 들어 S1 단위가 2개인 경우 2\*12 = 초당 24개에 해당합니다. 하지만 단위 전체의 연결 수는 초당 100개 이상이어야 합니다. S1 단위가 9개인 경우 단위 전체에 대한 값은 108/초(9\*12)입니다. | 120/초/단위 | 6000/초/단위 |
| 장치->클라우드 보내기 | 최대 100/초 또는 12/초/단위 <br/> 예를 들어 S1 단위가 2개인 경우 2\*12 = 초당 24개에 해당합니다. 하지만 단위 전체의 연결 수는 초당 100개 이상이어야 합니다. S1 단위가 9개인 경우 단위 전체에 대한 값은 108/초(9\*12)입니다. | 120/초/단위 | 6000/초/단위 |
| 클라우드-장치 보내기 | 1.67/초/단위(100/분/단위) | 1.67/초/단위(100/분/단위) | 83.33/초/단위(5000/분/단위) |
| 클라우드-장치 받기 <br/> (장치에서 HTTP를 사용하는 경우에만)| 16.67/초/단위(1000/분/단위) | 16.67/초/단위(1000/분/단위) | 833.33/초/단위(50000/분/단위) |
| 파일 업로드 | 1.67 파일 업로드 알림/초/단위(100/분/단위) | 1.67 파일 업로드 알림/초/단위(100/분/단위) | 83.33 파일 업로드 알림/초/단위(5000/분/단위) |
| 직접 메서드 | 20/초/단위 | 60/초/단위 | 3000/초/단위 | 
| 장치 쌍 읽기 | 10/초 | 최대 10/초 또는 1/초/단위 | 50/초/단위 |
| 장치 쌍 업데이트 | 10/초 | 최대 10/초 또는 1/초/단위 | 50/초/단위 |
| 작업 연산 <br/> (만들기, 업데이트, 나열, 삭제) | 1.67/초/단위(100/분/단위) | 1.67/초/단위(100/분/단위) | 83.33/초/단위(5000/분/단위) |
| 장치 단위 작업 연산 처리량 | 10/초 | 최대 10/초 또는 1/초/단위 | 50/초/단위 |

Hello 중요 tooclarify는 *장치 연결* 스로틀을 새 장치 연결을 설정할 수 있는 IoT hub hello 속도 제어 합니다. hello *장치 연결* 스로틀 hello 최대 수의 동시에 연결 된 장치를 관리 하지 않습니다. hello 스로틀 hello hello IoT 허브에 대 한 프로 비전 되는 단위 수에 따라 달라 집니다.

예를 들어 S1 단위 하나를 구매하는 경우 초당 연결 제한은 100개입니다. 따라서 tooconnect 100, 000 장치 1000 초 (약 16 분) 이상 필요 합니다. 그러나 ID 레지스트리에 등록한 수만큼의 장치를 동시에 연결할 수 있습니다.

자세한 내용은 IoT 허브에 대 한 hello 블로그 게시물을 참조 조정 동작을 [IoT Hub를 제한 하 고][lnk-throttle-blog]합니다.

> [!NOTE]
> 지정된 된 시간에는 가능한 tooincrease 할당량 제한 hello IoT 허브에서 프로 비전 된 단위 수를 늘려 스로틀 또는 합니다.
> 
> [!IMPORTANT]
> ID 레지스트리 작업은 장치 관리 및 프로비전 시나리오에서 런타임에 사용하기 위한 것입니다. 많은 수의 장치 ID 읽기 또는 업데이트는 [가져오기 및 내보내기 작업][lnk-importexport]을 통해 지원됩니다.
> 
> 

## <a name="other-limits"></a>기타 제한

IoT Hub에는 다른 작업 제한도 적용됩니다.

| 작업 | 제한 |
| --------- | ----- |
| 파일 업로드 URI | 10000 SAS URI는 한 번에 저장소 계정에 대해 나올 수 있습니다. <br/> 10 SAS URI/장치는 한 번에 나올 수 있습니다. |
| 작업 | 작업 기록의 too30 일 수를 보관합니다 <br/> 최대 동시 작업은 1개(무료 및 S1의 경우, 5(S2의 경우), 10(S3의 경우)입니다. |
| 추가 끝점 | 유료 SKU 허브에는 10개, 무료 SKU 허브에는 하나의 추가 끝점이 있을 수 있습니다. |
| 메시지 라우팅 규칙 | 유료 SKU 허브에는 100개, 무료 SKU 허브에는 5개의 라우팅 규칙이 있을 수 있습니다. |
| 장치-클라우드 메시징 | 최대 메시지 크기 256KB |
| 클라우드-장치 메시징 | 최대 메시지 크기 64KB |
| 클라우드-장치 메시징 | 배달 보류 중인 최대 메시지 수는 50개 |

> [!NOTE]
> 현재, 최대 수를 hello tooa 단일 IoT 허브는 500, 000의 장치에 연결할 수 있습니다. 이 제한을 tooincrease을 원하는 경우 문의 [Microsoft 지원](https://azure.microsoft.com/support/options/)합니다.

## <a name="latency"></a>대기 시간
IoT Hub 모든 작업에 대 한 짧은 대기 시간 tooprovide 노력 합니다. 그러나 toonetwork 조건 및 예측할 수 없는 기타 요인 때문 최대 대기 시간을 보장할 수 없습니다 것입니다. 솔루션을 설계할 때 다음을 수행해야 합니다.

* IoT Hub 작업의 hello 최대 대기 시간에 대 한 가정 하 하지 마십시오.
* IoT 허브 hello Azure 지역 가장 가까운 tooyour 장치를 프로 비전 합니다.
* Hello 장치 또는 게이트웨이 닫기 toohello 장치에서 Azure IoT 가장자리 tooperform 대기 시간에 민감한 작업을 사용 하는 것이 좋습니다.

여러 IoT Hub 단위는 앞에서 설명한 대로 제한에 영향을 주지만 추가 대기 시간을 주거나 보장하지 않습니다.
작업 대기 시간에 예기치 않은 증가가 발생한 경우 [Microsoft 지원](https://azure.microsoft.com/support/options/)에 문의하세요.

## <a name="next-steps"></a>다음 단계
이 IoT Hub 개발자 가이드의 다른 참조 자료:

* [IoT Hub 끝점][lnk-devguide-endpoints]
* [장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어][lnk-devguide-query]
* [IoT Hub MQTT 지원][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
