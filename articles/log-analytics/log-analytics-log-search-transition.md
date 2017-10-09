---
title: "로그 분석 쿼리 언어 치트 시트를 aaaAzure | Microsoft Docs"
description: "이 문서는 이미 hello 레거시 언어에 잘 알고 있다면 toohello 새로운 쿼리 언어 로그 분석에 대 한 전환에 지원을 제공 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>TooAzure 로그 분석 새로운 쿼리 언어를 전환합니다.

> [!NOTE]
> 새 로그 분석 쿼리 언어 및 get hello에 대 한 자세한 hello 프로시저 tooupgrade 업그레이드 작업 영역을 읽을 수 있습니다 프로그램 [Azure 로그 분석 작업 영역 toonew 로그 검색](log-analytics-log-search-upgrade.md)합니다.

이 문서는 이미 hello 레거시 언어에 잘 알고 있다면 toohello 새로운 쿼리 언어 로그 분석에 대 한 전환에 지원을 제공 합니다.

## <a name="language-converter"></a>언어 변환기

Hello 레거시 로그 분석 쿼리 언어에 익숙한 경우 hello toocreate hello hello 새로운 언어에서 동일한 쿼리는 가장 쉬운 방법은 toouse hello 작업 영역을 변환할 때 hello 로그 검색 포털에 설치 된 언어 변환기입니다.  Hello 변환기를 사용 하는 작업은 레거시 쿼리에 hello 상위 텍스트 상자에 입력 한 다음 클릭으로 **변환**합니다.  Hello 검색 단추 toorun hello 쿼리 또는 복사를 클릭 하 고 toouse 붙여 다른 곳입니다.

![언어 변환기](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>참고 자료

hello 다음 표에서 다양 한 일반적인 쿼리 비교 하 여 Azure 로그 분석에서 hello 새롭고 레거시 쿼리 언어 간의 tooequivalent 명령.

| 설명 | 레거시 | 신규 |
|:--|:--|:--|
| 모든 테이블 검색      | error | “오류” 검색(대소문자 구분 안 함) |
| 테이블에서 데이터 선택 | Type=Event |  이벤트 |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| 문자열 비교      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Event &#124; where Computer contains "contoso" (not case sensitive)<br>Event &#124; where Computer contains_cs "Contoso" (case sensitive) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| 날짜 비교        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| 부울 비교     | Type=Heartbeat IsGatewayInstalled=false  | Heartbeat | where IsGatewayInstalled == false |
| 정렬                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event \| sort by Computer asc, EventLog desc, EventLevelName asc |
| Distinct               | Type=Event &#124; dedup Computer \| select Computer | Event &#124; summarize by Computer, EventLog |
| 열 확장         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" \| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| 집계            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| 제한있는 집계 | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| 통합                  | Type=Event or Type=Syslog | union Event, Syslog |
| Join                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>다음 단계
- 체크 아웃 한 [쿼리 작성의 자습서](https://go.microsoft.com/fwlink/?linkid=856078) hello 새로운 쿼리 언어를 사용 하 여 합니다.
- Toohello 참조 [쿼리 언어 참조](https://go.microsoft.com/fwlink/?linkid=856079) 모든 명령, 연산자 및 hello 새로운 쿼리 언어에 대 한 함수에 대 한 자세한 내용은 합니다.  
