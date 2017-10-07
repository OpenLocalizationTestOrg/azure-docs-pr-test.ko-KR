---
title: "aaaDashboards 및 탐색 hello Azure Application Insights | Microsoft Docs"
description: "키 APM 차트 및 쿼리의 뷰를 만듭니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>탐색 및 hello Application Insights 포털의 대시보드
구성한 후 [프로젝트에 Application Insights 설정](app-insights-overview.md), hello에 프로젝트의 Application Insights 리소스에 앱의 성능 및 사용에 대 한 원격 분석 데이터가 표시 됩니다 [Azure 포털](https://portal.azure.com)합니다.

## <a name="find-your-telemetry"></a>원격 분석 찾기
Toohello 로그인 [Azure 포털](https://portal.azure.com) 응용 프로그램에 대해 만든 toohello Application Insights 리소스를 이동 합니다.

![찾아보기를 클릭하고 Application Insights를 선택한 후 앱을 선택합니다.](./media/app-insights-dashboards/00-start.png)

앱에 대 한 hello 개요 블레이드에 (페이지) 응용 프로그램의 주요 진단 메트릭 hello에 대 한 요약이 표시 되며 게이트웨이 toohello hello 포털의 다른 기능.

![주요 경로 tooview 원격 분석](./media/app-insights-dashboards/010-oview.png)

Hello 차트와 표 중 하나를 사용자 지정할 수 있으며 tooa 대시보드에 고정 합니다. 이런 방식으로 가져올 수 있습니다 함께 hello 키 원격 분석에서 다른 앱의에서 중앙 대시보드에서.

## <a name="dashboards"></a>대시보드
hello 먼저 표시 toohello 로그인 한 후 [Microsoft Azure 포털](https://portal.azure.com) 는 한 대시보드입니다. 여기 수 모아 놓은에서 원격 분석을 포함 하 여 모든 Azure 리소스를 통해 가장 중요 한 tooyou hello 차트 [Azure Application Insights](app-insights-overview.md)합니다.

![사용자 지정 대시보드입니다.](./media/app-insights-dashboards/31.png)

1. **Toospecific 리소스 이동** Application Insights에서 응용 프로그램 같은: hello 왼쪽된 막대 사용 합니다.
2. **반환 toohello 현재 대시보드**, tooother 최근 보기를 전환 하거나: 왼쪽 위에 hello 드롭 다운 메뉴를 사용 합니다.
3. **대시보드 전환**: hello 대시보드 제목에 사용 하 여 hello 드롭 다운 메뉴
4. **만들기, 편집 및 대시보드를 공유** hello 대시보드 도구 모음에 있습니다.
5. **Hello 대시보드 편집**: 타일 위로 마우스를 가져가고 다음 위쪽을 사용 하 여 toomove, 막대를 사용자 지정 하거나 제거 합니다.

## <a name="add-tooa-dashboard"></a>Tooa 대시보드를 추가 합니다.
블레이드 또는 특히 흥미롭습니다 되 차트는 집합을 원하는 경우 toohello 대시보드는 해당 복사본을 고정할 수 있습니다. 이 경우 다음에 대시보드로 돌아가면 해당 블레이드나 차트가 표시됩니다.

![toopin 차트 위로 마우스를 hello 헤더에 "..."를 클릭 합니다.](./media/app-insights-dashboards/33.png)

1. 차트 toodashboard를 고정 합니다. Hello 차트의 복사본 hello 대시보드에 나타납니다.
2. Pin hello 전체 블레이드 toohello 대시보드-hello 대시보드에서으로 나타납니다 타일 클릭 광고할 수 있습니다.
3. Hello 왼쪽된 위 모서리 tooreturn toohello 현재 대시보드를 클릭 합니다. 그런 다음 hello 드롭 다운 메뉴 tooreturn toohello 현재 보기를 사용할 수 있습니다.

차트는 타일로 그룹화되고 타일은 둘 이상의 차트를 포함할 수 있습니다. Hello 전체 타일 toohello 대시보드에 고정합니다.

hello 차트의 시간 범위에 따라 달라 지는 주파수에 hello 차트 자동으로 새로 고쳐집니다.

* 시간 범위를 too1 시간: 5 분 마다 새로 고침
* 시간 범위 1 - 24시간: 15분마다 새로 고침
* 시간 범위 24시간 초과: (시간 범위)/60

### <a name="pin-any-query-in-analytics"></a>분석에서 모든 쿼리를 고정
수도 있습니다 [분석 고정](app-insights-analytics-using.md#pin-to-dashboard) 차트 tooa [공유](#share-dashboards-with-your-team) 대시보드 합니다. 이렇게 하면 표준 메트릭이 hello와 함께 임의의 쿼리의 tooadd 차트 있습니다. 

결과는 1시간마다 자동으로 다시 계산됩니다. 즉시 hello 차트 toorecalculate에 hello 새로 고침 아이콘을 클릭 합니다. 브라우저 새로 고침은 다시 계산하지 않습니다.

## <a name="adjust-a-tile-on-hello-dashboard"></a>Hello 대시보드의 타일을 조정 합니다.
Hello 대시보드에서 타일 되 면이 조정할 수 있습니다.

![마우스로 순서 tooedit에서 차트 것입니다.](./media/app-insights-dashboards/36.png)

1. 차트 toohello 타일을 추가 합니다.
2. Hello 메트릭과 group by 차원 (테이블, 그래프)는 차트 스타일을 설정 합니다.
3. Hello 다이어그램 toozoom; 위를 끕니다. hello 실행 취소 단추 tooreset hello timespan;를 클릭 합니다. hello 타일 hello 차트에 대 한 필터 속성을 설정 합니다.
4. 타일 제목을 설정합니다.

메트릭 탐색기 블레이드에서 고정된 타일에는 개요 블레이드에서 고정된 타일보다 편집 옵션이 많이 있습니다.

고정 hello 원래 타일 편집 영향을 받지 않습니다.

## <a name="switch-between-dashboards"></a>대시보드 사이 전환
둘 이상의 대시보드를 저장하고 해당 대시보드 간에 전환할 수 있습니다. 차트 또는 블레이드를 고정 하면 toohello 현재 대시보드를 추가 됩니다.

![대시보드, 간의 tooswitch 대시보드를 클릭 하 고 저장 된 대시보드를 선택 합니다. toocreate 새 대시보드 저장 하 고, 새로 만들기를 클릭 합니다. toorearrange, 편집을 클릭 합니다.](./media/app-insights-dashboards/32.png)

예를 들어 하나의 대시보드에서 hello 단체 방을 만들고 일반 개발에 대해 다른 전체 화면을 표시 하기 위해 할 수 있습니다.

Hello 대시보드에서 블레이드를 타일 형태로 표시: toogo toohello 블레이드를 클릭 합니다. 차트에는 hello 차트 원래 위치에 복제합니다.

![나타내는 타일 tooopen hello 블레이드를 클릭 합니다.](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>대시보드 공유
대시보드를 만들면 다른 사용자와 공유할 수 있습니다.

![Hello 대시보드 헤더에서 공유를 클릭 합니다.](./media/app-insights-dashboards/41.png)

[역할 및 액세스 제어](app-insights-resources-roles-access-control.md)에 대해 알아보세요.

## <a name="app-navigation"></a>앱 탐색
hello 개요 블레이드에 앱에 대 한 hello 게이트웨이 toomore 정보입니다.

* **모든 차트 또는 타일** -모든 타일을 클릭 하거나 차트 toosee 표시 되는 내용에 대 한 자세한 정보.

### <a name="overview-blade-buttons"></a>개요 블레이드 단추
![개요 블레이드 위쪽 탐색 모음](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**메트릭 탐색기**](app-insights-metrics-explorer.md) - 성능 및 사용에 대한 사용자 고유의 차트를 만듭니다.
* [**검색**](app-insights-diagnostic-search.md) - 요청, 예외 또는 로그 추적과 같은 이벤트의 특정 인스턴스를 조사할 수 있습니다.
* [**분석**](app-insights-analytics.md) - 원격 분석을 통해 강력한 쿼리를 합니다.
* **시간 범위** -hello 블레이드의 모든 hello 차트에서 표시 하는 hello 범위를 조정 합니다.
* **삭제** -이 앱에 대 한 hello Application Insights 리소스를 삭제 합니다. 또한 인해 앱 코드에서 hello Application Insights 패키지를 제거 하거나 hello 편집 [계측 키](app-insights-create-new-resource.md#copy-the-instrumentation-key) 앱 toodirect 원격 분석 tooa 다른 Application Insights 리소스에 있습니다.

### <a name="essentials-tab"></a>Essentials 탭
* [계측 키](app-insights-create-new-resource.md#copy-the-instrumentation-key) - 이 앱 리소스를 식별합니다.
* 가격 - 기능을 사용할 수 있게 하고 볼륨 한도를 설정합니다.

### <a name="app-navigation-bar"></a>앱 탐색 모음
![왼쪽 탐색 모음](./media/app-insights-dashboards/app-left-nav-bar.png)

* **개요** -응용 프로그램 개요 블레이드에 toohello 반환 합니다.
* **활동 로그** - 경고 및 Azure 관리 이벤트입니다.
* [**액세스 제어** ](app-insights-resources-roles-access-control.md) -tooteam 멤버에 액세스 하 고 다른 사용자를 제공 합니다.
* [**태그** ](../azure-resource-manager/resource-group-using-tags.md) -사용 하 여 태그 toogroup 다른 사용자와 응용 프로그램입니다.

조사

* [**응용 프로그램 맵** ](app-insights-app-map.md) -응용 프로그램의 hello 구성 요소를 보여 주는 활성 맵 hello 종속성 정보에서 파생 됩니다.
* [**스마트 감지**](app-insights-proactive-diagnostics.md) - 최근 성능 경고를 검토합니다.
* [**라이브 스트림**](app-insights-live-stream.md) - 거의 즉각적인 고정된 메트릭 집합을 제공하며, 새 빌드를 배포 또는 디버깅할 때 유용합니다.
* [**가용성 웹 테스트 /** ](app-insights-monitor-web-app-availability.md) -송신 일반 요청 tooyour 웹 응용 프로그램에서 hello world.* 주위
* [**오류, 성능** ](app-insights-web-monitor-performance.md) -예외, 실패율 및 응답 시간이 응용 프로그램의 요청 및 요청 tooyour 응용 프로그램에 대 한 너무[종속성](app-insights-asp-net-dependencies.md)합니다.
* [**성능**](app-insights-web-monitor-performance.md) - 응답 시간, 종속성 응답 시간입니다.
* [서버](app-insights-web-monitor-performance.md) - 성능 카운터입니다. [상태 모니터를 설치하면](app-insights-monitor-performance-live-website-now.md)사용할 수 있습니다.
* **브라우저** - 페이지 뷰 및 AJAX 성능입니다. [웹 페이지를 계측할 때](app-insights-javascript.md)사용할 수 있습니다.
* **사용** - 페이지 조회수, 사용자 및 세션 수입니다. [웹 페이지를 계측할 때](app-insights-javascript.md)사용할 수 있습니다.

구성

* **시작하기** - 인라인 자습서입니다.
* **속성** - 계측 키, 구독 및 리소스 ID입니다.
* [경고](app-insights-alerts.md) -메트릭 경고 구성입니다.
* [연속 내보내기를](app-insights-export-telemetry.md) -의 원격 분석 tooAzure 저장소 내보내기를 구성 합니다.
* [성능 테스트](app-insights-monitor-web-app-availability.md#performance-tests) -웹 사이트에 대한 종합 부하를 설정 합니다.
* [할당량 및 가격 책정](app-insights-pricing.md)과 [수집 샘플링](app-insights-sampling.md)입니다.
* **API 액세스** -만들 [주석 릴리스](app-insights-annotations.md) 및 데이터 액세스 API hello에 대 한 합니다.
* [**작업 항목** ](app-insights-diagnostic-search.md#create-work-item) -tooa 작업 추적 원격 분석을 검사 하는 동안 버그를 만들 수 있도록 시스템을 연결 합니다.

설정

* [**잠금**](../azure-resource-manager/resource-group-lock-resources.md) - Azure 리소스를 잠급니다.
* [**자동화 스크립트** ](app-insights-powershell.md) -템플릿 toocreate 새 리소스 그룹으로 사용할 수 있도록 hello Azure 리소스에 대 한 정의 내보냅니다.


## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>다음 단계

|  |  |
| --- | --- |
| [메트릭 탐색기](app-insights-metrics-explorer.md)<br/>필터 및 세그먼트 메트릭 |![검색 예제](./media/app-insights-dashboards/64.png) |
| [진단 검색](app-insights-diagnostic-search.md)<br/>이벤트 찾기 및 검사, 관련 이벤트, 버그 만들기 |![검색 예제](./media/app-insights-dashboards/61.png) |
| [분석](app-insights-analytics.md)<br/>강력한 쿼리 언어 |![검색 예제](./media/app-insights-dashboards/63.png) |
