---
title: "리소스 관리자 템플릿 함수 aaaAzure-문자열 | Microsoft Docs"
description: "Hello 함수 toouse 문자열이 포함 된 Azure 리소스 관리자 템플릿 toowork 프로그램에 대해 설명합니다."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="cff89-103">Azure Resource Manager 템플릿용 문자열 함수</span><span class="sxs-lookup"><span data-stu-id="cff89-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="cff89-104">리소스 관리자는 다음 문자열 작업에 대 한 함수 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="cff89-105">base64</span><span class="sxs-lookup"><span data-stu-id="cff89-105">base64</span></span>](#base64)
* [<span data-ttu-id="cff89-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="cff89-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="cff89-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="cff89-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="cff89-108">concat</span><span class="sxs-lookup"><span data-stu-id="cff89-108">concat</span></span>](#concat)
* [<span data-ttu-id="cff89-109">contains</span><span class="sxs-lookup"><span data-stu-id="cff89-109">contains</span></span>](#contains)
* [<span data-ttu-id="cff89-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="cff89-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="cff89-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="cff89-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="cff89-112">empty</span><span class="sxs-lookup"><span data-stu-id="cff89-112">empty</span></span>](#empty)
* [<span data-ttu-id="cff89-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="cff89-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="cff89-114">first</span><span class="sxs-lookup"><span data-stu-id="cff89-114">first</span></span>](#first)
* [<span data-ttu-id="cff89-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="cff89-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="cff89-116">last</span><span class="sxs-lookup"><span data-stu-id="cff89-116">last</span></span>](#last)
* [<span data-ttu-id="cff89-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="cff89-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="cff89-118">length</span><span class="sxs-lookup"><span data-stu-id="cff89-118">length</span></span>](#length)
* [<span data-ttu-id="cff89-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="cff89-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="cff89-120">replace</span><span class="sxs-lookup"><span data-stu-id="cff89-120">replace</span></span>](#replace)
* [<span data-ttu-id="cff89-121">skip</span><span class="sxs-lookup"><span data-stu-id="cff89-121">skip</span></span>](#skip)
* [<span data-ttu-id="cff89-122">분할</span><span class="sxs-lookup"><span data-stu-id="cff89-122">split</span></span>](#split)
* [<span data-ttu-id="cff89-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="cff89-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="cff89-124">string</span><span class="sxs-lookup"><span data-stu-id="cff89-124">string</span></span>](#string)
* [<span data-ttu-id="cff89-125">substring</span><span class="sxs-lookup"><span data-stu-id="cff89-125">substring</span></span>](#substring)
* [<span data-ttu-id="cff89-126">take</span><span class="sxs-lookup"><span data-stu-id="cff89-126">take</span></span>](#take)
* [<span data-ttu-id="cff89-127">toLower</span><span class="sxs-lookup"><span data-stu-id="cff89-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="cff89-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="cff89-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="cff89-129">trim</span><span class="sxs-lookup"><span data-stu-id="cff89-129">trim</span></span>](#trim)
* [<span data-ttu-id="cff89-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="cff89-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="cff89-131">uri</span><span class="sxs-lookup"><span data-stu-id="cff89-131">uri</span></span>](#uri)
* [<span data-ttu-id="cff89-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="cff89-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="cff89-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="cff89-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="cff89-134">base64</span><span class="sxs-lookup"><span data-stu-id="cff89-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="cff89-135">반환 hello hello 입력된 문자열의 base64 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-136">Parameters</span></span>

| <span data-ttu-id="cff89-137">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-137">Parameter</span></span> | <span data-ttu-id="cff89-138">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-138">Required</span></span> | <span data-ttu-id="cff89-139">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-139">Type</span></span> | <span data-ttu-id="cff89-140">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-141">inputString</span><span class="sxs-lookup"><span data-stu-id="cff89-141">inputString</span></span> |<span data-ttu-id="cff89-142">예</span><span class="sxs-lookup"><span data-stu-id="cff89-142">Yes</span></span> |<span data-ttu-id="cff89-143">string</span><span class="sxs-lookup"><span data-stu-id="cff89-143">string</span></span> |<span data-ttu-id="cff89-144">base64 표현으로 hello 값 tooreturn 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-145">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-145">Return value</span></span>

<span data-ttu-id="cff89-146">Hello base64 표현을 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-147">예</span><span class="sxs-lookup"><span data-stu-id="cff89-147">Examples</span></span>

<span data-ttu-id="cff89-148">다음 예제는 hello toouse base64 함수 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="cff89-149">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-150">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-150">Name</span></span> | <span data-ttu-id="cff89-151">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-151">Type</span></span> | <span data-ttu-id="cff89-152">값</span><span class="sxs-lookup"><span data-stu-id="cff89-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="cff89-153">base64Output</span></span> | <span data-ttu-id="cff89-154">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-154">String</span></span> | <span data-ttu-id="cff89-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="cff89-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="cff89-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-156">toStringOutput</span></span> | <span data-ttu-id="cff89-157">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-157">String</span></span> | <span data-ttu-id="cff89-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="cff89-158">one, two, three</span></span> |
| <span data-ttu-id="cff89-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-159">toJsonOutput</span></span> | <span data-ttu-id="cff89-160">Object</span><span class="sxs-lookup"><span data-stu-id="cff89-160">Object</span></span> | <span data-ttu-id="cff89-161">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="cff89-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="cff89-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="cff89-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="cff89-163">Base64 표현을 tooa JSON 개체로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-164">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-164">Parameters</span></span>

| <span data-ttu-id="cff89-165">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-165">Parameter</span></span> | <span data-ttu-id="cff89-166">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-166">Required</span></span> | <span data-ttu-id="cff89-167">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-167">Type</span></span> | <span data-ttu-id="cff89-168">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="cff89-169">base64Value</span></span> |<span data-ttu-id="cff89-170">예</span><span class="sxs-lookup"><span data-stu-id="cff89-170">Yes</span></span> |<span data-ttu-id="cff89-171">string</span><span class="sxs-lookup"><span data-stu-id="cff89-171">string</span></span> |<span data-ttu-id="cff89-172">hello base64 표현 tooconvert tooa JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-173">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-173">Return value</span></span>

<span data-ttu-id="cff89-174">JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-175">예</span><span class="sxs-lookup"><span data-stu-id="cff89-175">Examples</span></span>

<span data-ttu-id="cff89-176">hello 다음 예제에서는 hello base64ToJson 함수 tooconvert base64 값:</span><span class="sxs-lookup"><span data-stu-id="cff89-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="cff89-177">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-178">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-178">Name</span></span> | <span data-ttu-id="cff89-179">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-179">Type</span></span> | <span data-ttu-id="cff89-180">값</span><span class="sxs-lookup"><span data-stu-id="cff89-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="cff89-181">base64Output</span></span> | <span data-ttu-id="cff89-182">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-182">String</span></span> | <span data-ttu-id="cff89-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="cff89-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="cff89-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-184">toStringOutput</span></span> | <span data-ttu-id="cff89-185">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-185">String</span></span> | <span data-ttu-id="cff89-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="cff89-186">one, two, three</span></span> |
| <span data-ttu-id="cff89-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-187">toJsonOutput</span></span> | <span data-ttu-id="cff89-188">Object</span><span class="sxs-lookup"><span data-stu-id="cff89-188">Object</span></span> | <span data-ttu-id="cff89-189">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="cff89-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="cff89-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="cff89-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="cff89-191">Base64 표현을 tooa 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-192">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-192">Parameters</span></span>

| <span data-ttu-id="cff89-193">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-193">Parameter</span></span> | <span data-ttu-id="cff89-194">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-194">Required</span></span> | <span data-ttu-id="cff89-195">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-195">Type</span></span> | <span data-ttu-id="cff89-196">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="cff89-197">base64Value</span></span> |<span data-ttu-id="cff89-198">예</span><span class="sxs-lookup"><span data-stu-id="cff89-198">Yes</span></span> |<span data-ttu-id="cff89-199">string</span><span class="sxs-lookup"><span data-stu-id="cff89-199">string</span></span> |<span data-ttu-id="cff89-200">hello base64 표현 tooconvert tooa 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-201">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-201">Return value</span></span>

<span data-ttu-id="cff89-202">Base64 값을 변환 하는 hello의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-203">예</span><span class="sxs-lookup"><span data-stu-id="cff89-203">Examples</span></span>

<span data-ttu-id="cff89-204">hello 다음 예제에서는 hello base64ToString 함수 tooconvert base64 값:</span><span class="sxs-lookup"><span data-stu-id="cff89-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="cff89-205">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-206">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-206">Name</span></span> | <span data-ttu-id="cff89-207">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-207">Type</span></span> | <span data-ttu-id="cff89-208">값</span><span class="sxs-lookup"><span data-stu-id="cff89-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="cff89-209">base64Output</span></span> | <span data-ttu-id="cff89-210">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-210">String</span></span> | <span data-ttu-id="cff89-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="cff89-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="cff89-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-212">toStringOutput</span></span> | <span data-ttu-id="cff89-213">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-213">String</span></span> | <span data-ttu-id="cff89-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="cff89-214">one, two, three</span></span> |
| <span data-ttu-id="cff89-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-215">toJsonOutput</span></span> | <span data-ttu-id="cff89-216">Object</span><span class="sxs-lookup"><span data-stu-id="cff89-216">Object</span></span> | <span data-ttu-id="cff89-217">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="cff89-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="cff89-218">concat</span><span class="sxs-lookup"><span data-stu-id="cff89-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="cff89-219">여러 개의 문자열 값을 결합 하 고 hello 연결 문자열을 반환 하 또는 여러 배열을 결합 하 고 연결 하는 hello 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-220">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-220">Parameters</span></span>

| <span data-ttu-id="cff89-221">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-221">Parameter</span></span> | <span data-ttu-id="cff89-222">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-222">Required</span></span> | <span data-ttu-id="cff89-223">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-223">Type</span></span> | <span data-ttu-id="cff89-224">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-225">arg1</span><span class="sxs-lookup"><span data-stu-id="cff89-225">arg1</span></span> |<span data-ttu-id="cff89-226">예</span><span class="sxs-lookup"><span data-stu-id="cff89-226">Yes</span></span> |<span data-ttu-id="cff89-227">문자열 또는 배열</span><span class="sxs-lookup"><span data-stu-id="cff89-227">string or array</span></span> |<span data-ttu-id="cff89-228">hello 연결에 대 한 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="cff89-229">추가 인수</span><span class="sxs-lookup"><span data-stu-id="cff89-229">additional arguments</span></span> |<span data-ttu-id="cff89-230">아니요</span><span class="sxs-lookup"><span data-stu-id="cff89-230">No</span></span> |<span data-ttu-id="cff89-231">string</span><span class="sxs-lookup"><span data-stu-id="cff89-231">string</span></span> |<span data-ttu-id="cff89-232">연결할 추가 값(순서대로)입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-233">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-233">Return value</span></span>
<span data-ttu-id="cff89-234">연결된 값의 문자열 또는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-235">예</span><span class="sxs-lookup"><span data-stu-id="cff89-235">Examples</span></span>

<span data-ttu-id="cff89-236">다음 예제는 hello toocombine 두 문자열 값 하 고 연결 된 문자열을 반환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="cff89-237">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-238">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-238">Name</span></span> | <span data-ttu-id="cff89-239">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-239">Type</span></span> | <span data-ttu-id="cff89-240">값</span><span class="sxs-lookup"><span data-stu-id="cff89-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-241">concatOutput</span></span> | <span data-ttu-id="cff89-242">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-242">String</span></span> | <span data-ttu-id="cff89-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="cff89-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="cff89-244">다음 예제는 hello toocombine 두 배열 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="cff89-245">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-246">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-246">Name</span></span> | <span data-ttu-id="cff89-247">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-247">Type</span></span> | <span data-ttu-id="cff89-248">값</span><span class="sxs-lookup"><span data-stu-id="cff89-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-249">return</span><span class="sxs-lookup"><span data-stu-id="cff89-249">return</span></span> | <span data-ttu-id="cff89-250">배열</span><span class="sxs-lookup"><span data-stu-id="cff89-250">Array</span></span> | <span data-ttu-id="cff89-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="cff89-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="cff89-252">contains</span><span class="sxs-lookup"><span data-stu-id="cff89-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="cff89-253">배열에 값이 포함되는지, 개체에 키가 포함되는지 또는 문자열에 하위 문자열이 포함되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-254">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-254">Parameters</span></span>

| <span data-ttu-id="cff89-255">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-255">Parameter</span></span> | <span data-ttu-id="cff89-256">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-256">Required</span></span> | <span data-ttu-id="cff89-257">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-257">Type</span></span> | <span data-ttu-id="cff89-258">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-259">container</span><span class="sxs-lookup"><span data-stu-id="cff89-259">container</span></span> |<span data-ttu-id="cff89-260">예</span><span class="sxs-lookup"><span data-stu-id="cff89-260">Yes</span></span> |<span data-ttu-id="cff89-261">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-261">array, object, or string</span></span> |<span data-ttu-id="cff89-262">hello 값 toofind를 포함 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="cff89-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="cff89-263">itemToFind</span></span> |<span data-ttu-id="cff89-264">예</span><span class="sxs-lookup"><span data-stu-id="cff89-264">Yes</span></span> |<span data-ttu-id="cff89-265">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="cff89-265">string or int</span></span> |<span data-ttu-id="cff89-266">hello 값 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-267">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-267">Return value</span></span>

<span data-ttu-id="cff89-268">**True 이면** hello 항목이 검색 되지 않으면 이면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-269">예</span><span class="sxs-lookup"><span data-stu-id="cff89-269">Examples</span></span>

<span data-ttu-id="cff89-270">hello 다음 예제는 toouse 여러 형식으로 포함 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="cff89-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="cff89-271">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-272">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-272">Name</span></span> | <span data-ttu-id="cff89-273">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-273">Type</span></span> | <span data-ttu-id="cff89-274">값</span><span class="sxs-lookup"><span data-stu-id="cff89-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-275">stringTrue</span></span> | <span data-ttu-id="cff89-276">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-276">Bool</span></span> | <span data-ttu-id="cff89-277">True</span><span class="sxs-lookup"><span data-stu-id="cff89-277">True</span></span> |
| <span data-ttu-id="cff89-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-278">stringFalse</span></span> | <span data-ttu-id="cff89-279">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-279">Bool</span></span> | <span data-ttu-id="cff89-280">False</span><span class="sxs-lookup"><span data-stu-id="cff89-280">False</span></span> |
| <span data-ttu-id="cff89-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-281">objectTrue</span></span> | <span data-ttu-id="cff89-282">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-282">Bool</span></span> | <span data-ttu-id="cff89-283">True</span><span class="sxs-lookup"><span data-stu-id="cff89-283">True</span></span> |
| <span data-ttu-id="cff89-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-284">objectFalse</span></span> | <span data-ttu-id="cff89-285">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-285">Bool</span></span> | <span data-ttu-id="cff89-286">False</span><span class="sxs-lookup"><span data-stu-id="cff89-286">False</span></span> |
| <span data-ttu-id="cff89-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-287">arrayTrue</span></span> | <span data-ttu-id="cff89-288">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-288">Bool</span></span> | <span data-ttu-id="cff89-289">True</span><span class="sxs-lookup"><span data-stu-id="cff89-289">True</span></span> |
| <span data-ttu-id="cff89-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-290">arrayFalse</span></span> | <span data-ttu-id="cff89-291">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-291">Bool</span></span> | <span data-ttu-id="cff89-292">False</span><span class="sxs-lookup"><span data-stu-id="cff89-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="cff89-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="cff89-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="cff89-294">값 tooa 데이터 URI를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-295">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-295">Parameters</span></span>

| <span data-ttu-id="cff89-296">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-296">Parameter</span></span> | <span data-ttu-id="cff89-297">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-297">Required</span></span> | <span data-ttu-id="cff89-298">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-298">Type</span></span> | <span data-ttu-id="cff89-299">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="cff89-300">stringToConvert</span></span> |<span data-ttu-id="cff89-301">예</span><span class="sxs-lookup"><span data-stu-id="cff89-301">Yes</span></span> |<span data-ttu-id="cff89-302">string</span><span class="sxs-lookup"><span data-stu-id="cff89-302">string</span></span> |<span data-ttu-id="cff89-303">hello 값 tooconvert tooa 데이터 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-304">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-304">Return value</span></span>

<span data-ttu-id="cff89-305">데이터 URI로 형식이 지정된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-306">예</span><span class="sxs-lookup"><span data-stu-id="cff89-306">Examples</span></span>

<span data-ttu-id="cff89-307">다음 예제는 hello 값 tooa 데이터 URI를 변환 하는 데이터 URI tooa 문자열:</span><span class="sxs-lookup"><span data-stu-id="cff89-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="cff89-308">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-309">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-309">Name</span></span> | <span data-ttu-id="cff89-310">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-310">Type</span></span> | <span data-ttu-id="cff89-311">값</span><span class="sxs-lookup"><span data-stu-id="cff89-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-312">dataUriOutput</span></span> | <span data-ttu-id="cff89-313">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-313">String</span></span> | <span data-ttu-id="cff89-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="cff89-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="cff89-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-315">toStringOutput</span></span> | <span data-ttu-id="cff89-316">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-316">String</span></span> | <span data-ttu-id="cff89-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="cff89-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="cff89-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="cff89-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="cff89-319">데이터 URI는 형식의 값 tooa 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-320">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-320">Parameters</span></span>

| <span data-ttu-id="cff89-321">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-321">Parameter</span></span> | <span data-ttu-id="cff89-322">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-322">Required</span></span> | <span data-ttu-id="cff89-323">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-323">Type</span></span> | <span data-ttu-id="cff89-324">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="cff89-325">dataUriToConvert</span></span> |<span data-ttu-id="cff89-326">예</span><span class="sxs-lookup"><span data-stu-id="cff89-326">Yes</span></span> |<span data-ttu-id="cff89-327">string</span><span class="sxs-lookup"><span data-stu-id="cff89-327">string</span></span> |<span data-ttu-id="cff89-328">hello 데이터 URI 값 tooconvert입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-329">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-329">Return value</span></span>

<span data-ttu-id="cff89-330">Hello를 포함 하는 문자열 값을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-331">예</span><span class="sxs-lookup"><span data-stu-id="cff89-331">Examples</span></span>

<span data-ttu-id="cff89-332">다음 예제는 hello 값 tooa 데이터 URI를 변환 하는 데이터 URI tooa 문자열:</span><span class="sxs-lookup"><span data-stu-id="cff89-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="cff89-333">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-334">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-334">Name</span></span> | <span data-ttu-id="cff89-335">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-335">Type</span></span> | <span data-ttu-id="cff89-336">값</span><span class="sxs-lookup"><span data-stu-id="cff89-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-337">dataUriOutput</span></span> | <span data-ttu-id="cff89-338">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-338">String</span></span> | <span data-ttu-id="cff89-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="cff89-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="cff89-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-340">toStringOutput</span></span> | <span data-ttu-id="cff89-341">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-341">String</span></span> | <span data-ttu-id="cff89-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="cff89-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="cff89-343">empty</span><span class="sxs-lookup"><span data-stu-id="cff89-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="cff89-344">배열, 개체 또는 문자열이 비어 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-345">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-345">Parameters</span></span>

| <span data-ttu-id="cff89-346">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-346">Parameter</span></span> | <span data-ttu-id="cff89-347">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-347">Required</span></span> | <span data-ttu-id="cff89-348">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-348">Type</span></span> | <span data-ttu-id="cff89-349">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="cff89-350">itemToTest</span></span> |<span data-ttu-id="cff89-351">예</span><span class="sxs-lookup"><span data-stu-id="cff89-351">Yes</span></span> |<span data-ttu-id="cff89-352">배열, 개체 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-352">array, object, or string</span></span> |<span data-ttu-id="cff89-353">비어 있는 경우 값 toocheck을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-354">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-354">Return value</span></span>

<span data-ttu-id="cff89-355">반환 **True** hello 값, 비어 있지 않으면이 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-356">예</span><span class="sxs-lookup"><span data-stu-id="cff89-356">Examples</span></span>

<span data-ttu-id="cff89-357">다음 예제는 hello는 배열, 개체 및 문자열 비어 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="cff89-358">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-359">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-359">Name</span></span> | <span data-ttu-id="cff89-360">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-360">Type</span></span> | <span data-ttu-id="cff89-361">값</span><span class="sxs-lookup"><span data-stu-id="cff89-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="cff89-362">arrayEmpty</span></span> | <span data-ttu-id="cff89-363">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-363">Bool</span></span> | <span data-ttu-id="cff89-364">True</span><span class="sxs-lookup"><span data-stu-id="cff89-364">True</span></span> |
| <span data-ttu-id="cff89-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="cff89-365">objectEmpty</span></span> | <span data-ttu-id="cff89-366">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-366">Bool</span></span> | <span data-ttu-id="cff89-367">True</span><span class="sxs-lookup"><span data-stu-id="cff89-367">True</span></span> |
| <span data-ttu-id="cff89-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="cff89-368">stringEmpty</span></span> | <span data-ttu-id="cff89-369">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-369">Bool</span></span> | <span data-ttu-id="cff89-370">True</span><span class="sxs-lookup"><span data-stu-id="cff89-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="cff89-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="cff89-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="cff89-372">문자열이 값으로 끝나는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="cff89-373">hello 비교는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-374">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-374">Parameters</span></span>

| <span data-ttu-id="cff89-375">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-375">Parameter</span></span> | <span data-ttu-id="cff89-376">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-376">Required</span></span> | <span data-ttu-id="cff89-377">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-377">Type</span></span> | <span data-ttu-id="cff89-378">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="cff89-379">stringToSearch</span></span> |<span data-ttu-id="cff89-380">예</span><span class="sxs-lookup"><span data-stu-id="cff89-380">Yes</span></span> |<span data-ttu-id="cff89-381">string</span><span class="sxs-lookup"><span data-stu-id="cff89-381">string</span></span> |<span data-ttu-id="cff89-382">hello 항목 toofind를 포함 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="cff89-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="cff89-383">stringToFind</span></span> |<span data-ttu-id="cff89-384">예</span><span class="sxs-lookup"><span data-stu-id="cff89-384">Yes</span></span> |<span data-ttu-id="cff89-385">string</span><span class="sxs-lookup"><span data-stu-id="cff89-385">string</span></span> |<span data-ttu-id="cff89-386">hello 값 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-387">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-387">Return value</span></span>

<span data-ttu-id="cff89-388">**True** hello 기본 동작은 일치 하는 hello 마지막 문자 또는 문자 hello 문자열의 경우 이렇게 하지 않으면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-389">예</span><span class="sxs-lookup"><span data-stu-id="cff89-389">Examples</span></span>

<span data-ttu-id="cff89-390">다음 예제는 hello toouse startsWith 및 endsWith 함수 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="cff89-391">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-392">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-392">Name</span></span> | <span data-ttu-id="cff89-393">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-393">Type</span></span> | <span data-ttu-id="cff89-394">값</span><span class="sxs-lookup"><span data-stu-id="cff89-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-395">startsTrue</span></span> | <span data-ttu-id="cff89-396">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-396">Bool</span></span> | <span data-ttu-id="cff89-397">True</span><span class="sxs-lookup"><span data-stu-id="cff89-397">True</span></span> |
| <span data-ttu-id="cff89-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-398">startsCapTrue</span></span> | <span data-ttu-id="cff89-399">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-399">Bool</span></span> | <span data-ttu-id="cff89-400">True</span><span class="sxs-lookup"><span data-stu-id="cff89-400">True</span></span> |
| <span data-ttu-id="cff89-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-401">startsFalse</span></span> | <span data-ttu-id="cff89-402">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-402">Bool</span></span> | <span data-ttu-id="cff89-403">False</span><span class="sxs-lookup"><span data-stu-id="cff89-403">False</span></span> |
| <span data-ttu-id="cff89-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-404">endsTrue</span></span> | <span data-ttu-id="cff89-405">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-405">Bool</span></span> | <span data-ttu-id="cff89-406">True</span><span class="sxs-lookup"><span data-stu-id="cff89-406">True</span></span> |
| <span data-ttu-id="cff89-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-407">endsCapTrue</span></span> | <span data-ttu-id="cff89-408">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-408">Bool</span></span> | <span data-ttu-id="cff89-409">True</span><span class="sxs-lookup"><span data-stu-id="cff89-409">True</span></span> |
| <span data-ttu-id="cff89-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-410">endsFalse</span></span> | <span data-ttu-id="cff89-411">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-411">Bool</span></span> | <span data-ttu-id="cff89-412">False</span><span class="sxs-lookup"><span data-stu-id="cff89-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="cff89-413">first</span><span class="sxs-lookup"><span data-stu-id="cff89-413">first</span></span>
`first(arg1)`

<span data-ttu-id="cff89-414">반환은 hello 문자열의 첫 번째 문자 또는 hello 배열의 첫 번째 요소 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-415">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-415">Parameters</span></span>

| <span data-ttu-id="cff89-416">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-416">Parameter</span></span> | <span data-ttu-id="cff89-417">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-417">Required</span></span> | <span data-ttu-id="cff89-418">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-418">Type</span></span> | <span data-ttu-id="cff89-419">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-420">arg1</span><span class="sxs-lookup"><span data-stu-id="cff89-420">arg1</span></span> |<span data-ttu-id="cff89-421">예</span><span class="sxs-lookup"><span data-stu-id="cff89-421">Yes</span></span> |<span data-ttu-id="cff89-422">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-422">array or string</span></span> |<span data-ttu-id="cff89-423">문자 또는 hello 값 tooretrieve hello 첫 번째 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-424">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-424">Return value</span></span>

<span data-ttu-id="cff89-425">Hello 첫 번째 문자 또는 배열에 hello 첫 번째 요소의 hello 형식 (string, int, 배열 또는 개체)는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-426">예</span><span class="sxs-lookup"><span data-stu-id="cff89-426">Examples</span></span>

<span data-ttu-id="cff89-427">hello 다음 예제에서는 어떻게 toouse hello 배열 및 문자열을 사용 하는 첫 번째 함수</span><span class="sxs-lookup"><span data-stu-id="cff89-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="cff89-428">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-429">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-429">Name</span></span> | <span data-ttu-id="cff89-430">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-430">Type</span></span> | <span data-ttu-id="cff89-431">값</span><span class="sxs-lookup"><span data-stu-id="cff89-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-432">arrayOutput</span></span> | <span data-ttu-id="cff89-433">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-433">String</span></span> | <span data-ttu-id="cff89-434">one</span><span class="sxs-lookup"><span data-stu-id="cff89-434">one</span></span> |
| <span data-ttu-id="cff89-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-435">stringOutput</span></span> | <span data-ttu-id="cff89-436">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-436">String</span></span> | <span data-ttu-id="cff89-437">O</span><span class="sxs-lookup"><span data-stu-id="cff89-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="cff89-438">indexof</span><span class="sxs-lookup"><span data-stu-id="cff89-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="cff89-439">반환 hello 문자열 내 값의 첫 번째 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="cff89-440">hello 비교는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-441">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-441">Parameters</span></span>

| <span data-ttu-id="cff89-442">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-442">Parameter</span></span> | <span data-ttu-id="cff89-443">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-443">Required</span></span> | <span data-ttu-id="cff89-444">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-444">Type</span></span> | <span data-ttu-id="cff89-445">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="cff89-446">stringToSearch</span></span> |<span data-ttu-id="cff89-447">예</span><span class="sxs-lookup"><span data-stu-id="cff89-447">Yes</span></span> |<span data-ttu-id="cff89-448">string</span><span class="sxs-lookup"><span data-stu-id="cff89-448">string</span></span> |<span data-ttu-id="cff89-449">hello 항목 toofind를 포함 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="cff89-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="cff89-450">stringToFind</span></span> |<span data-ttu-id="cff89-451">예</span><span class="sxs-lookup"><span data-stu-id="cff89-451">Yes</span></span> |<span data-ttu-id="cff89-452">string</span><span class="sxs-lookup"><span data-stu-id="cff89-452">string</span></span> |<span data-ttu-id="cff89-453">hello 값 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-454">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-454">Return value</span></span>

<span data-ttu-id="cff89-455">Hello 항목 toofind의 hello 위치를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="cff89-456">hello 값은 0부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-456">hello value is zero-based.</span></span> <span data-ttu-id="cff89-457">Hello 항목이 발견 되지 않으면-1이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-458">예</span><span class="sxs-lookup"><span data-stu-id="cff89-458">Examples</span></span>

<span data-ttu-id="cff89-459">다음 예제는 hello toouse indexOf 및 lastIndexOf 함수 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="cff89-460">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-461">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-461">Name</span></span> | <span data-ttu-id="cff89-462">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-462">Type</span></span> | <span data-ttu-id="cff89-463">값</span><span class="sxs-lookup"><span data-stu-id="cff89-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-464">firstT</span><span class="sxs-lookup"><span data-stu-id="cff89-464">firstT</span></span> | <span data-ttu-id="cff89-465">int</span><span class="sxs-lookup"><span data-stu-id="cff89-465">Int</span></span> | <span data-ttu-id="cff89-466">0</span><span class="sxs-lookup"><span data-stu-id="cff89-466">0</span></span> |
| <span data-ttu-id="cff89-467">lastT</span><span class="sxs-lookup"><span data-stu-id="cff89-467">lastT</span></span> | <span data-ttu-id="cff89-468">int</span><span class="sxs-lookup"><span data-stu-id="cff89-468">Int</span></span> | <span data-ttu-id="cff89-469">3</span><span class="sxs-lookup"><span data-stu-id="cff89-469">3</span></span> |
| <span data-ttu-id="cff89-470">firstString</span><span class="sxs-lookup"><span data-stu-id="cff89-470">firstString</span></span> | <span data-ttu-id="cff89-471">int</span><span class="sxs-lookup"><span data-stu-id="cff89-471">Int</span></span> | <span data-ttu-id="cff89-472">2</span><span class="sxs-lookup"><span data-stu-id="cff89-472">2</span></span> |
| <span data-ttu-id="cff89-473">lastString</span><span class="sxs-lookup"><span data-stu-id="cff89-473">lastString</span></span> | <span data-ttu-id="cff89-474">int</span><span class="sxs-lookup"><span data-stu-id="cff89-474">Int</span></span> | <span data-ttu-id="cff89-475">0</span><span class="sxs-lookup"><span data-stu-id="cff89-475">0</span></span> |
| <span data-ttu-id="cff89-476">notFound</span><span class="sxs-lookup"><span data-stu-id="cff89-476">notFound</span></span> | <span data-ttu-id="cff89-477">int</span><span class="sxs-lookup"><span data-stu-id="cff89-477">Int</span></span> | <span data-ttu-id="cff89-478">-1</span><span class="sxs-lookup"><span data-stu-id="cff89-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="cff89-479">last</span><span class="sxs-lookup"><span data-stu-id="cff89-479">last</span></span>
`last (arg1)`

<span data-ttu-id="cff89-480">마지막 hello 문자열의 문자 또는 hello hello 배열의 마지막 요소를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-481">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-481">Parameters</span></span>

| <span data-ttu-id="cff89-482">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-482">Parameter</span></span> | <span data-ttu-id="cff89-483">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-483">Required</span></span> | <span data-ttu-id="cff89-484">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-484">Type</span></span> | <span data-ttu-id="cff89-485">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-486">arg1</span><span class="sxs-lookup"><span data-stu-id="cff89-486">arg1</span></span> |<span data-ttu-id="cff89-487">예</span><span class="sxs-lookup"><span data-stu-id="cff89-487">Yes</span></span> |<span data-ttu-id="cff89-488">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-488">array or string</span></span> |<span data-ttu-id="cff89-489">문자 또는 hello 값 tooretrieve hello 마지막 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-490">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-490">Return value</span></span>

<span data-ttu-id="cff89-491">문자열 hello 마지막 문자 또는 hello 유형의 (string, int, 배열 또는 개체) hello 배열에서 마지막 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-492">예</span><span class="sxs-lookup"><span data-stu-id="cff89-492">Examples</span></span>

<span data-ttu-id="cff89-493">hello 다음 예제에서는 어떻게 toouse hello 수 있는 배열 및 문자열 last 함수</span><span class="sxs-lookup"><span data-stu-id="cff89-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="cff89-494">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-495">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-495">Name</span></span> | <span data-ttu-id="cff89-496">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-496">Type</span></span> | <span data-ttu-id="cff89-497">값</span><span class="sxs-lookup"><span data-stu-id="cff89-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-498">arrayOutput</span></span> | <span data-ttu-id="cff89-499">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-499">String</span></span> | <span data-ttu-id="cff89-500">three</span><span class="sxs-lookup"><span data-stu-id="cff89-500">three</span></span> |
| <span data-ttu-id="cff89-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-501">stringOutput</span></span> | <span data-ttu-id="cff89-502">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-502">String</span></span> | <span data-ttu-id="cff89-503">e</span><span class="sxs-lookup"><span data-stu-id="cff89-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="cff89-504">lastindexof</span><span class="sxs-lookup"><span data-stu-id="cff89-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="cff89-505">반환 된 문자열 내에서 값의 마지막 위치를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="cff89-506">hello 비교는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-507">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-507">Parameters</span></span>

| <span data-ttu-id="cff89-508">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-508">Parameter</span></span> | <span data-ttu-id="cff89-509">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-509">Required</span></span> | <span data-ttu-id="cff89-510">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-510">Type</span></span> | <span data-ttu-id="cff89-511">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="cff89-512">stringToSearch</span></span> |<span data-ttu-id="cff89-513">예</span><span class="sxs-lookup"><span data-stu-id="cff89-513">Yes</span></span> |<span data-ttu-id="cff89-514">string</span><span class="sxs-lookup"><span data-stu-id="cff89-514">string</span></span> |<span data-ttu-id="cff89-515">hello 항목 toofind를 포함 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="cff89-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="cff89-516">stringToFind</span></span> |<span data-ttu-id="cff89-517">예</span><span class="sxs-lookup"><span data-stu-id="cff89-517">Yes</span></span> |<span data-ttu-id="cff89-518">string</span><span class="sxs-lookup"><span data-stu-id="cff89-518">string</span></span> |<span data-ttu-id="cff89-519">hello 값 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-520">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-520">Return value</span></span>

<span data-ttu-id="cff89-521">Hello hello 항목 toofind의 마지막 위치를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="cff89-522">hello 값은 0부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-522">hello value is zero-based.</span></span> <span data-ttu-id="cff89-523">Hello 항목이 발견 되지 않으면-1이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-524">예</span><span class="sxs-lookup"><span data-stu-id="cff89-524">Examples</span></span>

<span data-ttu-id="cff89-525">다음 예제는 hello toouse indexOf 및 lastIndexOf 함수 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="cff89-526">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-527">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-527">Name</span></span> | <span data-ttu-id="cff89-528">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-528">Type</span></span> | <span data-ttu-id="cff89-529">값</span><span class="sxs-lookup"><span data-stu-id="cff89-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-530">firstT</span><span class="sxs-lookup"><span data-stu-id="cff89-530">firstT</span></span> | <span data-ttu-id="cff89-531">int</span><span class="sxs-lookup"><span data-stu-id="cff89-531">Int</span></span> | <span data-ttu-id="cff89-532">0</span><span class="sxs-lookup"><span data-stu-id="cff89-532">0</span></span> |
| <span data-ttu-id="cff89-533">lastT</span><span class="sxs-lookup"><span data-stu-id="cff89-533">lastT</span></span> | <span data-ttu-id="cff89-534">int</span><span class="sxs-lookup"><span data-stu-id="cff89-534">Int</span></span> | <span data-ttu-id="cff89-535">3</span><span class="sxs-lookup"><span data-stu-id="cff89-535">3</span></span> |
| <span data-ttu-id="cff89-536">firstString</span><span class="sxs-lookup"><span data-stu-id="cff89-536">firstString</span></span> | <span data-ttu-id="cff89-537">int</span><span class="sxs-lookup"><span data-stu-id="cff89-537">Int</span></span> | <span data-ttu-id="cff89-538">2</span><span class="sxs-lookup"><span data-stu-id="cff89-538">2</span></span> |
| <span data-ttu-id="cff89-539">lastString</span><span class="sxs-lookup"><span data-stu-id="cff89-539">lastString</span></span> | <span data-ttu-id="cff89-540">int</span><span class="sxs-lookup"><span data-stu-id="cff89-540">Int</span></span> | <span data-ttu-id="cff89-541">0</span><span class="sxs-lookup"><span data-stu-id="cff89-541">0</span></span> |
| <span data-ttu-id="cff89-542">notFound</span><span class="sxs-lookup"><span data-stu-id="cff89-542">notFound</span></span> | <span data-ttu-id="cff89-543">int</span><span class="sxs-lookup"><span data-stu-id="cff89-543">Int</span></span> | <span data-ttu-id="cff89-544">-1</span><span class="sxs-lookup"><span data-stu-id="cff89-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="cff89-545">length</span><span class="sxs-lookup"><span data-stu-id="cff89-545">length</span></span>
`length(string)`

<span data-ttu-id="cff89-546">문자열 또는 배열 요소에 hello 문자 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-547">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-547">Parameters</span></span>

| <span data-ttu-id="cff89-548">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-548">Parameter</span></span> | <span data-ttu-id="cff89-549">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-549">Required</span></span> | <span data-ttu-id="cff89-550">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-550">Type</span></span> | <span data-ttu-id="cff89-551">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-552">arg1</span><span class="sxs-lookup"><span data-stu-id="cff89-552">arg1</span></span> |<span data-ttu-id="cff89-553">예</span><span class="sxs-lookup"><span data-stu-id="cff89-553">Yes</span></span> |<span data-ttu-id="cff89-554">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-554">array or string</span></span> |<span data-ttu-id="cff89-555">hello 수의 요소를 가져오기 위한 배열 toouse hello 또는 hello 개수의 문자를 가져오기 위한 문자열 toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-556">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-556">Return value</span></span>

<span data-ttu-id="cff89-557">int입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="cff89-558">예</span><span class="sxs-lookup"><span data-stu-id="cff89-558">Examples</span></span>

<span data-ttu-id="cff89-559">hello 방법을 예제와 다음 toouse 배열 및 문자열 길이:</span><span class="sxs-lookup"><span data-stu-id="cff89-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="cff89-560">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-561">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-561">Name</span></span> | <span data-ttu-id="cff89-562">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-562">Type</span></span> | <span data-ttu-id="cff89-563">값</span><span class="sxs-lookup"><span data-stu-id="cff89-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="cff89-564">arrayLength</span></span> | <span data-ttu-id="cff89-565">int</span><span class="sxs-lookup"><span data-stu-id="cff89-565">Int</span></span> | <span data-ttu-id="cff89-566">3</span><span class="sxs-lookup"><span data-stu-id="cff89-566">3</span></span> |
| <span data-ttu-id="cff89-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="cff89-567">stringLength</span></span> | <span data-ttu-id="cff89-568">int</span><span class="sxs-lookup"><span data-stu-id="cff89-568">Int</span></span> | <span data-ttu-id="cff89-569">13</span><span class="sxs-lookup"><span data-stu-id="cff89-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="cff89-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="cff89-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="cff89-571">Hello 총 지정 된 길이 도달할 때까지 toohello 남은 문자를 추가 하 여 오른쪽 맞춤 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-572">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-572">Parameters</span></span>

| <span data-ttu-id="cff89-573">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-573">Parameter</span></span> | <span data-ttu-id="cff89-574">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-574">Required</span></span> | <span data-ttu-id="cff89-575">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-575">Type</span></span> | <span data-ttu-id="cff89-576">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="cff89-577">valueToPad</span></span> |<span data-ttu-id="cff89-578">예</span><span class="sxs-lookup"><span data-stu-id="cff89-578">Yes</span></span> |<span data-ttu-id="cff89-579">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="cff89-579">string or int</span></span> |<span data-ttu-id="cff89-580">값 tooright hello-정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="cff89-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="cff89-581">totalLength</span></span> |<span data-ttu-id="cff89-582">예</span><span class="sxs-lookup"><span data-stu-id="cff89-582">Yes</span></span> |<span data-ttu-id="cff89-583">int</span><span class="sxs-lookup"><span data-stu-id="cff89-583">int</span></span> |<span data-ttu-id="cff89-584">hello에 있는 문자의 총 수를 hello 문자열을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="cff89-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="cff89-585">paddingCharacter</span></span> |<span data-ttu-id="cff89-586">아니요</span><span class="sxs-lookup"><span data-stu-id="cff89-586">No</span></span> |<span data-ttu-id="cff89-587">단일 문자</span><span class="sxs-lookup"><span data-stu-id="cff89-587">single character</span></span> |<span data-ttu-id="cff89-588">hello 총 길이 도달할 때까지 왼쪽 여백에 대 한 hello 문자 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="cff89-589">hello 기본값은 공백입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-589">hello default value is a space.</span></span> |

<span data-ttu-id="cff89-590">Hello 원래 문자열 문자 toopad hello 개수 보다 긴 경우에 문자가 더 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="cff89-591">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-591">Return value</span></span>

<span data-ttu-id="cff89-592">문자열을 지정 된 문자 수를 최소한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-593">예</span><span class="sxs-lookup"><span data-stu-id="cff89-593">Examples</span></span>

<span data-ttu-id="cff89-594">다음 예제는 hello 방법을 toopad hello 사용자가 제공한 매개 변수 값 hello를 추가 하 여 0 문자 hello 총 문자 수에 도달할 때까지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="cff89-595">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-596">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-596">Name</span></span> | <span data-ttu-id="cff89-597">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-597">Type</span></span> | <span data-ttu-id="cff89-598">값</span><span class="sxs-lookup"><span data-stu-id="cff89-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-599">stringOutput</span></span> | <span data-ttu-id="cff89-600">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-600">String</span></span> | <span data-ttu-id="cff89-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="cff89-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="cff89-602">바꾸기</span><span class="sxs-lookup"><span data-stu-id="cff89-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="cff89-603">다른 문자열로 대체한 어떤 문자열의 인스턴스를 포함한 새 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-604">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-604">Parameters</span></span>

| <span data-ttu-id="cff89-605">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-605">Parameter</span></span> | <span data-ttu-id="cff89-606">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-606">Required</span></span> | <span data-ttu-id="cff89-607">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-607">Type</span></span> | <span data-ttu-id="cff89-608">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-609">originalString</span><span class="sxs-lookup"><span data-stu-id="cff89-609">originalString</span></span> |<span data-ttu-id="cff89-610">예</span><span class="sxs-lookup"><span data-stu-id="cff89-610">Yes</span></span> |<span data-ttu-id="cff89-611">string</span><span class="sxs-lookup"><span data-stu-id="cff89-611">string</span></span> |<span data-ttu-id="cff89-612">다른 문자열에 의해 대체 되는 한 문자열의 모든 인스턴스가 포함 된 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="cff89-613">oldString</span><span class="sxs-lookup"><span data-stu-id="cff89-613">oldString</span></span> |<span data-ttu-id="cff89-614">예</span><span class="sxs-lookup"><span data-stu-id="cff89-614">Yes</span></span> |<span data-ttu-id="cff89-615">string</span><span class="sxs-lookup"><span data-stu-id="cff89-615">string</span></span> |<span data-ttu-id="cff89-616">hello 문자열 toobe hello 원래 문자열에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="cff89-617">newString</span><span class="sxs-lookup"><span data-stu-id="cff89-617">newString</span></span> |<span data-ttu-id="cff89-618">예</span><span class="sxs-lookup"><span data-stu-id="cff89-618">Yes</span></span> |<span data-ttu-id="cff89-619">string</span><span class="sxs-lookup"><span data-stu-id="cff89-619">string</span></span> |<span data-ttu-id="cff89-620">hello 문자열 tooadd hello 대신 문자열을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-621">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-621">Return value</span></span>

<span data-ttu-id="cff89-622">Hello로 문자열로 문자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-623">예</span><span class="sxs-lookup"><span data-stu-id="cff89-623">Examples</span></span>

<span data-ttu-id="cff89-624">다음 예제는 hello hello 사용자가 제공한 문자열에서 모든 tooremove 대시 하는 방법 및 다른 문자열로 문자열 hello의 tooreplace 일부로 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="cff89-625">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-626">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-626">Name</span></span> | <span data-ttu-id="cff89-627">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-627">Type</span></span> | <span data-ttu-id="cff89-628">값</span><span class="sxs-lookup"><span data-stu-id="cff89-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-629">firstOutput</span></span> | <span data-ttu-id="cff89-630">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-630">String</span></span> | <span data-ttu-id="cff89-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="cff89-631">1231231234</span></span> |
| <span data-ttu-id="cff89-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-632">secodeOutput</span></span> | <span data-ttu-id="cff89-633">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-633">String</span></span> | <span data-ttu-id="cff89-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="cff89-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="cff89-635">skip</span><span class="sxs-lookup"><span data-stu-id="cff89-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="cff89-636">Hello 지정한 수 만큼의 문자 또는 배열 hello 요소가 모두 hello 요소 수를 지정한 후 후 모든 hello 문자로 이루어진 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-637">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-637">Parameters</span></span>

| <span data-ttu-id="cff89-638">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-638">Parameter</span></span> | <span data-ttu-id="cff89-639">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-639">Required</span></span> | <span data-ttu-id="cff89-640">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-640">Type</span></span> | <span data-ttu-id="cff89-641">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="cff89-642">originalValue</span></span> |<span data-ttu-id="cff89-643">예</span><span class="sxs-lookup"><span data-stu-id="cff89-643">Yes</span></span> |<span data-ttu-id="cff89-644">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-644">array or string</span></span> |<span data-ttu-id="cff89-645">건너뛰기 위한 hello 배열 또는 문자열 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="cff89-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="cff89-646">numberToSkip</span></span> |<span data-ttu-id="cff89-647">예</span><span class="sxs-lookup"><span data-stu-id="cff89-647">Yes</span></span> |<span data-ttu-id="cff89-648">int</span><span class="sxs-lookup"><span data-stu-id="cff89-648">int</span></span> |<span data-ttu-id="cff89-649">요소 또는 문자 tooskip hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="cff89-650">이 값이 0, 모든 요소를 hello 또는 hello 값의 문자 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="cff89-651">Hello 배열 또는 문자열의 hello 길이 보다 큰 경우 빈 배열 또는 문자열 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-652">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-652">Return value</span></span>

<span data-ttu-id="cff89-653">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-654">예</span><span class="sxs-lookup"><span data-stu-id="cff89-654">Examples</span></span>

<span data-ttu-id="cff89-655">다음 예에서는 건너뜁니다 hello hello hello 배열에서 요소 수를 지정 된 한 hello 문자열에 문자 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="cff89-656">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-657">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-657">Name</span></span> | <span data-ttu-id="cff89-658">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-658">Type</span></span> | <span data-ttu-id="cff89-659">값</span><span class="sxs-lookup"><span data-stu-id="cff89-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-660">arrayOutput</span></span> | <span data-ttu-id="cff89-661">배열</span><span class="sxs-lookup"><span data-stu-id="cff89-661">Array</span></span> | <span data-ttu-id="cff89-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="cff89-662">["three"]</span></span> |
| <span data-ttu-id="cff89-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-663">stringOutput</span></span> | <span data-ttu-id="cff89-664">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-664">String</span></span> | <span data-ttu-id="cff89-665">two three</span><span class="sxs-lookup"><span data-stu-id="cff89-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="cff89-666">분할</span><span class="sxs-lookup"><span data-stu-id="cff89-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="cff89-667">구분 기호를 지정 하는 hello 구분 되는 입력 문자열의 hello hello 하위 문자열이 포함 된 문자열의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-668">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-668">Parameters</span></span>

| <span data-ttu-id="cff89-669">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-669">Parameter</span></span> | <span data-ttu-id="cff89-670">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-670">Required</span></span> | <span data-ttu-id="cff89-671">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-671">Type</span></span> | <span data-ttu-id="cff89-672">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-673">inputString</span><span class="sxs-lookup"><span data-stu-id="cff89-673">inputString</span></span> |<span data-ttu-id="cff89-674">예</span><span class="sxs-lookup"><span data-stu-id="cff89-674">Yes</span></span> |<span data-ttu-id="cff89-675">string</span><span class="sxs-lookup"><span data-stu-id="cff89-675">string</span></span> |<span data-ttu-id="cff89-676">hello 문자열 toosplit 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-676">hello string toosplit.</span></span> |
| <span data-ttu-id="cff89-677">구분 기호</span><span class="sxs-lookup"><span data-stu-id="cff89-677">delimiter</span></span> |<span data-ttu-id="cff89-678">예</span><span class="sxs-lookup"><span data-stu-id="cff89-678">Yes</span></span> |<span data-ttu-id="cff89-679">문자열 또는 문자열 배열</span><span class="sxs-lookup"><span data-stu-id="cff89-679">string or array of strings</span></span> |<span data-ttu-id="cff89-680">구분 기호 toouse hello 문자열을 분할 하는 데 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-681">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-681">Return value</span></span>

<span data-ttu-id="cff89-682">문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-683">예</span><span class="sxs-lookup"><span data-stu-id="cff89-683">Examples</span></span>

<span data-ttu-id="cff89-684">hello 다음 예제에서는 분할 hello 입력된 문자열에 쉼표와 쉼표 또는 세미콜론입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="cff89-685">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-686">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-686">Name</span></span> | <span data-ttu-id="cff89-687">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-687">Type</span></span> | <span data-ttu-id="cff89-688">값</span><span class="sxs-lookup"><span data-stu-id="cff89-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-689">firstOutput</span></span> | <span data-ttu-id="cff89-690">배열</span><span class="sxs-lookup"><span data-stu-id="cff89-690">Array</span></span> | <span data-ttu-id="cff89-691">[“one”, “two”, “three”]</span><span class="sxs-lookup"><span data-stu-id="cff89-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="cff89-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-692">secondOutput</span></span> | <span data-ttu-id="cff89-693">배열</span><span class="sxs-lookup"><span data-stu-id="cff89-693">Array</span></span> | <span data-ttu-id="cff89-694">[“one”, “two”, “three”]</span><span class="sxs-lookup"><span data-stu-id="cff89-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="cff89-695">startswith</span><span class="sxs-lookup"><span data-stu-id="cff89-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="cff89-696">문자열이 값으로 시작하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="cff89-697">hello 비교는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-698">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-698">Parameters</span></span>

| <span data-ttu-id="cff89-699">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-699">Parameter</span></span> | <span data-ttu-id="cff89-700">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-700">Required</span></span> | <span data-ttu-id="cff89-701">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-701">Type</span></span> | <span data-ttu-id="cff89-702">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="cff89-703">stringToSearch</span></span> |<span data-ttu-id="cff89-704">예</span><span class="sxs-lookup"><span data-stu-id="cff89-704">Yes</span></span> |<span data-ttu-id="cff89-705">string</span><span class="sxs-lookup"><span data-stu-id="cff89-705">string</span></span> |<span data-ttu-id="cff89-706">hello 항목 toofind를 포함 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="cff89-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="cff89-707">stringToFind</span></span> |<span data-ttu-id="cff89-708">예</span><span class="sxs-lookup"><span data-stu-id="cff89-708">Yes</span></span> |<span data-ttu-id="cff89-709">string</span><span class="sxs-lookup"><span data-stu-id="cff89-709">string</span></span> |<span data-ttu-id="cff89-710">hello 값 toofind 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-711">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-711">Return value</span></span>

<span data-ttu-id="cff89-712">**True** hello 기본 동작은 일치 하는 hello 첫 번째 문자 또는 문자 hello 문자열의 경우 이렇게 하지 않으면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-713">예</span><span class="sxs-lookup"><span data-stu-id="cff89-713">Examples</span></span>

<span data-ttu-id="cff89-714">다음 예제는 hello toouse startsWith 및 endsWith 함수 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="cff89-715">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-716">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-716">Name</span></span> | <span data-ttu-id="cff89-717">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-717">Type</span></span> | <span data-ttu-id="cff89-718">값</span><span class="sxs-lookup"><span data-stu-id="cff89-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-719">startsTrue</span></span> | <span data-ttu-id="cff89-720">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-720">Bool</span></span> | <span data-ttu-id="cff89-721">True</span><span class="sxs-lookup"><span data-stu-id="cff89-721">True</span></span> |
| <span data-ttu-id="cff89-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-722">startsCapTrue</span></span> | <span data-ttu-id="cff89-723">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-723">Bool</span></span> | <span data-ttu-id="cff89-724">True</span><span class="sxs-lookup"><span data-stu-id="cff89-724">True</span></span> |
| <span data-ttu-id="cff89-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-725">startsFalse</span></span> | <span data-ttu-id="cff89-726">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-726">Bool</span></span> | <span data-ttu-id="cff89-727">False</span><span class="sxs-lookup"><span data-stu-id="cff89-727">False</span></span> |
| <span data-ttu-id="cff89-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-728">endsTrue</span></span> | <span data-ttu-id="cff89-729">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-729">Bool</span></span> | <span data-ttu-id="cff89-730">True</span><span class="sxs-lookup"><span data-stu-id="cff89-730">True</span></span> |
| <span data-ttu-id="cff89-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="cff89-731">endsCapTrue</span></span> | <span data-ttu-id="cff89-732">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-732">Bool</span></span> | <span data-ttu-id="cff89-733">True</span><span class="sxs-lookup"><span data-stu-id="cff89-733">True</span></span> |
| <span data-ttu-id="cff89-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="cff89-734">endsFalse</span></span> | <span data-ttu-id="cff89-735">Bool</span><span class="sxs-lookup"><span data-stu-id="cff89-735">Bool</span></span> | <span data-ttu-id="cff89-736">False</span><span class="sxs-lookup"><span data-stu-id="cff89-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="cff89-737">string</span><span class="sxs-lookup"><span data-stu-id="cff89-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="cff89-738">변환 hello tooa 문자열 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-739">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-739">Parameters</span></span>

| <span data-ttu-id="cff89-740">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-740">Parameter</span></span> | <span data-ttu-id="cff89-741">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-741">Required</span></span> | <span data-ttu-id="cff89-742">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-742">Type</span></span> | <span data-ttu-id="cff89-743">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="cff89-744">valueToConvert</span></span> |<span data-ttu-id="cff89-745">예</span><span class="sxs-lookup"><span data-stu-id="cff89-745">Yes</span></span> | <span data-ttu-id="cff89-746">모두</span><span class="sxs-lookup"><span data-stu-id="cff89-746">Any</span></span> |<span data-ttu-id="cff89-747">hello 값 tooconvert toostring 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="cff89-748">개체 및 배열을 비롯하여 모든 값 형식을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-749">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-749">Return value</span></span>

<span data-ttu-id="cff89-750">Hello 변환 된 값의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-751">예</span><span class="sxs-lookup"><span data-stu-id="cff89-751">Examples</span></span>

<span data-ttu-id="cff89-752">다음 예제는 hello tooconvert 다양 한 유형의 toostrings 값 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="cff89-753">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-754">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-754">Name</span></span> | <span data-ttu-id="cff89-755">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-755">Type</span></span> | <span data-ttu-id="cff89-756">값</span><span class="sxs-lookup"><span data-stu-id="cff89-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-757">objectOutput</span></span> | <span data-ttu-id="cff89-758">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-758">String</span></span> | <span data-ttu-id="cff89-759">{“valueA”:10,“valueB”:“Example Text”}</span><span class="sxs-lookup"><span data-stu-id="cff89-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="cff89-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-760">arrayOutput</span></span> | <span data-ttu-id="cff89-761">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-761">String</span></span> | <span data-ttu-id="cff89-762">[“a”,“b”,“c”]</span><span class="sxs-lookup"><span data-stu-id="cff89-762">["a","b","c"]</span></span> |
| <span data-ttu-id="cff89-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-763">intOutput</span></span> | <span data-ttu-id="cff89-764">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-764">String</span></span> | <span data-ttu-id="cff89-765">5</span><span class="sxs-lookup"><span data-stu-id="cff89-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="cff89-766">substring</span><span class="sxs-lookup"><span data-stu-id="cff89-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="cff89-767">지정한 문자 수를 지정 하는 hello에서 문자 위치 및 hello가 포함 되어 하위 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-768">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-768">Parameters</span></span>

| <span data-ttu-id="cff89-769">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-769">Parameter</span></span> | <span data-ttu-id="cff89-770">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-770">Required</span></span> | <span data-ttu-id="cff89-771">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-771">Type</span></span> | <span data-ttu-id="cff89-772">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="cff89-773">stringToParse</span></span> |<span data-ttu-id="cff89-774">예</span><span class="sxs-lookup"><span data-stu-id="cff89-774">Yes</span></span> |<span data-ttu-id="cff89-775">string</span><span class="sxs-lookup"><span data-stu-id="cff89-775">string</span></span> |<span data-ttu-id="cff89-776">부분 문자열을 추출할는 hello에서 원래 문자열 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="cff89-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="cff89-777">startIndex</span></span> |<span data-ttu-id="cff89-778">아니요</span><span class="sxs-lookup"><span data-stu-id="cff89-778">No</span></span> |<span data-ttu-id="cff89-779">int</span><span class="sxs-lookup"><span data-stu-id="cff89-779">int</span></span> |<span data-ttu-id="cff89-780">hello 부분 문자열에 대 한 0부터 시작할 문자 위치를 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="cff89-781">length</span><span class="sxs-lookup"><span data-stu-id="cff89-781">length</span></span> |<span data-ttu-id="cff89-782">아니요</span><span class="sxs-lookup"><span data-stu-id="cff89-782">No</span></span> |<span data-ttu-id="cff89-783">int</span><span class="sxs-lookup"><span data-stu-id="cff89-783">int</span></span> |<span data-ttu-id="cff89-784">hello 부분 문자열에 대 한 문자 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="cff89-785">Hello 문자열 내의 tooa 위치를 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-786">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-786">Return value</span></span>

<span data-ttu-id="cff89-787">hello 부분 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="cff89-788">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-788">Remarks</span></span>

<span data-ttu-id="cff89-789">hello 함수 hello 부분 문자열 hello 문자열 hello 끝을 넘어 확장 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="cff89-790">다음 예제는 hello 실패 hello 오류 "hello 인덱스 및 길이 매개 변수가 참조 해야 hello 문자열 내의 tooa 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="cff89-791">hello 인덱스 매개 변수: '0' hello 길이 매개 변수: '11' hello hello 문자열 매개 변수의 길이: '10'. "입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="cff89-792">예</span><span class="sxs-lookup"><span data-stu-id="cff89-792">Examples</span></span>

<span data-ttu-id="cff89-793">다음 예제는 hello 매개 변수에서 하위 문자열을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="cff89-794">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-795">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-795">Name</span></span> | <span data-ttu-id="cff89-796">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-796">Type</span></span> | <span data-ttu-id="cff89-797">값</span><span class="sxs-lookup"><span data-stu-id="cff89-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-798">substringOutput</span></span> | <span data-ttu-id="cff89-799">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-799">String</span></span> | <span data-ttu-id="cff89-800">two</span><span class="sxs-lookup"><span data-stu-id="cff89-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="cff89-801">take</span><span class="sxs-lookup"><span data-stu-id="cff89-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="cff89-802">Hello로 문자열의 시작 부분 hello에서에서 문자 수가 지정 된 반환 문자열 hello 또는 hello로 배열에서 hello 시작 hello 배열의 요소 수를 지정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cff89-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-803">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-803">Parameters</span></span>

| <span data-ttu-id="cff89-804">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-804">Parameter</span></span> | <span data-ttu-id="cff89-805">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-805">Required</span></span> | <span data-ttu-id="cff89-806">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-806">Type</span></span> | <span data-ttu-id="cff89-807">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="cff89-808">originalValue</span></span> |<span data-ttu-id="cff89-809">예</span><span class="sxs-lookup"><span data-stu-id="cff89-809">Yes</span></span> |<span data-ttu-id="cff89-810">배열 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-810">array or string</span></span> |<span data-ttu-id="cff89-811">배열 또는 문자열 tootake hello 요소를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="cff89-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="cff89-812">numberToTake</span></span> |<span data-ttu-id="cff89-813">예</span><span class="sxs-lookup"><span data-stu-id="cff89-813">Yes</span></span> |<span data-ttu-id="cff89-814">int</span><span class="sxs-lookup"><span data-stu-id="cff89-814">int</span></span> |<span data-ttu-id="cff89-815">요소 또는 문자 tootake hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="cff89-816">이 값이 0 이하이면 빈 배열 또는 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="cff89-817">지정 된 배열 또는 문자열 hello의 hello 길이 보다 큰 경우 hello 배열 또는 문자열의 모든 hello 요소가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-818">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-818">Return value</span></span>

<span data-ttu-id="cff89-819">배열 또는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-820">예</span><span class="sxs-lookup"><span data-stu-id="cff89-820">Examples</span></span>

<span data-ttu-id="cff89-821">다음 예제는 hello hello hello 배열에서 요소 및 문자열에서 문자 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="cff89-822">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-823">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-823">Name</span></span> | <span data-ttu-id="cff89-824">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-824">Type</span></span> | <span data-ttu-id="cff89-825">값</span><span class="sxs-lookup"><span data-stu-id="cff89-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-826">arrayOutput</span></span> | <span data-ttu-id="cff89-827">배열</span><span class="sxs-lookup"><span data-stu-id="cff89-827">Array</span></span> | <span data-ttu-id="cff89-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="cff89-828">["one", "two"]</span></span> |
| <span data-ttu-id="cff89-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-829">stringOutput</span></span> | <span data-ttu-id="cff89-830">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-830">String</span></span> | <span data-ttu-id="cff89-831">on</span><span class="sxs-lookup"><span data-stu-id="cff89-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="cff89-832">toLower</span><span class="sxs-lookup"><span data-stu-id="cff89-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="cff89-833">변환 hello 문자열 toolower 대/소문자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-834">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-834">Parameters</span></span>

| <span data-ttu-id="cff89-835">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-835">Parameter</span></span> | <span data-ttu-id="cff89-836">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-836">Required</span></span> | <span data-ttu-id="cff89-837">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-837">Type</span></span> | <span data-ttu-id="cff89-838">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="cff89-839">stringToChange</span></span> |<span data-ttu-id="cff89-840">예</span><span class="sxs-lookup"><span data-stu-id="cff89-840">Yes</span></span> |<span data-ttu-id="cff89-841">string</span><span class="sxs-lookup"><span data-stu-id="cff89-841">string</span></span> |<span data-ttu-id="cff89-842">hello 값 tooconvert toolower 케이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-843">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-843">Return value</span></span>

<span data-ttu-id="cff89-844">toolower 대/소문자를 변환 하는 hello 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-845">예</span><span class="sxs-lookup"><span data-stu-id="cff89-845">Examples</span></span>

<span data-ttu-id="cff89-846">다음 예제는 hello 매개 변수 값 toolower 대/소문자 및 tooupper 대/소문자 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="cff89-847">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-848">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-848">Name</span></span> | <span data-ttu-id="cff89-849">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-849">Type</span></span> | <span data-ttu-id="cff89-850">값</span><span class="sxs-lookup"><span data-stu-id="cff89-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-851">toLowerOutput</span></span> | <span data-ttu-id="cff89-852">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-852">String</span></span> | <span data-ttu-id="cff89-853">one two three</span><span class="sxs-lookup"><span data-stu-id="cff89-853">one two three</span></span> |
| <span data-ttu-id="cff89-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-854">toUpperOutput</span></span> | <span data-ttu-id="cff89-855">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-855">String</span></span> | <span data-ttu-id="cff89-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="cff89-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="cff89-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="cff89-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="cff89-858">변환 hello 문자열 tooupper 대/소문자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-859">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-859">Parameters</span></span>

| <span data-ttu-id="cff89-860">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-860">Parameter</span></span> | <span data-ttu-id="cff89-861">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-861">Required</span></span> | <span data-ttu-id="cff89-862">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-862">Type</span></span> | <span data-ttu-id="cff89-863">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="cff89-864">stringToChange</span></span> |<span data-ttu-id="cff89-865">예</span><span class="sxs-lookup"><span data-stu-id="cff89-865">Yes</span></span> |<span data-ttu-id="cff89-866">string</span><span class="sxs-lookup"><span data-stu-id="cff89-866">string</span></span> |<span data-ttu-id="cff89-867">hello 값 tooconvert tooupper 케이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-868">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-868">Return value</span></span>

<span data-ttu-id="cff89-869">tooupper 대/소문자를 변환 하는 hello 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-870">예</span><span class="sxs-lookup"><span data-stu-id="cff89-870">Examples</span></span>

<span data-ttu-id="cff89-871">다음 예제는 hello 매개 변수 값 toolower 대/소문자 및 tooupper 대/소문자 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="cff89-872">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-873">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-873">Name</span></span> | <span data-ttu-id="cff89-874">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-874">Type</span></span> | <span data-ttu-id="cff89-875">값</span><span class="sxs-lookup"><span data-stu-id="cff89-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-876">toLowerOutput</span></span> | <span data-ttu-id="cff89-877">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-877">String</span></span> | <span data-ttu-id="cff89-878">one two three</span><span class="sxs-lookup"><span data-stu-id="cff89-878">one two three</span></span> |
| <span data-ttu-id="cff89-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-879">toUpperOutput</span></span> | <span data-ttu-id="cff89-880">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-880">String</span></span> | <span data-ttu-id="cff89-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="cff89-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="cff89-882">trim</span><span class="sxs-lookup"><span data-stu-id="cff89-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="cff89-883">지정 된 모든 선행 및 후행 공백 문자 hello에서 제거.</span><span class="sxs-lookup"><span data-stu-id="cff89-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-884">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-884">Parameters</span></span>

| <span data-ttu-id="cff89-885">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-885">Parameter</span></span> | <span data-ttu-id="cff89-886">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-886">Required</span></span> | <span data-ttu-id="cff89-887">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-887">Type</span></span> | <span data-ttu-id="cff89-888">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="cff89-889">stringToTrim</span></span> |<span data-ttu-id="cff89-890">예</span><span class="sxs-lookup"><span data-stu-id="cff89-890">Yes</span></span> |<span data-ttu-id="cff89-891">string</span><span class="sxs-lookup"><span data-stu-id="cff89-891">string</span></span> |<span data-ttu-id="cff89-892">hello 값 tootrim 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-893">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-893">Return value</span></span>

<span data-ttu-id="cff89-894">선행 및 후행 공백 문자 없이 hello 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-895">예</span><span class="sxs-lookup"><span data-stu-id="cff89-895">Examples</span></span>

<span data-ttu-id="cff89-896">hello 다음 예제에서는 트림 hello 매개 변수에서 공백 문자 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="cff89-897">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-898">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-898">Name</span></span> | <span data-ttu-id="cff89-899">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-899">Type</span></span> | <span data-ttu-id="cff89-900">값</span><span class="sxs-lookup"><span data-stu-id="cff89-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-901">return</span><span class="sxs-lookup"><span data-stu-id="cff89-901">return</span></span> | <span data-ttu-id="cff89-902">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-902">String</span></span> | <span data-ttu-id="cff89-903">one two three</span><span class="sxs-lookup"><span data-stu-id="cff89-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="cff89-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="cff89-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="cff89-905">매개 변수로 제공 되는 hello 값에 따라 결정적 해시 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="cff89-906">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-906">Parameters</span></span>

| <span data-ttu-id="cff89-907">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-907">Parameter</span></span> | <span data-ttu-id="cff89-908">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-908">Required</span></span> | <span data-ttu-id="cff89-909">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-909">Type</span></span> | <span data-ttu-id="cff89-910">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-911">baseString</span><span class="sxs-lookup"><span data-stu-id="cff89-911">baseString</span></span> |<span data-ttu-id="cff89-912">예</span><span class="sxs-lookup"><span data-stu-id="cff89-912">Yes</span></span> |<span data-ttu-id="cff89-913">string</span><span class="sxs-lookup"><span data-stu-id="cff89-913">string</span></span> |<span data-ttu-id="cff89-914">hello 해시 함수 toocreate 고유한 문자열 hello 값 사용.</span><span class="sxs-lookup"><span data-stu-id="cff89-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="cff89-915">필요에 따라 추가하는 매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-915">additional parameters as needed</span></span> |<span data-ttu-id="cff89-916">아니요</span><span class="sxs-lookup"><span data-stu-id="cff89-916">No</span></span> |<span data-ttu-id="cff89-917">string</span><span class="sxs-lookup"><span data-stu-id="cff89-917">string</span></span> |<span data-ttu-id="cff89-918">Hello 수준의 고유성을 지정 하는 필요한 toocreate hello 값으로 만큼 문자열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="cff89-919">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-919">Remarks</span></span>

<span data-ttu-id="cff89-920">이 함수는 리소스에 대 한 고유한 이름을 toocreate 할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="cff89-921">Hello 결과 대 한 고유성 hello 범위를 제한 하는 매개 변수 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="cff89-922">Hello 이름이 고유 toosubscription, 리소스 그룹 또는 배포 인지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="cff89-923">값은 임의의 문자열이 아니지만 대신 해시 함수의 결과 hello hello 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="cff89-924">hello 반환 값은 13 자입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="cff89-925">전역적으로 고유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-925">It is not globally unique.</span></span> <span data-ttu-id="cff89-926">프로그램 명명 규칙 toocreate 의미 있는 이름에서에서 접두사로 toocombine hello 값을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="cff89-927">hello 다음 예제 hello 형식의 hello 값을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="cff89-928">제공 된 매개 변수는 hello hello 실제 값이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="cff89-929">다음 예제는 hello 어떻게 toouse uniqueString toocreate 고유 값을 일반적으로 사용 되는 수준의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="cff89-930">범위 지정 된 고유 toosubscription</span><span class="sxs-lookup"><span data-stu-id="cff89-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="cff89-931">범위 지정 된 고유 tooresource 그룹</span><span class="sxs-lookup"><span data-stu-id="cff89-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="cff89-932">리소스 그룹에 대 한 범위 지정 된 고유 toodeployment</span><span class="sxs-lookup"><span data-stu-id="cff89-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="cff89-933">다음 예제는 hello 방법을 toocreate 저장소 계정에 대 한 고유한 이름을 기반으로 리소스 그룹을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="cff89-934">Hello 리소스 그룹의 내부 hello 이름이 고유 하지 않은 hello를 생성 하는 경우 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="cff89-935">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-935">Return value</span></span>

<span data-ttu-id="cff89-936">13개의 문자를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-937">예</span><span class="sxs-lookup"><span data-stu-id="cff89-937">Examples</span></span>

<span data-ttu-id="cff89-938">다음 예에서는 hello uniquestring에서 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="cff89-939">uri</span><span class="sxs-lookup"><span data-stu-id="cff89-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="cff89-940">Hello baseUri 및 hello 될 문자열을 결합 하 여 절대 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-941">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-941">Parameters</span></span>

| <span data-ttu-id="cff89-942">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-942">Parameter</span></span> | <span data-ttu-id="cff89-943">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-943">Required</span></span> | <span data-ttu-id="cff89-944">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-944">Type</span></span> | <span data-ttu-id="cff89-945">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="cff89-946">baseUri</span></span> |<span data-ttu-id="cff89-947">예</span><span class="sxs-lookup"><span data-stu-id="cff89-947">Yes</span></span> |<span data-ttu-id="cff89-948">string</span><span class="sxs-lookup"><span data-stu-id="cff89-948">string</span></span> |<span data-ttu-id="cff89-949">hello 기본 uri 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-949">hello base uri string.</span></span> |
| <span data-ttu-id="cff89-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="cff89-950">relativeUri</span></span> |<span data-ttu-id="cff89-951">예</span><span class="sxs-lookup"><span data-stu-id="cff89-951">Yes</span></span> |<span data-ttu-id="cff89-952">string</span><span class="sxs-lookup"><span data-stu-id="cff89-952">string</span></span> |<span data-ttu-id="cff89-953">hello 상대 uri 문자열 tooadd toohello 기본 uri 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="cff89-954">hello에 대 한 값을 hello **baseUri** 매개 변수는 특정 파일을 포함할 수 있지만 hello 기본 경로만 hello URI를 구성할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="cff89-955">예를 들어 전달 `http://contoso.com/resources/azuredeploy.json` 의 기본 URI에 baseUri 매개 변수에 결과 hello로 `http://contoso.com/resources/`합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="cff89-956">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-956">Return value</span></span>

<span data-ttu-id="cff89-957">Hello 기본 및 상대 값에 대 한 절대 URI를 hello 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-958">예</span><span class="sxs-lookup"><span data-stu-id="cff89-958">Examples</span></span>

<span data-ttu-id="cff89-959">다음 예제는 hello 방법을 tooconstruct 링크 tooa 중첩 된 템플릿 값을 기반 hello hello 부모 템플릿의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="cff89-960">hello 방법을 예제와 다음 toouse uri, uriComponent, 및 uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="cff89-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="cff89-961">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-962">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-962">Name</span></span> | <span data-ttu-id="cff89-963">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-963">Type</span></span> | <span data-ttu-id="cff89-964">값</span><span class="sxs-lookup"><span data-stu-id="cff89-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-965">uriOutput</span></span> | <span data-ttu-id="cff89-966">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-966">String</span></span> | <span data-ttu-id="cff89-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="cff89-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-968">componentOutput</span></span> | <span data-ttu-id="cff89-969">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-969">String</span></span> | <span data-ttu-id="cff89-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="cff89-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-971">toStringOutput</span></span> | <span data-ttu-id="cff89-972">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-972">String</span></span> | <span data-ttu-id="cff89-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="cff89-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="cff89-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="cff89-975">URI를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-976">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-976">Parameters</span></span>

| <span data-ttu-id="cff89-977">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-977">Parameter</span></span> | <span data-ttu-id="cff89-978">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-978">Required</span></span> | <span data-ttu-id="cff89-979">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-979">Type</span></span> | <span data-ttu-id="cff89-980">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="cff89-981">stringToEncode</span></span> |<span data-ttu-id="cff89-982">예</span><span class="sxs-lookup"><span data-stu-id="cff89-982">Yes</span></span> |<span data-ttu-id="cff89-983">string</span><span class="sxs-lookup"><span data-stu-id="cff89-983">string</span></span> |<span data-ttu-id="cff89-984">hello 값 tooencode 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-985">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-985">Return value</span></span>

<span data-ttu-id="cff89-986">Hello URI의 문자열 값을 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-987">예</span><span class="sxs-lookup"><span data-stu-id="cff89-987">Examples</span></span>

<span data-ttu-id="cff89-988">hello 방법을 예제와 다음 toouse uri, uriComponent, 및 uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="cff89-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="cff89-989">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-990">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-990">Name</span></span> | <span data-ttu-id="cff89-991">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-991">Type</span></span> | <span data-ttu-id="cff89-992">값</span><span class="sxs-lookup"><span data-stu-id="cff89-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-993">uriOutput</span></span> | <span data-ttu-id="cff89-994">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-994">String</span></span> | <span data-ttu-id="cff89-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="cff89-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-996">componentOutput</span></span> | <span data-ttu-id="cff89-997">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-997">String</span></span> | <span data-ttu-id="cff89-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="cff89-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-999">toStringOutput</span></span> | <span data-ttu-id="cff89-1000">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-1000">String</span></span> | <span data-ttu-id="cff89-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="cff89-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="cff89-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="cff89-1003">URI로 인코딩된 값의 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="cff89-1004">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cff89-1004">Parameters</span></span>

| <span data-ttu-id="cff89-1005">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1005">Parameter</span></span> | <span data-ttu-id="cff89-1006">필수</span><span class="sxs-lookup"><span data-stu-id="cff89-1006">Required</span></span> | <span data-ttu-id="cff89-1007">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-1007">Type</span></span> | <span data-ttu-id="cff89-1008">설명</span><span class="sxs-lookup"><span data-stu-id="cff89-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cff89-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="cff89-1009">uriEncodedString</span></span> |<span data-ttu-id="cff89-1010">예</span><span class="sxs-lookup"><span data-stu-id="cff89-1010">Yes</span></span> |<span data-ttu-id="cff89-1011">string</span><span class="sxs-lookup"><span data-stu-id="cff89-1011">string</span></span> |<span data-ttu-id="cff89-1012">hello URI 인코딩된 tooconvert tooa 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cff89-1013">반환 값</span><span class="sxs-lookup"><span data-stu-id="cff89-1013">Return value</span></span>

<span data-ttu-id="cff89-1014">URI로 인코딩된 값의 디코딩된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="cff89-1015">예</span><span class="sxs-lookup"><span data-stu-id="cff89-1015">Examples</span></span>

<span data-ttu-id="cff89-1016">hello 방법을 예제와 다음 toouse uri, uriComponent, 및 uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="cff89-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="cff89-1017">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="cff89-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cff89-1018">이름</span><span class="sxs-lookup"><span data-stu-id="cff89-1018">Name</span></span> | <span data-ttu-id="cff89-1019">형식</span><span class="sxs-lookup"><span data-stu-id="cff89-1019">Type</span></span> | <span data-ttu-id="cff89-1020">값</span><span class="sxs-lookup"><span data-stu-id="cff89-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cff89-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-1021">uriOutput</span></span> | <span data-ttu-id="cff89-1022">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-1022">String</span></span> | <span data-ttu-id="cff89-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="cff89-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-1024">componentOutput</span></span> | <span data-ttu-id="cff89-1025">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-1025">String</span></span> | <span data-ttu-id="cff89-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="cff89-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="cff89-1027">toStringOutput</span></span> | <span data-ttu-id="cff89-1028">문자열</span><span class="sxs-lookup"><span data-stu-id="cff89-1028">String</span></span> | <span data-ttu-id="cff89-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="cff89-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="cff89-1030">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cff89-1030">Next steps</span></span>
* <span data-ttu-id="cff89-1031">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="cff89-1032">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="cff89-1033">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="cff89-1034">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cff89-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

