---
title: "Resource Manager 템플릿 함수 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 값을 검색하고 문자열과 숫자로 작업하며 배포 정보를 검색하는 데 사용하는 함수를 설명합니다."
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
ms.openlocfilehash: 1324bed07e991e9d84cb6832afe78bdb2d3348fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="41027-103">Azure Resource Manager 템플릿 함수</span><span class="sxs-lookup"><span data-stu-id="41027-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="41027-104">이 항목에서는 Azure Resource Manager 템플릿에서 사용할 수 있는 모든 함수에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="41027-105">`[` 및 `]` 각각 대괄호로 묶어서 템플릿에서 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="41027-106">배포하는 동안 식이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="41027-106">The expression is evaluated during deployment.</span></span> <span data-ttu-id="41027-107">문자열 리터럴로 작성되지만 식의 평가 결과는 다른 JSON 형식(예: 배열, 개체 또는 정수)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41027-107">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="41027-108">JavaScript에서와 마찬가지로 함수 호출은 `functionName(arg1,arg2,arg3)`과 같이 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="41027-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="41027-109">점과 [인덱스] 연산자를 사용하여 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41027-109">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="41027-110">템플릿 식은 24,576자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41027-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="41027-111">템플릿 함수 및 해당 매개 변수는 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41027-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="41027-112">예를 들어 Resource Manager에서 **variables('var1')**와 **VARIABLES('VAR1')**는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="41027-113">계산될 때 함수는 대/소문자를 명시적으로 수정하지 않는 한(toUpper 또는 toLower 등) 대/소문자를 보존합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-113">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="41027-114">특정 리소스 유형에는 함수가 계산되는 방식에 관계없이 대/소문자 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41027-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

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

