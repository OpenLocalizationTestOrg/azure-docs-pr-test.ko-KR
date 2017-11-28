---
title: "리소스 관리자 템플릿 aaaAzure 함수-배열 및 개체가 | Microsoft Docs"
description: "Hello 함수 toouse 배열 및 개체 사용에 대 한 Azure 리소스 관리자 템플릿에 설명 합니다."
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
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="9c294-103">Azure Resource Manager 템플릿에 대한 배열 및 개체 함수</span><span class="sxs-lookup"><span data-stu-id="9c294-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="9c294-104">Resource Manager는 배열 및 개체 작업을 위한 여러 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="9c294-105">array</span><span class="sxs-lookup"><span data-stu-id="9c294-105">array</span></span>](#array)
* [<span data-ttu-id="9c294-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="9c294-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="9c294-107">concat</span><span class="sxs-lookup"><span data-stu-id="9c294-107">concat</span></span>](#concat)
* [<span data-ttu-id="9c294-108">contains</span><span class="sxs-lookup"><span data-stu-id="9c294-108">contains</span></span>](#contains)
* [<span data-ttu-id="9c294-109">createArray</span><span class="sxs-lookup"><span data-stu-id="9c294-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="9c294-110">empty</span><span class="sxs-lookup"><span data-stu-id="9c294-110">empty</span></span>](#empty)
* [<span data-ttu-id="9c294-111">first</span><span class="sxs-lookup"><span data-stu-id="9c294-111">first</span></span>](#first)
* [<span data-ttu-id="9c294-112">intersection</span><span class="sxs-lookup"><span data-stu-id="9c294-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="9c294-113">json</span><span class="sxs-lookup"><span data-stu-id="9c294-113">json</span></span>](#json)
* [<span data-ttu-id="9c294-114">last</span><span class="sxs-lookup"><span data-stu-id="9c294-114">last</span></span>](#last)
* [<span data-ttu-id="9c294-115">length</span><span class="sxs-lookup"><span data-stu-id="9c294-115">length</span></span>](#length)
* [<span data-ttu-id="9c294-116">min</span><span class="sxs-lookup"><span data-stu-id="9c294-116">min</span></span>](#min)
* [<span data-ttu-id="9c294-117">max</span><span class="sxs-lookup"><span data-stu-id="9c294-117">max</span></span>](#max)
* [<span data-ttu-id="9c294-118">range</span><span class="sxs-lookup"><span data-stu-id="9c294-118">range</span></span>](#range)
* [<span data-ttu-id="9c294-119">skip</span><span class="sxs-lookup"><span data-stu-id="9c294-119">skip</span></span>](#skip)
* [<span data-ttu-id="9c294-120">take</span><span class="sxs-lookup"><span data-stu-id="9c294-120">take</span></span>](#take)
* [<span data-ttu-id="9c294-121">union</span><span class="sxs-lookup"><span data-stu-id="9c294-121">union</span></span>](#union)

<span data-ttu-id="9c294-122">tooget 값으로 구분 된 문자열 값의 배열을 참조 [분할](resource-group-template-functions-string.md#split)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="9c294-123">array</span><span class="sxs-lookup"><span data-stu-id="9c294-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="9c294-124">Hello, tooan 배열 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-125">Parameters</span></span>

| <span data-ttu-id="9c294-126">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-126">Parameter</span></span> | <span data-ttu-id="9c294-127">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-127">Required</span></span> | <span data-ttu-id="9c294-128">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-128">Type</span></span> | <span data-ttu-id="9c294-129">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="9c294-130">convertToArray</span></span> |<span data-ttu-id="9c294-131">예</span><span class="sxs-lookup"><span data-stu-id="9c294-131">Yes</span></span> |<span data-ttu-id="9c294-132">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-132">int, string, array, or object</span></span> |<span data-ttu-id="9c294-133">hello tooconvert tooan 배열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-134">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-134">Return value</span></span>

<span data-ttu-id="9c294-135">배열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-136">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-136">Example</span></span>

<span data-ttu-id="9c294-137">hello 다음 예제에서는 어떻게 toouse hello 여러 형식으로 배열 함수</span><span class="sxs-lookup"><span data-stu-id="9c294-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="9c294-138">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-139">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-139">Name</span></span> | <span data-ttu-id="9c294-140">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-140">Type</span></span> | <span data-ttu-id="9c294-141">값</span><span class="sxs-lookup"><span data-stu-id="9c294-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-142">intOutput</span></span> | <span data-ttu-id="9c294-143">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-143">Array</span></span> | <span data-ttu-id="9c294-144">[1]</span><span class="sxs-lookup"><span data-stu-id="9c294-144">[1]</span></span> |
| <span data-ttu-id="9c294-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-145">stringOutput</span></span> | <span data-ttu-id="9c294-146">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-146">Array</span></span> | <span data-ttu-id="9c294-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="9c294-147">["a"]</span></span> |
| <span data-ttu-id="9c294-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-148">objectOutput</span></span> | <span data-ttu-id="9c294-149">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-149">Array</span></span> | <span data-ttu-id="9c294-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="9c294-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="9c294-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="9c294-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="9c294-152">Hello 매개 변수에서 첫 번째 null이 아닌 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="9c294-153">빈 문자열, 빈 배열 및 빈 개체는 null이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-154">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-154">Parameters</span></span>

| <span data-ttu-id="9c294-155">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-155">Parameter</span></span> | <span data-ttu-id="9c294-156">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-156">Required</span></span> | <span data-ttu-id="9c294-157">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-157">Type</span></span> | <span data-ttu-id="9c294-158">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-159">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-159">arg1</span></span> |<span data-ttu-id="9c294-160">예</span><span class="sxs-lookup"><span data-stu-id="9c294-160">Yes</span></span> |<span data-ttu-id="9c294-161">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-161">int, string, array, or object</span></span> |<span data-ttu-id="9c294-162">null에 대 한 첫 번째 값 tootest을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="9c294-163">추가 인수</span><span class="sxs-lookup"><span data-stu-id="9c294-163">additional args</span></span> |<span data-ttu-id="9c294-164">아니요</span><span class="sxs-lookup"><span data-stu-id="9c294-164">No</span></span> |<span data-ttu-id="9c294-165">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-165">int, string, array, or object</span></span> |<span data-ttu-id="9c294-166">Null에 대 한 추가 값 tootest 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-167">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-167">Return value</span></span>

<span data-ttu-id="9c294-168">hello hello 첫 번째 null이 아닌 매개 변수 값, 문자열, int, 배열 또는 개체 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="9c294-169">모든 매개 변수가 null이면 null입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="9c294-170">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-170">Example</span></span>

<span data-ttu-id="9c294-171">hello 다음 예제에서는 hello 출력을에서 보여 줍니다 coalesce의 서로 다른 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="9c294-172">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-173">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-173">Name</span></span> | <span data-ttu-id="9c294-174">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-174">Type</span></span> | <span data-ttu-id="9c294-175">값</span><span class="sxs-lookup"><span data-stu-id="9c294-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-176">stringOutput</span></span> | <span data-ttu-id="9c294-177">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-177">String</span></span> | <span data-ttu-id="9c294-178">기본값</span><span class="sxs-lookup"><span data-stu-id="9c294-178">default</span></span> |
| <span data-ttu-id="9c294-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-179">intOutput</span></span> | <span data-ttu-id="9c294-180">int</span><span class="sxs-lookup"><span data-stu-id="9c294-180">Int</span></span> | <span data-ttu-id="9c294-181">1</span><span class="sxs-lookup"><span data-stu-id="9c294-181">1</span></span> |
| <span data-ttu-id="9c294-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-182">objectOutput</span></span> | <span data-ttu-id="9c294-183">Object</span><span class="sxs-lookup"><span data-stu-id="9c294-183">Object</span></span> | <span data-ttu-id="9c294-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="9c294-184">{"first": "default"}</span></span> |
| <span data-ttu-id="9c294-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-185">arrayOutput</span></span> | <span data-ttu-id="9c294-186">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-186">Array</span></span> | <span data-ttu-id="9c294-187">[1]</span><span class="sxs-lookup"><span data-stu-id="9c294-187">[1]</span></span> |
| <span data-ttu-id="9c294-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-188">emptyOutput</span></span> | <span data-ttu-id="9c294-189">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-189">Bool</span></span> | <span data-ttu-id="9c294-190">True</span><span class="sxs-lookup"><span data-stu-id="9c294-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="9c294-191">concat</span><span class="sxs-lookup"><span data-stu-id="9c294-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="9c294-192">여러 배열 및 연결 하는 hello 배열을 반환을 결합 또는 여러 개의 문자열 값을 결합 하 고 hello 연결 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="9c294-193">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-193">Parameters</span></span>

| <span data-ttu-id="9c294-194">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-194">Parameter</span></span> | <span data-ttu-id="9c294-195">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-195">Required</span></span> | <span data-ttu-id="9c294-196">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-196">Type</span></span> | <span data-ttu-id="9c294-197">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-198">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-198">arg1</span></span> |<span data-ttu-id="9c294-199">예</span><span class="sxs-lookup"><span data-stu-id="9c294-199">Yes</span></span> |<span data-ttu-id="9c294-200">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-200">array or string</span></span> |<span data-ttu-id="9c294-201">첫 번째 배열 또는 문자열 연결에 대 한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="9c294-202">추가 인수</span><span class="sxs-lookup"><span data-stu-id="9c294-202">additional arguments</span></span> |<span data-ttu-id="9c294-203">아니요</span><span class="sxs-lookup"><span data-stu-id="9c294-203">No</span></span> |<span data-ttu-id="9c294-204">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-204">array or string</span></span> |<span data-ttu-id="9c294-205">연결 순서로 나타낸 추가 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="9c294-206">이 함수는 변수 인수 수에 제한이 하며 문자열 또는 배열 hello 매개 변수에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="9c294-207">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-207">Return value</span></span>
<span data-ttu-id="9c294-208">연결된 값의 문자열 또는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-209">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-209">Example</span></span>

<span data-ttu-id="9c294-210">다음 예제는 hello toocombine 두 배열 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="9c294-211">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-212">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-212">Name</span></span> | <span data-ttu-id="9c294-213">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-213">Type</span></span> | <span data-ttu-id="9c294-214">값</span><span class="sxs-lookup"><span data-stu-id="9c294-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-215">return</span><span class="sxs-lookup"><span data-stu-id="9c294-215">return</span></span> | <span data-ttu-id="9c294-216">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-216">Array</span></span> | <span data-ttu-id="9c294-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="9c294-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="9c294-218">다음 예제는 hello toocombine 두 문자열 값 하 고 연결 된 문자열을 반환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="9c294-219">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-220">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-220">Name</span></span> | <span data-ttu-id="9c294-221">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-221">Type</span></span> | <span data-ttu-id="9c294-222">값</span><span class="sxs-lookup"><span data-stu-id="9c294-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-223">concatOutput</span></span> | <span data-ttu-id="9c294-224">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-224">String</span></span> | <span data-ttu-id="9c294-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="9c294-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="9c294-226">contains</span><span class="sxs-lookup"><span data-stu-id="9c294-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="9c294-227">배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-228">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-228">Parameters</span></span>

| <span data-ttu-id="9c294-229">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-229">Parameter</span></span> | <span data-ttu-id="9c294-230">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-230">Required</span></span> | <span data-ttu-id="9c294-231">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-231">Type</span></span> | <span data-ttu-id="9c294-232">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-233">container</span><span class="sxs-lookup"><span data-stu-id="9c294-233">container</span></span> |<span data-ttu-id="9c294-234">예</span><span class="sxs-lookup"><span data-stu-id="9c294-234">Yes</span></span> |<span data-ttu-id="9c294-235">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-235">array, object, or string</span></span> |<span data-ttu-id="9c294-236">hello 값 toofind를 포함 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="9c294-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="9c294-237">itemToFind</span></span> |<span data-ttu-id="9c294-238">예</span><span class="sxs-lookup"><span data-stu-id="9c294-238">Yes</span></span> |<span data-ttu-id="9c294-239">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="9c294-239">string or int</span></span> |<span data-ttu-id="9c294-240">hello 값 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-241">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-241">Return value</span></span>

<span data-ttu-id="9c294-242">**True 이면** hello 항목이 검색 되지 않으면 이면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-243">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-243">Example</span></span>

<span data-ttu-id="9c294-244">hello 다음 예제는 toouse 여러 형식으로 포함 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="9c294-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="9c294-245">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-246">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-246">Name</span></span> | <span data-ttu-id="9c294-247">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-247">Type</span></span> | <span data-ttu-id="9c294-248">값</span><span class="sxs-lookup"><span data-stu-id="9c294-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="9c294-249">stringTrue</span></span> | <span data-ttu-id="9c294-250">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-250">Bool</span></span> | <span data-ttu-id="9c294-251">True</span><span class="sxs-lookup"><span data-stu-id="9c294-251">True</span></span> |
| <span data-ttu-id="9c294-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="9c294-252">stringFalse</span></span> | <span data-ttu-id="9c294-253">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-253">Bool</span></span> | <span data-ttu-id="9c294-254">False</span><span class="sxs-lookup"><span data-stu-id="9c294-254">False</span></span> |
| <span data-ttu-id="9c294-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="9c294-255">objectTrue</span></span> | <span data-ttu-id="9c294-256">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-256">Bool</span></span> | <span data-ttu-id="9c294-257">True</span><span class="sxs-lookup"><span data-stu-id="9c294-257">True</span></span> |
| <span data-ttu-id="9c294-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="9c294-258">objectFalse</span></span> | <span data-ttu-id="9c294-259">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-259">Bool</span></span> | <span data-ttu-id="9c294-260">False</span><span class="sxs-lookup"><span data-stu-id="9c294-260">False</span></span> |
| <span data-ttu-id="9c294-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="9c294-261">arrayTrue</span></span> | <span data-ttu-id="9c294-262">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-262">Bool</span></span> | <span data-ttu-id="9c294-263">True</span><span class="sxs-lookup"><span data-stu-id="9c294-263">True</span></span> |
| <span data-ttu-id="9c294-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="9c294-264">arrayFalse</span></span> | <span data-ttu-id="9c294-265">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-265">Bool</span></span> | <span data-ttu-id="9c294-266">False</span><span class="sxs-lookup"><span data-stu-id="9c294-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="9c294-267">createarray</span><span class="sxs-lookup"><span data-stu-id="9c294-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="9c294-268">Hello 매개 변수에서 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-269">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-269">Parameters</span></span>

| <span data-ttu-id="9c294-270">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-270">Parameter</span></span> | <span data-ttu-id="9c294-271">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-271">Required</span></span> | <span data-ttu-id="9c294-272">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-272">Type</span></span> | <span data-ttu-id="9c294-273">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-274">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-274">arg1</span></span> |<span data-ttu-id="9c294-275">예</span><span class="sxs-lookup"><span data-stu-id="9c294-275">Yes</span></span> |<span data-ttu-id="9c294-276">문자열, 정수, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="9c294-277">hello hello 배열의 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="9c294-278">추가 인수</span><span class="sxs-lookup"><span data-stu-id="9c294-278">additional arguments</span></span> |<span data-ttu-id="9c294-279">아니요</span><span class="sxs-lookup"><span data-stu-id="9c294-279">No</span></span> |<span data-ttu-id="9c294-280">문자열, 정수, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="9c294-281">Hello 배열에 추가 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-282">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-282">Return value</span></span>

<span data-ttu-id="9c294-283">배열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-284">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-284">Example</span></span>

<span data-ttu-id="9c294-285">hello 방법을 예제와 다음 여러 형식으로 toouse createArray:</span><span class="sxs-lookup"><span data-stu-id="9c294-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="9c294-286">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-287">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-287">Name</span></span> | <span data-ttu-id="9c294-288">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-288">Type</span></span> | <span data-ttu-id="9c294-289">값</span><span class="sxs-lookup"><span data-stu-id="9c294-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="9c294-290">stringArray</span></span> | <span data-ttu-id="9c294-291">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-291">Array</span></span> | <span data-ttu-id="9c294-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="9c294-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="9c294-293">intArray</span><span class="sxs-lookup"><span data-stu-id="9c294-293">intArray</span></span> | <span data-ttu-id="9c294-294">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-294">Array</span></span> | <span data-ttu-id="9c294-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="9c294-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="9c294-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="9c294-296">objectArray</span></span> | <span data-ttu-id="9c294-297">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-297">Array</span></span> | <span data-ttu-id="9c294-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="9c294-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="9c294-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="9c294-299">arrayArray</span></span> | <span data-ttu-id="9c294-300">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-300">Array</span></span> | <span data-ttu-id="9c294-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="9c294-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="9c294-302">empty</span><span class="sxs-lookup"><span data-stu-id="9c294-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="9c294-303">배열, 개체 또는 문자열이 비어 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-304">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-304">Parameters</span></span>

| <span data-ttu-id="9c294-305">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-305">Parameter</span></span> | <span data-ttu-id="9c294-306">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-306">Required</span></span> | <span data-ttu-id="9c294-307">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-307">Type</span></span> | <span data-ttu-id="9c294-308">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="9c294-309">itemToTest</span></span> |<span data-ttu-id="9c294-310">예</span><span class="sxs-lookup"><span data-stu-id="9c294-310">Yes</span></span> |<span data-ttu-id="9c294-311">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-311">array, object, or string</span></span> |<span data-ttu-id="9c294-312">비어 있는 경우 값 toocheck을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-313">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-313">Return value</span></span>

<span data-ttu-id="9c294-314">반환 **True** hello 값, 비어 있지 않으면이 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-315">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-315">Example</span></span>

<span data-ttu-id="9c294-316">다음 예제는 hello는 배열, 개체 및 문자열 비어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="9c294-317">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-318">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-318">Name</span></span> | <span data-ttu-id="9c294-319">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-319">Type</span></span> | <span data-ttu-id="9c294-320">값</span><span class="sxs-lookup"><span data-stu-id="9c294-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="9c294-321">arrayEmpty</span></span> | <span data-ttu-id="9c294-322">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-322">Bool</span></span> | <span data-ttu-id="9c294-323">True</span><span class="sxs-lookup"><span data-stu-id="9c294-323">True</span></span> |
| <span data-ttu-id="9c294-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="9c294-324">objectEmpty</span></span> | <span data-ttu-id="9c294-325">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-325">Bool</span></span> | <span data-ttu-id="9c294-326">True</span><span class="sxs-lookup"><span data-stu-id="9c294-326">True</span></span> |
| <span data-ttu-id="9c294-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="9c294-327">stringEmpty</span></span> | <span data-ttu-id="9c294-328">Bool</span><span class="sxs-lookup"><span data-stu-id="9c294-328">Bool</span></span> | <span data-ttu-id="9c294-329">True</span><span class="sxs-lookup"><span data-stu-id="9c294-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="9c294-330">first</span><span class="sxs-lookup"><span data-stu-id="9c294-330">first</span></span>
`first(arg1)`

<span data-ttu-id="9c294-331">반환은 hello 배열의 첫 번째 요소 또는 hello 문자열의 첫 번째 문자 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-332">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-332">Parameters</span></span>

| <span data-ttu-id="9c294-333">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-333">Parameter</span></span> | <span data-ttu-id="9c294-334">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-334">Required</span></span> | <span data-ttu-id="9c294-335">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-335">Type</span></span> | <span data-ttu-id="9c294-336">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-337">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-337">arg1</span></span> |<span data-ttu-id="9c294-338">예</span><span class="sxs-lookup"><span data-stu-id="9c294-338">Yes</span></span> |<span data-ttu-id="9c294-339">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-339">array or string</span></span> |<span data-ttu-id="9c294-340">문자 또는 hello 값 tooretrieve hello 첫 번째 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-341">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-341">Return value</span></span>

<span data-ttu-id="9c294-342">hello 형식 (string, int, 배열 또는 개체)의 배열 또는 문자열의 첫 번째 문자 hello hello 첫 번째 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-343">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-343">Example</span></span>

<span data-ttu-id="9c294-344">hello 다음 예제에서는 어떻게 toouse hello 배열 및 문자열을 사용 하는 첫 번째 함수</span><span class="sxs-lookup"><span data-stu-id="9c294-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="9c294-345">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-346">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-346">Name</span></span> | <span data-ttu-id="9c294-347">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-347">Type</span></span> | <span data-ttu-id="9c294-348">값</span><span class="sxs-lookup"><span data-stu-id="9c294-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-349">arrayOutput</span></span> | <span data-ttu-id="9c294-350">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-350">String</span></span> | <span data-ttu-id="9c294-351">one</span><span class="sxs-lookup"><span data-stu-id="9c294-351">one</span></span> |
| <span data-ttu-id="9c294-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-352">stringOutput</span></span> | <span data-ttu-id="9c294-353">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-353">String</span></span> | <span data-ttu-id="9c294-354">O</span><span class="sxs-lookup"><span data-stu-id="9c294-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="9c294-355">교집합</span><span class="sxs-lookup"><span data-stu-id="9c294-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="9c294-356">Hello 매개 변수에서 단일 배열 또는 개체 hello 공통 요소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-357">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-357">Parameters</span></span>

| <span data-ttu-id="9c294-358">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-358">Parameter</span></span> | <span data-ttu-id="9c294-359">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-359">Required</span></span> | <span data-ttu-id="9c294-360">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-360">Type</span></span> | <span data-ttu-id="9c294-361">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-362">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-362">arg1</span></span> |<span data-ttu-id="9c294-363">예</span><span class="sxs-lookup"><span data-stu-id="9c294-363">Yes</span></span> |<span data-ttu-id="9c294-364">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-364">array or object</span></span> |<span data-ttu-id="9c294-365">공통 요소를 찾기 위한 첫 번째 값 toouse를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="9c294-366">arg2</span><span class="sxs-lookup"><span data-stu-id="9c294-366">arg2</span></span> |<span data-ttu-id="9c294-367">예</span><span class="sxs-lookup"><span data-stu-id="9c294-367">Yes</span></span> |<span data-ttu-id="9c294-368">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-368">array or object</span></span> |<span data-ttu-id="9c294-369">공통 요소를 찾기 위한 두 번째 값 toouse를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="9c294-370">추가 인수</span><span class="sxs-lookup"><span data-stu-id="9c294-370">additional arguments</span></span> |<span data-ttu-id="9c294-371">아니요</span><span class="sxs-lookup"><span data-stu-id="9c294-371">No</span></span> |<span data-ttu-id="9c294-372">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-372">array or object</span></span> |<span data-ttu-id="9c294-373">공통 요소를 찾기 위한 toouse 추가 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-374">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-374">Return value</span></span>

<span data-ttu-id="9c294-375">배열 또는 hello 공통 요소를 가진 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-376">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-376">Example</span></span>

<span data-ttu-id="9c294-377">다음 예제는 hello toouse 교집합 배열 하는 방법을 보여 줍니다. 및 개체:</span><span class="sxs-lookup"><span data-stu-id="9c294-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="9c294-378">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-379">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-379">Name</span></span> | <span data-ttu-id="9c294-380">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-380">Type</span></span> | <span data-ttu-id="9c294-381">값</span><span class="sxs-lookup"><span data-stu-id="9c294-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-382">objectOutput</span></span> | <span data-ttu-id="9c294-383">Object</span><span class="sxs-lookup"><span data-stu-id="9c294-383">Object</span></span> | <span data-ttu-id="9c294-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="9c294-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="9c294-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-385">arrayOutput</span></span> | <span data-ttu-id="9c294-386">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-386">Array</span></span> | <span data-ttu-id="9c294-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="9c294-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="9c294-388">json :</span><span class="sxs-lookup"><span data-stu-id="9c294-388">json</span></span>
`json(arg1)`

<span data-ttu-id="9c294-389">JSON 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-390">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-390">Parameters</span></span>

| <span data-ttu-id="9c294-391">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-391">Parameter</span></span> | <span data-ttu-id="9c294-392">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-392">Required</span></span> | <span data-ttu-id="9c294-393">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-393">Type</span></span> | <span data-ttu-id="9c294-394">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-395">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-395">arg1</span></span> |<span data-ttu-id="9c294-396">예</span><span class="sxs-lookup"><span data-stu-id="9c294-396">Yes</span></span> |<span data-ttu-id="9c294-397">string</span><span class="sxs-lookup"><span data-stu-id="9c294-397">string</span></span> |<span data-ttu-id="9c294-398">hello 값 tooconvert tooJSON 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="9c294-399">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-399">Return value</span></span>

<span data-ttu-id="9c294-400">문자열 또는 빈 개체 hello JSON 개체 hello에서 지정 된 경우 **null** 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-401">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-401">Example</span></span>

<span data-ttu-id="9c294-402">다음 예제는 hello toouse 교집합 배열 하는 방법을 보여 줍니다. 및 개체:</span><span class="sxs-lookup"><span data-stu-id="9c294-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="9c294-403">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-404">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-404">Name</span></span> | <span data-ttu-id="9c294-405">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-405">Type</span></span> | <span data-ttu-id="9c294-406">값</span><span class="sxs-lookup"><span data-stu-id="9c294-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-407">jsonOutput</span></span> | <span data-ttu-id="9c294-408">Object</span><span class="sxs-lookup"><span data-stu-id="9c294-408">Object</span></span> | <span data-ttu-id="9c294-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="9c294-409">{"a": "b"}</span></span> |
| <span data-ttu-id="9c294-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-410">nullOutput</span></span> | <span data-ttu-id="9c294-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="9c294-411">Boolean</span></span> | <span data-ttu-id="9c294-412">True</span><span class="sxs-lookup"><span data-stu-id="9c294-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="9c294-413">last</span><span class="sxs-lookup"><span data-stu-id="9c294-413">last</span></span>
`last (arg1)`

<span data-ttu-id="9c294-414">반환은 hello 배열의 마지막 요소 또는 hello 문자열의 마지막 문자 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-415">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-415">Parameters</span></span>

| <span data-ttu-id="9c294-416">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-416">Parameter</span></span> | <span data-ttu-id="9c294-417">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-417">Required</span></span> | <span data-ttu-id="9c294-418">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-418">Type</span></span> | <span data-ttu-id="9c294-419">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-420">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-420">arg1</span></span> |<span data-ttu-id="9c294-421">예</span><span class="sxs-lookup"><span data-stu-id="9c294-421">Yes</span></span> |<span data-ttu-id="9c294-422">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-422">array or string</span></span> |<span data-ttu-id="9c294-423">문자 또는 hello 값 tooretrieve hello 마지막 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-424">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-424">Return value</span></span>

<span data-ttu-id="9c294-425">hello 형식 (string, int, 배열 또는 개체)에 배열 또는 문자열의 마지막 문자 hello hello 마지막 요소의입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-426">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-426">Example</span></span>

<span data-ttu-id="9c294-427">hello 다음 예제에서는 어떻게 toouse hello 수 있는 배열 및 문자열 last 함수</span><span class="sxs-lookup"><span data-stu-id="9c294-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="9c294-428">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-429">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-429">Name</span></span> | <span data-ttu-id="9c294-430">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-430">Type</span></span> | <span data-ttu-id="9c294-431">값</span><span class="sxs-lookup"><span data-stu-id="9c294-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-432">arrayOutput</span></span> | <span data-ttu-id="9c294-433">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-433">String</span></span> | <span data-ttu-id="9c294-434">three</span><span class="sxs-lookup"><span data-stu-id="9c294-434">three</span></span> |
| <span data-ttu-id="9c294-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-435">stringOutput</span></span> | <span data-ttu-id="9c294-436">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-436">String</span></span> | <span data-ttu-id="9c294-437">e</span><span class="sxs-lookup"><span data-stu-id="9c294-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="9c294-438">length</span><span class="sxs-lookup"><span data-stu-id="9c294-438">length</span></span>
`length(arg1)`

<span data-ttu-id="9c294-439">배열 또는 문자열의 문자에 hello 수의 요소를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-440">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-440">Parameters</span></span>

| <span data-ttu-id="9c294-441">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-441">Parameter</span></span> | <span data-ttu-id="9c294-442">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-442">Required</span></span> | <span data-ttu-id="9c294-443">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-443">Type</span></span> | <span data-ttu-id="9c294-444">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-445">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-445">arg1</span></span> |<span data-ttu-id="9c294-446">예</span><span class="sxs-lookup"><span data-stu-id="9c294-446">Yes</span></span> |<span data-ttu-id="9c294-447">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-447">array or string</span></span> |<span data-ttu-id="9c294-448">hello 수의 요소를 가져오기 위한 배열 toouse hello 또는 hello 개수의 문자를 가져오기 위한 문자열 toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-449">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-449">Return value</span></span>

<span data-ttu-id="9c294-450">int입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="9c294-451">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-451">Example</span></span>

<span data-ttu-id="9c294-452">hello 방법을 예제와 다음 toouse 배열 및 문자열 길이:</span><span class="sxs-lookup"><span data-stu-id="9c294-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="9c294-453">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-454">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-454">Name</span></span> | <span data-ttu-id="9c294-455">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-455">Type</span></span> | <span data-ttu-id="9c294-456">값</span><span class="sxs-lookup"><span data-stu-id="9c294-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="9c294-457">arrayLength</span></span> | <span data-ttu-id="9c294-458">int</span><span class="sxs-lookup"><span data-stu-id="9c294-458">Int</span></span> | <span data-ttu-id="9c294-459">3</span><span class="sxs-lookup"><span data-stu-id="9c294-459">3</span></span> |
| <span data-ttu-id="9c294-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="9c294-460">stringLength</span></span> | <span data-ttu-id="9c294-461">int</span><span class="sxs-lookup"><span data-stu-id="9c294-461">Int</span></span> | <span data-ttu-id="9c294-462">13</span><span class="sxs-lookup"><span data-stu-id="9c294-462">13</span></span> |

<span data-ttu-id="9c294-463">리소스를 만들 때 배열 toospecify hello 수의 반복으로이 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="9c294-464">다음 예제는 hello에서 매개 변수를 hello **siteNames** hello 웹 사이트를 만들 때 이름 toouse tooan 배열을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="9c294-465">배열과 함께 이 함수를 사용하는 방법의 예제는 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c294-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="9c294-466">Min</span><span class="sxs-lookup"><span data-stu-id="9c294-466">min</span></span>
`min(arg1)`

<span data-ttu-id="9c294-467">반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최소 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-468">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-468">Parameters</span></span>

| <span data-ttu-id="9c294-469">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-469">Parameter</span></span> | <span data-ttu-id="9c294-470">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-470">Required</span></span> | <span data-ttu-id="9c294-471">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-471">Type</span></span> | <span data-ttu-id="9c294-472">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-473">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-473">arg1</span></span> |<span data-ttu-id="9c294-474">예</span><span class="sxs-lookup"><span data-stu-id="9c294-474">Yes</span></span> |<span data-ttu-id="9c294-475">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="9c294-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="9c294-476">hello 컬렉션 tooget hello 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-477">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-477">Return value</span></span>

<span data-ttu-id="9c294-478">Hello에 대 한 최소값 정보를 나타내는 int입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-479">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-479">Example</span></span>

<span data-ttu-id="9c294-480">hello 방법을 예제와 다음 toouse min 배열 및 정수 목록:</span><span class="sxs-lookup"><span data-stu-id="9c294-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="9c294-481">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-482">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-482">Name</span></span> | <span data-ttu-id="9c294-483">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-483">Type</span></span> | <span data-ttu-id="9c294-484">값</span><span class="sxs-lookup"><span data-stu-id="9c294-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-485">arrayOutput</span></span> | <span data-ttu-id="9c294-486">int</span><span class="sxs-lookup"><span data-stu-id="9c294-486">Int</span></span> | <span data-ttu-id="9c294-487">0</span><span class="sxs-lookup"><span data-stu-id="9c294-487">0</span></span> |
| <span data-ttu-id="9c294-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-488">intOutput</span></span> | <span data-ttu-id="9c294-489">int</span><span class="sxs-lookup"><span data-stu-id="9c294-489">Int</span></span> | <span data-ttu-id="9c294-490">0</span><span class="sxs-lookup"><span data-stu-id="9c294-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="9c294-491">max</span><span class="sxs-lookup"><span data-stu-id="9c294-491">max</span></span>
`max(arg1)`

<span data-ttu-id="9c294-492">반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최대 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-493">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-493">Parameters</span></span>

| <span data-ttu-id="9c294-494">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-494">Parameter</span></span> | <span data-ttu-id="9c294-495">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-495">Required</span></span> | <span data-ttu-id="9c294-496">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-496">Type</span></span> | <span data-ttu-id="9c294-497">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-498">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-498">arg1</span></span> |<span data-ttu-id="9c294-499">예</span><span class="sxs-lookup"><span data-stu-id="9c294-499">Yes</span></span> |<span data-ttu-id="9c294-500">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="9c294-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="9c294-501">hello 컬렉션 tooget hello 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-502">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-502">Return value</span></span>

<span data-ttu-id="9c294-503">Hello 최 댓 값을 나타내는 int입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-504">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-504">Example</span></span>

<span data-ttu-id="9c294-505">hello 방법을 예제와 다음 toouse 배열 및 정수 목록이 사용 하 여 최대:</span><span class="sxs-lookup"><span data-stu-id="9c294-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="9c294-506">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-507">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-507">Name</span></span> | <span data-ttu-id="9c294-508">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-508">Type</span></span> | <span data-ttu-id="9c294-509">값</span><span class="sxs-lookup"><span data-stu-id="9c294-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-510">arrayOutput</span></span> | <span data-ttu-id="9c294-511">int</span><span class="sxs-lookup"><span data-stu-id="9c294-511">Int</span></span> | <span data-ttu-id="9c294-512">5</span><span class="sxs-lookup"><span data-stu-id="9c294-512">5</span></span> |
| <span data-ttu-id="9c294-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-513">intOutput</span></span> | <span data-ttu-id="9c294-514">int</span><span class="sxs-lookup"><span data-stu-id="9c294-514">Int</span></span> | <span data-ttu-id="9c294-515">5</span><span class="sxs-lookup"><span data-stu-id="9c294-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="9c294-516">range</span><span class="sxs-lookup"><span data-stu-id="9c294-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="9c294-517">시작 정수 및 항목의 수를 포함하는 정수 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-518">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-518">Parameters</span></span>

| <span data-ttu-id="9c294-519">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-519">Parameter</span></span> | <span data-ttu-id="9c294-520">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-520">Required</span></span> | <span data-ttu-id="9c294-521">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-521">Type</span></span> | <span data-ttu-id="9c294-522">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="9c294-523">startingInteger</span></span> |<span data-ttu-id="9c294-524">예</span><span class="sxs-lookup"><span data-stu-id="9c294-524">Yes</span></span> |<span data-ttu-id="9c294-525">int</span><span class="sxs-lookup"><span data-stu-id="9c294-525">int</span></span> |<span data-ttu-id="9c294-526">hello hello 배열의 첫 번째 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="9c294-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="9c294-527">numberofElements</span></span> |<span data-ttu-id="9c294-528">예</span><span class="sxs-lookup"><span data-stu-id="9c294-528">Yes</span></span> |<span data-ttu-id="9c294-529">int</span><span class="sxs-lookup"><span data-stu-id="9c294-529">int</span></span> |<span data-ttu-id="9c294-530">hello 수 hello 배열에 있는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-531">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-531">Return value</span></span>

<span data-ttu-id="9c294-532">정수 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-533">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-533">Example</span></span>

<span data-ttu-id="9c294-534">다음 예제는 hello toouse 범위 함수 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="9c294-535">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-536">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-536">Name</span></span> | <span data-ttu-id="9c294-537">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-537">Type</span></span> | <span data-ttu-id="9c294-538">값</span><span class="sxs-lookup"><span data-stu-id="9c294-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-539">rangeOutput</span></span> | <span data-ttu-id="9c294-540">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-540">Array</span></span> | <span data-ttu-id="9c294-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="9c294-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="9c294-542">skip</span><span class="sxs-lookup"><span data-stu-id="9c294-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="9c294-543">Hello hello 배열에 지정 된 번호 또는 hello hello 문자열에 숫자를 지정 된 후 모든 hello 문자로 이루어진 문자열을 반환 하는 후 모든 hello 요소가 있는 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-544">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-544">Parameters</span></span>

| <span data-ttu-id="9c294-545">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-545">Parameter</span></span> | <span data-ttu-id="9c294-546">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-546">Required</span></span> | <span data-ttu-id="9c294-547">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-547">Type</span></span> | <span data-ttu-id="9c294-548">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="9c294-549">originalValue</span></span> |<span data-ttu-id="9c294-550">예</span><span class="sxs-lookup"><span data-stu-id="9c294-550">Yes</span></span> |<span data-ttu-id="9c294-551">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-551">array or string</span></span> |<span data-ttu-id="9c294-552">건너뛰기 위한 hello 배열 또는 문자열 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="9c294-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="9c294-553">numberToSkip</span></span> |<span data-ttu-id="9c294-554">예</span><span class="sxs-lookup"><span data-stu-id="9c294-554">Yes</span></span> |<span data-ttu-id="9c294-555">int</span><span class="sxs-lookup"><span data-stu-id="9c294-555">int</span></span> |<span data-ttu-id="9c294-556">요소 또는 문자 tooskip hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="9c294-557">이 값이 0, 모든 요소를 hello 또는 hello 값의 문자 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="9c294-558">Hello 배열 또는 문자열의 hello 길이 보다 큰 경우 빈 배열 또는 문자열 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-559">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-559">Return value</span></span>

<span data-ttu-id="9c294-560">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-561">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-561">Example</span></span>

<span data-ttu-id="9c294-562">다음 예에서는 건너뜁니다 hello hello hello 배열에서 요소 수를 지정 된 한 hello 문자열에 문자 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="9c294-563">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-564">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-564">Name</span></span> | <span data-ttu-id="9c294-565">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-565">Type</span></span> | <span data-ttu-id="9c294-566">값</span><span class="sxs-lookup"><span data-stu-id="9c294-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-567">arrayOutput</span></span> | <span data-ttu-id="9c294-568">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-568">Array</span></span> | <span data-ttu-id="9c294-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="9c294-569">["three"]</span></span> |
| <span data-ttu-id="9c294-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-570">stringOutput</span></span> | <span data-ttu-id="9c294-571">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-571">String</span></span> | <span data-ttu-id="9c294-572">two three</span><span class="sxs-lookup"><span data-stu-id="9c294-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="9c294-573">take</span><span class="sxs-lookup"><span data-stu-id="9c294-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="9c294-574">Hello로 배열에서 요소 수를 지정 된 반환 hello hello 배열의 시작 또는 hello로 문자열 hello hello 문자열 시작에서 문자 수를 지정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c294-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-575">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-575">Parameters</span></span>

| <span data-ttu-id="9c294-576">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-576">Parameter</span></span> | <span data-ttu-id="9c294-577">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-577">Required</span></span> | <span data-ttu-id="9c294-578">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-578">Type</span></span> | <span data-ttu-id="9c294-579">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="9c294-580">originalValue</span></span> |<span data-ttu-id="9c294-581">예</span><span class="sxs-lookup"><span data-stu-id="9c294-581">Yes</span></span> |<span data-ttu-id="9c294-582">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-582">array or string</span></span> |<span data-ttu-id="9c294-583">배열 또는 문자열 tootake hello 요소를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="9c294-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="9c294-584">numberToTake</span></span> |<span data-ttu-id="9c294-585">예</span><span class="sxs-lookup"><span data-stu-id="9c294-585">Yes</span></span> |<span data-ttu-id="9c294-586">int</span><span class="sxs-lookup"><span data-stu-id="9c294-586">int</span></span> |<span data-ttu-id="9c294-587">요소 또는 문자 tootake hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="9c294-588">이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="9c294-589">지정 된 배열 또는 문자열 hello의 hello 길이 보다 큰 경우 hello 배열 또는 문자열의 모든 hello 요소가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-590">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-590">Return value</span></span>

<span data-ttu-id="9c294-591">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-592">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-592">Example</span></span>

<span data-ttu-id="9c294-593">다음 예제는 hello hello hello 배열에서 요소 및 문자열에서 문자 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="9c294-594">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-595">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-595">Name</span></span> | <span data-ttu-id="9c294-596">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-596">Type</span></span> | <span data-ttu-id="9c294-597">값</span><span class="sxs-lookup"><span data-stu-id="9c294-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-598">arrayOutput</span></span> | <span data-ttu-id="9c294-599">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-599">Array</span></span> | <span data-ttu-id="9c294-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="9c294-600">["one", "two"]</span></span> |
| <span data-ttu-id="9c294-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-601">stringOutput</span></span> | <span data-ttu-id="9c294-602">문자열</span><span class="sxs-lookup"><span data-stu-id="9c294-602">String</span></span> | <span data-ttu-id="9c294-603">on</span><span class="sxs-lookup"><span data-stu-id="9c294-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="9c294-604">union</span><span class="sxs-lookup"><span data-stu-id="9c294-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="9c294-605">Hello 매개 변수에서 단일 배열 또는 모든 요소 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="9c294-606">중복된 값 또는 키는 한 번만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="9c294-607">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9c294-607">Parameters</span></span>

| <span data-ttu-id="9c294-608">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-608">Parameter</span></span> | <span data-ttu-id="9c294-609">필수</span><span class="sxs-lookup"><span data-stu-id="9c294-609">Required</span></span> | <span data-ttu-id="9c294-610">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-610">Type</span></span> | <span data-ttu-id="9c294-611">설명</span><span class="sxs-lookup"><span data-stu-id="9c294-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9c294-612">arg1</span><span class="sxs-lookup"><span data-stu-id="9c294-612">arg1</span></span> |<span data-ttu-id="9c294-613">예</span><span class="sxs-lookup"><span data-stu-id="9c294-613">Yes</span></span> |<span data-ttu-id="9c294-614">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-614">array or object</span></span> |<span data-ttu-id="9c294-615">hello 첫 번째 값 toouse 요소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="9c294-616">arg2</span><span class="sxs-lookup"><span data-stu-id="9c294-616">arg2</span></span> |<span data-ttu-id="9c294-617">예</span><span class="sxs-lookup"><span data-stu-id="9c294-617">Yes</span></span> |<span data-ttu-id="9c294-618">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-618">array or object</span></span> |<span data-ttu-id="9c294-619">요소에 추가 하기 위해 두 번째 값 toouse를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="9c294-620">추가 인수</span><span class="sxs-lookup"><span data-stu-id="9c294-620">additional arguments</span></span> |<span data-ttu-id="9c294-621">아니요</span><span class="sxs-lookup"><span data-stu-id="9c294-621">No</span></span> |<span data-ttu-id="9c294-622">배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="9c294-622">array or object</span></span> |<span data-ttu-id="9c294-623">요소에 추가 하기 위해 추가 값 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9c294-624">반환 값</span><span class="sxs-lookup"><span data-stu-id="9c294-624">Return value</span></span>

<span data-ttu-id="9c294-625">배열 또는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="9c294-626">예제</span><span class="sxs-lookup"><span data-stu-id="9c294-626">Example</span></span>

<span data-ttu-id="9c294-627">다음 예제는 hello toouse 공용 구조체 배열 하는 방법을 보여 줍니다. 및 개체:</span><span class="sxs-lookup"><span data-stu-id="9c294-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="9c294-628">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9c294-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9c294-629">이름</span><span class="sxs-lookup"><span data-stu-id="9c294-629">Name</span></span> | <span data-ttu-id="9c294-630">형식</span><span class="sxs-lookup"><span data-stu-id="9c294-630">Type</span></span> | <span data-ttu-id="9c294-631">값</span><span class="sxs-lookup"><span data-stu-id="9c294-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9c294-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-632">objectOutput</span></span> | <span data-ttu-id="9c294-633">Object</span><span class="sxs-lookup"><span data-stu-id="9c294-633">Object</span></span> | <span data-ttu-id="9c294-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="9c294-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="9c294-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="9c294-635">arrayOutput</span></span> | <span data-ttu-id="9c294-636">배열</span><span class="sxs-lookup"><span data-stu-id="9c294-636">Array</span></span> | <span data-ttu-id="9c294-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="9c294-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c294-638">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c294-638">Next steps</span></span>
* <span data-ttu-id="9c294-639">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9c294-640">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="9c294-641">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="9c294-642">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c294-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

