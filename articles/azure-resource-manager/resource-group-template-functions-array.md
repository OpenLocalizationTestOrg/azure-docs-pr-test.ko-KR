---
title: "Azure Resource Manager 템플릿 함수 - 배열 및 개체 | Microsoft Docs"
description: "배열 및 개체 작업을 위해 Azure Resource Manager 템플릿에서 사용할 수 있는 함수에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c72c0-103">Azure Resource Manager 템플릿에 대한 배열 및 개체 함수</span><span class="sxs-lookup"><span data-stu-id="c72c0-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="c72c0-104">Resource Manager는 배열 및 개체 작업을 위한 여러 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="c72c0-105">array</span><span class="sxs-lookup"><span data-stu-id="c72c0-105">array</span></span>](#array)
* [<span data-ttu-id="c72c0-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="c72c0-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="c72c0-107">concat</span><span class="sxs-lookup"><span data-stu-id="c72c0-107">concat</span></span>](#concat)
* [<span data-ttu-id="c72c0-108">contains</span><span class="sxs-lookup"><span data-stu-id="c72c0-108">contains</span></span>](#contains)
* [<span data-ttu-id="c72c0-109">createArray</span><span class="sxs-lookup"><span data-stu-id="c72c0-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="c72c0-110">empty</span><span class="sxs-lookup"><span data-stu-id="c72c0-110">empty</span></span>](#empty)
* [<span data-ttu-id="c72c0-111">first</span><span class="sxs-lookup"><span data-stu-id="c72c0-111">first</span></span>](#first)
* [<span data-ttu-id="c72c0-112">intersection</span><span class="sxs-lookup"><span data-stu-id="c72c0-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="c72c0-113">json</span><span class="sxs-lookup"><span data-stu-id="c72c0-113">json</span></span>](#json)
* [<span data-ttu-id="c72c0-114">last</span><span class="sxs-lookup"><span data-stu-id="c72c0-114">last</span></span>](#last)
* [<span data-ttu-id="c72c0-115">length</span><span class="sxs-lookup"><span data-stu-id="c72c0-115">length</span></span>](#length)
* [<span data-ttu-id="c72c0-116">min</span><span class="sxs-lookup"><span data-stu-id="c72c0-116">min</span></span>](#min)
* [<span data-ttu-id="c72c0-117">max</span><span class="sxs-lookup"><span data-stu-id="c72c0-117">max</span></span>](#max)
* [<span data-ttu-id="c72c0-118">range</span><span class="sxs-lookup"><span data-stu-id="c72c0-118">range</span></span>](#range)
* [<span data-ttu-id="c72c0-119">skip</span><span class="sxs-lookup"><span data-stu-id="c72c0-119">skip</span></span>](#skip)
* [<span data-ttu-id="c72c0-120">take</span><span class="sxs-lookup"><span data-stu-id="c72c0-120">take</span></span>](#take)
* [<span data-ttu-id="c72c0-121">union</span><span class="sxs-lookup"><span data-stu-id="c72c0-121">union</span></span>](#union)

<span data-ttu-id="c72c0-122">값으로 구분되는 문자열 값의 배열을 가져오려면 [split](resource-group-template-functions-string.md#split)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72c0-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="c72c0-123">array</span><span class="sxs-lookup"><span data-stu-id="c72c0-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="c72c0-124">값을 배열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-125">Parameters</span></span>

| <span data-ttu-id="c72c0-126">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-126">Parameter</span></span> | <span data-ttu-id="c72c0-127">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-127">Required</span></span> | <span data-ttu-id="c72c0-128">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-128">Type</span></span> | <span data-ttu-id="c72c0-129">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="c72c0-130">convertToArray</span></span> |<span data-ttu-id="c72c0-131">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-131">Yes</span></span> |<span data-ttu-id="c72c0-132">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-132">int, string, array, or object</span></span> |<span data-ttu-id="c72c0-133">배열로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-134">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-134">Return value</span></span>

<span data-ttu-id="c72c0-135">배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-136">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-136">Example</span></span>

<span data-ttu-id="c72c0-137">다음 예제에서는 여러 다른 형식의 배열 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-137">The following example shows how to use the array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-138">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-139">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-139">Name</span></span> | <span data-ttu-id="c72c0-140">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-140">Type</span></span> | <span data-ttu-id="c72c0-141">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-142">intOutput</span></span> | <span data-ttu-id="c72c0-143">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-143">Array</span></span> | <span data-ttu-id="c72c0-144">[1]</span><span class="sxs-lookup"><span data-stu-id="c72c0-144">[1]</span></span> |
| <span data-ttu-id="c72c0-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-145">stringOutput</span></span> | <span data-ttu-id="c72c0-146">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-146">Array</span></span> | <span data-ttu-id="c72c0-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-147">["a"]</span></span> |
| <span data-ttu-id="c72c0-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-148">objectOutput</span></span> | <span data-ttu-id="c72c0-149">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-149">Array</span></span> | <span data-ttu-id="c72c0-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="c72c0-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="c72c0-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="c72c0-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="c72c0-152">매개 변수에서 첫 번째 null이 아닌 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="c72c0-153">빈 문자열, 빈 배열 및 빈 개체는 null이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-154">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-154">Parameters</span></span>

| <span data-ttu-id="c72c0-155">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-155">Parameter</span></span> | <span data-ttu-id="c72c0-156">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-156">Required</span></span> | <span data-ttu-id="c72c0-157">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-157">Type</span></span> | <span data-ttu-id="c72c0-158">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-159">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-159">arg1</span></span> |<span data-ttu-id="c72c0-160">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-160">Yes</span></span> |<span data-ttu-id="c72c0-161">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-161">int, string, array, or object</span></span> |<span data-ttu-id="c72c0-162">null인지 테스트할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-162">The first value to test for null.</span></span> |
| <span data-ttu-id="c72c0-163">추가 인수</span><span class="sxs-lookup"><span data-stu-id="c72c0-163">additional args</span></span> |<span data-ttu-id="c72c0-164">아니요</span><span class="sxs-lookup"><span data-stu-id="c72c0-164">No</span></span> |<span data-ttu-id="c72c0-165">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-165">int, string, array, or object</span></span> |<span data-ttu-id="c72c0-166">null인지 테스트할 추가 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-167">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-167">Return value</span></span>

<span data-ttu-id="c72c0-168">문자열, int, 배열 또는 개체일 수 있는 첫 번째 null이 아닌 매개 변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="c72c0-169">모든 매개 변수가 null이면 null입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="c72c0-170">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-170">Example</span></span>

<span data-ttu-id="c72c0-171">다음 예제에서는 coalesce의 다른 사용에서 출력된 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-171">The following example shows the output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="c72c0-172">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-173">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-173">Name</span></span> | <span data-ttu-id="c72c0-174">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-174">Type</span></span> | <span data-ttu-id="c72c0-175">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-176">stringOutput</span></span> | <span data-ttu-id="c72c0-177">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-177">String</span></span> | <span data-ttu-id="c72c0-178">기본값</span><span class="sxs-lookup"><span data-stu-id="c72c0-178">default</span></span> |
| <span data-ttu-id="c72c0-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-179">intOutput</span></span> | <span data-ttu-id="c72c0-180">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-180">Int</span></span> | <span data-ttu-id="c72c0-181">1</span><span class="sxs-lookup"><span data-stu-id="c72c0-181">1</span></span> |
| <span data-ttu-id="c72c0-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-182">objectOutput</span></span> | <span data-ttu-id="c72c0-183">Object</span><span class="sxs-lookup"><span data-stu-id="c72c0-183">Object</span></span> | <span data-ttu-id="c72c0-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="c72c0-184">{"first": "default"}</span></span> |
| <span data-ttu-id="c72c0-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-185">arrayOutput</span></span> | <span data-ttu-id="c72c0-186">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-186">Array</span></span> | <span data-ttu-id="c72c0-187">[1]</span><span class="sxs-lookup"><span data-stu-id="c72c0-187">[1]</span></span> |
| <span data-ttu-id="c72c0-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-188">emptyOutput</span></span> | <span data-ttu-id="c72c0-189">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-189">Bool</span></span> | <span data-ttu-id="c72c0-190">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="c72c0-191">concat</span><span class="sxs-lookup"><span data-stu-id="c72c0-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="c72c0-192">여러 배열을 결합하고 연결된 배열을 반환하거나 여러 문자열 값을 결합하고 연결된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c72c0-193">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-193">Parameters</span></span>

| <span data-ttu-id="c72c0-194">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-194">Parameter</span></span> | <span data-ttu-id="c72c0-195">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-195">Required</span></span> | <span data-ttu-id="c72c0-196">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-196">Type</span></span> | <span data-ttu-id="c72c0-197">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-198">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-198">arg1</span></span> |<span data-ttu-id="c72c0-199">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-199">Yes</span></span> |<span data-ttu-id="c72c0-200">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-200">array or string</span></span> |<span data-ttu-id="c72c0-201">연결을 위한 첫 번째 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="c72c0-202">추가 인수</span><span class="sxs-lookup"><span data-stu-id="c72c0-202">additional arguments</span></span> |<span data-ttu-id="c72c0-203">아니요</span><span class="sxs-lookup"><span data-stu-id="c72c0-203">No</span></span> |<span data-ttu-id="c72c0-204">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-204">array or string</span></span> |<span data-ttu-id="c72c0-205">연결 순서로 나타낸 추가 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="c72c0-206">이 함수는 인수를 개수에 관계없이 사용할 수 있으며 매개 변수에 대한 문자열이나 배열 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="c72c0-207">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-207">Return value</span></span>
<span data-ttu-id="c72c0-208">연결된 값의 문자열 또는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-209">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-209">Example</span></span>

<span data-ttu-id="c72c0-210">다음 예제에서는 두 개의 배열을 결합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-210">The following example shows how to combine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-211">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-212">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-212">Name</span></span> | <span data-ttu-id="c72c0-213">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-213">Type</span></span> | <span data-ttu-id="c72c0-214">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-215">return</span><span class="sxs-lookup"><span data-stu-id="c72c0-215">return</span></span> | <span data-ttu-id="c72c0-216">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-216">Array</span></span> | <span data-ttu-id="c72c0-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="c72c0-218">다음 예제에서는 2개의 문자열 값을 결합하고 연결된 문자열을 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="c72c0-219">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-220">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-220">Name</span></span> | <span data-ttu-id="c72c0-221">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-221">Type</span></span> | <span data-ttu-id="c72c0-222">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-223">concatOutput</span></span> | <span data-ttu-id="c72c0-224">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-224">String</span></span> | <span data-ttu-id="c72c0-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="c72c0-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="c72c0-226">contains</span><span class="sxs-lookup"><span data-stu-id="c72c0-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="c72c0-227">배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-228">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-228">Parameters</span></span>

| <span data-ttu-id="c72c0-229">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-229">Parameter</span></span> | <span data-ttu-id="c72c0-230">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-230">Required</span></span> | <span data-ttu-id="c72c0-231">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-231">Type</span></span> | <span data-ttu-id="c72c0-232">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-233">container</span><span class="sxs-lookup"><span data-stu-id="c72c0-233">container</span></span> |<span data-ttu-id="c72c0-234">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-234">Yes</span></span> |<span data-ttu-id="c72c0-235">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-235">array, object, or string</span></span> |<span data-ttu-id="c72c0-236">찾을 값을 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="c72c0-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="c72c0-237">itemToFind</span></span> |<span data-ttu-id="c72c0-238">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-238">Yes</span></span> |<span data-ttu-id="c72c0-239">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="c72c0-239">string or int</span></span> |<span data-ttu-id="c72c0-240">찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-241">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-241">Return value</span></span>

<span data-ttu-id="c72c0-242">항목이 있으면 **True**이고, 항목이 없으면 **False**입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-243">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-243">Example</span></span>

<span data-ttu-id="c72c0-244">다음 예제에서는 여러 다른 형식의 contains를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-244">The following example shows how to use contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="c72c0-245">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-246">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-246">Name</span></span> | <span data-ttu-id="c72c0-247">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-247">Type</span></span> | <span data-ttu-id="c72c0-248">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="c72c0-249">stringTrue</span></span> | <span data-ttu-id="c72c0-250">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-250">Bool</span></span> | <span data-ttu-id="c72c0-251">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-251">True</span></span> |
| <span data-ttu-id="c72c0-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="c72c0-252">stringFalse</span></span> | <span data-ttu-id="c72c0-253">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-253">Bool</span></span> | <span data-ttu-id="c72c0-254">False</span><span class="sxs-lookup"><span data-stu-id="c72c0-254">False</span></span> |
| <span data-ttu-id="c72c0-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="c72c0-255">objectTrue</span></span> | <span data-ttu-id="c72c0-256">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-256">Bool</span></span> | <span data-ttu-id="c72c0-257">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-257">True</span></span> |
| <span data-ttu-id="c72c0-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="c72c0-258">objectFalse</span></span> | <span data-ttu-id="c72c0-259">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-259">Bool</span></span> | <span data-ttu-id="c72c0-260">False</span><span class="sxs-lookup"><span data-stu-id="c72c0-260">False</span></span> |
| <span data-ttu-id="c72c0-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="c72c0-261">arrayTrue</span></span> | <span data-ttu-id="c72c0-262">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-262">Bool</span></span> | <span data-ttu-id="c72c0-263">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-263">True</span></span> |
| <span data-ttu-id="c72c0-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="c72c0-264">arrayFalse</span></span> | <span data-ttu-id="c72c0-265">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-265">Bool</span></span> | <span data-ttu-id="c72c0-266">False</span><span class="sxs-lookup"><span data-stu-id="c72c0-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="c72c0-267">createarray</span><span class="sxs-lookup"><span data-stu-id="c72c0-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="c72c0-268">매개 변수에서 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-269">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-269">Parameters</span></span>

| <span data-ttu-id="c72c0-270">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-270">Parameter</span></span> | <span data-ttu-id="c72c0-271">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-271">Required</span></span> | <span data-ttu-id="c72c0-272">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-272">Type</span></span> | <span data-ttu-id="c72c0-273">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-274">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-274">arg1</span></span> |<span data-ttu-id="c72c0-275">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-275">Yes</span></span> |<span data-ttu-id="c72c0-276">문자열, 정수, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="c72c0-277">배열의 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-277">The first value in the array.</span></span> |
| <span data-ttu-id="c72c0-278">추가 인수</span><span class="sxs-lookup"><span data-stu-id="c72c0-278">additional arguments</span></span> |<span data-ttu-id="c72c0-279">아니요</span><span class="sxs-lookup"><span data-stu-id="c72c0-279">No</span></span> |<span data-ttu-id="c72c0-280">문자열, 정수, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="c72c0-281">배열의 추가 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-282">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-282">Return value</span></span>

<span data-ttu-id="c72c0-283">배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-284">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-284">Example</span></span>

<span data-ttu-id="c72c0-285">다음 예제에서는 여러 다른 형식의 createArray를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-285">The following example shows how to use createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-286">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-287">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-287">Name</span></span> | <span data-ttu-id="c72c0-288">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-288">Type</span></span> | <span data-ttu-id="c72c0-289">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="c72c0-290">stringArray</span></span> | <span data-ttu-id="c72c0-291">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-291">Array</span></span> | <span data-ttu-id="c72c0-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="c72c0-293">intArray</span><span class="sxs-lookup"><span data-stu-id="c72c0-293">intArray</span></span> | <span data-ttu-id="c72c0-294">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-294">Array</span></span> | <span data-ttu-id="c72c0-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="c72c0-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="c72c0-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="c72c0-296">objectArray</span></span> | <span data-ttu-id="c72c0-297">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-297">Array</span></span> | <span data-ttu-id="c72c0-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="c72c0-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="c72c0-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="c72c0-299">arrayArray</span></span> | <span data-ttu-id="c72c0-300">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-300">Array</span></span> | <span data-ttu-id="c72c0-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="c72c0-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="c72c0-302">empty</span><span class="sxs-lookup"><span data-stu-id="c72c0-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="c72c0-303">배열, 개체 또는 문자열이 비어 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-304">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-304">Parameters</span></span>

| <span data-ttu-id="c72c0-305">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-305">Parameter</span></span> | <span data-ttu-id="c72c0-306">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-306">Required</span></span> | <span data-ttu-id="c72c0-307">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-307">Type</span></span> | <span data-ttu-id="c72c0-308">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="c72c0-309">itemToTest</span></span> |<span data-ttu-id="c72c0-310">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-310">Yes</span></span> |<span data-ttu-id="c72c0-311">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-311">array, object, or string</span></span> |<span data-ttu-id="c72c0-312">비어 있는지 확인할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-313">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-313">Return value</span></span>

<span data-ttu-id="c72c0-314">값이 비어 있으면 **True**를 반환하고 비어 있지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-315">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-315">Example</span></span>

<span data-ttu-id="c72c0-316">다음 예제에서는 배열, 개체 및 문자열이 비어 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-316">The following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-317">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-318">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-318">Name</span></span> | <span data-ttu-id="c72c0-319">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-319">Type</span></span> | <span data-ttu-id="c72c0-320">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="c72c0-321">arrayEmpty</span></span> | <span data-ttu-id="c72c0-322">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-322">Bool</span></span> | <span data-ttu-id="c72c0-323">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-323">True</span></span> |
| <span data-ttu-id="c72c0-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="c72c0-324">objectEmpty</span></span> | <span data-ttu-id="c72c0-325">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-325">Bool</span></span> | <span data-ttu-id="c72c0-326">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-326">True</span></span> |
| <span data-ttu-id="c72c0-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="c72c0-327">stringEmpty</span></span> | <span data-ttu-id="c72c0-328">Bool</span><span class="sxs-lookup"><span data-stu-id="c72c0-328">Bool</span></span> | <span data-ttu-id="c72c0-329">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="c72c0-330">first</span><span class="sxs-lookup"><span data-stu-id="c72c0-330">first</span></span>
`first(arg1)`

<span data-ttu-id="c72c0-331">배열의 첫 번째 요소 또는 문자열의 첫 번째 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-332">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-332">Parameters</span></span>

| <span data-ttu-id="c72c0-333">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-333">Parameter</span></span> | <span data-ttu-id="c72c0-334">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-334">Required</span></span> | <span data-ttu-id="c72c0-335">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-335">Type</span></span> | <span data-ttu-id="c72c0-336">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-337">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-337">arg1</span></span> |<span data-ttu-id="c72c0-338">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-338">Yes</span></span> |<span data-ttu-id="c72c0-339">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-339">array or string</span></span> |<span data-ttu-id="c72c0-340">첫 번째 요소 또는 문자를 검색할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-341">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-341">Return value</span></span>

<span data-ttu-id="c72c0-342">배열의 첫 번째 요소 또는 문자열의 첫 번째 문자에 대한 형식(문자열, int, 배열 또는 개체)입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-343">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-343">Example</span></span>

<span data-ttu-id="c72c0-344">다음 예제에서는 배열 및 문자열에 첫 번째 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-344">The following example shows how to use the first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="c72c0-345">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-346">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-346">Name</span></span> | <span data-ttu-id="c72c0-347">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-347">Type</span></span> | <span data-ttu-id="c72c0-348">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-349">arrayOutput</span></span> | <span data-ttu-id="c72c0-350">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-350">String</span></span> | <span data-ttu-id="c72c0-351">one</span><span class="sxs-lookup"><span data-stu-id="c72c0-351">one</span></span> |
| <span data-ttu-id="c72c0-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-352">stringOutput</span></span> | <span data-ttu-id="c72c0-353">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-353">String</span></span> | <span data-ttu-id="c72c0-354">O</span><span class="sxs-lookup"><span data-stu-id="c72c0-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="c72c0-355">교집합</span><span class="sxs-lookup"><span data-stu-id="c72c0-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="c72c0-356">매개 변수에서 공통 요소를 갖는 단일 배열 또는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-357">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-357">Parameters</span></span>

| <span data-ttu-id="c72c0-358">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-358">Parameter</span></span> | <span data-ttu-id="c72c0-359">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-359">Required</span></span> | <span data-ttu-id="c72c0-360">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-360">Type</span></span> | <span data-ttu-id="c72c0-361">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-362">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-362">arg1</span></span> |<span data-ttu-id="c72c0-363">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-363">Yes</span></span> |<span data-ttu-id="c72c0-364">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-364">array or object</span></span> |<span data-ttu-id="c72c0-365">공통 요소를 찾는 데 사용할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="c72c0-366">arg2</span><span class="sxs-lookup"><span data-stu-id="c72c0-366">arg2</span></span> |<span data-ttu-id="c72c0-367">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-367">Yes</span></span> |<span data-ttu-id="c72c0-368">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-368">array or object</span></span> |<span data-ttu-id="c72c0-369">공통 요소를 찾는 데 사용할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="c72c0-370">추가 인수</span><span class="sxs-lookup"><span data-stu-id="c72c0-370">additional arguments</span></span> |<span data-ttu-id="c72c0-371">아니요</span><span class="sxs-lookup"><span data-stu-id="c72c0-371">No</span></span> |<span data-ttu-id="c72c0-372">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-372">array or object</span></span> |<span data-ttu-id="c72c0-373">공통 요소를 찾는 데 사용할 추가 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-374">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-374">Return value</span></span>

<span data-ttu-id="c72c0-375">공통 요소가 있는 배열 또는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-376">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-376">Example</span></span>

<span data-ttu-id="c72c0-377">다음 예제에서는 배열 및 개체에 intersection을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-377">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-378">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-379">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-379">Name</span></span> | <span data-ttu-id="c72c0-380">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-380">Type</span></span> | <span data-ttu-id="c72c0-381">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-382">objectOutput</span></span> | <span data-ttu-id="c72c0-383">Object</span><span class="sxs-lookup"><span data-stu-id="c72c0-383">Object</span></span> | <span data-ttu-id="c72c0-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="c72c0-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="c72c0-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-385">arrayOutput</span></span> | <span data-ttu-id="c72c0-386">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-386">Array</span></span> | <span data-ttu-id="c72c0-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="c72c0-388">json :</span><span class="sxs-lookup"><span data-stu-id="c72c0-388">json</span></span>
`json(arg1)`

<span data-ttu-id="c72c0-389">JSON 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-390">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-390">Parameters</span></span>

| <span data-ttu-id="c72c0-391">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-391">Parameter</span></span> | <span data-ttu-id="c72c0-392">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-392">Required</span></span> | <span data-ttu-id="c72c0-393">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-393">Type</span></span> | <span data-ttu-id="c72c0-394">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-395">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-395">arg1</span></span> |<span data-ttu-id="c72c0-396">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-396">Yes</span></span> |<span data-ttu-id="c72c0-397">string</span><span class="sxs-lookup"><span data-stu-id="c72c0-397">string</span></span> |<span data-ttu-id="c72c0-398">JSON으로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="c72c0-399">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-399">Return value</span></span>

<span data-ttu-id="c72c0-400">지정된 문자열의 JSON 개체이거나, **null**을 지정한 경우 빈 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-401">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-401">Example</span></span>

<span data-ttu-id="c72c0-402">다음 예제에서는 배열 및 개체에 intersection을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-402">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-403">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-404">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-404">Name</span></span> | <span data-ttu-id="c72c0-405">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-405">Type</span></span> | <span data-ttu-id="c72c0-406">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-407">jsonOutput</span></span> | <span data-ttu-id="c72c0-408">Object</span><span class="sxs-lookup"><span data-stu-id="c72c0-408">Object</span></span> | <span data-ttu-id="c72c0-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="c72c0-409">{"a": "b"}</span></span> |
| <span data-ttu-id="c72c0-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-410">nullOutput</span></span> | <span data-ttu-id="c72c0-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="c72c0-411">Boolean</span></span> | <span data-ttu-id="c72c0-412">True</span><span class="sxs-lookup"><span data-stu-id="c72c0-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="c72c0-413">last</span><span class="sxs-lookup"><span data-stu-id="c72c0-413">last</span></span>
`last (arg1)`

<span data-ttu-id="c72c0-414">배열의 마지막 요소 또는 문자열의 마지막 문자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-415">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-415">Parameters</span></span>

| <span data-ttu-id="c72c0-416">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-416">Parameter</span></span> | <span data-ttu-id="c72c0-417">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-417">Required</span></span> | <span data-ttu-id="c72c0-418">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-418">Type</span></span> | <span data-ttu-id="c72c0-419">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-420">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-420">arg1</span></span> |<span data-ttu-id="c72c0-421">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-421">Yes</span></span> |<span data-ttu-id="c72c0-422">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-422">array or string</span></span> |<span data-ttu-id="c72c0-423">마지막 요소 또는 문자를 검색할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-424">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-424">Return value</span></span>

<span data-ttu-id="c72c0-425">배열의 마지막 요소 또는 문자열의 마지막 문자에 대한 형식(문자열, int, 배열 또는 개체)입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-426">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-426">Example</span></span>

<span data-ttu-id="c72c0-427">다음 예제에서는 배열 및 문자열에 마지막 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-427">The following example shows how to use the last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="c72c0-428">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-429">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-429">Name</span></span> | <span data-ttu-id="c72c0-430">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-430">Type</span></span> | <span data-ttu-id="c72c0-431">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-432">arrayOutput</span></span> | <span data-ttu-id="c72c0-433">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-433">String</span></span> | <span data-ttu-id="c72c0-434">three</span><span class="sxs-lookup"><span data-stu-id="c72c0-434">three</span></span> |
| <span data-ttu-id="c72c0-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-435">stringOutput</span></span> | <span data-ttu-id="c72c0-436">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-436">String</span></span> | <span data-ttu-id="c72c0-437">e</span><span class="sxs-lookup"><span data-stu-id="c72c0-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="c72c0-438">length</span><span class="sxs-lookup"><span data-stu-id="c72c0-438">length</span></span>
`length(arg1)`

<span data-ttu-id="c72c0-439">배열의 요소 수 또는 문자열의 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-440">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-440">Parameters</span></span>

| <span data-ttu-id="c72c0-441">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-441">Parameter</span></span> | <span data-ttu-id="c72c0-442">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-442">Required</span></span> | <span data-ttu-id="c72c0-443">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-443">Type</span></span> | <span data-ttu-id="c72c0-444">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-445">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-445">arg1</span></span> |<span data-ttu-id="c72c0-446">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-446">Yes</span></span> |<span data-ttu-id="c72c0-447">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-447">array or string</span></span> |<span data-ttu-id="c72c0-448">요소 수를 가져오는 데 사용할 배열 또는 문자 수를 가져오는 데 사용할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-449">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-449">Return value</span></span>

<span data-ttu-id="c72c0-450">int입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="c72c0-451">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-451">Example</span></span>

<span data-ttu-id="c72c0-452">다음 예제에서는 배열 및 문자열에 length를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-452">The following example shows how to use length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-453">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-454">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-454">Name</span></span> | <span data-ttu-id="c72c0-455">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-455">Type</span></span> | <span data-ttu-id="c72c0-456">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="c72c0-457">arrayLength</span></span> | <span data-ttu-id="c72c0-458">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-458">Int</span></span> | <span data-ttu-id="c72c0-459">3</span><span class="sxs-lookup"><span data-stu-id="c72c0-459">3</span></span> |
| <span data-ttu-id="c72c0-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="c72c0-460">stringLength</span></span> | <span data-ttu-id="c72c0-461">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-461">Int</span></span> | <span data-ttu-id="c72c0-462">13</span><span class="sxs-lookup"><span data-stu-id="c72c0-462">13</span></span> |

<span data-ttu-id="c72c0-463">배열과 함께 이 함수를 사용하면 리소스를 만들 때 반복 횟수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="c72c0-464">다음 예제에서 매개 변수 **siteNames** 는 웹 사이트를 만들 때 사용할 이름 배열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="c72c0-465">배열과 함께 이 함수를 사용하는 방법의 예제는 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72c0-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="c72c0-466">min</span><span class="sxs-lookup"><span data-stu-id="c72c0-466">min</span></span>
`min(arg1)`

<span data-ttu-id="c72c0-467">정수 배열 또는 쉼표로 구분된 정수 목록 중에서 최소값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-468">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-468">Parameters</span></span>

| <span data-ttu-id="c72c0-469">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-469">Parameter</span></span> | <span data-ttu-id="c72c0-470">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-470">Required</span></span> | <span data-ttu-id="c72c0-471">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-471">Type</span></span> | <span data-ttu-id="c72c0-472">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-473">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-473">arg1</span></span> |<span data-ttu-id="c72c0-474">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-474">Yes</span></span> |<span data-ttu-id="c72c0-475">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="c72c0-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c72c0-476">최소값을 가져올 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-477">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-477">Return value</span></span>

<span data-ttu-id="c72c0-478">최소값을 나타내는 int입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-479">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-479">Example</span></span>

<span data-ttu-id="c72c0-480">다음 예제에서는 배열 및 정소 목록에 min을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-480">The following example shows how to use min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="c72c0-481">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-482">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-482">Name</span></span> | <span data-ttu-id="c72c0-483">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-483">Type</span></span> | <span data-ttu-id="c72c0-484">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-485">arrayOutput</span></span> | <span data-ttu-id="c72c0-486">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-486">Int</span></span> | <span data-ttu-id="c72c0-487">0</span><span class="sxs-lookup"><span data-stu-id="c72c0-487">0</span></span> |
| <span data-ttu-id="c72c0-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-488">intOutput</span></span> | <span data-ttu-id="c72c0-489">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-489">Int</span></span> | <span data-ttu-id="c72c0-490">0</span><span class="sxs-lookup"><span data-stu-id="c72c0-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="c72c0-491">max</span><span class="sxs-lookup"><span data-stu-id="c72c0-491">max</span></span>
`max(arg1)`

<span data-ttu-id="c72c0-492">정수 배열 또는 쉼표로 구분된 정수 목록 중에서 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-493">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-493">Parameters</span></span>

| <span data-ttu-id="c72c0-494">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-494">Parameter</span></span> | <span data-ttu-id="c72c0-495">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-495">Required</span></span> | <span data-ttu-id="c72c0-496">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-496">Type</span></span> | <span data-ttu-id="c72c0-497">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-498">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-498">arg1</span></span> |<span data-ttu-id="c72c0-499">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-499">Yes</span></span> |<span data-ttu-id="c72c0-500">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="c72c0-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="c72c0-501">최대값을 가져올 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-502">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-502">Return value</span></span>

<span data-ttu-id="c72c0-503">최대값을 나타내는 int입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-504">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-504">Example</span></span>

<span data-ttu-id="c72c0-505">다음 예제에서는 배열 및 정소 목록에 max를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-505">The following example shows how to use max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="c72c0-506">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-507">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-507">Name</span></span> | <span data-ttu-id="c72c0-508">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-508">Type</span></span> | <span data-ttu-id="c72c0-509">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-510">arrayOutput</span></span> | <span data-ttu-id="c72c0-511">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-511">Int</span></span> | <span data-ttu-id="c72c0-512">5</span><span class="sxs-lookup"><span data-stu-id="c72c0-512">5</span></span> |
| <span data-ttu-id="c72c0-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-513">intOutput</span></span> | <span data-ttu-id="c72c0-514">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-514">Int</span></span> | <span data-ttu-id="c72c0-515">5</span><span class="sxs-lookup"><span data-stu-id="c72c0-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="c72c0-516">range</span><span class="sxs-lookup"><span data-stu-id="c72c0-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="c72c0-517">시작 정수 및 항목의 수를 포함하는 정수 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-518">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-518">Parameters</span></span>

| <span data-ttu-id="c72c0-519">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-519">Parameter</span></span> | <span data-ttu-id="c72c0-520">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-520">Required</span></span> | <span data-ttu-id="c72c0-521">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-521">Type</span></span> | <span data-ttu-id="c72c0-522">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="c72c0-523">startingInteger</span></span> |<span data-ttu-id="c72c0-524">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-524">Yes</span></span> |<span data-ttu-id="c72c0-525">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-525">int</span></span> |<span data-ttu-id="c72c0-526">배열에서 첫 번째 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-526">The first integer in the array.</span></span> |
| <span data-ttu-id="c72c0-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="c72c0-527">numberofElements</span></span> |<span data-ttu-id="c72c0-528">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-528">Yes</span></span> |<span data-ttu-id="c72c0-529">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-529">int</span></span> |<span data-ttu-id="c72c0-530">배열에 있는 정수의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-531">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-531">Return value</span></span>

<span data-ttu-id="c72c0-532">정수 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-533">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-533">Example</span></span>

<span data-ttu-id="c72c0-534">다음 예제에서는 range 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-534">The following example shows how to use the range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-535">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-536">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-536">Name</span></span> | <span data-ttu-id="c72c0-537">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-537">Type</span></span> | <span data-ttu-id="c72c0-538">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-539">rangeOutput</span></span> | <span data-ttu-id="c72c0-540">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-540">Array</span></span> | <span data-ttu-id="c72c0-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="c72c0-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="c72c0-542">skip</span><span class="sxs-lookup"><span data-stu-id="c72c0-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="c72c0-543">배열에서 지정된 숫자 이후의 모든 요소를 포함하는 배열을 반환하거나 문자열에서 지정된 숫자 이후의 모든 숫자를 포함하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-544">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-544">Parameters</span></span>

| <span data-ttu-id="c72c0-545">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-545">Parameter</span></span> | <span data-ttu-id="c72c0-546">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-546">Required</span></span> | <span data-ttu-id="c72c0-547">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-547">Type</span></span> | <span data-ttu-id="c72c0-548">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="c72c0-549">originalValue</span></span> |<span data-ttu-id="c72c0-550">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-550">Yes</span></span> |<span data-ttu-id="c72c0-551">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-551">array or string</span></span> |<span data-ttu-id="c72c0-552">건너뛰는 데 사용할 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="c72c0-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="c72c0-553">numberToSkip</span></span> |<span data-ttu-id="c72c0-554">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-554">Yes</span></span> |<span data-ttu-id="c72c0-555">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-555">int</span></span> |<span data-ttu-id="c72c0-556">건너뛸 요소 또는 문자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="c72c0-557">이 값이 0 이하이면 값의 모든 요소 또는 문자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="c72c0-558">이 값이 배열 또는 문자열의 길이보다 크면 빈 배열 또는 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-559">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-559">Return value</span></span>

<span data-ttu-id="c72c0-560">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-561">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-561">Example</span></span>

<span data-ttu-id="c72c0-562">다음 예제에서는 배열에서 지정된 요소 수 및 문자열에서 지정된 수의 문자를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-563">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-564">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-564">Name</span></span> | <span data-ttu-id="c72c0-565">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-565">Type</span></span> | <span data-ttu-id="c72c0-566">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-567">arrayOutput</span></span> | <span data-ttu-id="c72c0-568">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-568">Array</span></span> | <span data-ttu-id="c72c0-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-569">["three"]</span></span> |
| <span data-ttu-id="c72c0-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-570">stringOutput</span></span> | <span data-ttu-id="c72c0-571">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-571">String</span></span> | <span data-ttu-id="c72c0-572">two three</span><span class="sxs-lookup"><span data-stu-id="c72c0-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="c72c0-573">take</span><span class="sxs-lookup"><span data-stu-id="c72c0-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="c72c0-574">배열 시작부터 지정된 수의 요소를 포함하는 배열 또는 문자열 시작부터 지정된 수의 문자를 포함하는 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-575">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-575">Parameters</span></span>

| <span data-ttu-id="c72c0-576">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-576">Parameter</span></span> | <span data-ttu-id="c72c0-577">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-577">Required</span></span> | <span data-ttu-id="c72c0-578">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-578">Type</span></span> | <span data-ttu-id="c72c0-579">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="c72c0-580">originalValue</span></span> |<span data-ttu-id="c72c0-581">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-581">Yes</span></span> |<span data-ttu-id="c72c0-582">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-582">array or string</span></span> |<span data-ttu-id="c72c0-583">요소를 가져올 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="c72c0-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="c72c0-584">numberToTake</span></span> |<span data-ttu-id="c72c0-585">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-585">Yes</span></span> |<span data-ttu-id="c72c0-586">int</span><span class="sxs-lookup"><span data-stu-id="c72c0-586">int</span></span> |<span data-ttu-id="c72c0-587">수락할 요소 또는 문자의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-587">The number of elements or characters to take.</span></span> <span data-ttu-id="c72c0-588">이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="c72c0-589">지정된 배열 또는 문자열의 길이보다 크면 배열 또는 문자열의 모든 요소가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-590">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-590">Return value</span></span>

<span data-ttu-id="c72c0-591">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-592">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-592">Example</span></span>

<span data-ttu-id="c72c0-593">다음 예제에서는 배열에서 지정된 수의 요소 및 문자열의 문자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-594">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-595">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-595">Name</span></span> | <span data-ttu-id="c72c0-596">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-596">Type</span></span> | <span data-ttu-id="c72c0-597">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-598">arrayOutput</span></span> | <span data-ttu-id="c72c0-599">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-599">Array</span></span> | <span data-ttu-id="c72c0-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-600">["one", "two"]</span></span> |
| <span data-ttu-id="c72c0-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-601">stringOutput</span></span> | <span data-ttu-id="c72c0-602">문자열</span><span class="sxs-lookup"><span data-stu-id="c72c0-602">String</span></span> | <span data-ttu-id="c72c0-603">on</span><span class="sxs-lookup"><span data-stu-id="c72c0-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="c72c0-604">union</span><span class="sxs-lookup"><span data-stu-id="c72c0-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="c72c0-605">매개 변수의 모든 요소를 포함하는 단일 배열 또는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="c72c0-606">중복된 값 또는 키는 한 번만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="c72c0-607">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c72c0-607">Parameters</span></span>

| <span data-ttu-id="c72c0-608">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-608">Parameter</span></span> | <span data-ttu-id="c72c0-609">필수</span><span class="sxs-lookup"><span data-stu-id="c72c0-609">Required</span></span> | <span data-ttu-id="c72c0-610">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-610">Type</span></span> | <span data-ttu-id="c72c0-611">설명</span><span class="sxs-lookup"><span data-stu-id="c72c0-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c72c0-612">arg1</span><span class="sxs-lookup"><span data-stu-id="c72c0-612">arg1</span></span> |<span data-ttu-id="c72c0-613">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-613">Yes</span></span> |<span data-ttu-id="c72c0-614">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-614">array or object</span></span> |<span data-ttu-id="c72c0-615">요소를 조인하는 데 사용할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="c72c0-616">arg2</span><span class="sxs-lookup"><span data-stu-id="c72c0-616">arg2</span></span> |<span data-ttu-id="c72c0-617">예</span><span class="sxs-lookup"><span data-stu-id="c72c0-617">Yes</span></span> |<span data-ttu-id="c72c0-618">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-618">array or object</span></span> |<span data-ttu-id="c72c0-619">요소를 조인하는 데 사용할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="c72c0-620">추가 인수</span><span class="sxs-lookup"><span data-stu-id="c72c0-620">additional arguments</span></span> |<span data-ttu-id="c72c0-621">아니요</span><span class="sxs-lookup"><span data-stu-id="c72c0-621">No</span></span> |<span data-ttu-id="c72c0-622">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="c72c0-622">array or object</span></span> |<span data-ttu-id="c72c0-623">요소를 조인하는 데 사용할 추가 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c72c0-624">반환 값</span><span class="sxs-lookup"><span data-stu-id="c72c0-624">Return value</span></span>

<span data-ttu-id="c72c0-625">배열 또는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="c72c0-626">예제</span><span class="sxs-lookup"><span data-stu-id="c72c0-626">Example</span></span>

<span data-ttu-id="c72c0-627">다음 예제에서는 배열 및 개체에 union을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-627">The following example shows how to use union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="c72c0-628">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c72c0-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c72c0-629">이름</span><span class="sxs-lookup"><span data-stu-id="c72c0-629">Name</span></span> | <span data-ttu-id="c72c0-630">형식</span><span class="sxs-lookup"><span data-stu-id="c72c0-630">Type</span></span> | <span data-ttu-id="c72c0-631">값</span><span class="sxs-lookup"><span data-stu-id="c72c0-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c72c0-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-632">objectOutput</span></span> | <span data-ttu-id="c72c0-633">Object</span><span class="sxs-lookup"><span data-stu-id="c72c0-633">Object</span></span> | <span data-ttu-id="c72c0-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="c72c0-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="c72c0-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c72c0-635">arrayOutput</span></span> | <span data-ttu-id="c72c0-636">배열</span><span class="sxs-lookup"><span data-stu-id="c72c0-636">Array</span></span> | <span data-ttu-id="c72c0-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="c72c0-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c72c0-638">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c72c0-638">Next steps</span></span>
* <span data-ttu-id="c72c0-639">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72c0-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c72c0-640">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72c0-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c72c0-641">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72c0-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c72c0-642">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c72c0-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

