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
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="ef658-103">SQLRuleAction 구문</span><span class="sxs-lookup"><span data-stu-id="ef658-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="ef658-104">A *SqlRuleAction* hello의 인스턴스가 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 클래스 및 나타내는 일련의 SQL 언어로 작성 된 작업 기반 구문에 대해 수행 되는 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="ef658-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="ef658-105">이 항목에서는 SQL 규칙 동작 문법 hello에 대 한 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="ef658-106">인수</span><span class="sxs-lookup"><span data-stu-id="ef658-106">Arguments</span></span>  
  
-   <span data-ttu-id="ef658-107">`<scope>`속성은 hello hello 범위를 나타내는 선택적 문자열 `<property_name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="ef658-108">유효한 값은 `sys` 또는 `user`입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="ef658-109">hello `sys` 값 시스템 범위를 나타냅니다. 여기서 `<property_name>` hello의 공용 속성 이름인 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="ef658-110">`user`사용자 범위를 나타냅니다. 여기서 `<property_name>` hello의 키가 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="ef658-111">`user`범위 경우 hello 기본 범위는 `<scope>` 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="ef658-112">설명</span><span class="sxs-lookup"><span data-stu-id="ef658-112">Remarks</span></span>  

<span data-ttu-id="ef658-113">시도 tooaccess 존재 하지 않는 시스템 속성 있고 오류가 시도 tooaccess 존재 하지 사용자 속성은 오류가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="ef658-114">대신, 존재하지 않는 사용자 속성은 알 수 없는 값;으로 내부적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="ef658-115">알 수 없는 값은 연산자 평가 중에 특별히 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="ef658-116">property_name</span><span class="sxs-lookup"><span data-stu-id="ef658-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="ef658-117">인수</span><span class="sxs-lookup"><span data-stu-id="ef658-117">Arguments</span></span>  
 <span data-ttu-id="ef658-118">`<regular_identifier>`hello 표시 되는 문자열은 정규식을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="ef658-119">따라서 문자로 시작하고 뒤에 하나 이상의 밑줄/문자/숫자가 나오는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="ef658-120">`[:IsLetter:]`는 유니코드 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="ef658-121">`System.Char.IsLetter(c)`에서는 `c`가 유니코드 문자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="ef658-122">`[:IsDigit:]`는 10진수 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="ef658-123">`System.Char.IsDigit(c)`에서는 `c`가 유니코드 숫자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="ef658-124">`<regular_identifier>`는 예약된 키워드일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="ef658-125">`<delimited_identifier>`는 왼쪽/오른쪽 대괄호([])로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="ef658-126">오른쪽 대괄호는 두 개의 오른쪽 대괄호로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="ef658-127">hello 다음은 몇 가지 `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="ef658-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="ef658-128">`<quoted_identifier>`는 큰따옴표로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="ef658-129">식별자에서 큰따옴표는 두 개의 큰따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="ef658-130">Toouse 따옴표 붙은 식별자는 문자열 상수과 쉽게 혼동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="ef658-131">가능하면 구분된 식별자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ef658-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="ef658-132">hello 예를 들면의 `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="ef658-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="ef658-133">패턴</span><span class="sxs-lookup"><span data-stu-id="ef658-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="ef658-134">설명</span><span class="sxs-lookup"><span data-stu-id="ef658-134">Remarks</span></span>
  
 <span data-ttu-id="ef658-135">`<pattern>`은 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="ef658-136">LIKE 연산자 hello에 대 한 패턴으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="ef658-137">Hello 와일드 카드 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="ef658-138">`%`: 0개 이상의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="ef658-139">`_`: 단일 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="ef658-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="ef658-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="ef658-141">설명</span><span class="sxs-lookup"><span data-stu-id="ef658-141">Remarks</span></span>
  
 <span data-ttu-id="ef658-142">`<escape_char>`은 길이가 1인 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="ef658-143">LIKE 연산자 hello에 대 한 이스케이프 문자로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="ef658-144">예를 들어 `property LIKE 'ABC\%' ESCAPE '\'`는 `ABC`로 시작되는 문자열 대신 `ABC%`와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="ef658-145">constant</span><span class="sxs-lookup"><span data-stu-id="ef658-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="ef658-146">인수</span><span class="sxs-lookup"><span data-stu-id="ef658-146">Arguments</span></span>  
  
