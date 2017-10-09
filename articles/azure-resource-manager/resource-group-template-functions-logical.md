---
title: "aaaAzure 리소스 관리자 템플릿 함수-논리 | Microsoft Docs"
description: "Hello 함수 toouse Azure 리소스 관리자 템플릿 toodetermine 논리 값에 설명합니다."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="9516c-103">Azure Resource Manager 템플릿용 논리 함수</span><span class="sxs-lookup"><span data-stu-id="9516c-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="9516c-104">Resource Manager는 템플릿에서 비교를 수행하기 위한 몇 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="9516c-105">and</span><span class="sxs-lookup"><span data-stu-id="9516c-105">and</span></span>](#and)
* [<span data-ttu-id="9516c-106">bool</span><span class="sxs-lookup"><span data-stu-id="9516c-106">bool</span></span>](#bool)
* [<span data-ttu-id="9516c-107">if</span><span class="sxs-lookup"><span data-stu-id="9516c-107">if</span></span>](#if)
* [<span data-ttu-id="9516c-108">not</span><span class="sxs-lookup"><span data-stu-id="9516c-108">not</span></span>](#not)
* [<span data-ttu-id="9516c-109">or</span><span class="sxs-lookup"><span data-stu-id="9516c-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="9516c-110">and</span><span class="sxs-lookup"><span data-stu-id="9516c-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="9516c-111">두 매개 변수 값이 모두 true인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="9516c-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9516c-112">Parameters</span></span>

| <span data-ttu-id="9516c-113">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-113">Parameter</span></span> | <span data-ttu-id="9516c-114">필수</span><span class="sxs-lookup"><span data-stu-id="9516c-114">Required</span></span> | <span data-ttu-id="9516c-115">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-115">Type</span></span> | <span data-ttu-id="9516c-116">설명</span><span class="sxs-lookup"><span data-stu-id="9516c-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9516c-117">arg1</span><span class="sxs-lookup"><span data-stu-id="9516c-117">arg1</span></span> |<span data-ttu-id="9516c-118">예</span><span class="sxs-lookup"><span data-stu-id="9516c-118">Yes</span></span> |<span data-ttu-id="9516c-119">부울</span><span class="sxs-lookup"><span data-stu-id="9516c-119">boolean</span></span> |<span data-ttu-id="9516c-120">첫 번째 값 toocheck 여부 hello 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="9516c-121">arg2</span><span class="sxs-lookup"><span data-stu-id="9516c-121">arg2</span></span> |<span data-ttu-id="9516c-122">예</span><span class="sxs-lookup"><span data-stu-id="9516c-122">Yes</span></span> |<span data-ttu-id="9516c-123">부울</span><span class="sxs-lookup"><span data-stu-id="9516c-123">boolean</span></span> |<span data-ttu-id="9516c-124">두 번째 값 toocheck 여부 hello 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9516c-125">반환 값</span><span class="sxs-lookup"><span data-stu-id="9516c-125">Return value</span></span>

<span data-ttu-id="9516c-126">두 값이 모두 true이면 **True**를 반환하고 그렇지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9516c-127">예</span><span class="sxs-lookup"><span data-stu-id="9516c-127">Examples</span></span>

<span data-ttu-id="9516c-128">hello 방법을 예제와 다음 toouse 논리 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-128">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="9516c-129">앞 예제는 hello hello 출력은:</span><span class="sxs-lookup"><span data-stu-id="9516c-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="9516c-130">이름</span><span class="sxs-lookup"><span data-stu-id="9516c-130">Name</span></span> | <span data-ttu-id="9516c-131">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-131">Type</span></span> | <span data-ttu-id="9516c-132">값</span><span class="sxs-lookup"><span data-stu-id="9516c-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9516c-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-133">andExampleOutput</span></span> | <span data-ttu-id="9516c-134">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-134">Bool</span></span> | <span data-ttu-id="9516c-135">False</span><span class="sxs-lookup"><span data-stu-id="9516c-135">False</span></span> |
| <span data-ttu-id="9516c-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-136">orExampleOutput</span></span> | <span data-ttu-id="9516c-137">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-137">Bool</span></span> | <span data-ttu-id="9516c-138">True</span><span class="sxs-lookup"><span data-stu-id="9516c-138">True</span></span> |
| <span data-ttu-id="9516c-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-139">notExampleOutput</span></span> | <span data-ttu-id="9516c-140">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-140">Bool</span></span> | <span data-ttu-id="9516c-141">False</span><span class="sxs-lookup"><span data-stu-id="9516c-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="9516c-142">bool</span><span class="sxs-lookup"><span data-stu-id="9516c-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="9516c-143">변환 매개 변수 tooa hello 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="9516c-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9516c-144">Parameters</span></span>

| <span data-ttu-id="9516c-145">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-145">Parameter</span></span> | <span data-ttu-id="9516c-146">필수</span><span class="sxs-lookup"><span data-stu-id="9516c-146">Required</span></span> | <span data-ttu-id="9516c-147">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-147">Type</span></span> | <span data-ttu-id="9516c-148">설명</span><span class="sxs-lookup"><span data-stu-id="9516c-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9516c-149">arg1</span><span class="sxs-lookup"><span data-stu-id="9516c-149">arg1</span></span> |<span data-ttu-id="9516c-150">예</span><span class="sxs-lookup"><span data-stu-id="9516c-150">Yes</span></span> |<span data-ttu-id="9516c-151">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="9516c-151">string or int</span></span> |<span data-ttu-id="9516c-152">값 tooconvert tooa hello 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9516c-153">반환 값</span><span class="sxs-lookup"><span data-stu-id="9516c-153">Return value</span></span>
<span data-ttu-id="9516c-154">Hello의 부울 값을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="9516c-155">예</span><span class="sxs-lookup"><span data-stu-id="9516c-155">Examples</span></span>

<span data-ttu-id="9516c-156">hello 방법을 예제와 다음 toouse bool 된 문자열 또는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-156">hello following example shows how toouse bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="9516c-157">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="9516c-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="9516c-158">이름</span><span class="sxs-lookup"><span data-stu-id="9516c-158">Name</span></span> | <span data-ttu-id="9516c-159">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-159">Type</span></span> | <span data-ttu-id="9516c-160">값</span><span class="sxs-lookup"><span data-stu-id="9516c-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9516c-161">trueString</span><span class="sxs-lookup"><span data-stu-id="9516c-161">trueString</span></span> | <span data-ttu-id="9516c-162">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-162">Bool</span></span> | <span data-ttu-id="9516c-163">True</span><span class="sxs-lookup"><span data-stu-id="9516c-163">True</span></span> |
| <span data-ttu-id="9516c-164">falseString</span><span class="sxs-lookup"><span data-stu-id="9516c-164">falseString</span></span> | <span data-ttu-id="9516c-165">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-165">Bool</span></span> | <span data-ttu-id="9516c-166">False</span><span class="sxs-lookup"><span data-stu-id="9516c-166">False</span></span> |
| <span data-ttu-id="9516c-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="9516c-167">trueInt</span></span> | <span data-ttu-id="9516c-168">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-168">Bool</span></span> | <span data-ttu-id="9516c-169">True</span><span class="sxs-lookup"><span data-stu-id="9516c-169">True</span></span> |
| <span data-ttu-id="9516c-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="9516c-170">falseInt</span></span> | <span data-ttu-id="9516c-171">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-171">Bool</span></span> | <span data-ttu-id="9516c-172">False</span><span class="sxs-lookup"><span data-stu-id="9516c-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="9516c-173">if</span><span class="sxs-lookup"><span data-stu-id="9516c-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="9516c-174">조건이 true인지 아니면 false인지에 따라 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="9516c-175">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9516c-175">Parameters</span></span>

| <span data-ttu-id="9516c-176">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-176">Parameter</span></span> | <span data-ttu-id="9516c-177">필수</span><span class="sxs-lookup"><span data-stu-id="9516c-177">Required</span></span> | <span data-ttu-id="9516c-178">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-178">Type</span></span> | <span data-ttu-id="9516c-179">설명</span><span class="sxs-lookup"><span data-stu-id="9516c-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9516c-180">condition</span><span class="sxs-lookup"><span data-stu-id="9516c-180">condition</span></span> |<span data-ttu-id="9516c-181">예</span><span class="sxs-lookup"><span data-stu-id="9516c-181">Yes</span></span> |<span data-ttu-id="9516c-182">부울</span><span class="sxs-lookup"><span data-stu-id="9516c-182">boolean</span></span> |<span data-ttu-id="9516c-183">true 일 경우 값 toocheck을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="9516c-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="9516c-184">trueValue</span></span> |<span data-ttu-id="9516c-185">예</span><span class="sxs-lookup"><span data-stu-id="9516c-185">Yes</span></span> | <span data-ttu-id="9516c-186">문자열, 정수, 개체 또는 배열</span><span class="sxs-lookup"><span data-stu-id="9516c-186">string, int, object, or array</span></span> |<span data-ttu-id="9516c-187">hello 값 tooreturn hello 조건이 true 인 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="9516c-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="9516c-188">falseValue</span></span> |<span data-ttu-id="9516c-189">예</span><span class="sxs-lookup"><span data-stu-id="9516c-189">Yes</span></span> | <span data-ttu-id="9516c-190">문자열, 정수, 개체 또는 배열</span><span class="sxs-lookup"><span data-stu-id="9516c-190">string, int, object, or array</span></span> |<span data-ttu-id="9516c-191">hello 값 tooreturn hello 조건이 false 인 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9516c-192">반환 값</span><span class="sxs-lookup"><span data-stu-id="9516c-192">Return value</span></span>

<span data-ttu-id="9516c-193">첫 번째 매개 변수가 **True**이면 두 번째 매개 변수를 반환하고 그렇지 않으면 세 번째 매개 변수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="9516c-194">설명</span><span class="sxs-lookup"><span data-stu-id="9516c-194">Remarks</span></span>

<span data-ttu-id="9516c-195">리소스 속성이 함수 tooconditionally 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="9516c-196">hello 다음 예제는 전체 서식 파일을 없지만 조건부로 hello 가용성 집합을 설정 하기 위한 hello 관련 부분을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="9516c-197">예</span><span class="sxs-lookup"><span data-stu-id="9516c-197">Examples</span></span>

<span data-ttu-id="9516c-198">hello 방법을 예제와 다음 toouse hello `if` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-198">hello following example shows how toouse hello `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="9516c-199">앞 예제는 hello hello 출력은:</span><span class="sxs-lookup"><span data-stu-id="9516c-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="9516c-200">이름</span><span class="sxs-lookup"><span data-stu-id="9516c-200">Name</span></span> | <span data-ttu-id="9516c-201">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-201">Type</span></span> | <span data-ttu-id="9516c-202">값</span><span class="sxs-lookup"><span data-stu-id="9516c-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9516c-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-203">yesOutput</span></span> | <span data-ttu-id="9516c-204">문자열</span><span class="sxs-lookup"><span data-stu-id="9516c-204">String</span></span> | <span data-ttu-id="9516c-205">yes</span><span class="sxs-lookup"><span data-stu-id="9516c-205">yes</span></span> |
| <span data-ttu-id="9516c-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-206">noOutput</span></span> | <span data-ttu-id="9516c-207">문자열</span><span class="sxs-lookup"><span data-stu-id="9516c-207">String</span></span> | <span data-ttu-id="9516c-208">no</span><span class="sxs-lookup"><span data-stu-id="9516c-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="9516c-209">not</span><span class="sxs-lookup"><span data-stu-id="9516c-209">not</span></span>
`not(arg1)`

<span data-ttu-id="9516c-210">부울 값 tooits 변환 값 반대입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9516c-211">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9516c-211">Parameters</span></span>

| <span data-ttu-id="9516c-212">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-212">Parameter</span></span> | <span data-ttu-id="9516c-213">필수</span><span class="sxs-lookup"><span data-stu-id="9516c-213">Required</span></span> | <span data-ttu-id="9516c-214">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-214">Type</span></span> | <span data-ttu-id="9516c-215">설명</span><span class="sxs-lookup"><span data-stu-id="9516c-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9516c-216">arg1</span><span class="sxs-lookup"><span data-stu-id="9516c-216">arg1</span></span> |<span data-ttu-id="9516c-217">예</span><span class="sxs-lookup"><span data-stu-id="9516c-217">Yes</span></span> |<span data-ttu-id="9516c-218">부울</span><span class="sxs-lookup"><span data-stu-id="9516c-218">boolean</span></span> |<span data-ttu-id="9516c-219">hello 값 tooconvert 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="9516c-220">반환 값</span><span class="sxs-lookup"><span data-stu-id="9516c-220">Return value</span></span>

<span data-ttu-id="9516c-221">매개 변수가 **False**이면 **True**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="9516c-222">매개 변수가 **True**이면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="9516c-223">예</span><span class="sxs-lookup"><span data-stu-id="9516c-223">Examples</span></span>

<span data-ttu-id="9516c-224">hello 방법을 예제와 다음 toouse 논리 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-224">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="9516c-225">앞 예제는 hello hello 출력은:</span><span class="sxs-lookup"><span data-stu-id="9516c-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="9516c-226">이름</span><span class="sxs-lookup"><span data-stu-id="9516c-226">Name</span></span> | <span data-ttu-id="9516c-227">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-227">Type</span></span> | <span data-ttu-id="9516c-228">값</span><span class="sxs-lookup"><span data-stu-id="9516c-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9516c-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-229">andExampleOutput</span></span> | <span data-ttu-id="9516c-230">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-230">Bool</span></span> | <span data-ttu-id="9516c-231">False</span><span class="sxs-lookup"><span data-stu-id="9516c-231">False</span></span> |
| <span data-ttu-id="9516c-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-232">orExampleOutput</span></span> | <span data-ttu-id="9516c-233">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-233">Bool</span></span> | <span data-ttu-id="9516c-234">True</span><span class="sxs-lookup"><span data-stu-id="9516c-234">True</span></span> |
| <span data-ttu-id="9516c-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-235">notExampleOutput</span></span> | <span data-ttu-id="9516c-236">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-236">Bool</span></span> | <span data-ttu-id="9516c-237">False</span><span class="sxs-lookup"><span data-stu-id="9516c-237">False</span></span> |

<span data-ttu-id="9516c-238">hello 다음 예제에서는 **하지** 와 [equals](resource-group-template-functions-comparison.md#equals)합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="9516c-239">앞 예제는 hello hello 출력은:</span><span class="sxs-lookup"><span data-stu-id="9516c-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="9516c-240">이름</span><span class="sxs-lookup"><span data-stu-id="9516c-240">Name</span></span> | <span data-ttu-id="9516c-241">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-241">Type</span></span> | <span data-ttu-id="9516c-242">값</span><span class="sxs-lookup"><span data-stu-id="9516c-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9516c-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="9516c-243">checkNotEquals</span></span> | <span data-ttu-id="9516c-244">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-244">Bool</span></span> | <span data-ttu-id="9516c-245">True</span><span class="sxs-lookup"><span data-stu-id="9516c-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="9516c-246">또는</span><span class="sxs-lookup"><span data-stu-id="9516c-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="9516c-247">매개 변수 값 중 하나가 true인지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="9516c-248">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9516c-248">Parameters</span></span>

| <span data-ttu-id="9516c-249">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-249">Parameter</span></span> | <span data-ttu-id="9516c-250">필수</span><span class="sxs-lookup"><span data-stu-id="9516c-250">Required</span></span> | <span data-ttu-id="9516c-251">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-251">Type</span></span> | <span data-ttu-id="9516c-252">설명</span><span class="sxs-lookup"><span data-stu-id="9516c-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9516c-253">arg1</span><span class="sxs-lookup"><span data-stu-id="9516c-253">arg1</span></span> |<span data-ttu-id="9516c-254">예</span><span class="sxs-lookup"><span data-stu-id="9516c-254">Yes</span></span> |<span data-ttu-id="9516c-255">부울</span><span class="sxs-lookup"><span data-stu-id="9516c-255">boolean</span></span> |<span data-ttu-id="9516c-256">첫 번째 값 toocheck 여부 hello 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="9516c-257">arg2</span><span class="sxs-lookup"><span data-stu-id="9516c-257">arg2</span></span> |<span data-ttu-id="9516c-258">예</span><span class="sxs-lookup"><span data-stu-id="9516c-258">Yes</span></span> |<span data-ttu-id="9516c-259">부울</span><span class="sxs-lookup"><span data-stu-id="9516c-259">boolean</span></span> |<span data-ttu-id="9516c-260">두 번째 값 toocheck 여부 hello 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9516c-261">반환 값</span><span class="sxs-lookup"><span data-stu-id="9516c-261">Return value</span></span>

<span data-ttu-id="9516c-262">두 값 중 하나가 true이면 **True**를 반환하고 그렇지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9516c-263">예</span><span class="sxs-lookup"><span data-stu-id="9516c-263">Examples</span></span>

<span data-ttu-id="9516c-264">hello 방법을 예제와 다음 toouse 논리 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-264">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="9516c-265">앞 예제는 hello hello 출력은:</span><span class="sxs-lookup"><span data-stu-id="9516c-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="9516c-266">이름</span><span class="sxs-lookup"><span data-stu-id="9516c-266">Name</span></span> | <span data-ttu-id="9516c-267">형식</span><span class="sxs-lookup"><span data-stu-id="9516c-267">Type</span></span> | <span data-ttu-id="9516c-268">값</span><span class="sxs-lookup"><span data-stu-id="9516c-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9516c-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-269">andExampleOutput</span></span> | <span data-ttu-id="9516c-270">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-270">Bool</span></span> | <span data-ttu-id="9516c-271">False</span><span class="sxs-lookup"><span data-stu-id="9516c-271">False</span></span> |
| <span data-ttu-id="9516c-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-272">orExampleOutput</span></span> | <span data-ttu-id="9516c-273">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-273">Bool</span></span> | <span data-ttu-id="9516c-274">True</span><span class="sxs-lookup"><span data-stu-id="9516c-274">True</span></span> |
| <span data-ttu-id="9516c-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9516c-275">notExampleOutput</span></span> | <span data-ttu-id="9516c-276">Bool</span><span class="sxs-lookup"><span data-stu-id="9516c-276">Bool</span></span> | <span data-ttu-id="9516c-277">False</span><span class="sxs-lookup"><span data-stu-id="9516c-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9516c-278">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9516c-278">Next steps</span></span>
* <span data-ttu-id="9516c-279">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9516c-280">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="9516c-281">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="9516c-282">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9516c-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

