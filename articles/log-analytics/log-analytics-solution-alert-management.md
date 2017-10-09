---
title: "Operations Management Suite (OMS)에서 관리 솔루션 aaaAlert | Microsoft Docs"
description: "hello 로그 분석에서 경고 관리 솔루션을 사용 하 여 모든 사용자 환경에서 hello 경고를 분석할 수 있습니다.  또한 tooconsolidating 경고 OMS 내에서 생성, 경고에서에서 가져온 연결 된 System Center Operations Manager 관리 그룹 로그 분석에 있습니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>OMS(Operations Management Suite)의 경고 관리 솔루션

![경고 관리 아이콘](media/log-analytics-solution-alert-management/icon.png)

hello 경고 관리 솔루션을 사용 하 여 모든 로그 분석 저장소의 hello 경고를 분석할 수 있습니다.  [Log Analytics에서 만든](log-analytics-alerts.md) 또는 [Nagios 또는 Zabbix에서 가져온](log-analytics-linux-agents.md) 원본을 포함하여 다양한 원본에서 이러한 경고가 발생할 수 있습니다.  hello 솔루션도 경고를 가져오는 모든 [System Center Operations Manager 관리 그룹 연결](log-analytics-om-agents.md)합니다.

## <a name="prerequisites"></a>필수 조건
hello 솔루션이 작동 하는 형식의 hello 로그 분석 저장소의 모든 레코드와 **경고**모든 구성은 필요한 toocollect 수행 해야 하므로, 이러한 레코드입니다.

- 로그 분석 경고에 대 한 [경고 규칙을 만들려면](log-analytics-alerts.md) hello 저장소에서 직접 toocreate 경고 레코드입니다.
- Nagios 및 Zabbix 경고에 대 한 [해당 서버를 구성할](log-analytics-linux-agents.md) toosend 경고 tooLog 분석 합니다.
- System Center Operations Manager 경고에 대 한 [Operations Manager 관리 그룹 tooyour 로그 분석 작업 영역 연결](log-analytics-om-agents.md)합니다.  그러면 System Center Operations Manager에서 생성된 모든 경고를 Log Analytics로 가져옵니다.  

## <a name="configuration"></a>구성
Hello 프로세스를 사용 하 여 OMS 작업 영역에서 설명 하는 hello 경고 관리 솔루션 tooyour 추가 [솔루션 추가](log-analytics-add-solutions.md)합니다.  추가 구성은 필요 없습니다.

## <a name="management-packs"></a>관리 팩
System Center Operations Manager 관리 그룹에 연결 된 tooyour OMS 작업 영역 이면 다음 다음 관리 팩 hello에에서 설치 됩니다 System Center Operations Manager이이 솔루션을 추가 합니다.  구성 또는 필요한 hello 관리 팩의 유지 관리 없을 합니다.  

* Microsoft System Center Advisor 경고 관리(Microsoft.IntelligencePacks.AlertManagement)

솔루션 관리 팩 업데이트 되는 방식에 대 한 자세한 내용은 참조 하십시오. [Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md)합니다.

## <a name="data-collection"></a>데이터 수집
### <a name="agents"></a>에이전트
다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 원본에 설명 합니다.

| 연결된 소스 | 지원 | 설명 |
|:--- |:--- |:--- |
| [Windows 에이전트](log-analytics-windows-agents.md) | 아니요 |직접 Windows 에이전트는 경고를 생성하지 않습니다.  이벤트에서 Log Analytics 경고를 만들고 Windows 에이전트에서 성능 데이터를 수집할 수 있습니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 |직접 Linux 에이전트는 경고를 생성하지 않습니다.  이벤트에서 Log Analytics 경고를 만들고 Linux 에이전트에서 성능 데이터를 수집할 수 있습니다.  Nagios 및 Zabbix 경고 hello Linux 에이전트를 필요로 하는 해당 서버에서 수집 됩니다. |
| [System Center Operations Manager 관리 그룹](log-analytics-om-agents.md) |예 |Operations Manager 에이전트에서 생성 되는 경고 toohello 관리 그룹 전달 되며 tooLog 분석 전달 됩니다.<br><br>Operations Manager 에이전트 tooLog의 직접 연결 분석 필요 하지 않습니다. 경고 데이터는 hello 관리 그룹 toohello 로그 분석 저장소에서 전달 됩니다. |


