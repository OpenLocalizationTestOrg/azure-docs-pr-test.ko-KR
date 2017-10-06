---
title: "aaaCapacity 및 Azure 로그 분석에서 성능 솔루션 | Microsoft Docs"
description: "사용 하 여 hello 용량 및 성능 솔루션을 이해 하는 로그 분석 toohelp hello Hyper-v 서버의 용량을 합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>용량 hello로 Hyper-v 가상 컴퓨터 용량 및 성능 솔루션 (미리 보기) 계획

![용량 및 성능 기호](./media/log-analytics-capacity/capacity-solution.png)

Hello 용량을 사용할 수 있습니다 및 이해 하는 로그 분석 toohelp에서 성능 솔루션 hello Hyper-v 서버의 용량을 합니다. hello 솔루션을 표시 하 여 Hyper-v 환경에 대 한 정보 hello hello 호스트의 전체 사용률 (CPU, 메모리 및 디스크) 및 해당 Hyper-v 호스트에서 실행 중인 Vm hello를 제공 합니다. 모든 호스트와 hello Vm에서 실행 중인 CPU, 메모리 및 디스크에 대 한 메트릭이 수집 됩니다.

hello 해결 방법:

-   최고 및 최저 CPU 및 메모리 사용률을 가진 호스트를 보여 줍니다.
-   최고 및 최저 CPU 및 메모리 사용률을 가진 VM을 보여 줍니다.
-   최고 및 최저 IOPS 및 처리량 사용률을 가진 VM을 보여 줍니다.
-   어떤 호스트에서 어떤 VM이 실행되고 있는지 보여 줍니다.
-   Hello 상위 디스크 IOPS, 높은 처리량 및 대기 시간에 클러스터 공유 볼륨을 보여 줍니다.
- 그룹을 기준으로 필터링 하 고 toocustomize 있습니다.

> [!NOTE]
> 이전 버전의 hello 용량 및 성능 솔루션 용량 관리 라는 hello System Center Operations Manager 및 System Center Virtual Machine Manager 모두 필요 합니다. 업데이트된 이 솔루션에는 이러한 종속성이 없습니다.


## <a name="connected-sources"></a>연결된 소스

다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 원본에 설명 합니다.

| 연결된 소스 | 지원 | 설명 |
|---|---|---|
| [Windows 에이전트](log-analytics-windows-agents.md) | 예 | hello 솔루션 Windows 에이전트에서 용량 및 성능 데이터 정보를 수집합니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요    | hello 솔루션 직접 Linux 에이전트에서 용량 및 성능 데이터 정보를 수집 하지 않습니다.|
| [SCOM 관리 그룹](log-analytics-om-agents.md) | 예 |hello 솔루션 연결된 SCOM 관리 그룹의 에이전트에서 용량 및 성능 데이터를 수집합니다. Hello SCOM 에이전트 tooOMS의 직접 연결 필요 하지 않습니다. Hello 관리 그룹 toohello OMS 리포지토리에서 데이터 전달 됩니다.|
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | Azure 저장소는 용량 및 성능 데이터를 포함하지 않습니다.|

## <a name="prerequisites"></a>필수 조건

- Windows 또는 Operations Manager 에이전트는 가상 컴퓨터가 아닌 Windows Server 2012 이상의 Hyper-V 호스트에 설치해야 합니다.


## <a name="configuration"></a>구성

Hello 단계 tooadd hello 용량 및 성능 솔루션 tooyour 작업 영역을 다음을 수행 합니다.

- Hello 용량 및 성능 솔루션 tooyour OMS 작업 영역 hello 프로세스를 사용 하는에 설명 된 추가 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.

## <a name="management-packs"></a>관리 팩

연결 된 tooyour OMS 작업 영역에 SCOM 관리 그룹을 사용 하는 경우 다음 다음 관리 팩 hello는 설치 하도록 SCOM에서이 솔루션을 추가 합니다. 이 관리 팩에 대한 구성 또는 유지 관리는 필요 없습니다.

- Microsoft.IntelligencePacks.CapacityPerformance

hello 1201 이벤트와 유사합니다.


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Hello 용량 및 성능 솔루션 업데이트 되 면 hello 버전 번호가 변경 됩니다.

솔루션 관리 팩 업데이트 되는 방식에 대 한 자세한 내용은 참조 하십시오. [Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md)합니다.

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

