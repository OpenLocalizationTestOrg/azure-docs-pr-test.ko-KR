---
title: "Azure Resource Manager 템플릿 함수 - 문자열 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 문자열 작업을 수행하는 데 사용할 수 있는 함수에 대해 설명합니다."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="c5cc5-103">Azure Resource Manager 템플릿용 문자열 함수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="c5cc5-104">Resource Manager는 문자열 작업을 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="c5cc5-105">base64</span><span class="sxs-lookup"><span data-stu-id="c5cc5-105">base64</span></span>](#base64)
* [<span data-ttu-id="c5cc5-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="c5cc5-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="c5cc5-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="c5cc5-108">concat</span><span class="sxs-lookup"><span data-stu-id="c5cc5-108">concat</span></span>](#concat)
* [<span data-ttu-id="c5cc5-109">contains</span><span class="sxs-lookup"><span data-stu-id="c5cc5-109">contains</span></span>](#contains)
* [<span data-ttu-id="c5cc5-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="c5cc5-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="c5cc5-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="c5cc5-112">empty</span><span class="sxs-lookup"><span data-stu-id="c5cc5-112">empty</span></span>](#empty)
* [<span data-ttu-id="c5cc5-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="c5cc5-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="c5cc5-114">first</span><span class="sxs-lookup"><span data-stu-id="c5cc5-114">first</span></span>](#first)
* [<span data-ttu-id="c5cc5-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="c5cc5-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="c5cc5-116">last</span><span class="sxs-lookup"><span data-stu-id="c5cc5-116">last</span></span>](#last)
* [<span data-ttu-id="c5cc5-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="c5cc5-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="c5cc5-118">length</span><span class="sxs-lookup"><span data-stu-id="c5cc5-118">length</span></span>](#length)
* [<span data-ttu-id="c5cc5-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="c5cc5-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="c5cc5-120">replace</span><span class="sxs-lookup"><span data-stu-id="c5cc5-120">replace</span></span>](#replace)
* [<span data-ttu-id="c5cc5-121">skip</span><span class="sxs-lookup"><span data-stu-id="c5cc5-121">skip</span></span>](#skip)
* [<span data-ttu-id="c5cc5-122">분할</span><span class="sxs-lookup"><span data-stu-id="c5cc5-122">split</span></span>](#split)
* [<span data-ttu-id="c5cc5-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="c5cc5-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="c5cc5-124">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-124">string</span></span>](#string)
* [<span data-ttu-id="c5cc5-125">substring</span><span class="sxs-lookup"><span data-stu-id="c5cc5-125">substring</span></span>](#substring)
* [<span data-ttu-id="c5cc5-126">take</span><span class="sxs-lookup"><span data-stu-id="c5cc5-126">take</span></span>](#take)
* [<span data-ttu-id="c5cc5-127">toLower</span><span class="sxs-lookup"><span data-stu-id="c5cc5-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="c5cc5-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="c5cc5-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="c5cc5-129">trim</span><span class="sxs-lookup"><span data-stu-id="c5cc5-129">trim</span></span>](#trim)
* [<span data-ttu-id="c5cc5-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="c5cc5-131">uri</span><span class="sxs-lookup"><span data-stu-id="c5cc5-131">uri</span></span>](#uri)
* [<span data-ttu-id="c5cc5-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="c5cc5-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="c5cc5-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="c5cc5-134">base64</span><span class="sxs-lookup"><span data-stu-id="c5cc5-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="c5cc5-135">입력 문자열의 base64 표현을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-136">Parameters</span></span>

| <span data-ttu-id="c5cc5-137">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-137">Parameter</span></span> | <span data-ttu-id="c5cc5-138">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-138">Required</span></span> | <span data-ttu-id="c5cc5-139">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-139">Type</span></span> | <span data-ttu-id="c5cc5-140">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-141">inputString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-141">inputString</span></span> |<span data-ttu-id="c5cc5-142">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-142">Yes</span></span> |<span data-ttu-id="c5cc5-143">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-143">string</span></span> |<span data-ttu-id="c5cc5-144">base64 표현으로 반환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-145">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-145">Return value</span></span>

<span data-ttu-id="c5cc5-146">Base64 표현을 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-147">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-147">Examples</span></span>

<span data-ttu-id="c5cc5-148">다음 예에서는 base64 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-148">The following example shows how to use the base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-149">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-150">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-150">Name</span></span> | <span data-ttu-id="c5cc5-151">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-151">Type</span></span> | <span data-ttu-id="c5cc5-152">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="c5cc5-153">base64Output</span></span> | <span data-ttu-id="c5cc5-154">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-154">String</span></span> | <span data-ttu-id="c5cc5-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="c5cc5-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="c5cc5-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-156">toStringOutput</span></span> | <span data-ttu-id="c5cc5-157">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-157">String</span></span> | <span data-ttu-id="c5cc5-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-158">one, two, three</span></span> |
| <span data-ttu-id="c5cc5-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-159">toJsonOutput</span></span> | <span data-ttu-id="c5cc5-160">Object</span><span class="sxs-lookup"><span data-stu-id="c5cc5-160">Object</span></span> | <span data-ttu-id="c5cc5-161">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="c5cc5-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="c5cc5-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="c5cc5-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="c5cc5-163">base64 표현을 JSON 개체로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-164">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-164">Parameters</span></span>

| <span data-ttu-id="c5cc5-165">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-165">Parameter</span></span> | <span data-ttu-id="c5cc5-166">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-166">Required</span></span> | <span data-ttu-id="c5cc5-167">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-167">Type</span></span> | <span data-ttu-id="c5cc5-168">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="c5cc5-169">base64Value</span></span> |<span data-ttu-id="c5cc5-170">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-170">Yes</span></span> |<span data-ttu-id="c5cc5-171">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-171">string</span></span> |<span data-ttu-id="c5cc5-172">JSON 개체로 변환할 base64 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-173">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-173">Return value</span></span>

<span data-ttu-id="c5cc5-174">JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-175">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-175">Examples</span></span>

<span data-ttu-id="c5cc5-176">다음 예제에서는 base64ToJson 함수를 사용하여 base64 값을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-177">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-178">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-178">Name</span></span> | <span data-ttu-id="c5cc5-179">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-179">Type</span></span> | <span data-ttu-id="c5cc5-180">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="c5cc5-181">base64Output</span></span> | <span data-ttu-id="c5cc5-182">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-182">String</span></span> | <span data-ttu-id="c5cc5-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="c5cc5-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="c5cc5-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-184">toStringOutput</span></span> | <span data-ttu-id="c5cc5-185">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-185">String</span></span> | <span data-ttu-id="c5cc5-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-186">one, two, three</span></span> |
| <span data-ttu-id="c5cc5-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-187">toJsonOutput</span></span> | <span data-ttu-id="c5cc5-188">Object</span><span class="sxs-lookup"><span data-stu-id="c5cc5-188">Object</span></span> | <span data-ttu-id="c5cc5-189">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="c5cc5-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="c5cc5-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="c5cc5-191">base64 표현을 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-192">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-192">Parameters</span></span>

| <span data-ttu-id="c5cc5-193">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-193">Parameter</span></span> | <span data-ttu-id="c5cc5-194">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-194">Required</span></span> | <span data-ttu-id="c5cc5-195">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-195">Type</span></span> | <span data-ttu-id="c5cc5-196">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="c5cc5-197">base64Value</span></span> |<span data-ttu-id="c5cc5-198">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-198">Yes</span></span> |<span data-ttu-id="c5cc5-199">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-199">string</span></span> |<span data-ttu-id="c5cc5-200">문자열로 변환할 base64 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-201">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-201">Return value</span></span>

<span data-ttu-id="c5cc5-202">변환된 base64 값의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-203">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-203">Examples</span></span>

<span data-ttu-id="c5cc5-204">다음 예제에서는 base64ToString 함수를 사용하여 base64 값을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-205">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-206">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-206">Name</span></span> | <span data-ttu-id="c5cc5-207">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-207">Type</span></span> | <span data-ttu-id="c5cc5-208">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="c5cc5-209">base64Output</span></span> | <span data-ttu-id="c5cc5-210">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-210">String</span></span> | <span data-ttu-id="c5cc5-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="c5cc5-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="c5cc5-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-212">toStringOutput</span></span> | <span data-ttu-id="c5cc5-213">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-213">String</span></span> | <span data-ttu-id="c5cc5-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-214">one, two, three</span></span> |
| <span data-ttu-id="c5cc5-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-215">toJsonOutput</span></span> | <span data-ttu-id="c5cc5-216">Object</span><span class="sxs-lookup"><span data-stu-id="c5cc5-216">Object</span></span> | <span data-ttu-id="c5cc5-217">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="c5cc5-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="c5cc5-218">concat</span><span class="sxs-lookup"><span data-stu-id="c5cc5-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="c5cc5-219">여러 문자열 값을 결합하고 연결된 문자열을 반환하거나 여러 배열을 결합하고 연결된 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-220">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-220">Parameters</span></span>

| <span data-ttu-id="c5cc5-221">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-221">Parameter</span></span> | <span data-ttu-id="c5cc5-222">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-222">Required</span></span> | <span data-ttu-id="c5cc5-223">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-223">Type</span></span> | <span data-ttu-id="c5cc5-224">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-225">arg1</span><span class="sxs-lookup"><span data-stu-id="c5cc5-225">arg1</span></span> |<span data-ttu-id="c5cc5-226">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-226">Yes</span></span> |<span data-ttu-id="c5cc5-227">문자열 또는 배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-227">string or array</span></span> |<span data-ttu-id="c5cc5-228">연결할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="c5cc5-229">추가 인수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-229">additional arguments</span></span> |<span data-ttu-id="c5cc5-230">아니요</span><span class="sxs-lookup"><span data-stu-id="c5cc5-230">No</span></span> |<span data-ttu-id="c5cc5-231">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-231">string</span></span> |<span data-ttu-id="c5cc5-232">연결할 추가 값(순서대로)입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-233">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-233">Return value</span></span>
<span data-ttu-id="c5cc5-234">연결된 값의 문자열 또는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-235">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-235">Examples</span></span>

<span data-ttu-id="c5cc5-236">다음 예제에서는 2개의 문자열 값을 결합하고 연결된 문자열을 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="c5cc5-237">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-238">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-238">Name</span></span> | <span data-ttu-id="c5cc5-239">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-239">Type</span></span> | <span data-ttu-id="c5cc5-240">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-241">concatOutput</span></span> | <span data-ttu-id="c5cc5-242">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-242">String</span></span> | <span data-ttu-id="c5cc5-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="c5cc5-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="c5cc5-244">다음 예제에서는 두 개의 배열을 결합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="c5cc5-245">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-246">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-246">Name</span></span> | <span data-ttu-id="c5cc5-247">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-247">Type</span></span> | <span data-ttu-id="c5cc5-248">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-249">return</span><span class="sxs-lookup"><span data-stu-id="c5cc5-249">return</span></span> | <span data-ttu-id="c5cc5-250">배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-250">Array</span></span> | <span data-ttu-id="c5cc5-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="c5cc5-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="c5cc5-252">contains</span><span class="sxs-lookup"><span data-stu-id="c5cc5-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="c5cc5-253">배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-254">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-254">Parameters</span></span>

| <span data-ttu-id="c5cc5-255">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-255">Parameter</span></span> | <span data-ttu-id="c5cc5-256">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-256">Required</span></span> | <span data-ttu-id="c5cc5-257">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-257">Type</span></span> | <span data-ttu-id="c5cc5-258">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-259">container</span><span class="sxs-lookup"><span data-stu-id="c5cc5-259">container</span></span> |<span data-ttu-id="c5cc5-260">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-260">Yes</span></span> |<span data-ttu-id="c5cc5-261">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-261">array, object, or string</span></span> |<span data-ttu-id="c5cc5-262">찾을 값을 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="c5cc5-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="c5cc5-263">itemToFind</span></span> |<span data-ttu-id="c5cc5-264">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-264">Yes</span></span> |<span data-ttu-id="c5cc5-265">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-265">string or int</span></span> |<span data-ttu-id="c5cc5-266">찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-267">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-267">Return value</span></span>

<span data-ttu-id="c5cc5-268">항목이 있으면 **True**이고, 항목이 없으면 **False**입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-269">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-269">Examples</span></span>

<span data-ttu-id="c5cc5-270">다음 예제에서는 여러 다른 형식의 contains를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="c5cc5-271">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-272">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-272">Name</span></span> | <span data-ttu-id="c5cc5-273">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-273">Type</span></span> | <span data-ttu-id="c5cc5-274">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-275">stringTrue</span></span> | <span data-ttu-id="c5cc5-276">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-276">Bool</span></span> | <span data-ttu-id="c5cc5-277">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-277">True</span></span> |
| <span data-ttu-id="c5cc5-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-278">stringFalse</span></span> | <span data-ttu-id="c5cc5-279">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-279">Bool</span></span> | <span data-ttu-id="c5cc5-280">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-280">False</span></span> |
| <span data-ttu-id="c5cc5-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-281">objectTrue</span></span> | <span data-ttu-id="c5cc5-282">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-282">Bool</span></span> | <span data-ttu-id="c5cc5-283">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-283">True</span></span> |
| <span data-ttu-id="c5cc5-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-284">objectFalse</span></span> | <span data-ttu-id="c5cc5-285">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-285">Bool</span></span> | <span data-ttu-id="c5cc5-286">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-286">False</span></span> |
| <span data-ttu-id="c5cc5-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-287">arrayTrue</span></span> | <span data-ttu-id="c5cc5-288">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-288">Bool</span></span> | <span data-ttu-id="c5cc5-289">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-289">True</span></span> |
| <span data-ttu-id="c5cc5-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-290">arrayFalse</span></span> | <span data-ttu-id="c5cc5-291">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-291">Bool</span></span> | <span data-ttu-id="c5cc5-292">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="c5cc5-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="c5cc5-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="c5cc5-294">값을 데이터 URI로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-295">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-295">Parameters</span></span>

| <span data-ttu-id="c5cc5-296">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-296">Parameter</span></span> | <span data-ttu-id="c5cc5-297">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-297">Required</span></span> | <span data-ttu-id="c5cc5-298">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-298">Type</span></span> | <span data-ttu-id="c5cc5-299">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="c5cc5-300">stringToConvert</span></span> |<span data-ttu-id="c5cc5-301">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-301">Yes</span></span> |<span data-ttu-id="c5cc5-302">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-302">string</span></span> |<span data-ttu-id="c5cc5-303">데이터 URI로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-304">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-304">Return value</span></span>

<span data-ttu-id="c5cc5-305">데이터 URI로 형식이 지정된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-306">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-306">Examples</span></span>

<span data-ttu-id="c5cc5-307">다음 예제에서는 값을 데이터 URI로 변환하고 데이터 URI를 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-308">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-309">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-309">Name</span></span> | <span data-ttu-id="c5cc5-310">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-310">Type</span></span> | <span data-ttu-id="c5cc5-311">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-312">dataUriOutput</span></span> | <span data-ttu-id="c5cc5-313">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-313">String</span></span> | <span data-ttu-id="c5cc5-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="c5cc5-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="c5cc5-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-315">toStringOutput</span></span> | <span data-ttu-id="c5cc5-316">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-316">String</span></span> | <span data-ttu-id="c5cc5-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="c5cc5-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="c5cc5-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="c5cc5-319">데이터 URI로 형식이 지정된 값을 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-320">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-320">Parameters</span></span>

| <span data-ttu-id="c5cc5-321">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-321">Parameter</span></span> | <span data-ttu-id="c5cc5-322">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-322">Required</span></span> | <span data-ttu-id="c5cc5-323">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-323">Type</span></span> | <span data-ttu-id="c5cc5-324">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="c5cc5-325">dataUriToConvert</span></span> |<span data-ttu-id="c5cc5-326">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-326">Yes</span></span> |<span data-ttu-id="c5cc5-327">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-327">string</span></span> |<span data-ttu-id="c5cc5-328">변환할 데이터 URI 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-329">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-329">Return value</span></span>

<span data-ttu-id="c5cc5-330">변환된 값을 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-331">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-331">Examples</span></span>

<span data-ttu-id="c5cc5-332">다음 예제에서는 값을 데이터 URI로 변환하고 데이터 URI를 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-333">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-334">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-334">Name</span></span> | <span data-ttu-id="c5cc5-335">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-335">Type</span></span> | <span data-ttu-id="c5cc5-336">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-337">dataUriOutput</span></span> | <span data-ttu-id="c5cc5-338">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-338">String</span></span> | <span data-ttu-id="c5cc5-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="c5cc5-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="c5cc5-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-340">toStringOutput</span></span> | <span data-ttu-id="c5cc5-341">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-341">String</span></span> | <span data-ttu-id="c5cc5-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="c5cc5-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="c5cc5-343">empty</span><span class="sxs-lookup"><span data-stu-id="c5cc5-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="c5cc5-344">배열, 개체 또는 문자열이 비어 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-345">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-345">Parameters</span></span>

| <span data-ttu-id="c5cc5-346">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-346">Parameter</span></span> | <span data-ttu-id="c5cc5-347">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-347">Required</span></span> | <span data-ttu-id="c5cc5-348">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-348">Type</span></span> | <span data-ttu-id="c5cc5-349">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="c5cc5-350">itemToTest</span></span> |<span data-ttu-id="c5cc5-351">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-351">Yes</span></span> |<span data-ttu-id="c5cc5-352">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-352">array, object, or string</span></span> |<span data-ttu-id="c5cc5-353">비어 있는지 확인할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-354">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-354">Return value</span></span>

<span data-ttu-id="c5cc5-355">값이 비어 있으면 **True**를 반환하고 비어 있지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-356">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-356">Examples</span></span>

<span data-ttu-id="c5cc5-357">다음 예제에서는 배열, 개체 및 문자열이 비어 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="c5cc5-358">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-359">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-359">Name</span></span> | <span data-ttu-id="c5cc5-360">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-360">Type</span></span> | <span data-ttu-id="c5cc5-361">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="c5cc5-362">arrayEmpty</span></span> | <span data-ttu-id="c5cc5-363">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-363">Bool</span></span> | <span data-ttu-id="c5cc5-364">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-364">True</span></span> |
| <span data-ttu-id="c5cc5-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="c5cc5-365">objectEmpty</span></span> | <span data-ttu-id="c5cc5-366">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-366">Bool</span></span> | <span data-ttu-id="c5cc5-367">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-367">True</span></span> |
| <span data-ttu-id="c5cc5-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="c5cc5-368">stringEmpty</span></span> | <span data-ttu-id="c5cc5-369">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-369">Bool</span></span> | <span data-ttu-id="c5cc5-370">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="c5cc5-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="c5cc5-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="c5cc5-372">문자열이 값으로 끝나는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="c5cc5-373">비교는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-374">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-374">Parameters</span></span>

| <span data-ttu-id="c5cc5-375">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-375">Parameter</span></span> | <span data-ttu-id="c5cc5-376">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-376">Required</span></span> | <span data-ttu-id="c5cc5-377">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-377">Type</span></span> | <span data-ttu-id="c5cc5-378">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="c5cc5-379">stringToSearch</span></span> |<span data-ttu-id="c5cc5-380">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-380">Yes</span></span> |<span data-ttu-id="c5cc5-381">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-381">string</span></span> |<span data-ttu-id="c5cc5-382">찾을 값을 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="c5cc5-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="c5cc5-383">stringToFind</span></span> |<span data-ttu-id="c5cc5-384">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-384">Yes</span></span> |<span data-ttu-id="c5cc5-385">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-385">string</span></span> |<span data-ttu-id="c5cc5-386">찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-387">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-387">Return value</span></span>

<span data-ttu-id="c5cc5-388">마지막 문자 또는 문자열의 문자가 값과 일치하면 **True**이고, 일치하지 않으면 **False**입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-389">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-389">Examples</span></span>

<span data-ttu-id="c5cc5-390">다음 예제에서는 startsWith 및 endsWith 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="c5cc5-391">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-392">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-392">Name</span></span> | <span data-ttu-id="c5cc5-393">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-393">Type</span></span> | <span data-ttu-id="c5cc5-394">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-395">startsTrue</span></span> | <span data-ttu-id="c5cc5-396">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-396">Bool</span></span> | <span data-ttu-id="c5cc5-397">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-397">True</span></span> |
| <span data-ttu-id="c5cc5-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-398">startsCapTrue</span></span> | <span data-ttu-id="c5cc5-399">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-399">Bool</span></span> | <span data-ttu-id="c5cc5-400">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-400">True</span></span> |
| <span data-ttu-id="c5cc5-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-401">startsFalse</span></span> | <span data-ttu-id="c5cc5-402">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-402">Bool</span></span> | <span data-ttu-id="c5cc5-403">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-403">False</span></span> |
| <span data-ttu-id="c5cc5-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-404">endsTrue</span></span> | <span data-ttu-id="c5cc5-405">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-405">Bool</span></span> | <span data-ttu-id="c5cc5-406">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-406">True</span></span> |
| <span data-ttu-id="c5cc5-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-407">endsCapTrue</span></span> | <span data-ttu-id="c5cc5-408">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-408">Bool</span></span> | <span data-ttu-id="c5cc5-409">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-409">True</span></span> |
| <span data-ttu-id="c5cc5-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-410">endsFalse</span></span> | <span data-ttu-id="c5cc5-411">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-411">Bool</span></span> | <span data-ttu-id="c5cc5-412">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="c5cc5-413">first</span><span class="sxs-lookup"><span data-stu-id="c5cc5-413">first</span></span>
`first(arg1)`

<span data-ttu-id="c5cc5-414">문자열의 첫 번째 문자 또는 배열의 첫 번째 요소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-415">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-415">Parameters</span></span>

| <span data-ttu-id="c5cc5-416">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-416">Parameter</span></span> | <span data-ttu-id="c5cc5-417">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-417">Required</span></span> | <span data-ttu-id="c5cc5-418">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-418">Type</span></span> | <span data-ttu-id="c5cc5-419">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-420">arg1</span><span class="sxs-lookup"><span data-stu-id="c5cc5-420">arg1</span></span> |<span data-ttu-id="c5cc5-421">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-421">Yes</span></span> |<span data-ttu-id="c5cc5-422">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-422">array or string</span></span> |<span data-ttu-id="c5cc5-423">첫 번째 요소 또는 문자를 검색할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-424">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-424">Return value</span></span>

<span data-ttu-id="c5cc5-425">배열의 첫 번째 문자의 문자열 또는 첫 번째 요소의 형식(문자열, int, 배열 또는 개체)입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-426">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-426">Examples</span></span>

<span data-ttu-id="c5cc5-427">다음 예제에서는 배열 및 문자열에 첫 번째 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="c5cc5-428">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-429">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-429">Name</span></span> | <span data-ttu-id="c5cc5-430">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-430">Type</span></span> | <span data-ttu-id="c5cc5-431">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-432">arrayOutput</span></span> | <span data-ttu-id="c5cc5-433">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-433">String</span></span> | <span data-ttu-id="c5cc5-434">one</span><span class="sxs-lookup"><span data-stu-id="c5cc5-434">one</span></span> |
| <span data-ttu-id="c5cc5-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-435">stringOutput</span></span> | <span data-ttu-id="c5cc5-436">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-436">String</span></span> | <span data-ttu-id="c5cc5-437">O</span><span class="sxs-lookup"><span data-stu-id="c5cc5-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="c5cc5-438">indexof</span><span class="sxs-lookup"><span data-stu-id="c5cc5-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="c5cc5-439">문자열 내 값의 첫 번째 위치를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="c5cc5-440">비교는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-441">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-441">Parameters</span></span>

| <span data-ttu-id="c5cc5-442">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-442">Parameter</span></span> | <span data-ttu-id="c5cc5-443">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-443">Required</span></span> | <span data-ttu-id="c5cc5-444">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-444">Type</span></span> | <span data-ttu-id="c5cc5-445">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="c5cc5-446">stringToSearch</span></span> |<span data-ttu-id="c5cc5-447">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-447">Yes</span></span> |<span data-ttu-id="c5cc5-448">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-448">string</span></span> |<span data-ttu-id="c5cc5-449">찾을 값을 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="c5cc5-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="c5cc5-450">stringToFind</span></span> |<span data-ttu-id="c5cc5-451">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-451">Yes</span></span> |<span data-ttu-id="c5cc5-452">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-452">string</span></span> |<span data-ttu-id="c5cc5-453">찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-454">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-454">Return value</span></span>

<span data-ttu-id="c5cc5-455">찾을 항목의 위치를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="c5cc5-456">값은 0부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-456">The value is zero-based.</span></span> <span data-ttu-id="c5cc5-457">항목이 없는 경우 -1이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-458">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-458">Examples</span></span>

<span data-ttu-id="c5cc5-459">다음 예제에서는 indexOf 및 lastIndexOf 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="c5cc5-460">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-461">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-461">Name</span></span> | <span data-ttu-id="c5cc5-462">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-462">Type</span></span> | <span data-ttu-id="c5cc5-463">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-464">firstT</span><span class="sxs-lookup"><span data-stu-id="c5cc5-464">firstT</span></span> | <span data-ttu-id="c5cc5-465">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-465">Int</span></span> | <span data-ttu-id="c5cc5-466">0</span><span class="sxs-lookup"><span data-stu-id="c5cc5-466">0</span></span> |
| <span data-ttu-id="c5cc5-467">lastT</span><span class="sxs-lookup"><span data-stu-id="c5cc5-467">lastT</span></span> | <span data-ttu-id="c5cc5-468">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-468">Int</span></span> | <span data-ttu-id="c5cc5-469">3</span><span class="sxs-lookup"><span data-stu-id="c5cc5-469">3</span></span> |
| <span data-ttu-id="c5cc5-470">firstString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-470">firstString</span></span> | <span data-ttu-id="c5cc5-471">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-471">Int</span></span> | <span data-ttu-id="c5cc5-472">2</span><span class="sxs-lookup"><span data-stu-id="c5cc5-472">2</span></span> |
| <span data-ttu-id="c5cc5-473">lastString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-473">lastString</span></span> | <span data-ttu-id="c5cc5-474">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-474">Int</span></span> | <span data-ttu-id="c5cc5-475">0</span><span class="sxs-lookup"><span data-stu-id="c5cc5-475">0</span></span> |
| <span data-ttu-id="c5cc5-476">notFound</span><span class="sxs-lookup"><span data-stu-id="c5cc5-476">notFound</span></span> | <span data-ttu-id="c5cc5-477">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-477">Int</span></span> | <span data-ttu-id="c5cc5-478">-1</span><span class="sxs-lookup"><span data-stu-id="c5cc5-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="c5cc5-479">last</span><span class="sxs-lookup"><span data-stu-id="c5cc5-479">last</span></span>
`last (arg1)`

<span data-ttu-id="c5cc5-480">문자열의 마지막 문자 또는 배열의 마지막 요소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-481">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-481">Parameters</span></span>

| <span data-ttu-id="c5cc5-482">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-482">Parameter</span></span> | <span data-ttu-id="c5cc5-483">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-483">Required</span></span> | <span data-ttu-id="c5cc5-484">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-484">Type</span></span> | <span data-ttu-id="c5cc5-485">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-486">arg1</span><span class="sxs-lookup"><span data-stu-id="c5cc5-486">arg1</span></span> |<span data-ttu-id="c5cc5-487">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-487">Yes</span></span> |<span data-ttu-id="c5cc5-488">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-488">array or string</span></span> |<span data-ttu-id="c5cc5-489">마지막 요소 또는 문자를 검색할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-490">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-490">Return value</span></span>

<span data-ttu-id="c5cc5-491">배열의 마지막 문자의 문자열 또는 마지막 요소의 형식(문자열, int, 배열 또는 개체)입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-492">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-492">Examples</span></span>

<span data-ttu-id="c5cc5-493">다음 예제에서는 배열 및 문자열에 마지막 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="c5cc5-494">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-495">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-495">Name</span></span> | <span data-ttu-id="c5cc5-496">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-496">Type</span></span> | <span data-ttu-id="c5cc5-497">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-498">arrayOutput</span></span> | <span data-ttu-id="c5cc5-499">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-499">String</span></span> | <span data-ttu-id="c5cc5-500">three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-500">three</span></span> |
| <span data-ttu-id="c5cc5-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-501">stringOutput</span></span> | <span data-ttu-id="c5cc5-502">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-502">String</span></span> | <span data-ttu-id="c5cc5-503">e</span><span class="sxs-lookup"><span data-stu-id="c5cc5-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="c5cc5-504">lastindexof</span><span class="sxs-lookup"><span data-stu-id="c5cc5-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="c5cc5-505">문자열 내 값의 마지막 위치를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="c5cc5-506">비교는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-507">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-507">Parameters</span></span>

| <span data-ttu-id="c5cc5-508">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-508">Parameter</span></span> | <span data-ttu-id="c5cc5-509">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-509">Required</span></span> | <span data-ttu-id="c5cc5-510">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-510">Type</span></span> | <span data-ttu-id="c5cc5-511">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="c5cc5-512">stringToSearch</span></span> |<span data-ttu-id="c5cc5-513">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-513">Yes</span></span> |<span data-ttu-id="c5cc5-514">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-514">string</span></span> |<span data-ttu-id="c5cc5-515">찾을 값을 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="c5cc5-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="c5cc5-516">stringToFind</span></span> |<span data-ttu-id="c5cc5-517">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-517">Yes</span></span> |<span data-ttu-id="c5cc5-518">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-518">string</span></span> |<span data-ttu-id="c5cc5-519">찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-520">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-520">Return value</span></span>

<span data-ttu-id="c5cc5-521">찾을 항목의 마지막 위치를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="c5cc5-522">값은 0부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-522">The value is zero-based.</span></span> <span data-ttu-id="c5cc5-523">항목이 없는 경우 -1이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-524">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-524">Examples</span></span>

<span data-ttu-id="c5cc5-525">다음 예제에서는 indexOf 및 lastIndexOf 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="c5cc5-526">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-527">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-527">Name</span></span> | <span data-ttu-id="c5cc5-528">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-528">Type</span></span> | <span data-ttu-id="c5cc5-529">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-530">firstT</span><span class="sxs-lookup"><span data-stu-id="c5cc5-530">firstT</span></span> | <span data-ttu-id="c5cc5-531">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-531">Int</span></span> | <span data-ttu-id="c5cc5-532">0</span><span class="sxs-lookup"><span data-stu-id="c5cc5-532">0</span></span> |
| <span data-ttu-id="c5cc5-533">lastT</span><span class="sxs-lookup"><span data-stu-id="c5cc5-533">lastT</span></span> | <span data-ttu-id="c5cc5-534">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-534">Int</span></span> | <span data-ttu-id="c5cc5-535">3</span><span class="sxs-lookup"><span data-stu-id="c5cc5-535">3</span></span> |
| <span data-ttu-id="c5cc5-536">firstString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-536">firstString</span></span> | <span data-ttu-id="c5cc5-537">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-537">Int</span></span> | <span data-ttu-id="c5cc5-538">2</span><span class="sxs-lookup"><span data-stu-id="c5cc5-538">2</span></span> |
| <span data-ttu-id="c5cc5-539">lastString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-539">lastString</span></span> | <span data-ttu-id="c5cc5-540">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-540">Int</span></span> | <span data-ttu-id="c5cc5-541">0</span><span class="sxs-lookup"><span data-stu-id="c5cc5-541">0</span></span> |
| <span data-ttu-id="c5cc5-542">notFound</span><span class="sxs-lookup"><span data-stu-id="c5cc5-542">notFound</span></span> | <span data-ttu-id="c5cc5-543">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-543">Int</span></span> | <span data-ttu-id="c5cc5-544">-1</span><span class="sxs-lookup"><span data-stu-id="c5cc5-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="c5cc5-545">length</span><span class="sxs-lookup"><span data-stu-id="c5cc5-545">length</span></span>
`length(string)`

<span data-ttu-id="c5cc5-546">문자열의 문자 수 또는 배열의 요소 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-547">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-547">Parameters</span></span>

| <span data-ttu-id="c5cc5-548">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-548">Parameter</span></span> | <span data-ttu-id="c5cc5-549">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-549">Required</span></span> | <span data-ttu-id="c5cc5-550">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-550">Type</span></span> | <span data-ttu-id="c5cc5-551">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-552">arg1</span><span class="sxs-lookup"><span data-stu-id="c5cc5-552">arg1</span></span> |<span data-ttu-id="c5cc5-553">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-553">Yes</span></span> |<span data-ttu-id="c5cc5-554">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-554">array or string</span></span> |<span data-ttu-id="c5cc5-555">요소 수를 가져오는 데 사용할 배열 또는 문자 수를 가져오는 데 사용할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-556">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-556">Return value</span></span>

<span data-ttu-id="c5cc5-557">int입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="c5cc5-558">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-558">Examples</span></span>

<span data-ttu-id="c5cc5-559">다음 예제에서는 배열 및 문자열에 length를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="c5cc5-560">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-561">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-561">Name</span></span> | <span data-ttu-id="c5cc5-562">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-562">Type</span></span> | <span data-ttu-id="c5cc5-563">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="c5cc5-564">arrayLength</span></span> | <span data-ttu-id="c5cc5-565">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-565">Int</span></span> | <span data-ttu-id="c5cc5-566">3</span><span class="sxs-lookup"><span data-stu-id="c5cc5-566">3</span></span> |
| <span data-ttu-id="c5cc5-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="c5cc5-567">stringLength</span></span> | <span data-ttu-id="c5cc5-568">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-568">Int</span></span> | <span data-ttu-id="c5cc5-569">13</span><span class="sxs-lookup"><span data-stu-id="c5cc5-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="c5cc5-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="c5cc5-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="c5cc5-571">지정된 총 길이에 도달할 때까지 왼쪽에 문자를 추가하여 오른쪽 맞추어진 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-572">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-572">Parameters</span></span>

| <span data-ttu-id="c5cc5-573">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-573">Parameter</span></span> | <span data-ttu-id="c5cc5-574">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-574">Required</span></span> | <span data-ttu-id="c5cc5-575">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-575">Type</span></span> | <span data-ttu-id="c5cc5-576">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="c5cc5-577">valueToPad</span></span> |<span data-ttu-id="c5cc5-578">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-578">Yes</span></span> |<span data-ttu-id="c5cc5-579">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-579">string or int</span></span> |<span data-ttu-id="c5cc5-580">오른쪽으로 맞출 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-580">The value to right-align.</span></span> |
| <span data-ttu-id="c5cc5-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="c5cc5-581">totalLength</span></span> |<span data-ttu-id="c5cc5-582">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-582">Yes</span></span> |<span data-ttu-id="c5cc5-583">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-583">int</span></span> |<span data-ttu-id="c5cc5-584">반환된 문자열에서 문자의 총수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="c5cc5-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="c5cc5-585">paddingCharacter</span></span> |<span data-ttu-id="c5cc5-586">아니요</span><span class="sxs-lookup"><span data-stu-id="c5cc5-586">No</span></span> |<span data-ttu-id="c5cc5-587">단일 문자</span><span class="sxs-lookup"><span data-stu-id="c5cc5-587">single character</span></span> |<span data-ttu-id="c5cc5-588">총 길이에 도달할 때까지 왼쪽 여백에 사용되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="c5cc5-589">기본값은 공백입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-589">The default value is a space.</span></span> |

<span data-ttu-id="c5cc5-590">원래 문자열이 채울 문자 수보다 긴 경우 문자가 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="c5cc5-591">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-591">Return value</span></span>

<span data-ttu-id="c5cc5-592">최소한 지정된 문자의 수를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-593">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-593">Examples</span></span>

<span data-ttu-id="c5cc5-594">다음 예제는 문자열이 총 문자 수에 도달할 때까지 0 문자를 추가하여 사용자가 제공한 매개 변수 값을 채우는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="c5cc5-595">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-596">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-596">Name</span></span> | <span data-ttu-id="c5cc5-597">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-597">Type</span></span> | <span data-ttu-id="c5cc5-598">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-599">stringOutput</span></span> | <span data-ttu-id="c5cc5-600">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-600">String</span></span> | <span data-ttu-id="c5cc5-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="c5cc5-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="c5cc5-602">바꾸기</span><span class="sxs-lookup"><span data-stu-id="c5cc5-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="c5cc5-603">다른 문자열로 대체한 어떤 문자열의 인스턴스를 포함한 새 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-604">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-604">Parameters</span></span>

| <span data-ttu-id="c5cc5-605">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-605">Parameter</span></span> | <span data-ttu-id="c5cc5-606">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-606">Required</span></span> | <span data-ttu-id="c5cc5-607">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-607">Type</span></span> | <span data-ttu-id="c5cc5-608">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-609">originalString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-609">originalString</span></span> |<span data-ttu-id="c5cc5-610">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-610">Yes</span></span> |<span data-ttu-id="c5cc5-611">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-611">string</span></span> |<span data-ttu-id="c5cc5-612">다른 문자열로 대체한 어떤 문자열의 인스턴스를 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="c5cc5-613">oldString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-613">oldString</span></span> |<span data-ttu-id="c5cc5-614">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-614">Yes</span></span> |<span data-ttu-id="c5cc5-615">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-615">string</span></span> |<span data-ttu-id="c5cc5-616">원래 문자열에서 제거할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="c5cc5-617">newString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-617">newString</span></span> |<span data-ttu-id="c5cc5-618">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-618">Yes</span></span> |<span data-ttu-id="c5cc5-619">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-619">string</span></span> |<span data-ttu-id="c5cc5-620">제거된 문자열 대신 추가할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-621">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-621">Return value</span></span>

<span data-ttu-id="c5cc5-622">문자가 대체된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-623">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-623">Examples</span></span>

<span data-ttu-id="c5cc5-624">다음 예제에서는 사용자가 제공한 문자열에서 모든 대시를 제거하는 방법 및 문자열의 일부를 다른 문자열로 대체하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="c5cc5-625">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-626">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-626">Name</span></span> | <span data-ttu-id="c5cc5-627">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-627">Type</span></span> | <span data-ttu-id="c5cc5-628">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-629">firstOutput</span></span> | <span data-ttu-id="c5cc5-630">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-630">String</span></span> | <span data-ttu-id="c5cc5-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="c5cc5-631">1231231234</span></span> |
| <span data-ttu-id="c5cc5-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-632">secodeOutput</span></span> | <span data-ttu-id="c5cc5-633">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-633">String</span></span> | <span data-ttu-id="c5cc5-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="c5cc5-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="c5cc5-635">skip</span><span class="sxs-lookup"><span data-stu-id="c5cc5-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="c5cc5-636">지정된 문자 수 이후의 모든 문자를 포함하는 문자열 또는 지정된 요소 수 이후의 모든 요소를 포함하는 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-637">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-637">Parameters</span></span>

| <span data-ttu-id="c5cc5-638">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-638">Parameter</span></span> | <span data-ttu-id="c5cc5-639">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-639">Required</span></span> | <span data-ttu-id="c5cc5-640">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-640">Type</span></span> | <span data-ttu-id="c5cc5-641">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-642">originalValue</span></span> |<span data-ttu-id="c5cc5-643">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-643">Yes</span></span> |<span data-ttu-id="c5cc5-644">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-644">array or string</span></span> |<span data-ttu-id="c5cc5-645">건너뛰는 데 사용할 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="c5cc5-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="c5cc5-646">numberToSkip</span></span> |<span data-ttu-id="c5cc5-647">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-647">Yes</span></span> |<span data-ttu-id="c5cc5-648">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-648">int</span></span> |<span data-ttu-id="c5cc5-649">건너뛸 요소 또는 문자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="c5cc5-650">이 값이 0 이하이면 값의 모든 요소 또는 문자가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="c5cc5-651">이 값이 배열 또는 문자열의 길이보다 크면 빈 배열 또는 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-652">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-652">Return value</span></span>

<span data-ttu-id="c5cc5-653">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-654">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-654">Examples</span></span>

<span data-ttu-id="c5cc5-655">다음 예제에서는 배열에서 지정된 요소 수 및 문자열에서 지정된 수의 문자를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="c5cc5-656">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-657">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-657">Name</span></span> | <span data-ttu-id="c5cc5-658">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-658">Type</span></span> | <span data-ttu-id="c5cc5-659">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-660">arrayOutput</span></span> | <span data-ttu-id="c5cc5-661">배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-661">Array</span></span> | <span data-ttu-id="c5cc5-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="c5cc5-662">["three"]</span></span> |
| <span data-ttu-id="c5cc5-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-663">stringOutput</span></span> | <span data-ttu-id="c5cc5-664">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-664">String</span></span> | <span data-ttu-id="c5cc5-665">two three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="c5cc5-666">분할</span><span class="sxs-lookup"><span data-stu-id="c5cc5-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="c5cc5-667">지정된 구분 기호로 구분되는 입력 문자열의 부분 문자열을 포함하는 문자열의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-668">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-668">Parameters</span></span>

| <span data-ttu-id="c5cc5-669">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-669">Parameter</span></span> | <span data-ttu-id="c5cc5-670">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-670">Required</span></span> | <span data-ttu-id="c5cc5-671">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-671">Type</span></span> | <span data-ttu-id="c5cc5-672">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-673">inputString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-673">inputString</span></span> |<span data-ttu-id="c5cc5-674">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-674">Yes</span></span> |<span data-ttu-id="c5cc5-675">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-675">string</span></span> |<span data-ttu-id="c5cc5-676">분할할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-676">The string to split.</span></span> |
| <span data-ttu-id="c5cc5-677">구분 기호</span><span class="sxs-lookup"><span data-stu-id="c5cc5-677">delimiter</span></span> |<span data-ttu-id="c5cc5-678">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-678">Yes</span></span> |<span data-ttu-id="c5cc5-679">문자열 또는 문자열 배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-679">string or array of strings</span></span> |<span data-ttu-id="c5cc5-680">문자열 분할에 사용할 구분 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-681">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-681">Return value</span></span>

<span data-ttu-id="c5cc5-682">문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-683">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-683">Examples</span></span>

<span data-ttu-id="c5cc5-684">다음 예제에서는 쉼표를 사용하여 또는 쉼표 또는 세미콜론을 사용하여 입력 문자열을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-685">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-686">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-686">Name</span></span> | <span data-ttu-id="c5cc5-687">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-687">Type</span></span> | <span data-ttu-id="c5cc5-688">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-689">firstOutput</span></span> | <span data-ttu-id="c5cc5-690">배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-690">Array</span></span> | <span data-ttu-id="c5cc5-691">[“one”, “two”, “three”]</span><span class="sxs-lookup"><span data-stu-id="c5cc5-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="c5cc5-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-692">secondOutput</span></span> | <span data-ttu-id="c5cc5-693">배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-693">Array</span></span> | <span data-ttu-id="c5cc5-694">[“one”, “two”, “three”]</span><span class="sxs-lookup"><span data-stu-id="c5cc5-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="c5cc5-695">startswith</span><span class="sxs-lookup"><span data-stu-id="c5cc5-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="c5cc5-696">문자열이 값으로 시작하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="c5cc5-697">비교는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-698">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-698">Parameters</span></span>

| <span data-ttu-id="c5cc5-699">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-699">Parameter</span></span> | <span data-ttu-id="c5cc5-700">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-700">Required</span></span> | <span data-ttu-id="c5cc5-701">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-701">Type</span></span> | <span data-ttu-id="c5cc5-702">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="c5cc5-703">stringToSearch</span></span> |<span data-ttu-id="c5cc5-704">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-704">Yes</span></span> |<span data-ttu-id="c5cc5-705">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-705">string</span></span> |<span data-ttu-id="c5cc5-706">찾을 값을 포함하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="c5cc5-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="c5cc5-707">stringToFind</span></span> |<span data-ttu-id="c5cc5-708">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-708">Yes</span></span> |<span data-ttu-id="c5cc5-709">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-709">string</span></span> |<span data-ttu-id="c5cc5-710">찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-711">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-711">Return value</span></span>

<span data-ttu-id="c5cc5-712">첫 번째 문자 또는 문자열의 문자가 값과 일치하면 **True**이고, 일치하지 않으면 **False**입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-713">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-713">Examples</span></span>

<span data-ttu-id="c5cc5-714">다음 예제에서는 startsWith 및 endsWith 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="c5cc5-715">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-716">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-716">Name</span></span> | <span data-ttu-id="c5cc5-717">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-717">Type</span></span> | <span data-ttu-id="c5cc5-718">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-719">startsTrue</span></span> | <span data-ttu-id="c5cc5-720">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-720">Bool</span></span> | <span data-ttu-id="c5cc5-721">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-721">True</span></span> |
| <span data-ttu-id="c5cc5-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-722">startsCapTrue</span></span> | <span data-ttu-id="c5cc5-723">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-723">Bool</span></span> | <span data-ttu-id="c5cc5-724">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-724">True</span></span> |
| <span data-ttu-id="c5cc5-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-725">startsFalse</span></span> | <span data-ttu-id="c5cc5-726">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-726">Bool</span></span> | <span data-ttu-id="c5cc5-727">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-727">False</span></span> |
| <span data-ttu-id="c5cc5-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-728">endsTrue</span></span> | <span data-ttu-id="c5cc5-729">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-729">Bool</span></span> | <span data-ttu-id="c5cc5-730">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-730">True</span></span> |
| <span data-ttu-id="c5cc5-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-731">endsCapTrue</span></span> | <span data-ttu-id="c5cc5-732">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-732">Bool</span></span> | <span data-ttu-id="c5cc5-733">True</span><span class="sxs-lookup"><span data-stu-id="c5cc5-733">True</span></span> |
| <span data-ttu-id="c5cc5-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-734">endsFalse</span></span> | <span data-ttu-id="c5cc5-735">Bool</span><span class="sxs-lookup"><span data-stu-id="c5cc5-735">Bool</span></span> | <span data-ttu-id="c5cc5-736">False</span><span class="sxs-lookup"><span data-stu-id="c5cc5-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="c5cc5-737">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="c5cc5-738">지정된 값을 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-739">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-739">Parameters</span></span>

| <span data-ttu-id="c5cc5-740">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-740">Parameter</span></span> | <span data-ttu-id="c5cc5-741">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-741">Required</span></span> | <span data-ttu-id="c5cc5-742">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-742">Type</span></span> | <span data-ttu-id="c5cc5-743">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="c5cc5-744">valueToConvert</span></span> |<span data-ttu-id="c5cc5-745">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-745">Yes</span></span> | <span data-ttu-id="c5cc5-746">모두</span><span class="sxs-lookup"><span data-stu-id="c5cc5-746">Any</span></span> |<span data-ttu-id="c5cc5-747">문자열로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-747">The value to convert to string.</span></span> <span data-ttu-id="c5cc5-748">개체 및 배열을 비롯하여 모든 값 형식을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-749">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-749">Return value</span></span>

<span data-ttu-id="c5cc5-750">변환된 값의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-751">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-751">Examples</span></span>

<span data-ttu-id="c5cc5-752">다음 예제에서는 다른 형식의 값을 문자열로 변환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-752">The following example shows how to convert different types of values to strings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-753">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-754">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-754">Name</span></span> | <span data-ttu-id="c5cc5-755">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-755">Type</span></span> | <span data-ttu-id="c5cc5-756">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-757">objectOutput</span></span> | <span data-ttu-id="c5cc5-758">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-758">String</span></span> | <span data-ttu-id="c5cc5-759">{“valueA”:10,“valueB”:“Example Text”}</span><span class="sxs-lookup"><span data-stu-id="c5cc5-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="c5cc5-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-760">arrayOutput</span></span> | <span data-ttu-id="c5cc5-761">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-761">String</span></span> | <span data-ttu-id="c5cc5-762">[“a”,“b”,“c”]</span><span class="sxs-lookup"><span data-stu-id="c5cc5-762">["a","b","c"]</span></span> |
| <span data-ttu-id="c5cc5-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-763">intOutput</span></span> | <span data-ttu-id="c5cc5-764">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-764">String</span></span> | <span data-ttu-id="c5cc5-765">5</span><span class="sxs-lookup"><span data-stu-id="c5cc5-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="c5cc5-766">substring</span><span class="sxs-lookup"><span data-stu-id="c5cc5-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="c5cc5-767">지정된 문자 위치에서 시작하고 지정한 개수의 문자를 포함하는 부분 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-768">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-768">Parameters</span></span>

| <span data-ttu-id="c5cc5-769">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-769">Parameter</span></span> | <span data-ttu-id="c5cc5-770">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-770">Required</span></span> | <span data-ttu-id="c5cc5-771">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-771">Type</span></span> | <span data-ttu-id="c5cc5-772">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="c5cc5-773">stringToParse</span></span> |<span data-ttu-id="c5cc5-774">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-774">Yes</span></span> |<span data-ttu-id="c5cc5-775">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-775">string</span></span> |<span data-ttu-id="c5cc5-776">부분 문자열을 추출할 원래 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="c5cc5-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="c5cc5-777">startIndex</span></span> |<span data-ttu-id="c5cc5-778">아니요</span><span class="sxs-lookup"><span data-stu-id="c5cc5-778">No</span></span> |<span data-ttu-id="c5cc5-779">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-779">int</span></span> |<span data-ttu-id="c5cc5-780">부분 문자열의 0부터 시작하는 문자 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="c5cc5-781">length</span><span class="sxs-lookup"><span data-stu-id="c5cc5-781">length</span></span> |<span data-ttu-id="c5cc5-782">아니요</span><span class="sxs-lookup"><span data-stu-id="c5cc5-782">No</span></span> |<span data-ttu-id="c5cc5-783">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-783">int</span></span> |<span data-ttu-id="c5cc5-784">부분 문자열에 대한 문자 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-784">The number of characters for the substring.</span></span> <span data-ttu-id="c5cc5-785">문자열 내 위치를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-786">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-786">Return value</span></span>

<span data-ttu-id="c5cc5-787">하위 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="c5cc5-788">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-788">Remarks</span></span>

<span data-ttu-id="c5cc5-789">함수는 부분 문자열이 문자열의 끝을 넘어 확장하는 경우 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="c5cc5-790">다음 예제는 "인덱스 및 길이 매개 변수는 문자열 내 위치를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="c5cc5-791">인덱스 매개 변수: '0', 길이 매개 변수: '11', 문자열 매개 변수의 길이: '10'." 오류와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="c5cc5-792">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-792">Examples</span></span>

<span data-ttu-id="c5cc5-793">다음 예제에서는 매개 변수에서 하위 문자열을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-793">The following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="c5cc5-794">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-795">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-795">Name</span></span> | <span data-ttu-id="c5cc5-796">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-796">Type</span></span> | <span data-ttu-id="c5cc5-797">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-798">substringOutput</span></span> | <span data-ttu-id="c5cc5-799">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-799">String</span></span> | <span data-ttu-id="c5cc5-800">two</span><span class="sxs-lookup"><span data-stu-id="c5cc5-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="c5cc5-801">take</span><span class="sxs-lookup"><span data-stu-id="c5cc5-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="c5cc5-802">문자열 시작부터 지정된 수의 문자를 포함하는 문자열 또는 배열 시작부터 지정된 수의 요소를 포함하는 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-803">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-803">Parameters</span></span>

| <span data-ttu-id="c5cc5-804">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-804">Parameter</span></span> | <span data-ttu-id="c5cc5-805">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-805">Required</span></span> | <span data-ttu-id="c5cc5-806">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-806">Type</span></span> | <span data-ttu-id="c5cc5-807">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="c5cc5-808">originalValue</span></span> |<span data-ttu-id="c5cc5-809">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-809">Yes</span></span> |<span data-ttu-id="c5cc5-810">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-810">array or string</span></span> |<span data-ttu-id="c5cc5-811">요소를 가져올 배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="c5cc5-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="c5cc5-812">numberToTake</span></span> |<span data-ttu-id="c5cc5-813">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-813">Yes</span></span> |<span data-ttu-id="c5cc5-814">int</span><span class="sxs-lookup"><span data-stu-id="c5cc5-814">int</span></span> |<span data-ttu-id="c5cc5-815">수락할 요소 또는 문자의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-815">The number of elements or characters to take.</span></span> <span data-ttu-id="c5cc5-816">이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="c5cc5-817">지정된 배열 또는 문자열의 길이보다 크면 배열 또는 문자열의 모든 요소가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-818">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-818">Return value</span></span>

<span data-ttu-id="c5cc5-819">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-820">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-820">Examples</span></span>

<span data-ttu-id="c5cc5-821">다음 예제에서는 배열에서 지정된 수의 요소 및 문자열의 문자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="c5cc5-822">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-823">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-823">Name</span></span> | <span data-ttu-id="c5cc5-824">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-824">Type</span></span> | <span data-ttu-id="c5cc5-825">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-826">arrayOutput</span></span> | <span data-ttu-id="c5cc5-827">배열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-827">Array</span></span> | <span data-ttu-id="c5cc5-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="c5cc5-828">["one", "two"]</span></span> |
| <span data-ttu-id="c5cc5-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-829">stringOutput</span></span> | <span data-ttu-id="c5cc5-830">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-830">String</span></span> | <span data-ttu-id="c5cc5-831">on</span><span class="sxs-lookup"><span data-stu-id="c5cc5-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="c5cc5-832">toLower</span><span class="sxs-lookup"><span data-stu-id="c5cc5-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="c5cc5-833">지정된 문자열을 소문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-834">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-834">Parameters</span></span>

| <span data-ttu-id="c5cc5-835">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-835">Parameter</span></span> | <span data-ttu-id="c5cc5-836">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-836">Required</span></span> | <span data-ttu-id="c5cc5-837">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-837">Type</span></span> | <span data-ttu-id="c5cc5-838">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="c5cc5-839">stringToChange</span></span> |<span data-ttu-id="c5cc5-840">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-840">Yes</span></span> |<span data-ttu-id="c5cc5-841">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-841">string</span></span> |<span data-ttu-id="c5cc5-842">소문자로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-843">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-843">Return value</span></span>

<span data-ttu-id="c5cc5-844">소문자로 변환된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-845">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-845">Examples</span></span>

<span data-ttu-id="c5cc5-846">다음 예제는 매개 변수 값을 소문자 및 대문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-846">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-847">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-848">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-848">Name</span></span> | <span data-ttu-id="c5cc5-849">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-849">Type</span></span> | <span data-ttu-id="c5cc5-850">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-851">toLowerOutput</span></span> | <span data-ttu-id="c5cc5-852">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-852">String</span></span> | <span data-ttu-id="c5cc5-853">one two three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-853">one two three</span></span> |
| <span data-ttu-id="c5cc5-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-854">toUpperOutput</span></span> | <span data-ttu-id="c5cc5-855">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-855">String</span></span> | <span data-ttu-id="c5cc5-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="c5cc5-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="c5cc5-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="c5cc5-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="c5cc5-858">지정된 문자열을 대문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-859">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-859">Parameters</span></span>

| <span data-ttu-id="c5cc5-860">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-860">Parameter</span></span> | <span data-ttu-id="c5cc5-861">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-861">Required</span></span> | <span data-ttu-id="c5cc5-862">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-862">Type</span></span> | <span data-ttu-id="c5cc5-863">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="c5cc5-864">stringToChange</span></span> |<span data-ttu-id="c5cc5-865">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-865">Yes</span></span> |<span data-ttu-id="c5cc5-866">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-866">string</span></span> |<span data-ttu-id="c5cc5-867">대문자로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-868">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-868">Return value</span></span>

<span data-ttu-id="c5cc5-869">대문자로 변환된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-870">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-870">Examples</span></span>

<span data-ttu-id="c5cc5-871">다음 예제는 매개 변수 값을 소문자 및 대문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-871">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-872">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-873">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-873">Name</span></span> | <span data-ttu-id="c5cc5-874">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-874">Type</span></span> | <span data-ttu-id="c5cc5-875">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-876">toLowerOutput</span></span> | <span data-ttu-id="c5cc5-877">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-877">String</span></span> | <span data-ttu-id="c5cc5-878">one two three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-878">one two three</span></span> |
| <span data-ttu-id="c5cc5-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-879">toUpperOutput</span></span> | <span data-ttu-id="c5cc5-880">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-880">String</span></span> | <span data-ttu-id="c5cc5-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="c5cc5-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="c5cc5-882">trim</span><span class="sxs-lookup"><span data-stu-id="c5cc5-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="c5cc5-883">지정된 문자열에서 모든 선행 및 후행 공백 문자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-884">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-884">Parameters</span></span>

| <span data-ttu-id="c5cc5-885">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-885">Parameter</span></span> | <span data-ttu-id="c5cc5-886">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-886">Required</span></span> | <span data-ttu-id="c5cc5-887">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-887">Type</span></span> | <span data-ttu-id="c5cc5-888">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="c5cc5-889">stringToTrim</span></span> |<span data-ttu-id="c5cc5-890">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-890">Yes</span></span> |<span data-ttu-id="c5cc5-891">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-891">string</span></span> |<span data-ttu-id="c5cc5-892">자를 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-893">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-893">Return value</span></span>

<span data-ttu-id="c5cc5-894">선행 및 후행 공백 문자가 없는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-895">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-895">Examples</span></span>

<span data-ttu-id="c5cc5-896">다음은 매개 변수에서 공백 문자를 자르는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-896">The following example trims the white-space characters from the parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-897">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-898">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-898">Name</span></span> | <span data-ttu-id="c5cc5-899">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-899">Type</span></span> | <span data-ttu-id="c5cc5-900">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-901">return</span><span class="sxs-lookup"><span data-stu-id="c5cc5-901">return</span></span> | <span data-ttu-id="c5cc5-902">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-902">String</span></span> | <span data-ttu-id="c5cc5-903">one two three</span><span class="sxs-lookup"><span data-stu-id="c5cc5-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="c5cc5-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="c5cc5-905">매개 변수로 제공된 값을 기반으로 결정 해시 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="c5cc5-906">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-906">Parameters</span></span>

| <span data-ttu-id="c5cc5-907">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-907">Parameter</span></span> | <span data-ttu-id="c5cc5-908">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-908">Required</span></span> | <span data-ttu-id="c5cc5-909">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-909">Type</span></span> | <span data-ttu-id="c5cc5-910">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-911">baseString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-911">baseString</span></span> |<span data-ttu-id="c5cc5-912">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-912">Yes</span></span> |<span data-ttu-id="c5cc5-913">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-913">string</span></span> |<span data-ttu-id="c5cc5-914">고유한 문자열을 만들기 위해 해시 함수에서 사용되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="c5cc5-915">필요에 따라 추가하는 매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-915">additional parameters as needed</span></span> |<span data-ttu-id="c5cc5-916">아니요</span><span class="sxs-lookup"><span data-stu-id="c5cc5-916">No</span></span> |<span data-ttu-id="c5cc5-917">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-917">string</span></span> |<span data-ttu-id="c5cc5-918">고유성 수준을 지정하는 값을 만들기 위해 필요한 만큼 문자열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="c5cc5-919">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-919">Remarks</span></span>

<span data-ttu-id="c5cc5-920">이 함수는 리소스의 고유한 이름을 만들어야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="c5cc5-921">결과의 고유성 범위를 제한하는 매개 변수 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="c5cc5-922">구독, 리소스 그룹 또는 배포까지 해당 이름이 고유한지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="c5cc5-923">반환된 값은 임의 문자열이 아닌 해시 함수의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="c5cc5-924">반환된 값은 13자입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="c5cc5-925">전역적으로 고유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-925">It is not globally unique.</span></span> <span data-ttu-id="c5cc5-926">의미있는 이름을 만들기 위해 해당 값과 명명 규칙의 접두사를 결합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="c5cc5-927">다음 예제에서는 반환된 값의 형식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="c5cc5-928">실제 값은 제공된 매개 변수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="c5cc5-929">다음 예제에서는 uniqueString를 사용하여 일반적으로 사용하는 수준에 대해 고유한 값을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="c5cc5-930">구독에 범위가 지정된 고유함</span><span class="sxs-lookup"><span data-stu-id="c5cc5-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="c5cc5-931">리소스 그룹에 범위가 지정된 고유함</span><span class="sxs-lookup"><span data-stu-id="c5cc5-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="c5cc5-932">리소스 그룹의 배포에 범위가 지정된 고유함</span><span class="sxs-lookup"><span data-stu-id="c5cc5-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="c5cc5-933">다음 예제에서는 리소스 그룹에 따라 저장소 계정에 고유한 이름을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="c5cc5-934">리소스 그룹의 내부에서 같은 방식으로 생성된 경우 이름은 고유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="c5cc5-935">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-935">Return value</span></span>

<span data-ttu-id="c5cc5-936">13개의 문자를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-937">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-937">Examples</span></span>

<span data-ttu-id="c5cc5-938">다음 예제에서는 uniquestring에서 결과 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-938">The following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="c5cc5-939">uri</span><span class="sxs-lookup"><span data-stu-id="c5cc5-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="c5cc5-940">baseUri와 relativeUri 문자열을 결합하여 절대 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-941">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-941">Parameters</span></span>

| <span data-ttu-id="c5cc5-942">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-942">Parameter</span></span> | <span data-ttu-id="c5cc5-943">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-943">Required</span></span> | <span data-ttu-id="c5cc5-944">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-944">Type</span></span> | <span data-ttu-id="c5cc5-945">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="c5cc5-946">baseUri</span></span> |<span data-ttu-id="c5cc5-947">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-947">Yes</span></span> |<span data-ttu-id="c5cc5-948">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-948">string</span></span> |<span data-ttu-id="c5cc5-949">기본 uri 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-949">The base uri string.</span></span> |
| <span data-ttu-id="c5cc5-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="c5cc5-950">relativeUri</span></span> |<span data-ttu-id="c5cc5-951">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-951">Yes</span></span> |<span data-ttu-id="c5cc5-952">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-952">string</span></span> |<span data-ttu-id="c5cc5-953">기본 uri 문자열에 추가할 상대 uri 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="c5cc5-954">**baseUri** 매개 변수에 대한 값은 특정 파일을 포함할 수 있지만 URI를 생성하는 경우 기본 경로만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="c5cc5-955">예를 들어 `http://contoso.com/resources/azuredeploy.json`을 baseUri 매개 변수로 전달하면 기본 URI는 `http://contoso.com/resources/`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="c5cc5-956">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-956">Return value</span></span>

<span data-ttu-id="c5cc5-957">기본 및 상대 값에 대한 절대 URI를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-958">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-958">Examples</span></span>

<span data-ttu-id="c5cc5-959">다음 예제에서는 부모 템플릿의 값을 기반으로 중첩된 템플릿에 대한 링크를 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="c5cc5-960">다음 예제에서는 uri, uriComponent 및 uriComponentToString를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-961">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-962">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-962">Name</span></span> | <span data-ttu-id="c5cc5-963">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-963">Type</span></span> | <span data-ttu-id="c5cc5-964">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-965">uriOutput</span></span> | <span data-ttu-id="c5cc5-966">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-966">String</span></span> | <span data-ttu-id="c5cc5-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="c5cc5-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-968">componentOutput</span></span> | <span data-ttu-id="c5cc5-969">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-969">String</span></span> | <span data-ttu-id="c5cc5-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="c5cc5-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-971">toStringOutput</span></span> | <span data-ttu-id="c5cc5-972">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-972">String</span></span> | <span data-ttu-id="c5cc5-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="c5cc5-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="c5cc5-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="c5cc5-975">URI를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-976">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-976">Parameters</span></span>

| <span data-ttu-id="c5cc5-977">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-977">Parameter</span></span> | <span data-ttu-id="c5cc5-978">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-978">Required</span></span> | <span data-ttu-id="c5cc5-979">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-979">Type</span></span> | <span data-ttu-id="c5cc5-980">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="c5cc5-981">stringToEncode</span></span> |<span data-ttu-id="c5cc5-982">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-982">Yes</span></span> |<span data-ttu-id="c5cc5-983">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-983">string</span></span> |<span data-ttu-id="c5cc5-984">인코딩할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-985">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-985">Return value</span></span>

<span data-ttu-id="c5cc5-986">URI로 인코딩된 값의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-987">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-987">Examples</span></span>

<span data-ttu-id="c5cc5-988">다음 예제에서는 uri, uriComponent 및 uriComponentToString를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-989">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-990">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-990">Name</span></span> | <span data-ttu-id="c5cc5-991">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-991">Type</span></span> | <span data-ttu-id="c5cc5-992">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-993">uriOutput</span></span> | <span data-ttu-id="c5cc5-994">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-994">String</span></span> | <span data-ttu-id="c5cc5-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="c5cc5-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-996">componentOutput</span></span> | <span data-ttu-id="c5cc5-997">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-997">String</span></span> | <span data-ttu-id="c5cc5-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="c5cc5-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-999">toStringOutput</span></span> | <span data-ttu-id="c5cc5-1000">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1000">String</span></span> | <span data-ttu-id="c5cc5-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="c5cc5-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="c5cc5-1003">URI로 인코딩된 값의 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="c5cc5-1004">매개 변수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1004">Parameters</span></span>

| <span data-ttu-id="c5cc5-1005">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1005">Parameter</span></span> | <span data-ttu-id="c5cc5-1006">필수</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1006">Required</span></span> | <span data-ttu-id="c5cc5-1007">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1007">Type</span></span> | <span data-ttu-id="c5cc5-1008">설명</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5cc5-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1009">uriEncodedString</span></span> |<span data-ttu-id="c5cc5-1010">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1010">Yes</span></span> |<span data-ttu-id="c5cc5-1011">string</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1011">string</span></span> |<span data-ttu-id="c5cc5-1012">문자열로 변환할 URI 인코딩 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="c5cc5-1013">반환 값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1013">Return value</span></span>

<span data-ttu-id="c5cc5-1014">URI로 인코딩된 값의 디코딩된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="c5cc5-1015">예</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1015">Examples</span></span>

<span data-ttu-id="c5cc5-1016">다음 예제에서는 uri, uriComponent 및 uriComponentToString를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="c5cc5-1017">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="c5cc5-1018">이름</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1018">Name</span></span> | <span data-ttu-id="c5cc5-1019">형식</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1019">Type</span></span> | <span data-ttu-id="c5cc5-1020">값</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="c5cc5-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1021">uriOutput</span></span> | <span data-ttu-id="c5cc5-1022">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1022">String</span></span> | <span data-ttu-id="c5cc5-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="c5cc5-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1024">componentOutput</span></span> | <span data-ttu-id="c5cc5-1025">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1025">String</span></span> | <span data-ttu-id="c5cc5-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="c5cc5-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1027">toStringOutput</span></span> | <span data-ttu-id="c5cc5-1028">문자열</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1028">String</span></span> | <span data-ttu-id="c5cc5-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c5cc5-1030">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1030">Next steps</span></span>
* <span data-ttu-id="c5cc5-1031">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c5cc5-1032">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c5cc5-1033">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="c5cc5-1034">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5cc5-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

