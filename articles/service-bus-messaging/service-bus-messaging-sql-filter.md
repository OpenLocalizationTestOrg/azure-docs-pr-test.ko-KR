---
title: "서비스 버스 SQLFilter 구문 참조 aaaAzure | Microsoft Docs"
description: "SQLFilter 문법에 대한 세부 정보입니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a>SQLFilter 구문

A *SqlFilter* hello의 인스턴스가 [SqlFilter 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)에 대해 평가 되는 SQL 언어 기반 필터 식을 나타냅니다는 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)합니다. SqlFilter hello sql-92 표준의 하위 집합을 지원 합니다.  
  
 이 항목에서는 SqlFilter 문법에 대한 세부 정보를 나열합니다.  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a>인수  
  
-   `<scope>`속성은 hello hello 범위를 나타내는 선택적 문자열 `<property_name>`합니다. 유효한 값은 `sys` 또는 `user`입니다. hello `sys` 값 시스템 범위를 나타냅니다. 여기서 `<property_name>` hello의 공용 속성 이름인 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)합니다. `user`사용자 범위를 나타냅니다. 여기서 `<property_name>` hello의 키가 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 사전입니다. `user`범위 경우 hello 기본 범위는 `<scope>` 지정 되지 않았습니다.  
  
## <a name="remarks"></a>설명

시도 tooaccess 존재 하지 않는 시스템 속성 있고 오류가 시도 tooaccess 존재 하지 사용자 속성은 오류가 아닙니다. 대신, 존재하지 않는 사용자 속성은 알 수 없는 값;으로 내부적으로 평가됩니다. 알 수 없는 값은 연산자 평가 중에 특별히 처리됩니다.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>인수  

 `<regular_identifier>`hello 표시 되는 문자열은 정규식을 다음과 같습니다.  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
이 문법은 문자로 시작하고 뒤에 하나 이상의 밑줄/문자/숫자가 나오는 문자열입니다.  
  
`[:IsLetter:]`는 유니코드 문자로 분류된 유니코드 문자를 의미합니다. `System.Char.IsLetter(c)`에서는 `c`가 유니코드 문자인 경우 `true`를 반환합니다.  
  
`[:IsDigit:]`는 10진수 문자로 분류된 유니코드 문자를 의미합니다. `System.Char.IsDigit(c)`에서는 `c`가 유니코드 숫자인 경우 `true`를 반환합니다.  
  
`<regular_identifier>`는 예약된 키워드일 수 없습니다.  
  
`<delimited_identifier>`는 왼쪽/오른쪽 대괄호([])로 묶인 문자열입니다. 오른쪽 대괄호는 두 개의 오른쪽 대괄호로 표시됩니다. hello 다음은 몇 가지 `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>`는 큰따옴표로 묶인 문자열입니다. 식별자에서 큰따옴표는 두 개의 큰따옴표로 표시됩니다. Toouse 따옴표 붙은 식별자는 문자열 상수과 쉽게 혼동 될 수 있으므로 권장 되지 않습니다. 가능하면 구분된 식별자를 사용하세요. hello 예를 들면의 `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>패턴  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>설명
  
`<pattern>`은 문자열로 평가할 식이어야 합니다. LIKE 연산자 hello에 대 한 패턴으로 사용 됩니다.      Hello 와일드 카드 문자를 포함할 수 있습니다.  
  
-   `%`: 0개 이상의 문자입니다.  
  
-   `_`: 단일 문자입니다.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>설명  

`<escape_char>`은 길이가 1인 문자열로 평가할 식이어야 합니다. LIKE 연산자 hello에 대 한 이스케이프 문자로 사용 됩니다.  
  
 예를 들어 `property LIKE 'ABC\%' ESCAPE '\'`는 `ABC`로 시작되는 문자열 대신 `ABC%`와 일치합니다.  
  
## <a name="constant"></a>constant  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>인수  
  
