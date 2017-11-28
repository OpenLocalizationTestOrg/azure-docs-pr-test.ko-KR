---
title: "Azure Active Directory에서 특성 매핑에 대 한 식 aaaWriting | Microsoft Docs"
description: "Azure Active Directory에 있는 SaaS 응용 프로그램 개체의 자동화 된 프로 비전 하는 동안 toouse 식 매핑 tootransform 특성 허용 가능한 형식으로 값 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a><span data-ttu-id="6ba3c-103">Azure Active Directory의 특성 매핑에 대한 식 작성</span><span class="sxs-lookup"><span data-stu-id="6ba3c-103">Writing Expressions for Attribute Mappings in Azure Active Directory</span></span>
<span data-ttu-id="6ba3c-104">프로 비전 tooa SaaS 응용 프로그램을 구성한 경우 식으로 매핑하는 hello 유형의 지정할 수 있는 특성 매핑 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-104">When you configure provisioning tooa SaaS application, one of hello types of attribute mappings that you can specify is an expression mapping.</span></span> <span data-ttu-id="6ba3c-105">이러한 경우를 위해 hello SaaS 응용 프로그램에 대 한 더 허용 되는 형식으로 tootransform를 허용 하는 스크립트와 유사한 식에 사용자의 데이터 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-105">For these, you must write a script-like expression that allows you tootransform your users’ data into formats that are more acceptable for hello SaaS application.</span></span>

## <a name="syntax-overview"></a><span data-ttu-id="6ba3c-106">구문 개요</span><span class="sxs-lookup"><span data-stu-id="6ba3c-106">Syntax Overview</span></span>
<span data-ttu-id="6ba3c-107">특성 매핑에 대 한 식에 대 한 hello 구문은 VBA 함수에 대 한 Visual Basic의 연상입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-107">hello syntax for Expressions for Attribute Mappings is reminiscent of Visual Basic for Applications (VBA) functions.</span></span>

* <span data-ttu-id="6ba3c-108">hello 전체 식은 다음 괄호 안에 인수 이름으로 구성 하는 함수 측면에서 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-108">hello entire expression must be defined in terms of functions, which consist of a name followed by arguments in parentheses:</span></span> <br><span data-ttu-id="6ba3c-109">
  *FunctionName (<<인수 1>>,<<argument N>>)*</span><span class="sxs-lookup"><span data-stu-id="6ba3c-109">
*FunctionName(<<argument 1>>,<<argument N>>)*</span></span>
* <span data-ttu-id="6ba3c-110">서로 함수를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-110">You may nest functions within each other.</span></span> <span data-ttu-id="6ba3c-111">예:</span><span class="sxs-lookup"><span data-stu-id="6ba3c-111">For example:</span></span> <br> <span data-ttu-id="6ba3c-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span><span class="sxs-lookup"><span data-stu-id="6ba3c-112">*FunctionOne(FunctionTwo(<<argument1>>))*</span></span>
* <span data-ttu-id="6ba3c-113">함수에 3가지 다른 유형의 인수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-113">You can pass three different types of arguments into functions:</span></span>
  
  1. <span data-ttu-id="6ba3c-114">특성은 대괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-114">Attributes, which must be enclosed in square square brackets.</span></span> <span data-ttu-id="6ba3c-115">예: [attributeName]</span><span class="sxs-lookup"><span data-stu-id="6ba3c-115">For example: [attributeName]</span></span>
  2. <span data-ttu-id="6ba3c-116">문자열 상수는 큰따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-116">String constants, which must be enclosed in double quotes.</span></span> <span data-ttu-id="6ba3c-117">예: "미국"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-117">For example: "United States"</span></span>
  3. <span data-ttu-id="6ba3c-118">기타 함수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-118">Other Functions.</span></span> <span data-ttu-id="6ba3c-119">예: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span><span class="sxs-lookup"><span data-stu-id="6ba3c-119">For example: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))</span></span>
