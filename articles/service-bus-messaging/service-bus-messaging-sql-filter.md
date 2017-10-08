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
# <a name="sqlfilter-syntax"></a><span data-ttu-id="951af-103">SQLFilter 구문</span><span class="sxs-lookup"><span data-stu-id="951af-103">SQLFilter syntax</span></span>

<span data-ttu-id="951af-104">A *SqlFilter* hello의 인스턴스가 [SqlFilter 클래스](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)에 대해 평가 되는 SQL 언어 기반 필터 식을 나타냅니다는 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="951af-105">SqlFilter hello sql-92 표준의 하위 집합을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="951af-106">이 항목에서는 SqlFilter 문법에 대한 세부 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="951af-107">인수</span><span class="sxs-lookup"><span data-stu-id="951af-107">Arguments</span></span>  
  
-   <span data-ttu-id="951af-108">`<scope>`속성은 hello hello 범위를 나타내는 선택적 문자열 `<property_name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="951af-109">유효한 값은 `sys` 또는 `user`입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="951af-110">hello `sys` 값 시스템 범위를 나타냅니다. 여기서 `<property_name>` hello의 공용 속성 이름인 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="951af-111">`user`사용자 범위를 나타냅니다. 여기서 `<property_name>` hello의 키가 [BrokeredMessage 클래스](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="951af-112">`user`범위 경우 hello 기본 범위는 `<scope>` 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="951af-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="951af-113">설명</span><span class="sxs-lookup"><span data-stu-id="951af-113">Remarks</span></span>

<span data-ttu-id="951af-114">시도 tooaccess 존재 하지 않는 시스템 속성 있고 오류가 시도 tooaccess 존재 하지 사용자 속성은 오류가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="951af-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="951af-115">대신, 존재하지 않는 사용자 속성은 알 수 없는 값;으로 내부적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="951af-116">알 수 없는 값은 연산자 평가 중에 특별히 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="951af-117">property_name</span><span class="sxs-lookup"><span data-stu-id="951af-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="951af-118">인수</span><span class="sxs-lookup"><span data-stu-id="951af-118">Arguments</span></span>  

 <span data-ttu-id="951af-119">`<regular_identifier>`hello 표시 되는 문자열은 정규식을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="951af-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="951af-120">이 문법은 문자로 시작하고 뒤에 하나 이상의 밑줄/문자/숫자가 나오는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="951af-121">`[:IsLetter:]`는 유니코드 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="951af-122">`System.Char.IsLetter(c)`에서는 `c`가 유니코드 문자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="951af-123">`[:IsDigit:]`는 10진수 문자로 분류된 유니코드 문자를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="951af-124">`System.Char.IsDigit(c)`에서는 `c`가 유니코드 숫자인 경우 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="951af-125">`<regular_identifier>`는 예약된 키워드일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="951af-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="951af-126">`<delimited_identifier>`는 왼쪽/오른쪽 대괄호([])로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="951af-127">오른쪽 대괄호는 두 개의 오른쪽 대괄호로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="951af-128">hello 다음은 몇 가지 `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="951af-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="951af-129">`<quoted_identifier>`는 큰따옴표로 묶인 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="951af-130">식별자에서 큰따옴표는 두 개의 큰따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="951af-131">Toouse 따옴표 붙은 식별자는 문자열 상수과 쉽게 혼동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="951af-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="951af-132">가능하면 구분된 식별자를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="951af-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="951af-133">hello 예를 들면의 `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="951af-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="951af-134">패턴</span><span class="sxs-lookup"><span data-stu-id="951af-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="951af-135">설명</span><span class="sxs-lookup"><span data-stu-id="951af-135">Remarks</span></span>
  
<span data-ttu-id="951af-136">`<pattern>`은 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="951af-137">LIKE 연산자 hello에 대 한 패턴으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="951af-138">Hello 와일드 카드 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="951af-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="951af-139">`%`: 0개 이상의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="951af-140">`_`: 단일 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="951af-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="951af-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="951af-142">설명</span><span class="sxs-lookup"><span data-stu-id="951af-142">Remarks</span></span>  

<span data-ttu-id="951af-143">`<escape_char>`은 길이가 1인 문자열로 평가할 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="951af-144">LIKE 연산자 hello에 대 한 이스케이프 문자로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="951af-145">예를 들어 `property LIKE 'ABC\%' ESCAPE '\'`는 `ABC`로 시작되는 문자열 대신 `ABC%`와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="951af-146">constant</span><span class="sxs-lookup"><span data-stu-id="951af-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="951af-147">인수</span><span class="sxs-lookup"><span data-stu-id="951af-147">Arguments</span></span>  
  