-   <span data-ttu-id="ef658-147">`<integer_constant>`는 따옴표로 묶이지 않고 소수점을 포함하지 않는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="ef658-148">hello 값으로 저장 됩니다 `System.Int64` 내부적으로 다음과 같은 hello 및 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="ef658-149">hello 다음은 긴 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="ef658-150">`<decimal_constant>`는 따옴표로 묶이지 않고 소수점을 포함하는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="ef658-151">hello 값으로 저장 됩니다 `System.Double` 내부적으로 hello 같은 범위/정밀도 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="ef658-152">이후 버전에서이 번호는 다른 데이터 형식 toosupport 정확한 숫자 의미 체계에 저장 될 수 있습니다, 데이터 형식이 hello 팩트 hello 기본 의존 해야 하므로 `System.Double` 에 대 한 `<decimal_constant>`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="ef658-153">hello 다음은 10 진수 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="ef658-154">`<approximate_number_constant>`는 과학적 표기법으로 작성된 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="ef658-155">hello 값으로 저장 됩니다 `System.Double` 내부적으로 hello 같은 범위/정밀도 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="ef658-156">hello 다음은 근사 숫자 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="ef658-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="ef658-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="ef658-158">설명</span><span class="sxs-lookup"><span data-stu-id="ef658-158">Remarks</span></span>
  
<span data-ttu-id="ef658-159">부울 상수는 hello 키워드로 표시 `TRUE` 또는 `FALSE`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="ef658-160">hello 값으로 저장 됩니다 `System.Boolean`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="ef658-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="ef658-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="ef658-162">설명</span><span class="sxs-lookup"><span data-stu-id="ef658-162">Remarks</span></span>
  
<span data-ttu-id="ef658-163">문자열 상수는 작은따옴표로 묶으며 유효한 유니코드 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="ef658-164">문자열 상수에 포함된 작은따옴표는 두 개의 작은따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="ef658-165">함수</span><span class="sxs-lookup"><span data-stu-id="ef658-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="ef658-166">설명</span><span class="sxs-lookup"><span data-stu-id="ef658-166">Remarks</span></span>  

<span data-ttu-id="ef658-167">hello `newid()` 함수에서 반환 된 **System.Guid** hello에 의해 생성 된 `System.Guid.NewGuid()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ef658-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="ef658-168">hello `property(name)` 함수에서 참조 하는 hello 속성의 hello 값을 반환 `name`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="ef658-169">hello `name` 값일 수는 문자열 값을 반환 하는 모든 유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="ef658-170">고려 사항</span><span class="sxs-lookup"><span data-stu-id="ef658-170">Considerations</span></span>

- <span data-ttu-id="ef658-171">집합은 사용 되는 toocreate 기존 속성의 새 속성이 나 업데이트 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="ef658-172">제거에 사용 되는 tooremove 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="ef658-173">Hello 식 형식 및 hello 기존 속성 유형 서로 암시적으로 변환 가능 하면 수행 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="ef658-174">존재하지 않는 시스템 속성을 참조하면 작업에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="ef658-175">존재하지 않는 사용자 속성을 참조하면 작업에 실패하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef658-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="ef658-176">존재 하지 않는 사용자 속성이 "알 수 없음"으로 내부적으로 확인, 다음 hello 동일한 의미 체계 [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 연산자를 평가할 때.</span><span class="sxs-lookup"><span data-stu-id="ef658-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef658-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef658-177">Next steps</span></span>

- [<span data-ttu-id="ef658-178">SQLRuleAction 클래스</span><span class="sxs-lookup"><span data-stu-id="ef658-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="ef658-179">SQLFilter 클래스</span><span class="sxs-lookup"><span data-stu-id="ef658-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
