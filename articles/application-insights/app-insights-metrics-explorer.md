---
title: "Azure Application Insights에서 메트릭 aaaExploring | Microsoft Docs"
description: "메트릭 탐색기 차트 toointerpret 방법 등에 toocustomize 메트릭 탐색기 블레이드입니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Application Insights에서 메트릭 탐색
[Application Insights][start]의 메트릭은 응용 프로그램의 원격 분석에서 전송된 측정된 값 및 이벤트 수입니다. 성능 문제를 감지하고 응용 프로그램 사용 방식의 추세를 볼 수 있습니다. 다양한 표준 메트릭이 있으며 사용자 고유의 사용자 지정 메트릭 및 이벤트를 만들 수도 있습니다.

메트릭 및 이벤트 수는 합계, 평균 또는 개수 등의 집계된 값에 대한 차트에 표시됩니다.

다음은 차트의 샘플 집합입니다.

![](./media/app-insights-metrics-explorer/01-overview.png)

Hello Application Insights 포털에서 메트릭 차트에 모든 위치에서 찾을 있습니다. 대부분의 경우에서은 사용자 지정할 수 있습니다, 그리고 및 더 많은 차트 toohello 블레이드를 추가할 수 있습니다. Hello 개요 블레이드에에서 클릭 하 여 toomore 세부 (예: "서버" 제목이 없는 경우)는 차트, 하거나 클릭 **메트릭 탐색기** tooopen는 새 블레이드가 사용자 지정 차트를 만들 수 있습니다.

## <a name="time-range"></a>시간 범위
Hello hello 차트 또는 표에 모든 블레이드를 여는 시간 범위를 변경할 수 있습니다.

![Hello Azure 포털에서에서 응용 프로그램의 열린 hello 개요 블레이드](./media/app-insights-metrics-explorer/03-range.png)

일부 데이터가 표시되어야 하지만 아직 표시되지 않은 경우 새로 고침을 클릭합니다. 차트 자체 간격에 따라 새로 고침 하지만 hello 간격을 더 큰 시간 범위에 대해 긴 하 합니다. 차트에는 hello 분석 파이프라인을 통해 데이터 toocome 데 시간이 걸릴 수 있습니다.

차트의 일부분으로 toozoom 위로 끕니다.

![차트의 일부를 끕니다.](./media/app-insights-metrics-explorer/12-drag.png)

확대/축소 실행 취소 단추 toorestore hello 클릭 것입니다.

## <a name="granularity-and-point-values"></a>세분성 및 지점 값
마우스를 포인터로 hello 차트 toodisplay hello 값 hello 메트릭의 시점입니다.

![차트 위로 hello 마우스를 가져가고](./media/app-insights-metrics-explorer/02-focus.png)

특정 지점에서 hello 메트릭의 hello 값 hello 앞에 샘플링 간격에 걸쳐 집계 됩니다.

hello 샘플링 간격 또는 "세분성" hello hello 블레이드 위쪽에 표시 됩니다.

![블레이드의 hello 헤더입니다.](./media/app-insights-metrics-explorer/11-grain.png)

Hello 시간 범위 블레이드에서 hello 세분성을 조정할 수 있습니다.

![블레이드의 hello 헤더입니다.](./media/app-insights-metrics-explorer/grain.png)

사용 가능한 hello 세분성 hello 시간 범위 선택에 따라 다릅니다. 안녕하세요 명시적 세분성은 hello 시간 범위에 대 한 대안 toohello "자동" 세분성입니다.


## <a name="editing-charts-and-grids"></a>차트 및 표 편집
새 차트 toohello 블레이드 tooadd:

![메트릭 탐색기에서 추가 차트 선택](./media/app-insights-metrics-explorer/04-add.png)

선택 **편집** 는 기존 또는 새 차트 tooedit에 어떤 보여 줍니다.

![하나 이상의 메트릭 선택](./media/app-insights-metrics-explorer/08-select.png)

함께 표시 될 수 있는 hello 조합에 대 한 제한 된 경우에 차트에서 메트릭을 하나 이상 표시할 수 있습니다. 메트릭을 하나, 일부 hello 다른 사람이 사용할 수 없습니다 선택.

코딩 하는 경우 [사용자 지정 메트릭] [ track] (호출 tooTrackMetric 및 TrackEvent) 앱에은 여기에 나열 됩니다.

## <a name="segment-your-data"></a>데이터 분할
메트릭 속성-서로 다른 운영 체제 클라이언트에서 페이지 보기 예를 들어 toocompare로 분할할 수 있습니다.

차트 또는 그리드 선택 하 고 그룹화에 전환 하 여 속성 toogroup 선택:

