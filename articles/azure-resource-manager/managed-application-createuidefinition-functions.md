---
title: "관리 되는 응용 프로그램 aaaAzure UI 정의 함수를 만들 | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 UI 정의 생성할 때 hello 함수 toouse 설명"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a>CreateUiDefinition 함수
이 섹션에는 CreateUiDefinition의 지원 되는 모든 함수에 대 한 hello 서명을 포함합니다.

toouse는 함수를 대괄호로 서라운드 hello 선언 합니다. 예:

```json
"[function()]"
```

문자열 및 기타 함수를 함수에 대한 매개 변수로 참조할 수 있지만 문자열을 따옴표로 묶어야 합니다. 예:

```json
"[fn1(fn2(), 'foobar')]"
```

해당 되는 경우에 hello 점 연산자를 사용 하 여 함수 hello 출력의 속성을 참조할 수 있습니다. 예:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>참조 함수
이러한 함수는 hello 속성 또는 CreateUiDefinition의 컨텍스트에서 사용 되는 tooreference 출력 될 수 있습니다.

### <a name="basics"></a>기본 사항
Hello 기본적인 단계에 정의 된 요소의 hello 출력 값을 반환 합니다.

hello 다음 예제에서는 출력을 반환 hello 라는 hello 요소의 `foo` hello 기본 사항 단계에서:

```json
"[basics('foo')]"
```

### <a name="steps"></a>단계
단계를 지정된 하는 hello에 정의 된 요소의 hello 출력 값을 반환 합니다. hello 기본적인 단계에 있는 요소의 tooget hello 출력 값에 사용 하 여 `basics()` 대신 합니다.

hello 다음 예제에서는 출력을 반환 hello 라는 hello 요소의 `bar` hello 단계 라는 `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Hello 현재 컨텍스트 또는 hello 기본 사항 단계에서 선택한 hello 위치를 반환 합니다.

hello 다음 예제에서는 반환 될 수 `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>문자열 함수
이러한 함수는 JSON 문자열하고만 사용할 수 있습니다.

### <a name="concat"></a>concat
하나 이상의 문자열을 연결합니다.

예를 들어 hello 출력 값의 `element1` 경우 `"bar"`, hello 문자열을 반환 하는이 예에서는 다음 `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
지정 된 hello의 hello 부분 문자열을 반환 합니다. hello 지정 된 인덱스에서 시작 된 hello 부분 문자열을이 hello 길이 지정 합니다.

hello 다음 예제에서는 반환 `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>replace
Hello 발견 되는 모든 문자열 hello 현재 문자열에 문자열을 지정 된 반환 된 다른 문자열로 대체 됩니다.

hello 다음 예제에서는 반환 `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
전역적으로 고유한 문자열(GUID)을 생성합니다.

hello 다음 예제에서는 반환 될 수 `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
변환 된 문자열 toolowercase를 반환합니다.

hello 다음 예제에서는 반환 `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
변환 된 문자열 toouppercase를 반환합니다.

hello 다음 예제에서는 반환 `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>컬렉션 함수
이러한 함수는 JSON 문자열, 배열, 개체 등의 컬렉션과 함께 사용할 수 있습니다.

