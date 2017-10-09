---
title: "aaaCollect Azure 로그 분석에서 성능 카운터를 분석 하 고 | Microsoft Docs"
description: "성능 카운터는 Windows 및 Linux 에이전트에서 로그 분석 tooanalyze 성능으로 수집 됩니다.  이 문서에서는 성능 tooconfigure 컬렉션이 카운터 하는 방법 및 hello OMS 리포지토리에 저장 된 것의 세부 정보는 Windows 및 Linux 에이전트에 대 한 설명 tooanalyze hello OMS 포털에서 해당 합니다."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Log Analytics의 Windows 및 Linux 성능 데이터 원본
Windows 및 Linux에서 성능 카운터는 하드웨어 구성 요소, 운영 체제 및 응용 프로그램 성능 hello에 대 한 정보를 제공합니다.  로그 분석 긴 용어 분석 및 보고에 대 한 추가 tooaggregating 성능 데이터에 실시간으로 (NRT) 근처 분석을 위한 잦은 간격 성능 카운터를 수집할 수 있습니다.

![성능 카운터](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>성능 카운터 구성
Hello에서 hello OMS 포털의 성능 카운터 구성 [로그 분석 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)합니다.

먼저 Windows를 구성 하거나 제공 되는 새로운 OMS 작업 영역에 대 한 Linux 성능 카운터 hello 옵션 tooquickly 몇 가지 일반적인 카운터를 만듭니다.  Checkbox 다음 tooeach로 나열 됩니다.  모든 카운터를 tooinitially 만들지 확인 되 고 클릭 **추가 hello 선택한 성능 카운터**합니다.

Windows 성능 카운터의 경우, 각 성능 카운터에 대해 특정 인스턴스를 선택할 수 있습니다. Linux 성능 카운터에 대 한 사용자가 선택한 각 카운터의 hello 인스턴스 hello 부모 카운터의 tooall 자식 카운터를 적용 합니다. hello 다음 표에서 hello 공용 인스턴스 사용 가능한 tooboth Linux 맟 Windows 성능 카운터입니다.

| 인스턴스 이름 | 설명 |
| --- | --- |
| \_합계 |모든 hello 인스턴스 |
| \* |모든 인스턴스 |
| (/&#124;/var) |/ 또는 /var로 명명된 인스턴트와 일치 |

### <a name="windows-performance-counters"></a>Windows 성능 카운터

![Windows 성능 카운터 구성](media/log-analytics-data-sources-performance-counters/configure-windows.png)

이 절차 tooadd 새 Windows 성능 카운터 toocollect를 따릅니다.

1. Hello 형태로 표시 hello 텍스트 상자에 hello 카운터의 유형 hello 이름을 *개체 (인스턴스) \counter*합니다.  입력을 시작하면 일치하는 공용 카운터 목록이 나타납니다.  하거나 hello 목록 또는 형식 자체에서 카운터를 선택할 수 있습니다.  *object\counter*를 지정하면 특정 카운터에 대한 모든 인스턴스를 반환할 수도 있습니다.  

    명명 된 인스턴스와에서 SQL Server 성능 카운터를 수집, 모든 명명 된 인스턴스 카운터 시작 *MSSQL$* hello hello 인스턴스 이름 뒤에 야 합니다.  예를 들어 toocollect hello 로그 Cache Hit Ratio 카운터에 대 한 명명 된 SQL 데이터베이스 성능 개체 hello에서에서 모든 데이터베이스 인스턴스 INST2, 한 지정 `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`합니다.

2. 클릭  **+**  하거나 키를 눌러 **Enter** tooadd hello 카운터 toohello 목록입니다.
3. Hello 기본값은 10 초 동안 사용 하 여 카운터를 추가 하면 해당 **샘플 간격**합니다.  성능 데이터를 수집 하는 hello tooreduce hello 저장소 요구 사항을 하려는 경우이 tooa의 값이 높을수록 too1800 초 (30 분)을 변경할 수 있습니다.
4. 추가 카운터를 마친 경우 클릭 hello **저장** hello 화면 toosave hello 구성의 hello 위쪽에 단추입니다.

### <a name="linux-performance-counters"></a>Linux 성능 카운터

![Linux 성능 카운터 구성](media/log-analytics-data-sources-performance-counters/configure-linux.png)

이 절차 tooadd 새 Linux 성능 카운터 toocollect를 따릅니다.

1. 기본적으로 모든 구성 변경 내용은 tooall 에이전트를 자동으로 이동 됩니다.  Linux 에이전트에 대 한 구성 파일에는 toohello Fluentd 데이터 수집기를 전송 됩니다.  각 Linux 에이전트에서 수동으로이 파일 toomodify 원하는 hello 확인란의 선택을 취소 한 다음 *구성 toomy Linux 컴퓨터 아래 적용* 아래 hello 지침을 따릅니다.
2. Hello 형태로 표시 hello 텍스트 상자에 hello 카운터의 유형 hello 이름을 *개체 (인스턴스) \counter*합니다.  입력을 시작하면 일치하는 공용 카운터 목록이 나타납니다.  하거나 hello 목록 또는 형식 자체에서 카운터를 선택할 수 있습니다.  
3. 클릭  **+**  하거나 키를 눌러 **Enter** tooadd hello 카운터 toohello hello 개체에 대 한 다른 카운터의 목록입니다.
4. 개체 사용에 대 한 모든 카운터 hello 동일 **샘플 간격**합니다.  hello 기본값은 10 초입니다.  성능 데이터를 수집 하는 hello tooreduce hello 저장소 요구 사항을 하려는 경우 too1800 초 (30 분)을의이 tooa 더 높은 값을 변경 합니다.
5. 추가 카운터를 마친 경우 클릭 hello **저장** hello 화면 toosave hello 구성의 hello 위쪽에 단추입니다.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>구성 파일에서 Linux 성능 카운터 구성
Hello OMS 포털을 사용 하 여 Linux 성능 카운터를 구성 하는 대신 hello Linux 에이전트에서 구성 파일 편집으로 인해 hello 선택할을 수 있습니다.  성능 메트릭 toocollect hello 구성에 의해 제어 됩니다 **/등/옵트인/microsoft/omsagent/\<작업 영역 id\>/conf/omsagent.conf**합니다.

각 개체 또는 성능 메트릭 toocollect의 범주는 단일 hello 구성 파일에 정의 되어야 합니다 `<source>` 요소입니다. hello 구문 아래 hello 패턴을 따릅니다.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


다음 표에 hello이 요소의 hello 매개 변수를 설명 합니다.

| 매개 변수 | 설명 |
|:--|:--|
| object\_name | Hello 컬렉션에 대 한 개체 이름입니다. |
| instance\_regex |  A *정규식* 어떤 인스턴스 toocollect를 정의 합니다. 값 hello: `.*` 모든 인스턴스를 지정 합니다. 만 hello에 대 한 프로세서 메트릭 toocollect \_지정 총 인스턴스 `_Total`합니다. 에 대 한 toocollect 프로세스 메트릭만 crond 또는 sshd 인스턴스에 hello, 지정할 수 있습니다: ' (crond\|sshd)`를 지정합니다. |
| counter\_name\_regex | A *정규식* 어떤 (hello 개체)에 대 한 카운터 toocollect를 정의 합니다. toocollect hello 개체에 대 한 모든 카운터 지정: `.*`합니다. hello 메모리 개체에 대 한만 스왑 공간 카운터만 toocollect, 예를 들어 지정할 수 있습니다.`.+Swap.+` |
| interval | 빈도 hello 개체의 카운터를 수집 합니다. |


hello 다음 표에 hello 개체 및 카운터를 hello 구성 파일에서 지정할 수 있습니다.  [Log Analytics에서 Linux 응용 프로그램에 대한 성능 카운터 수집](log-analytics-data-sources-linux-applications.md)에서 설명된 대로 특정 응용 프로그램에 사용할 수 있는 추가 카운터가 있습니다.

| 개체 이름 | 카운터 이름 |
|:--|:--|
| 논리 디스크 | % 사용 가능한 Inodes |
| 논리 디스크 | % 사용 가능한 공간 |
| 논리 디스크 | % 사용된 Inodes |
| 논리 디스크 | % 사용된 공간 |
| 논리 디스크 | 디스크 읽기 바이트/초  |
| 논리 디스크 | 디스크 읽기/초  |
| 논리 디스크 | 디스크 전송/초 |
| 논리 디스크 | 디스크 쓰기 바이트/초 |
| 논리 디스크 | 디스크 쓰기/초 |
| 논리 디스크 | 사용 가능한 메가바이트 |
| 논리 디스크 | 논리 디스크 바이트/초 |
| 메모리 | % 사용 가능한 메모리 |
| 메모리 | % 사용 가능한 스왑 공간 |
| 메모리 | % 사용된 메모리 |
| 메모리 | % 사용된 스왑 공간 |
| 메모리 | 사용 가능한 MB 메모리 |
| 메모리 | 사용 가능한 MB 스왑 |
| 메모리 | 페이지 읽기/초 |
| 메모리 | 페이지 쓰기/초 |
| 메모리 | 페이지/초 |
| 메모리 | 사용된 MB 스왑 공간 |
| 메모리 | 사용된 메모리 MB |
| 네트워크 | 전송된 총 바이트 |
| 네트워크 | 받은 총 바이트 |
| 네트워크 | 총 바이트 |
| 네트워크 | 전송된 총 패킷 |
| 네트워크 | 받은 총 패킷 |
| 네트워크 | 총 Rx 오류 |
| 네트워크 | 총 Tx 오류 |
| 네트워크 | 총 충돌 |
| 물리적 디스크 | 평균 디스크 초/읽기 |
| 물리적 디스크 | 평균 디스크 초/전송 |
| 물리적 디스크 | 평균 디스크 초/쓰기 |
| 물리적 디스크 | 물리적 디스크 바이트/초 |
| Process | Pct 권한이 부여된 시간 |
| Process | Pct 사용자 시간 |
| Process | 사용된 메모리 KB |
| Process | 가상 공유 메모리 |
| 프로세서 | % DPC 시간 |
| 프로세서 | % 유휴 시간 |
| 프로세서 | % 인터럽트 시간 |
| 프로세서 | % IO 대기 시간 |
| 프로세서 | % Nice 시간 |
| 프로세서 | % 권한이 부여된 시간 |
| 프로세서 | % Processor Time |
| 프로세서 | % 사용자 시간 |
| 시스템 | 사용 가능한 실제 메모리 |
| 시스템 | 페이징 파일에 사용 가능한 공간 |
| 시스템 | 사용 가능한 가상 메모리 |
| 시스템 | 프로세스 |
| 시스템 | 페이징 파일에 저장된 크기 |
| 시스템 | 작동 시간 |
| 시스템 | 사용자 |


다음은 성능 메트릭에 대 한 hello 기본 구성입니다.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>데이터 수집
Log Analytics는 카운터가 설치된 모든 에이전트에서 지정된 모든 성능 카운터를 지정된 샘플 간격으로 수집합니다.  hello 데이터가 집계 되지 않아서 및 hello 원시 데이터를 OMS 구독에 지정 된 hello 기간에 대 한 모든 로그 검색 보기에서 사용할 수 있습니다.

## <a name="performance-record-properties"></a>성능 레코드 속성
성능 기록에는 형식이 **성능** 한 hello 속성의 다음 표에 hello 합니다.

| 속성 | 설명 |
|:--- |:--- |
| 컴퓨터 |이벤트를 hello 하는 컴퓨터에서 수집 되었습니다. |
| CounterName |Hello 성능 카운터의 이름 |
| CounterPath |Hello 형태로 hello 카운터의 전체 경로 \\ \\ \<컴퓨터 >\\object(instance)\\카운터입니다. |
| CounterValue |Hello 카운터의 숫자 값입니다. |
| InstanceName |Hello 이벤트 인스턴스의 이름입니다.  인스턴스가 없으면 비어 있게 됩니다. |
| ObjectName |Hello 성능 개체의 이름 |
| SourceSystem |에이전트 hello 데이터의 형식에서 수집 되었습니다. <br><br>OpsManager – Windows 에이전트, 직접 연결 또는 SCOM <br> Linux – 모든 Linux 에이전트  <br> AzureStorage – Azure 진단 |
| TimeGenerated |날짜 및 시간 hello 데이터 샘플링 합니다. |

## <a name="sizing-estimates"></a>예상 크기 조정
 10초 간격으로 특정 카운터가 수집되는 양은 인스턴스당 일별 약 1MB입니다.  다음 수식을 hello로 특정 카운터의 hello 저장소 요구 사항을 예측할 수 있습니다.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>성능 레코드를 통한 로그 검색
hello 다음 표에서 다양 한 성능 레코드를 검색 하는 로그 검색 예.

| 쿼리 | 설명 |
|:--- |:--- |
| Type=Perf |모든 성능 데이터 |
| Type=Perf Computer="MyComputer" |특정 컴퓨터의 모든 성능 데이터 |
| Type=Perf CounterName="Current Disk Queue Length" |특정 컴퓨터에 대한 모든 성능 데이터 |
| Type=Perf (ObjectName=Processor) CounterName="% Processor Time" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU by Computer |모든 컴퓨터의 평균 CPU 사용률 |
| Type=Perf (CounterName="% Processor Time") &#124;  measure max(Max) by Computer |모든 컴퓨터의 최대 CPU 사용률 |
| Type=Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" &#124; measure Avg(Average) by InstanceName |지정된 된 컴퓨터의 모든 hello 인스턴스에서 평균 현재 디스크 큐 길이 |
| Type=Perf CounterName="DiskTransfers/sec" &#124; measure percentile95(Average) by Computer |모든 컴퓨터에 대한 디스크 전송/초의 95 백분위수 |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  &#124; measure avg(CounterValue) by Computer Interval 1HOUR |모든 컴퓨터에서 시간별 평균 CPU 사용량 |
| Type=Perf Computer="MyComputer" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |특정 컴퓨터에 대한 % 백분율 카운터당 시간별 70백분위수 |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  (Computer="MyComputer") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |특정 컴퓨터의 시간별 평균, 최소, 최대, 75백분위수 CPU 사용량 |
| Type=Perf ObjectName=“MSSQL$INST2:Databases” InstanceName=master | Hello 데이터베이스 성능에서 모든 성능 데이터 개체에서 명명 된 SQL Server 인스턴스 INST2 hello hello master 데이터베이스에 대 한 합니다.  

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.

> | 쿼리 | 설명 |
|:--- |:--- |
| Perf |모든 성능 데이터 |
| Perf &#124; where Computer == "MyComputer" |특정 컴퓨터의 모든 성능 데이터 |
| Perf &#124; where CounterName == "Current Disk Queue Length" |특정 컴퓨터에 대한 모든 성능 데이터 |
| Perf &#124; where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AVGCPU = avg(Average) by Computer |모든 컴퓨터의 평균 CPU 사용률 |
| Perf &#124; where CounterName == "% Processor Time" &#124; summarize AggregatedValue = max(Max) by Computer |모든 컴퓨터의 최대 CPU 사용률 |
| Perf &#124; where ObjectName == "LogicalDisk" and CounterName == "Current Disk Queue Length" and Computer == "MyComputerName" &#124; summarize AggregatedValue = avg(Average) by InstanceName |지정된 된 컴퓨터의 모든 hello 인스턴스에서 평균 현재 디스크 큐 길이 |
| Perf &#124; where CounterName == "DiskTransfers/sec" &#124; summarize AggregatedValue = percentile(Average, 95) by Computer |모든 컴퓨터에 대한 디스크 전송/초의 95 백분위수 |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), Computer |모든 컴퓨터에서 시간별 평균 CPU 사용량 |
| Perf &#124; where Computer == "MyComputer" and CounterName startswith_cs "%" and InstanceName == "_Total" &#124; summarize AggregatedValue = percentile(CounterValue, 70) by bin(TimeGenerated, 1h), CounterName | 특정 컴퓨터에 대한 % 백분율 카운터당 시간별 70백분위수 |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" and Computer == "MyComputer" &#124; summarize ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentile(CounterValue, 75), ["max(CounterValue)"] = max(CounterValue) by bin(TimeGenerated, 1h), Computer |특정 컴퓨터의 시간별 평균, 최소, 최대, 75백분위수 CPU 사용량 |
| Perf &#124; where ObjectName == "MSSQL$INST2:Databases" and InstanceName == "master" | Hello 데이터베이스 성능에서 모든 성능 데이터 개체에서 명명 된 SQL Server 인스턴스 INST2 hello hello master 데이터베이스에 대 한 합니다.  

## <a name="viewing-performance-data"></a>성능 데이터 보기
성능 데이터에 대 한 로그 검색을 실행 하면 hello **목록** 뷰가 기본적으로 표시 됩니다.  tooview hello 데이터를 그래픽 형식 클릭 **메트릭**합니다.  그래픽 정보를 자세히 확인할 클릭 hello  **+**  다음 tooa 카운터입니다.  

![축소된 메트릭 보기](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

로그 검색에 성능 데이터를 tooaggregate 참조 [주문형 메트릭 집계 및 OMS에서 시각화](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/)합니다.


## <a name="next-steps"></a>다음 단계
* MySQL 및 Apache HTTP 서버를 포함하여 [Linux 응용 프로그램에서 성능 카운터를 수집](log-analytics-data-sources-linux-applications.md)합니다.
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.  
* 수집 된 데이터를 너무 내보내기[Power BI](log-analytics-powerbi.md) 추가 시각화 및 분석에 대 한 합니다.
