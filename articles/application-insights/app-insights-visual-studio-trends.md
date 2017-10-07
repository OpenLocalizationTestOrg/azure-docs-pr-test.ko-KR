---
title: "Visual Studio에서 aaaAnalyzing 추세 | Microsoft Docs"
description: "Visual Studio의 Application Insights 원격 분석에서 추세를 분석, 시각화 및 탐색합니다."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Visual Studio에서 추세 분석
hello Application Insights 추세 도구는 웹 응용 프로그램의 중요 한 원격 분석 이벤트에 따라 어떻게 변경 시간, 문제 및 비정상을 신속 하 게 식별 하는 데 도움이 시각화 합니다. 자세한 진단 정보를 toomore를 연결 하 여 추세 도와 앱의 성능을 향상 시킬, 예외의 원인을 hello 추적 하 고, 사용자 지정 이벤트를 발견 합니다.

![예제 추세 창](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Application Insights의 웹앱 구성

이 작업을 아직 수행하지 않은 경우 [Application Insights의 웹앱을 구성](app-insights-overview.md)합니다. 그러면이 toosend 원격 분석 toohello Application Insights 포털. hello 추세 도구에서에서 hello 원격 분석을 읽습니다.

Application Insights 추세는 Visual Studio 2015 업데이트 3 이상에서 사용할 수 있습니다.

## <a name="open-application-insights-trends"></a>Application Insights 추세 열기
tooopen hello Application Insights 추세 창:

* Hello Application Insights 도구 모음 단추를 선택 **원격 분석 추세 탐색**, 또는
* Hello 프로젝트 상황에 맞는 메뉴에서 선택 **Application Insights > 원격 분석 추세 탐색**, 또는
* Hello Visual Studio 메뉴 모음에서 **보기 > 다른 창 > Application Insights 추세**합니다.

프롬프트 tooselect 리소스를 볼 수 있습니다. 클릭 **리소스 선택**, Azure 구독을 사용 하 여 로그인 한 다음 하려는 tooanalyze 원격 분석 추세 hello 목록에서 Application Insights 리소스를 선택 합니다.

## <a name="choose-a-trend-analysis"></a>추세 분석 선택
![일반적인 유형의 추세 분석 메뉴](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

5 개의 일반적인 추세 분석을 hello 지난 24 시간 동안에서에서 각 분석 데이터 중 하나를 선택 하 여 시작 하려면:

* **서버 요청 된 성능 문제를 조사** -만든 tooyour 서비스, 응답 시간으로 그룹화 된 요청
* **서버 요청에서 오류를 분석** -만든 tooyour 서비스, HTTP 응답 코드로 그룹화 된 요청
* **응용 프로그램에서 hello 예외를 검사** -예외 유형별로 그룹화 된, 서비스에서 예외
* **응용 프로그램의 종속성의 hello 성능을 검사 하 여** -응답 시간으로 그룹화 된 서비스에 의해 호출 된 서비스
* **사용자 지정 이벤트 검사** - 서비스에 대해 설정한 사용자 지정 이벤트로, 이벤트 유형별로 그룹화됨

Hello에서 나중에 사용할 수 있는 분석을 미리 만들어진이 **일반적인 유형의 원격 분석을 보려면** hello 추세 창의 hello 왼쪽 위 모퉁이의 단추입니다.

## <a name="visualize-trends-in-your-application"></a>응용 프로그램에서 추세 시각화
Application Insights 추세는 앱의 원격 분석으로부터 시계열 시각화를 만듭니다. 각 시계열 시각화는 어떤 시간 범위 동안 한 원격 분석 유형을 표시하며, 해당 원격 분석의 한 가지 속성으로 그룹화됩니다. 예를 들어 있는 + hello 지난 24 시간 동안 통해 hello 국가로 그룹화 된, tooview 서버 요청 좋습니다. 이 예제에서는 hello 시각화에서 각 거품은 1 시간 동안 일부 국가/지역에 대 한 hello 서버 요청 수를 나타냅니다.

어떤 유형의 원격 분석 보면 hello 창 tooadjust hello 맨 hello 컨트롤을 사용 합니다. 첫째, 관심이 있는 hello 원격 분석 유형을 선택 합니다.

* **원격 분석 유형** - 서버 요청, 예외, 종속성 또는 사용자 지정 이벤트
* **시간 범위** -hello 마지막 30 분 toohello 지난 3 일에서 아무 곳 이나
* **그룹별** - 예외 형식, 문제 ID, 국가/지역 등

클릭 **원격 분석** toorun hello 쿼리 합니다.

hello 시각화에서 거품 사이의 toonavigate:

* Tooselect hello hello 특정 기간 동안 발생 한 정당한 hello 이벤트 요약 hello 창 맨 아래에 필터를 업데이트 하는 한 거품을 클릭 합니다.
* 거품형 toonavigate toohello 검색 도구를 두 번 클릭 하 고 모든 해당 시간 동안 발생 하는 hello 개별 원격 이벤트 표시
* Ctrl 키를 누른 채 클릭 거품형 toode 선택 hello 시각화에서 합니다.

> [!TIP]
> 추세와 검색 hello 도구가 함께 작동 toohelp 수천 개의 원격 분석 이벤트 간에 서비스에서 문제의 원인 hello를 정확히 파악 합니다. 예를 들어, 어느 날 오후 고객이 앱의 응답 속도 저하를 인지한 경우 추세를 시작합니다. 경과 따른 tooyour 서비스 hello 지난 수 시간, 응답 시간을 기준으로 그룹화 된 요청을 분석 합니다. 비정상적으로 큰 느린 요청 클러스터가 있는지 확인합니다. 다음 두 번 해당 거품 toogo toohello 검색 도구를 필터링 된 toothose 요청 이벤트를 클릭 합니다. 검색에서 이러한 요청 hello 내용을 탐색 및 toohello 코드를 탐색할 수 tooresolve hello 문제를 포함 합니다.
> 
> 

## <a name="filter"></a>Filter
Hello 필터 컨트롤이 hello hello 창 맨 아래에 있는 보다 구체적인 추세를 검색 합니다. tooapply 필터를 해당 이름을 클릭 합니다. 원격 분석의 특정 차원에 숨어 있을 수도 있습니다는 서로 다른 필터가 toodiscover 추세 간에 빠르게 전환할 수 있습니다. 예외 유형, 같은 차원이 두 개에 필터를 적용 하는 경우 흐리게 표시 있지만 다른 차원에서 필터 클릭할 수 있는 유지 됩니다. tooun-, 필터를 적용 한 다음 다시 클릭 합니다. Ctrl + 클릭 tooselect 여러 필터 hello 동일한 차원입니다.

![추세 필터](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

어떻게 할까요 tooapply 여러 필터? 

1. Hello 첫 번째 필터를 적용 합니다. 
2. Hello 클릭 **선택한 필터를 적용 하 고 다시 쿼리** 첫 번째 필터의 hello 차원 hello 이름별 단추입니다. 이것은 hello 첫 번째 필터와 일치 하는 이벤트만 대 한 원격 분석 다시 쿼리 합니다. 
3. 두 번째 필터를 적용합니다. 
4. 원격 분석의 특정 하위 집합의 hello 프로세스 toofind 추세를 반복 합니다. 예를 들어, "GET Home/Index"라는 서버 요청 *및* 독일에서 발생한 서버 요청 *및* 500 응답 코드를 수신한 서버 요청입니다. 

tooun-이러한 필터 중 하나를 적용을 hello 클릭 **선택한 필터를 제거 하 고 다시 쿼리** hello 차원에 대 한 단추입니다.

![여러 필터](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>잘못된 부분을 찾기
hello 추세 도구 비정상적인 비교 tooother 거품 hello에 있는 이벤트의 거품을 강조 표시할 수 시계열 동일 합니다. Hello 보기 형식 드롭다운에서 선택 **시간 버킷의 (변칙 강조 표시)** 또는 **(변칙 강조 표시) 시간 버킷의 백분율**합니다. 빨간색 거품이 잘못된 것입니다. 변칙은 2.1 회 이상 hello hello 개수/비율의 hello (48 시간 hello를 보는 경우 지난 24 시간, 등입니다.)의 두 시점 이전에 발생 한 표준 편차의 횟수/백분율로 거품으로 정의 됩니다.

![컬러 점은 잘못된 부분을 나타냅니다.](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> 잘못된 부분을 강조 표시하면, 그렇지 않은 경우 비슷하게 보일 수 있는 작은 거품의 시계열에서 이상값을 찾는 데 특히 유용합니다.  
> 
> 

## <a name="next"></a>다음 단계
|  |  |
| --- | --- |
| **[Visual Studio Online에서 Application Insights로 작업](app-insights-visual-studio.md)**<br/>원격 분석을 검색하고, CodeLens에서 데이터를 확인하며, Application Insights를 구성합니다. Visual Studio 내에서 모두 수행할 수 있습니다. |![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights 선택 검색](./media/app-insights-visual-studio-trends/34.png) |
| **[더 많은 데이터 추가](app-insights-asp-net-more.md)**<br/>사용량, 가용성, 종속성, 예외를 모니터링합니다. 로깅 프레임 워크의 추적을 통합합니다. 사용자 지정 원격 분석을 작성합니다. |![Visual studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Hello Application Insights 포털 작업](app-insights-dashboards.md)**<br/>대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 원격 분석 내보내기입니다. |![Visual studio](./media/app-insights-visual-studio-trends/62.png) |

