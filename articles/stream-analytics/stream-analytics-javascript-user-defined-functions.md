---
title: "aaaAzure 스트림 분석 JavaScript 사용자 정의 함수가 | Microsoft Docs"
description: "JavaScript 사용자 정의 함수로 고급 쿼리 역학 수행"
keywords: "javascript, 사용자 정의 함수, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Azure Stream Analytics JavaScript 사용자 정의 함수
Azure Stream Analytics에서는 JavaScript로 작성된 사용자 정의 함수를 지원합니다. 풍부한 hello와 **문자열**, **RegExp**, **수학**, **배열**, 및 **날짜** 메서드는 복잡 한 데이터 변환에 대 한 스트림 분석 작업에 쉽게 toocreate 있게 JavaScript에서 제공 됩니다.

## <a name="javascript-user-defined-functions"></a>JavaScript 사용자 정의 함수
JavaScript 사용자 정의 함수는 외부 연결이 필요 없는 상태 비저장, 계산 전용 스칼라 함수를 지원합니다. hello 함수 값만 값일 수는 스칼라 (단일)를 반환 합니다. JavaScript 사용자 정의 함수 tooa 작업을 추가한 후에 기본 제공 스칼라 함수 처럼 hello 쿼리에서 아무 곳 이나 hello 함수를 사용할 수 있습니다.

다음은 JavaScript 사용자 정의 함수가 유용할 수 있는 몇 가지 시나리오입니다.
* 정규식 함수를 가진 문자열을 구문 분석 및 조작(예: **Regexp_Replace()** 및 **Regexp_Extract()**)
* 데이터 디코딩 및 인코딩(예: 2진을 16진으로 변환)
* JavaScript **Math** 함수로 수학 계산 수행
* 정렬, 조인, 찾기 및 채우기 등의 배열 작업 수행

다음은 Stream Analytics에서 JavaScript 사용자 정의 함수로 수행할 수 없는 작업입니다.
* 외부 REST 끝점 호출(예: 역방향 IP 조회 수행 또는 외부 원본에서 참조 데이터 끌어오기)
* 입력/출력에서 사용자 지정 이벤트 형식 직렬화 또는 역직렬화 수행
* 사용자 지정 집계 만들기

처럼 작동 하지만 **Date.GetDate()** 또는 **Math.random()** 차단 되지 않는지 hello 함수 정의에 사용 하면 안 하 합니다. 이러한 함수 **없는** 반환 hello 동일 호출 하면 함수 호출의 저널 hello Azure 스트림 분석 서비스를 보관 하지 않습니다 때마다 발생 하 고 결과 반환 합니다. 함수는 다른 결과가 반환 hello에 동일한 이벤트 또는 hello 스트림 분석 서비스에서 작업을 다시 시작 되 면 반복성 보장 되지 않습니다.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>JavaScript 사용자 정의 함수 hello Azure 포털에 추가
toocreate는 간단한 JavaScript 사용자 정의 함수는 기존 스트림 분석 작업에서 다음이 단계를 수행 합니다.

1.  Hello Azure 포털에서에서 스트림 분석 작업을 찾습니다.
2.  **작업 토폴로지** 아래에서 함수를 선택합니다. 함수의 빈 목록이 표시됩니다.
3.  toocreate 새 사용자 정의 함수 선택 **추가**합니다.
4.  Hello에 **새 함수** 블레이드에서 대 한 **함수 형식**선택, **JavaScript**합니다. 기본 함수 템플릿을 hello 편집기에 나타납니다.
5.  Hello에 대 한 **UDF 별칭**, 입력 **hex2Int**, 다음과 같이 hello 함수 구현 변경:

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  **저장**을 선택합니다. 사용자가 함수 hello 함수 목록에 나타납니다.
7.  새 선택 hello **hex2Int** 작동 하 고 hello 함수 정의 확인 합니다. 모든 함수는 **UDF** 접두사 추가 toohello 함수 별칭입니다. 너무 필요한*hello 접두사를 포함* 스트림 분석 쿼리에 hello 함수를 호출 합니다. 이 경우 **UDF.hex2Int**를 호출합니다.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>쿼리에서 JavaScript 사용자 정의 함수 호출

1. Hello에서 쿼리 편집기에서 **작업 토폴로지**선택, **쿼리**합니다.
2.  쿼리를 편집 하 고 hello 사용자 정의 함수를 다음과 같이 호출:

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  tooupload hello 예제 데이터 파일을 마우스 오른쪽 단추로 클릭 hello 작업 입력 합니다.
4.  tootest 선택 쿼리에 **테스트**합니다.


## <a name="supported-javascript-objects"></a>지원되는 JavaScript 개체
Azure Stream Analytics JavaScript 사용자 정의 함수는 표준인 기본 제공 JavaScript 개체를 지원합니다. 이러한 개체의 목록은 [전역 개체](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)를 참조하세요.

### <a name="stream-analytics-and-javascript-type-conversion"></a>Stream Analytics 및 JavaScript 형식 변환

Hello 스트림 분석 쿼리 언어 및 JavaScript를 지원 하는 hello 형식에는 차이가 있습니다. 이 표에서 두 hello 간의 hello 변환 매핑을 보여 줍니다.

스트림 분석 | JavaScript
--- | ---
bigint | 숫자 (JavaScript 정수 tooprecisely 2 나타낼 수 있습니다 ^53)
DateTime | Date(JavaScript에서는 밀리초만 지원)
double | Number
nvarchar(MAX) | 문자열
레코드 | Object
배열 | 배열
NULL | Null


다음은 JavaScript-Stream Analytics 변환입니다.


JavaScript | 스트림 분석
--- | ---
Number | Bigint (경우 hello 번호가 round 및 long 사이입니다. MinValue 및 long입니다. MaxValue; 그렇지 않으면 double은)
Date | DateTime
String | nvarchar(MAX)
Object | 레코드
배열 | 배열
Null, Undefined | NULL
기타 다른 형식(예: 함수 또는 오류) | 지원되지 않음(런타임 오류 발생)

## <a name="troubleshooting"></a>문제 해결
JavaScript 런타임 오류, 간주 되 고 hello 활동 로그를 통해 노출 됩니다. hello Azure 포털, go tooyour 작업 및 선택 tooretrieve hello 로그 **활동 로그**합니다.


## <a name="other-javascript-user-defined-function-patterns"></a>기타 JavaScript 사용자 정의 함수 패턴

### <a name="write-nested-json-toooutput"></a>중첩 된 JSON toooutput 작성
출력 스트림 분석 작업 입력으로 사용 하는 후속 처리 단계 있고 JSON 형식이 필요한 경우에 JSON 문자열 toooutput를 작성할 수 있습니다. hello 다음 예제에서는 호출 hello **JSON.stringify()** toopack 모든 이름/값 쌍의 hello 입력과 출력에는 단일 문자열 값으로 쓸지를 작동 합니다.

**JavaScript 사용자 정의 함수 정의:**

```
function main(x) {
return JSON.stringify(x);
}
```

**샘플 쿼리:**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>도움말 보기
추가 도움이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure 스트림 분석 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
