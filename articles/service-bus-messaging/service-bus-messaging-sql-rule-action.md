---
title: "Azure에서 aaaSQLRuleAction 구문 참조 | Microsoft Docs"
description: "SQLRuleAction 문법에 대한 세부 정보입니다."
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a>SQLRuleAction 구문

A *SqlRuleAction* hello의 인스턴스가 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 클래스 및 나타내는 일련의 SQL 언어로 작성 된 작업 기반 구문에 대해 수행 되는 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
이 항목에서는 SQL 규칙 동작 문법 hello에 대 한 세부 정보를 나열 합니다.  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
### <a name="remarks"></a>설명  

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
  
 따라서 문자로 시작하고 뒤에 하나 이상의 밑줄/문자/숫자가 나오는 문자열입니다.  
  
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
  
     hello 다음은 긴 상수의 예입니다.  
  
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
  
부울 상수는 hello 키워드로 표시 `TRUE` 또는 `FALSE`합니다. hello 값으로 저장 됩니다 `System.Boolean`합니다.  
  
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

- 집합은 사용 되는 toocreate 기존 속성의 새 속성이 나 업데이트 hello 값입니다.
- 제거에 사용 되는 tooremove 속성입니다.
- Hello 식 형식 및 hello 기존 속성 유형 서로 암시적으로 변환 가능 하면 수행 설정 합니다.
- 존재하지 않는 시스템 속성을 참조하면 작업에 실패합니다.
- 존재하지 않는 사용자 속성을 참조하면 작업에 실패하지 않습니다.
- 존재 하지 않는 사용자 속성이 "알 수 없음"으로 내부적으로 확인, 다음 hello 동일한 의미 체계 [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 연산자를 평가할 때.

## <a name="next-steps"></a>다음 단계

- [SQLRuleAction 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [SQLFilter 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
