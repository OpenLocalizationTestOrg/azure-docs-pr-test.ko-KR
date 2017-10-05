---
title: "Azure에서 SQLRuleAction 구문 참조 | Microsoft Docs"
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
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="6909d-103">SQLRuleAction 구문</span><span class="sxs-lookup"><span data-stu-id="6909d-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="6909d-104">*SqlRuleAction*은 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 클래스의 인스턴스이며 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)에 대해 수행된SQL 언어 기반 구문으로 작성된 일련의 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="6909d-105">이 항목에서는 SQL 규칙 동작 문법에 대한 세부 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="6909d-106">인수</span><span class="sxs-lookup"><span data-stu-id="6909d-106">Arguments</span></span>  
  
-   <span data-ttu-id="6909d-107">`<scope>`는 `<property_name>`의 범위를 나타내는 선택적 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="6909d-108">유효한 값은 `sys` 또는 `user`입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="6909d-109">`sys` 값은 `<property_name>`이 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)의 공용 속성 이름인 시스템 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="6909d-110">`user`는 `<property_name>`이 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 사전의 키인 사용자 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="6909d-111">`<scope>`가 지정되지 않은 경우 `user` 범위가 기본 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="6909d-112">설명</span><span class="sxs-lookup"><span data-stu-id="6909d-112">Remarks</span></span>  

<span data-ttu-id="6909d-113">존재하지 않는 시스템 속성에 대한 액세스 시도는 오류이지만 존재하지 않는 사용자 속성에 대한 액세스 시도는 오류가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="6909d-114">대신, 존재하지 않는 사용자 속성은 알 수 없는 값;으로 내부적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="6909d-115">알 수 없는 값은 연산자 평가 중에 특별히 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="6909d-116">property_name</span><span class="sxs-lookup"><span data-stu-id="6909d-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="6909d-117">인수</span><span class="sxs-lookup"><span data-stu-id="6909d-117">Arguments</span></span>  
 <span data-ttu-id="6909d-118">`<regular_identifier>`는 다음 정규식으로 표현되는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="6909d-119">따라서 문자로 시작하고 뒤에 하나 이상의 밑줄/문자/숫자가 나오는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="6909d-120">`[:IsLetter:]`는 유니코드 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="6909d-121">`System.Char.IsLetter(c)`에서는 `c`가 유니코드 문자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="6909d-122">`[:IsDigit:]`는 10진수 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="6909d-123">`System.Char.IsDigit(c)`에서는 `c`가 유니코드 숫자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="6909d-124">`<regular_identifier>`는 예약된 키워드일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="6909d-125">`<delimited_identifier>`는 왼쪽/오른쪽 대괄호([])로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="6909d-126">오른쪽 대괄호는 두 개의 오른쪽 대괄호로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="6909d-127">다음은 `<delimited_identifier>`에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="6909d-128">`<quoted_identifier>`는 큰따옴표로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="6909d-129">식별자에서 큰따옴표는 두 개의 큰따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="6909d-130">문자열 상수와 혼동될 수 있으므로 따옴표가 있는 식별자를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="6909d-131">가능하면 구분된 식별자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6909d-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="6909d-132">다음은 `<quoted_identifier>`의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="6909d-133">패턴</span><span class="sxs-lookup"><span data-stu-id="6909d-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="6909d-134">설명</span><span class="sxs-lookup"><span data-stu-id="6909d-134">Remarks</span></span>
  
 <span data-ttu-id="6909d-135">`<pattern>`은 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="6909d-136">LIKE 연산자에 대한 패턴으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="6909d-137">다음 와일드 카드 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="6909d-138">`%`: 0개 이상의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="6909d-139">`_`: 단일 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="6909d-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="6909d-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="6909d-141">설명</span><span class="sxs-lookup"><span data-stu-id="6909d-141">Remarks</span></span>
  
 <span data-ttu-id="6909d-142">`<escape_char>`은 길이가 1인 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="6909d-143">LIKE 연산자에 대한 이스케이프 문자로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="6909d-144">예를 들어 `property LIKE 'ABC\%' ESCAPE '\'`는 `ABC`로 시작되는 문자열 대신 `ABC%`와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="6909d-145">constant</span><span class="sxs-lookup"><span data-stu-id="6909d-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="6909d-146">인수</span><span class="sxs-lookup"><span data-stu-id="6909d-146">Arguments</span></span>  
  
