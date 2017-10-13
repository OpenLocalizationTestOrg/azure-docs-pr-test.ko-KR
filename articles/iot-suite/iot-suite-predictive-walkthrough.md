---
title: "예측 유지 관리 연습 | Microsoft Docs"
description: "Azure IoT 예측 정비 사전 구성 솔루션에 대한 연습입니다."
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
ms.openlocfilehash: a68a8fdc3976ade0d1036d5ed58c8b2eb6d32a5d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>미리 구성된 예측 유지 관리 솔루션 연습

미리 구성된 예측 유지 관리 솔루션은 오류가 발생할 가능성이 있는 경우 지점을 예측하는 비즈니스 시나리오에 대한 종단 간 솔루션입니다. 유지 관리를 최적화하는 등의 작업에 미리 구성된 솔루션을 사용할 수 있습니다. 솔루션은 IoT Hub, Stream Analytics 및 [Azure Machine Learning][lnk-machine-learning] 작업 영역과 같은 주요 Azure IoT Suite 서비스를 결합합니다. 이 작업 영역에는 공용 샘플 데이터 집합에 따라 항공기 엔진의 RUL(잔여 수명)을 예측하는 모델이 포함되어 있습니다. 솔루션은 IoT 비즈니스 시나리오를 시작점으로 구현하여 고유한 특정 비즈니스 요구 사항을 충족하는 솔루션을 계획하고 구현합니다.

## <a name="logical-architecture"></a>논리 아키텍처

다음 다이어그램에서는 미리 구성된 솔루션의 논리적 구성 요소를 간략히 보여줍니다.

![][img-architecture]

파란색 항목은 미리 구성된 솔루션을 배포한 지역에 프로비전되는 Azure 서비스입니다. 미리 구성된 솔루션을 배포할 수 있는 지역 목록은 [프로비전 페이지][lnk-azureiotsuite]에 표시됩니다.

녹색 항목은 항공기 엔진을 나타내는 시뮬레이션된 장치입니다. 다음 섹션에서 이러한 시뮬레이션된 장치에 대해 자세히 알아볼 수 있습니다.

회색 항목은 *장치 관리* 기능을 구현하는 구성 요소를 나타냅니다. 미리 구성된 예측 유지 관리 솔루션의 현재 릴리스에서는 이러한 리소스를 프로비전하지 않습니다. 장치 관리에 대한 자세한 내용은 [미리 구성된 솔루션 원격 모니터링][lnk-remote-monitoring]을 참조합니다.

## <a name="simulated-devices"></a>시뮬레이션된 장치

미리 구성된 솔루션에서 시뮬레이션된 장치는 항공기 엔진을 나타냅니다. 솔루션은 단일 비행기에 매핑하는 2개의 엔진으로 프로비전됩니다. 각 엔진은 다음과 같은 4가지 형식의 원격 분석을 내보냅니다. 센서9, 센서11, 센서14 및 센서15는 Machine Learning 모델이 엔진의 RUL을 계산하는 데 필요한 데이터를 제공합니다. 시뮬레이션된 각 장치는 IoT Hub에 다음과 같은 원격 분석 메시지를 보냅니다.

*계수 주기*. 주기는 2시간에서 10시간 사이의 기간으로 완료된 비행을 나타냅니다. 비행 동안 원격 분석 데이터는 30분마다 캡처됩니다.

*원격 분석*. 엔진 특성을 나타내는 4가지 센서가 있습니다. 센서9, 센서11, 센서14 및 센서15는 일반적으로 레이블이 지정됩니다. 이러한 네 가지 센서는 RUL 모델에서 유용한 결과를 얻을 수 있는 데 충분한 원격 분석을 나타냅니다. 미리 구성된 솔루션에서 사용되는 모델은 실제 엔진 센서 데이터를 포함하는 공용 데이터 집합에서 만들어집니다. 원래 데이터 집합에서 모델을 만드는 방법에 대한 자세한 내용은 [Cortana Intelligence 갤러리 예측 유지 관리 템플릿][lnk-cortana-analytics]을 참조하세요.

또한 시뮬레이션된 장치는 솔루션의 IoT Hub에서 보낸 다음 명령을 처리할 수 있습니다.

| 명령 | 설명 |
| --- | --- |
| StartTelemetry |시뮬레이션의 상태를 제어합니다.<br/>원격 분석을 보내는 장치를 시작합니다. |
| StopTelemetry |시뮬레이션의 상태를 제어합니다.<br/>원격 분석을 보내는 장치를 중지합니다. |

IoT Hub는 장치 명령 승인을 제공합니다.

## <a name="azure-stream-analytics-job"></a>Azure Stream Analytics 작업

**작업: 원격 분석**은 두 가지 문을 사용하여 들어오는 장치 원격 분석 스트림에서 작동합니다.

* 첫 번째 문은 장치에서 모든 원격 분석을 선택하고 Blob Storage에 이 데이터를 보냅니다. 여기에서 데이터가 웹앱에 시각화됩니다.
* 두 번째 문은 2분 슬라이딩 창을 통해 평균 센서 값을 계산하고 이벤트 허브를 통해 **이벤트 프로세서**로 이 데이터를 보냅니다.

## <a name="event-processor"></a>이벤트 프로세서
**이벤트 프로세서 호스트**는 Azure Web Job에서 실행됩니다. **이벤트 프로세서** 는 완료된 주기의 평균 센서 값을 사용합니다. 학습된 모델을 노출하는 API에 해당 값을 전달하여 엔진에 대한 RUL를 계산합니다. API는 솔루션의 일부로 프로비전되는 Machine Learning 작업 영역에 의해 노출됩니다.

## <a name="machine-learning"></a>기계 학습
Machine Learning 구성 요소는 실제 항공기 엔진에서 수집된 데이터에서 파생된 모델을 사용합니다. 프로비전된 솔루션에 대한 [azureiotsuite.com][lnk-azureiotsuite] 페이지의 타일에서 Machine Learning 작업 영역으로 이동할 수 있습니다. 솔루션이 **준비** 상태일 때 타일이 제공됩니다.


## <a name="next-steps"></a>다음 단계
지금까지 미리 구성된 예측 유지 관리 솔루션의 주요 구성 요소를 살펴보았으며 이를 사용자 지정할 수 있습니다. [미리 구성된 솔루션 사용자 지정에 대한 지침][lnk-customize]을 참조하세요.

미리 구성된 IoT Suite 솔루션의 몇 가지 다른 기능 및 기능을 탐색할 수 있습니다.

* [IoT Suite에 대한 질문과 대답][lnk-faq]
* [처음부터 IoT 보안을 고려][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/