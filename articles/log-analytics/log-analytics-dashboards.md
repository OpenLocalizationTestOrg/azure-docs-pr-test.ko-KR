---
title: "Azure 로그 분석에서 사용자 지정 대시보드 aaaCreate | Microsoft Docs"
description: "이 가이드를 사용 하면 로그 분석 대시보드 시각화 방법을 저장 된 로그 검색이 모두 이해, 제공 단일 렌즈 tooview 환경입니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Log Analytics에서 사용할 사용자 지정 대시보드 만들기

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 다음 기존 대시보드를 편집 하거나 새 대시보드를 만들 수 없습니다. 

이 가이드를 사용 하면 로그 분석 대시보드 시각화 방법을 저장 된 로그 검색이 모두 이해, 제공 단일 렌즈 tooview 환경입니다.

![예제 대시보드](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Hello OMS 포털에서 만드는 모든 hello 사용자 지정 대시보드 hello OMS 모바일 앱에서에서 사용할 수 있습니다. Hello hello 앱에 대 한 자세한 내용은 다음을 참조 하십시오.

* [Microsoft 스토어 hello에서 OMS 모바일 앱](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Apple iTunes의 OMS 모바일 앱](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![모바일 대시보드](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>내 대시보드를 만드는 방법
toobegin, 이동 toohello OMS 개요 페이지 Hello 표시 **내 대시보드** 타일 hello 왼쪽에 있습니다. 클릭 toodrill 아래로 대시보드에.

![개요](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>타일 추가
대시보드에서 타일은 저장된 로그 검색을 기반으로 합니다. OMS에는 여러 저장된 로그 검색이 미리 만들어져 있으므로 바로 시작할 수 있습니다. 사용 하 여 hello 다음 해당 개요를 어떻게 단계 toobegin 합니다.

Hello 내 대시보드 보기를 클릭 하기만 하면 **사용자 지정** tooenter 사용자 모드를 지정 합니다.

![그림](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 hello 열리는 패널에는 hello hello 페이지의 오른쪽에 작업 영역의 저장 된 로그 검색이 모두 표시 합니다. 저장 된 로그 검색을 타일로 toovisualize 저장된 된 검색 위에 놓고 클릭 hello **플러스** 기호입니다.

![타일 추가 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Hello를 클릭할 때 **플러스** 기호, 새 타일 hello 내 대시보드 보기에에서 나타납니다.

![타일 추가 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>타일 편집
Hello 내 대시보드 보기를 클릭 하기만 하면 **사용자 지정** tooenter 사용자 모드를 지정 합니다. Tooedit hello 타일을 클릭 합니다. 오른쪽 패널 hello tooedit를 변경 하 고 바뀌고 다양 한 옵션을 제공 합니다.

![타일 편집](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![타일 편집](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>타일 시각화
타일 시각화 toochoose의 세 가지 종류가 있습니다.

| 차트 종류 | 수행하는 작업 |
| --- | --- |
| ![가로 막대형 차트](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |로그 검색 결과가 필드에 따라 집계되는지 여부에 따라 저장된 로그 검색 결과의 타임라인이 막대형 그래프 또는 필드별 결과 목록 형태로 표시됩니다. |
| ![메트릭](./media/log-analytics-dashboards/oms-dashboards-metric.png) |총 로그 검색 결과 적중 횟수를 타일에 숫자로 표시합니다. 메트릭 타일 tooset hello 임계값에 도달할 때 hello 타일 강조 표시 하는 임계값을 사용 합니다. |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |저장된 로그 검색 결과 적중의 타임라인이 값과 함께 꺾은선 그래프로 표시됩니다. |

### <a name="threshold"></a>임계값
Hello 메트릭 시각화를 사용 하 여 타일에 임계값을 만들 수 있습니다. Hello 타일에 임계값 toocreate에서 선택 합니다. Hello 값이 초과 하거나 선택한 hello 임계값 미만일 경우 toohighlight hello 타일 hello 임계값 아래에 다음 설정 여부를 선택 합니다.

## <a name="organizing-hello-dashboard"></a>Hello 대시보드 구성
tooorganize 대시보드에 toohello 내 대시보드 보기를 탐색 하 고 클릭 **사용자 지정** tooenter 사용자 모드를 지정 합니다. 클릭 끌어서 hello 타일 toomove을 원하는 타일 toobe toowhere 이동 합니다.

![대시보드 구성](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>타일 제거
바둑판식 배열 tooremove toohello 내 대시보드 보기를 탐색 하 고 클릭 **사용자 지정** tooenter 사용자 모드를 지정 합니다. 선택 hello 타일 tooremove, 원하는 다음 hello 오른쪽 패널에서 선택 **타일 제거**합니다.

![타일 제거](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>다음 단계
* 만들 [경고](log-analytics-alerts.md) 로그 분석 toogenerate 알림과 tooremediate 문제입니다.
