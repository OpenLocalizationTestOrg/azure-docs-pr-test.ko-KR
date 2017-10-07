---
title: "Azure Application Insights에서 맵 aaaApplication | Microsoft Docs"
description: "응용 프로그램 구성 요소 간의 hello 종속성의 시각적 표현을 레이블이 Kpi 및 경고와 함께 표시 됩니다."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Application Insights의 응용 프로그램 맵
[Azure Application Insights](app-insights-overview.md), 응용 프로그램 구조는 응용 프로그램 구성 요소의 hello 종속성 관계의 시각적 레이아웃 합니다. 각 구성 요소를 보여 줍니다 Kpi toohelp 부하, 성능, 오류 및 경고와 같은 성능 문제 또는 실패를 발생 시키는 구성 요소를 검색 합니다. 모든 구성 요소 toomore에서 하나씩 클릭 하면 진단, 예: Application Insights 이벤트를 자세히 설명 합니다. 앱에서 Azure 서비스를 사용 하는 경우 SQL 데이터베이스 관리자 권장 구성 같은 tooAzure 진단을 통해 클릭할 수도 있습니다.

다른 차트와 마찬가지로 응용 프로그램 맵 toohello가 올바르게 작동 하는 Azure 대시보드를 고정할 수 있습니다. 

## <a name="open-hello-application-map"></a>응용 프로그램 맵 열기 hello
응용 프로그램에 대 한 hello 개요 블레이드에서 맵 열기 hello:

![앱 맵 열기](./media/app-insights-app-map/01.png)

![앱 맵](./media/app-insights-app-map/02.png)

hello 맵은 보여 줍니다.

* 가용성 테스트
* 클라이언트 측 구성 요소 (hello JavaScript SDK로 모니터링)
* 서버 쪽 구성 요소
* Hello 클라이언트 및 서버 구성의 종속성

종속성 링크 그룹을 확장하고 축소할 수 있습니다.

![축소](./media/app-insights-app-map/03.png)

SQL, HTTP 등 한 종류의 종속성이 많은 경우 그룹화되어 표시될 수 있습니다. 

![그룹화된 종속성](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>문제 발견
각 노드에 해당 구성 요소에 대 한 hello 부하, 성능 및 실패 속도 같은 관련 된 성능 지표입니다. 

경고 아이콘은 발생 가능한 문제를 강조 표시합니다. 주황색 경고는 요청, 페이지 보기 또는 종속성 호출에서 오류가 발생했음을 의미합니다. 빨간색 경고는 5% 이상의 실패율을 의미합니다. 이러한 임계값 tooadjust을 원하는 경우 옵션을 엽니다.

![오류 아이콘](./media/app-insights-app-map/04.png)

활성 경고도 다음과 같이 표시됩니다. 

![활성 경고](./media/app-insights-app-map/05.png)

SQL Azure를 사용하는 경우 성능을 향상시키는 방법에 대한 권장 사항이 있는 경우 나타나는 아이콘이 있습니다. 

![Azure 권장 사항](./media/app-insights-app-map/06.png)

자세한 내용은 모든 아이콘 tooget를 클릭 합니다.

![Azure 권장 사항](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>진단 클릭
각 hello 노드 hello 지도에 진단에 대 한 대상으로 지정 된 클릭 광고를 제공합니다. hello 옵션 hello hello 노드 유형에 따라 달라 집니다.

![서버 옵션](./media/app-insights-app-map/09.png)

Azure에서 호스트 되는 구성 요소에 대 한 hello 옵션에 대 한 직접 링크 toothem을 포함 됩니다.

## <a name="filters-and-time-range"></a>필터 및 시간 범위
기본적으로 hello 맵 hello 시간 범위 선택에 사용할 수 있는 모든 hello 데이터를 요약 합니다. 하지만 tooinclude만 특정 작업 이름 또는 종속성 필터링 할 수 있습니다.

* 작업 이름: 페이지 보기 및 서버 쪽 요청 형식을 모두 포함합니다. 이 옵션을 사용 hello 지도 표시만 hello 선택 작업에 대 한 hello 서버/클라이언트 쪽 노드에서 KPI를 hello 합니다. 이러한 특정 작업의 hello 컨텍스트에서 호출 hello 종속성을 표시 합니다.
* 종속성 기본 이름: hello AJAX 브라우저 종속성과 서버 쪽 종속성이 포함 됩니다. 사용자 지정 종속성 원격 분석 hello TrackDependency API로 보고 하는 경우 또한 여기에 나와 있습니다. Hello 맵에 종속성 tooshow hello를 선택할 수 있습니다. 현재이 옵션을이 선택 hello 서버 쪽 요청 또는 hello 클라이언트 쪽 페이지 보기에는 필터링 하지 않습니다.

![필터 설정](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>필터 저장
toosave hello 필터를 적용 한 pin hello 필터링 된 뷰는 [대시보드](app-insights-dashboards.md)합니다.

![Pin toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>오류 창
Hello 맵에서 노드를 클릭할 때 오류 창의 해당 노드에 대 한 오류 요약으로 hello 오른쪽에 표시 됩니다. 먼저 오류는 작업 ID별로 그룹화된 후 문제 ID별로 그룹화됩니다.

![오류 창](./media/app-insights-app-map/error-pane.png)

실패에서을 클릭 하면 해당 오류 toohello 가장 최근 인스턴스를 이동 합니다.

## <a name="resource-health"></a>리소스 상태
일부 리소스 유형에 대 한 리소스 상태 hello 위쪽 hello 오류 창에 표시 됩니다. 예를 들어 SQL 노드를 클릭 하면 표시 됩니다 hello 데이터베이스 상태 및 경고가 발생 하지 않습니다.

![리소스 상태](./media/app-insights-app-map/resource-health.png)

해당 리소스에 대 한 hello 리소스 이름 tooview 표준 개요 메트릭을 클릭 수 있습니다.

## <a name="end-to-end-system-app-maps"></a>종단 간 시스템 앱 맵

*SDK 버전 2.3 이상 필요합니다.*

응용 프로그램에 몇 가지 구성 요소로 구성 하는 경우 예를 들어 백 엔드 서비스 또한 toohello 웹 앱-합니다 표시 지도 하나의 통합 된 앱에서 모두 합니다.

![필터 설정](./media/app-insights-app-map/multi-component-app-map.png)

hello 응용 프로그램 맵 Application Insights SDK를 설치 하는 hello와 서버 간의 모든 HTTP 종속성 호출에 따라 서버 노드를 찾습니다. 각 Application Insights 리소스 toocontain 하나의 서버를 가정 합니다.

### <a name="multi-role-app-map-preview"></a>다중 역할 앱 맵(미리 보기)

hello 미리 보기 다중 역할 응용 프로그램 맵 기능은 toouse hello 앱 지도 데이터 toohello 보내는 여러 서버와 같은 Application Insights 리소스 / 계측 키입니다. 서버 hello 지도에 원격 분석 항목 hello cloud_RoleName 속성으로 분할 됩니다. 설정 *다중 역할 응용 프로그램 맵* 너무*에* 에서 hello 미리 보기 블레이드에서 tooenable이이 구성 합니다.

이 방법은 마이크로 서비스 응용 프로그램 또는 단일 Application Insights 리소스 내의 여러 서버 toocorrelate 이벤트를 원하는 다른 시나리오에서 권장 될 수도 있습니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>사용자 의견
Hello 포털 사용자 의견 옵션을 통해 피드백을 제공 하십시오.

![MapLink-1 이미지](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>다음 단계

* [Azure Portal](https://portal.azure.com)