-   <span data-ttu-id="6909d-147">`<integer_constant>`는 따옴표로 묶이지 않고 소수점을 포함하지 않는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="6909d-148">값은 내부적으로는 `System.Int64`로 저장되며 동일한 범위를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="6909d-149">다음은 long 상수에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="6909d-150">`<decimal_constant>`는 따옴표로 묶이지 않고 소수점을 포함하는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="6909d-151">값은 내부적으로는 `System.Double`로 저장되며 동일한 범위/자릿수를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="6909d-152">이후 버전에서는 이 숫자가 정확한 숫자 의미 체계를 지원하기 위해 다른 데이터 형식으로 저장될 수 있으므로 `<decimal_constant>`에 대한 기본 데이터 형식이 `System.Double`이라는 사실이 해당되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="6909d-153">다음은 10진수 상수에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="6909d-154">`<approximate_number_constant>`는 과학적 표기법으로 작성된 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="6909d-155">값은 내부적으로는 `System.Double`로 저장되며 동일한 범위/자릿수를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="6909d-156">다음은 대략적인 숫자 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="6909d-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="6909d-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="6909d-158">설명</span><span class="sxs-lookup"><span data-stu-id="6909d-158">Remarks</span></span>
  
<span data-ttu-id="6909d-159">Boolean 상수는 `TRUE` 또는 `FALSE` 키워드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="6909d-160">값은 `System.Boolean`으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="6909d-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="6909d-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="6909d-162">설명</span><span class="sxs-lookup"><span data-stu-id="6909d-162">Remarks</span></span>
  
<span data-ttu-id="6909d-163">문자열 상수는 작은따옴표로 묶으며 유효한 유니코드 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="6909d-164">문자열 상수에 포함된 작은따옴표는 두 개의 작은따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="6909d-165">함수</span><span class="sxs-lookup"><span data-stu-id="6909d-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="6909d-166">설명</span><span class="sxs-lookup"><span data-stu-id="6909d-166">Remarks</span></span>  

<span data-ttu-id="6909d-167">`newid()` 함수는 `System.Guid.NewGuid()` 메서드에 의해 생성된 **System.Guid**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="6909d-168">`property(name)` 함수는 `name`으로 참조되는 속성 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="6909d-169">`name` 값은 문자열 값을 반환하는 유효한 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="6909d-170">고려 사항</span><span class="sxs-lookup"><span data-stu-id="6909d-170">Considerations</span></span>

- <span data-ttu-id="6909d-171">SET은 새 속성을 만들고 기존 속성의 값을 업데이트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="6909d-172">REMOVE는 속성을 제거하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="6909d-173">SET은 식 형식과 기존 속성 형식이 다른 경우 암시적 변환을 수행합니다(가능한 경우).</span><span class="sxs-lookup"><span data-stu-id="6909d-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="6909d-174">존재하지 않는 시스템 속성을 참조하면 작업에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="6909d-175">존재하지 않는 사용자 속성을 참조하면 작업에 실패하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="6909d-176">연산자를 평가할 때 [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)와 동일한 의미 체계에 따라 존재하지 않는 사용자 속성이 내부적으로 "알 수 없음"으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6909d-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6909d-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6909d-177">Next steps</span></span>

- [<span data-ttu-id="6909d-178">SQLRuleAction 클래스</span><span class="sxs-lookup"><span data-stu-id="6909d-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="6909d-179">SQLFilter 클래스</span><span class="sxs-lookup"><span data-stu-id="6909d-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
