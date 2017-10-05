---
title: "Azure Resource Manager 템플릿 함수 - 숫자 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 숫자 작업을 수행하는 데 사용할 수 있는 함수에 대해 설명합니다."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: ae0261134b8d4a934048f58d6c679a48a904950b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="60b04-103">Azure Resource Manager 템플릿용 숫자 함수</span><span class="sxs-lookup"><span data-stu-id="60b04-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="60b04-104">Resource Manager는 정수 작업을 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="60b04-105">추가</span><span class="sxs-lookup"><span data-stu-id="60b04-105">add</span></span>](#add)
* [<span data-ttu-id="60b04-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="60b04-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="60b04-107">div</span><span class="sxs-lookup"><span data-stu-id="60b04-107">div</span></span>](#div)
* [<span data-ttu-id="60b04-108">float</span><span class="sxs-lookup"><span data-stu-id="60b04-108">float</span></span>](#float)
* [<span data-ttu-id="60b04-109">int</span><span class="sxs-lookup"><span data-stu-id="60b04-109">int</span></span>](#int)
* [<span data-ttu-id="60b04-110">min</span><span class="sxs-lookup"><span data-stu-id="60b04-110">min</span></span>](#min)
* [<span data-ttu-id="60b04-111">max</span><span class="sxs-lookup"><span data-stu-id="60b04-111">max</span></span>](#max)
* [<span data-ttu-id="60b04-112">mod</span><span class="sxs-lookup"><span data-stu-id="60b04-112">mod</span></span>](#mod)
* [<span data-ttu-id="60b04-113">mul</span><span class="sxs-lookup"><span data-stu-id="60b04-113">mul</span></span>](#mul)
* [<span data-ttu-id="60b04-114">sub</span><span class="sxs-lookup"><span data-stu-id="60b04-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="60b04-115">추가</span><span class="sxs-lookup"><span data-stu-id="60b04-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="60b04-116">제공된 두 정수의 합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-117">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-117">Parameters</span></span>

| <span data-ttu-id="60b04-118">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-118">Parameter</span></span> | <span data-ttu-id="60b04-119">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-119">Required</span></span> | <span data-ttu-id="60b04-120">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-120">Type</span></span> | <span data-ttu-id="60b04-121">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="60b04-122">operand1</span><span class="sxs-lookup"><span data-stu-id="60b04-122">operand1</span></span> |<span data-ttu-id="60b04-123">예</span><span class="sxs-lookup"><span data-stu-id="60b04-123">Yes</span></span> |<span data-ttu-id="60b04-124">int</span><span class="sxs-lookup"><span data-stu-id="60b04-124">int</span></span> |<span data-ttu-id="60b04-125">더할 첫 번째 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-125">First number to add.</span></span> |
|<span data-ttu-id="60b04-126">operand2</span><span class="sxs-lookup"><span data-stu-id="60b04-126">operand2</span></span> |<span data-ttu-id="60b04-127">예</span><span class="sxs-lookup"><span data-stu-id="60b04-127">Yes</span></span> |<span data-ttu-id="60b04-128">int</span><span class="sxs-lookup"><span data-stu-id="60b04-128">int</span></span> |<span data-ttu-id="60b04-129">더할 두 번째 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-130">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-130">Return value</span></span>

<span data-ttu-id="60b04-131">매개 변수의 합계를 포함하는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-132">예</span><span class="sxs-lookup"><span data-stu-id="60b04-132">Example</span></span>

<span data-ttu-id="60b04-133">다음 예제에서는 두 개의 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-133">The following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="60b04-134">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-135">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-135">Name</span></span> | <span data-ttu-id="60b04-136">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-136">Type</span></span> | <span data-ttu-id="60b04-137">값</span><span class="sxs-lookup"><span data-stu-id="60b04-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-138">addResult</span><span class="sxs-lookup"><span data-stu-id="60b04-138">addResult</span></span> | <span data-ttu-id="60b04-139">int</span><span class="sxs-lookup"><span data-stu-id="60b04-139">Int</span></span> | <span data-ttu-id="60b04-140">8</span><span class="sxs-lookup"><span data-stu-id="60b04-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="60b04-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="60b04-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="60b04-142">반복 루프의 인덱스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-142">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="60b04-143">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-143">Parameters</span></span>

| <span data-ttu-id="60b04-144">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-144">Parameter</span></span> | <span data-ttu-id="60b04-145">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-145">Required</span></span> | <span data-ttu-id="60b04-146">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-146">Type</span></span> | <span data-ttu-id="60b04-147">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-148">loopName</span><span class="sxs-lookup"><span data-stu-id="60b04-148">loopName</span></span> | <span data-ttu-id="60b04-149">아니요</span><span class="sxs-lookup"><span data-stu-id="60b04-149">No</span></span> | <span data-ttu-id="60b04-150">string</span><span class="sxs-lookup"><span data-stu-id="60b04-150">string</span></span> | <span data-ttu-id="60b04-151">반복을 가져오기 위한 루프의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-151">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="60b04-152">offset</span><span class="sxs-lookup"><span data-stu-id="60b04-152">offset</span></span> |<span data-ttu-id="60b04-153">아니요</span><span class="sxs-lookup"><span data-stu-id="60b04-153">No</span></span> |<span data-ttu-id="60b04-154">int</span><span class="sxs-lookup"><span data-stu-id="60b04-154">int</span></span> |<span data-ttu-id="60b04-155">0부터 시작하는 반복 값에 더할 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-155">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="60b04-156">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-156">Remarks</span></span>

<span data-ttu-id="60b04-157">이 함수는 항상 **copy** 개체에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="60b04-158">**offset** 값을 제공하지 않으면 현재 반복 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-158">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="60b04-159">반복 값은 0부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-159">The iteration value starts at zero.</span></span>

<span data-ttu-id="60b04-160">**loopName** 속성을 사용하면 copyIndex에서 리소스 반복 또는 속성 반복을 참조하는지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-160">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="60b04-161">**loopName**에 값을 제공하지 않으면 현재 리소스 종류 반복이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-161">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="60b04-162">속성에서 반복하는 경우 **loopName**의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="60b04-163">**copyIndex**를 사용하는 방법의 설명은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b04-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="60b04-164">예</span><span class="sxs-lookup"><span data-stu-id="60b04-164">Example</span></span>

<span data-ttu-id="60b04-165">다음 예제에서는 복사 루프 및 이름에 포함되는 인덱스 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-165">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="60b04-166">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-166">Return value</span></span>

<span data-ttu-id="60b04-167">반복의 현재 인덱스를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-167">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="60b04-168">div</span><span class="sxs-lookup"><span data-stu-id="60b04-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="60b04-169">제공된 두 정수의 나누기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-169">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-170">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-170">Parameters</span></span>

| <span data-ttu-id="60b04-171">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-171">Parameter</span></span> | <span data-ttu-id="60b04-172">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-172">Required</span></span> | <span data-ttu-id="60b04-173">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-173">Type</span></span> | <span data-ttu-id="60b04-174">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-175">operand1</span><span class="sxs-lookup"><span data-stu-id="60b04-175">operand1</span></span> |<span data-ttu-id="60b04-176">예</span><span class="sxs-lookup"><span data-stu-id="60b04-176">Yes</span></span> |<span data-ttu-id="60b04-177">int</span><span class="sxs-lookup"><span data-stu-id="60b04-177">int</span></span> |<span data-ttu-id="60b04-178">나누어지는 수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-178">The number being divided.</span></span> |
| <span data-ttu-id="60b04-179">operand2</span><span class="sxs-lookup"><span data-stu-id="60b04-179">operand2</span></span> |<span data-ttu-id="60b04-180">예</span><span class="sxs-lookup"><span data-stu-id="60b04-180">Yes</span></span> |<span data-ttu-id="60b04-181">int</span><span class="sxs-lookup"><span data-stu-id="60b04-181">int</span></span> |<span data-ttu-id="60b04-182">나누는 데 사용되는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-182">The number that is used to divide.</span></span> <span data-ttu-id="60b04-183">0일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-184">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-184">Return value</span></span>

<span data-ttu-id="60b04-185">나누기를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-185">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-186">예</span><span class="sxs-lookup"><span data-stu-id="60b04-186">Example</span></span>

<span data-ttu-id="60b04-187">다음 예제에서는 다른 매개 변수로 매개 변수 하나를 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-187">The following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="60b04-188">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-188">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-189">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-189">Name</span></span> | <span data-ttu-id="60b04-190">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-190">Type</span></span> | <span data-ttu-id="60b04-191">값</span><span class="sxs-lookup"><span data-stu-id="60b04-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-192">divResult</span><span class="sxs-lookup"><span data-stu-id="60b04-192">divResult</span></span> | <span data-ttu-id="60b04-193">int</span><span class="sxs-lookup"><span data-stu-id="60b04-193">Int</span></span> | <span data-ttu-id="60b04-194">2</span><span class="sxs-lookup"><span data-stu-id="60b04-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="60b04-195">float</span><span class="sxs-lookup"><span data-stu-id="60b04-195">float</span></span>
`float(arg1)`

<span data-ttu-id="60b04-196">값을 부동 소수점 숫자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-196">Converts the value to a floating point number.</span></span> <span data-ttu-id="60b04-197">논리 앱과 같은 응용 프로그램에 사용자 지정 매개 변수를 전달할 때만 이 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-197">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-198">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-198">Parameters</span></span>

| <span data-ttu-id="60b04-199">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-199">Parameter</span></span> | <span data-ttu-id="60b04-200">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-200">Required</span></span> | <span data-ttu-id="60b04-201">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-201">Type</span></span> | <span data-ttu-id="60b04-202">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-203">arg1</span><span class="sxs-lookup"><span data-stu-id="60b04-203">arg1</span></span> |<span data-ttu-id="60b04-204">예</span><span class="sxs-lookup"><span data-stu-id="60b04-204">Yes</span></span> |<span data-ttu-id="60b04-205">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="60b04-205">string or int</span></span> |<span data-ttu-id="60b04-206">부동 소수점 숫자로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-206">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-207">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-207">Return value</span></span>
<span data-ttu-id="60b04-208">부동 소수점 수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-209">예</span><span class="sxs-lookup"><span data-stu-id="60b04-209">Example</span></span>

<span data-ttu-id="60b04-210">다음 예제에서는 float를 사용해서 매개 변수를 논리 앱에 전달하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-210">The following example shows how to use float to pass parameters to a Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="60b04-211">int</span><span class="sxs-lookup"><span data-stu-id="60b04-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="60b04-212">지정된 값을 정수로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-212">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-213">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-213">Parameters</span></span>

| <span data-ttu-id="60b04-214">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-214">Parameter</span></span> | <span data-ttu-id="60b04-215">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-215">Required</span></span> | <span data-ttu-id="60b04-216">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-216">Type</span></span> | <span data-ttu-id="60b04-217">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="60b04-218">valueToConvert</span></span> |<span data-ttu-id="60b04-219">예</span><span class="sxs-lookup"><span data-stu-id="60b04-219">Yes</span></span> |<span data-ttu-id="60b04-220">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="60b04-220">string or int</span></span> |<span data-ttu-id="60b04-221">정수로 변환할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-221">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-222">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-222">Return value</span></span>

<span data-ttu-id="60b04-223">변환된 값의 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-223">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-224">예</span><span class="sxs-lookup"><span data-stu-id="60b04-224">Example</span></span>

<span data-ttu-id="60b04-225">다음 예제는 사용자가 제공한 매개 변수 값을 정수로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-225">The following example converts the user-provided parameter value to integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="60b04-226">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-226">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-227">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-227">Name</span></span> | <span data-ttu-id="60b04-228">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-228">Type</span></span> | <span data-ttu-id="60b04-229">값</span><span class="sxs-lookup"><span data-stu-id="60b04-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-230">intResult</span><span class="sxs-lookup"><span data-stu-id="60b04-230">intResult</span></span> | <span data-ttu-id="60b04-231">int</span><span class="sxs-lookup"><span data-stu-id="60b04-231">Int</span></span> | <span data-ttu-id="60b04-232">4</span><span class="sxs-lookup"><span data-stu-id="60b04-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="60b04-233">min</span><span class="sxs-lookup"><span data-stu-id="60b04-233">min</span></span>
`min (arg1)`

<span data-ttu-id="60b04-234">정수 배열 또는 쉼표로 구분된 정수 목록 중에서 최소값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-234">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-235">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-235">Parameters</span></span>

| <span data-ttu-id="60b04-236">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-236">Parameter</span></span> | <span data-ttu-id="60b04-237">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-237">Required</span></span> | <span data-ttu-id="60b04-238">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-238">Type</span></span> | <span data-ttu-id="60b04-239">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-240">arg1</span><span class="sxs-lookup"><span data-stu-id="60b04-240">arg1</span></span> |<span data-ttu-id="60b04-241">예</span><span class="sxs-lookup"><span data-stu-id="60b04-241">Yes</span></span> |<span data-ttu-id="60b04-242">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="60b04-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="60b04-243">최소값을 가져올 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-243">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-244">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-244">Return value</span></span>

<span data-ttu-id="60b04-245">컬렉션의 최소값을 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-245">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-246">예</span><span class="sxs-lookup"><span data-stu-id="60b04-246">Example</span></span>

<span data-ttu-id="60b04-247">다음 예제에서는 배열 및 정소 목록에 min을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-247">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="60b04-248">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-248">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-249">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-249">Name</span></span> | <span data-ttu-id="60b04-250">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-250">Type</span></span> | <span data-ttu-id="60b04-251">값</span><span class="sxs-lookup"><span data-stu-id="60b04-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="60b04-252">arrayOutput</span></span> | <span data-ttu-id="60b04-253">int</span><span class="sxs-lookup"><span data-stu-id="60b04-253">Int</span></span> | <span data-ttu-id="60b04-254">0</span><span class="sxs-lookup"><span data-stu-id="60b04-254">0</span></span> |
| <span data-ttu-id="60b04-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="60b04-255">intOutput</span></span> | <span data-ttu-id="60b04-256">int</span><span class="sxs-lookup"><span data-stu-id="60b04-256">Int</span></span> | <span data-ttu-id="60b04-257">0</span><span class="sxs-lookup"><span data-stu-id="60b04-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="60b04-258">max</span><span class="sxs-lookup"><span data-stu-id="60b04-258">max</span></span>
`max (arg1)`

<span data-ttu-id="60b04-259">정수 배열 또는 쉼표로 구분된 정수 목록 중에서 최대값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-259">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-260">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-260">Parameters</span></span>

| <span data-ttu-id="60b04-261">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-261">Parameter</span></span> | <span data-ttu-id="60b04-262">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-262">Required</span></span> | <span data-ttu-id="60b04-263">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-263">Type</span></span> | <span data-ttu-id="60b04-264">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-265">arg1</span><span class="sxs-lookup"><span data-stu-id="60b04-265">arg1</span></span> |<span data-ttu-id="60b04-266">예</span><span class="sxs-lookup"><span data-stu-id="60b04-266">Yes</span></span> |<span data-ttu-id="60b04-267">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="60b04-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="60b04-268">최대값을 가져올 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-268">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-269">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-269">Return value</span></span>

<span data-ttu-id="60b04-270">컬렉션의 최대값을 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-270">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-271">예</span><span class="sxs-lookup"><span data-stu-id="60b04-271">Example</span></span>

<span data-ttu-id="60b04-272">다음 예제에서는 배열 및 정소 목록에 max를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-272">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="60b04-273">기본값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-273">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-274">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-274">Name</span></span> | <span data-ttu-id="60b04-275">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-275">Type</span></span> | <span data-ttu-id="60b04-276">값</span><span class="sxs-lookup"><span data-stu-id="60b04-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="60b04-277">arrayOutput</span></span> | <span data-ttu-id="60b04-278">int</span><span class="sxs-lookup"><span data-stu-id="60b04-278">Int</span></span> | <span data-ttu-id="60b04-279">5</span><span class="sxs-lookup"><span data-stu-id="60b04-279">5</span></span> |
| <span data-ttu-id="60b04-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="60b04-280">intOutput</span></span> | <span data-ttu-id="60b04-281">int</span><span class="sxs-lookup"><span data-stu-id="60b04-281">Int</span></span> | <span data-ttu-id="60b04-282">5</span><span class="sxs-lookup"><span data-stu-id="60b04-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="60b04-283">mod</span><span class="sxs-lookup"><span data-stu-id="60b04-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="60b04-284">제공된 두 정수를 사용하여 나누기한 나머지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-284">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-285">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-285">Parameters</span></span>

| <span data-ttu-id="60b04-286">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-286">Parameter</span></span> | <span data-ttu-id="60b04-287">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-287">Required</span></span> | <span data-ttu-id="60b04-288">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-288">Type</span></span> | <span data-ttu-id="60b04-289">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-290">operand1</span><span class="sxs-lookup"><span data-stu-id="60b04-290">operand1</span></span> |<span data-ttu-id="60b04-291">예</span><span class="sxs-lookup"><span data-stu-id="60b04-291">Yes</span></span> |<span data-ttu-id="60b04-292">int</span><span class="sxs-lookup"><span data-stu-id="60b04-292">int</span></span> |<span data-ttu-id="60b04-293">나누어지는 수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-293">The number being divided.</span></span> |
| <span data-ttu-id="60b04-294">operand2</span><span class="sxs-lookup"><span data-stu-id="60b04-294">operand2</span></span> |<span data-ttu-id="60b04-295">예</span><span class="sxs-lookup"><span data-stu-id="60b04-295">Yes</span></span> |<span data-ttu-id="60b04-296">int</span><span class="sxs-lookup"><span data-stu-id="60b04-296">int</span></span> |<span data-ttu-id="60b04-297">나누는 데 사용되는 정수로, 0일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-297">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-298">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-298">Return value</span></span>
<span data-ttu-id="60b04-299">나머지를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-299">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-300">예</span><span class="sxs-lookup"><span data-stu-id="60b04-300">Example</span></span>

<span data-ttu-id="60b04-301">다음 예제에서는 다른 매개 변수로 매개 변수 하나를 나눈 나머지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-301">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="60b04-302">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-302">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-303">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-303">Name</span></span> | <span data-ttu-id="60b04-304">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-304">Type</span></span> | <span data-ttu-id="60b04-305">값</span><span class="sxs-lookup"><span data-stu-id="60b04-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-306">modResult</span><span class="sxs-lookup"><span data-stu-id="60b04-306">modResult</span></span> | <span data-ttu-id="60b04-307">int</span><span class="sxs-lookup"><span data-stu-id="60b04-307">Int</span></span> | <span data-ttu-id="60b04-308">1</span><span class="sxs-lookup"><span data-stu-id="60b04-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="60b04-309">mul</span><span class="sxs-lookup"><span data-stu-id="60b04-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="60b04-310">제공된 두 정수의 곱하기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-310">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-311">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-311">Parameters</span></span>

| <span data-ttu-id="60b04-312">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-312">Parameter</span></span> | <span data-ttu-id="60b04-313">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-313">Required</span></span> | <span data-ttu-id="60b04-314">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-314">Type</span></span> | <span data-ttu-id="60b04-315">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-316">operand1</span><span class="sxs-lookup"><span data-stu-id="60b04-316">operand1</span></span> |<span data-ttu-id="60b04-317">예</span><span class="sxs-lookup"><span data-stu-id="60b04-317">Yes</span></span> |<span data-ttu-id="60b04-318">int</span><span class="sxs-lookup"><span data-stu-id="60b04-318">int</span></span> |<span data-ttu-id="60b04-319">곱할 첫 번째 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-319">First number to multiply.</span></span> |
| <span data-ttu-id="60b04-320">operand2</span><span class="sxs-lookup"><span data-stu-id="60b04-320">operand2</span></span> |<span data-ttu-id="60b04-321">예</span><span class="sxs-lookup"><span data-stu-id="60b04-321">Yes</span></span> |<span data-ttu-id="60b04-322">int</span><span class="sxs-lookup"><span data-stu-id="60b04-322">int</span></span> |<span data-ttu-id="60b04-323">곱할 두 번째 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-323">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-324">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-324">Return value</span></span>

<span data-ttu-id="60b04-325">곱하기를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-325">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-326">예</span><span class="sxs-lookup"><span data-stu-id="60b04-326">Example</span></span>

<span data-ttu-id="60b04-327">다음 예제에서는 다른 매개 변수로 매개 변수 하나를 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-327">The following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="60b04-328">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-328">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-329">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-329">Name</span></span> | <span data-ttu-id="60b04-330">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-330">Type</span></span> | <span data-ttu-id="60b04-331">값</span><span class="sxs-lookup"><span data-stu-id="60b04-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="60b04-332">mulResult</span></span> | <span data-ttu-id="60b04-333">int</span><span class="sxs-lookup"><span data-stu-id="60b04-333">Int</span></span> | <span data-ttu-id="60b04-334">15</span><span class="sxs-lookup"><span data-stu-id="60b04-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="60b04-335">sub</span><span class="sxs-lookup"><span data-stu-id="60b04-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="60b04-336">제공된 두 정수의 빼기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-336">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="60b04-337">매개 변수</span><span class="sxs-lookup"><span data-stu-id="60b04-337">Parameters</span></span>

| <span data-ttu-id="60b04-338">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-338">Parameter</span></span> | <span data-ttu-id="60b04-339">필수</span><span class="sxs-lookup"><span data-stu-id="60b04-339">Required</span></span> | <span data-ttu-id="60b04-340">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-340">Type</span></span> | <span data-ttu-id="60b04-341">설명</span><span class="sxs-lookup"><span data-stu-id="60b04-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="60b04-342">operand1</span><span class="sxs-lookup"><span data-stu-id="60b04-342">operand1</span></span> |<span data-ttu-id="60b04-343">예</span><span class="sxs-lookup"><span data-stu-id="60b04-343">Yes</span></span> |<span data-ttu-id="60b04-344">int</span><span class="sxs-lookup"><span data-stu-id="60b04-344">int</span></span> |<span data-ttu-id="60b04-345">빼는 피감수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-345">The number that is subtracted from.</span></span> |
| <span data-ttu-id="60b04-346">operand2</span><span class="sxs-lookup"><span data-stu-id="60b04-346">operand2</span></span> |<span data-ttu-id="60b04-347">예</span><span class="sxs-lookup"><span data-stu-id="60b04-347">Yes</span></span> |<span data-ttu-id="60b04-348">int</span><span class="sxs-lookup"><span data-stu-id="60b04-348">int</span></span> |<span data-ttu-id="60b04-349">빼는 감수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-349">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="60b04-350">반환 값</span><span class="sxs-lookup"><span data-stu-id="60b04-350">Return value</span></span>
<span data-ttu-id="60b04-351">빼기를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-351">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="60b04-352">예</span><span class="sxs-lookup"><span data-stu-id="60b04-352">Example</span></span>

<span data-ttu-id="60b04-353">다음 예제에서는 다른 매개 변수에서 매개 변수 하나를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-353">The following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="60b04-354">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60b04-354">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="60b04-355">이름</span><span class="sxs-lookup"><span data-stu-id="60b04-355">Name</span></span> | <span data-ttu-id="60b04-356">형식</span><span class="sxs-lookup"><span data-stu-id="60b04-356">Type</span></span> | <span data-ttu-id="60b04-357">값</span><span class="sxs-lookup"><span data-stu-id="60b04-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="60b04-358">subResult</span><span class="sxs-lookup"><span data-stu-id="60b04-358">subResult</span></span> | <span data-ttu-id="60b04-359">int</span><span class="sxs-lookup"><span data-stu-id="60b04-359">Int</span></span> | <span data-ttu-id="60b04-360">4</span><span class="sxs-lookup"><span data-stu-id="60b04-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="60b04-361">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60b04-361">Next steps</span></span>
* <span data-ttu-id="60b04-362">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b04-362">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="60b04-363">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b04-363">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="60b04-364">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b04-364">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="60b04-365">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60b04-365">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

