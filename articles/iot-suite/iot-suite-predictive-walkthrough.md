---
title: "aaaPredictive 유지 관리 연습 | Microsoft Docs"
description: "Hello Azure IoT 예측 유지 관리의 연습 미리 솔루션을 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>미리 구성된 예측 유지 관리 솔루션 연습

hello 미리 구성 하는 예측 유지 관리 솔루션은 문제일 가능성이 toooccur이 있는 hello 지점을 예측 하는 비즈니스 시나리오에 대 한 종단 간 솔루션입니다. 유지 관리를 최적화하는 등의 작업에 미리 구성된 솔루션을 사용할 수 있습니다. hello 솔루션은 스트림 분석, IoT Hub와 같은 핵심 Azure IoT Suite 서비스를 결합 및 [Azure 기계 학습] [ lnk-machine-learning] 작업 영역입니다. 이 작업 영역에는 공용 샘플 데이터 집합, toopredict hello 남은 연수 (RUL) 비행기 엔진을 기반으로 모델을 포함 합니다. 완전히 hello 솔루션 tooplan 하기 위한 시작 지점으로 hello IoT 비즈니스 시나리오를 구현 하 고 사용자의 특정 비즈니스 요구 사항을 충족 하는 솔루션을 구현 합니다.

## <a name="logical-architecture"></a>논리 아키텍처

다음 다이어그램 hello hello hello 미리 구성 된 솔루션의 논리적 구성 요소를 설명 합니다.

![][img-architecture]

파란색 hello 항목은 미리 구성 하는 hello 솔루션을 배포한 hello 영역에 사용자를 프로 비전 하는 Azure 서비스입니다. hello에 hello 목록 hello 미리 구성 된 솔루션을 배포할 수 있는 영역에 표시 됩니다. [프로 비전 페이지][lnk-azureiotsuite]합니다.

녹색 hello 항목은 시뮬레이션 된 장치 비행기 엔진을 나타내는입니다. Hello 다음 섹션에서에서 이러한 시뮬레이션 된 장치에 대해 자세히 알아보십시오.

hello 회색 항목 구성 요소를 나타내는 구현 하는 *장치 관리* 기능입니다. hello hello 미리 구성 하는 예측 유지 관리 솔루션의 현재 릴리스에서 이러한 리소스를 제공 하지 않습니다. 장치 관리에 대해 자세히 toolearn 참조 toohello [미리 구성 된 솔루션 모니터링 원격][lnk-remote-monitoring]합니다.

## <a name="simulated-devices"></a>시뮬레이션된 장치

시뮬레이션된 된 장치는 미리 구성 하는 hello 솔루션에서 비행기 엔진을 나타냅니다. hello 솔루션 tooa 단일 비행기를 매핑하는 두 개의 엔진으로 프로 비전 됩니다. 각 엔진에서 네 가지 유형의 원격 분석: 센서 9, 센서 11, 센서 14 및 15의 센서 hello 엔진에 대 한 hello 기계 학습 모델 toocalculate hello RUL에 필요한 hello 데이터를 제공 합니다. 메시지 tooIoT 허브 원격 분석을 수행 하는 hello를 전송 하는 각 시뮬레이션 된 장치:

*계수 주기*. 주기는 2시간에서 10시간 사이의 기간으로 완료된 비행을 나타냅니다. Hello 비행 중 원격 분석 데이터는 30 분 마다 캡처됩니다.

*원격 분석*. 엔진 특성을 나타내는 4가지 센서가 있습니다. 센서 9, 센서 11, 센서 14 및 15의 센서 hello 센서는 일반적으로 레이블이 지정 됩니다. 이러한 네 가지 센서 hello RUL 모델에서 충분 한 원격 분석 tooobtain 유용한 결과를 나타냅니다. 미리 구성 하는 hello 솔루션에 사용 되는 hello 모델은 실제 엔진 센서 데이터를 포함 하는 공용 데이터 집합에서 만들어집니다. Hello 원래 데이터 집합에서 모델 hello를 생성 하는 방법에 대 한 자세한 내용은 참조 hello [Cortana Intelligence 갤러리 예측 유지 관리 템플릿][lnk-cortana-analytics]합니다.

시뮬레이션 된 hello 장치 hello 다음 hello 솔루션의 hello IoT 허브에서 전송 되는 명령을 처리할 수 있습니다.

| 명령 | 설명 |
| --- | --- |
| StartTelemetry |컨트롤 hello hello 시뮬레이션의 상태입니다.<br/>원격 분석 보내기 시작 hello 장치 |
| StopTelemetry |컨트롤 hello hello 시뮬레이션의 상태입니다.<br/>중지 hello 장치 원격 분석 보내기 |

IoT Hub는 장치 명령 승인을 제공합니다.

## <a name="azure-stream-analytics-job"></a>Azure Stream Analytics 작업

**작업: 원격 분석** hello 들어오는 장치 원격 분석 스트림에 두 문을 사용 하 여에서 작동 합니다.

* 먼저 hello는 hello 장치에서 모든 원격 분석을 선택 하 고이 데이터 tooblob 저장소를 보냅니다. 여기에서 hello 웹 응용 프로그램에서 표시 합니다.
* hello 평균 센서 2 분 슬라이딩 윈도우를 통해 값을 이벤트 허브 tooan hello 통해이 데이터를 보내는 두 번째 계산 **이벤트 프로세서**합니다.

## <a name="event-processor"></a>이벤트 프로세서
hello **이벤트 프로세서 호스트** Azure 웹 작업에서 실행 합니다. hello **이벤트 프로세서** 완료 주기에 대 한 hello 센서 평균 값을 사용 합니다. 그런 다음 해당 값 tooan toocalculate hello RUL는 엔진에 대 한 학습 된 모델을 노출 하는 API에 전달 합니다. hello API hello 솔루션의 일부로 제공 되는 기계 학습 작업 영역에 의해 노출 됩니다.

## <a name="machine-learning"></a>Machine Learning
hello 기계 학습 구성 요소는 실제 비행기 엔진에서 수집 된 데이터에서 파생 된 모델을 사용 합니다. Hello에 hello 타일에서 toohello 기계 학습 작업 영역을 탐색할 수 [azureiotsuite.com] [ lnk-azureiotsuite] 프로 비전 된 솔루션에 대 한 페이지입니다. hello 타일은 사용할 수 있는 hello 솔루션은 hello 때 **준비** 상태입니다.


## <a name="next-steps"></a>다음 단계
Toocustomize 경우가 hello 미리 구성 하는 예측 유지 관리 솔루션의 주요 구성 요소 hello 살펴보았습니다 것입니다. [미리 구성된 솔루션 사용자 지정에 대한 지침][lnk-customize]을 참조하세요.

탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:

* [IoT Suite에 대한 질문과 대답][lnk-faq]
* [Hello 접지에서 IoT 보안][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/