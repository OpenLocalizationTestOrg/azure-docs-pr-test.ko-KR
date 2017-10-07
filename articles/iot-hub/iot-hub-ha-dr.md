---
title: "IoT Hub 고가용성 및 재해 복구 aaaAzure | Microsoft Docs"
description: "재해 복구 기능을 사용 하는 항상 사용 가능한 Azure IoT 솔루션 toobuild 수 있는 hello Azure와 IoT 허브 기능에 설명 합니다."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>IoT Hub 고가용성 및 재해 복구
IoT Hub와 Azure 서비스로 HA (고가용성) hello Azure 지역 수준에서 중복을 사용 하 여 hello 솔루션에 필요한 추가 작업 없이 제공 합니다. hello Microsoft Azure 플랫폼에는 지역 간 가용성 또는 재해 복구 (DR) 기능을 사용 하 여 솔루션을 작성 하는 기능 toohelp 포함 되어 있습니다. Tooprovide를 전역 원하는 지역 간 고가용성 장치 또는 사용자가에 대 한 디자인 하 고 이러한 Azure dr 간의 보호 기능을 활용 tootake 솔루션을 준비 합니다. hello 문서 [Azure 비즈니스 연속성 기술 지침](../resiliency/resiliency-technical-guidance.md) 비즈니스 연속성 및 DR을 위한 Azure의 hello 기본 제공 기능에 설명 합니다. hello [Azure 응용 프로그램에 대 한 고가용성 및 재해 복구] [ Disaster recovery and high availability for Azure applications] 문서 tooachieve Azure 응용 프로그램에 대 한 전략에 아키텍처 지침에서는 HA과 DR 기능을 합니다.

## <a name="azure-iot-hub-dr"></a>Azure IoT Hub DR
또한 toointra 지역 HA IoT Hub hello 사용자의 개입 없이 필요로 하는 재해 복구에 대 한 장애 조치 메커니즘을 구현 합니다. IoT 허브 DR 자체 시작 되었으며 2-26, 시간 및 복구 지점 목표 (Rpo)를 수행 하는 hello의 복구 시간 목표 (RTO).

| 기능 | RPO |
| --- | --- |
| 레지스트리 및 통신 작업에 대 한 서비스 가용성 |CName 손실 가능성 |
| ID 레지스트리의 ID 데이터 |0-5분 데이터 손실 |
| 장치-클라우드 메시지 |읽지 않은 메시지가 모두 손실됨 |
| 작업 모니터링 메시지 |읽지 않은 메시지가 모두 손실됨 |
| 클라우드-장치 메시지 |0-5분 데이터 손실 |
| 클라우드-장치 피드백 큐 |읽지 않은 메시지가 모두 손실됨 |

## <a name="regional-failover-with-iot-hub"></a>IoT Hub를 통한 국가별 장애 조치
IoT 솔루션에서 배포 토폴로지에 대가 문서의 hello 범위를 벗어납니다. hello 설명 hello *국가별 장애 조치가* 고가용성 및 재해 복구의 hello 용도 대 한 배포 모델입니다.

국가별 장애 조치가 모델에서는 기본적으로 하나의 데이터 센터 위치에서 백 엔드 실행 솔루션 hello 하 고 보조 IoT hub 및 백 엔드 다른 데이터 센터 위치에 배포 됩니다. Hello IoT hub hello 기본 데이터 센터에서 가동 중단의 성능이 경우 hello 장치 toohello 기본 데이터 센터에서 hello 네트워크 연결이 중단 되었습니다. 장치는 hello 기본 게이트웨이에 연결할 수 없는 보조 서비스 끝점을 사용 합니다. 지역 간 장애 조치 기능을 통해 단일 영역의 hello 고가용성 외 hello 솔루션 가용성을 높일 수 있습니다.

IoT 허브를 사용 하 여 국가별 장애 조치가 모델 tooimplement 높은 수준 hello 다음이 필요합니다.

* **보조 IoT hub 및 라우팅 논리 장치**: hello 하면 기본 지역의 서비스 중단의 경우에 장치 연결 tooyour 보조 지역 시작 해야 합니다. 관련 된 대부분의 서비스의 상태를 인식 특성 hello 들어 것 솔루션 관리자 tootrigger hello 지역 간 장애 조치 프로세스에 대 한 합니다. hello 가장 좋은 방법은 toocommunicate hello 새 끝점 toodevices, hello 프로세스의 제어를 유지 하면서은 toohave 정기적으로 확인 하는 *호텔* hello 현재 활성 상태인 끝점에 대 한 서비스입니다. hello 호텔 서비스 일 수 있습니다 복제 되 고 연결할 수를 유지 하는 웹 응용 프로그램 리디렉션 DNS 기술을 사용 하 여 (예를 들어를 사용 하 여 [Azure 트래픽 관리자][Azure Traffic Manager]).
* **Identity 레지스트리 복제** -사용 가능한 toobe, hello 보조 IoT 허브 toohello 솔루션에 연결할 수 있는 모든 장치 id를 포함 해야 합니다. hello 솔루션 장치 id의 지리적으로 복제 된 백업을 유지 하 고 hello 장치에 대 한 활성 끝점이 hello를 전환 하기 전에 toohello 보조 IoT 허브를 업로드 해야 합니다. IoT Hub의 hello 장치 identity 내보내기 기능은이 컨텍스트에서 유용합니다. 자세한 내용은 [IoT Hub 개발자 가이드 - ID 레지스트리][IoT Hub developer guide - identity registry]를 참조하세요.
* **논리 병합** -다시 사용할 수 있게 hello 기본 지역, 모든 hello 상태 및 hello 보조 사이트에서 생성 된 데이터에는 마이그레이션된 백 toohello 기본 지역 이어야 합니다. 이 상태 및 데이터 대부분와 관련 된 toodevice id 및 응용 프로그램 메타 데이터를 hello 기본 IoT 허브 및 다른 응용 프로그램 관련 저장소 hello 기본 지역에 병합 해야 합니다. toosimplify이이 단계에서는 idempotent 작업을 사용 해야 합니다. Idempotent 작업 hello 예기치 않은 결과 및 중복 또는 이벤트의 순서가 배달 hello 결과적 일관성 있게 배포 이벤트의에서 최소화합니다. 또한 응용 프로그램 논리를 hello 디자인 된 tootolerate 잠재적인 불일치 또는 날짜 상태에서 해제 "약간" 여야 합니다. 이 경우 복구 지점 목표 (RPO)에 따라 "치료" toohello 추가 시간이 걸리는 hello 시스템에 대 한 너무 인해 발생할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이러한 링크 toolearn Azure IoT 허브에 대 한 자세한를 수행 합니다.

* [IoT Hub 시작(자습서)][lnk-get-started]
* [Azure IoT Hub란?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
