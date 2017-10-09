---
title: "Azure 로그 분석에서 로그 검색을 사용 하 여 aaaFind 데이터 | Microsoft Docs"
description: "로그 검색 toocombine 사용 하면 사용자 환경 내에서 여러 원본의 모든 컴퓨터 데이터를 서로 연결 하 고 있습니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Log Analytics에서 로그 검색을 사용하여 데이터 찾기

>[!NOTE]
> 이 문서에서는 로그 분석에 hello 현재 쿼리 언어를 사용 하 여 로그 검색을 설명 합니다.  작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 너무 참조 해야 하는 다음[로그 분석 (새)에 있는 이해 로그 검색](log-analytics-log-search-new.md)합니다.


사용자 환경 내에서 여러 원본의 모든 컴퓨터 데이터를 서로 연결 하 고 로그 분석의 hello 핵심은 toocombine 수 있는 hello 로그 검색 기능. 솔루션에서 특정 문제 영역 주위에 피벗 된 메트릭을 하면 로그 검색 toobring 제공 되어 있습니다.

Hello 검색 페이지에서 쿼리를 만들 수 있습니다 및 다음 검색 하는 경우 필터링 할 수 있습니다 hello 결과 패싯 컨트롤을 사용 하 여 합니다. 또한 결과 tootransform 고급 쿼리, 필터 및 보고서를 만들 수 있습니다.

일반적인 로그 검색 쿼리는 대부분의 솔루션 페이지에 표시됩니다. Hello OMS 콘솔에서 타일을 클릭 하거나 로그 검색을 사용 하 여 hello 항목에 대 한 세부 정보 tooview을 tooother 항목에서 드릴 수 있습니다.

이 자습서에서는 살펴봅니다 예제 toocover 모든 hello 기본 로그 검색을 사용 하는 경우.

다음에 빌드 방법을 toouse hello 구문 tooextract hello insights에서에서 원하는 hello 데이터에 대 한 실용적인 사용 사례에 대 한 이해가 얻을 수 있도록 알아보고 간단 하 고 실용적인 예제부터 시작 하겠습니다.

검색 기법을 알아본 후 hello을 검토할 수 있습니다 [로그 분석 로그 검색 참조](log-analytics-search-reference.md)합니다.

## <a name="use-basic-filters"></a>기본 필터 사용
hello 먼저 tooknow는 hello 첫 번째 부분의 앞 검색 쿼리를 "|" 세로줄 문자는 항상 한 *필터*합니다. TSQL에서 WHERE 절로 결정의 생각할 수 *어떤* hello OMS 데이터 저장소에서 데이터 toopull의 하위 집합입니다. Hello 데이터 저장소에서 검색은 대개 지정 하므로 쿼리가 WHERE 절 hello로 시작 하는 자연 tooextract, 원하는 hello 데이터의 hello 특성입니다.

hello 사용할 수 있는 가장 기본적인 필터는 *키워드*'오류' 또는 '시간 제한' 또는 컴퓨터 이름과 같은 합니다. 이러한 유형의 간단한 쿼리는 일반적으로 다양 한 도형을 반환할 hello 내 데이터의 동일한 결과 집합입니다. 로그 분석에 다른 때문에 이것이 *형식* hello 시스템의 데이터입니다.

