---
title: "응용 프로그램 Insights 원격 분석 데이터 모델 aaaAzure | Microsoft Docs"
description: "Application Insights 데이터 모델 개요"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Application Insights 원격 분석 데이터 모델

[Azure Application Insights](app-insights-overview.md) hello 성능 및 응용 프로그램의 사용을 분석할 수 있도록 웹 응용 프로그램 toohello Azure 포털에서에서 원격 분석을 보냅니다. hello 원격 분석 모델은 가능한 toocreate 플랫폼 및 언어 독립적 모니터링 되도록 표준화 되었습니다. 

Application Insights에서 수집한 데이터를 통해 다음과 같은 일반적인 응용 프로그램 실행 패턴을 모델링합니다.

![Application Insights 응용 프로그램 모델](./media/application-insights-data-model/application-insights-data-model.png)

hello 다음과 같은 유형의 원격 분석은 응용 프로그램 사용 되는 toomonitor hello 실행 합니다. hello 다음 세 가지 종류는 일반적으로 자동으로 수집 hello Application Insights SDK에서 hello 웹 응용 프로그램 프레임 워크에서:

* [**요청** ](application-insights-data-model-request-telemetry.md) -toolog 응용 프로그램에서 수신 하는 요청을 생성 합니다. 예를 들어 hello Application Insights 웹 SDK 웹 앱 수신 하는 각 HTTP 요청에 대 한 요청 원격 분석 항목을 자동으로 생성 합니다. 

    **작업** hello 스레드는 요청을 처리 하는 실행 됩니다. 수도 있습니다 [코드를 작성](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor 다른 종류의 작업, 작업 또는 정기적으로 사용 하는 함수를 "해제" 웹에 같은 데이터를 처리 합니다.  각 작업에는 ID가 있습니다. Too[group]((application-insights-correlation.md) 사용된 될 수 있는이 ID 생성 된 응용 프로그램에서 hello 요청을 처리 하는 동안 모든 원격 분석 각 작업은 성공하거나 실패하며 일정 기간 동안 지속됩니다.
* [**예외** ](application-insights-data-model-exception-telemetry.md) -일반적으로 작업 toofail를 발생 시키는 예외를 나타냅니다.
* [**종속성** ](application-insights-data-model-dependency-telemetry.md) -앱 tooan 외부 서비스 또는 REST API 또는 SQL과 같은 저장소에서 호출을 나타냅니다. ASP.NET, 종속성 호출 tooSQL 하 여 정의 된 `System.Data`합니다. 호출 tooHTTP 끝점은 정의한 `System.Net`합니다. 

Application Insights는 사용자 지정 원격 분석을 위한 데이터 형식으로 다음 세 가지 형식을 추가로 제공합니다.

* [추적](application-insights-data-model-trace-telemetry.md) -중 하나를 직접 사용 하거나 어댑터 tooimplement 진단 로깅을 통해과 같은 친숙 한 tooyou를가 하는 계측 프레임 워크를 사용 하 여 `Log4Net` 또는 `System.Diagnostics`합니다.
* [이벤트](application-insights-data-model-event-telemetry.md) -일반적으로 서비스를 tooanalyze 사용 패턴 toocapture 사용자 상호 작용을 사용 합니다.
* [메트릭](application-insights-data-model-metric-telemetry.md) -tooreport 주기적 스칼라 측정을 사용 합니다.

모든 원격 분석 항목 hello를 정의할 수 [컨텍스트 정보](application-insights-data-model-context.md) 응용 프로그램 버전 또는 사용자 세션 id입니다. 컨텍스트는 특정 시나리오를 차단 해제하는 강력한 형식의 필드 집합입니다. 응용 프로그램 버전이 올바르게 초기화된 경우 Application Insights는 재배포와 상호 관련된 응용 프로그램 동작에서 새 패턴을 검색할 수 있습니다. 세션 id 사용된 toocalculate hello 장애 또는 사용자에 게 문제 영향을 수 있습니다. 실패한 특정 종속성, 오류 추적 또는 중요한 예외에 대한 세션 ID 값의 고유 개수를 계산하면 영향을 쉽게 이해할 수 있습니다.

Application Insights 원격 분석 모델 정의 방법을 너무[상관 관계를 지정](application-insights-correlation.md) 원격 분석 toohello 작업이 포함 되었습니다. 예를 들어 요청은 SQL Database 호출을 수행하고 기록된 진단 정보를 작성할 수 있습니다. 뒤로 toohello 요청 원격 분석을 연결 하는 원격 분석 항목에 대 한 hello 상관 관계 컨텍스트를 설정할 수 있습니다.

## <a name="schema-improvements"></a>향상된 스키마

응용 프로그램 Insights 데이터 모델은 단순 하 고 기본 하지만 강력한 방법은 toomodel 응용 프로그램 원격 분석 합니다. Tookeep hello 모델 간단 하 고 슬림 toosupport 중요 시나리오를 위해 노력 하 고 고급 사용을 위한 tooextend hello 스키마를 허용 합니다.

GitHub를 사용 하 여 데이터 모델 또는 스키마 문제 tooreport 및 제안 사항 [ApplicationInsights 홈](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) 저장소입니다.

## <a name="next-steps"></a>다음 단계

- [사용자 지정 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md).
- 너무 방법에 대해 알아봅니다[확장 하 고 원격 분석 필터링](app-insights-api-filtering-sampling.md)합니다.
- 사용 하 여 [샘플링](app-insights-sampling.md) toominimize 양의 원격 분석 데이터 모델에 기반 합니다.
- Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.
