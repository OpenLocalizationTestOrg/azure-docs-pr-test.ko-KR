---
title: "OMS 로그 분석에서 aaaLog 검색 | Microsoft Docs"
description: "로그 검색 tooretrieve 로그 분석에서 모든 데이터가 필요합니다.  이 문서는 검색 로그 분석에 사용 되는 새로운 로그에 설명 하 고 하나를 만들기 전에 toounderstand 해야 하는 개념을 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Log Analytics의 로그 검색 이해

> [!NOTE]
> 이 문서에서는 hello 새로운 쿼리 언어를 사용 하 여 Azure 로그 분석에서 로그 검색을 설명 합니다.  Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.  
>
> 작업 영역에는 업그레이드 된 toohello 새로운 쿼리 언어 되지 않았는지를 하는 경우를 참조 해야 너무[로그 분석 로그 검색을 사용 하 여 데이터를 찾을](log-analytics-log-searches.md)합니다.

로그 검색 tooretrieve 로그 분석에서 모든 데이터가 필요합니다.  Hello 포털에서 데이터를 분석 하 고 있는지 여부를 경고 규칙 toobe 구성에 대 한 알림을 특정 조건 또는 hello 로그 분석 API를 사용 하 여 데이터를 검색할 원하는 로그 검색 toospecify hello 데이터를 사용 합니다.  이 문서는 Log Analytics에서 로그 검색이 어떻게 사용되는지를 설명하고 새로 만들기 전에 이해해야 하는 개념을 제공합니다. Hello 참조 [다음 단계](#next-steps) hello 쿼리 언어에 대 한 자료 및 만들기 및 편집 로그 검색에 대 한 자세한 내용은 섹션.

## <a name="where-log-searches-are-used"></a>로그 검색이 사용되는 위치

로그 검색을 사용 하는 로그 분석에는 hello 다양 한 방법 hello 다음 포함:

- **포털.** Hello로 hello 리포지토리에 데이터를 대화형으로 분석을 수행할 수 있습니다 [로그 검색 포털](log-analytics-log-search-log-search-portal.md) 또는 hello [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587)합니다.  이렇게 하면 tooedit 프로그램 쿼리 및 다양 한 형식 및 시각화에에서 hello 결과 분석 합니다.  대부분의 쿼리를 만들면가 hello 포털 중 하나에서 시작 되 고 예상 대로 작동 하는지 확인 한 후 복사 합니다.
- **경고 규칙.** [경고 규칙](log-analytics-alerts.md)은 작업 영역에서 데이터의 문제를 사전에 식별합니다.  각 경고 규칙은 일정한 간격으로 자동으로 실행되는 로그 검색을 기반으로 합니다.  hello 결과가 경고를 생성 하면 검사 toodetermine 됩니다.
- **뷰.**  사용자 대시보드 (포함)에 포함 된 데이터 toobe의 시각화를 만들 수 있습니다 [뷰 디자이너](log-analytics-view-designer.md)합니다.  로그 검색에서 사용 하는 hello 데이터를 제공 [타일](log-analytics-view-designer-tiles.md) 및 [시각화 부분](log-analytics-view-designer-parts.md) 각 보기에서.  Hello hello 데이터에 포털 tooperform 추가 분석 로그 검색으로 시각화 부분에서 다운 드릴 수 있습니다.
- **내보내기.**  로그 분석 작업 영역 tooExcel hello에서에서 데이터를 내보낼 때 또는 [Power BI](log-analytics-powerbi.md), 로그 검색 toodefine hello 데이터 tooexport를 만듭니다.
- **PowerShell.** 명령줄 또는 사용 하는 Azure 자동화 runbook에서 PowerShell 스크립트를 실행할 수 있습니다 [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) 로그 분석에서 tooretrieve 데이터입니다.  이 cmdlet에는 쿼리 toodetermine hello 데이터 tooretrieve가 필요합니다.
- **Log Analytics API.**  hello [로그 분석 로그 검색 API](log-analytics-log-search-api.md) 모든 REST API 클라이언트 hello 작업 영역에서 tooretrieve 데이터를 허용 합니다.  로그 분석 toodetermine hello 데이터 tooretrieve에 대해 실행 되는 쿼리를 포함 하는 hello API 요청 합니다.

![로그 검색](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Log Analytics 데이터 구성 방법
쿼리를 작성할 때 테이블 hello 하는 데이터를 찾고 확인 하 여 시작 합니다. 각 [데이터 소스](log-analytics-data-sources.md) 및 [솔루션](../operations-management-suite/operations-management-suite-solutions.md) hello 로그 분석 작업 영역에서 전용된 테이블에 데이터를 저장 합니다.  각 데이터 원본 및 솔루션에 대 한 설명서는 생성 된 hello 데이터 형식의 hello 이름 및 각 속성에 대 한 설명을 포함 합니다.     많은 쿼리 되 면 필요 단일 테이블의 데이터를에서 하지만 다른 사용자 다양 한 옵션 tooinclude 여러 테이블의에서 데이터를 사용할 수 있습니다.

![테이블](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>쿼리 작성
로그의 hello 핵심 로그 분석에서 검색은 [광범위 한 쿼리 언어](https://docs.loganalytics.io/) 수 있게 해 주는 여러 가지 방법으로 hello 저장소에서 데이터를 분석 하 고 검색 합니다.  이 동일한 쿼리 언어는 [Application Insights](../application-insights/app-insights-analytics.md)에 사용됩니다.  Toowrite 쿼리 로그 분석에서 중요 한 toocreating 로그 검색은 어떻게 알 수 있습니다.  일반적으로 처음부터 기본 쿼리 및 다음 진행 toouse 더 높은 수준의 함수 요구 사항 복잡 해지면 합니다.

쿼리의 hello 기본 구조는 일련의 연산자 파이프 문자 뒤의 원본 테이블 `|`합니다.  여러 연산자 toorefine hello 데이터를 함께 연결할 수 있으며 고급 기능을 수행할 수 있습니다.

예를 들어 한다고 가정 toofind hello 상위 10 개 컴퓨터가 hello로 대부분의 오류 이벤트 hello를 통해 어제 합니다.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

또는 hello 마지막 날에에서 하트 비트를 보유 한 하지 않은 toofind 컴퓨터 할 수도 있습니다.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

어떻습니까와 꺾은선형 차트는 각 컴퓨터에서 지난 주에 대 한 hello 프로세서 사용률?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Hello 쿼리의 구조는와 작업 하는 데이터의 hello 종류에 관계 없이 hello는 이러한 빠른 예제에서 볼 수 있습니다.  Hello 파이프라인 toohello 다음 명령을 통해 hello 명령 하나에서 결과 데이터를 보내는 위치 고유 단계로 분석할 수 있습니다.

자습서 및 언어 참조를 포함 하 여 hello Azure 로그 분석 쿼리 언어에 대 한 전체 설명서를 참조 hello [Azure 로그 분석 쿼리 언어 설명서](https://docs.loganalytics.io/)합니다.

## <a name="next-steps"></a>다음 단계

- Hello에 대 한 자세한 내용은 [toocreate를 사용 하 고 로그 검색을 편집 하는 포털](log-analytics-log-search-portals.md)합니다.
- 체크 아웃 한 [쿼리 작성의 자습서](https://go.microsoft.com/fwlink/?linkid=856078) hello 새로운 쿼리 언어를 사용 하 여 합니다.