### <a name="tooconduct-a-simple-search"></a>단순 검색 tooconduct
1. Hello OMS 포털에서 클릭 **로그 검색**합니다.  
    ![검색 타일](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. Hello 쿼리 필드에 입력 `error` 클릭 하 고 **검색**합니다.  
    ![검색 오류](./media/log-analytics-log-searches/oms-search-error.png)  
    에 대 한 예를 들어 hello 쿼리 `error` hello 다음 이미지 반환 100000 **이벤트** 레코드 (로그 관리에서 수집), 18 **ConfigurationAlert** 레코드 (구성으로 생성 합니다. 평가) 및 12 **ConfigurationChange** 레코드 (hello 변경 내용 추적에서 캡처) 합니다.   
    ![검색 결과](./media/log-analytics-log-searches/oms-search-results01.png)  

이러한 필터는 실제로 개체 유형/클래스가 아닙니다. *형식* 은 한 개의 태그, 또는 속성, 또는 문자열/이름/범주 이며 있는 tooa 하나의 데이터를 연결 합니다. Hello 시스템의 일부 문서 분류 **유형: ConfigurationAlert** 고 일부는 **유형: 성능**, 또는 **유형: 이벤트**등. 각 검색 결과, 문서, 레코드 또는 항목의 데이터를 이러한 각 작업에 대 한 hello 원시 속성 및 해당 값 표시 및 사용 하 여 이러한 필드 이름은 toospecify hello 필터에서 tooretrieve hello 레코드만 하려는 경우 여기서 hello 필드에 지정 된이 값입니다.

*유형*은 실제로 모든 레코드가 있는 필드이며 다른 필드와 다르지 않습니다. Hello 형식 필드의 hello 값을 기준으로 설정 되었습니다. 해당 레코드를 다른 형태 또는 모습을 갖습니다. 참고로, **유형 = Perf**, 또는 **유형 =** 성능 데이터 또는 이벤트에 대 한 toolearn tooquery 할 hello 구문 이기도 합니다.

Hello 필드 이름 및 hello 값 앞에 콜론 (:) 또는 등호 (=) 중 하나를 사용할 수 있습니다. **Type: Event** 및 **유형 =** 에 해당 하는 의미를 선택할 수 있습니다 hello 원하는 스타일입니다.

따라서 경우 hello 형식 = Perf 레코드 'CounterName' 라는 필드가 있는 다음 비슷한 쿼리를 작성할 수 있습니다 `Type=Perf CounterName="% Processor Time"`합니다.

이렇게 하면 있습니다 hello 성능 데이터만 hello 성능 카운터 이름 "% Processor Time"입니다.

### <a name="toosearch-for-processor-time-performance-data"></a>프로세서 시간 성능 데이터에 대 한 toosearch
* Hello 검색 쿼리 필드에 입력`Type=Perf CounterName="% Processor Time"`

더 정확 하 게 하 고 사용할 수도 있습니다 **InstanceName = _'total '** Windows 성능 카운터는 hello 쿼리 합니다. 또한 패싯 및 다른 **field:value**을 선택할 수 있습니다. hello 필터 hello 쿼리 표시줄에 tooyour 필터를 자동으로 추가 됩니다. 다음 이미지는 hello에서 볼 수 있습니다. 표시 여기서 tooclick tooadd **InstanceName: '_Total'** 아무것도 입력 하지 않고 toohello 쿼리 합니다.

![검색 패싯](./media/log-analytics-log-searches/oms-search-facet.png)

쿼리는 `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

이 예제에서는 toospecify 없는 **유형 = Perf** tooget toothis 결과입니다. Hello 필드 CounterName 및 InstanceName 종류의 레코드에만 존재 하므로 = Perf, hello 쿼리는 모호한 tooreturn hello 동일한 결과 더 긴 이전과 hello:

```
CounterName="% Processor Time" InstanceName="_Total"
```

이 hello 쿼리에서 모든 hello 필터에 있는 것으로 평가 되기 때문 *AND* 서로 합니다. 효과적으로 hello toohello 조건을 추가 하면 필드 더 할수록 더 구체적이 고 구체화 된 결과입니다.

예를 들어 hello 쿼리 `Type=Event EventLog="Windows PowerShell"` 는 너무 동일`Type=Event AND EventLog="Windows PowerShell"`합니다. 로그인 하 고 hello Windows PowerShell 이벤트 로그에서 수집 된 모든 이벤트를 반환 합니다. 추가 하는 경우 필터를 여러 번 반복 해 서 hello 동일한 패싯을 다음 hello 문제는 순수 하 게 외관상 hello 검색 표시줄을 채울 수 있지만 여전히 결과 반환 hello 같은 hello 암시적 AND 연산자가 항상 있기 때문에 선택 하 여 합니다.

NOT 연산자를 명시적으로 사용 하 여 쉽게 암시적 AND 연산자 hello를 되돌릴 수 있습니다. 예:

`Type:Event NOT(EventLog:"Windows PowerShell")`또는 이와 동등한 `Type=Event EventLog!="Windows PowerShell"` hello Windows PowerShell 로그 되지 않은 모든 로그에서 모든 이벤트를 반환 합니다.

또는 'OR'같은 다른 부울 연산자를 사용할 수 있습니다. hello 다음 쿼리는 hello에 대 한 이벤트 로그는 두 응용 프로그램 또는 시스템 레코드를 반환 합니다.

```
EventLog=Application OR EventLog=System
```

위의 쿼리는 hello를 사용 하 여 항목 얻을 수 있습니다 both 로그에 대 한 hello에서 동일한 결과 집합입니다.

그러나 hello 또는 hello 암시적 AND 두어 위치를 제거 하면 다음 hello 다음 쿼리 생성 하지 않습니다 결과 tooBOTH 로그에 속하는 이벤트 로그 항목이 없기 때문에 있습니다. 각 이벤트 로그 항목 tooonly hello 두 로그 중 하나 작성 되었습니다.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>추가 필터 사용
hello 다음 쿼리는 반환 데이터를 전송 하는 모든 hello 컴퓨터에 대 한 2 개의 이벤트 로그에 대 한 항목입니다.

```
EventLog=Application OR EventLog=System
```

![검색 결과](./media/log-analytics-log-searches/oms-search-results03.png)

Hello 필드 또는 필터 중 하나를 선택 하면 hello 쿼리 tooa 제외 특정 컴퓨터를 모든 다른 좁혀집니다. hello 결과 쿼리는 hello 다음과 유사 합니다.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Hello 때문에 해당 하는 toohello 다음 변수인 암시적 and.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

각 쿼리 명시적 순서에 따라 hello에 평가 됩니다. 참고 hello 괄호가 있습니다.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Hello 이벤트 로그 필드와 마찬가지로 추가 하 여 특정 컴퓨터 집합에 대 한 데이터를 검색할 수 있습니다 또는 합니다. 예:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

마찬가지로, 다음 쿼리 반환이이 hello **CPU 시간 %** hello 두 컴퓨터를 선택 합니다.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>필드 형식
필터를 만들 때 다양 한 유형의 필드를 로그 검색에서 반환 된 작업의 hello 차이 이해 해야 합니다.

**검색 가능한 필드**는 검색 결과에 파란색으로 표시됩니다.  Hello 다음과 같은 검색 조건 특정 toohello 필드에 검색 가능한 필드를 사용할 수 있습니다.

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**자유 텍스트 검색 가능 필드**는 검색 결과에서 회색으로 표시됩니다.  검색 가능한 필드와 같은 검색 조건 특정 toohello 필드와 사용할 수 없습니다.  값 형식은 hello 다음과 같은 모든 필드에서 쿼리를 수행할 때 검색 됩니다.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>부울 연산자
날짜/시간 및 숫자 필드를 사용하여 *보다 큼*, *보다 작음*, *보다 작거나 같음*을 사용하는 값을 검색할 수 있습니다. 와 같은 간단한 연산자를 사용할 수 있습니다 >, <>, =, < =,! = hello 쿼리 검색 표시줄에 있습니다.

특정 기간에 특정 이벤트 로그를 쿼리할 수 있습니다. 예를 들어 hello 지난 24 시간 동안은 표현 다음 mnemonic 식 hello로 합니다.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>부울 연산자를 사용 하 여 toosearch
* Hello 검색 쿼리 필드에 입력`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![부울 값을 사용하여 검색](./media/log-analytics-log-searches/oms-search-boolean.png)

제어할 수 있지만 시간 간격을 그래픽으로 hello 하 고 대부분의 시간 toodo 발생 하는 이점을 tooincluding hello 쿼리에 직접 시간 필터를 설정할 수 있습니다. 예를 들어이 방식은 효과적 hello에 관계 없이 각 타일에 대 한 hello 시간을 재정의할 수 대시보드와 *글로벌* hello 대시보드 페이지에서 시간 선택기입니다. 자세한 내용은 [대시보드에서 시간 문제](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/)를 참조하십시오.

시간별으로 필터링 하는 경우 유의 hello에 대 한 결과 얻을 *교차* hello의 두 기간의: hello OMS 포털 (S1)에 지정 된 hello 및 hello 쿼리 (S2)에 지정 된 hello 합니다.

![교집합](./media/log-analytics-log-searches/oms-search-intersection.png)

즉, hello 기간이 교차 하지 않는, 예를 들어 선택할 수 있는 hello OMS 포털의 경우 **이번 주** hello 쿼리에서 정의 하는 경우 **지난주**, 교차가 없습니다 및 사용자가 없습니다 어떤 결과도 받을 수 있습니다.

Hello TimeGenerated 필드에 사용 되는 비교 연산자가 다른 경우에도 유용 합니다. 예를 들어 숫자 필드를 사용하는 경우입니다.

예를 들어을 가진다 고 구성 평가 경고 심각도 값을 다음 hello:

* 0 = 정보
* 1 = 경고
* 2 = 중요

경고 및 위험 경고에 대 한 쿼리 및 다음 쿼리는 hello 쿼리하고 정보를 제외할 수 있습니다.

```
Type=ConfigurationAlert  Severity>=1
```


범위 쿼리를 사용할 수 있습니다. 즉, 시퀀스에 있는 값의 hello 시작 및 끝 범위를 제공할 수 있습니다. 예를 들어 여기서 hello hello Operations Manager 이벤트 로그에서 이벤트를 하려는 경우 EventID가 보다 크거나 같은 too2100 넘지 않는, 2199 hello 다음 쿼리는 이벤트를 반환 합니다.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> hello 사용 해야 하는 범위 구문은 hello 콜론 (:) field: value 구분 기호 및 *하지* hello 등호 (=) 합니다. Hello 범위의 hello 아래쪽과 위쪽 끝 대괄호로 묶고 두 마침표 (.)로 구분 합니다.
>
>

## <a name="manipulate-search-results"></a>검색 결과 조작
데이터를 검색할 때 검색 쿼리 toorefine 원하는 고 hello 결과 대 한 제어를 어느 정도 합니다. 결과가 검색 되 면 명령을 tootransform를 적용할 수 있습니다 이러한.

로그 분석 검색에서 명령은 *해야* hello 세로줄 문자 (|) 뒤 합니다. 필터는 쿼리 문자열의 첫 번째 부분 hello 항상 있어야 합니다. 작업할 때 hello 데이터 집합을 정의 하 고 "파이프" 합니다 그 결과 명령입니다. Hello 파이프 tooadd 추가 명령을 사용할 수 있습니다. 이것은 느슨하게 비슷한 toohello Windows PowerShell 파이프라인입니다.

로그 분석 검색 언어 hello toofollow PowerShell 스타일 및 지침 toomake를 시도 하는 일반적으로 it 비슷한 toohello IT 전문가 및 tooease hello 배워야 할 필요성이 합니다.

명령은 동사의 이름이 있으므로 수행할 작업을 쉽게 알 수 있습니다.  

### <a name="sort"></a>정렬
hello 정렬 명령 toodefine hello를 하나 또는 여러 필드에서 순서를 정렬할 수 있습니다. 기본적으로 사용하지 않아도 시간 내림차순으로 정렬되도록 적용됩니다. hello 가장 최근의 결과가 검색 결과의 hello 위쪽에 항상 표시 됩니다. 즉, `Type=Event EventID=1234` 로 검색을 실행하면 실제로 실행되는 작업은 다음과 같습니다.

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Hello 유형의 로그를 잘 알고 있다면 경험을 이기 때문입니다. 예를 들어 Windows 이벤트 뷰어 안녕하세요에.

Toochange hello 방식으로 결과 반환 하는 정렬을 사용할 수 있습니다. hello 다음 예제에서는이 과정

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


hello 위의 간단한 예제 알려주는 명령이 작동 하는 방법을 hello 필터를 반환 하는 hello 결과의 hello 형태를 변경 합니다.

### <a name="limit-and-top"></a>제한 및 위쪽
덜 알려진 다른 명령에는 제한이 있습니다. 제한은 PowerShell같은 동사입니다. 제한은 TOP 명령과 기능적으로 동일한 toohello입니다. hello 쿼리인 hello 동일한 결과 반환 합니다.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>top를 사용 하 여 toosearch
* Hello 검색 쿼리 필드에 입력`Type=Event EventID=600 | Top 1`   
    ![상위 검색](./media/log-analytics-log-searches/oms-search-top.png)

위 hello 이미지에서 된 358 천 레코드가 EventID = 600입니다. 필드, 패싯 및 왼쪽 항상 반환 된 hello 결과 대 한 정보를 표시 하는 hello에 대 한 필터 hello *hello 필터 부분에 의해* 모든 파이프 문자 앞 hello 참가 하는 hello 쿼리 합니다. hello **결과** hello 예제 명령이 모양을 만들고 hello 결과 변환 하기 때문에 창 hello 가장 최근 1 개의 결과 반환 합니다.

### <a name="select"></a>여기서
hello SELECT 명령은 PowerShell에서 Select-object 처럼 동작 합니다. 자신의 원래 속성을 모두 갖지 않는 필터된 결과를 반환합니다. 대신 사용자가 지정한 hello 속성만 선택 합니다.

#### <a name="toorun-a-search-using-hello-select-command"></a>select 명령 hello를 사용 하 여 검색 한 toorun
1. 검색에서 `Type=Event` 을 입력하고 **검색**을 클릭합니다.
2. 클릭 **+ 자세히 표시** hello 결과 tooview 결과 hello 하는 모든 hello 속성 중 하나에 있습니다.
3. 그 중 일부를 명시적으로 및 선택 hello 쿼리 변경 내용을 너무`Type=Event | Select Computer,EventID,RenderedDescription`합니다.  
    ![선택 검색](./media/log-analytics-log-searches/oms-search-select.png)

이 명령은 toocontrol 검색 출력을 종종 hello 전체 레코드는 아닙니다 하 고 탐색을 위한 중요 데이터의 hello 부분만 선택 하는 경우에 특히 유용 합니다. 이 기능은 다른 유형의 레코드들이 *일부* 공통 속성이 있지만 *일부* 속성은 공통이 아닌 경우에도 유용합니다. 는 테이블 처럼 더 자연스럽 게는 출력을 생성 하거나 tooa CSV 파일을 내보낸 다음 Excel에서 massaged 되는 경우에 사용할 수 있습니다.

## <a name="use-hello-measure-command"></a>Hello 측정값 명령 사용
측정값은 hello 로그 분석 검색에서 가장 용도가 넓은 함수로 명령 중 하나입니다. 있습니다 tooapply 통계 *함수* tooyour 데이터 및 집계 결과 지정된 된 필드를 그룹화 합니다. 측정값이 지원하는 여러 통계 함수가 있습니다.

### <a name="measure-count"></a>개수() 측정
hello, 첫 번째 통계 함수로 toowork 및 가장 간단한 toounderstand hello 중 하나는 hello *count ()* 함수입니다.

와 같은 모든 검색 쿼리에서 나온 결과 `Type=Event`, hello 검색 결과의 왼쪽에 패싯이 라는 필터를 표시 합니다. hello 필터 실행 된 hello 검색에서 지정된 된 필드 hello 결과에 의해 값의 분포를 보여 줍니다.

![측정값 개수 검색](./media/log-analytics-log-searches/oms-search-measure-count01.png)

예를 들어 hello 이미지 위의 살펴보겠습니다 hello **컴퓨터** 필드가 hello 739 천 거의에서 이벤트 내 hello 결과 표시 68 고유한 특정 값에 대 한 hello **컴퓨터** 해당 레코드에서 필드입니다. hello 타일이 표시 hello hello 가장 일반적인 5 개의 값인 hello로 작성 된 상위 5 **컴퓨터** 필드), 해당 필드에 특정 값을 포함 하는 문서 hello 수로 정렬 합니다. Hello 이미지에는 –는 거의 369 천 이벤트 중 90 천 hello OpsInsights04.contoso.com 컴퓨터 83 천 hello DB03.contoso.com 컴퓨터에서에서 제공 하 고 볼 수 있습니다.

