---
title: "aaaAzure 리소스 관리자 템플릿 함수 비교 | Microsoft Docs"
description: "Hello 함수 toouse Azure 리소스 관리자 템플릿 toocompare 값에 설명합니다."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="70607-103">Azure Resource Manager 템플릿용 비교 함수</span><span class="sxs-lookup"><span data-stu-id="70607-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="70607-104">Resource Manager는 템플릿에서 비교를 수행하기 위한 몇 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="70607-105">equals</span><span class="sxs-lookup"><span data-stu-id="70607-105">equals</span></span>](#equals)
* [<span data-ttu-id="70607-106">greater</span><span class="sxs-lookup"><span data-stu-id="70607-106">greater</span></span>](#greater)
* [<span data-ttu-id="70607-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="70607-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="70607-108">less</span><span class="sxs-lookup"><span data-stu-id="70607-108">less</span></span>](#less)
* [<span data-ttu-id="70607-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="70607-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="70607-110">equals</span><span class="sxs-lookup"><span data-stu-id="70607-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="70607-111">두 값이 서로 일치하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="70607-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="70607-112">Parameters</span></span>

| <span data-ttu-id="70607-113">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-113">Parameter</span></span> | <span data-ttu-id="70607-114">필수</span><span class="sxs-lookup"><span data-stu-id="70607-114">Required</span></span> | <span data-ttu-id="70607-115">형식</span><span class="sxs-lookup"><span data-stu-id="70607-115">Type</span></span> | <span data-ttu-id="70607-116">설명</span><span class="sxs-lookup"><span data-stu-id="70607-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70607-117">arg1</span><span class="sxs-lookup"><span data-stu-id="70607-117">arg1</span></span> |<span data-ttu-id="70607-118">예</span><span class="sxs-lookup"><span data-stu-id="70607-118">Yes</span></span> |<span data-ttu-id="70607-119">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="70607-119">int, string, array, or object</span></span> |<span data-ttu-id="70607-120">같음에 대 한 첫 번째 값 toocheck을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="70607-121">arg2</span><span class="sxs-lookup"><span data-stu-id="70607-121">arg2</span></span> |<span data-ttu-id="70607-122">예</span><span class="sxs-lookup"><span data-stu-id="70607-122">Yes</span></span> |<span data-ttu-id="70607-123">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="70607-123">int, string, array, or object</span></span> |<span data-ttu-id="70607-124">같음에 대 한 두 번째 값 toocheck을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70607-125">반환 값</span><span class="sxs-lookup"><span data-stu-id="70607-125">Return value</span></span>

<span data-ttu-id="70607-126">반환 **True** hello 값이 같고, 그렇지 않으면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="70607-127">설명</span><span class="sxs-lookup"><span data-stu-id="70607-127">Remarks</span></span>

<span data-ttu-id="70607-128">hello equals 함수는 대개 hello로 `condition` 요소 tootest 리소스 배포 되었는지 여부.</span><span class="sxs-lookup"><span data-stu-id="70607-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="70607-129">예제</span><span class="sxs-lookup"><span data-stu-id="70607-129">Example</span></span>

<span data-ttu-id="70607-130">hello 예제 서식 파일에는 다양 한 유형의 값이 같은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="70607-131">모든 hello 기본값 True를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="70607-132">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="70607-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70607-133">이름</span><span class="sxs-lookup"><span data-stu-id="70607-133">Name</span></span> | <span data-ttu-id="70607-134">형식</span><span class="sxs-lookup"><span data-stu-id="70607-134">Type</span></span> | <span data-ttu-id="70607-135">값</span><span class="sxs-lookup"><span data-stu-id="70607-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70607-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="70607-136">checkInts</span></span> | <span data-ttu-id="70607-137">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-137">Bool</span></span> | <span data-ttu-id="70607-138">True</span><span class="sxs-lookup"><span data-stu-id="70607-138">True</span></span> |
| <span data-ttu-id="70607-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70607-139">checkStrings</span></span> | <span data-ttu-id="70607-140">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-140">Bool</span></span> | <span data-ttu-id="70607-141">True</span><span class="sxs-lookup"><span data-stu-id="70607-141">True</span></span> |
| <span data-ttu-id="70607-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="70607-142">checkArrays</span></span> | <span data-ttu-id="70607-143">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-143">Bool</span></span> | <span data-ttu-id="70607-144">True</span><span class="sxs-lookup"><span data-stu-id="70607-144">True</span></span> |
| <span data-ttu-id="70607-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="70607-145">checkObjects</span></span> | <span data-ttu-id="70607-146">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-146">Bool</span></span> | <span data-ttu-id="70607-147">True</span><span class="sxs-lookup"><span data-stu-id="70607-147">True</span></span> |


<span data-ttu-id="70607-148">hello 다음 예제에서는 [하지](resource-group-template-functions-logical.md#not) 와 **equals**합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="70607-149">앞 예제는 hello hello 출력은:</span><span class="sxs-lookup"><span data-stu-id="70607-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="70607-150">이름</span><span class="sxs-lookup"><span data-stu-id="70607-150">Name</span></span> | <span data-ttu-id="70607-151">형식</span><span class="sxs-lookup"><span data-stu-id="70607-151">Type</span></span> | <span data-ttu-id="70607-152">값</span><span class="sxs-lookup"><span data-stu-id="70607-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70607-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="70607-153">checkNotEquals</span></span> | <span data-ttu-id="70607-154">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-154">Bool</span></span> | <span data-ttu-id="70607-155">True</span><span class="sxs-lookup"><span data-stu-id="70607-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="70607-156">greater</span><span class="sxs-lookup"><span data-stu-id="70607-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="70607-157">첫 번째 값 hello hello 두 번째 값 보다 큰지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70607-158">매개 변수</span><span class="sxs-lookup"><span data-stu-id="70607-158">Parameters</span></span>

| <span data-ttu-id="70607-159">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-159">Parameter</span></span> | <span data-ttu-id="70607-160">필수</span><span class="sxs-lookup"><span data-stu-id="70607-160">Required</span></span> | <span data-ttu-id="70607-161">형식</span><span class="sxs-lookup"><span data-stu-id="70607-161">Type</span></span> | <span data-ttu-id="70607-162">설명</span><span class="sxs-lookup"><span data-stu-id="70607-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70607-163">arg1</span><span class="sxs-lookup"><span data-stu-id="70607-163">arg1</span></span> |<span data-ttu-id="70607-164">예</span><span class="sxs-lookup"><span data-stu-id="70607-164">Yes</span></span> |<span data-ttu-id="70607-165">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-165">int or string</span></span> |<span data-ttu-id="70607-166">hello hello 큰 비교에 대 한 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="70607-167">arg2</span><span class="sxs-lookup"><span data-stu-id="70607-167">arg2</span></span> |<span data-ttu-id="70607-168">예</span><span class="sxs-lookup"><span data-stu-id="70607-168">Yes</span></span> |<span data-ttu-id="70607-169">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-169">int or string</span></span> |<span data-ttu-id="70607-170">hello hello 큰 비교에 대 한 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70607-171">반환 값</span><span class="sxs-lookup"><span data-stu-id="70607-171">Return value</span></span>

<span data-ttu-id="70607-172">반환 **True** hello 첫 번째 값이 고, 그렇지 않으면 hello 두 번째 값 보다 큰 경우 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70607-173">예제</span><span class="sxs-lookup"><span data-stu-id="70607-173">Example</span></span>

<span data-ttu-id="70607-174">hello 예제 템플릿 hello 하나의 값 hello 다른 보다 큰지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70607-175">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="70607-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70607-176">이름</span><span class="sxs-lookup"><span data-stu-id="70607-176">Name</span></span> | <span data-ttu-id="70607-177">형식</span><span class="sxs-lookup"><span data-stu-id="70607-177">Type</span></span> | <span data-ttu-id="70607-178">값</span><span class="sxs-lookup"><span data-stu-id="70607-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70607-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="70607-179">checkInts</span></span> | <span data-ttu-id="70607-180">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-180">Bool</span></span> | <span data-ttu-id="70607-181">False</span><span class="sxs-lookup"><span data-stu-id="70607-181">False</span></span> |
| <span data-ttu-id="70607-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70607-182">checkStrings</span></span> | <span data-ttu-id="70607-183">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-183">Bool</span></span> | <span data-ttu-id="70607-184">True</span><span class="sxs-lookup"><span data-stu-id="70607-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="70607-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="70607-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="70607-186">Hello 첫 번째 값이 둘째 값 보다 크거나 같은 toohello 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70607-187">매개 변수</span><span class="sxs-lookup"><span data-stu-id="70607-187">Parameters</span></span>

| <span data-ttu-id="70607-188">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-188">Parameter</span></span> | <span data-ttu-id="70607-189">필수</span><span class="sxs-lookup"><span data-stu-id="70607-189">Required</span></span> | <span data-ttu-id="70607-190">형식</span><span class="sxs-lookup"><span data-stu-id="70607-190">Type</span></span> | <span data-ttu-id="70607-191">설명</span><span class="sxs-lookup"><span data-stu-id="70607-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70607-192">arg1</span><span class="sxs-lookup"><span data-stu-id="70607-192">arg1</span></span> |<span data-ttu-id="70607-193">예</span><span class="sxs-lookup"><span data-stu-id="70607-193">Yes</span></span> |<span data-ttu-id="70607-194">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-194">int or string</span></span> |<span data-ttu-id="70607-195">hello hello 크거나 같음 비교에 대 한 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="70607-196">arg2</span><span class="sxs-lookup"><span data-stu-id="70607-196">arg2</span></span> |<span data-ttu-id="70607-197">예</span><span class="sxs-lookup"><span data-stu-id="70607-197">Yes</span></span> |<span data-ttu-id="70607-198">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-198">int or string</span></span> |<span data-ttu-id="70607-199">hello hello 크거나 같음 비교에 대 한 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70607-200">반환 값</span><span class="sxs-lookup"><span data-stu-id="70607-200">Return value</span></span>

<span data-ttu-id="70607-201">반환 **True** hello 첫 번째 값이 둘째 값 보다 크거나 같은 toohello; 그렇지 않으면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70607-202">예제</span><span class="sxs-lookup"><span data-stu-id="70607-202">Example</span></span>

<span data-ttu-id="70607-203">hello 예제 서식 파일 또는 다른 같은 toohello hello 하나의 값 보다 큰 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70607-204">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="70607-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70607-205">이름</span><span class="sxs-lookup"><span data-stu-id="70607-205">Name</span></span> | <span data-ttu-id="70607-206">형식</span><span class="sxs-lookup"><span data-stu-id="70607-206">Type</span></span> | <span data-ttu-id="70607-207">값</span><span class="sxs-lookup"><span data-stu-id="70607-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70607-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="70607-208">checkInts</span></span> | <span data-ttu-id="70607-209">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-209">Bool</span></span> | <span data-ttu-id="70607-210">False</span><span class="sxs-lookup"><span data-stu-id="70607-210">False</span></span> |
| <span data-ttu-id="70607-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70607-211">checkStrings</span></span> | <span data-ttu-id="70607-212">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-212">Bool</span></span> | <span data-ttu-id="70607-213">True</span><span class="sxs-lookup"><span data-stu-id="70607-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="70607-214">less</span><span class="sxs-lookup"><span data-stu-id="70607-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="70607-215">여부 hello 첫 번째 값 보다 작은 hello 두 번째 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70607-216">매개 변수</span><span class="sxs-lookup"><span data-stu-id="70607-216">Parameters</span></span>

| <span data-ttu-id="70607-217">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-217">Parameter</span></span> | <span data-ttu-id="70607-218">필수</span><span class="sxs-lookup"><span data-stu-id="70607-218">Required</span></span> | <span data-ttu-id="70607-219">형식</span><span class="sxs-lookup"><span data-stu-id="70607-219">Type</span></span> | <span data-ttu-id="70607-220">설명</span><span class="sxs-lookup"><span data-stu-id="70607-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70607-221">arg1</span><span class="sxs-lookup"><span data-stu-id="70607-221">arg1</span></span> |<span data-ttu-id="70607-222">예</span><span class="sxs-lookup"><span data-stu-id="70607-222">Yes</span></span> |<span data-ttu-id="70607-223">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-223">int or string</span></span> |<span data-ttu-id="70607-224">hello 비교 덜 hello에 대 한 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="70607-225">arg2</span><span class="sxs-lookup"><span data-stu-id="70607-225">arg2</span></span> |<span data-ttu-id="70607-226">예</span><span class="sxs-lookup"><span data-stu-id="70607-226">Yes</span></span> |<span data-ttu-id="70607-227">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-227">int or string</span></span> |<span data-ttu-id="70607-228">hello 비교 덜 hello에 대 한 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70607-229">반환 값</span><span class="sxs-lookup"><span data-stu-id="70607-229">Return value</span></span>

<span data-ttu-id="70607-230">반환 **True** hello 첫 번째 값을 사용 하면 hello 보다 작으면 두 번째 값입니다; 그렇지 않으면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70607-231">예제</span><span class="sxs-lookup"><span data-stu-id="70607-231">Example</span></span>

<span data-ttu-id="70607-232">hello 예제 템플릿 hello 하나의 값 hello 다른 보다 작은지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70607-233">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="70607-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70607-234">이름</span><span class="sxs-lookup"><span data-stu-id="70607-234">Name</span></span> | <span data-ttu-id="70607-235">형식</span><span class="sxs-lookup"><span data-stu-id="70607-235">Type</span></span> | <span data-ttu-id="70607-236">값</span><span class="sxs-lookup"><span data-stu-id="70607-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70607-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="70607-237">checkInts</span></span> | <span data-ttu-id="70607-238">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-238">Bool</span></span> | <span data-ttu-id="70607-239">True</span><span class="sxs-lookup"><span data-stu-id="70607-239">True</span></span> |
| <span data-ttu-id="70607-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70607-240">checkStrings</span></span> | <span data-ttu-id="70607-241">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-241">Bool</span></span> | <span data-ttu-id="70607-242">False</span><span class="sxs-lookup"><span data-stu-id="70607-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="70607-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="70607-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="70607-244">Hello 첫 번째 값 보다 작거나 같은 인지를 확인 toohello 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70607-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70607-245">매개 변수</span><span class="sxs-lookup"><span data-stu-id="70607-245">Parameters</span></span>

| <span data-ttu-id="70607-246">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-246">Parameter</span></span> | <span data-ttu-id="70607-247">필수</span><span class="sxs-lookup"><span data-stu-id="70607-247">Required</span></span> | <span data-ttu-id="70607-248">형식</span><span class="sxs-lookup"><span data-stu-id="70607-248">Type</span></span> | <span data-ttu-id="70607-249">설명</span><span class="sxs-lookup"><span data-stu-id="70607-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70607-250">arg1</span><span class="sxs-lookup"><span data-stu-id="70607-250">arg1</span></span> |<span data-ttu-id="70607-251">예</span><span class="sxs-lookup"><span data-stu-id="70607-251">Yes</span></span> |<span data-ttu-id="70607-252">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-252">int or string</span></span> |<span data-ttu-id="70607-253">덜 hello에 대 한 첫 번째 값 hello 또는 같음 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="70607-254">arg2</span><span class="sxs-lookup"><span data-stu-id="70607-254">arg2</span></span> |<span data-ttu-id="70607-255">예</span><span class="sxs-lookup"><span data-stu-id="70607-255">Yes</span></span> |<span data-ttu-id="70607-256">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="70607-256">int or string</span></span> |<span data-ttu-id="70607-257">hello 적은 hello에 대 한 두 번째 값 또는 같음 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70607-258">반환 값</span><span class="sxs-lookup"><span data-stu-id="70607-258">Return value</span></span>

<span data-ttu-id="70607-259">반환 **True** hello 첫 번째 값 보다 작거나 같은 경우 toohello 두 번째 값, 그렇지 않으면 **False**합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70607-260">예제</span><span class="sxs-lookup"><span data-stu-id="70607-260">Example</span></span>

<span data-ttu-id="70607-261">hello 예제 서식 파일 인지를 확인 hello 하나의 값 보다 작거나 같은 다른 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70607-262">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="70607-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70607-263">이름</span><span class="sxs-lookup"><span data-stu-id="70607-263">Name</span></span> | <span data-ttu-id="70607-264">형식</span><span class="sxs-lookup"><span data-stu-id="70607-264">Type</span></span> | <span data-ttu-id="70607-265">값</span><span class="sxs-lookup"><span data-stu-id="70607-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70607-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="70607-266">checkInts</span></span> | <span data-ttu-id="70607-267">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-267">Bool</span></span> | <span data-ttu-id="70607-268">True</span><span class="sxs-lookup"><span data-stu-id="70607-268">True</span></span> |
| <span data-ttu-id="70607-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70607-269">checkStrings</span></span> | <span data-ttu-id="70607-270">Bool</span><span class="sxs-lookup"><span data-stu-id="70607-270">Bool</span></span> | <span data-ttu-id="70607-271">False</span><span class="sxs-lookup"><span data-stu-id="70607-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="70607-272">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70607-272">Next steps</span></span>
* <span data-ttu-id="70607-273">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="70607-274">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="70607-275">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="70607-276">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70607-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