### <a name="contains"></a>contains
반환 `true` 문자열에 포함 된 경우 지정 된 부분 문자열 hello, 배열에 포함 되어 hello 지정한 키가 들어 있는 개체 또는 hello 값을 지정 합니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 다음 예제에서는 반환 `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>length
문자열, 배열에는 값의 hello 수 또는 키 개체에 hello 수의 문자 수가 hello를 반환합니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 다음 예제에서는 반환 `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
반환 `true` hello 문자열, 배열 또는 개체가 null 이거나 비어 있으면 합니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 다음 예제에서는 반환 `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>예제 4: null 및 undefined
`element1`이 `null` 또는 undefined라고 가정합니다. hello 다음 예제에서는 반환 `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
지정 된 문자열의 hello 반환 hello 첫 번째 문자가 지정 된 배열 hello;의 첫 번째 값 또는 첫 번째 키와 hello 지정된 개체의 값을 환영 합니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
hello 다음 예제에서는 반환 `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
지정 된 hello 반환 hello 마지막 문자는 문자열, hello hello 지정 배열의 마지막 값 또는 hello 마지막 키와 hello 지정된 개체의 값입니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 다음 예제에서는 반환 `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
지정된 된 수의 hello hello 문자열 시작에서 연속 된 문자, 지정된 된 수의 hello 배열의 hello 시작에서 인접 하는 값 또는 지정 된 개수의 연속 키와 hello 시작 hello 개체의 값을 반환합니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 다음 예제에서는 반환 `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
지정 된 된 수는 컬렉션의 요소를 무시 하 고 나머지 요소의 hello를 반환 합니다.

#### <a name="example-1-string"></a>예제 1: 문자열
hello 다음 예제에서는 반환 `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>예제 2: 배열
`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다. hello 다음 예제에서는 반환 `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>예제 3: 개체
`element1`이 다음을 반환한다고 가정합니다.

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
hello 다음 예제에서는 반환 `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>논리 함수
조건문에서 이러한 함수를 사용할 수 있습니다. 일부 함수는 모든 JSON 데이터 형식을 지원하지 않을 수 있습니다.

### <a name="equals"></a>equals
반환 `true` 두 매개 변수에 있는 hello 동일한 입력 한 값 경우. 이 함수는 모든 JSON 데이터 형식을 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[equals(0, 0)]"
```

hello 다음 예제에서는 반환 `true`:

```json
"[equals('foo', 'foo')]"
```

hello 다음 예제에서는 반환 `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
반환 `true` hello 첫 번째 매개 변수가 이면 hello 두 번째 매개 변수 보다 작아야 합니다. 이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[less(1, 2)]"
```

hello 다음 예제에서는 반환 `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
반환 `true` hello 첫 번째 매개 변수 보다 작거나 같은 경우 toohello 두 번째 매개 변수입니다. 이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
반환 `true` hello 첫 번째 매개 변수가 엄격 하 게 hello 두 번째 매개 변수 보다 큰 경우. 이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `false`:

```json
"[greater(1, 2)]"
```

hello 다음 예제에서는 반환 `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
반환 `true` hello 첫 번째 매개 변수 보다 크거나 같은 toohello 두 번째 매개 변수인 경우. 이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>and
반환 `true` 모든 hello 매개 변수가 너무 평가 되 면`true`합니다. 이 함수는 두 개 이상의 부울 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

hello 다음 예제에서는 반환 `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>또는
반환 `true` hello 매개 변수 중 하나 이상이 너무 평가 되 면`true`합니다. 이 함수는 두 개 이상의 부울 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

hello 다음 예제에서는 반환 `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>not
반환 `true` hello 매개 변수가 너무 평가 하는 경우`false`합니다. 이 함수는 부울 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[not(false)]"
```

hello 다음 예제에서는 반환 `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
반환 hello hello 첫 번째 null이 아닌 매개 변수의 값입니다. 이 함수는 모든 JSON 데이터 형식을 지원합니다.

`element1` 및 `element2`를 undefined로 가정합니다. hello 다음 예제에서는 반환 `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>변환 함수
이러한 함수에는 JSON 데이터 형식 및 인코딩에서 간에 사용 되는 tooconvert 값일 수 있습니다.

### <a name="int"></a>int
Hello tooan 정수 매개 변수를 변환합니다. 이 함수는 숫자 및 문자열 형식의 매개 변수를 지원합니다.

hello 다음 예제에서는 반환 `1`:

```json
"[int('1')]"
```

hello 다음 예제에서는 반환 `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>float
Hello 매개 변수 tooa 부동 소수점 변환합니다. 이 함수는 숫자 및 문자열 형식의 매개 변수를 지원합니다.

hello 다음 예제에서는 반환 `1.0`:

```json
"[float('1.0')]"
```

hello 다음 예제에서는 반환 `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>string
Hello 매개 변수 tooa 문자열을 변환합니다. 이 함수는 모든 JSON 데이터 형식의 매개 변수를 지원합니다.

hello 다음 예제에서는 반환 `"1"`:

```json
"[string(1)]"
```

hello 다음 예제에서는 반환 `"2.9"`:

```json
"[string(2.9)]"
```

hello 다음 예제에서는 반환 `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

