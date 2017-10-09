---
title: "aaaAnalyze Azure Application Insights의 흐름에서는 사용자를 사용 하는 사용자 탐색 패턴 | Microsoft docs"
description: "Hello 페이지 및 웹 앱의 기능 간에 사용자가 탐색 하는 방식을 분석 합니다."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Application Insights에서 사용자 흐름을 사용하여 사용자 탐색 패턴 분석

![Application Insights 사용자 흐름 도구](./media/app-insights-usage-flows/flows.png)

hello 사용자 흐름 도구 hello 페이지 및 사이트의 기능 간에 사용자가 탐색 하는 방식을 시각화 합니다. 다음과 같은 질문에 대답할 수 있습니다.
* 사용자가 사이트 페이지에서 벗어나려면 어떻게 할까요?
* 사용자가 사이트 페이지에서 어디를 클릭하나요?
* 사용자가 사이트에서 가장 변동는 배치 있는 hello?
* 여기서 사용자가 반복 hello 동일한 작업을 반복 하는 장소 있습니까?

hello 사용자 흐름 도구 초기 페이지 뷰 또는 지정 하는 이벤트를 시작 합니다. 페이지 보기 및 사용자는 나중에 세션에서 두 단계를 나중에, 등 즉시 연결 하는 사용자 지정 이벤트 표시 hello이 페이지 보기 또는 사용자 지정 이벤트를 전달 하는 사용자 지정 합니다. 다양한 두께의 선은 사용자가 따라간 각 경로의 횟수를 보여줍니다. 특별 한 "세션이 종료" 노드는 사용자 수 이후에 보낸 메시지 페이지 뷰 또는 사용자 지정 이벤트가 없습니다 hello 앞에 노드를 사이트에 사용자가 아마도 왼쪽 강조 표시를 보여 줍니다.



> [!NOTE]
> Application Insights 리소스 페이지 뷰 또는 사용자 지정 이벤트 toouse hello 사용자 흐름 도구에 포함 해야 합니다. [Tooset 앱 toocollect 페이지를 자동으로 hello Application Insights JavaScript SDK로 보는 방법에 대해 알아봅니다](app-insights-javascript.md)합니다.
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>초기 페이지 보기 또는 사용자 지정 이벤트를 선택하여 시작

![사용자 흐름에 대한 초기 이벤트 선택](./media/app-insights-usage-flows/flows-initial-event.png)

hello 사용자 흐름 도구를 사용 하는 질문에 대답 시작 tooget 초기 페이지 뷰 또는 사용자 지정 이벤트 tooserve hello 시작 hello 시각화에 대 한 지점으로 선택 합니다.
1. Hello hello 링크를 클릭 "않으면 사용자가 수행할 작업 후...?" 제목, 또는 hello 편집 단추를 클릭 합니다. 
2. Hello "초기 이벤트" 드롭다운에서 페이지 보기 또는 사용자 지정 이벤트를 선택 합니다.
3. "그래프 만들기"를 클릭합니다.

hello 시각화의 hello "1 단계" 열 어떤 사용자가 점에 만족 하셨나요 가장 자주 위쪽에서 아래쪽에서 대부분 tooleast를 자주 정렬 hello 초기 이벤트 바로 다음을 표시 합니다. 사이트를 통해 어떤 사용자가 그 후 모든 hello 방법으로 사용자의 사진 만드는 hello "2 단계" 및 그 열 표시 탐색 합니다.

기본적으로 hello 사용자 흐름 도구만 hello를 페이지 보기 및 사이트에서 사용자 지정 이벤트의 지난 24 시간 동안 임의로 샘플링합니다. Hello 시간 범위를 늘리고 hello 편집 메뉴에서 무작위 샘플링에 대 한 성능 및 정확도의 hello 균형을 변경할 수 있습니다.

일부 hello 페이지 뷰 및 사용자 지정 이벤트 관련 tooyou 하지 않으면 hello "X"를 클릭 하려는 toohide hello 노드에서 합니다. 원하는 toohide hello 노드를 선택한 후에 hello 시각화 아래 hello "그래프 만들기" 단추를 클릭 합니다. toosee 모든 hello 노드가 숨겨진 hello 편집 단추를 클릭 하 여 다음에 hello "이벤트 제외" 섹션을 참조 합니다.

페이지 뷰 또는 사용자 지정 이벤트는 누락 된 hello 시각화에서 toosee 예상:
* Hello hello 편집 메뉴에서 "제외 된 이벤트" 섹션을 확인 합니다.
* Hello 편집 메뉴 tooinclude 작음-자주 사용 하는 이벤트 hello 시각화에서에서 hello "세부 정보 수준" 컨트롤을 사용 합니다.
* Hello 페이지 보기 또는 원하는 사용자 지정 이벤트는 사용자가 자주 전달 되 면 hello 편집 메뉴에서 hello 시각화의 증가 hello 시간 범위를 시도 합니다.
* 있는지 hello 페이지 보기 또는 hello Application Insights SDK 사이트의 hello 소스 코드에 의해 수집 된 toobe 설정 하려는 사용자 지정 이벤트를 확인 합니다. [사용자 지정 이벤트 수집에 대해 자세히 알아봅니다.](app-insights-api-custom-events-metrics.md)