-   `<integer_constant>`는 따옴표로 묶이지 않고 소수점을 포함하지 않는 숫자의 문자열입니다. hello 값으로 저장 됩니다 `System.Int64` 내부적으로 다음과 같은 hello 및 범위입니다.  
  
     다음은 long 상수에 대한 예입니다.  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>`는 따옴표로 묶이지 않고 소수점을 포함하는 숫자의 문자열입니다. hello 값으로 저장 됩니다 `System.Double` 내부적으로 hello 같은 범위/정밀도 따라 합니다.  
  
     이후 버전에서이 번호는 다른 데이터 형식 toosupport 정확한 숫자 의미 체계에 저장 될 수 있습니다, 데이터 형식이 hello 팩트 hello 기본 의존 해야 하므로 `System.Double` 에 대 한 `<decimal_constant>`합니다.  
  
     hello 다음은 10 진수 상수의 예입니다.  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>`는 과학적 표기법으로 작성된 숫자입니다. hello 값으로 저장 됩니다 `System.Double` 내부적으로 hello 같은 범위/정밀도 따라 합니다. hello 다음은 근사 숫자 상수의 예입니다.  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>설명  

부울 상수는 hello 키워드로 표시 **TRUE** 또는 **FALSE**합니다. hello 값으로 저장 됩니다 `System.Boolean`합니다.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>설명  

문자열 상수는 작은따옴표로 묶으며 유효한 유니코드 문자를 포함합니다. 문자열 상수에 포함된 작은따옴표는 두 개의 작은따옴표로 표시됩니다.  
  
## <a name="function"></a>함수  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>설명
  
hello `newid()` 함수에서 반환 된 **System.Guid** hello에 의해 생성 된 `System.Guid.NewGuid()` 메서드.  
  
hello `property(name)` 함수에서 참조 하는 hello 속성의 hello 값을 반환 `name`합니다. hello `name` 값일 수는 문자열 값을 반환 하는 모든 유효한 식입니다.  
  
## <a name="considerations"></a>고려 사항
  
Hello 다음 사항을 고려 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 의미 체계:  
  
-   속성 이름은 대/소문자를 구분하지 않습니다.  
  
-   연산자는 가능하면 C# 암시적 변환 의미 체계를 따릅니다.  
  
-   시스템 속성은 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 인스턴스에서 노출되는 공용 속성입니다.  
  
    Hello 다음 사항을 고려 `IS [NOT] NULL` 의미 체계:  
  
    -   `property IS NULL`로 평가 `true` hello 속성 중 하나가 존재 하지 못하거나 hello 속성의 값은 `null`합니다.  
  
### <a name="property-evaluation-semantics"></a>속성 평가 의미 체계  
  
-   존재 하지 않는 시스템 속성에서 throw 하는 시도 tooevaluate는 [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) 예외입니다.  
  
-   존재하지 않는 속성은 내부적으로 **알 수 없음**으로 평가됩니다.  
  
 알 수 없음 평가는 산술 연산자입니다.  
  
-   이항 연산자에 대 한 왼쪽 이나 오른쪽 피연산자의 hello 하나으로 평가 됩니다 **알 수 없는**, hello 결과 **알 수 없는**합니다.  
  
-   단항 연산자의 피연산자도 확인 될 경우 **알 수 없는**, hello 결과 **알 수 없는**합니다.  
  
 알 수 없음 평가는 이항 비교 연산자입니다.  
  
-   왼쪽 이나 오른쪽 피연산자의 hello 하나으로 평가 됩니다 **알 수 없는**, hello 결과 **알 수 없는**합니다.  
  
 `[NOT] LIKE`에서 알 수 없음 평가:  
  
-   모든 피연산자도 확인 될 경우 **알 수 없는**, hello 결과 **알 수 없는**합니다.  
  
 `[NOT] IN`에서 알 수 없음 평가:  
  
-   왼쪽 피연산자 hello로 평가 되는 경우 **알 수 없는**, hello 결과 **알 수 없는**합니다.  
  
 **AND** 연산자에서 알 수 없음 평가:  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 **OR** 연산자에서 알 수 없음 평가:  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a>연산자 바인딩 의미 체계
  
-   비교 연산자와 같은 `>`, `>=`, `<`, `<=`, `!=`, 및 `=` 따라 hello 동일한 데이터에서 바인딩 hello C# 연산자와 의미 체계 형식 승격 및 암시적 변환 합니다.  
  
-   산술 연산자와 같은 `+`, `-`, `*`, `/`, 및 `%` 따라 hello 동일한 데이터에서 바인딩 hello C# 연산자와 의미 체계 형식 승격 및 암시적 변환 합니다.

## <a name="next-steps"></a>다음 단계

- [SQLFilter 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [SQLRuleAction 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)