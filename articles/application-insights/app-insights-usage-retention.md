---
title: "Azure Application Insights를 사용한 웹 응용 프로그램에 대 한 보존 분석 aaaUser | Microsoft docs"
description: "Tooyour 앱 반환 하는 몇 명 입니까?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Application Insights를 사용한 웹 응용 프로그램의 사용자 재방문 주기 분석

hello 보존 기능인 [Azure Application Insights](app-insights-overview.md) tooyour 응용 프로그램 및 특정 작업을 수행 하거나 목표를 달성 얼마나 자주 사용 하면 사용자 수를 분석할 반환 합니다. 예를 들어 게임 사이트를 실행 하는 경우 우위 후 반환 hello 번호로 게임 손실 된 후 toohello 사이트를 반환 하는 사용자의 hello 숫자를 비교할 수 있습니다. 이러한 지식이 있으면 사용자 환경 및 비즈니스 전략을 둘 다 향상시킬 수 있습니다.

## <a name="get-started"></a>시작

Hello 보존 도구 hello Application Insights 포털에서 데이터를 아직 표시 되지 않으면 [tooget hello 사용량 도구를 시작 하는 방법에 대해 알아봅니다](app-insights-usage-overview.md)합니다.

## <a name="hello-retention-tool"></a>hello 보존 도구

![재방문 주기 도구](./media/app-insights-usage-retention/retention.png)

1. hello 도구 모음 toocreate 새 보존 보고서 사용자가 사용, 기존 보존 보고서를 열고, 현재 보존 보고서 저장 또는 다른 이름으로 저장, toosaved 보고서 변경 내용이 되돌릴, 전자 메일 또는 직접 연결 및 액세스 hello를 통해 공유 보고서 hello 보고서에서 데이터 새로 고침 설명서 페이지입니다. 
2. 기본적으로 재방문 주기는 기간에 따라 작업을 한 후 다시 방문하고 다른 작업을 한 모든 사용자를 보여 줍니다. 특정 사용자 활동에 이벤트 toonarrow hello 포커스의 여러 조합을 선택할 수 있습니다.
3. 속성에 대해 하나 이상의 필터를 추가합니다. 예를 들어 특정 국가 또는 하위 지역에 있는 사용자에 집중할 수 있습니다. 클릭 **업데이트** hello 필터를 설정한 후 합니다. 
4. hello 전반적인 보존 차트 요약해 서 보여주는 사용자 보존 hello 특정 기간에 걸쳐 있습니다. 
5. hello 표 형식으로 사용자 수가 hello 유지 따라 toohello 쿼리 작성기 # 2를 표시 합니다. 각 행에 표시 된 기간 hello 시간에 모든 이벤트를 수행한 사용자의 코 호트를 나타냅니다. Hello 행의 각 셀 이후 기간에 적어도 한 번 해당 코 호트의 반환을 표시 합니다. 일부 사용자는 둘 이상의 기간에 돌아올 수 있습니다. 
6. 상위 5 개 반환 이벤트 toogive 사용자가 자신의 보존 보고서를 더 잘 이해를 hello insights 카드 상위 5 개 시작 이벤트를 표시 합니다. 

![재방문 주기 마우스 가리키기](./media/app-insights-usage-retention/hover.png)

사용자가 셀 hello 보존 tool tooaccess hello 분석 단추 위로 수 및 도구 설명 바로 hello 셀에 설명 합니다. hello 분석 단추 hello 셀에서 미리 입력된 쿼리 toogenerate 사용자와 사용자 toohello 분석 도구를 사용 합니다. 

## <a name="use-business-events-tootrack-retention"></a>비즈니스 이벤트 tootrack 보존을 사용 하 여

tooget hello 가장 유용한 보존 분석, 중요 한 비즈니스 활동을 나타내는 측정값 이벤트입니다. 

예를 들어 많은 사용자가 표시 하는 hello 게임을 재생 하지 않고 앱에서 페이지를 열 수 있습니다. 방금 hello 페이지 뷰를 추적 하는 것은 얼마나 많은 사람들이 반환 tooplay hello 게임 후 이전에 지속적인 부정확 한 예상을 제공 따라서 합니다. 플레이어 반환 명확히 tooget 앱 실제로 수행 하는 경우 사용자 지정 이벤트를 보내야 합니다.  

것이 좋습니다 toocode 사용자 지정 이벤트 및 보존 분석에 사용 하는 주요 비즈니스 동작을 나타냅니다. toocapture hello 게임 결과 한 줄의 코드 toosend 사용자 지정 이벤트 tooApplication Insights toowrite가 필요합니다. Node.JS 또는 hello 웹 페이지 코드에 해당 작성, 하는 경우 다음과 같이 보입니다.

```JavaScript
    appinsights.trackEvent("won game");
```

또는 ASP.NET 서버 코드:

```C#
   telemetry.TrackEvent("won game");
```

[사용자 지정 이벤트 작성에 대해 자세히 알아봅니다](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>다음 단계
- tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.
- 사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.
    - [사용자, 세션, 이벤트](app-insights-usage-segmentation.md)
    - [깔때기](usage-funnels.md)
    - [사용자 흐름](app-insights-usage-flows.md)
    - [통합 문서](app-insights-usage-workbooks.md)
    - [사용자 컨텍스트 추가](app-insights-usage-send-user-context.md)


