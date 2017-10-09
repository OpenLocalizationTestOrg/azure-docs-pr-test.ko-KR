---
title: "aaaCollect OMS 로그 분석에서 Windows 이벤트 로그 및 분석 | Microsoft Docs"
description: "Windows 이벤트 로그는 로그 분석에서 사용 하는 hello 가장 일반적인 데이터 원본 중 하나입니다.  이 문서에서는 Windows 이벤트 로그의 tooconfigure 컬렉션 및 hello 레코드의 세부 정보 작성 방법과 hello OMS 리포지토리에 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Log Analytics의 Windows 이벤트 로그 데이터 원본
Windows 이벤트 로그는 가장 일반적인 hello 중 [데이터 원본](log-analytics-data-sources.md) toohello Windows 이벤트 로그를 작성 하는 많은 응용 프로그램이 이후 Windows 에이전트를 사용 하 여 데이터를 수집 하기 위한 합니다.  만든 모든 사용자 지정 로그에서 추가 toospecifying 시스템 및 응용 프로그램 등 표준 로그에서 이벤트를 수집할 수 있습니다 toomonitor 응용 프로그램에서 필요 합니다.

![Windows 이벤트](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Windows 이벤트 로그 수집
Windows 이벤트 로그에서 hello 구성 [로그 분석 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)합니다.

로그 분석만 hello 설정에 지정 된 hello Windows 이벤트 로그에서 이벤트를 수집 합니다.  Hello 로그의 hello 이름에 입력 하 고 클릭 하 여 이벤트 로그를 추가할 수 있습니다  **+** 합니다.  각 로그에 대해 선택한 hello 심각도 인 경우 hello 이벤트만 수집 됩니다.  원하는 toocollect hello 특정 로그에 대 한 hello 심각도 확인 합니다.  추가 조건을 toofilter 이벤트를 제공할 수 없습니다.

Hello 이벤트 로그 이름을 입력할 때 로그 분석의 일반적인 이벤트 로그 이름 제안을 제공 합니다. Tooadd hello 로그 hello 목록에 나타나지 않으면 hello hello 로그의 전체 이름을 입력 하 여 추가할 수 있습니다. 이벤트 뷰어를 사용 하 여 hello hello 로그의 전체 이름을 찾을 수 있습니다. 이벤트 뷰어를 열고 hello *속성* hello에서 hello 로그 및 복사 hello 문자열에 대 한 페이지 *전체 이름을* 필드입니다.

![Windows 이벤트 구성](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>데이터 수집
로그 분석 hello 이벤트를 만들 때 모니터링 되는 이벤트 로그에서 선택한 심각도 일치 하는 각 이벤트를 수집 합니다.  hello 에이전트를 수집 하는 각 이벤트 로그에 해당 위치를 기록 합니다.  Hello 에이전트 일정 시간 동안 오프 라인이 되 면 다음 로그 분석에서 이벤트를 수집 마지막 중단, 이러한 이벤트는 hello 에이전트 오프 라인 상태인 동안 생성 된 경우에 합니다.  이러한 이벤트 toonot 이면 hello 에이전트 오프 라인 상태인 동안 덮어쓰지 수집 되지 않은 이벤트와 함께 배치 hello 이벤트 로그 수집에 대 한 가능성이 있습니다.

>[!NOTE]
>Log Analytics는 키워드 *클래식* 또는 *감사 성공* 및 키워드 *0xa0000000000000*을 포함하는 이벤트 ID 18453과 함께 원본 *MSSQLSERVER*의 SQL Server에서 생성되는 감사 이벤트를 수집하지 않습니다.
>

## <a name="windows-event-records-properties"></a>Windows 이벤트 레코드 속성
Windows 이벤트 레코드에는 형식이 **이벤트** 한 hello 속성의 다음 표에 hello:

| 속성 | 설명 |
|:--- |:--- |
| 컴퓨터 |이벤트 hello hello 컴퓨터의 이름에서 수집 되었습니다. |
| EventCategory |Hello 이벤트의 범주입니다. |
| EventData |원시 형식의 모든 이벤트 데이터입니다. |
| EventID |Hello 이벤트의 수입니다. |
| EventLevel |숫자 형식으로 hello 이벤트의 심각도입니다. |
| EventLevelName |텍스트 형태로 hello 이벤트의 심각도입니다. |
| EventLog |이벤트 hello hello 이벤트 로그의 이름에서 수집 되었습니다. |
| ParameterXml |XML 형식의 이벤트 매개 변수 값입니다. |
| ManagementGroupName |System Center Operations Manager 에이전트에 대 한 hello 관리 그룹의 이름입니다.  다른 에이전트의 경우 이 값은 AOI-<workspace ID>입니다. |
| RenderedDescription |매개 변수 값을 포함하는 이벤트 설명입니다. |
| 원본 |Hello 이벤트의 소스입니다. |
| SourceSystem |유형의 에이전트 hello 이벤트에서 수집 되었습니다. <br> OpsManager – Windows 에이전트, 직접 연결 또는 관리된 Operations Manager <br> Linux – 모든 Linux 에이전트  <br> AzureStorage – Azure 진단 |
| TimeGenerated |날짜 및 시간 hello 이벤트는 Windows에서 작성 되었습니다. |
| 사용자 이름 |Hello 이벤트를 기록 하는 hello 계정의 사용자 이름입니다. |

## <a name="log-searches-with-windows-events"></a>Windows 이벤트 로그로 로그 검색
hello 다음 표에서 Windows 이벤트 레코드를 검색 하는 로그 검색의 다른 예.

| 쿼리 | 설명 |
|:--- |:--- |
| Type=Event |모든 Windows 이벤트 |
| Type=Event EventLevelName=error |심각도가 오류인 모든 Windows 이벤트 |
| Type=Event &#124; Measure count() by Source |원본별 Windows 이벤트 수 |
| Type=Event EventLevelName=error &#124; Measure count() by Source |원본별 Windows 오류 이벤트 수 |


>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.
>
>| 쿼리 | 설명 |
|:---|:---|
| 이벤트 |모든 Windows 이벤트 |
| Event &#124; where EventLevelName == "error" |심각도가 오류인 모든 Windows 이벤트 |
| Event &#124; summarize count() by Source |원본별 Windows 이벤트 수 |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |원본별 Windows 오류 이벤트 수 |


## <a name="next-steps"></a>다음 단계
* 로그 분석 toocollect 다른 구성 [데이터 원본](log-analytics-data-sources.md) 분석 합니다.
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.  
* 사용 하 여 [사용자 정의 필드](log-analytics-custom-fields.md) 개별 필드로 tooparse hello 이벤트 레코드입니다.
* Windows 에이전트에서 [성능 카운터 수집](log-analytics-data-sources-performance-counters.md)을 구성합니다.
