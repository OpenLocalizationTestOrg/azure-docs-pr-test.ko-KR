---
title: "Azure Service Bus SQLFilter 구문 참조 | Microsoft Docs"
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="2fed1-103">SQLFilter 구문</span><span class="sxs-lookup"><span data-stu-id="2fed1-103">SQLFilter syntax</span></span>

<span data-ttu-id="2fed1-104">*SqlFilter*는 [SqlFilter 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)의 인스턴스이며 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)에 대해 평가되는 SQL 언어 기반 필터 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="2fed1-105">SqlFilter는 SQL-92 표준의 하위 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="2fed1-106">이 항목에서는 SqlFilter 문법에 대한 세부 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="2fed1-107">인수</span><span class="sxs-lookup"><span data-stu-id="2fed1-107">Arguments</span></span>  
  
-   <span data-ttu-id="2fed1-108">`<scope>`는 `<property_name>`의 범위를 나타내는 선택적 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="2fed1-109">유효한 값은 `sys` 또는 `user`입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="2fed1-110">`sys` 값은 `<property_name>`이 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)의 공용 속성 이름인 시스템 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="2fed1-111">`user`는 `<property_name>`이 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 사전의 키인 사용자 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="2fed1-112">`<scope>`가 지정되지 않은 경우 `user` 범위가 기본 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2fed1-113">설명</span><span class="sxs-lookup"><span data-stu-id="2fed1-113">Remarks</span></span>

<span data-ttu-id="2fed1-114">존재하지 않는 시스템 속성에 대한 액세스 시도는 오류이지만 존재하지 않는 사용자 속성에 대한 액세스 시도는 오류가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="2fed1-115">대신, 존재하지 않는 사용자 속성은 알 수 없는 값;으로 내부적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="2fed1-116">알 수 없는 값은 연산자 평가 중에 특별히 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="2fed1-117">property_name</span><span class="sxs-lookup"><span data-stu-id="2fed1-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="2fed1-118">인수</span><span class="sxs-lookup"><span data-stu-id="2fed1-118">Arguments</span></span>  

 <span data-ttu-id="2fed1-119">`<regular_identifier>`는 다음 정규식으로 표현되는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="2fed1-120">이 문법은 문자로 시작하고 뒤에 하나 이상의 밑줄/문자/숫자가 나오는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="2fed1-121">`[:IsLetter:]`는 유니코드 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="2fed1-122">`System.Char.IsLetter(c)`에서는 `c`가 유니코드 문자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="2fed1-123">`[:IsDigit:]`는 10진수 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="2fed1-124">`System.Char.IsDigit(c)`에서는 `c`가 유니코드 숫자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="2fed1-125">`<regular_identifier>`는 예약된 키워드일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="2fed1-126">`<delimited_identifier>`는 왼쪽/오른쪽 대괄호([])로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="2fed1-127">오른쪽 대괄호는 두 개의 오른쪽 대괄호로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="2fed1-128">다음은 `<delimited_identifier>`에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="2fed1-129">`<quoted_identifier>`는 큰따옴표로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="2fed1-130">식별자에서 큰따옴표는 두 개의 큰따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="2fed1-131">문자열 상수와 혼동될 수 있으므로 따옴표가 있는 식별자를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="2fed1-132">가능하면 구분된 식별자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2fed1-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="2fed1-133">다음은 `<quoted_identifier>`의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="2fed1-134">패턴</span><span class="sxs-lookup"><span data-stu-id="2fed1-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="2fed1-135">설명</span><span class="sxs-lookup"><span data-stu-id="2fed1-135">Remarks</span></span>
  
<span data-ttu-id="2fed1-136">`<pattern>`은 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="2fed1-137">LIKE 연산자에 대한 패턴으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="2fed1-138">다음 와일드 카드 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="2fed1-139">`%`: 0개 이상의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="2fed1-140">`_`: 단일 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="2fed1-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="2fed1-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="2fed1-142">설명</span><span class="sxs-lookup"><span data-stu-id="2fed1-142">Remarks</span></span>  

<span data-ttu-id="2fed1-143">`<escape_char>`은 길이가 1인 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="2fed1-144">LIKE 연산자에 대한 이스케이프 문자로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="2fed1-145">예를 들어 `property LIKE 'ABC\%' ESCAPE '\'`는 `ABC`로 시작되는 문자열 대신 `ABC%`와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="2fed1-146">constant</span><span class="sxs-lookup"><span data-stu-id="2fed1-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="2fed1-147">인수</span><span class="sxs-lookup"><span data-stu-id="2fed1-147">Arguments</span></span>  
  
