---
title: "aaaAzure 로그 분석 검색 참조 | Microsoft Docs"
description: "로그 분석 검색 참조 hello hello 검색 언어에 설명 하 고 데이터 검색 및 필터링 식을 toohelp 검색 범위 좁히기 때 사용할 수 있는 hello 일반 쿼리 구문 옵션을 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Log Analytics 검색 참조

>[!NOTE]
> 이 문서에서는 로그 분석에 hello 현재 쿼리 언어를 사용 하 여 로그 검색을 설명 합니다.  작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 너무 참조 해야 하는 다음[hello 새 언어에 대 한 언어 참조 hello](https://go.microsoft.com/fwlink/?linkid=856079)합니다.

hello 검색 언어에 대 한 참조 섹션에 설명 hello 일반 쿼리 구문 옵션 데이터 검색 및 필터링 식을 toohelp 검색 범위 좁히기 때 사용할 수 있습니다. 검색 된 hello 데이터에서 tootake 동작을 사용할 수 있는 명령을 설명 합니다.

검색을 반환 하는 hello 필드에 대 한 읽을 수 있으며 hello 패싯 데 도움이 되는 검색 데이터의 hello와 유사한 범주에 대 한 자세한 [검색 필드 및 패싯 참조 섹션](#search-field-and-facet-reference)합니다.

## <a name="general-query-syntax"></a>일반 쿼리 구문
hello 일반 쿼리 하기 위한 구문은 다음과 같습니다.

```
filterExpression | command1 | command2 …
```

필터 식 hello (`filterExpression`) hello에 대 한 "where" 조건을 hello 쿼리를 정의 합니다. hello 명령은 hello 쿼리에 의해 반환 된 toohello 결과 적용 합니다. 여러 개의 명령은 hello 세로줄 문자 (|)로 구분 되어야 합니다.

### <a name="general-syntax-examples"></a>일반 구문 예제
예제:

```
system
```

이 쿼리는 hello 단어를 포함 하는 결과 반환 *시스템* 검색 용어 또는 전체 텍스트 인덱싱된 모든 필드에서 합니다.

> [!NOTE]
> 모든 필드가 이러한 방식으로 인덱싱되지 않는 hello 가장 일반적인 텍스트 필드 (예: 설명 및 이름) 일반적으로.
>
>

```
system error
```

이 쿼리는 hello 단어를 포함 하는 결과 반환 *시스템* 및 *오류*합니다.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

이 쿼리는 hello 단어를 포함 하는 결과 반환 *시스템* 및 *오류*합니다. 다음 hello 하 여 hello 결과 정렬 *ManagementGroupName* 필드 (오름차순), 한 다음 hello *TimeGenerated* (내림차순) 필드입니다. 처음 10 개 결과가 hello이 필요합니다.

> [!IMPORTANT]
> 모든 hello 필드 이름 및 hello 문자열 및 텍스트 필드에 대 한 hello 값은 대/소문자 구분 합니다.
>
>

## <a name="filter-expressions"></a>필터 식
다음 하위 섹션으로 구성 하는 hello에 hello 필터 식을 설명 합니다.

### <a name="string-literals"></a>문자열 리터럴
문자열 리터럴을 키워드 또는 미리 정의 된 데이터 형식 (예를 들어 숫자 또는 날짜)으로 hello 파서에서 인식 되지 않는 모든 문자열.

예제:

```
These all are string literals
```

이 쿼리는 발생하는 5개 단어를 모두 포함하는 결과를 검색합니다. 복잡 한 문자열 검색 tooperform hello 문자열을 리터럴을 큰따옴표로 묶습니다. 예:

```
"Windows Server"
```

*Windows Server*와 정확히 일치하는 결과를 반환합니다.

### <a name="numbers"></a>숫자
hello 파서는 숫자 필드에 대 한 hello 10 진수 정수 및 부동 소수점 수 구문을 지원합니다.

예제:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>날짜 및 시간
Hello 시스템 데이터의 모든 부분을 *TimeGenerated* hello 원래 날짜 및 hello 레코드의 시간을 나타내는 속성입니다. 또한 일부 데이터 형식에 더 많은 날짜 및 시간 필드가 있을 수 있습니다(예를 들어 *LastModified*).

타임 라인 hello **차트/시간** Azure 로그 분석에 선택 기가 (따라 toohello 현재 실행 중인 쿼리에) 시간에 따른 결과의 분포를 보여 줍니다. 이 hello 기반 *TimeGenerated* 필드입니다. 날짜 및 시간 필드는 쿼리 toorestrict hello 쿼리 tooa 특정 시간 내에 사용할 수 있는 특정 문자열 형식이 있습니다. 구문 toorefer toorelative 사이의 시간 간격 (예를 들어 "3 일 전 및 2 시간 전")를 사용할 수 있습니다.

hello 다음은 날짜 및 시간에 유효한 형식의 구문입니다.

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


예:

```
TimeGenerated:2013-10-01T12:20
```

hello 이전 명령에는 레코드를 반환는 *TimeGenerated* 2013 년 10 월 1 일 12 시 20 정확히의 값입니다.

hello 파서도 지원 hello mnemonic 날짜/시간 값을 합니다. (그럴 가능성은 모든 결과 생성할 데이터 hello 빠른 시스템을 통해 변경할 하지 않습니다.)

다음이 예제는 상대 및 절대 날짜에 대 한 빌딩 블록 toouse 됩니다. Hello 다음 세 하위 섹션에서 어떻게 toouse에 더 높은 수준의 표시 상대 날짜 범위를 사용 하는 예제 필터입니다.

### <a name="datetime-math"></a>날짜/시간 수학
날짜/시간 수학 연산자 toooffset hello를 사용 하 여 또는 간단한 날짜/시간 계산을 사용 하 여 hello 날짜/시간 값을 반올림 합니다.

구문

```
datetime/unit
```

```
datetime[+|-]count unit
```

| 연산자 | 설명 |
| --- | --- |
| / |날짜/시간 toohello 라운드 단위를 지정 합니다. 예를 들어 지금 / 일 hello의 현재 날짜/시간 toomidnight hello를 현재 날짜로 반올림 합니다. |
| + 또는- |날짜/시간 오프셋 hello 단위 수를 지정 합니다. 예를 들어 지금 + 1 시간은 오프셋 hello 현재 날짜/시간을 한 시간 빠르게 합니다. 2013-10-01t12: 00-10DAYS hello 날짜 값을 10 일 전으로 오프셋 합니다. |

Hello 날짜/시간 수치 연산자를 함께 연결할 수 있습니다. 예:

```
NOW+1HOUR-10MONTHS/MINUTE
```

hello 다음 표 hello 지원 되는 날짜/시간 단위입니다.

| 날짜/시간 단위 | 설명 |
| --- | --- |
| YEAR, YEARS |라운드 toocurrent 연도 또는 hello에서 오프셋 년 수를 지정 합니다. |
| MONTH, MONTHS |라운드 toocurrent 월 또는 hello 여 오프셋 개월 수를 지정 합니다. |
| DAY, DAYS, DATE |라운드 toocurrent 날짜 hello 월 또는 hello 여 오프셋 일 수를 지정 합니다. |
| HOUR, HOURS |라운드 toocurrent 시간 또는 오프셋 hello 하 여 지정 된 시간 수입니다. |
| MINUTE, MINUTES |라운드 toocurrent 분 또는 hello 여 오프셋 시간 (분)을 지정 합니다. |
| SECOND, SECONDS |둘째, toocurrent를 반올림 하거나 지정 된 hello 만큼 오프셋 시간 (초)입니다. |
| MILLISECOND, MILLISECONDS, MILLI, MILLIS |라운드 toocurrent 밀리초 또는 hello 여 오프셋 시간 (밀리초)을 지정 합니다. |

### <a name="field-facets"></a>필드 패싯
패싯 필드를 사용 하 여 특정 필드 및 정확한 값에 대 한 hello 검색 조건을 지정할 수 있습니다. 이와 달리에서 hello 인덱스 전체에서 다양 한 용어에 "자유 텍스트" 쿼리를 작성 합니다. 여러 개의 이전 예에서 이 기법을 이미 보았습니다. hello 다음은 더 복잡 한 예입니다.

**구문**

```
field:value
```

```
field=value
```

**설명**

검색 hello hello 특정 값에 대 한 필드입니다. 문자열 리터럴, 숫자 또는 날짜와 시간 hello 값일 수 있습니다.

예:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**구문**

*field>value*

*field<value*

*field>=value*

*field<=value*

*field!=value*

**설명**

비교를 제공합니다.

예:

```
TimeGenerated>NOW+2HOURS
```

**구문**

```
field:[from..to]
```

**설명**

패싯 범위를 제공합니다.

예:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
hello **IN** tooselect 값 목록에서 키워드를 사용 합니다. 사용 하는 hello 구문에 따라이 사용자가 제공한 값의 단순 목록 또는 집계에서 값의 목록 수 있습니다.

구문 1:

```
field IN {value1,value2,value3,...}
```

이 구문은 tooinclude를 간단한 목록 값이 모두 있습니다.



예제:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

구문 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

이 구문은 집계 toocreate가 있습니다. 그런 다음 해당 값이 있는 이벤트를 찾는 다른 외부 (기본) 검색에 해당 집계의 hello 값 목록이 제공할 수 있습니다. 이렇게 하려면 hello 내부 검색을 중괄호로 묶고 hello IN 연산자를 사용 하 여 hello 외부 검색에서 필드에 대 한 가능한 값으로 해당 결과 제공 합니다.

내부 쿼리 예: *현재 보안 업데이트가 누락 된 컴퓨터* 다음 집계 쿼리 hello로:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

hello 찾는 최종 쿼리 *현재 보안 업데이트가 누락 된 컴퓨터에 대 한 모든 Windows 이벤트* hello 다음 예제와 유사 합니다.

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>포함
hello **Contains** toofilter 지정한 문자열을 포함 하는 필드와 레코드에 대 한 키워드를 사용 합니다. 이는 대/소문자를 구분하고 문자열 필드에 대해서만 작동하며 이스케이프 문자를 포함하지 않을 수 있습니다.

구문

```
field:contains("string")
```

예제:

```
Type:contains("Event")
```

"이벤트" hello 문자열을 포함 하는 형식 가진 레코드를 반환 합니다. 예를 들어 **이벤트**, **SecurityEvent** 및 **ServiceFabricOperationEvent**를 포함합니다.



### <a name="regular-expressions"></a>정규식
Hello를 사용 하 여 정규식을 필드에 대 한 검색 조건을 지정할 수 있습니다 **Regex** 키워드입니다. 정규식에는 데 사용할 수는 hello 구문 설명과 참조 [로그 분석에서 정규식 toofilter 로그 검색을 사용 하 여](log-analytics-log-searches-regex.md)합니다.

구문

```
field:Regex("Regular Expression")
```

예제:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>논리 연산자
hello 쿼리 언어 지원 hello 논리 연산자 (*AND*, *또는*, 및 *하지*) 및 해당 C 스타일 별칭 (*&&*,  *||* , 및 *!*각각). 괄호 toogroup 이러한 연산자를 사용할 수 있습니다.

예제:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

Hello hello 최상위 필터 인수에 대 한 논리 연산자를 생략할 수 있습니다. 이 경우 hello AND 연산자를 가정 합니다.

| 필터 식 | 해당 하는 너무|
| --- | --- |
| 시스템 오류 |시스템 AND 오류 |
| 시스템 "Windows Server" OR 심각도:1 |시스템 AND ("Windows Server" OR 심각도:1) |

### <a name="wildcarding"></a>와일드 카드 사용
hello 쿼리 언어를 지 원하는 hello를 사용 하 여 ( \* ) 문자 너무 쿼리에서 값에 대 한 하나 이상의 문자를 나타냅니다.

예제:

 과 같이"Redmond" hello 이름에 "SQL"로 모든 컴퓨터를 찾습니다.

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> 현재 와일드 카드는 따옴표 안에서 사용할 수 없습니다. 예를 들어 hello 메시지 `"*This text*"` hello 간주 (\*) 리터럴로 사용할 (\*) 문자.


## <a name="commands"></a>명령


hello 명령은 hello 쿼리에 의해 반환 되는 toohello 결과 적용 합니다. 사용 하 여 hello 파이프 문자 (|) tooapply 명령 toohello 결과 검색 합니다. 여러 개의 명령은 hello 파이프 문자로 구분 되어야 합니다.

> [!NOTE]
> 명령 이름은 대문자 또는 소문자 hello 필드 이름 및 hello 데이터와 달리 작성할 수 있습니다.
>
>

### <a name="sort"></a>정렬
구문

    sort field1 asc|desc, field2 asc|desc, …

특정 필드에 hello 결과 정렬합니다. hello asc/desc 접미사 toosort hello 결과를 오름차순 또는 내림차순 선택 사항입니다. 생략 하는 hello *asc* 정렬 순서를 가정 합니다. Hello에 대 한 **TimeGenerated** 필드 *desc* 기본적으로 먼저 hello 가장 최근의 결과 반환 하므로 정렬 순서를 가정 합니다.

### <a name="toplimit"></a>위쪽/제한
구문

    top number


    limit number
제한 hello 응답 toohello 상위 n 개 결과입니다.

예제:

    Type:Alert errors detected | top 10

반환 결과 일치 하는 상위 10을 hello 합니다.

### <a name="skip"></a>Skip
구문

    skip number

건너뜁니다 hello 나열 된 결과의 수입니다.

예제:

    Type:Alert errors detected | top 10 | skip 200

200개 결과에서 시작하여 상위 10개의 일치하는 결과를 반환합니다.

### <a name="select"></a>여기서
구문

    select field1, field2, ...

선택한 결과 toohello 필드를 제한 합니다.

예제:

    Type:Alert errors detected | select Name, Severity

반환 된 결과 필드를 너무 hello 제한*이름* 및 *심각도*합니다.

### <a name="measure"></a>측정값
hello *측정값* 명령에 사용 되는 tooapply 통계 함수 toohello 원시 검색 결과입니다. 이 매우 유용한 tooget *group by* hello 데이터 보기입니다. Hello 측정값 명령을 사용 하면 로그 분석 검색 집계 된 결과가 포함 된 테이블을 표시 합니다.

**구문:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



집계 hello *groupField*를 사용 하 여 hello 집계 측정값을 계산 하 고 *aggregatedField*합니다.

| 측정 통계 함수 | 설명 |
| --- | --- |
| *aggregateFunction* |hello 이름 (대/소문자 구분) hello 집계 함수입니다. 집계 함수를 수행 하는 hello는 지원: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, 백분위 수 # # 또는 PCT # # (# #은 1과 99 사이의 임의의 숫자)입니다. |
| *aggregatedField* |집계 중인 hello 필드입니다. 이 필드는 COUNT 집계 함수 hello에 대 한 선택 사항 이지만 toobe 기존 숫자 필드는 SUM, MAX, MIN, AVG, STDDEV, 백분위 수 # # 또는 PCT # #에 대 한 (# #은 1과 99 사이의 임의의 숫자)입니다. hello aggregatedField도 중 하나일 수 있습니다 hello **확장** 함수를 지원 합니다. |
| *fieldAlias* |hello에 대 한 별칭 (선택 사항)는 hello 집계 값을 계산합니다. 지정 하지 않으면 hello 필드 이름이 **AggregatedValue**합니다. |
| *groupField* |hello 결과 집합는 hello 필드의 hello 이름으로 그룹화 됩니다. |
| *간격* |hello 형식에서 hello 시간 간격:**nnnNAME**합니다. **nnn**hello 양의 정수 번호가입니다. **이름** hello 간격 이름입니다. 지원되는 간격 이름은 대/소문자를 구분하며 MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S] 및 YEAR[S]를 포함합니다. |

hello 간격 옵션 날짜/시간 그룹 필드 에서만 사용할 수 있습니다 (예: *TimeGenerated* 및 *TimeCreated*). 현재, hello 서비스에 의해 적용 되지 않지만 toohello 백 엔드로 전달 되는 날짜/시간 없는 필드에 런타임 오류가 발생 합니다. Hello 스키마 유효성 검사를 구현 하는 경우 hello 서비스 API는 집계 간격에 대해 날짜/시간 없는 필드를 사용 하는 쿼리를 거부 합니다. 현재 hello *측정값* 구현은 임의의 집계 함수에 대 한 간격 그룹화를 지원 합니다.

Hello BY 절을 생략 하지만 간격을 지정 하 여 (두 번째 구문 처럼), hello *TimeGenerated* 기본적으로 필드를 가정 합니다.

예제:

**예 1**

    Type:Alert | measure count() as Count by ObjectId

그룹에서 경고 hello *ObjectID*, hello 각 그룹에 대 한 경고 수를 계산 하 고 있습니다. hello 집계 된 값으로 반환 됩니다 hello *Count* 필드 (별칭).

**예 2**

    Type:Alert | measure count() interval 1HOUR

그룹 1 시간 간격으로 경고 hello를 사용 하 여 hello *TimeGenerated* 필드 및 각 간격의 경고 hello 수를 반환 합니다.

**예 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Hello 이전 예제와 동일 하지만 집계 된 필드 별칭 (*AlertsPerHour*).

**예제 4**

    * | measure count() by TimeCreated interval 5DAYS

Hello를 사용 하 여 5 일 간격으로 hello 결과 그룹화 *TimeCreated* 필드 및 각 간격의 결과의 hello 수를 반환 합니다.

**예제 5**

    Type:Alert | measure max(Severity) by WorkflowName

그룹 워크 로드 이름 별로 경고를 hello 및 반환 hello 각 워크플로에 대 한 최대 경고 심각도 값입니다.

**예제 6**

    Type:Alert | measure min(Severity) by WorkflowName

Hello 이전 예제와 동일 하지만 hello로 *min* 집계 함수입니다.

**예제 7**

    Type:Perf | measure avg(CounterValue) by Computer

Perf 컴퓨터 별로 그룹화 하 고 hello 평균 (평균)을 계산 합니다.

**예제 8**

    Type:Perf | measure sum(CounterValue) by Computer

Hello 이전 예제와 동일 하지만 사용 *sum*합니다.

**예제 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Hello 이전 예제와 동일 하지만 사용 *stddev*합니다.

**예제 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Hello 이전 예제와 동일 하지만 사용 *percentile70*합니다.

**예제 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Hello 이전 예제와 동일 하지만 사용 *pct70*합니다. *PCT##*은 *PERCENTILE##* 함수의 유일한 별칭입니다.

**예제 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

컴퓨터에서 성능 먼저 그룹화 하 고 다음 CounterName 및 hello 평균 (평균)을 계산 합니다.

**예제 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Hello hello 최대 경고 수와 상위 5 개 워크플로 가져옵니다.

**예제 14**

    * | measure countdistinct(Computer) by Type

Hello 각 형식에 대해 보고 하는 고유 컴퓨터 수를 계산 합니다.

**예제 15**

    * | measure countdistinct(Computer) Interval 1HOUR

Hello 매시간에 대 한 보고 하는 고유 컴퓨터 수를 계산 합니다.

**예제 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

% Processor Time 컴퓨터 별로 그룹화 하 고 1 시간 마다 hello 평균을 반환 합니다.

**예제 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

W3CIISLog 방법으로 그룹화 하 고 5 분 마다에 대 한 hello를 최대 반환 합니다.

**예제 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

컴퓨터 및 반환 hello, 평균, 75th 백분위 수를 최대값과 최소값에 1 시간 마다 하 여 그룹 % 프로세서 시간입니다.

**예제 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

그룹 % Processor Time 먼저 컴퓨터와 인스턴스 이름 및 평균을 반환 hello 최소 75 번째 백분위 수, 및 최대 1 시간 마다.

**예제 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

컴퓨터에 모든 디스크에 대 한 분당 디스크 쓰기 hello 최대값을 계산합니다.

### <a name="where"></a>Where
구문

```
**where** AggregatedValue>20
```

뒤에 사용할 수는 *측정값* 명령 toofurther 필터 hello 집계 결과 hello *측정값* 집계 함수가 만든 합니다.

예제:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Dedup
구문

    Dedup FieldName

Hello 필드의 모든 고 윳 값에 대 한 hello 첫 번째 문서를 반환 합니다.

예제:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

이 예에서는 EventID 당 하나의 이벤트 (hello 최신 이벤트)를 반환 합니다.

### <a name="join"></a>Join
조인 결과를 두 개의 쿼리는 단일 tooform hello 결과 집합입니다.  테이블에 따라 hello에 설명 된 여러 개의 조인 유형을 지원 합니다.

| 조인 유형 | 설명 |
|:--|:--|
| inner | 두 쿼리 모두 일치하는 값을 가진 레코드만 반환합니다. |
| outer | 두 쿼리 모두에서 모든 레코드를 반환합니다.  |
| left  | 왼쪽 쿼리의 모든 레코드와 오른쪽 쿼리에서 일치하는 레코드를 반환합니다. |


- 조인 hello를 포함 하는 쿼리를 현재 지원 하지 않는 **IN** 키워드, hello **측정값** 명령 또는 hello **확장** hello 오른쪽 쿼리에서 필드 대상으로 하는 경우 명령입니다.
- 현재는 조인에 단일 필드만 포함할 수 있습니다.
- 단일 검색에서 둘 이상의 조인이 포함되지 않을 수 있습니다.

**구문**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**예**

tooillustrate hello 다른 조인 유형, 각 컴퓨터에 대 한 MyBackup_CL hello 하트 비트를 사용 하 여 호출 하는 사용자 지정 로그에서 수집 된 데이터 형식에 가입 것이 좋습니다.  이러한 데이터 형식이 같은 데이터가 hello가 있어야 합니다.

`Type = MyBackup_CL`

| TimeGenerated | 컴퓨터 | LastBackupStatus |
|:---|:---|:---|
| 4/20/2017 01:26:32.137 AM | srv01.contoso.com | 성공 |
| 4/20/2017 02:13:12.381 AM | srv02.contoso.com | 성공 |
| 4/20/2017 02:13:12.381 AM | srv03.contoso.com | 실패 |

`Type = Hearbeat`(표시된 필드의 하위 집합만)

| TimeGenerated | 컴퓨터 | ComputerIP |
|:---|:---|:---|
| 4/21/2017 12:01:34.482 PM | srv01.contoso.com | 10.10.100.1 |
| 4/21/2017 12:02:21.916 PM | srv02.contoso.com | 10.10.100.2 |
| 4/21/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>내부 조인

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

두 데이터 형식에 대 한 hello 컴퓨터 필드와 일치 하는 레코드를 따라 hello를 반환 합니다.

| 컴퓨터| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | 성공 | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | 성공 | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |


#### <a name="outer-join"></a>외부 조인

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Hello 두 데이터 형식에 대 한 레코드를 반환 합니다.

| 컴퓨터| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | 성공  | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:14:12.381 AM | 성공  | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 01:33:35.974 AM | 실패  | 4/21/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 4/21/2017 12:01:47.373 PM | 10.10.100.2 | Heartbeat |



#### <a name="left-join"></a>왼쪽 조인

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Hello 하트 비트에서 일치 하는 모든 필드와 레코드 MyBackup_CL에서 다음을 반환 합니다.

| 컴퓨터| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | 성공 | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | 성공 | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 02:13:12.381 AM | 실패 | | | |


### <a name="extend"></a>Extend
쿼리에서 런타임 필드를 toocreate 있습니다. 참고 hello 측정값 명령 tooperform 집계 된 런타임 필드를 사용할 수 없습니다.

**예 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
SQL 평가 권장 사항에 대해 가중 평균 권장 점수를 표시합니다.

**예 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
바이트가 아닌 KB 단위로 카운터 값을 표시합니다.

**예 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
눈금이 0에서 100 사이의 모든 결과 되도록 WireData TotalBytes의 값을 hello 합니다.

**예제 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
50% 미만인 성능 카운터 값을 LOW로 태깅하고 나머지는 HIGH로 태깅합니다.

**예제 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
컴퓨터에 모든 디스크에 대 한 분당 디스크 쓰기 hello 최대값을 계산합니다.

**지원되는 함수**

| 함수 | 설명 | 구문 예제 |
| --- | --- | --- |
| abs |Hello의 hello 절대 값을 반환 값 또는 함수를 지정 합니다. |`abs(x)` <br> `abs(-5)` |
| acos |값 또는 함수의 아크코사인을 반환합니다. |`acos(x)` |
| and |모든 피연산자 tootrue를 평가 하는 경우에 true 값을 반환 합니다. |`and(not(exists(popularity)),exists(price))` |
| asin |값 또는 함수의 아크사인을 반환합니다. |`asin(x)` |
| atan |값 또는 함수의 아크탄젠트를 반환합니다. |`atan(x)` |
| atan2 |x, y toopolar 좌표 hello 사각형 좌표로의 hello 변환으로 인해 발생 하는 hello 각도 반환 합니다. |`atan2(x,y)` |
| cbrt |세제곱근입니다. |`cbrt(x)` |
| ceil |Tooan 정수를 반올림 합니다. |`ceil(x)`  <br> `ceil(5.6)` 6을 반환합니다. |
| cos |각도의 코사인을 반환합니다. |`cos(x)` |
| cosh |쌍곡선 코사인을 반환합니다. |`cosh(x)` |
| def |기본값에 대한 약어입니다. 반환 hello 필드 "field"의 값입니다. Hello 필드가 없는 경우 지정 된 hello 기본값을 반환 하 고 hello 첫 번째 값이 생성 위치: `exists()==true`합니다. |`def(rating,5)` 이 def() 함수 hello 등급을 반환 하거나 등급이 지정 되지 않은 hello 문서에 지정 된 경우 5를 반환 합니다. <br> `def(myfield, 1.0)`너무`if(exists(myfield),myfield,1.0)`합니다. |
| deg |Toodegrees 라디안으로 변환합니다. |`deg(x)` |
| div |`div(x,y)` 는 x를 y로 나눕니다. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dist |두 벡터 사이의 (포인트) n 차원 공간의 hello 거리를 반환합니다. Hello 전원 및 둘 이상의 ValueSource 인스턴스를 사용 하 고 hello 두 벡터 사이의 hello 거리를 계산 합니다. 각 ValueSource는 숫자여야 합니다. 전달 되는 ValueSource 인스턴스의 수는 짝수 이어야 하며 hello 메서드에서 처음 절반은 hello는 hello 첫 번째 벡터를 나타내고 hello 두 번째 절반 hello 두 번째 벡터를 나타냅니다. |`dist(2, x, y, 0, 0)`Hello (0, 0) 사이의 유 클 리 디안 거리를 계산 및 (x, y) 각 문서에 대 한 합니다. <br> `dist(1, x, y, 0, 0)`계산 (0, 0) 사이의 맨해튼 (택시) 거리 hello 및 (x, y) 각 문서에 대 한 합니다. <br> `dist(2,,x,y,z,0,0,0)` 각 문서에 대해 (0,0,0)과 (x,y,z) 사이의 유클리드 거리를 계산합니다.<br>`dist(1,x,y,z,e,f,g)` (x,y,z)와 (e,f,g) 사이의 맨해턴 거리이며 각 문자는 필드 이름입니다. |
| exists |Hello 필드의 멤버가 있는 경우 TRUE 반환 존재합니다. |`exists(author)`Hello "author" 필드에 값이 있는 임의 문서에 대 한 TRUE를 반환 합니다.<br>`exists(query(price:5.00))` "price"가 "5.00"과 일치할 경우 TRUE를 반환합니다. |
| exp |발생 한 toopower 반환 오일러의 수 x. |`exp(x)` |
| floor |Tooan 정수로 내림 합니다. |`floor(x)`  <br> `floor(5.6)` 5를 반환합니다. |
| hypo |중간 오버플로 또는 언더플로 없이 sqrt(sum(pow(x,2),pow(y,2)))를 반환합니다. |`hypo(x,y)`  <br> ` |
| if |조건부 함수 쿼리를 사용합니다. `if(test,value1,value2)`, 테스트 되었거나 tooa 논리 값 또는 논리적 값 (TRUE 또는 FALSE)을 반환 하는 식을 참조 합니다. `value1`hello 값 함수에서 반환 hello 테스트가 TRUE를 나타낼 경우. `value2`hello 값 함수에서 반환 hello 테스트가 FALSE를 나타낼 경우. 식은 부울 값을 출력하는 함수일 수 있습니다. 또한 숫자 값을 반환하는 함수일 수도 있으며, 이 경우 값 0은 FALSE 또는 반환 문자열로 해석되며, 후자의 경우 빈 문자열은 FALSE로 해석됩니다. |`if(termfreq(cat,'electronics'),popularity,42)`이 함수는 hello hello cat 필드에 표시 된 "electronics" 라는 용어가 포함 된 경우 각 문서 toosee를 확인 합니다. 다음 hello지 않습니다, hello popularity 필드의 값이 반환 됩니다. 그렇지 않으면 hello 값 42가 반환 됩니다. |
| linear |`m*x+c`을 구현하며, 여기서 m과 c는 상수이고 x는 임의의 함수입니다. 이것은 너무`sum(product(m,x),c)`, 하지만 단일 함수로 구현 되므로 약간 더 효율적입니다. |`linear(x,m,c) linear(x,2,4)` `2*x+4`를 반환합니다 |
| ln |반환 hello 자연 로그의 hello 함수를 지정 합니다. |`ln(x)` |
| 로그 |반환 hello 로그 밑수 10을 hello 함수를 지정 합니다. |`log(x)   log(sum(x,100))` |
| map |Min 및 max (포함) toohello 지정 된 대상에 속하는 입력된 함수 x의 값을 매핑합니다. hello 인수 min 및 max는 상수 여야 합니다. 상수 또는 함수 hello target 및 기본 수 있습니다. X의 hello 값은 min과 max 사이의 속하지 않을, 하는 경우 다음 x의 hello 값 중 하나가 반환 되는지, 아니면 5 번째 인수로 지정 된 경우 기본값이 반환 됩니다. |`map(x,min,max,target) map(x,0,0,1)`값 0 too1로 변경 합니다. 이 함수는 기본값 0을 처리하는 데 유용할 수 있습니다.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`0부터 100 too1 및 모든 다른 값 너무-1 사이의 모든 값을 변경합니다.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`0과 100 toox 사이의 모든 값 + 599 및 hello 용어의 'solr' hello 필드 텍스트에 있는 다른 모든 값 toofrequency 변경합니다. |
| max |반환 hello 다중 중첩 된 함수 또는 상수 인수로 지정 되는 최대 숫자 값: `max(x,y,...)`합니다. max 함수 hello "bottoming" 다른 함수에 대 한 유용할 수 있습니다 또는 일부 필드는 상수를 지정 합니다.  사용 하 여 hello `field(myfield,max)` 구문 hello 단일 다중값된 필드의 최대 값을 선택 합니다. |`max(myfield,myotherfield,0)` |
| Min |반환 값 여러 개의 중첩 된 인수로 지정 된 상수 함수의 hello: `min(x,y,...)`합니다. hello min 함수는 상수를 사용 하는 함수에 "상한"을 제공 하는 데 유용할 수 있습니다. 사용 하 여 hello `field(myfield,min)` hello 단일 다중값된 필드의 최소 값을 선택 하기 위한 구문입니다. |`min(myfield,myotherfield,0)` |
| mod |Hello 함수 y로 hello 함수 x의 hello 모듈러스를 계산합니다. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| ms |인수간 차이를 밀리초 단위로 반환합니다. 상대 toohello Unix 또는 POSIX epoch, UTC 1970 년 1 월 1 일 자정은 하는 날짜입니다. 인수는 날짜나 NOW hello의 이름은 인덱싱된 TrieDateField 또는 날짜 상수는 날짜에 따라 식일 수 있습니다. `ms()`너무`ms(NOW)`, hello epoch 이후의 시간 (밀리초)의 수입니다. `ms(a)`hello 인수를 나타내는 hello epoch 이후의 시간 (밀리초) hello 번호를 반환 합니다. `ms(a,b)`b hello 기간 (밀리초) 반환 하기 전에 발생 a, 즉 `a - b`합니다. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| not |hello의 논리적으로 부정 hello 값 래핑된 함수입니다. |`not(exists(author))` `exists(author)`가 false일 경우에만 TRUE입니다. |
| 또는 |논리적 분리. |`or(value1,value2)` value1 또는 value2가 true일 경우에만 TRUE입니다. |
| pow |발생 hello 지정 지정 된 기본 toohello 전원 합니다. `pow(x,y)`y의 거듭제곱을 x toohello를 발생 시킵니다. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`sqrt와 동일 hello 합니다. |
| product |반환 hello 제품의 다중 값 또는 함수의 쉼표로 구분 된 목록에 지정 됩니다. `mul(...)` 도 이 함수의 별칭으로 사용될 수 있습니다. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |`recip(x,m,a,b)`를 구현하는 `a/(m*x+b)`를 사용하는 역함수를 수행합니다. 여기서 m, a 및 b는 상수이며 x는 임의의 복소수 함수입니다. a와 b가 동일하고 x>=0일 경우 이 함수의 최대값 1은 x가 증가함에 따라 감소합니다. Hello 값이 늘어나는 고 hello 함수 전체 tooa의 이동에서 b 함께 결과 일반적인 방법 hello 곡선의 일부입니다. 이러한 속성으로 인해 x가 `rord(datefield)`일 때 더 많은 최근 문서를 출력하는 데 적합한 함수가 됩니다. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |도 tooradians를 변환합니다. |`rad(x)` |
| rint |가장 근접 한 정수로 반올림 toohello 합니다. |`rint(x)`  <br> `rint(5.6)` 6을 반환합니다. |
| sin |각도의 사인을 반환합니다. |`sin(x)` |
| sinh |각도의 쌍곡선 사인을 반환합니다. |`sinh(x)` |
| 크기 조정 |Hello 함수 x의 값 크기 조정, hello 사이 지정 된 minTarget와 maxTarget (포함). 현재 구현 hello hello 올바른 소수 자릿수를 선택할 수 있도록 모든 hello 함수 값 tooobtain hello min 및 max 트래버스 합니다. 문서를 삭제 하는 경우 현재 구현 hello 구분할 수 없습니다 또는 값이 없는 문서. 그러한 경우는 0.0 값을 사용합니다. 이 값은 일반적으로 0.0 보다 큰 경우 하나는 여전히 결국 0.0에서 min 값 toomap hello으로 의미 합니다. 이러한 경우 적절 한 `map()` 함수 다음 그림과 같이 hello 실제 범위 내에 해결 방법 toochange 0.0 tooa 값으로 사용 될 수 있습니다.`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`1과 2 (포함) 사이의 모든 값이 되도록 눈금 x의 값을 hello 합니다. |
| sqrt |Hello의 반환 hello 제곱근 값 또는 함수를 지정 합니다. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |두 문자열 사이의 hello 거리를 계산합니다. Hello Lucene 맞춤법 검사기 StringDistance 인터페이스를 사용 하 고 해당 패키지에서 사용할 수 있는 hello 구현의 모두 지원 합니다. 또한 응용 프로그램 tooplug을 로드 기능을 통해 자기 자신, Solr의 리소스에 있습니다. strdist는 `(string1, string2, distance measure)`를 사용합니다. 거리 측정에 가능한 값은 <ul><li>jw: Jaro-Winkler</li><li>edit: Levenstein 또는 편집 거리</li><li>ngram: NGramDistance, hello를 지정 하는 경우 선택적으로 전달할 수 ngram 크기도 제공할 hello 너무 합니다. 기본값은 2입니다.</li><li>FQN: 구현 된 StringDistance 인터페이스 hello에 대 한 이름을 클래스를 정규화 합니다. 인수가 없는 생성자여야 합니다.</li></ul> |`strdist("SOLR",id,edit)` |
| sub |`sub(x,y)`에서 x-y를 반환합니다. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| sum |반환 hello 다중 값 또는 함수의 쉼표로 구분 된 목록에 지정 된의 합계입니다. `add(...)` 도 이 함수의 별칭으로 사용될 수 있습니다. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Hello hello 용어가 나타나는 횟수 해당 문서에 대 한 hello 필드에 반환 합니다. |termfreq(text,'memory') |
| tan |각도의 탄젠트를 반환합니다. |`tan(x)` |
| tanh |각도의 쌍곡선 탄젠트를 반환합니다. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>검색 필드 및 패싯 참조
로그 검색 toofind 데이터를 사용할 때 결과가 다양 한 필드 및 패싯을 표시 됩니다. Hello 정보 중 일부는 매우 자세히 나타나지 않을 수 있습니다. 다음 정보 toohelp hello 결과 이해 하는 hello를 사용 합니다.

| 필드 | 검색 유형 | 설명 |
| --- | --- | --- |
| TenantId |모두 |Toopartition 데이터를 사용 합니다. |
| TimeGenerated |모두 |Toodrive hello 타임 라인, timeselectors입니다 (검색 및 다른 화면)을 사용합니다. 데이터의 hello 일부가 (일반적으로 hello 에이전트)에서 생성 된 때를 나타냅니다. ISO 형식으로 표현 되 hello 시간이 며 항상 UTC입니다. 기존 계측 (즉, 로그의 이벤트)를 기반으로 하는 형식의 hello 경우이 일반적으로 hello 해당 hello 로그 항목/라인/레코드가 기록 된 실제 시간입니다. 일부 hello에 대 한 다른 형식 (예를 들어 권장 사항 또는 경고) hello 클라우드 또는 관리 팩을 통해 생성 되는 서로 다른 무엇 인가 시간 나타냅니다 hello 합니다. 이 새 데이터 조각 일종의 구성 스냅숏 사용 하 여 수집 된 또는 권장 사항/경고가 그에 따라 생성 된 경우 hello 시간입니다. |
| EventID |이벤트 |Hello Windows 이벤트 로그에서 EventID입니다. |
| EventLog |이벤트 |이벤트 로그에서 Windows hello 이벤트를 로그 하는 위치입니다. |
| EventLevelName |이벤트 |중요/경고/정보/성공 |
| EventLevel |이벤트 |중요/경고/정보/성공에 대한 숫자 값입니다(보다 쉽게/보다 읽기 쉬운 쿼리 대신 EventLevelName 사용). |
| SourceSystem |모두 |Hello 데이터에서 제공 된 위치 (의 측면에서 모드 toohello 서비스 첨부). 예를 들어 Microsoft System Center Operations Manager 및 Azure Storage를 포함합니다. |
| ObjectName |PerfHourly |Windows 성능 개체 이름입니다. |
| InstanceName |PerfHourly |Windows 성능 카운터 인스턴스 이름입니다. |
| CounteName |PerfHourly |Windows 성능 카운터 이름입니다. |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Operations Manager에서 성능 수집 규칙이 대상으로 하는 hello 개체의 표시 이름입니다. 또한 Operational Insights에서 검색 되는 hello 개체의 표시 이름을 hello 수 또는 어떤 hello에 대 한 경고가 발생 했습니다. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Hello 부모 (이중 호스팅 관계)에서 Operations Manager에서 성능 수집 규칙이 대상으로 하는 hello 개체의 hello 부모의 이름을 표시 합니다. 또한 Operational Insights에서 검색 되는 hello 개체의 표시 이름을 hello 수 또는 어떤 hello에 대 한 경고가 발생 했습니다. |
| 컴퓨터 |대부분의 형식 |Hello 데이터가 속한 컴퓨터 이름입니다. |
| DeviceName |ProtectionStatus |컴퓨터 이름 hello 데이터가 너무 속한 ("Computer"와 같음). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |위협 상태 순위는 hello 위협 상태의 숫자 표현입니다. 비슷한 tooHTTP 응답 코드 hello 순위 hello 번호 사이 간격이 발생 했습니다 (위협이 아닌 이유은 150 및 하지 100 또는 0), 방 tooadd는 새 상태를 유지 합니다. 위협 상태 및 보호 상태 롤업을 hello 의도 tooshow hello 있었던 최악의 상태를 컴퓨터 hello 된 동안에 hello 특정 기간입니다. hello 숫자 순위 hello 다양 한 상태의 번호가 높은 hello hello 레코드를 볼 수 있도록 합니다. |
| ThreatStatus |ProtectionStatus |ThreatStatus에 대한 설명이며, ThreatStatusRank와 1:1 매핑합니다. |
| TypeofProtection |ProtectionStatus |Hello 컴퓨터에서 검색 된 맬웨어 방지 제품: 없음, Microsoft 맬웨어 제거 도구, Forefront, 등에. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |이 컴퓨터의 에이전트에 대한 HealthService ID입니다. |
| HealthServiceId |대부분의 형식 |이 컴퓨터의 에이전트에 대한 HealthService ID입니다. |
| ManagementGroupName |대부분의 형식 |Operations Manager에 연결된 에이전트용 관리 그룹 이름입니다. 그렇지 않은 경우 null/blank입니다. |
| ObjectType |ConfigurationObject |Log Analytics 구성 평가에서 검색된 개체의 형식(Operations Manager 관리 팩의 형식/클래스와 동일)입니다. |
| UpdateTitle |RequiredUpdate |설치 된 발견 된 hello 업데이트의 이름입니다. |
| PublishDate |RequiredUpdate |Hello 업데이트 Microsoft 업데이트에 게시 된 시점입니다. |
| 서버 |RequiredUpdate |컴퓨터 이름 hello 데이터가 너무 속한 ("Computer"와 같음). |
| 제품 |RequiredUpdate |Hello 업데이트 제품에 적용 됩니다. |
| UpdateClassification |RequiredUpdate |업데이트 유형(예를 들어 업데이트 롤업 또는 서비스 팩)입니다. |
| KBID |RequiredUpdate |모범 사례 또는 업데이트를 설명하는 KB 문서 ID입니다. |
| WorkflowName |ConfigurationAlert |Hello 규칙 또는 hello 경고를 생성 하는 모니터의 이름입니다. |
| 심각도 |ConfigurationAlert |Hello 경고의 심각도입니다. |
| 우선 순위 |ConfigurationAlert |Hello 경고의 우선 순위입니다. |
| IsMonitorAlert |ConfigurationAlert |이 경고는 모니터(true) 또는 규칙(false)에 의해 생성되었습니까? |
| AlertParameters |ConfigurationAlert |Hello 로그 분석 경고의 hello 매개 변수를 사용 하 여 XML입니다. |
| Context |ConfigurationAlert |Hello 로그 분석 경고의 hello 컨텍스트를 사용 하 여 XML입니다. |
| 워크로드 |ConfigurationAlert |경고 hello는 기술 또는 작업을 가리킵니다. |
| AdvisorWorkload |권장 사항 |권장 사항 hello는 기술 또는 작업을 가리킵니다. |
| 설명 |ConfigurationAlert |경고 설명(간략)입니다. |
| DaysSinceLastUpdate |UpdateAgent |날 (이 레코드의 상대 tooTimeGenerated)가이 에이전트에서 업데이트를 설치한 서버 업데이트 서비스 WSUS (Windows) 또는 Microsoft Update? |
| DaysSinceLastUpdateBucket |UpdateAgent |DaysSinceLastUpdate에 따라 컴퓨터가 WSUS/Microsoft Update에서 업데이트를 마지막 설치한 것이 얼마 전인지에 대한 시간 버킷의 분류입니다. |
| AutomaticUpdateEnabled |UpdateAgent |자동 업데이트가 이 에이전트에서 활성화 또는 비활성화를 확인하고 있습니까? |
| AutomaticUpdateValue |UpdateAgent |자동 업데이트 검사 집합 tooautomatically 다운로드 및 설치, 다운로드만 또는 확인만? |
| WindowsUpdateAgentVersion |UpdateAgent |Hello Microsoft 업데이트 에이전트의 버전 번호입니다. |
| WSUSServer |UpdateAgent |어떤 WSUS 서버가 이 업데이트 에이전트를 대상으로 합니까? |
| OSVersion |UpdateAgent |이 업데이트 에이전트에서 실행 중인 hello 운영 체제의 버전입니다. |
| 이름 |Recommendation, ConfigurationObjectProperty |이름/제목 hello 권장 또는 로그 분석 구성 평가에서 hello 속성의 이름입니다. |
| 값 |ConfigurationObjectProperty |Log Analytics 구성 평가에서 속성의 값입니다. |
| KBLink |권장 사항 |이 모범 사례 또는 업데이트를 설명 하는 URL toohello KB 문서입니다. |
| RecommendationStatus |권장 사항 |권장 사항을 레코드가 업데이트 되 고 방금 추가한 toohello 검색 인덱스를 가져올 몇 가지 유형 hello 가장 합니다. 로그 분석에 해결 된 것을 감지 했는지 hello 권장 구성을 액티브/열기 인지 또는이 상태가 변경 합니다. |
| RenderedDescription |이벤트 |Windows 이벤트의 렌더링된 설명(채워진 매개 변수와 재사용된 텍스트)입니다. |
| ParameterXml |이벤트 |Windows 이벤트 (이벤트 뷰어 처럼)의 데이터 섹션 hello에에서 hello 매개 변수를 사용 하 여 XML입니다. |
| EventData |이벤트 |Windows 이벤트 (이벤트 뷰어 처럼)의 hello 전체 데이터 섹션 XML입니다. |
| 원본 |이벤트 |이벤트 로그 소스 hello 이벤트를 생성 합니다. |
| EventCategory |이벤트 |Hello Windows 이벤트 로그에서 직접 hello 이벤트의 범주입니다. |
| 사용자 이름 |이벤트 |Hello Windows 이벤트 (일반적으로 NT AUTHORITY\LOCALSYSTEM)의 사용자 이름입니다. |
| SampleValue |PerfHourly |성능 카운터의 시간별 집계 hello에 대 한 평균 값입니다. |
| Min |PerfHourly |Hello 성능 카운터 매시간 집계의 시간 간격의 최소값입니다. |
| max |PerfHourly |Hello 성능 카운터 매시간 집계의 시간 간격의 최대값입니다. |
| Percentile95 |PerfHourly |hello 95 번째 백분위 수 값 hello 성능 카운터 매시간 집계의 시간 간격입니다. |
| SampleCount |PerfHourly |얼마나 많은 원시 성능 카운터 샘플이 된 사용된 tooproduce이 매시간 집계 레코드 합니다. |
| 위협 |ProtectionStatus |발견한 맬웨어의 이름입니다. |
| StorageAccount |W3CIISLog |Azure 저장소 계정 hello 로그에서 읽은 합니다. |
| AzureDeploymentID |W3CIISLog |Hello 클라우드 서비스 hello 로그의 azure 배포 ID에 속해 있습니다. |
| 역할 |W3CIISLog |Hello Azure 클라우드 서비스 hello 로그의 역할에 속합니다. |
| RoleInstance |W3CIISLog |Hello 로그 hello Azure 역할의 RoleInstance에 속해 있습니다. |
| sSiteName |W3CIISLog |로그 hello 하는 IIS 웹 사이트가 속해 too(metabase notation); hello hello 원래 로그에서 s-sitename 필드입니다. |
| sComputerName |W3CIISLog |hello hello 원래 로그에서 s-computername 필드입니다. |
| sIP |W3CIISLog |서버 IP 주소 hello HTTP 요청이 지정 된입니다. hello hello 원래 로그에서 s-ip 필드입니다. |
| csMethod |W3CIISLog |(예: GET/POST) HTTP 메서드를 hello 클라이언트가 hello HTTP 요청에 사용 합니다. hello 원래 로그에서 cs-method hello 합니다. |
| cIP |W3CIISLog |클라이언트 IP 주소 hello HTTP 요청에서 제공 합니다. hello hello 원래 로그에서 c-ip 필드입니다. |
| csUserAgent |W3CIISLog |Hello 클라이언트에서 선언한 HTTP 사용자 에이전트 (브라우저 또는 그렇지 않은 경우). hello cs-사용자-에이전트 hello 원래 로그에서입니다. |
| scStatus |W3CIISLog |HTTP 상태 코드 (예를 들어 200/403/500) hello 서버 toohello 클라이언트에서 반환 합니다. hello 원래 로그에서 cs-status hello 합니다. |
| TimeTaken |W3CIISLog |Hello 요청 하는 시간 (밀리초) toocomplete를 걸렸습니다. hello hello 원래 로그에서 timetaken 필드입니다. |
| csUriStem |W3CIISLog |요청된 상대 URI( 호스트 주소 즉, /search 없이)입니다. hello hello 원래 로그에서 cs-uristem 필드입니다. |
| csUriQuery |W3CIISLog |URI 쿼리입니다. URI 쿼리는 ASP 페이지와 같은 동적 페이지에만 필요하므로 이 필드는 일반적으로 정적 페이지에 대한 하이픈을 포함합니다. |
| sPort |W3CIISLog |너무 전송 HTTP 요청을 hello 서버 포트 (및 선택 되었기 때문에 IIS에서 수신함). |
| csUserName |W3CIISLog |인증 된 사용자 이름 hello 요청이 인증 되 고 익명이 아닌 경우. |
| csVersion |W3CIISLog |Hello 요청 (예: HTTP/1.1)에 사용 되는 HTTP 프로토콜 버전입니다. |
| csCookie |W3CIISLog |쿠키 정보입니다. |
| csReferer |W3CIISLog |해당 hello 사용자가 마지막으로 방문한 사이트입니다. 이 사이트 링크 toohello 현재 사이트를 제공 합니다. |
| csHost |W3CIISLog |요청된 호스트 헤더(예: www.mysite.com)입니다. |
| scSubStatus |W3CIISLog |하위 상태 오류 코드입니다. |
| scWin32Status |W3CIISLog |Windows 상태 코드입니다. |
| csBytes |W3CIISLog |Hello 클라이언트 toohello 서버 hello 요청에서 보낸 바이트 수입니다. |
| scBytes |W3CIISLog |바이트는 hello 서버 toohello 클라이언트로부터 hello 응답에서 반환 합니다. |
| ConfigChangeType |ConfigurationChange |변경의 유형(예: WindowsServices/소프트웨어)입니다. |
| ChangeCategory |ConfigurationChange |Hello 변경 (수정/추가/제거 됨)의 범주입니다. |
| SoftwareType |ConfigurationChange |소프트웨어의 종류(업데이트/응용 프로그램)입니다. |
| SoftwareName |ConfigurationChange |Hello 소프트웨어 (적용 가능한 toosoftware 변경 내용만)의 이름입니다. |
| 게시자 |ConfigurationChange |Hello (적용 가능한 toosoftware 변경 내용만) 소프트웨어를 게시 하는 공급 업체입니다. |
| SvcChangeType |ConfigurationChange |Windows 서비스에 적용된 변경의 유형(상태/StartupType/경로/ServiceAccount)입니다. 서비스 변경 내용만 적용 가능한 tooWindows입니다. |
| SvcDisplayName |ConfigurationChange |변경 된 hello 서비스의 표시 이름입니다. |
| SvcName |ConfigurationChange |변경 된 hello 서비스의 이름입니다. |
| SvcState |ConfigurationChange |Hello 서비스의 새 (현재) 상태입니다. |
| SvcPreviousState |ConfigurationChange |이전에 알려진 hello 서비스 (서비스 상태를 변경 하는 경우에 해당)의 상태입니다. |
| SvcStartupType |ConfigurationChange |서비스 시작 유형입니다. |
| SvcPreviousStartupType |ConfigurationChange |이전 서비스 시작 유형(서비스 시작 유형을 변경하는 경우만 해당)입니다. |
| SvcAccount |ConfigurationChange |서비스 계정입니다. |
| SvcPreviousAccount |ConfigurationChange |이전 서비스 계정(서비스 계정이 변경된 경우만 해당)입니다. |
| SvcPath |ConfigurationChange |경로 toohello hello Windows 서비스의 실행 파일입니다. |
| SvcPreviousPath |ConfigurationChange |Hello hello Windows 서비스 (이것이 변경 된 경우에 해당)에 대 한 실행 파일의 이전 경로입니다. |
| SvcDescription |ConfigurationChange |Hello 서비스의 설명입니다. |
| 이전 |ConfigurationChange |이 소프트웨어의 이전 상태(설치됨/설치되지 않음/이전 버전)입니다. |
| Current |ConfigurationChange |이 소프트웨어의 최근 상태(설치됨/설치되지 않음/현재 버전)입니다. |

## <a name="next-steps"></a>다음 단계
로그 검색에 대한 자세한 내용은 다음을 참조하십시오.

* 익숙해질 목적으로 [검색 로그](log-analytics-log-searches.md) tooview 솔루션에서 수집 된 정보를 자세히 설명 합니다.
* 사용 하 여 [로그 분석의 사용자 지정 필드가](log-analytics-custom-fields.md) tooextend 로그 검색 합니다.
