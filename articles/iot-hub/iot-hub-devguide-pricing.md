---
title: "Azure IoT 허브 가격 책정 aaaUnderstand | Microsoft Docs"
description: "개발자 가이드 - 작동 예제를 비롯하여 IoT Hub에서 측정 및 가격 책정이 진행되는 방식에 대한 정보를 제공합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Azure IoT Hub 가격 책정 정보

[Azure IoT 허브 가격 책정] [ lnk-pricing] 다른 Sku 및 IoT 허브에 대 한 가격 책정에 hello 일반 정보를 제공 합니다. 이 문서는 IoT 허브에서 IoT Hub에 다양 한 기능으로 요금이 부과 되며 hello 메시지 하는 방법을 대 한 자세한 정보를 포함 합니다.

## <a name="charges-per-operation"></a>작업당 요금

| 작업 | 대금 청구 정보 | 
| --------- | ------------------- |
| ID 레지스트리 작업 <br/> (만들기, 검색, 목록, 업데이트, 삭제) | 요금이 부과되지 않습니다. |
| 장치-클라우드 메시지 | IoT Hub에 수신 시, 성공적으로 전송된 메시지는 4KB 청크 단위로 요금이 청구됩니다. 예를 들어 6KB 메시지에는 2개 메시지로 요금이 청구됩니다. |
| 클라우드-장치 메시지 | 성공적으로 전송된 메시지는 4KB 청크 단위로 요금이 청구됩니다. 예를 들어 6KB 메시지에는 2개 메시지로 요금이 청구됩니다. |
| 파일 업로드 | IoT Hub에서 파일 전송 tooAzure 저장소 유료일 되지 않습니다. 파일 전송 시작 및 완료 메시지는 4KB 증분으로 측정되어 요금이 청구됩니다. 예를 들어 10MB 파일 전송 더하기 toohello Azure 저장소 비용을에서 두 개의 메시지 청구 됩니다. |
| 직접 메서드 | 성공적인 메서드 요청은 4KB 청크 단위로 요금이 청구됩니다. 본문이 비어 있지 않은 응답은 추가 메시지로서 4KB 단위로 요금이 청구됩니다. 요청 toodisconnected 장치 4KB 청크로 메시지로 요금이 청구 됩니다. 응답 본문이 없는 hello 장치에서 발생 하는 6 KB 본문이 있는 메서드를; 두 개의 메시지로 요금이 부과 됩니다 예를 들어, 1KB 응답 hello 장치에서 발생 하는 6 KB 본문이 있는 메서드는 hello 요청에 대 한 두 개의 메시지 + hello 응답에 대 한 다른 메시지도 청구 됩니다. |
| 장치 쌍 읽기 | 장치로 이중 읽고 hello 장치에서 다시 hello 솔루션에서 끝 512 바이트 청크에서 메시지로 요금이 청구 됩니다. 예를 들어 6KB 장치 쌍 읽기는 12개 메시지로 요금이 청구됩니다. |
| 장치 쌍 업데이트(태그 및 속성) | Hello 장치와 hello 장치에서 장치로 이중 업데이트는 512 바이트 청크에서 메시지로 요금이 청구 됩니다. 예를 들어 6KB 장치 쌍 읽기는 12개 메시지로 요금이 청구됩니다. |
| 장치 쌍 쿼리 | 쿼리는 512 바이트 청크에서 hello 결과 크기에 따라 메시지로 요금이 청구 됩니다. |
| 작업 연산 <br/> (만들기, 업데이트, 나열, 삭제) | 요금이 부과되지 않습니다. |
| 장치 단위 작업 연산 | 작업 연산(예: 장치 쌍 업데이트 및 메서드)은 정상적으로 요금이 청구됩니다. 예를 들어 1000개 메서드 호출로 1KB 요청 및 비어 있는 본문 응답을 야기하는 작업은 1000개 메시지로 요금이 청구됩니다. |

> [!NOTE]
> 모든 규모 고려 hello 페이로드 크기 바이트 (프레이밍 프로토콜은 무시 됨)으로 계산 됩니다. 메시지 (포함 하는 속성 및 본문)의 경우 hello 크기는 계산 프로토콜을 알 수 없는 방식으로 hello에 설명 된 대로 [IoT 허브 개발자 가이드 메시징][lnk-message-size]합니다.

## <a name="example-1"></a>예제 1

장치 분 tooIoT 허브와 Azure Stream Analytics를 읽은 다음 당 하나의 1KB 장치-클라우드 메시지를 보냅니다. hello 솔루션 백 엔드 메서드 호출 (페이로드를 사용한 512 바이트) hello 장치에 모든 10 분 tootrigger 특정 작업. hello 장치 toohello 메서드 200 바이트의 결과 함께 응답합니다.

hello 장치가 소비 가능 메시지 1 개 * 60 분 * 24 시간 = hello 장치-클라우드 메시지 2 요청 및 응답에 대 한 하루 1440 메시지 * 시간당 6 번 * 24 시간 = 288 하루 1728 메시지의 총 hello 방법에 대 한 메시지입니다.

## <a name="example-2"></a>예제 2

장치는 1시간마다 하나의 100KB 장치-클라우드 메시지를 보냅니다. 또한 4시간마다 1KB 페이로드로 장치 쌍을 업데이트합니다. hello 다시 하루에 한 번 읽기 hello 14 KB 장치로 이중 종료 솔루션과 512 바이트 페이로드 toochange 구성으로 업데이트 합니다.

25 (100KB/4KB) 메시지를 사용 하는 hello 장치 * 24 시간 동안 장치-클라우드 메시지와 메시지 1 개 * 6 회 하루 장치로 이중 업데이트에 대 한 하루 156 메시지의 총 합니다.
hello 솔루션 백 엔드 소비 28 메시지 (KB 14 KB/0.5) tooread hello 장치로 이중 플러스 1 인 메시지 tooupdate 29 메시지의 총 것입니다.

전체적으로 hello 장치와 hello 솔루션 백 엔드 하루 185 메시지를 사용합니다.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
