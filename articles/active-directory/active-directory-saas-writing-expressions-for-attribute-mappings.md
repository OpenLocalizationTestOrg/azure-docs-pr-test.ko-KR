---
title: "Azure Active Directory의 특성 매핑에 대한 식 작성 | Microsoft Docs"
description: "Azure Active Directory에서 SaaS 앱 개체의 자동화된 프로비전 중 허용되는 형식으로 특성 값을 변환하기 위해 식 매핑을 사용하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: c944a355c07b96c27dcdd477f625638284eabdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a><span data-ttu-id="75972-103">Azure Active Directory의 특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="75972-103">Writing Expressions for Attribute Mappings in Azure Active Directory</span></span>
<span data-ttu-id="75972-104">SaaS 응용 프로그램에 프로비전을 구성하면 식 매핑은 지정할 수 있는 특성 매핑의 유형 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-104">When you configure provisioning to a SaaS application, one of the types of attribute mappings that you can specify is an expression mapping.</span></span> <span data-ttu-id="75972-105">이러한 경우, 사용자의 데이터를 SaaS 응용 프로그램에 대해 사용하는 형식으로 변환할 수 있는 스크립트 방식의 식을 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-105">For these, you must write a script-like expression that allows you to transform your users’ data into formats that are more acceptable for the SaaS application.</span></span>

## <a name="syntax-overview"></a><span data-ttu-id="75972-106">구문 개요</span><span class="sxs-lookup"><span data-stu-id="75972-106">Syntax Overview</span></span>
<span data-ttu-id="75972-107">특성 매핑을 위한 식의 구문은 VBA(Visual Basic Applications) 함수를 연상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="75972-107">The syntax for Expressions for Attribute Mappings is reminiscent of Visual Basic for Applications (VBA) functions.</span></span>

* <span data-ttu-id="75972-108">전체 식은 </span><span class="sxs-lookup"><span data-stu-id="75972-108">The entire expression must be defined in terms of functions, which consist of a name followed by arguments in parentheses:</span></span> <br><span data-ttu-id="75972-109">
  *FunctionName (<<인수 1>>,<<argument N>>)*</span><span class="sxs-lookup"><span data-stu-id="75972-109">
*FunctionName(<<argument 1>>,<<argument N>>)*</span></span>
* <span data-ttu-id="75972-110">서로 함수를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-110">You may nest functions within each other.</span></span> <span data-ttu-id="75972-111">예:</span><span class="sxs-lookup"><span data-stu-id="75972-111">For example:</span></span> <br> <span data-ttu-id="75972-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span><span class="sxs-lookup"><span data-stu-id="75972-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span></span>
* <span data-ttu-id="75972-113">함수에 3가지 다른 유형의 인수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-113">You can pass three different types of arguments into functions:</span></span>
  
  1. <span data-ttu-id="75972-114">특성은 대괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-114">Attributes, which must be enclosed in square square brackets.</span></span> <span data-ttu-id="75972-115">예: [attributeName]</span><span class="sxs-lookup"><span data-stu-id="75972-115">For example: [attributeName]</span></span>
  2. <span data-ttu-id="75972-116">문자열 상수는 큰따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-116">String constants, which must be enclosed in double quotes.</span></span> <span data-ttu-id="75972-117">예: "미국"</span><span class="sxs-lookup"><span data-stu-id="75972-117">For example: "United States"</span></span>
  3. <span data-ttu-id="75972-118">기타 함수</span><span class="sxs-lookup"><span data-stu-id="75972-118">Other Functions.</span></span> <span data-ttu-id="75972-119">예: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span><span class="sxs-lookup"><span data-stu-id="75972-119">For example: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span></span>