* <span data-ttu-id="6ba3c-120">문자열 상수에 대 한 백슬래시 (\) 또는 hello 문자열에 따옴표 (")가 필요한 경우 이스케이프 해야 hello 백슬래시 (\) 기호로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-120">For string constants, if you need a backslash ( \ ) or quotation mark ( " ) in hello string, it must be escaped with hello backslash ( \ ) symbol.</span></span> <span data-ttu-id="6ba3c-121">예: "회사 이름: \"Contoso\""</span><span class="sxs-lookup"><span data-stu-id="6ba3c-121">For example: "Company name: \"Contoso\""</span></span>

## <a name="list-of-functions"></a><span data-ttu-id="6ba3c-122">함수 목록</span><span class="sxs-lookup"><span data-stu-id="6ba3c-122">List of Functions</span></span>
<span data-ttu-id="6ba3c-123">[추가](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-123">[Append](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)</span></span>

- - -
### <a name="append"></a><span data-ttu-id="6ba3c-124">추가</span><span class="sxs-lookup"><span data-stu-id="6ba3c-124">Append</span></span>
<span data-ttu-id="6ba3c-125">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-125">**Function:**</span></span><br> <span data-ttu-id="6ba3c-126">Append(source, suffix)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-126">Append(source, suffix)</span></span>

<span data-ttu-id="6ba3c-127">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-127">**Description:**</span></span><br> <span data-ttu-id="6ba3c-128">소스 문자열 값을 사용 하 고 hello toohello 끝에 접미사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-128">Takes a source string value and appends hello suffix toohello end of it.</span></span>

<span data-ttu-id="6ba3c-129">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-129">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-130">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-130">Name</span></span> | <span data-ttu-id="6ba3c-131">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-131">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-132">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-132">Type</span></span> | <span data-ttu-id="6ba3c-133">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-133">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-134">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-134">**source**</span></span> |<span data-ttu-id="6ba3c-135">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-135">Required</span></span> |<span data-ttu-id="6ba3c-136">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-136">String</span></span> |<span data-ttu-id="6ba3c-137">일반적으로 hello 원본 개체에서 hello 특성의 이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-137">Usually name of hello attribute from hello source object</span></span> |
| <span data-ttu-id="6ba3c-138">**접미사**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-138">**suffix**</span></span> |<span data-ttu-id="6ba3c-139">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-139">Required</span></span> |<span data-ttu-id="6ba3c-140">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-140">String</span></span> |<span data-ttu-id="6ba3c-141">hello 문자열 hello 소스 값의 tooappend toohello 끝 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-141">hello string that you want tooappend toohello end of hello source value.</span></span> |

- - -
### <a name="formatdatetime"></a><span data-ttu-id="6ba3c-142">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="6ba3c-142">FormatDateTime</span></span>
<span data-ttu-id="6ba3c-143">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-143">**Function:**</span></span><br> <span data-ttu-id="6ba3c-144">FormatDateTime(source, inputFormat, outputFormat)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-144">FormatDateTime(source, inputFormat, outputFormat)</span></span>

<span data-ttu-id="6ba3c-145">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-145">**Description:**</span></span><br> <span data-ttu-id="6ba3c-146">한 형식의 날짜 문자열을 다른 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-146">Takes a date string from one format and converts it into a different format.</span></span>

<span data-ttu-id="6ba3c-147">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-147">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-148">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-148">Name</span></span> | <span data-ttu-id="6ba3c-149">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-149">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-150">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-150">Type</span></span> | <span data-ttu-id="6ba3c-151">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-151">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-152">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-152">**source**</span></span> |<span data-ttu-id="6ba3c-153">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-153">Required</span></span> |<span data-ttu-id="6ba3c-154">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-154">String</span></span> |<span data-ttu-id="6ba3c-155">일반적으로 이름 사용 하 여 hello 원본 개체에서 hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-155">Usually name of hello attribute from hello source object.</span></span> |
| <span data-ttu-id="6ba3c-156">**inputFormat**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-156">**inputFormat**</span></span> |<span data-ttu-id="6ba3c-157">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-157">Required</span></span> |<span data-ttu-id="6ba3c-158">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-158">String</span></span> |<span data-ttu-id="6ba3c-159">Hello 소스 값의 예상된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-159">Expected format of hello source value.</span></span> <span data-ttu-id="6ba3c-160">지원되는 형식은 [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-160">For supported formats, see [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx).</span></span> |
| <span data-ttu-id="6ba3c-161">**outputFormat**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-161">**outputFormat**</span></span> |<span data-ttu-id="6ba3c-162">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-162">Required</span></span> |<span data-ttu-id="6ba3c-163">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-163">String</span></span> |<span data-ttu-id="6ba3c-164">Hello 출력 날짜의 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-164">Format of hello output date.</span></span> |

- - -
### <a name="join"></a><span data-ttu-id="6ba3c-165">Join</span><span class="sxs-lookup"><span data-stu-id="6ba3c-165">Join</span></span>
<span data-ttu-id="6ba3c-166">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-166">**Function:**</span></span><br> <span data-ttu-id="6ba3c-167">Join(separator, source1, source2, …)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-167">Join(separator, source1, source2, …)</span></span>

<span data-ttu-id="6ba3c-168">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-168">**Description:**</span></span><br> <span data-ttu-id="6ba3c-169">Join ()은 유사한 tooAppend() 점을 제외 하 고 결합할 수 있다는 점을 다중 **소스** 단일 문자열로 문자열 값 및 각 값으로 구분 됩니다는 **구분 기호** 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-169">Join() is similar tooAppend(), except that it can combine multiple **source** string values into a single string, and each value will be separated by a **separator** string.</span></span>

<span data-ttu-id="6ba3c-170">이면 hello 소스 값 중 하나는 다중 값 특성 해당 특성의 각 값이 함께 조인, 분리 된 hello 구분 기호 값 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-170">If one of hello source values is a multi-value attribute, then every value in that attribute will be joined together, separated hello separator value.</span></span>

<span data-ttu-id="6ba3c-171">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-171">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-172">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-172">Name</span></span> | <span data-ttu-id="6ba3c-173">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-173">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-174">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-174">Type</span></span> | <span data-ttu-id="6ba3c-175">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-175">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-176">**구분 기호**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-176">**separator**</span></span> |<span data-ttu-id="6ba3c-177">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-177">Required</span></span> |<span data-ttu-id="6ba3c-178">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-178">String</span></span> |<span data-ttu-id="6ba3c-179">문자열을 하나의 문자열로 연결할 때 tooseparate 소스 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-179">String used tooseparate source values when they are concatenated into one string.</span></span> <span data-ttu-id="6ba3c-180">구분 기호가 필요하지 않은 경우 ""일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-180">Can be "" if no separator is required.</span></span> |
| <span data-ttu-id="6ba3c-181">**source1  …</span><span class="sxs-lookup"><span data-stu-id="6ba3c-181">**source1  …</span></span> <span data-ttu-id="6ba3c-182">sourceN **</span><span class="sxs-lookup"><span data-stu-id="6ba3c-182">sourceN **</span></span> |<span data-ttu-id="6ba3c-183">필수, 시간 변수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-183">Required, variable-number of times</span></span> |<span data-ttu-id="6ba3c-184">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-184">String</span></span> |<span data-ttu-id="6ba3c-185">문자열 값 toobe 함께 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-185">String values toobe joined together.</span></span> |

- - -
### <a name="mid"></a><span data-ttu-id="6ba3c-186">Mid</span><span class="sxs-lookup"><span data-stu-id="6ba3c-186">Mid</span></span>
<span data-ttu-id="6ba3c-187">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-187">**Function:**</span></span><br> <span data-ttu-id="6ba3c-188">Mid(source, start, length)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-188">Mid(source, start, length)</span></span>

<span data-ttu-id="6ba3c-189">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-189">**Description:**</span></span><br> <span data-ttu-id="6ba3c-190">Hello 소스 값의 부분 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-190">Returns a substring of hello source value.</span></span> <span data-ttu-id="6ba3c-191">부분 문자열은 hello 소스 문자열에서 문자를 hello 중 일부만 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-191">A substring is a string that contains only some of hello characters from hello source string.</span></span>

<span data-ttu-id="6ba3c-192">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-192">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-193">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-193">Name</span></span> | <span data-ttu-id="6ba3c-194">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-194">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-195">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-195">Type</span></span> | <span data-ttu-id="6ba3c-196">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-196">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-197">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-197">**source**</span></span> |<span data-ttu-id="6ba3c-198">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-198">Required</span></span> |<span data-ttu-id="6ba3c-199">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-199">String</span></span> |<span data-ttu-id="6ba3c-200">일반적으로 이름 사용 하 여 hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-200">Usually name of hello attribute.</span></span> |
| <span data-ttu-id="6ba3c-201">**시작**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-201">**start**</span></span> |<span data-ttu-id="6ba3c-202">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-202">Required</span></span> |<span data-ttu-id="6ba3c-203">정수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-203">integer</span></span> |<span data-ttu-id="6ba3c-204">Hello에서 인덱스 **소스** 하위 문자열이 시작 되어야 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-204">Index in hello **source** string where substring should start.</span></span> <span data-ttu-id="6ba3c-205">Hello 문자열의 첫 번째 문자를 갖게 됩니다 인덱스 1의 두 번째 문자 인덱스 2가 되며 등.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-205">First character in hello string will have index of 1, second character will have index 2, and so on.</span></span> |
| <span data-ttu-id="6ba3c-206">**length**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-206">**length**</span></span> |<span data-ttu-id="6ba3c-207">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-207">Required</span></span> |<span data-ttu-id="6ba3c-208">정수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-208">integer</span></span> |<span data-ttu-id="6ba3c-209">Hello 부분 문자열의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-209">Length of hello substring.</span></span> <span data-ttu-id="6ba3c-210">길이 외부 hello 종료 되 면 **소스** 문자열 함수에서 부분 문자열을 반환 합니다 **시작** 인덱스의 끝까지 **소스** 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-210">If length ends outside hello **source** string, function will return substring from **start** index till end of **source** string.</span></span> |

- - -
### <a name="not"></a><span data-ttu-id="6ba3c-211">not</span><span class="sxs-lookup"><span data-stu-id="6ba3c-211">Not</span></span>
<span data-ttu-id="6ba3c-212">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-212">**Function:**</span></span><br> <span data-ttu-id="6ba3c-213">Not(source)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-213">Not(source)</span></span>

<span data-ttu-id="6ba3c-214">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-214">**Description:**</span></span><br> <span data-ttu-id="6ba3c-215">대칭 hello의 부울 값을 hello **소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-215">Flips hello boolean value of hello **source**.</span></span> <span data-ttu-id="6ba3c-216">**원본** 값이 "*True*"인 경우 "*False*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-216">If **source** value is "*True*", returns "*False*".</span></span> <span data-ttu-id="6ba3c-217">그렇지 않은 경우 "*True*"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-217">Otherwise, returns "*True*".</span></span>

<span data-ttu-id="6ba3c-218">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-218">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-219">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-219">Name</span></span> | <span data-ttu-id="6ba3c-220">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-220">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-221">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-221">Type</span></span> | <span data-ttu-id="6ba3c-222">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-222">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-223">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-223">**source**</span></span> |<span data-ttu-id="6ba3c-224">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-224">Required</span></span> |<span data-ttu-id="6ba3c-225">부울 문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-225">Boolean String</span></span> |<span data-ttu-id="6ba3c-226">예상 **원본** 값은 "True" 또는 "False"입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-226">Expected **source** values are "True" or "False"..</span></span> |

- - -
### <a name="replace"></a><span data-ttu-id="6ba3c-227">Replace</span><span class="sxs-lookup"><span data-stu-id="6ba3c-227">Replace</span></span>
<span data-ttu-id="6ba3c-228">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-228">**Function:**</span></span><br> <span data-ttu-id="6ba3c-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-229">ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)</span></span>

<span data-ttu-id="6ba3c-230">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-230">**Description:**</span></span><br>
<span data-ttu-id="6ba3c-231">문자열 내 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-231">Replaces values within a string.</span></span> <span data-ttu-id="6ba3c-232">제공 하는 hello 매개 변수에 따라 다르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-232">It works differently depending on hello parameters provided:</span></span>

* <span data-ttu-id="6ba3c-233">**oldValue** 및 **replacementValue**가 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ba3c-233">When **oldValue** and **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="6ba3c-234">OldValue hello 소스에 나타나는 모든 replacementValue 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-234">Replaces all occurrences of oldValue in hello source  with replacementValue</span></span>
* <span data-ttu-id="6ba3c-235">**oldValue** 및 **template**이 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ba3c-235">When **oldValue** and **template** are provided:</span></span>
  
  * <span data-ttu-id="6ba3c-236">Hello을 모두 바꿉니다 **oldValue** hello에 **템플릿** hello로 **소스** 값</span><span class="sxs-lookup"><span data-stu-id="6ba3c-236">Replaces all occurrences of hello **oldValue** in hello **template** with hello **source** value</span></span>
* <span data-ttu-id="6ba3c-237">**oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue**가 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ba3c-237">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue** are provided:</span></span>
  
  * <span data-ttu-id="6ba3c-238">OldValueRegexPattern replacementValue 사용 hello 원본 문자열에 일치 하는 모든 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-238">Replaces all values matching oldValueRegexPattern in hello source string with replacementValue</span></span>
* <span data-ttu-id="6ba3c-239">**oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName**이 제공되는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ba3c-239">When **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** are provided:</span></span>
  
  * <span data-ttu-id="6ba3c-240">**원본**에 값이 있는 경우 **원본**이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-240">If **source** has value, **source** is returned</span></span>
  * <span data-ttu-id="6ba3c-241">경우 **소스** 값이 없는 사용 하 여 **oldValueRegexPattern** 및 **oldValueRegexGroupName** tooextract 대체 값으로 hello 속성에서  **replacementPropertyName**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-241">If **source** has no value, uses **oldValueRegexPattern** and **oldValueRegexGroupName** tooextract replacement value from hello property with **replacementPropertyName**.</span></span> <span data-ttu-id="6ba3c-242">대체 값 hello 결과로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-242">Replacement value is returned as hello result</span></span>

<span data-ttu-id="6ba3c-243">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-243">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-244">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-244">Name</span></span> | <span data-ttu-id="6ba3c-245">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-245">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-246">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-246">Type</span></span> | <span data-ttu-id="6ba3c-247">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-247">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-248">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-248">**source**</span></span> |<span data-ttu-id="6ba3c-249">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-249">Required</span></span> |<span data-ttu-id="6ba3c-250">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-250">String</span></span> |<span data-ttu-id="6ba3c-251">일반적으로 이름 사용 하 여 hello 원본 개체에서 hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-251">Usually name of hello attribute from hello source object.</span></span> |
| <span data-ttu-id="6ba3c-252">**oldValue**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-252">**oldValue**</span></span> |<span data-ttu-id="6ba3c-253">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-253">Optional</span></span> |<span data-ttu-id="6ba3c-254">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-254">String</span></span> |<span data-ttu-id="6ba3c-255">대체 toobe 값 **소스** 또는 **템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-255">Value toobe replaced in **source** or **template**.</span></span> |
| <span data-ttu-id="6ba3c-256">**regexPattern**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-256">**regexPattern**</span></span> |<span data-ttu-id="6ba3c-257">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-257">Optional</span></span> |<span data-ttu-id="6ba3c-258">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-258">String</span></span> |<span data-ttu-id="6ba3c-259">Regex 패턴에서 대체 hello 값 toobe입니다 **소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-259">Regex pattern for hello value toobe replaced in **source**.</span></span> <span data-ttu-id="6ba3c-260">또는 replacementPropertyName이 사용 된 경우 tooextract 값 대체 속성의 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-260">Or, when replacementPropertyName is used, pattern tooextract value from replacement property.</span></span> |
| <span data-ttu-id="6ba3c-261">**regexGroupName**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-261">**regexGroupName**</span></span> |<span data-ttu-id="6ba3c-262">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-262">Optional</span></span> |<span data-ttu-id="6ba3c-263">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-263">String</span></span> |<span data-ttu-id="6ba3c-264">내부 hello 그룹의 이름 **regexPattern**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-264">Name of hello group inside **regexPattern**.</span></span> <span data-ttu-id="6ba3c-265">replacementPropertyName를 사용하는 경우에만 replacement 속성에서 replacementValue로 이 그룹의 값을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-265">Only when  replacementPropertyName is used, we will extract value of this group as replacementValue from replacement property.</span></span> |
| <span data-ttu-id="6ba3c-266">**replacementValue**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-266">**replacementValue**</span></span> |<span data-ttu-id="6ba3c-267">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-267">Optional</span></span> |<span data-ttu-id="6ba3c-268">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-268">String</span></span> |<span data-ttu-id="6ba3c-269">새 값 tooreplace 이전과 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-269">New value tooreplace old one with.</span></span> |
| <span data-ttu-id="6ba3c-270">**replacementAttributeName**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-270">**replacementAttributeName**</span></span> |<span data-ttu-id="6ba3c-271">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-271">Optional</span></span> |<span data-ttu-id="6ba3c-272">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-272">String</span></span> |<span data-ttu-id="6ba3c-273">소스에 값이 없으면 대체 값에 사용 되는 hello 특성 toobe의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-273">Name of hello attribute toobe used for replacement value, when source has no value.</span></span> |
| <span data-ttu-id="6ba3c-274">**template**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-274">**template**</span></span> |<span data-ttu-id="6ba3c-275">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-275">Optional</span></span> |<span data-ttu-id="6ba3c-276">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-276">String</span></span> |<span data-ttu-id="6ba3c-277">때 **템플릿** 값이 제공을 볼 수에 대 한 **oldValue** 내부 템플릿을 hello와 소스 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-277">When **template** value is provided, we will look for **oldValue** inside hello template and replace it with source value.</span></span> |

- - -
### <a name="stripspaces"></a><span data-ttu-id="6ba3c-278">StripSpaces</span><span class="sxs-lookup"><span data-stu-id="6ba3c-278">StripSpaces</span></span>
<span data-ttu-id="6ba3c-279">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-279">**Function:**</span></span><br> <span data-ttu-id="6ba3c-280">StripSpaces(source)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-280">StripSpaces(source)</span></span>

<span data-ttu-id="6ba3c-281">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-281">**Description:**</span></span><br> <span data-ttu-id="6ba3c-282">모든 공백을 제거 ("") 문자 hello에서 원본 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-282">Removes all space (" ") characters from hello source string.</span></span>

<span data-ttu-id="6ba3c-283">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-283">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-284">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-284">Name</span></span> | <span data-ttu-id="6ba3c-285">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-285">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-286">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-286">Type</span></span> | <span data-ttu-id="6ba3c-287">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-287">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-288">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-288">**source**</span></span> |<span data-ttu-id="6ba3c-289">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-289">Required</span></span> |<span data-ttu-id="6ba3c-290">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-290">String</span></span> |<span data-ttu-id="6ba3c-291">**소스** 값 tooupdate 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-291">**source** value tooupdate.</span></span> |

- - -
### <a name="switch"></a><span data-ttu-id="6ba3c-292">Switch</span><span class="sxs-lookup"><span data-stu-id="6ba3c-292">Switch</span></span>
<span data-ttu-id="6ba3c-293">**함수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-293">**Function:**</span></span><br> <span data-ttu-id="6ba3c-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span><span class="sxs-lookup"><span data-stu-id="6ba3c-294">Switch(source, defaultValue, key1, value1, key2, value2, …)</span></span>

<span data-ttu-id="6ba3c-295">**설명:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-295">**Description:**</span></span><br> <span data-ttu-id="6ba3c-296">**원본** 값이 **key**와 일치하면, 해당 **key**의 **value**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-296">When **source** value matches a **key**, returns **value** for that **key**.</span></span> <span data-ttu-id="6ba3c-297">**원본** 값과 일치하는 키가 없으면 **defaultValue**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-297">If **source** value doesn't match any keys, returns **defaultValue**.</span></span>  <span data-ttu-id="6ba3c-298">**Key** 및 **value** 매개 변수는 항상 쌍으로 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-298">**Key** and **value** parameters must always come in pairs.</span></span> <span data-ttu-id="6ba3c-299">hello 함수는 항상 짝수 개수의 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-299">hello function always expects an even number of parameters.</span></span>

<span data-ttu-id="6ba3c-300">**매개 변수:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-300">**Parameters:**</span></span><br> 

| <span data-ttu-id="6ba3c-301">이름</span><span class="sxs-lookup"><span data-stu-id="6ba3c-301">Name</span></span> | <span data-ttu-id="6ba3c-302">필수/ 반복</span><span class="sxs-lookup"><span data-stu-id="6ba3c-302">Required/ Repeating</span></span> | <span data-ttu-id="6ba3c-303">형식</span><span class="sxs-lookup"><span data-stu-id="6ba3c-303">Type</span></span> | <span data-ttu-id="6ba3c-304">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ba3c-304">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ba3c-305">**원본**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-305">**source**</span></span> |<span data-ttu-id="6ba3c-306">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-306">Required</span></span> |<span data-ttu-id="6ba3c-307">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-307">String</span></span> |<span data-ttu-id="6ba3c-308">**소스** 값 tooupdate 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-308">**Source** value tooupdate.</span></span> |
| <span data-ttu-id="6ba3c-309">**defaultValue**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-309">**defaultValue**</span></span> |<span data-ttu-id="6ba3c-310">옵션</span><span class="sxs-lookup"><span data-stu-id="6ba3c-310">Optional</span></span> |<span data-ttu-id="6ba3c-311">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-311">String</span></span> |<span data-ttu-id="6ba3c-312">기본 값 toobe 소스 모든 키와도 일치 하지 않는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-312">Default value toobe used when source doesn't match any keys.</span></span> <span data-ttu-id="6ba3c-313">빈 문자열("")일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-313">Can be empty string ("").</span></span> |
| <span data-ttu-id="6ba3c-314">**key**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-314">**key**</span></span> |<span data-ttu-id="6ba3c-315">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-315">Required</span></span> |<span data-ttu-id="6ba3c-316">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-316">String</span></span> |<span data-ttu-id="6ba3c-317">**키** toocompare **소스** 를 갖는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-317">**Key** toocompare **source** value with.</span></span> |
| <span data-ttu-id="6ba3c-318">**값**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-318">**value**</span></span> |<span data-ttu-id="6ba3c-319">필수</span><span class="sxs-lookup"><span data-stu-id="6ba3c-319">Required</span></span> |<span data-ttu-id="6ba3c-320">문자열</span><span class="sxs-lookup"><span data-stu-id="6ba3c-320">String</span></span> |<span data-ttu-id="6ba3c-321">Hello에 대 한 대체 값 **소스** 일치 하는 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-321">Replacement value for hello **source** matching hello key.</span></span> |

## <a name="examples"></a><span data-ttu-id="6ba3c-322">예</span><span class="sxs-lookup"><span data-stu-id="6ba3c-322">Examples</span></span>
### <a name="strip-known-domain-name"></a><span data-ttu-id="6ba3c-323">알려진 도메인 이름 제거</span><span class="sxs-lookup"><span data-stu-id="6ba3c-323">Strip known domain name</span></span>
<span data-ttu-id="6ba3c-324">사용자의 전자 메일 tooobtain 사용자 이름에서에서 알려진된 도메인 이름을 toostrip이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-324">You need toostrip a known domain name from a user’s email tooobtain a user name.</span></span> <br>
<span data-ttu-id="6ba3c-325">예를 들어 hello 도메인이 "contoso.com" 인 경우 hello 다음 식은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-325">For example, if hello domain is "contoso.com", then you could use hello following expression:</span></span>

<span data-ttu-id="6ba3c-326">**식:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-326">**Expression:**</span></span> <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

<span data-ttu-id="6ba3c-327">**샘플 입출력:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-327">**Sample input / output:**</span></span> <br>

* <span data-ttu-id="6ba3c-328">**입력**(메일): “john.doe@contoso.com”</span><span class="sxs-lookup"><span data-stu-id="6ba3c-328">**INPUT** (mail): "john.doe@contoso.com"</span></span>
* <span data-ttu-id="6ba3c-329">**출력**: "john.doe"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-329">**OUTPUT**:  "john.doe"</span></span>

### <a name="append-constant-suffix-toouser-name"></a><span data-ttu-id="6ba3c-330">Toouser 이름을 상수 접미사 추가</span><span class="sxs-lookup"><span data-stu-id="6ba3c-330">Append constant suffix toouser name</span></span>
<span data-ttu-id="6ba3c-331">Salesforce 샌드박스를 사용 하는 경우 해야 tooappend 추가 접미사 tooall 사용자 이름을 동기화 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-331">If you are using a Salesforce Sandbox, you might need tooappend an additional suffix tooall your user names before synchronizing them.</span></span>

<span data-ttu-id="6ba3c-332">**식:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-332">**Expression:**</span></span> <br>
`Append([userPrincipalName], ".test"))`

<span data-ttu-id="6ba3c-333">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-333">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="6ba3c-334">**입력**: (userPrincipalName): “John.Doe@contoso.com”</span><span class="sxs-lookup"><span data-stu-id="6ba3c-334">**INPUT**: (userPrincipalName): "John.Doe@contoso.com"</span></span>
* <span data-ttu-id="6ba3c-335">**출력**:  “John.Doe@contoso.com.test”</span><span class="sxs-lookup"><span data-stu-id="6ba3c-335">**OUTPUT**:  "John.Doe@contoso.com.test"</span></span>

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a><span data-ttu-id="6ba3c-336">이름과 성의 부분을 연결하여 사용자 별칭을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-336">Generate user alias by concatenating parts of first and last name</span></span>
<span data-ttu-id="6ba3c-337">사용자의 이름 중 처음 3 문자 및 사용자의 성 처음 5 개 문자를 수행 하 여 사용자 별칭 toogenerate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-337">You need toogenerate a user alias by taking first 3 letters of user's first name and first 5 letters of user's last name.</span></span>

<span data-ttu-id="6ba3c-338">**식:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-338">**Expression:**</span></span> <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

<span data-ttu-id="6ba3c-339">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-339">**Sample input/output:**</span></span> <br>

* <span data-ttu-id="6ba3c-340">**입력** (givenName): "John"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-340">**INPUT** (givenName): "John"</span></span>
* <span data-ttu-id="6ba3c-341">**입력** (surname): "Doe"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-341">**INPUT** (surname): "Doe"</span></span>
* <span data-ttu-id="6ba3c-342">**출력**: "JohDoe"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-342">**OUTPUT**:  "JohDoe"</span></span>

### <a name="output-date-as-a-string-in-a-certain-format"></a><span data-ttu-id="6ba3c-343">특정 형식에서 문자열로 출력 날짜</span><span class="sxs-lookup"><span data-stu-id="6ba3c-343">Output date as a string in a certain format</span></span>
<span data-ttu-id="6ba3c-344">원하는 toosend 날짜 tooa SaaS 응용 프로그램 특정 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-344">You want toosend dates tooa SaaS application in a certain format.</span></span> <br>
<span data-ttu-id="6ba3c-345">예를 들어 ServiceNow에 대 한 tooformat 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-345">For example, you want tooformat dates for ServiceNow.</span></span>

<span data-ttu-id="6ba3c-346">**식:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-346">**Expression:**</span></span> <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

<span data-ttu-id="6ba3c-347">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-347">**Sample input/output:**</span></span>

* <span data-ttu-id="6ba3c-348">**입력** (extensionAttribute1): "20150123105347.1Z"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-348">**INPUT** (extensionAttribute1): "20150123105347.1Z"</span></span>
* <span data-ttu-id="6ba3c-349">**출력**: “2015-01-23”</span><span class="sxs-lookup"><span data-stu-id="6ba3c-349">**OUTPUT**:  "2015-01-23"</span></span>

### <a name="replace-a-value-based-on-predefined-set-of-options"></a><span data-ttu-id="6ba3c-350">미리 정의된 옵션 집합을 기반으로 값 바꾸기</span><span class="sxs-lookup"><span data-stu-id="6ba3c-350">Replace a value based on predefined set of options</span></span>
<span data-ttu-id="6ba3c-351">Azure AD에 저장 된 hello 상태 코드를 기반으로 하는 hello 사용자의 toodefine hello 표준 시간대 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-351">You need toodefine hello time zone of hello user based on hello state code stored in Azure AD.</span></span> <br>
<span data-ttu-id="6ba3c-352">Hello 상태 코드는 미리 정의 된 hello 옵션 중 하나는 일치 하지 않으면, "Australia/Sydney"의 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba3c-352">If hello state code doesn't match any of hello predefined options, use default value of "Australia/Sydney".</span></span>

<span data-ttu-id="6ba3c-353">**식:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-353">**Expression:**</span></span> <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

<span data-ttu-id="6ba3c-354">**샘플 입/출력:**</span><span class="sxs-lookup"><span data-stu-id="6ba3c-354">**Sample input/output:**</span></span>

* <span data-ttu-id="6ba3c-355">**입력** (상태): "QLD"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-355">**INPUT** (state): "QLD"</span></span>
* <span data-ttu-id="6ba3c-356">**출력**: "오스트레일리아/브리즈번"</span><span class="sxs-lookup"><span data-stu-id="6ba3c-356">**OUTPUT**: "Australia/Brisbane"</span></span>

## <a name="related-articles"></a><span data-ttu-id="6ba3c-357">관련 문서</span><span class="sxs-lookup"><span data-stu-id="6ba3c-357">Related Articles</span></span>
* [<span data-ttu-id="6ba3c-358">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="6ba3c-358">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6ba3c-359">사용자 프로 비전/프로 비전 해제 tooSaaS 응용 프로그램 자동화</span><span class="sxs-lookup"><span data-stu-id="6ba3c-359">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="6ba3c-360">사용자 프로비저닝에 대한 특성 매핑 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6ba3c-360">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="6ba3c-361">사용자 프로 비전에 대 한 필터 범위 지정</span><span class="sxs-lookup"><span data-stu-id="6ba3c-361">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="6ba3c-362">SCIM tooenable 자동으로 프로 tooapplications Azure Active Directory에서에서 사용자 및 그룹을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6ba3c-362">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="6ba3c-363">계정 프로비전 알림</span><span class="sxs-lookup"><span data-stu-id="6ba3c-363">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="6ba3c-364">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱</span><span class="sxs-lookup"><span data-stu-id="6ba3c-364">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