## <a name="array-and-object-functions"></a><span data-ttu-id="41027-115">배열 및 개체 함수</span><span class="sxs-lookup"><span data-stu-id="41027-115">Array and object functions</span></span>
<span data-ttu-id="41027-116">Resource Manager는 배열 및 개체 작업을 위한 여러 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="41027-117">array</span><span class="sxs-lookup"><span data-stu-id="41027-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="41027-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="41027-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="41027-119">concat</span><span class="sxs-lookup"><span data-stu-id="41027-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="41027-120">contains</span><span class="sxs-lookup"><span data-stu-id="41027-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="41027-121">createArray</span><span class="sxs-lookup"><span data-stu-id="41027-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="41027-122">empty</span><span class="sxs-lookup"><span data-stu-id="41027-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="41027-123">first</span><span class="sxs-lookup"><span data-stu-id="41027-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="41027-124">intersection</span><span class="sxs-lookup"><span data-stu-id="41027-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="41027-125">json</span><span class="sxs-lookup"><span data-stu-id="41027-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="41027-126">last</span><span class="sxs-lookup"><span data-stu-id="41027-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="41027-127">length</span><span class="sxs-lookup"><span data-stu-id="41027-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="41027-128">min</span><span class="sxs-lookup"><span data-stu-id="41027-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="41027-129">max</span><span class="sxs-lookup"><span data-stu-id="41027-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="41027-130">range</span><span class="sxs-lookup"><span data-stu-id="41027-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="41027-131">skip</span><span class="sxs-lookup"><span data-stu-id="41027-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="41027-132">take</span><span class="sxs-lookup"><span data-stu-id="41027-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="41027-133">union</span><span class="sxs-lookup"><span data-stu-id="41027-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="41027-134">비교 함수</span><span class="sxs-lookup"><span data-stu-id="41027-134">Comparison functions</span></span>
<span data-ttu-id="41027-135">Resource Manager는 템플릿에서 비교를 수행하기 위한 몇 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="41027-136">equals</span><span class="sxs-lookup"><span data-stu-id="41027-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="41027-137">less</span><span class="sxs-lookup"><span data-stu-id="41027-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="41027-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="41027-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="41027-139">greater</span><span class="sxs-lookup"><span data-stu-id="41027-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="41027-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="41027-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="41027-141">배포 값 함수</span><span class="sxs-lookup"><span data-stu-id="41027-141">Deployment value functions</span></span>
<span data-ttu-id="41027-142">Resource Manager는 템플릿의 섹션에서 값을 가져오고 배포와 관련된 값을 가져오기 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-142">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="41027-143">deployment</span><span class="sxs-lookup"><span data-stu-id="41027-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="41027-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="41027-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="41027-145">variables</span><span class="sxs-lookup"><span data-stu-id="41027-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a><span data-ttu-id="41027-146">논리 함수</span><span class="sxs-lookup"><span data-stu-id="41027-146">Logical functions</span></span>
<span data-ttu-id="41027-147">Resource Manager는 논리 조건 사용을 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-147">Resource Manager provides the following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="41027-148">and</span><span class="sxs-lookup"><span data-stu-id="41027-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="41027-149">bool</span><span class="sxs-lookup"><span data-stu-id="41027-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="41027-150">if</span><span class="sxs-lookup"><span data-stu-id="41027-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="41027-151">not</span><span class="sxs-lookup"><span data-stu-id="41027-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="41027-152">or</span><span class="sxs-lookup"><span data-stu-id="41027-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="41027-153">숫자 함수</span><span class="sxs-lookup"><span data-stu-id="41027-153">Numeric functions</span></span>
<span data-ttu-id="41027-154">Resource Manager는 정수 작업을 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-154">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="41027-155">추가</span><span class="sxs-lookup"><span data-stu-id="41027-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="41027-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="41027-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="41027-157">div</span><span class="sxs-lookup"><span data-stu-id="41027-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="41027-158">float</span><span class="sxs-lookup"><span data-stu-id="41027-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="41027-159">int</span><span class="sxs-lookup"><span data-stu-id="41027-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="41027-160">min</span><span class="sxs-lookup"><span data-stu-id="41027-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="41027-161">max</span><span class="sxs-lookup"><span data-stu-id="41027-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="41027-162">mod</span><span class="sxs-lookup"><span data-stu-id="41027-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="41027-163">mul</span><span class="sxs-lookup"><span data-stu-id="41027-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="41027-164">sub</span><span class="sxs-lookup"><span data-stu-id="41027-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="41027-165">리소스 함수</span><span class="sxs-lookup"><span data-stu-id="41027-165">Resource functions</span></span>
<span data-ttu-id="41027-166">Resource Manager는 리소스 값을 가져오기 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-166">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="41027-167">listKeys 및 list{Value}</span><span class="sxs-lookup"><span data-stu-id="41027-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="41027-168">providers</span><span class="sxs-lookup"><span data-stu-id="41027-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="41027-169">reference</span><span class="sxs-lookup"><span data-stu-id="41027-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="41027-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="41027-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="41027-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="41027-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="41027-172">subscription</span><span class="sxs-lookup"><span data-stu-id="41027-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a><span data-ttu-id="41027-173">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="41027-173">String functions</span></span>
<span data-ttu-id="41027-174">Resource Manager는 문자열 작업을 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41027-174">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="41027-175">base64</span><span class="sxs-lookup"><span data-stu-id="41027-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="41027-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="41027-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="41027-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="41027-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="41027-178">concat</span><span class="sxs-lookup"><span data-stu-id="41027-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="41027-179">contains</span><span class="sxs-lookup"><span data-stu-id="41027-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="41027-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="41027-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="41027-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="41027-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="41027-182">empty</span><span class="sxs-lookup"><span data-stu-id="41027-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="41027-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="41027-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="41027-184">first</span><span class="sxs-lookup"><span data-stu-id="41027-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="41027-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="41027-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="41027-186">last</span><span class="sxs-lookup"><span data-stu-id="41027-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="41027-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="41027-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="41027-188">length</span><span class="sxs-lookup"><span data-stu-id="41027-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="41027-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="41027-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="41027-190">replace</span><span class="sxs-lookup"><span data-stu-id="41027-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="41027-191">skip</span><span class="sxs-lookup"><span data-stu-id="41027-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="41027-192">분할</span><span class="sxs-lookup"><span data-stu-id="41027-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="41027-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="41027-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="41027-194">string</span><span class="sxs-lookup"><span data-stu-id="41027-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="41027-195">substring</span><span class="sxs-lookup"><span data-stu-id="41027-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="41027-196">take</span><span class="sxs-lookup"><span data-stu-id="41027-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="41027-197">toLower</span><span class="sxs-lookup"><span data-stu-id="41027-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="41027-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="41027-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="41027-199">trim</span><span class="sxs-lookup"><span data-stu-id="41027-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="41027-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="41027-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="41027-201">uri</span><span class="sxs-lookup"><span data-stu-id="41027-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="41027-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="41027-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="41027-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="41027-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="41027-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41027-204">Next steps</span></span>
* <span data-ttu-id="41027-205">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="41027-205">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="41027-206">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="41027-206">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="41027-207">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="41027-207">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="41027-208">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="41027-208">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

