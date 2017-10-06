---
title: "Azure 시간 시계열 Insights aaaOverview | Microsoft Docs"
description: "소개 tooAzure 시간 시계열 통찰력을 시간 시계열 데이터 분석 및 IoT 솔루션에 대 한 새 서비스"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>Azure Time Series Insights란?

Azure 시간 시계열 Insights는 저장소, 분석, 쉽게 tooingest 확인, 저장 하 고, 탐색 하 고 동시에 수십 억 개의 이벤트를 분석 하는 시각화 구성 요소와 관리 되는 클라우드 서비스입니다. Time Series Insights는 데이터의 전체 보기를 제공하여 IoT 솔루션의 유효성을 빠르게 검사할 수 있으며, 숨겨진 추세와 비정상을 검색하고 거의 실시간으로 근본 원인 분석을 수행할 수 있도록 하여 비용이 많이 드는 장치 가동 중지를 방지할 수 있습니다. 시간 시계열 Insights 이벤트 브로커 (예: IoT 허브 또는 이벤트 허브)의 시계열 데이터를 수집 하 고 인덱스 hello 데이터 및 구성 가능한 보존 정책에 따라 데이터를 만료 합니다. 사용자는 직관적인 UX 또는 REST 쿼리 Api를 통해 hello 데이터를 사용합니다.

![Time Series Insight 개요](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>기본 시나리오

* 수분 내에 IoT 솔루션을 모니터링하고 유효성을 검사합니다.
* 대용량 IoT 데이터를 시각화하고 분석합니다.
* 근본 원인 분석 및 변칙 검색을 빠르게 수행합니다.
* 여러 장치, 장비 및 데이터의 전체 보기를 만듭니다.

## <a name="capabilities-and-benefits"></a>기능 및 이점

* **시작 하는 쉬운 tooget**: Azure 시간 시계열 Insights 사전 데이터의 준비 없이 있어야 하며 아주 빨리 됩니다. Azure IoT Hub 및 이벤트 허브의 이벤트 toobillions 분 후에 연결 합니다. 연결 되 면 시각화 하 고 tooquickly IoT 솔루션의 유효성을 검사 하는 시간 (초)의 센서 데이터와 상호 작용 합니다. 시간 시계열 Insights는 쉽게 toouse; 코드의 한 줄도 작성 하지 않고 데이터와 상호 작용할 수 있습니다.  새 언어 toolearn 없습니다. 시간 시계열 Insights 고급 사용자를 위해 세부적인, 자유 텍스트 쿼리 화면을 제공 하 고 가리킨 모두에 대 한 탐색을 클릭 합니다.

* **실시간 정보 근처**: toochanges를 신속 하 게 대응할 수 있도록 시간 시계열 Insights 1 분 대기 시간으로 수백만 개의 하루 센서 이벤트 수집 수 있습니다. Time Series Insights는 추세와 비정상을 빠르게 찾아내고, 복잡한 근본 원인을 분석하며, 비용이 많이 드는 가동 중지를 방지할 수 있게 함으로써 센서 데이터에 대한 심층적인 정보를 얻을 수 있습니다. 실시간 및 과거 데이터 간의 간 상관 관계를 활성화 하 여 시간 시계열 Insights hello 데이터의 숨겨진된 추세를 잠금 해제 수 있습니다.

* **사용자 지정 솔루션 빌드**: Azure Time Series Insights 데이터를 기존 응용 프로그램에 포함하거나 Time Series Insights REST API를 사용하여 새로운 사용자 지정 솔루션을 만들 수 있습니다. 만들고 공유 공유할 수 있습니다 다른 사용자에 대 한 tooexplore 사용자 검색 보기 개인 설정 합니다.

* **확장성**: 시간 시계열 Insights는 규모에 디자인 된 toosupport IoT 합니다. 미리 보기에서 1 백만 too100 31 일의 기본 보존 기간으로 하루 백만 이벤트에 걸쳐에서 들어 오는 수 있습니다. 방대한 양의 기록 데이터와 함께 라이브 데이터 스트림을 거의 실시간으로 시각화하고 분석할 수 있습니다. 앞으로 이동, 수신 및 보존 비율 tooaccommodate 적이 변화 하는 엔터프라이즈 규모를 증가 합니다.

## <a name="time-series-insights-glossary"></a>Time Series Insights 용어

* **환경**: 환경은 수신 및 저장 용량이 있는 Azure 리소스입니다.  고객 환경 hello 필요한 용량으로 Azure 포털을 통해 프로 비전합니다.
* **이벤트 원본**: 이벤트 원본은 Azure Event Hubs 같은 이벤트 브로커에서 파생됩니다.  시간 시계열 Insights tooEvent 소스 코드를 작성 하지 않고 hello 데이터 스트림을 수집 직접 연결 합니다. 현재 Time Series Insights는 Azure Event Hubs 및 Azure IoT Hubs를 지원합니다.
* **참조 데이터**: 시간 시계열 Insights hello 기능 toojoin 시계열 데이터를 참조 데이터와 사용자가 제공 합니다.  참조 데이터는 장치에 대한 메타데이터 또는 비교적 자주 변경되지 않는 다른 정적 데이터를 포함할 수 있습니다. 시간 시계열 Insights 사용자 toovisualize 수 있도록 데이터 스트림 사용 하 여 hello 참조 데이터를 조인 하 고 거의 실시간으로이 데이터를 분석할 합니다.