* <span data-ttu-id="75972-120">문자열 상수의 경우, 백슬래시 (\) 또는 따옴표(")가 문자열에 필요한 경우 백슬래시(\) 기호로 이스케이프되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-120">For string constants, if you need a backslash ( \ ) or quotation mark ( " ) in the string, it must be escaped with the backslash ( \ ) symbol.</span></span> <span data-ttu-id="75972-121">예: "회사 이름: \"Contoso\""</span><span class="sxs-lookup"><span data-stu-id="75972-121">For example: "Company name: \"Contoso\""</span></span>

## <a name="list-of-functions"></a><span data-ttu-id="75972-122">함수 목록</span><span class="sxs-lookup"><span data-stu-id="75972-122">List of Functions</span></span>
<span data-ttu-id="75972-123">[추가](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span><span class="sxs-lookup"><span data-stu-id="75972-123">[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span></span>

- - -
### <a name="append"></a><span data-ttu-id="75972-124">추가</span><span class="sxs-lookup"><span data-stu-id="75972-124">Append</span></span>
<span data-ttu-id="75972-125">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-125">**Function:**</span></span><br> <span data-ttu-id="75972-126">Append(source, suffix)</span><span class="sxs-lookup"><span data-stu-id="75972-126">Append(source, suffix)</span></span>

<span data-ttu-id="75972-127">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-127">**Description:**</span></span><br> <span data-ttu-id="75972-128">원본 문자열 값을 문자열의 끝에 접미사로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-128">Takes a source string value and appends the suffix to the end of it.</span></span>

<span data-ttu-id="75972-129">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-129">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-130">이름</span><span class="sxs-lookup"><span data-stu-id="75972-130">Name</span></span> | <span data-ttu-id="75972-131">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-131">Required/ Repeating</span></span> | <span data-ttu-id="75972-132">형식</span><span class="sxs-lookup"><span data-stu-id="75972-132">Type</span></span> | <span data-ttu-id="75972-133">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-133">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-134">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-134">**source**</span></span> |<span data-ttu-id="75972-135">필수</span><span class="sxs-lookup"><span data-stu-id="75972-135">Required</span></span> |<span data-ttu-id="75972-136">String</span><span class="sxs-lookup"><span data-stu-id="75972-136">String</span></span> |<span data-ttu-id="75972-137">대개는 원본 개체의 특성 이름</span><span class="sxs-lookup"><span data-stu-id="75972-137">Usually name of the attribute from the source object</span></span> |
| <span data-ttu-id="75972-138">**접미사**</span><span class="sxs-lookup"><span data-stu-id="75972-138">**suffix**</span></span> |<span data-ttu-id="75972-139">필수</span><span class="sxs-lookup"><span data-stu-id="75972-139">Required</span></span> |<span data-ttu-id="75972-140">String</span><span class="sxs-lookup"><span data-stu-id="75972-140">String</span></span> |<span data-ttu-id="75972-141">원본 값의 끝에 추가하려는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-141">The string that you want to append to the end of the source value.</span></span> |

- - -
### <a name="formatdatetime"></a><span data-ttu-id="75972-142">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="75972-142">FormatDateTime</span></span>
<span data-ttu-id="75972-143">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-143">**Function:**</span></span><br> <span data-ttu-id="75972-144">FormatDateTime(source, inputFormat, outputFormat)</span><span class="sxs-lookup"><span data-stu-id="75972-144">FormatDateTime(source, inputFormat, outputFormat)</span></span>

<span data-ttu-id="75972-145">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-145">**Description:**</span></span><br> <span data-ttu-id="75972-146">한 형식의 날짜 문자열을 다른 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-146">Takes a date string from one format and converts it into a different format.</span></span>

<span data-ttu-id="75972-147">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-147">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-148">이름</span><span class="sxs-lookup"><span data-stu-id="75972-148">Name</span></span> | <span data-ttu-id="75972-149">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-149">Required/ Repeating</span></span> | <span data-ttu-id="75972-150">형식</span><span class="sxs-lookup"><span data-stu-id="75972-150">Type</span></span> | <span data-ttu-id="75972-151">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-151">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-152">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-152">**source**</span></span> |<span data-ttu-id="75972-153">필수</span><span class="sxs-lookup"><span data-stu-id="75972-153">Required</span></span> |<span data-ttu-id="75972-154">String</span><span class="sxs-lookup"><span data-stu-id="75972-154">String</span></span> |<span data-ttu-id="75972-155">대개는 원본 개체의 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-155">Usually name of the attribute from the source object.</span></span> |
| <span data-ttu-id="75972-156">**inputFormat**</span><span class="sxs-lookup"><span data-stu-id="75972-156">**inputFormat**</span></span> |<span data-ttu-id="75972-157">필수</span><span class="sxs-lookup"><span data-stu-id="75972-157">Required</span></span> |<span data-ttu-id="75972-158">String</span><span class="sxs-lookup"><span data-stu-id="75972-158">String</span></span> |<span data-ttu-id="75972-159">원본 값의 예상된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-159">Expected format of the source value.</span></span> <span data-ttu-id="75972-160">지원되는 형식은 [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75972-160">For supported formats, see [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx).</span></span> |
| <span data-ttu-id="75972-161">**outputFormat**</span><span class="sxs-lookup"><span data-stu-id="75972-161">**outputFormat**</span></span> |<span data-ttu-id="75972-162">필수</span><span class="sxs-lookup"><span data-stu-id="75972-162">Required</span></span> |<span data-ttu-id="75972-163">String</span><span class="sxs-lookup"><span data-stu-id="75972-163">String</span></span> |<span data-ttu-id="75972-164">출력 날짜의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-164">Format of the output date.</span></span> |

- - -
### <a name="join"></a><span data-ttu-id="75972-165">Join</span><span class="sxs-lookup"><span data-stu-id="75972-165">Join</span></span>
<span data-ttu-id="75972-166">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-166">**Function:**</span></span><br> <span data-ttu-id="75972-167">Join(separator, source1, source2, …)</span><span class="sxs-lookup"><span data-stu-id="75972-167">Join(separator, source1, source2, …)</span></span>

<span data-ttu-id="75972-168">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-168">**Description:**</span></span><br> <span data-ttu-id="75972-169">다중 **source** 문자열 값을 단일 문자열로 결합할 수 있다는 점을 제외하고 Join()은 Append()와 유사하며, 각 값은 **separator** 문자열로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="75972-169">Join() is similar to Append(), except that it can combine multiple **source** string values into a single string, and each value will be separated by a **separator** string.</span></span>

<span data-ttu-id="75972-170">원본 값 중 하나가 다중 값 특성인 경우, 해당 특성의 모든 값은 함께 조인되며 구분 기호 값을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-170">If one of the source values is a multi-value attribute, then every value in that attribute will be joined together, separated the separator value.</span></span>

<span data-ttu-id="75972-171">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-171">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-172">이름</span><span class="sxs-lookup"><span data-stu-id="75972-172">Name</span></span> | <span data-ttu-id="75972-173">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-173">Required/ Repeating</span></span> | <span data-ttu-id="75972-174">형식</span><span class="sxs-lookup"><span data-stu-id="75972-174">Type</span></span> | <span data-ttu-id="75972-175">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-175">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-176">**구분 기호**</span><span class="sxs-lookup"><span data-stu-id="75972-176">**separator**</span></span> |<span data-ttu-id="75972-177">필수</span><span class="sxs-lookup"><span data-stu-id="75972-177">Required</span></span> |<span data-ttu-id="75972-178">String</span><span class="sxs-lookup"><span data-stu-id="75972-178">String</span></span> |<span data-ttu-id="75972-179">문자열이 하나의 문자열로 연결되면 원본 값을 구분하는데 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-179">String used to separate source values when they are concatenated into one string.</span></span> <span data-ttu-id="75972-180">구분 기호가 필요하지 않은 경우 ""일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-180">Can be "" if no separator is required.</span></span> |
| <span data-ttu-id="75972-181">**source1  …</span><span class="sxs-lookup"><span data-stu-id="75972-181">**source1  …</span></span> <span data-ttu-id="75972-182">sourceN **</span><span class="sxs-lookup"><span data-stu-id="75972-182">sourceN **</span></span> |<span data-ttu-id="75972-183">필수, 시간 변수</span><span class="sxs-lookup"><span data-stu-id="75972-183">Required, variable-number of times</span></span> |<span data-ttu-id="75972-184">String</span><span class="sxs-lookup"><span data-stu-id="75972-184">String</span></span> |<span data-ttu-id="75972-185">값이 함께 조인될 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-185">String values to be joined together.</span></span> |

- - -
### <a name="mid"></a><span data-ttu-id="75972-186">Mid</span><span class="sxs-lookup"><span data-stu-id="75972-186">Mid</span></span>
<span data-ttu-id="75972-187">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-187">**Function:**</span></span><br> <span data-ttu-id="75972-188">Mid(source, start, length)</span><span class="sxs-lookup"><span data-stu-id="75972-188">Mid(source, start, length)</span></span>

<span data-ttu-id="75972-189">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-189">**Description:**</span></span><br> <span data-ttu-id="75972-190">원본 값의 부분 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-190">Returns a substring of the source value.</span></span> <span data-ttu-id="75972-191">부분 문자열은 원본 문자열에서 문자 중 일부만 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-191">A substring is a string that contains only some of the characters from the source string.</span></span>

<span data-ttu-id="75972-192">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-192">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-193">이름</span><span class="sxs-lookup"><span data-stu-id="75972-193">Name</span></span> | <span data-ttu-id="75972-194">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-194">Required/ Repeating</span></span> | <span data-ttu-id="75972-195">형식</span><span class="sxs-lookup"><span data-stu-id="75972-195">Type</span></span> | <span data-ttu-id="75972-196">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-196">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-197">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-197">**source**</span></span> |<span data-ttu-id="75972-198">필수</span><span class="sxs-lookup"><span data-stu-id="75972-198">Required</span></span> |<span data-ttu-id="75972-199">String</span><span class="sxs-lookup"><span data-stu-id="75972-199">String</span></span> |<span data-ttu-id="75972-200">일반적으로 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-200">Usually name of the attribute.</span></span> |
| <span data-ttu-id="75972-201">**시작**</span><span class="sxs-lookup"><span data-stu-id="75972-201">**start**</span></span> |<span data-ttu-id="75972-202">필수</span><span class="sxs-lookup"><span data-stu-id="75972-202">Required</span></span> |<span data-ttu-id="75972-203">정수</span><span class="sxs-lookup"><span data-stu-id="75972-203">integer</span></span> |<span data-ttu-id="75972-204">부분 문자열이 시작될 **원본** 문자열의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-204">Index in the **source** string where substring should start.</span></span> <span data-ttu-id="75972-205">문자열의 첫번째 문자에는 인덱스 1이 있고, 두번째 문자에는 인덱스 2가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-205">First character in the string will have index of 1, second character will have index 2, and so on.</span></span> |
| <span data-ttu-id="75972-206">**length**</span><span class="sxs-lookup"><span data-stu-id="75972-206">**length**</span></span> |<span data-ttu-id="75972-207">필수</span><span class="sxs-lookup"><span data-stu-id="75972-207">Required</span></span> |<span data-ttu-id="75972-208">정수</span><span class="sxs-lookup"><span data-stu-id="75972-208">integer</span></span> |<span data-ttu-id="75972-209">부분 문자열의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-209">Length of the substring.</span></span> <span data-ttu-id="75972-210">길이가 **원본** 문자열 외부에서 종료되면 함수는 **시작** 인덱스부터 **원본** 문자열 끝까지의 부분 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-210">If length ends outside the **source** string, function will return substring from **start** index till end of **source** string.</span></span> |

- - -
### <a name="not"></a><span data-ttu-id="75972-211">not</span><span class="sxs-lookup"><span data-stu-id="75972-211">Not</span></span>
<span data-ttu-id="75972-212">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-212">**Function:**</span></span><br> <span data-ttu-id="75972-213">Not(source)</span><span class="sxs-lookup"><span data-stu-id="75972-213">Not(source)</span></span>

<span data-ttu-id="75972-214">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-214">**Description:**</span></span><br> <span data-ttu-id="75972-215">**원본**의 부울 값을 대칭 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-215">Flips the boolean value of the **source**.</span></span> <span data-ttu-id="75972-216">**원본** 값이 "*True*"인 경우 "*False*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-216">If **source** value is "*True*", returns "*False*".</span></span> <span data-ttu-id="75972-217">그렇지 않은 경우 "*True*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-217">Otherwise, returns "*True*".</span></span>

<span data-ttu-id="75972-218">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-218">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-219">이름</span><span class="sxs-lookup"><span data-stu-id="75972-219">Name</span></span> | <span data-ttu-id="75972-220">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-220">Required/ Repeating</span></span> | <span data-ttu-id="75972-221">형식</span><span class="sxs-lookup"><span data-stu-id="75972-221">Type</span></span> | <span data-ttu-id="75972-222">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-222">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-223">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-223">**source**</span></span> |<span data-ttu-id="75972-224">필수</span><span class="sxs-lookup"><span data-stu-id="75972-224">Required</span></span> |<span data-ttu-id="75972-225">부울 문자열</span><span class="sxs-lookup"><span data-stu-id="75972-225">Boolean String</span></span> |<span data-ttu-id="75972-226">예상 **원본** 값은 "True" 또는 "False"입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-226">Expected **source** values are "True" or "False"..</span></span> |

- - -
### <a name="replace"></a><span data-ttu-id="75972-227">Replace</span><span class="sxs-lookup"><span data-stu-id="75972-227">Replace</span></span>
<span data-ttu-id="75972-228">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-228">**Function:**</span></span><br> <span data-ttu-id="75972-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span><span class="sxs-lookup"><span data-stu-id="75972-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span></span>

<span data-ttu-id="75972-230">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-230">**Description:**</span></span><br>
<span data-ttu-id="75972-231">문자열 내 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-231">Replaces values within a string.</span></span> <span data-ttu-id="75972-232">제공된 매개 변수에 따라 다르게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-232">It works differently depending on the parameters provided:</span></span>

* <span data-ttu-id="75972-233">**oldValue** 및 **replacementValue**가 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="75972-233">When **oldValue** and **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="75972-234">소스에서 oldValue의 모든 항목을 replacementValue로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-234">Replaces all occurrences of oldValue in the source  with replacementValue</span></span>
* <span data-ttu-id="75972-235">**oldValue** 및 **template**이 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="75972-235">When **oldValue** and **template** are provided:</span></span>
  
  * <span data-ttu-id="75972-236">**template**에서 **oldValue**의 모든 항목을 **원본** 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="75972-236">Replaces all occurrences of the **oldValue** in the **template** with the **source** value</span></span>
* <span data-ttu-id="75972-237">**oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue**가 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="75972-237">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="75972-238">원본 문자열에서 OldValueRegexPattern과 일치하는 모든 값을 replacementValue로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-238">Replaces all values matching oldValueRegexPattern in the source string with replacementValue</span></span>
* <span data-ttu-id="75972-239">**oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName**이 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="75972-239">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** are provided:</span></span>
  
  * <span data-ttu-id="75972-240">**원본**에 값이 있는 경우 **원본**이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="75972-240">If **source** has value, **source** is returned</span></span>
  * <span data-ttu-id="75972-241">**원본**에 값이 없는 경우 **oldValueRegexPattern** 및 **oldValueRegexGroupName**을 사용하여 **replacementPropertyName**으로 속성에서 대체 값을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-241">If **source** has no value, uses **oldValueRegexPattern** and **oldValueRegexGroupName** to extract replacement value from the property with **replacementPropertyName**.</span></span> <span data-ttu-id="75972-242">대체 값이 결과로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="75972-242">Replacement value is returned as the result</span></span>

<span data-ttu-id="75972-243">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-243">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-244">이름</span><span class="sxs-lookup"><span data-stu-id="75972-244">Name</span></span> | <span data-ttu-id="75972-245">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-245">Required/ Repeating</span></span> | <span data-ttu-id="75972-246">형식</span><span class="sxs-lookup"><span data-stu-id="75972-246">Type</span></span> | <span data-ttu-id="75972-247">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-247">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-248">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-248">**source**</span></span> |<span data-ttu-id="75972-249">필수</span><span class="sxs-lookup"><span data-stu-id="75972-249">Required</span></span> |<span data-ttu-id="75972-250">String</span><span class="sxs-lookup"><span data-stu-id="75972-250">String</span></span> |<span data-ttu-id="75972-251">대개는 원본 개체의 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-251">Usually name of the attribute from the source object.</span></span> |
| <span data-ttu-id="75972-252">**oldValue**</span><span class="sxs-lookup"><span data-stu-id="75972-252">**oldValue**</span></span> |<span data-ttu-id="75972-253">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-253">Optional</span></span> |<span data-ttu-id="75972-254">String</span><span class="sxs-lookup"><span data-stu-id="75972-254">String</span></span> |<span data-ttu-id="75972-255">**원본** 또는 **템플릿**에서 대체될 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-255">Value to be replaced in **source** or **template**.</span></span> |
| <span data-ttu-id="75972-256">**regexPattern**</span><span class="sxs-lookup"><span data-stu-id="75972-256">**regexPattern**</span></span> |<span data-ttu-id="75972-257">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-257">Optional</span></span> |<span data-ttu-id="75972-258">String</span><span class="sxs-lookup"><span data-stu-id="75972-258">String</span></span> |<span data-ttu-id="75972-259">**원본**에서 대체될 값에 대한 Regex 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-259">Regex pattern for the value to be replaced in **source**.</span></span> <span data-ttu-id="75972-260">또는 replacementPropertyName를 사용하면 대체 속성에서 값을 추출하는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-260">Or, when replacementPropertyName is used, pattern to extract value from replacement property.</span></span> |
| <span data-ttu-id="75972-261">**regexGroupName**</span><span class="sxs-lookup"><span data-stu-id="75972-261">**regexGroupName**</span></span> |<span data-ttu-id="75972-262">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-262">Optional</span></span> |<span data-ttu-id="75972-263">String</span><span class="sxs-lookup"><span data-stu-id="75972-263">String</span></span> |<span data-ttu-id="75972-264">**regexPattern**내 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-264">Name of the group inside **regexPattern**.</span></span> <span data-ttu-id="75972-265">replacementPropertyName를 사용하는 경우에만 replacement 속성에서 replacementValue로 이 그룹의 값을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-265">Only when  replacementPropertyName is used, we will extract value of this group as replacementValue from replacement property.</span></span> |
| <span data-ttu-id="75972-266">**replacementValue**</span><span class="sxs-lookup"><span data-stu-id="75972-266">**replacementValue**</span></span> |<span data-ttu-id="75972-267">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-267">Optional</span></span> |<span data-ttu-id="75972-268">String</span><span class="sxs-lookup"><span data-stu-id="75972-268">String</span></span> |<span data-ttu-id="75972-269">이전 값과 대체할 새로운 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-269">New value to replace old one with.</span></span> |
| <span data-ttu-id="75972-270">**replacementAttributeName**</span><span class="sxs-lookup"><span data-stu-id="75972-270">**replacementAttributeName**</span></span> |<span data-ttu-id="75972-271">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-271">Optional</span></span> |<span data-ttu-id="75972-272">String</span><span class="sxs-lookup"><span data-stu-id="75972-272">String</span></span> |<span data-ttu-id="75972-273">원본에 값이 없는 경우 대체 값에 사용할 특성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-273">Name of the attribute to be used for replacement value, when source has no value.</span></span> |
| <span data-ttu-id="75972-274">**template**</span><span class="sxs-lookup"><span data-stu-id="75972-274">**template**</span></span> |<span data-ttu-id="75972-275">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-275">Optional</span></span> |<span data-ttu-id="75972-276">String</span><span class="sxs-lookup"><span data-stu-id="75972-276">String</span></span> |<span data-ttu-id="75972-277">**template** 값이 제공되면, 템플릿 내에서 **oldValue**를 찾아 원본 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="75972-277">When **template** value is provided, we will look for **oldValue** inside the template and replace it with source value.</span></span> |

- - -
### <a name="stripspaces"></a><span data-ttu-id="75972-278">StripSpaces</span><span class="sxs-lookup"><span data-stu-id="75972-278">StripSpaces</span></span>
<span data-ttu-id="75972-279">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-279">**Function:**</span></span><br> <span data-ttu-id="75972-280">StripSpaces(source)</span><span class="sxs-lookup"><span data-stu-id="75972-280">StripSpaces(source)</span></span>

<span data-ttu-id="75972-281">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-281">**Description:**</span></span><br> <span data-ttu-id="75972-282">원본 문자열에서 모든 공백(" ")을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-282">Removes all space (" ") characters from the source string.</span></span>

<span data-ttu-id="75972-283">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-283">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-284">이름</span><span class="sxs-lookup"><span data-stu-id="75972-284">Name</span></span> | <span data-ttu-id="75972-285">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-285">Required/ Repeating</span></span> | <span data-ttu-id="75972-286">형식</span><span class="sxs-lookup"><span data-stu-id="75972-286">Type</span></span> | <span data-ttu-id="75972-287">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-287">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-288">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-288">**source**</span></span> |<span data-ttu-id="75972-289">필수</span><span class="sxs-lookup"><span data-stu-id="75972-289">Required</span></span> |<span data-ttu-id="75972-290">String</span><span class="sxs-lookup"><span data-stu-id="75972-290">String</span></span> |<span data-ttu-id="75972-291">**원본** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-291">**source** value to update.</span></span> |

- - -
### <a name="switch"></a><span data-ttu-id="75972-292">Switch</span><span class="sxs-lookup"><span data-stu-id="75972-292">Switch</span></span>
<span data-ttu-id="75972-293">**함수:**</span><span class="sxs-lookup"><span data-stu-id="75972-293">**Function:**</span></span><br> <span data-ttu-id="75972-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span><span class="sxs-lookup"><span data-stu-id="75972-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span></span>

<span data-ttu-id="75972-295">**설명:**</span><span class="sxs-lookup"><span data-stu-id="75972-295">**Description:**</span></span><br> <span data-ttu-id="75972-296">**원본** 값이 **key**와 일치하면, 해당 **key**의 **value**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-296">When **source** value matches a **key**, returns **value** for that **key**.</span></span> <span data-ttu-id="75972-297">**원본** 값과 일치하는 키가 없으면 **defaultValue**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-297">If **source** value doesn't match any keys, returns **defaultValue**.</span></span>  <span data-ttu-id="75972-298">**Key** 및 **value** 매개 변수는 항상 쌍으로 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-298">**Key** and **value** parameters must always come in pairs.</span></span> <span data-ttu-id="75972-299">함수는 항상 짝수 개수의 매개 변수를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-299">The function always expects an even number of parameters.</span></span>

<span data-ttu-id="75972-300">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="75972-300">**Parameters:**</span></span><br> 

| <span data-ttu-id="75972-301">이름</span><span class="sxs-lookup"><span data-stu-id="75972-301">Name</span></span> | <span data-ttu-id="75972-302">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="75972-302">Required/ Repeating</span></span> | <span data-ttu-id="75972-303">형식</span><span class="sxs-lookup"><span data-stu-id="75972-303">Type</span></span> | <span data-ttu-id="75972-304">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75972-304">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75972-305">**원본**</span><span class="sxs-lookup"><span data-stu-id="75972-305">**source**</span></span> |<span data-ttu-id="75972-306">필수</span><span class="sxs-lookup"><span data-stu-id="75972-306">Required</span></span> |<span data-ttu-id="75972-307">String</span><span class="sxs-lookup"><span data-stu-id="75972-307">String</span></span> |<span data-ttu-id="75972-308">**Source** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-308">**Source** value to update.</span></span> |
| <span data-ttu-id="75972-309">**defaultValue**</span><span class="sxs-lookup"><span data-stu-id="75972-309">**defaultValue**</span></span> |<span data-ttu-id="75972-310">옵션</span><span class="sxs-lookup"><span data-stu-id="75972-310">Optional</span></span> |<span data-ttu-id="75972-311">String</span><span class="sxs-lookup"><span data-stu-id="75972-311">String</span></span> |<span data-ttu-id="75972-312">원본이 모든 키와 일치하지 않는 경우 사용할 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-312">Default value to be used when source doesn't match any keys.</span></span> <span data-ttu-id="75972-313">빈 문자열("")일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-313">Can be empty string ("").</span></span> |
| <span data-ttu-id="75972-314">**key**</span><span class="sxs-lookup"><span data-stu-id="75972-314">**key**</span></span> |<span data-ttu-id="75972-315">필수</span><span class="sxs-lookup"><span data-stu-id="75972-315">Required</span></span> |<span data-ttu-id="75972-316">String</span><span class="sxs-lookup"><span data-stu-id="75972-316">String</span></span> |<span data-ttu-id="75972-317">**원본** 값과 비교할 **Key**입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-317">**Key** to compare **source** value with.</span></span> |
| <span data-ttu-id="75972-318">**값**</span><span class="sxs-lookup"><span data-stu-id="75972-318">**value**</span></span> |<span data-ttu-id="75972-319">필수</span><span class="sxs-lookup"><span data-stu-id="75972-319">Required</span></span> |<span data-ttu-id="75972-320">String</span><span class="sxs-lookup"><span data-stu-id="75972-320">String</span></span> |<span data-ttu-id="75972-321">키와 일치하는 **원본** 의 대체 값입니다.</span><span class="sxs-lookup"><span data-stu-id="75972-321">Replacement value for the **source** matching the key.</span></span> |

## <a name="examples"></a><span data-ttu-id="75972-322">예</span><span class="sxs-lookup"><span data-stu-id="75972-322">Examples</span></span>
### <a name="strip-known-domain-name"></a><span data-ttu-id="75972-323">알려진 도메인 이름 제거</span><span class="sxs-lookup"><span data-stu-id="75972-323">Strip known domain name</span></span>
<span data-ttu-id="75972-324">사용자 이름을 가져오려면 사용자의 전자 메일에서 알려진 도메인 이름을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-324">You need to strip a known domain name from a user’s email to obtain a user name.</span></span> <br>
<span data-ttu-id="75972-325">예를 들어, 도메인이 "contoso.com"인 경우 다음 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-325">For example, if the domain is "contoso.com", then you could use the following expression:</span></span>

<span data-ttu-id="75972-326">**식:**</span><span class="sxs-lookup"><span data-stu-id="75972-326">**Expression:**</span></span> <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

<span data-ttu-id="75972-327">**샘플 입출력:**</span><span class="sxs-lookup"><span data-stu-id="75972-327">**Sample input / output:**</span></span> <br>

* <span data-ttu-id="75972-328">**입력**(메일): “john.doe@contoso.com”</span><span class="sxs-lookup"><span data-stu-id="75972-328">**INPUT** (mail): "john.doe@contoso.com"</span></span>
* <span data-ttu-id="75972-329">**출력**: "john.doe"</span><span class="sxs-lookup"><span data-stu-id="75972-329">**OUTPUT**:  "john.doe"</span></span>

### <a name="append-constant-suffix-to-user-name"></a><span data-ttu-id="75972-330">사용자 이름에 상수 접미사 추가</span><span class="sxs-lookup"><span data-stu-id="75972-330">Append constant suffix to user name</span></span>
<span data-ttu-id="75972-331">Salesforce 샌드박스를 사용하는 경우 동기화하기 전에 모든 사용자 이름에 추가 접미사를 추가해야할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-331">If you are using a Salesforce Sandbox, you might need to append an additional suffix to all your user names before synchronizing them.</span></span>

<span data-ttu-id="75972-332">**식:**</span><span class="sxs-lookup"><span data-stu-id="75972-332">**Expression:**</span></span> <br>
`Append([userPrincipalName], ".test"))`

<span data-ttu-id="75972-333">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="75972-333">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="75972-334">**입력**: (userPrincipalName): “John.Doe@contoso.com”</span><span class="sxs-lookup"><span data-stu-id="75972-334">**INPUT**: (userPrincipalName): "John.Doe@contoso.com"</span></span>
* <span data-ttu-id="75972-335">**출력**:  “John.Doe@contoso.com.test”</span><span class="sxs-lookup"><span data-stu-id="75972-335">**OUTPUT**:  "John.Doe@contoso.com.test"</span></span>

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a><span data-ttu-id="75972-336">이름과 성의 부분을 연결하여 사용자 별칭을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-336">Generate user alias by concatenating parts of first and last name</span></span>
<span data-ttu-id="75972-337">사용자의 이름 중 처음 3개 문자 및 사용자 성의 처음 5개 문자를 사용하여 사용자 별칭을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-337">You need to generate a user alias by taking first 3 letters of user's first name and first 5 letters of user's last name.</span></span>

<span data-ttu-id="75972-338">**식:**</span><span class="sxs-lookup"><span data-stu-id="75972-338">**Expression:**</span></span> <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

<span data-ttu-id="75972-339">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="75972-339">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="75972-340">**입력** (givenName): "John"</span><span class="sxs-lookup"><span data-stu-id="75972-340">**INPUT** (givenName): "John"</span></span>
* <span data-ttu-id="75972-341">**입력** (surname): "Doe"</span><span class="sxs-lookup"><span data-stu-id="75972-341">**INPUT** (surname): "Doe"</span></span>
* <span data-ttu-id="75972-342">**출력**: "JohDoe"</span><span class="sxs-lookup"><span data-stu-id="75972-342">**OUTPUT**:  "JohDoe"</span></span>

### <a name="output-date-as-a-string-in-a-certain-format"></a><span data-ttu-id="75972-343">특정 형식에서 문자열로 출력 날짜</span><span class="sxs-lookup"><span data-stu-id="75972-343">Output date as a string in a certain format</span></span>
<span data-ttu-id="75972-344">SaaS 응용 프로그램에 특정 형식의 날짜를 전송하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-344">You want to send dates to a SaaS application in a certain format.</span></span> <br>
<span data-ttu-id="75972-345">예를 들어 ServiceNow에 대한 날짜 형식을 지정하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75972-345">For example, you want to format dates for ServiceNow.</span></span>

<span data-ttu-id="75972-346">**식:**</span><span class="sxs-lookup"><span data-stu-id="75972-346">**Expression:**</span></span> <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

<span data-ttu-id="75972-347">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="75972-347">**Sample input/output:**</span></span>

* <span data-ttu-id="75972-348">**입력** (extensionAttribute1): "20150123105347.1Z"</span><span class="sxs-lookup"><span data-stu-id="75972-348">**INPUT** (extensionAttribute1): "20150123105347.1Z"</span></span>
* <span data-ttu-id="75972-349">**출력**: “2015-01-23”</span><span class="sxs-lookup"><span data-stu-id="75972-349">**OUTPUT**:  "2015-01-23"</span></span>

### <a name="replace-a-value-based-on-predefined-set-of-options"></a><span data-ttu-id="75972-350">미리 정의된 옵션 집합을 기반으로 값 바꾸기</span><span class="sxs-lookup"><span data-stu-id="75972-350">Replace a value based on predefined set of options</span></span>
<span data-ttu-id="75972-351">Azure AD에 저장된 상태 코드를 기반으로 사용자의 시간대를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-351">You need to define the time zone of the user based on the state code stored in Azure AD.</span></span> <br>
<span data-ttu-id="75972-352">상태 코드가 미리 정의된 옵션 중 하나와 일치하지 않으면 기본값인 "오스트레일리아/시드니"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75972-352">If the state code doesn't match any of the predefined options, use default value of "Australia/Sydney".</span></span>

<span data-ttu-id="75972-353">**식:**</span><span class="sxs-lookup"><span data-stu-id="75972-353">**Expression:**</span></span> <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

<span data-ttu-id="75972-354">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="75972-354">**Sample input/output:**</span></span>

* <span data-ttu-id="75972-355">**입력** (상태): "QLD"</span><span class="sxs-lookup"><span data-stu-id="75972-355">**INPUT** (state): "QLD"</span></span>
* <span data-ttu-id="75972-356">**출력**: "오스트레일리아/브리즈번"</span><span class="sxs-lookup"><span data-stu-id="75972-356">**OUTPUT**: "Australia/Brisbane"</span></span>

## <a name="related-articles"></a><span data-ttu-id="75972-357">관련 문서</span><span class="sxs-lookup"><span data-stu-id="75972-357">Related Articles</span></span>
* [<span data-ttu-id="75972-358">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="75972-358">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="75972-359">SaaS 앱에 자동화된 사용자 프로비전/프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="75972-359">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="75972-360">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="75972-360">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="75972-361">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="75972-361">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="75972-362">SCIM를 사용하여 Azure Active Directory으로부터 응용 프로그램에 사용자 및 그룹의 자동 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="75972-362">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="75972-363">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="75972-363">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="75972-364">SaaS App을 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="75972-364">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

