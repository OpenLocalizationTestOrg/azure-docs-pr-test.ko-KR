---
title: "Azure 로그 분석에서 aaaUnderstanding 경고 | Microsoft Docs"
description: "로그 분석에 OMS 리포지토리에 중요 한 정보를 식별 및 수 사전 문제점을 알려 경고나 작업 tooattempt toocorrect 호출을 합니다.  이 문서에서는 hello 다양 한 경고 규칙 및 정의 하는 방법을 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Log Analytics의 경고 이해

Log Analytics의 경고는 Log Analytics 리포지토리에서 중요한 정보를 식별합니다.  이 문서는 어떻게 경고 규칙 로그 분석 작업에 대 한 세부 정보를 제공 하 고 여러 유형의 경고 규칙의 hello 차이점을 설명 합니다.

Hello 경고 규칙을 만드는 과정을 hello 다음 문서를 참조 하세요.

- [Azure Portal](log-analytics-alerts-creating.md)을 사용하여 경고 규칙 만들기
- [Resource Manager 템플릿](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)을 사용하여 경고 규칙 만들기
- [REST API](log-analytics-api-alerts.md)를 사용하여 경고 규칙 만들기


## <a name="alert-rules"></a>경고 규칙

경고는 일정한 간격으로 로그 검색을 자동으로 실행하는 경고 규칙에 의해 만들어집니다.  Hello hello 로그 검색 결과는 특정 조건과 일치 하는 경우 경고 레코드가 만들어집니다.  hello 규칙 수 후 자동으로 하나를 실행 하거나 더 많은 작업 tooproactively hello 경고의 알림을 또는 다른 프로세스를 호출 합니다.  여러 유형의 경고 규칙 다른 논리 tooperform이이 분석을 사용합니다.

![Log Analytics 경고](media/log-analytics-alerts/overview.png)

경고 규칙 hello 다음 세부 정보에 의해 정의 됩니다.

- **로그 검색**.  hello 경고 규칙이 실행 될 때마다 실행 하는 hello 쿼리.  이 쿼리에서 반환 된 hello 레코드는 사용 되는 toodetermine 경고가 만들어지고 합니다.
- **기간**.  Hello 쿼리에 대 한 hello 시간 범위를 지정합니다.  hello 쿼리는 현재 시간 hello이이 범위 내에서 생성 된 레코드만 반환 합니다.  이는 5 분에서 24 시간 사이의 임의 값일 수 있습니다. 예를 들어 hello too60 분과 hello 쿼리 창을 설정 된 시간에 실행 된 경우 오후 1 시 15 분 오후 12시 15분와 오후 1시 15분 사이 레코드만 반환 됩니다.
- **빈도**.  얼마나 자주 hello 쿼리 실행 되도록 지정 합니다. 5 분에서 24 시간 사이의 임의 값일 수 있습니다. Hello 기간 보다 작은 tooor 동일 해야 합니다.  Hello 값 hello 기간 보다 큰 경우 레코드가 누락 될 위험이 있습니다.<br>예를 들어 30분의 기간과 60분의 빈도를 사용하는 것이 좋습니다.  Hello 쿼리 1:00에 실행 된 경우 오후 12시 30분 1시 사이 레코드를 반환 합니다.  hello는 hello 쿼리는 실행 하는 다음에 2:00 때 1시 30분 2시 사이 레코드를 반환 합니다.  1:00 및 1:30 사이에 생성된 레코드는 평가되지 않습니다.
- **임계값**.  hello hello 로그 검색 결과 경고를 만들 수 있는지 여부를 평가 toodetermine를 됩니다.  hello 임계값 hello 여러 유형의 경고 규칙에 대 한 차이가 있습니다.

Log Analytics의 각 경고 규칙은 두 가지 형식 중 하나입니다.  이러한 각 유형의 hello 섹션에서 자세히 설명 되어 있습니다.

