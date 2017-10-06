---
title: "Azure 로그 분석에서 aaaUsing hello 로그 검색 포털 | Microsoft Docs"
description: "이 문서에 toocreate 로그를 검색 하 고 hello 로그 검색 포털을 사용 하 여 로그 분석 작업 영역에 저장 된 데이터를 분석 하는 방법을 설명 하는 자습서에 포함 됩니다.  서로 다른 유형의 데이터를 tooreturn 간단한 쿼리를 실행 하 고 결과 분석 hello 자습서에 포함 됩니다."
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
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Hello 로그 검색 포털을 사용 하는 Azure 로그 분석에서 로그 검색을 만들려면

> [!NOTE]
> 이 문서에서는 hello 새로운 쿼리 언어를 사용 하 여 Azure 로그 분석에서 로그 검색 포털 hello를 설명 합니다.  Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.  
>
> 작업 영역에는 업그레이드 된 toohello 새로운 쿼리 언어 되지 않았는지를 하는 경우를 참조 해야 너무[로그 분석 로그 검색을 사용 하 여 데이터를 찾을](log-analytics-log-searches.md) hello hello 로그 검색 포털의 최신 버전에 대 한 내용은 합니다.

이 문서에 toocreate 로그를 검색 하 고 hello 로그 검색 포털을 사용 하 여 로그 분석 작업 영역에 저장 된 데이터를 분석 하는 방법을 설명 하는 자습서에 포함 됩니다.  서로 다른 유형의 데이터를 tooreturn 간단한 쿼리를 실행 하 고 결과 분석 hello 자습서에 포함 됩니다.  직접 수정 하지 않고 hello 쿼리를 수정에 대 한 hello 로그 검색 포털의 기능에 중점을 둡니다.  Hello 쿼리를 직접 편집에 대 한 자세한 내용은 참조 hello [쿼리 언어 참조](https://go.microsoft.com/fwlink/?linkid=856079)합니다.

hello 로그 검색 포털 대신 hello 고급 분석 포털에서 toocreate 검색 참조 [hello 분석 포털 시작](https://go.microsoft.com/fwlink/?linkid=856587)합니다.  두 포털 hello를 사용 하 여 동일한 쿼리 언어 tooaccess hello hello 로그 분석 작업 영역에서 같은 데이터입니다.

## <a name="prerequisites"></a>필수 조건
이 자습서 쿼리 tooanalyze hello에 대 한 데이터를 생성 하는 하나 이상의 연결 된 원본에 있는 로그 분석 작업 영역이 이미 있다고 가정 합니다.  

- 작업 영역에 없으면 무료 하나 만들 수 있습니다에 hello 절차를 사용 하 여 [로그 분석 작업 영역 시작](log-analytics-get-started.md)합니다.
- 하나 이상의 연결 [Windows 에이전트](log-analytics-windows-agents.md) 또는 한 개의 [Linux 에이전트](log-analytics-linux-agents.md) toohello 작업 영역입니다.  

## <a name="open-hello-log-search-portal"></a>열기 hello 로그 검색 포털
Hello 로그 검색 포털을 열어 시작 합니다.  Hello Azure 포털 또는 hello OMS 포털에 액세스할 수 있습니다.

1. Azure 포털 hello를 엽니다.
2. 분석 tooLog 찾아서 작업 영역을 선택 합니다.
3. 선택 하거나 **로그 검색** Azure 포털 또는 시작 hello OMS 포털을 선택 하 여 hello에 toostay **OMS 포털** hello 로그 검색 단추를 클릭 합니다.

![로그 검색 단추](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>단순 검색 만들기
가장 빠른 방법은 tooretrieve hello와 일부 데이터 toowork 테이블의 모든 레코드를 반환 하는 간단한 쿼리를입니다.  경우 모든 windows 또는 Linux 클라이언트 연결 된 tooyour 작업 영역 데이터 이벤트 (Windows) 또는 Syslog (Linux) 테이블 하거나 hello에 더 합니다.

하나의 hello 쿼리 hello 검색 상자에 다음을 입력 하 고 hello 검색 단추를 클릭 합니다.  

```
Event
```
```
Syslog
```

Hello 기본 목록 보기에 데이터가 반환 됩니다 하 고 반환 된 총 레코드 수를 확인할 수 있습니다.

![단순 쿼리](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

만 hello 각 레코드의 첫 번째 몇 가지 속성 표시 됩니다.  클릭 **자세히 표시** toodisplay 특정 레코드에 대 한 모든 속성.

![레코드 세부 정보](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Hello 시간 범위 설정
로그 분석에 의해 수집 된 모든 레코드에는 **TimeGenerated** 해당 hello 레코드가 생성 된 hello 날짜 및 시간을 포함 하는 속성입니다.  Hello 로그 검색 포털에서 쿼리 된 레코드만 반환는 **TimeGenerated** hello hello 화면의 왼쪽에 표시 되는 hello 시간 범위 내에서.  

Hello 드롭다운을 선택 하거나 hello 슬라이더를 수정 하 여 hello 시간 필터를 변경할 수 있습니다.  hello 슬라이더 hello 상대 hello 범위 내에서 각 시간 세그먼트에 대 한 레코드 수를 표시 하는 막대 그래프를 표시 합니다.  이 세그먼트는 hello 범위에 따라 달라 집니다.

hello 기본 시간 범위는 **1 일**합니다.  이 값도 변경**7 일**, 및 hello 레코드의 총 수는 증가 해야 합니다.

![날짜 시간 범위](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Hello 쿼리의 결과 필터링 합니다.
Hello에 hello 화면 왼쪽에는 직접 수정 하지 않고 필터링 toohello 쿼리 tooadd 수 있는 hello 필터 창입니다.  반환 된 hello 레코드의 여러 속성을 해당 레코드 수와 상위 10 개의 값과 함께 표시 됩니다.

작업 하는 경우 **이벤트**, 선택 hello 확인란 옆 너무**오류** 아래 **EVENTLEVELNAME**합니다.   작업 하는 경우 **Syslog**, 선택 hello 확인란 옆 너무**err** 아래 **SEVERITYLEVEL**합니다.  이 변경의 hello toolimit hello 다음 tooone 결과 tooerror 이벤트 hello 쿼리 됩니다.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

선택 하 여 추가 속성 toohello 필터 창 **toofilters 추가** hello 속성 메뉴에서 hello 레코드 중 하나입니다.

![Toofilter 메뉴 추가](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

동일한 필터를 선택 하 여 hello를 설정할 수 있습니다 **필터** toofilter hello 값이 있는 레코드에 대 한 hello 속성 메뉴에서 원하는 합니다.  

Hello를 하나만 **필터** 파란색에 있는 이름 사용 하 여 속성에 대 한 옵션입니다.  이러한 필드는 검색 조건에 대해 인덱싱되는 *검색 가능* 필드입니다.  회색 필드는 *텍스트로 검색 가능한 자유* hello에만 있는 필드 **참조 표시** 옵션입니다.  이 옵션은 속성에 해당 값이 포함된 레코드를 반환합니다.

![필터 메뉴](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Hello를 선택 하 여 단일 속성에 대 한 hello 결과 그룹화 할 수 있습니다 **그룹화** hello 레코드 메뉴 옵션입니다.  이렇게 하면 추가 됩니다 한 [요약](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) hello 결과 차트에 표시 하는 연산자 tooyour 쿼리 합니다.  둘 이상의 속성을 그룹화 할 수 있습니다 하지만 tooedit hello 쿼리를 직접 할 수 있습니다.  선택 hello 레코드 메뉴 다음 hello hello **컴퓨터** 속성과 선택 **Group by 'Computer'**합니다.  

![컴퓨터를 기준으로 그룹화](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>결과 작업
hello 로그 검색 포털에는 다양 한 쿼리 결과 hello 사용 하기 위한 기능입니다.  정렬할 수 있습니다, 필터 및 그룹 tooanalyze hello 데이터 hello 실제 쿼리를 수정 하지 않고 결과입니다.  기본적으로 쿼리 결과는 정렬되지 않습니다.

tooview hello 데이터를 필터링 및 정렬에 대 한 추가 옵션을 제공 하는 테이블 형식 클릭 **테이블**합니다.  

![테이블 보기](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

해당 레코드에 대 한 레코드 tooview hello 세부 정보에서 hello 화살표를 클릭 합니다.

![결과 정렬](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

필드의 열 머리글을 클릭하여 필드를 정렬할 수 있습니다.

![결과 정렬](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Hello 필터 단추를 클릭 하 고 필터 조건을 제공 하 여 hello 열에 특정 값에 hello 결과 필터링 합니다.

![결과 필터링](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Hello 결과의 열 머리글 toohello 위쪽을 끌어서 열을 그룹화 합니다.  여러 열 toohello 위쪽을 끌어서 여러 필드에서 그룹화 수 있습니다.

![결과 그룹화](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>성능 데이터 사용
Windows 및 Linux 에이전트에 대 한 성능 데이터는 hello에 hello 로그 분석 작업 영역에 저장 **성능** 테이블입니다.  성능 레코드는 다른 레코드와 비슷하며, 이벤트와 마찬가지로 모든 성능 레코드를 반환하는 단순 쿼리를 작성할 수 있습니다.

```
Perf
```

![성능 데이터](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

모든 성능 개체와 카운터의 레코드 수백만 개가 반환된다면 원하는 데이터를 찾기가 어렵습니다.  동일한 방법을 hello 다음을 입력 하거나 toofilter hello 데이터 위에 사용 하면 쿼리 hello hello 로그 검색 상자에 직접 사용할 수 있습니다.  이 경우 Windows 및 Linux 컴퓨터의 프로세서 사용률 레코드만 반환됩니다.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![프로세서 사용률](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

이 인해 hello 데이터 tooa 특정 카운터에 제한 하기는 하지만 것 여전히 하지 않습니다는 특히 유용 형태로 합니다.  Hello 데이터는 꺾은선형 차트를 표시할 수 있지만 toogroup 먼저 컴퓨터와 TimeGenerated 여 합니다.  여러 필드에 대해 toogroup, 해야 toomodify hello 쿼리를 직접 hello 쿼리 toohello 다음 하므로 수정 합니다.  Hello를 사용 하 여이 [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) 함수 hello에 **CounterValue** 속성 toocalculate hello 각 1 시간 동안 평균 값입니다.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![성능 데이터 차트](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Hello 데이터를 그룹화 하는 적절 하 게 했으므로 표시할 수 있습니다 시각적 차트에 hello를 추가 하 여 [렌더링](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) 연산자입니다.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![꺾은선형 차트](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>다음 단계

- Hello 로그 분석 쿼리 언어에 대 한 자세한 [hello 분석 포털 시작](https://go.microsoft.com/fwlink/?linkid=856079)합니다.
- Hello를 사용 하 여 자습서 살펴보면서 [Advanced Analytics 포털](https://go.microsoft.com/fwlink/?linkid=856587) toorun hello 수 있는 동일한 쿼리 및 액세스 hello hello 로그 검색 포털와 동일한 데이터입니다.