hello 다음 예제에서는 반환 `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>bool
Hello 매개 변수 tooa 부울 값으로 변환합니다. 이 함수는 숫자, 문자열 및 부울 형식의 매개 변수를 지원합니다. JavaScript 제외한 모든 값에에서 비슷한 tooBooleans `0` 또는 `'false'` 반환 `true`합니다.

hello 다음 예제에서는 반환 `true`:

```json
"[bool(1)]"
```

hello 다음 예제에서는 반환 `false`:

```json
"[bool(0)]"
```

hello 다음 예제에서는 반환 `true`:

```json
"[bool(true)]"
```

hello 다음 예제에서는 반환 `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parse
Hello 매개 변수 tooa 네이티브 형식으로 변환합니다. 즉,이 함수는의 hello 역 `string()`합니다. 이 함수는 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `1`:

```json
"[parse('1')]"
```

hello 다음 예제에서는 반환 `true`:

```json
"[parse('true')]"
```

hello 다음 예제에서는 반환 `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

hello 다음 예제에서는 반환 `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Hello 매개 변수 tooa e-64로 인코딩된 문자열을 인코딩합니다. 이 함수는 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Hello 매개 변수를에서 e-64로 인코딩된 문자열을 디코딩합니다. 이 함수는 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Hello 매개 변수 tooa URL로 인코딩된 문자열을 인코딩합니다. 이 함수는 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Hello 매개 변수를를 URL로 인코딩된 문자열로 디코딩합니다. 이 함수는 문자열 형식의 매개 변수만 지원합니다.

hello 다음 예제에서는 반환 `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>수학 함수
### <a name="add"></a>추가
두 숫자를 추가 하 고 hello 결과 반환 합니다.

hello 다음 예제에서는 반환 `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Hello hello 첫 번째 숫자에서 두 번째 숫자를 뺍니다 하 고 hello 결과 반환 합니다.

hello 다음 예제에서는 반환 `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
두 숫자를 곱합니다 하 고 hello 결과 반환 합니다.

hello 다음 예제에서는 반환 `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
첫 번째 숫자 hello hello 두 번째 숫자를 나누고 hello 결과 반환 합니다. hello 결과 항상는 정수입니다.

hello 다음 예제에서는 반환 `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
첫 번째 숫자 hello hello 두 번째 숫자를 나누고 hello 나머지를 반환 합니다.

hello 다음 예제에서는 반환 `0`:

```json
"[mod(6, 3)]"
```

hello 다음 예제에서는 반환 `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
반환 hello hello 두 숫자의 작은 합니다.

hello 다음 예제에서는 반환 `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
반환 hello hello 두 숫자 중 더 큰 숫자입니다.

hello 다음 예제에서는 반환 `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
정수 시퀀스를 생성 hello 내에서 숫자 범위를 지정 합니다.

hello 다음 예제에서는 반환 `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
임의 반환 hello 내의 정수 계열 숫자 범위를 지정 합니다. 이 함수는 암호화하여 보안 설정된 난수를 생성하지 않습니다.

hello 다음 예제에서는 반환 될 수 `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
보다 작거나 같은 최대 정수 hello 반환 toohello 번호를 지정 합니다.

hello 다음 예제에서는 반환 `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
반환 hello 보다 큰 가장 큰 정수 또는 같은 toohello 번호를 지정 하십시오.

hello 다음 예제에서는 반환 `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>날짜 함수
### <a name="utcnow"></a>utcNow
ISO 8601 서식의 hello hello 로컬 컴퓨터의 현재 날짜 및 시간 문자열을 반환 합니다.

hello 다음 예제에서는 반환 될 수 `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
지정 된 시간 (초) toohello의 정수가 추가 하는 타임 스탬프입니다.

hello 다음 예제에서는 반환 `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
지정 된 시간 (분) toohello의 정수가 추가 하는 타임 스탬프입니다.

hello 다음 예제에서는 반환 `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
지정 된 시간 toohello의 정수가 추가 하는 타임 스탬프입니다.

hello 다음 예제에서는 반환 `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>다음 단계
* 리소스 관리자에는 소개 tooAzure 참조 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.