어떻게 할까요 toosee 모든 값 hello 타일 표시 하므로 hello 상위 5?

Hello 측정값 즉 명령을 hello count () 함수를 사용 하 여 수행할 수 있습니다. 이 함수는 매개 변수를 사용하지 않습니다. Hello 필드를 기준으로 – hello toogroup 사용할 지정 **컴퓨터** 이 경우 필드:

`Type=Event | Measure count() by Computer`

![측정값 개수 검색](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

하지만 **컴퓨터**는 각 데이터*에서* 사용되는 필드입니다. 관련된 관계 데이터베이스가 없고 별도의 **컴퓨터** 개체는 없습니다. 방금 값 hello *에* , 및 여러 다른 특성과 측면 hello 데이터를 생성 한 엔터티 데이터를 설명할 수 hello 따라서 hello 용어 *패싯*합니다. 그러나 다른 필드에 의해 그룹화할 수 있습니다. Hello hello 측정값 명령으로 파이프 하는 거의 739 천 이벤트의 원래 결과는 또한 라는 필드가 있기 때문에 **EventID**를 적용할 수 있습니다 하 여 해당 필드로 동일한 기술을 toogroup hello 하 고 EventID로 이벤트의 개수를 가져올:

```
Type=Event | Measure count() by EventID
```

경우 특정 값을 포함 하는 hello 실제 레코드 개수에 관심이 모르겠으면 되지만 대신의 목록을 원하는 경우 hello 값 자체를 추가할 수는 *선택* 선택 hello 첫 번째 열 및 hello 끝나기 전에 명령을:

```
Type=Event | Measure count() by EventID | Select EventID
```

더 복잡해 하 고 미리 hello 쿼리에서 hello 결과 정렬할 수 다음 또는 hello 표의 hello 열을 너무 클릭할 수 있습니다.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>측정값 개수를 사용 하 여 toosearch
* Hello 검색 쿼리 필드에 입력`Type=Event | Measure count() by EventID`
* 추가 `| Select EventID` hello 쿼리의 toohello 끝입니다.
* 마지막으로 추가 `| Sort EventID asc` hello 쿼리의 toohello 끝입니다.

몇 가지 중요 한 사항 toonotice 및 강조를 알아봅니다.

첫째, hello 결과가 표시 되지 않습니다 hello 원래 원시 결과가 더 이상. 대신 집계된 결과이며 기본적으로 그룹의 결과입니다. 이 문제가 아니지 하지만 hello 원래 원시 모양과 hello 집계/통계 함수의 결과로 서 hello 즉석에서 생성 되는 매우 다른 모양의 데이터를 상호 작용 하는 이해 해야 합니다.

두 번째, **개수 측정** 만 hello 상위 100 고유한 결과 현재 반환 합니다. 이 제한은 toohello 다른 통계 함수 적용 되지 않습니다. 따라서 일반적으로 해야 toouse 보다 정확 하 게 필터 첫 번째 toosearch 특정 항목에 대 한 측정값 개수 ()를 적용 하기 전에 합니다.

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Hello 측정값 명령으로 hello 최대 및 최소 함수 사용
**Measure Max()** 및 **Measure Min()**이 유용한 다양한 시나리오가 있습니다. 그러나 각 함수는 서로 반대이므로 최대()를 설명하고 최소()를 직접 시험해 보겠습니다.

보안 이벤트를 쿼리할 경우 **레벨** 속성이 있을 수 있습니다. 예:

```
Type=SecurityEvent
```

![측정값 개수 시작 검색](./media/log-analytics-log-searches/oms-search-measure-max01.png)

모든 hello 보안에 대해 tooview hello 가장 높은 값을 원하는 경우 사용할 수 이벤트 필드에 따라 hello 그룹, 공용 컴퓨터를 지정 합니다.

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![측정값 최대 컴퓨터 검색](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Hello 컴퓨터에 대 한 있음을 표시 합니다 **수준** 레코드, 그 중 대부분에는 적어도 수준 8, 수준 16의 많은 했습니다.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![최대 시간이 생성된 컴퓨터 검색](./media/log-analytics-log-searches/oms-search-measure-max03.png)

이 함수는 숫자와 잘 작동하지만 DateTime 필드와도 작동합니다. Hello에 대 한 유용한 toocheck를 마지막 또는 각 컴퓨터에 인덱싱된 데이터의 모든 부분에 대 한 가장 최근 타임 스탬프입니다. 예를 들어: hello 최신 보안 이벤트를 보고 한 때는 각 컴퓨터에 대 한?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Hello 측정값 명령으로 hello avg 함수 사용
그룹을 기준으로 결과 hello 동일 또는 다른 필드 및 측정값을 사용한 평균 () 통계 함수 hello 있습니다 toocalculate hello 일부 필드에 대 한 평균 값. 다양한 성능 데이터와 같은 경우에 유용합니다.

성능 데이터를 시작하겠습니다. OMS는 현재 Windows 및 Linux 컴퓨터 양쪽 모두에 대한 성능 카운터를 수집합니다.

에 대 한 toosearch *모든* 성능 데이터를 hello 가장 기본적인 쿼리는:

```
Type=Perf
```

![avg 시작 검색](./media/log-analytics-log-searches/oms-search-avg01.png)

hello 먼저 보면 점은 로그 분석에서는 설명 세 가지 관점: hello 차트; 뒤에 실제 레코드가 hello를 보여 주는 보여 주는 목록 성능 카운터 데이터;의 테이블 형식 뷰를 보여 주는 표 및 메트릭을 보여 주는 차트 hello에 대 한 성능 카운터입니다.

위 hello 이미지에서 hello 다음 나타내는 표시 된 필드의 두 집합이 있습니다.

* 첫 번째 집합 hello hello 쿼리 필터에서 Windows 성능 카운터 이름, 개체 이름 및 인스턴스 이름을 식별합니다. Hello 필드로 있습니다 것은 가장 일반적으로 사용할 패싯/필터
* **CounterValue** hello hello 카운터의 실제 값이 있습니다. 이 예제에서는 hello 값은 *75*합니다.
* **TimeGenerated**는 24시간 형식으로 12:51입니다.

다음은 그래프에서 hello 메트릭 보기입니다.

![avg 시작 검색](./media/log-analytics-log-searches/oms-search-avg02.png)

Hello Perf 레코드 도형에 대 한 읽기 및 다른 검색 방법에 대 한 읽은 후 측정값 평균 () tooaggregate이이 종류의 숫자 데이터를 사용할 수 있습니다.

간단한 예는 다음과 같습니다.

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![avg samplevalue 검색](./media/log-analytics-log-searches/oms-search-avg03.png)

이 예제에서는 hello CPU 총 시간 성능 카운터 및 컴퓨터별 평균을 선택합니다. Toonarrow 결과 tooonly hello 지난 6 시간 동안 다운 하려는 경우 hello 시간 필터 컨트롤을 사용 하거나 다음과 같이 쿼리에서 지정 합니다.

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>toosearch hello avg 함수를 사용 하 여 hello 측정값 명령 사용
* Hello 검색 쿼리 상자에 입력 `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`합니다.

컴퓨터 *간에* 데이터를 집계하고 상호 연결할 수 있습니다. 예를 들어, 다른 하나 종류의 일부는 같은 tooany 팜에서 호스트 집합이 있는지와 동일한 유형의 작업 및 부하를 대략적으로 분산 해야 하는 모든 hello를 방금 않으므로 한다고 가정 합니다. 다음 쿼리 평균을 hello 전체 팜에 대 한 hello로 이동 하는 하나에 모든 카운터를 가져올 수 있습니다. 다음 예제는 hello로 hello 컴퓨터를 선택 하 여 시작할 수 있습니다.

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Tooselect 2 개의 핵심 성과 지표 (Kpi)만 원하는 hello 컴퓨터를가지고: CPU 사용량 % 및 % 사용 가능한 디스크 공간입니다. 따라서 hello 쿼리 부분의 됩니다.:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

이제 다음 예제는 hello로 컴퓨터 및 카운터를 추가할 수 있습니다.

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

매우 구체적으로 선택 해야 하므로 hello **avg () 측정** 명령을 반환할 수 있습니다 hello 평균 컴퓨터가 아니라 hello 팜 전체에서 단순히 CounterName로 그룹화 하 여 합니다. 예:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

사용자 환경 KPI의 간단한 보기를 제공하므로 유용합니다.

![avg 그룹화 검색](./media/log-analytics-log-searches/oms-search-avg04.png)

대시보드에서 hello 검색 쿼리를 쉽게 사용할 수 있습니다. Hello 검색 쿼리를 저장 하 고 라는 여기에서 대시보드를 만들 수 예를 들어 *웹 팜 Kpi*합니다. 대시보드를 사용 하 여에 대 한 더 toolearn 참조 [로그 분석에 사용자 지정 대시보드를 만들](log-analytics-dashboards.md)합니다.

![avg 대시보드 검색](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Hello sum 함수를 사용 하 여 hello 측정값 명령 사용
hello sum 함수는 hello 측정값 명령의 유사한 tooother 기능입니다. Toouse에서 sum 함수 hello 하는 방법에 대 한 예제를 볼 수 [Microsoft Azure Operational Insights의 W3C IIS 로그 검색](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx)합니다.

숫자, 날짜 시간 및 텍스트 문자열이 포함된  Max() 및 Min()을 사용할 수 있습니다. 텍스트 문자열을 이용하여 사전순으로 정렬하고 처음 및 마지막을 가져옵니다.

그러나 숫자 필드가 아닌 어느 것도 합계()를 사용할 수 없습니다. 도 tooAvg() 적용 됩니다.

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Hello 백분위 수 함수 hello 측정값 명령 사용
숫자 필드에만 사용할 수 있다는 점에서 hello 백분위 수 함수는 유사한 tooAvg() 및 sum ()입니다. 숫자 필드에 1 too99 사이의 모든 백분위 수를 사용할 수 있습니다. **percentile** 및 **pct** 명령을 모두 사용할 수 있습니다. 다음은 몇 가지 예입니다.  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>명령을 경우 hello를 사용 합니다.
측정값 명령이 – hello 쿼리의 시작 부분에서 필터링 하는 것과 반대로 tooraw 결과로 생성 된 결과 집계 하는 hello 여기서 명령이 필터와 같이 작동 하지만 hello 파이프라인 toofurther 필터에 적용할 수 있습니다.

예:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

다른 파이프를 추가할 수 있습니다 "|" 문자 및 hello 명령 tooonly 구할 컴퓨터와 이상 80% 평균 CPU가 다음 예제에서는 hello:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Microsoft System Center-Operations Manager에 잘 알고 있는 관리 팩 측면에서 명령을의 hello 생각할 수 있습니다. Hello 예제가 규칙 인 경우 hello 첫번째 hello 쿼리의 부분이 hello 데이터 원본과 hello 명령 hello conditiondetection 수 없는 합니다.

타일로 hello 쿼리를 사용 하 여 **내 대시보드**, 일종의 모니터로 toosee 때 컴퓨터 Cpu 초과 사용 됩니다. 대시보드에 대 한 자세한 정보는 toolearn 참조 [로그 분석에 사용자 지정 대시보드를 만들](log-analytics-dashboards.md)합니다. 만들고 및 hello 모바일 앱을 사용 하 여 대시보드를 사용 하 여 수도 있습니다. 자세한 내용은 [OMS Mobile App](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)(OMS 모바일 앱)을 참조하세요. 다음 이미지는 hello의 hello 아래쪽 두 타일을 볼 수 있습니다 목록을 표시 한 hello 모니터를 숫자로 합니다. 기본적으로, 항상 hello 숫자 toobe 0을 빈 목록 toobe hello 합니다. 그렇지 않은 경우 경고 조건을 나타냅니다. 필요한 경우 컴퓨터를 살펴보면 압력을 받고 있기 tootake를 사용할 수 있습니다.

![모바일 대시보드](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Hello를 사용 하 여 in 연산자
hello *IN* 연산자와 함께 *NOT IN* 는 다른 검색을 인수로 포함 하는 검색 toouse 하위 있습니다. 이러한 연산자는 다른 *기본* 또는 *외부* 검색 내 중괄호 {} 안에 포함됩니다. hello 결과 대체로, 고유한 결과 목록이 며 기본 검색에서 인수로 사용 됩니다.

검색에서 생성할 수 있는 하지만 검색 식에서 직접 설명할 수 없는 데이터의 하위 toomatch 하위 집합을 사용할 수 있습니다. 예를 들어 하나의 검색 toofind 모든 이벤트를 사용 하 여 관심이 있는 경우 *보안 업데이트가 누락 된 컴퓨터*, toodesign를 먼저 식별 하는 대체로 며 필요 *보안 업데이트가 누락 된 컴퓨터*  속하는 toothose 호스트 이벤트를 찾기 전에 합니다.

따라서 표현할 수 있습니다 *필수 보안 업데이트가 누락 된 현재 컴퓨터* 다음 쿼리에서 hello로:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Hello 목록을 만든 후에 한 해당 컴퓨터에 대 한 이벤트를 찾는 외부 (기본) 검색을 내부 검색 toofeed hello 컴퓨터의 목록으로 hello 검색을 사용할 수 있습니다. Hello 내부 검색을 중괄호로 묶고 IN 연산자 hello를 사용 하 여 hello 외부 검색에서 필터/필드에 대 한 가능한 값으로 해당 결과 제공 하 여이 작업을 수행 합니다. hello 쿼리는 다음과 같습니다.

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in02-revised.png)

또한 공지 hello 시간 때문에 hello 내부 검색에 사용 된 필터 hello 시스템 업데이트 평가 24 시간 마다 모든 컴퓨터의 스냅숏을 만들기를 사용 합니다. 하루에만 검색 하 여 더 간단 하 고 정확한 hello 내부 쿼리를 만들 수 있습니다. hello 외부 검색 대신 사용 하 여 hello 시간 선택을 hello 사용자 인터페이스에서 지난 7 일 동안 hello에서 이벤트를 검색 합니다. time 연산자에 대한 자세한 내용은 [부울 연산자](#boolean-operators) 참조하세요.

때문에 사용자에 대 한 필터 값으로 hello 내부 검색만 실제로 사용 하 여 hello 결과 hello 외부, hello 외부 검색에 명령을 적용할 수 있습니다. 예를 들어 계속 수 이벤트를 다른 measure 명령으로 위에 그룹 hello:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN 검색 예제](./media/log-analytics-log-searches/oms-search-in03-revised.png)

일반적으로 원하는 내부 쿼리 tooexecute 신속 하 게 및 또한 tooreturn 적은 양의 결과 대 한 로그 분석에는 서비스 쪽 시간 제한이 때문입니다. Hello 내부 쿼리가 더 많은 결과 반환 하는 경우 hello 결과 목록이 잘리기 있는 발생 시키는 외부 검색 tooreturn hello 잘못 된 결과가 있습니다.

다른 규칙은 해당 hello 내부 검색에는 현재 tooprovide 필요한 *집계* 결과입니다. 즉, *measure* 명령을 포함해야 합니다. 현재는 외부 검색에 원시 결과를 제공할 수 없습니다.

또한 IN 연산자를 하나만 있을 수 있으며 hello hello 쿼리의 마지막 필터 여야 합니다. 또는 여러 명의 IN 연산자 수 없습니다.-이 기본적으로 실행할 수 없으며 여러 하위 검색: 각 외부 검색에 대 한 중요 한 점은 하나의 하위/내부 검색만 hello 불가능 합니다.

이러한 제한은 IN 통해 많은 종류의 상관 관계 검색이 가능 및 toodefine 사용 하면 다음과 유사한 toogroups 컴퓨터, 사용자 또는 파일 – 등 어떤 hello 필드 데이터에 포함 합니다. 다음은 추가적인 예입니다.

**자동 업데이트 설정이 비활성화된 컴퓨터에 누락된 모든 업데이트**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**SQL Server(=SQL 평가가 실행된)를 실행하는 컴퓨터의 모든 오류 이벤트**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**도메인 컨트롤러(=AD 평가가 실행된)인 컴퓨터의 모든 보안 이벤트**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**다른 계정 toohello 로그온 되어 있는 동일한 컴퓨터 BACONLAND\jochan 계정이 로그온가?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Hello distinct 명령 사용
Hello 이름에서 알 수 있듯이이 명령은 필드의 고유 값 목록을 제공 합니다. 매우 간단하지만 유용합니다. 동일한 결과 얻을 수도 measure count () 명령을 사용도 아래와 같이 hello 합니다.

```
Type=Event | Measure count() by Computer
```

![DISTINCT 검색 명령 예제](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

그러나에 관심이 모든 고유 값 및 해당 값이 있는 문서 hello 수가 아니라 목록만 이면 다음 DISTINCT 및 제공할 수를 출력 하는 쉽고 명확한 tooread 간단한 구문을 아래와 같이.

```
Type=Event | Distinct Computer
```
![DISTINCT 검색 명령 예제](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Hello countdistinct 함수 hello 측정값 명령 사용
countdistinct 함수 hello hello 각 그룹 내에서 고유 값 수를 계산합니다. 예를 들어, 될 수 toocount hello 수가 고유 컴퓨터 각 형식에 대 한 보고를 사용 합니다.

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Hello 측정 간격 명령을 사용 하 여
실시간에 가까운 성능 데이터 수집을 통해, Log Analytics의 모든 성능 카운터를 수집하고 시각화할 수 있습니다. 단순히 입력 hello 쿼리 **유형: 성능** 메트릭 그래프 카운터 및 로그 분석 환경에서 서버 hello 수에 따라 수천을 반환 합니다. Hello를 살펴볼 수 주문형 메트릭 집계로 높은 수준과 심층 탐구는 데 필요한 만큼 더 세분화 된 데이터에서 사용자 환경에서 전반적인 메트릭.

원하는 tooknow hello 평균 CPU 모든 컴퓨터에서 이란 경우를 가정해 봅니다. 모든 컴퓨터에 대 한 평균 CPU hello 살펴보면 아닐 수 있습니다 유용 하므로 결과 매끄럽게 얻을 수 있습니다. 더 세부적으로 toolook를 집계할 수 있습니다 결과 창이 청크를 더 작은 시간과 모양에 시계열에 다른 차원에서. 예를 들어 다음과 같은 모든 컴퓨터에서 CPU 사용량의 hello 시간별 평균을 수행할 수 있습니다.

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![평균 간격 측정](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

기본적으로, 이러한 결과는 다중 계열 대화형 꺾은선형 차트에 표시됩니다.  이 차트는 계열 전환(y 축 재조정 포함), 확대/축소 및 가리킴을 지원합니다.  hello 테이블 표시 옵션은 필요한 경우 hello 원시 데이터를 보기 위해 계속 사용할 수 있습니다.

다른 필드를 기준으로 그룹화가 가능합니다. 이 예제에서는 하나의 특정 컴퓨터에 대 한 모든 hello % 카운터 보고 하 고 모든 카운터의 시간별 70 백분위 수 hello 란 tooknow 원하는:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
한 가지 toonote은 이러한 쿼리 제한 tooperformance 카운터 되지 않는다는 것입니다. tooany 메트릭을 적용할 수 있습니다. 이 예제에서, W3C IIS 로그를 보고 있습니다. 각 요청을 처리 하기 위해 5 분 간격에 대해 걸리는 hello 최대 시간 이란 tooknow 합니다.

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>한 쿼리에 여러 집계 사용
measure 명령에 집계 절을 여러 개 지정할 수 있습니다.  각 절에는 개별적으로 별칭을 지정할 수 있습니다.  필드 이름이 사용 된 집계 함수를 hello 됩니다 별칭 hello 결과 부여 되지 않은 경우 (즉, "avg(CounterValue)" avg(CounterValue))에 대 한 합니다.

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

다른 예제입니다.

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>다음 단계
로그 검색에 대한 자세한 내용은 다음을 참조하십시오.

* 사용 하 여 [로그 분석의 사용자 지정 필드](log-analytics-custom-fields.md) tooextend 로그 검색 합니다.
* 검토 hello [로그 분석 로그 검색 참조](log-analytics-search-reference.md) tooview hello의 모든 필드 및 패싯 로그 분석에서 사용할 수를 검색 합니다.
