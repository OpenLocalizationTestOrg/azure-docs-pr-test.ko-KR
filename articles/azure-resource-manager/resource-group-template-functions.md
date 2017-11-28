---
title: "관리자 템플릿 함수 aaaResource | Microsoft Docs"
description: "Hello 함수 toouse 설명 Azure 리소스 관리자 템플릿 tooretrieve 값에서 문자열 및 숫자를 사용 하 고 배포 정보를 검색 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="e2b8b-103">Azure Resource Manager 템플릿 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="e2b8b-104">이 항목에서는 Azure Resource Manager 템플릿에 사용 가능한 모든 hello 함수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="e2b8b-105">`[` 및 `]` 각각 대괄호로 묶어서 템플릿에서 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="e2b8b-106">배포 하는 동안 hello 식이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="e2b8b-107">문자열 리터럴로 작성 하는 동안 다른 JSON 등의 형식, 배열, 개체 또는 정수 hello 식의 계산 결과 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="e2b8b-108">JavaScript에서와 마찬가지로 함수 호출은 `functionName(arg1,arg2,arg3)`과 같이 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="e2b8b-109">Hello 점 및 [index] 연산자를 사용 하 여 속성을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="e2b8b-110">템플릿 식은 24,576자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="e2b8b-111">템플릿 함수 및 해당 매개 변수는 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="e2b8b-112">예를 들어 리소스 관리자는 해결 **variables('var1')** 및 **VARIABLES('VAR1')** 대로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="e2b8b-113">평가 시 hello 함수 (예: toUpper 또는 toLower) 대/소문자를 명시적으로 수정 하지 않는 한 hello 함수 hello 대/소문자를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="e2b8b-114">특정 리소스 유형에는 함수가 계산되는 방식에 관계없이 대/소문자 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="e2b8b-115">배열 및 개체 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-115">Array and object functions</span></span>
<span data-ttu-id="e2b8b-116">Resource Manager는 배열 및 개체 작업을 위한 여러 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="e2b8b-117">array</span><span class="sxs-lookup"><span data-stu-id="e2b8b-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="e2b8b-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="e2b8b-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="e2b8b-119">concat</span><span class="sxs-lookup"><span data-stu-id="e2b8b-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="e2b8b-120">contains</span><span class="sxs-lookup"><span data-stu-id="e2b8b-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="e2b8b-121">createArray</span><span class="sxs-lookup"><span data-stu-id="e2b8b-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="e2b8b-122">empty</span><span class="sxs-lookup"><span data-stu-id="e2b8b-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="e2b8b-123">first</span><span class="sxs-lookup"><span data-stu-id="e2b8b-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="e2b8b-124">intersection</span><span class="sxs-lookup"><span data-stu-id="e2b8b-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="e2b8b-125">json</span><span class="sxs-lookup"><span data-stu-id="e2b8b-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="e2b8b-126">last</span><span class="sxs-lookup"><span data-stu-id="e2b8b-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="e2b8b-127">length</span><span class="sxs-lookup"><span data-stu-id="e2b8b-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="e2b8b-128">min</span><span class="sxs-lookup"><span data-stu-id="e2b8b-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="e2b8b-129">max</span><span class="sxs-lookup"><span data-stu-id="e2b8b-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="e2b8b-130">range</span><span class="sxs-lookup"><span data-stu-id="e2b8b-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="e2b8b-131">skip</span><span class="sxs-lookup"><span data-stu-id="e2b8b-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="e2b8b-132">take</span><span class="sxs-lookup"><span data-stu-id="e2b8b-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="e2b8b-133">union</span><span class="sxs-lookup"><span data-stu-id="e2b8b-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="e2b8b-134">비교 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-134">Comparison functions</span></span>
<span data-ttu-id="e2b8b-135">Resource Manager는 템플릿에서 비교를 수행하기 위한 몇 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="e2b8b-136">equals</span><span class="sxs-lookup"><span data-stu-id="e2b8b-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="e2b8b-137">less</span><span class="sxs-lookup"><span data-stu-id="e2b8b-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="e2b8b-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="e2b8b-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="e2b8b-139">greater</span><span class="sxs-lookup"><span data-stu-id="e2b8b-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="e2b8b-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="e2b8b-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="e2b8b-141">배포 값 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-141">Deployment value functions</span></span>
<span data-ttu-id="e2b8b-142">리소스 관리자는 hello 다음 hello 서식 파일의 섹션에서 값 가져오기에 대 한 함수 및 관련된 toohello 배포 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="e2b8b-143">deployment</span><span class="sxs-lookup"><span data-stu-id="e2b8b-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="e2b8b-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="e2b8b-145">variables</span><span class="sxs-lookup"><span data-stu-id="e2b8b-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="e2b8b-146">논리 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-146">Logical functions</span></span>
<span data-ttu-id="e2b8b-147">리소스 관리자 hello를 다음 논리 조건 작업에 대 한 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="e2b8b-148">and</span><span class="sxs-lookup"><span data-stu-id="e2b8b-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="e2b8b-149">bool</span><span class="sxs-lookup"><span data-stu-id="e2b8b-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="e2b8b-150">if</span><span class="sxs-lookup"><span data-stu-id="e2b8b-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="e2b8b-151">not</span><span class="sxs-lookup"><span data-stu-id="e2b8b-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="e2b8b-152">or</span><span class="sxs-lookup"><span data-stu-id="e2b8b-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="e2b8b-153">숫자 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-153">Numeric functions</span></span>
<span data-ttu-id="e2b8b-154">리소스 관리자 hello를 뒤 정수가 포함 된 작업에 대 한 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="e2b8b-155">추가</span><span class="sxs-lookup"><span data-stu-id="e2b8b-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="e2b8b-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="e2b8b-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="e2b8b-157">div</span><span class="sxs-lookup"><span data-stu-id="e2b8b-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="e2b8b-158">float</span><span class="sxs-lookup"><span data-stu-id="e2b8b-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="e2b8b-159">int</span><span class="sxs-lookup"><span data-stu-id="e2b8b-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="e2b8b-160">min</span><span class="sxs-lookup"><span data-stu-id="e2b8b-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="e2b8b-161">max</span><span class="sxs-lookup"><span data-stu-id="e2b8b-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="e2b8b-162">mod</span><span class="sxs-lookup"><span data-stu-id="e2b8b-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="e2b8b-163">mul</span><span class="sxs-lookup"><span data-stu-id="e2b8b-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="e2b8b-164">sub</span><span class="sxs-lookup"><span data-stu-id="e2b8b-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="e2b8b-165">리소스 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-165">Resource functions</span></span>
<span data-ttu-id="e2b8b-166">리소스 관리자 리소스 값을 가져오고이 대 한 함수를 수행 하는 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="e2b8b-167">listKeys 및 list{Value}</span><span class="sxs-lookup"><span data-stu-id="e2b8b-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="e2b8b-168">providers</span><span class="sxs-lookup"><span data-stu-id="e2b8b-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="e2b8b-169">reference</span><span class="sxs-lookup"><span data-stu-id="e2b8b-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="e2b8b-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2b8b-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="e2b8b-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="e2b8b-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="e2b8b-172">subscription</span><span class="sxs-lookup"><span data-stu-id="e2b8b-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="e2b8b-173">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="e2b8b-173">String functions</span></span>
<span data-ttu-id="e2b8b-174">리소스 관리자는 다음 문자열 작업에 대 한 함수 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b8b-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="e2b8b-175">base64</span><span class="sxs-lookup"><span data-stu-id="e2b8b-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="e2b8b-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="e2b8b-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="e2b8b-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="e2b8b-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="e2b8b-178">concat</span><span class="sxs-lookup"><span data-stu-id="e2b8b-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="e2b8b-179">contains</span><span class="sxs-lookup"><span data-stu-id="e2b8b-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="e2b8b-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="e2b8b-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="e2b8b-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="e2b8b-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="e2b8b-182">empty</span><span class="sxs-lookup"><span data-stu-id="e2b8b-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="e2b8b-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="e2b8b-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="e2b8b-184">first</span><span class="sxs-lookup"><span data-stu-id="e2b8b-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="e2b8b-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="e2b8b-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="e2b8b-186">last</span><span class="sxs-lookup"><span data-stu-id="e2b8b-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="e2b8b-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="e2b8b-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="e2b8b-188">length</span><span class="sxs-lookup"><span data-stu-id="e2b8b-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="e2b8b-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="e2b8b-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="e2b8b-190">replace</span><span class="sxs-lookup"><span data-stu-id="e2b8b-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="e2b8b-191">skip</span><span class="sxs-lookup"><span data-stu-id="e2b8b-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="e2b8b-192">분할</span><span class="sxs-lookup"><span data-stu-id="e2b8b-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="e2b8b-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="e2b8b-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="e2b8b-194">string</span><span class="sxs-lookup"><span data-stu-id="e2b8b-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="e2b8b-195">substring</span><span class="sxs-lookup"><span data-stu-id="e2b8b-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="e2b8b-196">take</span><span class="sxs-lookup"><span data-stu-id="e2b8b-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="e2b8b-197">toLower</span><span class="sxs-lookup"><span data-stu-id="e2b8b-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="e2b8b-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="e2b8b-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="e2b8b-199">trim</span><span class="sxs-lookup"><span data-stu-id="e2b8b-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="e2b8b-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="e2b8b-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="e2b8b-201">uri</span><span class="sxs-lookup"><span data-stu-id="e2b8b-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="e2b8b-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="e2b8b-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="e2b8b-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="e2b8b-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="e2b8b-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2b8b-204">Next steps</span></span>
* <span data-ttu-id="e2b8b-205">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="e2b8b-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="e2b8b-206">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="e2b8b-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="e2b8b-207">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="e2b8b-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="e2b8b-208">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="e2b8b-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