### <a name="collection-frequency"></a>수집 빈도
- 경고 레코드는 hello 저장소에 저장 되는 즉시 사용할 수 있는 toohello 솔루션입니다.
- 경고 데이터는 3 분 마다 hello Operations Manager 관리 그룹 tooLog 분석에서에서 전송 됩니다.  

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여
Hello 경고 관리 솔루션 tooyour OMS 작업 영역에 추가 하면 hello **경고 관리** 타일 tooyour OMS 대시보드에 추가 됩니다.  이 타일에는 개수 및 그래픽으로 나타낸 hello 지난 24 시간 동안 hello 내에서 생성 된 현재 활성 경고 수가 표시 됩니다.  이 시간 범위를 변경할 수 없습니다.

![경고 관리 타일](media/log-analytics-solution-alert-management/tile.png)

Hello 클릭 **경고 관리** 타일 tooopen hello **경고 관리** 대시보드 합니다.  hello 대시보드는 다음 표에 hello에 hello 열을 포함 합니다.  각 열에는 hello 상위 10 개의 경고 개수를 비교 하 여 hello에 대 한 열의 조건을 범위 및 시간 범위를 지정 했는지 나열 됩니다.  클릭 하 여 hello 전체 목록을 제공 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 열의 또는 hello 열 머리글을 클릭 하 여 hello 맨 아래에 있습니다.

| 열 | 설명 |
|:--- |:--- |
| 중요한 알림 |경고 이름별로 그룹화된 중요 심각도를 가진 모든 경고.  경고 이름 toorun 해당 경고에 대 한 모든 레코드를 반환 하는 로그 검색을 클릭 합니다. |
| 경고 알림 |경고 이름별로 그룹화된 경고의 심각도를 가진 모든 경고입니다.  경고 이름 toorun 해당 경고에 대 한 모든 레코드를 반환 하는 로그 검색을 클릭 합니다. |
| 활성 SCOM 경고 |모든 경고에서에서 수집 된 Operations Manager 상태와 이외의 *닫힘* 해당 생성 된 hello 경고 소스 별로 그룹화 합니다. |
| 모든 활성 경고 |경고 이름별로 그룹화된 심각도를 가진 모든 경고입니다. *닫힘*이외의 상태를 가진 Operations Manager 경고만 포함합니다. |

Hello 대시보드 tooperform에서 클릭할 수 있는 몇 가지 일반적인 쿼리가 나와 toohello 오른쪽 스크롤할 경우는 [로그 검색](log-analytics-log-searches.md) 경고 데이터에 대 한 합니다.