- **[결과 수](#number-of-results-alert-rules)** - Hello 숫자 레코드 hello 로그 검색에서 반환할 때 생성 되는 단일 경고는 지정된 된 수를 초과 합니다.
- **[미터법](#metric-measurement-alert-rules)** -  경고를 지정 된 임계값을 초과 하는 값을 사용 하 여 hello 로그 검색의 hello 결과에서 각 개체에 대해 만들었습니다.

경고 규칙 유형 간의 hello 차이점은 다음과 같습니다.

- **결과 수가** 경고 규칙 단일 경고 잠시 만들어집니다 **메트릭 측정** 경고 규칙은 hello 임계값을 초과 하는 각 개체에 대 한 경고를 생성 합니다.
- **결과 수가** hello 임계값을 한 번을 초과 하면 경고 규칙에서 경고를 생성 합니다. **메트릭 측정** hello 임계값을 초과 하면 경고 규칙에서 경고를 만들 수는 특정 횟수의 특정 시간 간격을 두고 있습니다.

## <a name="number-of-results-alert-rules"></a>결과 수 경고 규칙
**결과 수가** 경고 규칙 hello hello 검색 쿼리에서 반환 된 레코드 수가 hello 지정된 임계값을 초과 될 때 단일 경고를 생성 합니다.

### <a name="threshold"></a>임계값
에 대 한 hello 임계값은 **결과 수가** 경고 규칙은 단순히 보다 큰 또는 특정 값 보다 작지 합니다.  이 조건과 일치 하는 hello hello 로그 검색에서 반환 된 레코드 수, 경고가 생성 됩니다.

### <a name="scenarios"></a>시나리오

#### <a name="events"></a>이벤트
이 형식의 경고 규칙은 Windows 이벤트 로그, Syslog 및 사용자 지정 로그와 같은 이벤트 작업에 적합합니다.  특정 오류 이벤트를 생성 하거나 특정 시간 창 내에서 여러 오류 이벤트를 만들면 경고 toocreate를 할 수 있습니다.

단일 이벤트에 tooalert hello 수가 0이 고 두 hello 빈도 보다 결과 toogreater 설정 하 고 창 too5 분 시간.  5 분 마다이 고 hello 마지막 시간 hello 쿼리가 실행 된 이후 생성 된 단일 이벤트의 발생 hello에 대 한 확인 hello 쿼리를 실행 하는 합니다.  더 긴 빈도 hello 이벤트 되 고 수집 된 hello 경고를 만들려는 사이의 hello 시간을 지연 될 수 있습니다.

일부 응용 프로그램은 경고를 발생시키지 않아야 할 가끔씩 발생하는 오류를 기록할 수 있습니다.  예를 들어 hello 응용 프로그램 hello 오류 이벤트를 생성 하는 hello 프로세스를 다시 시도 하 고 hello을 다음 시간 성공 합니다.  이 경우 수도 있습니다 toocreate hello 경고 않으면 여러 이벤트가 특정 시간 창 내에서 만들어집니다.  

일부 경우에는 이벤트의 hello 없는 경우에서 경고 toocreate를 수도 있습니다.  예를 들어 프로세스는 제대로 작동 하는 일반 이벤트 tooindicate를 기록할 수 있습니다.  특정 기간 내에 이러한 이벤트 중 하나가 기록되지 않으면 경고를 만들어야 합니다.  이 경우 설정한 hello 임계값 너무**1 미만이**합니다.

#### <a name="performance-alerts"></a>성능 경고
[성능 데이터](log-analytics-data-sources-performance-counters.md) hello OMS 리포지토리에 비슷한 tooevents에서에서 레코드로 저장 됩니다.  성능 카운터는 특정 임계값을 초과할 때 tooalert를 원하는 임계값을 hello 쿼리에 포함 되어야 합니다.

통해 프로세서 실행 되 면 hello tooalert 하려는 경우 예를 들어 90% hello hello 경고 규칙에 대 한 hello 임계값 아래와 같은 쿼리를 사용 하는 **0 보다 큰**합니다.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Hello를 사용 하는 쿼리를 사용 하면 hello 프로세서 평균 특정 시간 창에 대 한 90% 이상를 tooalert를 려 [명령 측정](log-analytics-search-reference.md#commands) hello 경고 규칙에 대 한 hello 임계값을 사용 하 여 hello 다음 같은 **0 보다 큰** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>미터법 경고 규칙

>[!NOTE]
> 미터법 경고 규칙은 현재 공개 미리 보기 상태입니다.

**미터법** 경고 규칙은 쿼리에서 지정된 임계값을 초과하는 값을 포함한 각 개체에 대해 경고를 만듭니다.  Hello 뒤에서 명확한 차이점이 있는 **결과 수가** 규칙 경고 합니다.

#### <a name="log-search"></a>로그 검색
에 대 한 모든 쿼리를 사용할 수 있지만 한 **결과 수가** 메트릭 측정 경고 규칙에 대 한 특정 요구 사항 hello 쿼리는 경고 규칙을 합니다.  포함 해야 합니다는 [명령 측정](log-analytics-search-reference.md#commands) 특정 필드에 대 한 toogroup hello 결과입니다. 이 명령은 hello 요소 다음에 포함 되어야 합니다.

- **집계 함수** -  수행 하는 hello 계산 및 숫자 필드 tooaggregate 결정 합니다.  예를 들어 **count ()** hello 쿼리에서 hello 레코드 수를 반환 합니다 **avg(CounterValue)** hello 일정 간격에 걸쳐 hello CounterValue 필드의 hello 평균을 반환 합니다.
- **그룹 필드** -  이 필드의 각 인스턴스에 대해 집계된 값이 있는 레코드가 만들어지며 각각에 대해 경고가 생성될 수 있습니다.  예를 들어 각 컴퓨터에 대 한 경고 toogenerate 하려는 경우 사용 **컴퓨터별**합니다.   
- **간격**.  Hello 데이터를 집계 하는 hello 시간 간격을 정의 합니다.  예를 들어 지정한 **5minutes**, 레코드 hello 경고에 대 한 지정 된 hello 기간 동안 5 분 간격으로 집계 하는 hello 그룹 필드의 각 인스턴스에 대해 만들어집니다.

#### <a name="threshold"></a>임계값
hello 임계값 메트릭 측정 규칙에서는 경고에 대 한 집계 값와 위반 수가 정의 됩니다.  데이터 요소 hello 로그 검색에이 값을 초과 하는 경우 것으로 간주 보안 위반이 발생 합니다.  Hello hello 결과의 모든 개체에 대 한에 위반 수가 초과 하는 경우 hello 지정 된 값을 다음 해당 개체에 대해 경고가 생성 됩니다.

#### <a name="example"></a>예제
컴퓨터에서 30분 동안 90% 프로세서 사용률을 3회 초과하는 경우 경고가 필요한 시나리오를 고려해 보세요.  다음 세부 정보는 hello로 경고 규칙을 만듭니다.  

**쿼리:** Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer Interval 5minute<br>
**기간:** 30분<br>
**경고 빈도:** 5분<br>
**집계 값:** 90 초과<br>
**경고 트리거 조건:** 총 위반 5 초과<br>

hello 쿼리는 각 컴퓨터에 대 한 평균 값 5 분 간격으로 만듭니다.  이 쿼리 실행 수집 된 데이터에 대 일 분 마다 hello를 통해 이전 30 분입니다.  세 개의 컴퓨터에 대한 샘플 데이터는 다음과 같습니다.

![샘플 쿼리 결과](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

이 예제에서는 별도 경고는 만들 수 srv02 및 srv03은 위반 hello 90% 임계값 3 회 hello 기간 동안.  경우 hello **트리거 경고에 따라:** 너무 변경 된**연속** 3 연속 샘플에 대 한 hello 임계값을 위반 하므로 srv03에 대해서만 경고를 생성 합니다.

## <a name="alert-records"></a>경고 레코드
Log Analytics의 규칙에 의해 만든 경고 레코드에는 **경고**의 **유형** 및 **OMS**의 **SourceSystem**이 있습니다.  다음 표에 hello에 hello 속성을 갖게 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| 형식 |*경고* |
| SourceSystem |*OMS* |
| *Object*  | [메트릭 측정 경고](#metric-measurement-alert-rules) hello 그룹 필드에 대 한 속성을 갖습니다.  예를 들어 hello 로그 검색에 컴퓨터 그룹, hello 값으로 hello 컴퓨터의 hello 이름으로 컴퓨터 분야 hello 경고 레코드에 있어야 합니다.
| AlertName |Hello 경고의 이름입니다. |
| AlertSeverity |Hello 경고의 심각도 수준입니다. |
| LinkToSearchResults |Hello 경고를 생성 하는 hello 쿼리에서 hello 레코드를 반환 하는 tooLog 분석 로그 검색에 연결 합니다. |
| 쿼리 |실행 된 hello 쿼리의 텍스트입니다. |
| QueryExecutionEndTime |끝 hello 쿼리에 대 한 hello 시간 범위입니다. |
| QueryExecutionStartTime |시작 hello 쿼리에 대 한 hello 시간 범위입니다. |
| ThresholdOperator | Hello 경고 규칙에서 사용 하는 연산자입니다. |
| ThresholdValue | Hello 경고 규칙에서 사용 하는 값입니다. |
| TimeGenerated |날짜 및 시간 hello 경고가 생성 되었습니다. |

다른 종류의 hello 만든 경고 레코드 [경고 관리 솔루션](log-analytics-solution-alert-management.md) 및 [Power BI 내보냅니다](log-analytics-powerbi.md)합니다.  이들은 모두 **경고**의 **유형**을 갖지만 해당 **SourceSystem**에 의해 구별됩니다.


## <a name="next-steps"></a>다음 단계
* Hello 설치 [경고 관리 솔루션](log-analytics-solution-alert-management.md) System Center Operations Manager에서 경고와 함께 로그 분석에서 만든 tooanalyze 경고 수집 합니다.
* 경고를 생성할 수 있는 [로그 검색](log-analytics-log-searches.md) 에 대해 자세한 내용을 읽습니다.
* 경고 규칙을 사용하여 [웹후크를 구성](log-analytics-alerts-webhooks.md) 하는 연습을 완료합니다.  
* 자세한 내용은 어떻게 toowrite [Azure 자동화의 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 문제를 경고로 식별 합니다.