![그룹화를 선택한 다음 그룹별에서 속성 선택](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> 그룹화를 사용 하는 경우 hello 영역 및 가로 막대형 차트 종류는 누적된 디스플레이 제공 합니다. 적합 한 hello 집계 메서드는 Sum입니다. 하지만 hello 집계 형식은 평균이 두 hello 선 또는 눈금 표시 형식을 선택 합니다.
>
>

코딩 하는 경우 [사용자 지정 메트릭] [ track] 앱에 속성 값을 포함 하 고, hello 목록에서 수 tooselect hello 속성 수 있습니다.

Hello 차트 너무 작으면 분할 된 데이터에 대 한? 높이 조정:

![Hello 슬라이더를 조정 합니다.](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>집계 형식
일반적으로 기본적으로 hello 측면에 대 한 hello 범례를 차트 hello hello 일정 기간 동안 집계 hello 값을 보여줍니다. Hello 차트를 마우스로 가리키면 경우 hello 값 해당 시점에 표시 합니다.

Hello 차트에서 각 데이터 요소에는 hello 샘플링 간격 또는 "세분성" 앞에 수신 hello 데이터 값에 대 한 집계입니다. hello 세분성 hello hello 블레이드 위쪽에 표시 되 고 hello 따라 달라 지 며 hello 차트의 전체 시간 간격입니다.

메트릭은 다른 방법으로 집계할 수 있습니다.

* **Count** 는 hello 샘플링 간격에서 받은 hello 이벤트의 개수입니다. 요청과 같은 이벤트에 사용됩니다. Hello 높이 hello 차트의 변형 hello 이벤트가 발생 하는 hello 속도 변형을 나타냅니다. 하지만 hello 샘플링 간격을 변경 하면 hello 숫자 값이 바뀝니다.
* **Sum** hello 샘플링 간격 또는 hello 차트의 hello 기간을 통해 받은 모든 hello 데이터 요소의 hello 값을 추가 합니다.
* **평균** 나눕니다 hello 간격을 통해 받은 데이터 요소의 hello 번호로 Sum hello 합니다.
* **고유** 개수는 사용자 및 계정의 수를 세는 데 사용됩니다. Hello 샘플링 간격에 대해 또는 hello 차트 hello 기간에 걸쳐 hello 그림 해당 시간에 다른 사용자의 hello 수입니다.
* **%** - 각 집계의 백분율 버전은 세그먼트 차트에서만 사용됩니다. 총 hello 항상 too100 %를 추가 하 고 hello 차트 hello 상대적 기여도 전체의 다른 구성 요소를 표시 합니다.

    ![백분율 집계](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Hello 집계 유형 변경

![Hello 차트를 편집 하 고 집계를 선택](./media/app-insights-metrics-explorer/05-aggregation.png)

hello 기본 방법은 각 메트릭에 대 한 모든 메트릭을 선택 하지 않은 경우 또는 새 차트를 만들 때 표시 됩니다.

![모든 메트릭 toosee hello 기본값을 선택 취소](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Y축 고정 
기본적으로 차트는 hello 데이터 범위에서 toogive 양자 hello 값의 시각적 표현 되는 최대값까지 0부터 시작 하는 Y 축 값을 보여 줍니다. 하지만 일부 경우에 둘 이상의 값에 약간의 변경이 검사 하는 hello 퀀텀 흥미로운 toovisually 수도 있습니다. 같은 사용자 지정 항목에 대해이 사용 하이 여 hello y 축 범위 편집 기능 toopin hello y 축 최소값 또는 최대값 값 원하는 위치에 있습니다.
Y 축 범위가 설정 "고급 설정" 확인란 toobring hello 클릭

![고급 설정을 클릭하고, 사용자 지정 범위를 선택한 후 최소값 및 최대값 지정](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>데이터 필터링
속성 값의 선택된 된 집합에 대 한 정당한 hello 메트릭을 toosee:

![필터를 클릭하고 속성을 확장하여 값 선택](./media/app-insights-metrics-explorer/19-filter.png)

특정 속성에 대 한 모든 값을 선택 하지 않은 동일한 모두를 선택 하 여 hello에: 필터는 해당 속성에 있습니다.

각 속성 값과 함께 이벤트 알림 hello를 계산합니다. 한 속성의 값을 선택 하면 다른 속성 값이 조정 됩니다 함께 hello를 계산 합니다.

필터 블레이드 tooall hello 차트를 적용합니다. 다른 필터를 적용 하려는 경우 toodifferent 차트를 만들고 다른 메트릭 블레이드를 저장 합니다. 나란히 볼 수 있도록 차트 다른 블레이드 toohello 대시보드를 고정할 수 있습니다.

### <a name="remove-bot-and-web-test-traffic"></a>봇 및 웹 테스트 트래픽 제거
사용 하 여 hello 필터 **실제 또는 가상 트래픽** 확인 **실제**합니다.

**가상 트래픽 소스**로 필터링할 수도 있습니다.

### <a name="tooadd-properties-toohello-filter-list"></a>tooadd 속성 toohello 필터 목록
자신이 선택한 범주에 대 한 toofilter 원격 분석 하 시겠습니까? 예를 들어 사용자를 서로 다른 범주로 나누고 데이터를 이러한 범주로 분할하려고 할 수 있습니다.

[사용자 고유의 속성을 만듭니다](app-insights-api-custom-events-metrics.md#properties). 설정 된 [원격 분석 이니셜라이저](app-insights-api-custom-events-metrics.md#defaults) toohave SDK의 서로 다른 모듈에서 보낸 hello 표준 원격 분석을 포함 하 여 모든 원격 분석-에 나타납니다.

## <a name="edit-hello-chart-type"></a>Hello 차트 종류를 편집 합니다.
표와 그래프 간에 전환할 수 있습니다.

![표 또는 그래프를 선택한 다음 차트 종류 선택](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>매트릭 블레이드 저장
차트를 만든 경우 즐겨찾기로 저장합니다. 여부 tooshare 사용 하 여 다른 팀 멤버, 조직 계정을 사용 하는 경우 선택할 수 있습니다.

![즐겨찾기 선택](./media/app-insights-metrics-explorer/21-favorite-save.png)

toosee hello 블레이드를 다시 **이동 toohello 개요 블레이드에** 즐겨찾기를 엽니다.

![Hello 개요 블레이드에에서 즐겨찾기를 선택 합니다.](./media/app-insights-metrics-explorer/22-favorite-get.png)

저장을 상대 시간 범위를 선택한 경우 hello 블레이드 hello 최신 메트릭을 사용 하 여 업데이트 됩니다. 절대 시간 범위를 선택한 경우에 표시 됩니다 될 때마다 동일한 데이터 hello 합니다.

## <a name="reset-hello-blade"></a>Hello 블레이드를 다시 설정
블레이드를 편집 하는 경우 다음 원하는 tooget 백 toohello 원래 저장 집합 방금 재설정을 클릭 합니다.

![메트릭 탐색기의 hello 위쪽 hello 단추](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>라이브 메트릭 스트림

원격 분석을 더 빠르게 즉시 보려면 [라이브 스트림](app-insights-live-stream.md)을 엽니다. 대부분 메트릭 집계 hello 프로세스로 인해 몇 분 tooappear를 수행합니다. 반면 라이브 메트릭은 짧은 대기 시간에 최적화되었습니다. 

## <a name="set-alerts"></a>경고 설정
경고를 추가 하는 toobe 비정상적인 값이 모든 메트릭의 전자 메일 알림을 받습니다. Toosend hello 전자 메일 toohello 계정 관리자 또는 toospecific 전자 메일 주소를 선택할 수 있습니다.

![메트릭 탐색기에서 경고 규칙, 경고 추가 선택](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[경고에 대해 알아봅니다][alerts].


## <a name="continuous-export"></a>연속 내보내기
데이터를 외부에서 처리할 수 있도록 지속적으로 내보내려면 [연속 내보내기](app-insights-export-telemetry.md)를 사용하는 것이 좋습니다.

### <a name="power-bi"></a>Power BI
데이터도 다양 한 뷰를 사용 하도록 하려는 경우 다음을 할 수 있습니다 [tooPower BI 내보내기](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)합니다.

## <a name="analytics"></a>분석
[분석](app-insights-analytics.md) 더 다양 한 방식으로 tooanalyze 강력한 쿼리 언어를 사용 하 여 원격 분석 됩니다. Toocombine 또는 메트릭에서 결과 계산 하거나 응용 프로그램의 최근 성능 심층 탐구 수행 하는 경우 사용 합니다. 

메트릭 차트에서 hello 분석 아이콘 tooget 클릭할 수 있는 직접 toohello 동등한 분석 쿼리 합니다.

## <a name="troubleshooting"></a>문제 해결
*차트에 데이터가 표시되지 않습니다.*

* 필터는 hello 블레이드에서 tooall hello 차트를 적용합니다. 는 하나의 차트에 중점 동안 하지 않은 설정 하는 다른 모든 hello 데이터를 제외 하는 필터 있는지 확인 합니다.

    다른 차트에 서로 다른 필터가 tooset 원한다 면에서 만들 저장 다른 블레이드를 별도 즐겨찾기. 나란히 볼 수 있도록 해당를 toohello 대시보드에 고정할 수 있습니다.
* 차트 메트릭을 hello에 정의 되어 있지 않은 속성에 의해 그룹화 할 경우 다음 됩니다 아무 hello 차트에서. '그룹화 기준'을 지우거나 다른 그룹화 속성을 선택하세요.
* 성능 데이터(CPU, IO 속도 등)는 Java 웹 서비스, Windows 데스크톱 앱, [IIS Web Apps 및 서비스(상태 모니터를 설치한 경우)](app-insights-monitor-performance-live-website-now.md) 및 [Azure Cloud Services](app-insights-azure.md)에 사용할 수 있습니다. Azure 웹 사이트에는 사용할 수는 없습니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>다음 단계
* [Application Insights를 사용하여 사용량 모니터링](app-insights-web-track-usage.md)
* [진단 검색 사용](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