![경고 관리 대시보드](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Log Analytics 레코드
hello 경고 관리 솔루션의 형식 포함 된 레코드를 분석 하 여 **경고**합니다.  경고 로그 분석에 의해 생성 되거나 Nagios 또는 Zabbix에서 수집 된 hello 솔루션에 의해 직접 수집 되지 않습니다.

hello System Center Operations Manager에서 경고를 가져올 경우 솔루션과 형식의 각각에 대해 해당 레코드를 만듭니다 **경고** 및의 SourceSystem **OpsManager**합니다.  이러한 레코드는 다음 표에 hello에 hello 속성을 포함 합니다.  

| 속성 | 설명 |
|:--- |:--- |
| 형식 |*경고* |
| SourceSystem |*OpsManager* |
| AlertContext |XML 형식으로 생성 된 hello 경고 toobe를 발생 시킨 hello 데이터 항목의 세부 정보입니다. |
| AlertDescription |Hello 경고의 자세한 설명입니다. |
| AlertId |Hello 경고의 GUID입니다. |
| AlertName |Hello 경고의 이름입니다. |
| AlertPriority |Hello 경고의 우선 순위 수준입니다. |
| AlertSeverity |Hello 경고의 심각도 수준입니다. |
| AlertState |최신 hello 경고의 상태를 확인 하 고 합니다. |
| LastModifiedBy |Hello 경고를 마지막으로 수정한 hello 사용자 이름입니다. |
| ManagementGroupName |Hello 경고가 생성 된 hello 관리 그룹의 이름입니다. |
| RepeatCount |횟수입니다. 동일한 경고가 생성 된 hello 같은 모니터링 대상 개체를 확인 하는 이후 hello에 대 한 합니다. |
| ResolvedBy |해결 된 hello 알림 hello 사용자의 이름입니다. Hello 경고 아직 해결 되지 않았다고 경우 비어 있습니다. |
| SourceDisplayName |Hello 모니터링 hello 경고를 생성 하는 개체의 이름을 표시 합니다. |
| SourceFullName |Hello 모니터링 hello 경고를 생성 하는 개체의 전체 이름입니다. |
| TicketId |System Center Operations Manager 환경 hello 경고에 대 한 티켓을 할당 하는 프로세스와 통합 되 면 hello 경고에 대 한 티켓 ID입니다.  비어 있으면 티켓 ID가 할당되지 않습니다. |
| TimeGenerated |날짜 및 시간 경고 hello을 만들었습니다. |
| TimeLastModified |날짜 및 시간 경고 hello을 마지막으로 변경한 합니다. |
| TimeRaised |날짜 및 시간을 hello 경고가 생성 되었습니다. |
| TimeResolved |날짜 및 시간을 hello 경고 해결 되었습니다. Hello 경고 아직 해결 되지 않았다고 경우 비어 있습니다. |

## <a name="sample-log-searches"></a>샘플 로그 검색
hello 다음 표에서이 솔루션에 의해 수집 된 경고 레코드에 대 한 예제 로그 검색 합니다. 

| 쿼리 | 설명 |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |지난 24 시간 hello 동안 발생 한 중요 한 알림 |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |지난 24 시간 hello 하는 동안 발생 한 경고 알림 |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |지난 24 시간 hello 하는 동안 발생 하는 활성 경고 소스 |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |지난 24 시간 동안 계속 활성화 된 hello 동안 발생 한 중요 한 알림 |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |지난 24 시간 이제 닫혀 있는 hello 동안 발생 한 알림 |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Hello 심각도 별로 그룹화 된 지난 1 일 동안 발생 한 알림 |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Hello 반복 횟수 값을 기준으로 정렬 지난 1 일 동안 발생 한 알림 |


>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 앞에 오는 hello toohello 다음 변경 합니다.
>
>| 쿼리 | 설명 |
|:---|:---|
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) |지난 24 시간 hello 동안 발생 한 중요 한 알림 |
| Alert &#124; where AlertSeverity == "warning" and TimeRaised > ago(24h) |지난 24 시간 hello 하는 동안 발생 한 경고 알림 |
| Alert &#124; where SourceSystem == "OpsManager" and AlertState != "Closed" and TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |지난 24 시간 hello 하는 동안 발생 하는 활성 경고 소스 |
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) and AlertState != "Closed" |지난 24 시간 동안 계속 활성화 된 hello 동안 발생 한 중요 한 알림 |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(24h) and AlertState == "Closed" |지난 24 시간 이제 닫혀 있는 hello 동안 발생 한 알림 |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Hello 심각도 별로 그룹화 된 지난 1 일 동안 발생 한 알림 |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; sort by RepeatCount desc |Hello 반복 횟수 값을 기준으로 정렬 지난 1 일 동안 발생 한 알림 |


## <a name="next-steps"></a>다음 단계
* Log Analytics에서 경고 생성에 대한 자세한 내용은 [Log Analytics의 경고](log-analytics-alerts.md) 에 관하여 알아보세요.