원하는 경우 hello 시각화를 사용 하 여 hello "단계 수가" 슬라이더 hello에서의 단계를 자세히 toosee 메뉴를 편집 합니다.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>페이지 또는 기능을 방문한 후에 사용자가 어디로 이동하고 어떤 항목을 클릭하나요?

![사용자가 클릭할 수 있는 toounderstand 사용자 흐름 사용](./media/app-insights-usage-flows/flows-one-step.png)

초기 이벤트 페이지 보기 이면 hello 시각화의 hello 첫 번째 열 ("단계 1")는 hello 페이지를 방문한 직후 사용자가 신속 하 게 toounderstand 합니다. 창 다음 toohello 사용자 흐름 시각화에서에서 사이트를 열어 보십시오. 사용자가 hello "1 단계" 열에 있는 이벤트 목록은 페이지 toohello hello 상호 작용 하는 방법의 예상과 다를 비교 합니다. 종종 무효 tooyour 팀 보이는 hello 페이지에는 UI 요소는 hello 페이지에서 대부분 사용 하는 hello 간에 수 있습니다. 디자인 개선 tooyour 사이트에 대 한 좋은 시작 지점 수 있습니다.

초기 이벤트는 사용자 지정 이벤트, 사용자가 해당 작업을 수행 하는 바로 뒤 म hello 첫 번째 열 표시 됩니다. 페이지 보기와 마찬가지로 경우 hello 동작의 사용자 일치 팀의 목표와 기대치를 관찰 하는 것이 좋습니다. 선택한 초기 이벤트 "Added 항목 tooShopping 카트" 예를 들어 확인 toosee 경우 "Go tooCheckout" 및 "완료 구매" hello 시각화 잠시 후에 표시 합니다. 사용자 동작이 예상과 다를 경우 hello 시각화 toounderstand 어떻게 사용자는 가져오는 "트랩" 현재 사이트의 설계를 사용 합니다.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>사용자가 사이트에서 가장 변동는 배치 있는 hello?

높은 접속 나타나는 "세션이 종료" 노드에 대 한 조사식 흐름 특히 초기에 hello 시각화의 열에서입니다. 이 많은 사용자가 다음 페이지와 상호 작용 UI의 이전 경로 hello 후 사이트에서 churned 것을 의미 합니다. 예를 들어, 전자 상거래 사이트에서 구매를 완료한 후와 같은 경우 종종 변동이 예상됩니다. 하지만 변동은 일반적으로 설계 상의 문제, 성능 저하 또는 개선될 수 있는 사이트 관련 기타 문제를 의미합니다.

"종료된 세션" 노드가 이 Application Insights 리소스에 의해 수집된 원격 분석에만 기반한다는 점을 기억합니다. Application Insights는 특정 사용자 상호 작용에 대 한 원격 분석을 받지 못하면, 사용자 수 여전히 있는와 상호 작용할 이러한 방법으로 사이트 hello 사용자 흐름 도구 표시 hello 세션이 종료 된 후입니다.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>여기서 사용자가 반복 hello 동일한 작업을 반복 하는 장소 있습니까?

페이지 보기 또는 hello 시각화의 후속 단계를 통해 많은 사용자가 반복 되는 사용자 지정 이벤트를 찾아보십시오. 즉, 일반적으로 사용자가 사이트에서 반복 작업을 수행하고 있습니다. 반복을 찾을 경우 사이트의 hello 디자인을 변경 하거나 새 기능 tooreduce 반복을 추가 하는 방법에 대 한 생각 합니다. 예를 들어 테이블 요소의 각 행에서 반복되는 동작을 수행하는 사용자를 발견한 경우 대량 편집 기능을 추가합니다.

## <a name="common-questions"></a>일반적인 질문

### <a name="why-do-steps-appear-disconnected"></a>단계의 연결이 끊기는 이유는 무엇인가요?

![단계의 연결이 끊긴 사용자 흐름](./media/app-insights-usage-flows/flows-disconnected.png)

단계 (열) 사용자 흐름 시각화에서 연결이 끊긴 경우 자주 수행 하도록 toobe 표시 된 hello 단계 사이 사용자를 차지 하는 hello 경로 없음 의미 합니다. 덜 자주 이벤트 hello 시각화에서 tooshow hello 단계 연결 됨, 표시 슬라이더를 조정 hello "세부 정보 수준" hello 편집 메뉴에서.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Hello 초기 이벤트 나타내는 hello 첫 번째 시간 hello 이벤트 세션에서 나타납니다 또는 세션에 나타나는 언제 든 지?

hello hello 시각화에서 초기 이벤트는만 hello를 세션 중 해당 페이지 보기 또는 사용자 지정 이벤트를 전송 하는 사용자는 처음으로 나타냅니다. 사용자가 세션에서 여러 번 hello 초기 이벤트를 보낼 수 있으면 hello "1 단계" 열만 hello 후 사용자가 동작 하는 방법을 보여 줍니다 *첫 번째* 초기 이벤트의 인스턴스, 모든 인스턴스.

## <a name="next-steps"></a>다음 단계

* [사용 현황 개요](app-insights-usage-overview.md)
* [사용자, 세션 및 이벤트](app-insights-usage-segmentation.md)
* [보존](app-insights-usage-retention.md)
* [사용자 지정 이벤트 tooyour 앱 추가](app-insights-api-custom-events-metrics.md)