Hello 용량 및 성능 솔루션 tooyour 작업 영역에 추가 하면 hello 용량 및 성능 toohello 개요 대시보드에 추가 됩니다. 이 타일 hello 현재 활성 상태인 Hyper-v 호스트 수 및 hello 수가 hello 시간 선택한 기간에 대 한 모니터링 않은 활성 가상 컴퓨터의 수를 표시 합니다.

![용량 및 성능 타일](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>사용률 검토

클릭 hello 용량 및 성능은 타일 tooopen hello 용량 및 성능 대시보드 합니다. hello 대시보드는 다음 표에 hello에 hello 열을 포함 합니다. 각 열 hello에 대 한 열의 조건을 범위 및 시간 범위를 지정 했는지 일치 tooten 항목을 나열 합니다. 클릭 하 여 모든 레코드를 반환 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 열의 또는 hello 열 머리글을 클릭 하 여 hello 맨 아래에 있습니다.

- **호스트**
    - **호스트 CPU 사용량** hello 특정 기간에 따라 호스트의 목록과 호스트 컴퓨터의 hello CPU 사용률의 추세 그래픽을 표시 합니다. 시간에서 hello 꺾은선형 차트 tooview 세부 정보는 특정 시점에 대 한 포인터로 가리킵니다. 로그 검색에 대 한 자세한 내용은 hello 차트 tooview를 클릭 합니다. 모든 호스트 이름 tooopen 로그 검색을 클릭 하 고 호스팅된 Vm에 대 한 CPU 카운터 세부 정보를 확인 합니다.
    - **호스트 메모리 사용률이** hello 특정 기간에 따라 호스트의 목록과 호스트 컴퓨터의 메모리 사용률이 hello의 그래픽 추세를 보여 줍니다. 시간에서 hello 꺾은선형 차트 tooview 세부 정보는 특정 시점에 대 한 포인터로 가리킵니다. 로그 검색에 대 한 자세한 내용은 hello 차트 tooview를 클릭 합니다. 호스팅된 Vm에 대 한 모든 호스트 이름 tooopen 로그 검색 및 보기 메모리 카운터 세부 정보를 클릭 합니다.
- **가상 컴퓨터**
    - **VM의 CPU 사용률** hello 특정 기간에 따라 가상 컴퓨터의 목록과 가상 컴퓨터의 hello CPU 사용률의 추세 그래픽을 표시 합니다. 특정 시점에 대 한 hello 꺾은선형 차트 tooview 정보에서에서 마우스로 시간 hello 상위 3 개의 Vm에 대 한 합니다. 로그 검색에 대 한 자세한 내용은 hello 차트 tooview를 클릭 합니다. 모든 VM 이름 tooopen 로그 검색을 클릭 하 고 hello VM에 대 한 집계 된 CPU 카운터 세부 정보를 확인 합니다.
    - **VM 메모리 사용률** hello 특정 기간에 따라 가상 컴퓨터의 목록과 가상 컴퓨터의 메모리 사용률이 hello의 그래픽 추세를 보여 줍니다. 특정 시점에 대 한 hello 꺾은선형 차트 tooview 정보에서에서 마우스로 시간 hello 상위 3 개의 Vm에 대 한 합니다. 로그 검색에 대 한 자세한 내용은 hello 차트 tooview를 클릭 합니다. 모든 VM 이름 tooopen 로그 검색을 클릭 하 고 hello VM에 대 한 집계 된 메모리 카운터 세부 정보를 확인 합니다.
    - **총 디스크 IOPS VM** hello의 그래픽 추세는 총 표시 hello 특정 기간에 따라 각 항목에 대해 IOPS hello로 가상 컴퓨터의 목록과 가상 컴퓨터에 대 한 디스크 IOPS입니다. 특정 시점에 대 한 hello 꺾은선형 차트 tooview 정보에서에서 마우스로 시간 hello 상위 3 개의 Vm에 대 한 합니다. 로그 검색에 대 한 자세한 내용은 hello 차트 tooview를 클릭 합니다. 모든 VM 이름 tooopen 로그 검색 및 집계 된 디스크 IOPS 카운터 hello VM에 대 한 세부 정보 보기를 클릭 합니다.
    - **VM 총 디스크 처리량** 특정 기간 가상 컴퓨터 및 각각에 대 한 전체 디스크 처리량 hello 있는 가상 컴퓨터의 목록에 따라 hello에 대 한 hello 총 디스크 처리량의 추세 그래픽으로 보여 줍니다. 특정 시점에 대 한 hello 꺾은선형 차트 tooview 정보에서에서 마우스로 시간 hello 상위 3 개의 Vm에 대 한 합니다. 로그 검색에 대 한 자세한 내용은 hello 차트 tooview를 클릭 합니다. 모든 VM 이름 tooopen 로그 검색을 클릭 하 고 hello VM에 대 한 집계 된 총 디스크 처리량 카운터 세부 정보를 확인 합니다.
- **클러스터된 공유 볼륨**
    - **총 처리량** 둘 다의 hello 합계 읽기 및 클러스터 된 공유 볼륨에 쓰기를 보여 줍니다.
    - **총 IOPS** 클러스터 된 공유 볼륨에 초당 입력/출력 작업의 hello 합계를 보여 줍니다.
    - **총 대기 시간** 클러스터 된 공유 볼륨에 hello 총 대기 시간을 보여 줍니다.
- **밀도 호스트** hello 상위 타일 hello 사용 가능한 toohello 솔루션 호스트 및 가상 컴퓨터의 총 수를 표시 합니다. Hello 상위 타일 tooview 로그 검색에 추가 정보를 클릭 합니다. 또한 모든 호스트 및 호스트 되는 가상 컴퓨터의 hello 수를 나열 합니다. 로그 검색에 대 한 hello VM 결과로 호스트 toodrill를 클릭 합니다.


![호스트 블레이드 대시보드](./media/log-analytics-capacity/dashboard-hosts.png)

![가상 컴퓨터 블레이드 대시보드](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>성능 평가

프로덕션 컴퓨팅 환경에서 한 조직 tooanother 크게 다릅니다. 또한 용량 및 성능 워크로드는 VM을 실행하는 방법 및 일반적인 고려 사항에 따라 달라질 수 있습니다. 성능을 측정 하는 구체적인 절차 toohelp tooyour 환경을 적용 되지 않습니다. 지침 더 일반화 되므로 적합 한 toohelp 합니다. Microsoft는 다양 한 게시 지침 문서 toohelp의 성능을 측정 합니다.

hello 솔루션 toosummarize, 다양 한 성능 카운터를 포함 한 소스에서에서 용량 및 성능 데이터를 수집 합니다. Hello 솔루션의 다양 한 화면에 표시는 해당 용량 및 성능 데이터를 사용 하 고 hello에 프로그램 결과 toothose 비교 [Hyper-v에 대 한 성능 측정](https://msdn.microsoft.com/library/cc768535.aspx) 문서. Hello 문서는 얼마 전에 게시, 있지만 hello 메트릭과 고려 사항, 지침은 여전히 유효 합니다. hello 문서 링크 tooother 유용한 리소스를 포함합니다.


## <a name="sample-log-searches"></a>샘플 로그 검색

다음 표에서 hello 수집 되 고이 솔루션에서 계산 용량 및 성능 데이터에 대 한 예제 로그 검색을 제공 합니다.

| 쿼리 | 설명 |
|---|---|
| 모든 호스트 메모리 구성 | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| 모든 VM 메모리 구성 | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| 모든 VM의 총 디스크 IOPS 분석 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 모든 VM의 총 디스크 처리량 분석 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 모든 CSV의 총 IOPS 분석 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 모든 CSV의 총 처리량 분석 | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| 모든 CSV의 총 대기 시간 분석 | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.

> | 쿼리 | 설명 |
|:--- |:--- |
| 모든 호스트 메모리 구성 | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "Host Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| 모든 VM 메모리 구성 | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "VM Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| 모든 VM의 총 디스크 IOPS 분석 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Reads/s" or CounterName == "VHD Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 모든 VM의 총 디스크 처리량 분석 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Read MB/s" or CounterName == "VHD Write MB/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 모든 CSV의 총 IOPS 분석 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 모든 CSV의 총 처리량 분석 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| 모든 CSV의 총 대기 시간 분석 | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Read Latency" or CounterName == "CSV Write Latency") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>다음 단계
* 사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview 용량 및 성능 데이터를 자세히 설명 합니다.