-   <span data-ttu-id="951af-148">`<integer_constant>`는 따옴표로 묶이지 않고 소수점을 포함하지 않는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="951af-149">hello 값으로 저장 됩니다 `System.Int64` 내부적으로 다음과 같은 hello 및 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="951af-150">다음은 long 상수에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="951af-151">`<decimal_constant>`는 따옴표로 묶이지 않고 소수점을 포함하는 숫자의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="951af-152">hello 값으로 저장 됩니다 `System.Double` 내부적으로 hello 같은 범위/정밀도 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="951af-153">이후 버전에서이 번호는 다른 데이터 형식 toosupport 정확한 숫자 의미 체계에 저장 될 수 있습니다, 데이터 형식이 hello 팩트 hello 기본 의존 해야 하므로 `System.Double` 에 대 한 `<decimal_constant>`합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="951af-154">hello 다음은 10 진수 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="951af-155">`<approximate_number_constant>`는 과학적 표기법으로 작성된 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="951af-156">hello 값으로 저장 됩니다 `System.Double` 내부적으로 hello 같은 범위/정밀도 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="951af-157">hello 다음은 근사 숫자 상수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="951af-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="951af-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="951af-159">설명</span><span class="sxs-lookup"><span data-stu-id="951af-159">Remarks</span></span>  

<span data-ttu-id="951af-160">부울 상수는 hello 키워드로 표시 **TRUE** 또는 **FALSE**합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="951af-161">hello 값으로 저장 됩니다 `System.Boolean`합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="951af-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="951af-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="951af-163">설명</span><span class="sxs-lookup"><span data-stu-id="951af-163">Remarks</span></span>  

<span data-ttu-id="951af-164">문자열 상수는 작은따옴표로 묶으며 유효한 유니코드 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="951af-165">문자열 상수에 포함된 작은따옴표는 두 개의 작은따옴표로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="951af-166">함수</span><span class="sxs-lookup"><span data-stu-id="951af-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="951af-167">설명</span><span class="sxs-lookup"><span data-stu-id="951af-167">Remarks</span></span>
  
<span data-ttu-id="951af-168">hello `newid()` 함수에서 반환 된 **System.Guid** hello에 의해 생성 된 `System.Guid.NewGuid()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="951af-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="951af-169">hello `property(name)` 함수에서 참조 하는 hello 속성의 hello 값을 반환 `name`합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="951af-170">hello `name` 값일 수는 문자열 값을 반환 하는 모든 유효한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="951af-171">고려 사항</span><span class="sxs-lookup"><span data-stu-id="951af-171">Considerations</span></span>
  
<span data-ttu-id="951af-172">Hello 다음 사항을 고려 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 의미 체계:</span><span class="sxs-lookup"><span data-stu-id="951af-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="951af-173">속성 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="951af-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="951af-174">연산자는 가능하면 C# 암시적 변환 의미 체계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="951af-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="951af-175">시스템 속성은 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 인스턴스에서 노출되는 공용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="951af-176">Hello 다음 사항을 고려 `IS [NOT] NULL` 의미 체계:</span><span class="sxs-lookup"><span data-stu-id="951af-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="951af-177">`property IS NULL`로 평가 `true` hello 속성 중 하나가 존재 하지 못하거나 hello 속성의 값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="951af-178">속성 평가 의미 체계</span><span class="sxs-lookup"><span data-stu-id="951af-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="951af-179">존재 하지 않는 시스템 속성에서 throw 하는 시도 tooevaluate는 [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="951af-180">존재하지 않는 속성은 내부적으로 **알 수 없음**으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="951af-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="951af-181">알 수 없음 평가는 산술 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="951af-182">이항 연산자에 대 한 왼쪽 이나 오른쪽 피연산자의 hello 하나으로 평가 됩니다 **알 수 없는**, hello 결과 **알 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="951af-183">단항 연산자의 피연산자도 확인 될 경우 **알 수 없는**, hello 결과 **알 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="951af-184">알 수 없음 평가는 이항 비교 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="951af-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="951af-185">왼쪽 이나 오른쪽 피연산자의 hello 하나으로 평가 됩니다 **알 수 없는**, hello 결과 **알 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="951af-186">`[NOT] LIKE`에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="951af-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="951af-187">모든 피연산자도 확인 될 경우 **알 수 없는**, hello 결과 **알 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="951af-188">`[NOT] IN`에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="951af-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="951af-189">왼쪽 피연산자 hello로 평가 되는 경우 **알 수 없는**, hello 결과 **알 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="951af-190">**AND** 연산자에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="951af-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="951af-191">**OR** 연산자에서 알 수 없음 평가:</span><span class="sxs-lookup"><span data-stu-id="951af-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="951af-192">연산자 바인딩 의미 체계</span><span class="sxs-lookup"><span data-stu-id="951af-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="951af-193">비교 연산자와 같은 `>`, `>=`, `<`, `<=`, `!=`, 및 `=` 따라 hello 동일한 데이터에서 바인딩 hello C# 연산자와 의미 체계 형식 승격 및 암시적 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="951af-194">산술 연산자와 같은 `+`, `-`, `*`, `/`, 및 `%` 따라 hello 동일한 데이터에서 바인딩 hello C# 연산자와 의미 체계 형식 승격 및 암시적 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="951af-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="951af-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="951af-195">Next steps</span></span>

- [<span data-ttu-id="951af-196">SQLFilter 클래스</span><span class="sxs-lookup"><span data-stu-id="951af-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="951af-197">SQLRuleAction 클래스</span><span class="sxs-lookup"><span data-stu-id="951af-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)