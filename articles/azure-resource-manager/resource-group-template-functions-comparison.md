---
title: "Azure Resource Manager 템플릿 함수 - 비교 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 값을 비교하는 데 사용할 수 있는 함수에 대해 설명합니다."
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="5fdfb-103">Azure Resource Manager 템플릿용 비교 함수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="5fdfb-104">Resource Manager는 템플릿에서 비교를 수행하기 위한 몇 가지 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="5fdfb-105">equals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-105">equals</span></span>](#equals)
* [<span data-ttu-id="5fdfb-106">greater</span><span class="sxs-lookup"><span data-stu-id="5fdfb-106">greater</span></span>](#greater)
* [<span data-ttu-id="5fdfb-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="5fdfb-108">less</span><span class="sxs-lookup"><span data-stu-id="5fdfb-108">less</span></span>](#less)
* [<span data-ttu-id="5fdfb-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="5fdfb-110">equals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="5fdfb-111">두 값이 서로 일치하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="5fdfb-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-112">Parameters</span></span>

| <span data-ttu-id="5fdfb-113">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-113">Parameter</span></span> | <span data-ttu-id="5fdfb-114">필수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-114">Required</span></span> | <span data-ttu-id="5fdfb-115">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-115">Type</span></span> | <span data-ttu-id="5fdfb-116">설명</span><span class="sxs-lookup"><span data-stu-id="5fdfb-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5fdfb-117">arg1</span><span class="sxs-lookup"><span data-stu-id="5fdfb-117">arg1</span></span> |<span data-ttu-id="5fdfb-118">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-118">Yes</span></span> |<span data-ttu-id="5fdfb-119">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="5fdfb-119">int, string, array, or object</span></span> |<span data-ttu-id="5fdfb-120">같은지 확인할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="5fdfb-121">arg2</span><span class="sxs-lookup"><span data-stu-id="5fdfb-121">arg2</span></span> |<span data-ttu-id="5fdfb-122">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-122">Yes</span></span> |<span data-ttu-id="5fdfb-123">int, 문자열, 배열 또는 개체</span><span class="sxs-lookup"><span data-stu-id="5fdfb-123">int, string, array, or object</span></span> |<span data-ttu-id="5fdfb-124">같은지 확인할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5fdfb-125">반환 값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-125">Return value</span></span>

<span data-ttu-id="5fdfb-126">값이 같으면 **True**를 반환하고 같지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="5fdfb-127">설명</span><span class="sxs-lookup"><span data-stu-id="5fdfb-127">Remarks</span></span>

<span data-ttu-id="5fdfb-128">equals 함수는 종종 `condition` 요소와 함께 리소스 배포 여부를 테스트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="5fdfb-129">예제</span><span class="sxs-lookup"><span data-stu-id="5fdfb-129">Example</span></span>

<span data-ttu-id="5fdfb-130">이 예제 템플릿에서는 다른 형식의 값이 같은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="5fdfb-131">모든 기본값은 True를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-131">All the default values return True.</span></span>

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

<span data-ttu-id="5fdfb-132">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5fdfb-133">이름</span><span class="sxs-lookup"><span data-stu-id="5fdfb-133">Name</span></span> | <span data-ttu-id="5fdfb-134">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-134">Type</span></span> | <span data-ttu-id="5fdfb-135">값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5fdfb-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="5fdfb-136">checkInts</span></span> | <span data-ttu-id="5fdfb-137">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-137">Bool</span></span> | <span data-ttu-id="5fdfb-138">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-138">True</span></span> |
| <span data-ttu-id="5fdfb-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="5fdfb-139">checkStrings</span></span> | <span data-ttu-id="5fdfb-140">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-140">Bool</span></span> | <span data-ttu-id="5fdfb-141">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-141">True</span></span> |
| <span data-ttu-id="5fdfb-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="5fdfb-142">checkArrays</span></span> | <span data-ttu-id="5fdfb-143">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-143">Bool</span></span> | <span data-ttu-id="5fdfb-144">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-144">True</span></span> |
| <span data-ttu-id="5fdfb-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="5fdfb-145">checkObjects</span></span> | <span data-ttu-id="5fdfb-146">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-146">Bool</span></span> | <span data-ttu-id="5fdfb-147">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-147">True</span></span> |


<span data-ttu-id="5fdfb-148">다음 예제에서는 **equals**에 [not](resource-group-template-functions-logical.md#not)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="5fdfb-149">위 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="5fdfb-150">이름</span><span class="sxs-lookup"><span data-stu-id="5fdfb-150">Name</span></span> | <span data-ttu-id="5fdfb-151">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-151">Type</span></span> | <span data-ttu-id="5fdfb-152">값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5fdfb-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-153">checkNotEquals</span></span> | <span data-ttu-id="5fdfb-154">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-154">Bool</span></span> | <span data-ttu-id="5fdfb-155">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="5fdfb-156">greater</span><span class="sxs-lookup"><span data-stu-id="5fdfb-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="5fdfb-157">첫 번째 값이 두 번째 값보다 큰지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="5fdfb-158">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-158">Parameters</span></span>

| <span data-ttu-id="5fdfb-159">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-159">Parameter</span></span> | <span data-ttu-id="5fdfb-160">필수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-160">Required</span></span> | <span data-ttu-id="5fdfb-161">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-161">Type</span></span> | <span data-ttu-id="5fdfb-162">설명</span><span class="sxs-lookup"><span data-stu-id="5fdfb-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5fdfb-163">arg1</span><span class="sxs-lookup"><span data-stu-id="5fdfb-163">arg1</span></span> |<span data-ttu-id="5fdfb-164">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-164">Yes</span></span> |<span data-ttu-id="5fdfb-165">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-165">int or string</span></span> |<span data-ttu-id="5fdfb-166">greater 비교에 사용할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="5fdfb-167">arg2</span><span class="sxs-lookup"><span data-stu-id="5fdfb-167">arg2</span></span> |<span data-ttu-id="5fdfb-168">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-168">Yes</span></span> |<span data-ttu-id="5fdfb-169">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-169">int or string</span></span> |<span data-ttu-id="5fdfb-170">greater 비교에 사용할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5fdfb-171">반환 값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-171">Return value</span></span>

<span data-ttu-id="5fdfb-172">첫 번째 값이 두 번째 값보다 크면 **True**를 반환하고 크지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="5fdfb-173">예제</span><span class="sxs-lookup"><span data-stu-id="5fdfb-173">Example</span></span>

<span data-ttu-id="5fdfb-174">이 예제 템플릿에서는 한 값이 다른 값보다 큰지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-174">The example template checks whether the one value is greater than the other.</span></span>

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

<span data-ttu-id="5fdfb-175">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5fdfb-176">이름</span><span class="sxs-lookup"><span data-stu-id="5fdfb-176">Name</span></span> | <span data-ttu-id="5fdfb-177">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-177">Type</span></span> | <span data-ttu-id="5fdfb-178">값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5fdfb-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="5fdfb-179">checkInts</span></span> | <span data-ttu-id="5fdfb-180">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-180">Bool</span></span> | <span data-ttu-id="5fdfb-181">False</span><span class="sxs-lookup"><span data-stu-id="5fdfb-181">False</span></span> |
| <span data-ttu-id="5fdfb-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="5fdfb-182">checkStrings</span></span> | <span data-ttu-id="5fdfb-183">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-183">Bool</span></span> | <span data-ttu-id="5fdfb-184">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="5fdfb-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="5fdfb-186">첫 번째 값이 두 번째 값보다 크거나 같은지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="5fdfb-187">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-187">Parameters</span></span>

| <span data-ttu-id="5fdfb-188">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-188">Parameter</span></span> | <span data-ttu-id="5fdfb-189">필수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-189">Required</span></span> | <span data-ttu-id="5fdfb-190">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-190">Type</span></span> | <span data-ttu-id="5fdfb-191">설명</span><span class="sxs-lookup"><span data-stu-id="5fdfb-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5fdfb-192">arg1</span><span class="sxs-lookup"><span data-stu-id="5fdfb-192">arg1</span></span> |<span data-ttu-id="5fdfb-193">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-193">Yes</span></span> |<span data-ttu-id="5fdfb-194">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-194">int or string</span></span> |<span data-ttu-id="5fdfb-195">greater 또는 equal 비교에 사용할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="5fdfb-196">arg2</span><span class="sxs-lookup"><span data-stu-id="5fdfb-196">arg2</span></span> |<span data-ttu-id="5fdfb-197">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-197">Yes</span></span> |<span data-ttu-id="5fdfb-198">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-198">int or string</span></span> |<span data-ttu-id="5fdfb-199">greater 또는 equal 비교에 사용할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5fdfb-200">반환 값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-200">Return value</span></span>

<span data-ttu-id="5fdfb-201">첫 번째 값이 두 번째 값보다 크거나 같으면 **True**를 반환하고 작으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="5fdfb-202">예제</span><span class="sxs-lookup"><span data-stu-id="5fdfb-202">Example</span></span>

<span data-ttu-id="5fdfb-203">이 예제 템플릿에서는 한 값이 다른 값보다 크거나 같은지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

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

<span data-ttu-id="5fdfb-204">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5fdfb-205">이름</span><span class="sxs-lookup"><span data-stu-id="5fdfb-205">Name</span></span> | <span data-ttu-id="5fdfb-206">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-206">Type</span></span> | <span data-ttu-id="5fdfb-207">값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5fdfb-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="5fdfb-208">checkInts</span></span> | <span data-ttu-id="5fdfb-209">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-209">Bool</span></span> | <span data-ttu-id="5fdfb-210">False</span><span class="sxs-lookup"><span data-stu-id="5fdfb-210">False</span></span> |
| <span data-ttu-id="5fdfb-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="5fdfb-211">checkStrings</span></span> | <span data-ttu-id="5fdfb-212">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-212">Bool</span></span> | <span data-ttu-id="5fdfb-213">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="5fdfb-214">less</span><span class="sxs-lookup"><span data-stu-id="5fdfb-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="5fdfb-215">첫 번째 값이 두 번째 값보다 작은지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="5fdfb-216">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-216">Parameters</span></span>

| <span data-ttu-id="5fdfb-217">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-217">Parameter</span></span> | <span data-ttu-id="5fdfb-218">필수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-218">Required</span></span> | <span data-ttu-id="5fdfb-219">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-219">Type</span></span> | <span data-ttu-id="5fdfb-220">설명</span><span class="sxs-lookup"><span data-stu-id="5fdfb-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5fdfb-221">arg1</span><span class="sxs-lookup"><span data-stu-id="5fdfb-221">arg1</span></span> |<span data-ttu-id="5fdfb-222">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-222">Yes</span></span> |<span data-ttu-id="5fdfb-223">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-223">int or string</span></span> |<span data-ttu-id="5fdfb-224">less 비교에 사용할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="5fdfb-225">arg2</span><span class="sxs-lookup"><span data-stu-id="5fdfb-225">arg2</span></span> |<span data-ttu-id="5fdfb-226">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-226">Yes</span></span> |<span data-ttu-id="5fdfb-227">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-227">int or string</span></span> |<span data-ttu-id="5fdfb-228">less 비교에 사용할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5fdfb-229">반환 값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-229">Return value</span></span>

<span data-ttu-id="5fdfb-230">첫 번째 값이 두 번째 값보다 작으면 **True**를 반환하고 작지 않으면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="5fdfb-231">예제</span><span class="sxs-lookup"><span data-stu-id="5fdfb-231">Example</span></span>

<span data-ttu-id="5fdfb-232">이 예제 템플릿에서는 한 값이 다른 값보다 작은지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-232">The example template checks whether the one value is less than the other.</span></span>

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

<span data-ttu-id="5fdfb-233">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5fdfb-234">이름</span><span class="sxs-lookup"><span data-stu-id="5fdfb-234">Name</span></span> | <span data-ttu-id="5fdfb-235">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-235">Type</span></span> | <span data-ttu-id="5fdfb-236">값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5fdfb-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="5fdfb-237">checkInts</span></span> | <span data-ttu-id="5fdfb-238">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-238">Bool</span></span> | <span data-ttu-id="5fdfb-239">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-239">True</span></span> |
| <span data-ttu-id="5fdfb-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="5fdfb-240">checkStrings</span></span> | <span data-ttu-id="5fdfb-241">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-241">Bool</span></span> | <span data-ttu-id="5fdfb-242">False</span><span class="sxs-lookup"><span data-stu-id="5fdfb-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="5fdfb-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="5fdfb-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="5fdfb-244">첫 번째 값이 두 번째 값보다 작거나 같은지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="5fdfb-245">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-245">Parameters</span></span>

| <span data-ttu-id="5fdfb-246">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-246">Parameter</span></span> | <span data-ttu-id="5fdfb-247">필수</span><span class="sxs-lookup"><span data-stu-id="5fdfb-247">Required</span></span> | <span data-ttu-id="5fdfb-248">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-248">Type</span></span> | <span data-ttu-id="5fdfb-249">설명</span><span class="sxs-lookup"><span data-stu-id="5fdfb-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5fdfb-250">arg1</span><span class="sxs-lookup"><span data-stu-id="5fdfb-250">arg1</span></span> |<span data-ttu-id="5fdfb-251">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-251">Yes</span></span> |<span data-ttu-id="5fdfb-252">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-252">int or string</span></span> |<span data-ttu-id="5fdfb-253">less 또는 equals 비교에 사용할 첫 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="5fdfb-254">arg2</span><span class="sxs-lookup"><span data-stu-id="5fdfb-254">arg2</span></span> |<span data-ttu-id="5fdfb-255">예</span><span class="sxs-lookup"><span data-stu-id="5fdfb-255">Yes</span></span> |<span data-ttu-id="5fdfb-256">int 또는 문자열</span><span class="sxs-lookup"><span data-stu-id="5fdfb-256">int or string</span></span> |<span data-ttu-id="5fdfb-257">less 또는 equals 비교에 사용할 두 번째 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5fdfb-258">반환 값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-258">Return value</span></span>

<span data-ttu-id="5fdfb-259">첫 번째 값이 두 번째 값보다 작거나 같으면 **True**를 반환하고 크면 **False**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="5fdfb-260">예제</span><span class="sxs-lookup"><span data-stu-id="5fdfb-260">Example</span></span>

<span data-ttu-id="5fdfb-261">이 예제 템플릿에서는 한 값이 다른 값보다 작거나 같은지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-261">The example template checks whether the one value is less than or equal to the other.</span></span>

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

<span data-ttu-id="5fdfb-262">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5fdfb-263">이름</span><span class="sxs-lookup"><span data-stu-id="5fdfb-263">Name</span></span> | <span data-ttu-id="5fdfb-264">형식</span><span class="sxs-lookup"><span data-stu-id="5fdfb-264">Type</span></span> | <span data-ttu-id="5fdfb-265">값</span><span class="sxs-lookup"><span data-stu-id="5fdfb-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5fdfb-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="5fdfb-266">checkInts</span></span> | <span data-ttu-id="5fdfb-267">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-267">Bool</span></span> | <span data-ttu-id="5fdfb-268">True</span><span class="sxs-lookup"><span data-stu-id="5fdfb-268">True</span></span> |
| <span data-ttu-id="5fdfb-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="5fdfb-269">checkStrings</span></span> | <span data-ttu-id="5fdfb-270">Bool</span><span class="sxs-lookup"><span data-stu-id="5fdfb-270">Bool</span></span> | <span data-ttu-id="5fdfb-271">False</span><span class="sxs-lookup"><span data-stu-id="5fdfb-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="5fdfb-272">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fdfb-272">Next steps</span></span>
* <span data-ttu-id="5fdfb-273">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5fdfb-274">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="5fdfb-275">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="5fdfb-276">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fdfb-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

