---
title: "aaaPredict 차량 상태 습관-Azure 지원 하 고 | Microsoft Docs"
description: "습관 지원 하 고 차량 상태에 대해 Cortana 인텔리전스 toogain 실시간 및 예측 insights hello 기능을 사용 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>차량 원격 분석 솔루션 플레이북
이 **메뉴** toohello 장이 플레이이 북에 연결 합니다. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>개요
슈퍼 컴퓨터 hello 랩 외부로 이동한 우리의 시설에 주차 이제 됩니다! 이러한 첨단 자동차는 수많은 hello 기능 tootrack 부여 센서, 포함 및 초당 수백만 개의 이벤트를 모니터링 합니다. 2020 하 여 대부분의 이러한 자동차 됩니다 되었음을 인터넷 연결된 toohello 라고 생각 됩니다. 이러한 다양 한 데이터 tooprovide 큰 보안, 안정성 및 구동 더 잘 경험을 이용 가정해 보세요! Microsoft는 Cortana Intelligence를 통해 이 꿈을 현실화했습니다.

Microsoft의 Cortana 인텔리전스는 완전히 관리 되는 빅 데이터 및 지능형 동작으로 analytics suite tootransform 수 있는 데이터를 고급 합니다. Toointroduce 원하는 toohello Cortana Intelligence 차량 원격 분석 분석 솔루션 템플릿을 합니다. 이 솔루션은 방법을 보여 주는 딜러 car, automobile 제조업체 및 보험 회사 수 실시간 Cortana 인텔리전스 toogain hello 기능을 사용 하는 차량 상태 및 구동에서 예측 insights 습관입니다. 

hello 솔루션으로 구현 하는 [람다 아키텍처 패턴](https://en.wikipedia.org/wiki/Lambda_architecture) hello에 대 한 hello Cortana Intelligence 플랫폼에 잠재력을 보여 주는 실시간 및 일괄 처리 합니다. hello 해결 방법: 

* Vehicle Telematics 시뮬레이터 제공
* 이벤트 허브를 이용하여 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집 
* 스트림 분석 toogain 실시간 정보를 사용 하 여 차량 상태에 대해
* 일괄 처리의 다양 한 분석에 대 한 장기 저장소에 hello 데이터를 유지합니다. 
* 활용 기계 학습에서 비정상 검색에 대 한 실시간 및 처리 toogain 예측 insights 일괄 처리 합니다.
* 크기 조정 및 Data Factory toohandle 오케스트레이션, 예약, 리소스 관리 및 모니터링 hello 일괄 처리 파이프라인의에서 HDInsight tootransform 데이터를 활용 하 여 
* Power BI를 사용하여 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공

## <a name="architecture"></a>아키텍처
![솔루션 아키텍처 다이어그램](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*그림 1 - 차량 원격 분석 솔루션 아키텍처*

이 솔루션에 hello 다음과 같은 **Cortana Intelligence 구성 요소** 의 최종 tooend 통합에서는 및:

* **이벤트 허브** - 수백만 개의 차량 원격 분석 이벤트를 Azure에 수집합니다.
* **스트림 분석** - 차량 상태에 대한 실시간 통찰력을 얻고 다양한 일괄 처리 분석을 위해 해당 데이터를 장기간용 저장소에 보관합니다.
* **기계 학습** 실시간 이상 탐지에 대 한 및 일괄 처리 예측 insights toogain 합니다.
* **HDInsight** 규모로 tootransform 사용된 데이터는
* **Data Factory** 오케스트레이션, 예약, 리소스 관리 및 모니터링 hello 일괄 처리 파이프라인을 처리 합니다.
* **Power BI** - 실시간 데이터 및 예측 분석 시각화를 위해 이 솔루션을 다양한 대시보드에 제공합니다.

이 솔루션은 서로 다른 두 개의 **데이터 원본**에 액세스합니다. 

* **자동차를 움직일 신호 및 진단 시뮬레이션**: 차량 전자 통신 정보 시뮬레이터 진단 정보 및 해당 하는 hello 차량와 시간에서 지정된 된 지점에서 패턴을 구동 하는 hello toohello 상태는 신호를 내보냅니다. 
* **자동차를 움직일 카탈로그**: VIN toomodel 매핑을 포함 하는 참조 데이터 집합입니다.

