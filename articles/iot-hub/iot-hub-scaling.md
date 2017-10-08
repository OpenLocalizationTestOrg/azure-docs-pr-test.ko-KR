---
title: "aaaAzure IoT 허브를 크기 조정 | Microsoft Docs"
description: "어떻게 tooscale IoT 허브 toosupport 예상된 메시지 처리량입니다. 각 계층에 대 한 지원 hello 처리량 및 분할에 대 한 옵션에 대 한 요약을 포함합니다."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>IoT Hub 솔루션 크기 조정
Azure IoT Hub tooa 백만 동시에 연결 된 장치를 지원할 수 있습니다. 자세한 내용은 [IoT Hub 가격 책정][lnk-pricing]을 참조하세요. 각 IoT Hub 단위는 특정 개수의 일일 메시지를 허용합니다.

tooproperly는 솔루션 확장, IoT 허브의 특정 용도 것이 좋습니다. 특히 다음 범주의 작업 hello에 대 한 필요한 hello 최대 처리량을 고려해 야 합니다.

* 장치-클라우드 메시지
* 클라우드-장치 메시지
* ID 레지스트리 작업

또한 toothis 처리량 정보에서 참조 [IoT Hub 할당량 및 제한을] [ IoT Hub quotas and throttles] 및 그에 따라 솔루션을 디자인 합니다.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>장치-클라우드 및 클라우드-장치 메시지 처리량
hello 가장 좋은 방법은 toosize IoT Hub 솔루션에는 단위 별로 tooevaluate hello 트래픽입니다.

장치-클라우드 메시지는 다음과 같은 지속적인 처리량 지침을 따릅니다.

| 계층 | 지속적인 처리량 | 지속적인 전송 속도 |
| --- | --- | --- |
| S1 |단위당 KB too1111 수/분<br/>(1.5GB/일/장치) |장치당 평균 278메시지/분<br/>(400,000메시지/일/장치당) |
| S2 |Too16 MB/분 단위 당를<br/>(22.8GB/일/장치) |장치당 평균 4,167개 메시지/분<br/>(6백만 개의 메시지/일/장치당) |
| S3 |Too814 MB/분 단위 당를<br/>(1144.4GB/일/장치) |장치당 평균 208,333 메시지/분<br/>(3억 개의 메시지/일/장치당) |

## <a name="identity-registry-operation-throughput"></a>ID 레지스트리 작업 처리량
IoT Hub identity 레지스트리 작업 toobe 런타임 작업 멤버인 관련된 toodevice 프로 비전 대부분 안 됩니다.

관련 버스트 성능 수치는 [IoT Hub 할당량 및 제한][IoT Hub quotas and throttles]을 참조하세요.

## <a name="sharding"></a>분할
단일 IoT 허브 장치의 toomillions 확장할 수, 하는 동안 솔루션 특정 성능 특성을 단일 IoT 허브 보장할 수 없습니다이 필요한 경우도 있습니다. 이 경우 여러 IoT Hub로 장치를 분할하는 것이 좋습니다. 여러 IoT hub 트래픽 급증을 매끄럽게 하 고 hello 필요한 처리량 또는 필요한 작업 속도 가져옵니다.

## <a name="next-steps"></a>다음 단계
toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