-   <span data-ttu-id="2fed1-148">`<integer_constant>`는 따옴표로 묶이지 않고 소수점을 포함하지 않는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="2fed1-149">값은 내부적으로는 `System.Int64`로 저장되며 동일한 범위를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="2fed1-150">다음은 long 상수에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="2fed1-151">`<decimal_constant>`는 따옴표로 묶이지 않고 소수점을 포함하는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="2fed1-152">값은 내부적으로는 `System.Double`로 저장되며 동일한 범위/자릿수를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="2fed1-153">이후 버전에서는 이 숫자가 정확한 숫자 의미 체계를 지원하기 위해 다른 데이터 형식으로 저장될 수 있으므로 `<decimal_constant>`에 대한 기본 데이터 형식이 `System.Double`이라는 사실이 해당되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="2fed1-154">다음은 10진수 상수에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="2fed1-155">`<approximate_number_constant>`는 과학적 표기법으로 작성된 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="2fed1-156">값은 내부적으로는 `System.Double`로 저장되며 동일한 범위/자릿수를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="2fed1-157">다음은 대략적인 숫자 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="2fed1-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="2fed1-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="2fed1-159">설명</span><span class="sxs-lookup"><span data-stu-id="2fed1-159">Remarks</span></span>  

<span data-ttu-id="2fed1-160">Boolean 상수는 **TRUE** 또는 **FALSE** 키워드로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="2fed1-161">값은 `System.Boolean`으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="2fed1-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="2fed1-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="2fed1-163">설명</span><span class="sxs-lookup"><span data-stu-id="2fed1-163">Remarks</span></span>  

<span data-ttu-id="2fed1-164">문자열 상수는 작은따옴표로 묶으며 유효한 유니코드 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="2fed1-165">문자열 상수에 포함된 작은따옴표는 두 개의 작은따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="2fed1-166">함수</span><span class="sxs-lookup"><span data-stu-id="2fed1-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="2fed1-167">설명</span><span class="sxs-lookup"><span data-stu-id="2fed1-167">Remarks</span></span>
  
<span data-ttu-id="2fed1-168">`newid()` 함수는 `System.Guid.NewGuid()` 메서드에 의해 생성된 **System.Guid**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="2fed1-169">`property(name)` 함수는 `name`으로 참조되는 속성 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="2fed1-170">`name` 값은 문자열 값을 반환하는 유효한 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="2fed1-171">고려 사항</span><span class="sxs-lookup"><span data-stu-id="2fed1-171">Considerations</span></span>
  
<span data-ttu-id="2fed1-172">다음과 같은 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 의미 체계를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2fed1-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="2fed1-173">속성 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="2fed1-174">연산자는 가능하면 C# 암시적 변환 의미 체계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="2fed1-175">시스템 속성은 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 인스턴스에서 노출되는 공용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="2fed1-176">다음 `IS [NOT] NULL` 의미 체계를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2fed1-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="2fed1-177">속성이 존재하지 않거나 속성 값이 `null`인 경우 `property IS NULL`은 `true`로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="2fed1-178">속성 평가 의미 체계</span><span class="sxs-lookup"><span data-stu-id="2fed1-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="2fed1-179">존재하지 않는 시스템 속성을 평가하려고 시도하면 [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="2fed1-180">존재하지 않는 속성은 내부적으로 **알 수 없음**으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="2fed1-181">알 수 없음 평가는 산술 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="2fed1-182">이항 연산자의 경우 왼쪽 및/또는 오른쪽 피연산자 중 하나가 **알 수 없음**으로 평가되는 경우 결과는 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="2fed1-183">단항 연산자의 경우 피연산자가 **알 수 없음**으로 평가되는 경우 결과는 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="2fed1-184">알 수 없음 평가는 이항 비교 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="2fed1-185">왼쪽 및/또는 오른쪽 피연산자 중 하나가 **알 수 없음**으로 평가되는 경우 결과는 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="2fed1-186">`[NOT] LIKE`에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="2fed1-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="2fed1-187">피연산자가 **알 수 없음**으로 평가되는 경우 결과는 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="2fed1-188">`[NOT] IN`에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="2fed1-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="2fed1-189">왼쪽 피연산자가 **알 수 없음**으로 평가되는 경우 결과는 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="2fed1-190">**AND** 연산자에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="2fed1-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="2fed1-191">**OR** 연산자에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="2fed1-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="2fed1-192">연산자 바인딩 의미 체계</span><span class="sxs-lookup"><span data-stu-id="2fed1-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="2fed1-193">`>`, `>=`, `<`, `<=`, `!=`, `=`과 같은 비교 연산자는 데이터 형식 승격 및 암시적 변환에서 C# 연산자 바인딩과 동일한 의미 체계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="2fed1-194">`+`, `-`, `*`, `/`, `%`와 같은 산술 연산자는 데이터 형식 승격 및 암시적 변환에서 C# 연산자 바인딩과 동일한 의미 체계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fed1-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fed1-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2fed1-195">Next steps</span></span>

- [<span data-ttu-id="2fed1-196">SQLFilter 클래스</span><span class="sxs-lookup"><span data-stu-id="2fed1-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="2fed1-197">SQLRuleAction 클래스</span><span class="sxs-lookup"><span data-stu-id="2fed1-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)