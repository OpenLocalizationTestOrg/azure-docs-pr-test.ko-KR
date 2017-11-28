---
title: "aaaAzure 리소스 관리자 템플릿 함수-숫자 | Microsoft Docs"
description: "번호가 있는 hello 함수 toouse Azure 리소스 관리자 템플릿 toowork에 설명합니다."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="ac649-103">Azure Resource Manager 템플릿용 숫자 함수</span><span class="sxs-lookup"><span data-stu-id="ac649-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="ac649-104">리소스 관리자 hello를 뒤 정수가 포함 된 작업에 대 한 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="ac649-105">추가</span><span class="sxs-lookup"><span data-stu-id="ac649-105">add</span></span>](#add)
* [<span data-ttu-id="ac649-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="ac649-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="ac649-107">div</span><span class="sxs-lookup"><span data-stu-id="ac649-107">div</span></span>](#div)
* [<span data-ttu-id="ac649-108">float</span><span class="sxs-lookup"><span data-stu-id="ac649-108">float</span></span>](#float)
* [<span data-ttu-id="ac649-109">int</span><span class="sxs-lookup"><span data-stu-id="ac649-109">int</span></span>](#int)
* [<span data-ttu-id="ac649-110">min</span><span class="sxs-lookup"><span data-stu-id="ac649-110">min</span></span>](#min)
* [<span data-ttu-id="ac649-111">max</span><span class="sxs-lookup"><span data-stu-id="ac649-111">max</span></span>](#max)
* [<span data-ttu-id="ac649-112">mod</span><span class="sxs-lookup"><span data-stu-id="ac649-112">mod</span></span>](#mod)
* [<span data-ttu-id="ac649-113">mul</span><span class="sxs-lookup"><span data-stu-id="ac649-113">mul</span></span>](#mul)
* [<span data-ttu-id="ac649-114">sub</span><span class="sxs-lookup"><span data-stu-id="ac649-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="ac649-115">추가</span><span class="sxs-lookup"><span data-stu-id="ac649-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="ac649-116">반환 hello hello 두 제공 된 정수의 합입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-117">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-117">Parameters</span></span>

| <span data-ttu-id="ac649-118">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-118">Parameter</span></span> | <span data-ttu-id="ac649-119">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-119">Required</span></span> | <span data-ttu-id="ac649-120">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-120">Type</span></span> | <span data-ttu-id="ac649-121">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="ac649-122">operand1</span><span class="sxs-lookup"><span data-stu-id="ac649-122">operand1</span></span> |<span data-ttu-id="ac649-123">예</span><span class="sxs-lookup"><span data-stu-id="ac649-123">Yes</span></span> |<span data-ttu-id="ac649-124">int</span><span class="sxs-lookup"><span data-stu-id="ac649-124">int</span></span> |<span data-ttu-id="ac649-125">첫 번째 숫자 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-125">First number tooadd.</span></span> |
|<span data-ttu-id="ac649-126">operand2</span><span class="sxs-lookup"><span data-stu-id="ac649-126">operand2</span></span> |<span data-ttu-id="ac649-127">예</span><span class="sxs-lookup"><span data-stu-id="ac649-127">Yes</span></span> |<span data-ttu-id="ac649-128">int</span><span class="sxs-lookup"><span data-stu-id="ac649-128">int</span></span> |<span data-ttu-id="ac649-129">두 번째 숫자 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-130">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-130">Return value</span></span>

<span data-ttu-id="ac649-131">Hello 매개 변수의 hello 합계를 포함 하는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-132">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-132">Example</span></span>

<span data-ttu-id="ac649-133">다음 예제는 hello 두 개의 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
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

<span data-ttu-id="ac649-134">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-135">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-135">Name</span></span> | <span data-ttu-id="ac649-136">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-136">Type</span></span> | <span data-ttu-id="ac649-137">값</span><span class="sxs-lookup"><span data-stu-id="ac649-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-138">addResult</span><span class="sxs-lookup"><span data-stu-id="ac649-138">addResult</span></span> | <span data-ttu-id="ac649-139">int</span><span class="sxs-lookup"><span data-stu-id="ac649-139">Int</span></span> | <span data-ttu-id="ac649-140">8</span><span class="sxs-lookup"><span data-stu-id="ac649-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="ac649-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="ac649-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="ac649-142">반환 hello 반복 루프의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="ac649-143">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-143">Parameters</span></span>

| <span data-ttu-id="ac649-144">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-144">Parameter</span></span> | <span data-ttu-id="ac649-145">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-145">Required</span></span> | <span data-ttu-id="ac649-146">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-146">Type</span></span> | <span data-ttu-id="ac649-147">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-148">loopName</span><span class="sxs-lookup"><span data-stu-id="ac649-148">loopName</span></span> | <span data-ttu-id="ac649-149">아니요</span><span class="sxs-lookup"><span data-stu-id="ac649-149">No</span></span> | <span data-ttu-id="ac649-150">string</span><span class="sxs-lookup"><span data-stu-id="ac649-150">string</span></span> | <span data-ttu-id="ac649-151">hello 반복을 가져오기 위한 hello 루프의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="ac649-152">offset</span><span class="sxs-lookup"><span data-stu-id="ac649-152">offset</span></span> |<span data-ttu-id="ac649-153">아니요</span><span class="sxs-lookup"><span data-stu-id="ac649-153">No</span></span> |<span data-ttu-id="ac649-154">int</span><span class="sxs-lookup"><span data-stu-id="ac649-154">int</span></span> |<span data-ttu-id="ac649-155">hello 숫자 tooadd toohello 0부터 시작 하는 반복 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="ac649-156">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-156">Remarks</span></span>

<span data-ttu-id="ac649-157">이 함수는 항상 **copy** 개체에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="ac649-158">에 값이 제공 하는 경우 **오프셋**, hello 현재 반복 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="ac649-159">hello 반복 값이 0에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="ac649-160">hello **loopName** 속성 하면 toospecify copyIndex 참조 tooa 리소스 반복 또는 속성 반복 여부.</span><span class="sxs-lookup"><span data-stu-id="ac649-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="ac649-161">에 값이 제공 하는 경우 **loopName**, hello 현재 리소스 형식을 반복 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="ac649-162">속성에서 반복하는 경우 **loopName**의 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="ac649-163">**copyIndex**를 사용하는 방법의 설명은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac649-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="ac649-164">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-164">Example</span></span>

<span data-ttu-id="ac649-165">hello 다음 예제에서는 hello 이름에 포함 된 복사 루프 및 hello 인덱스 값</span><span class="sxs-lookup"><span data-stu-id="ac649-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="ac649-166">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-166">Return value</span></span>

<span data-ttu-id="ac649-167">Hello 반복의 hello 현재 인덱스를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="ac649-168">div</span><span class="sxs-lookup"><span data-stu-id="ac649-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="ac649-169">반환 hello hello 두 제공 된 정수의 정수 나누기입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-170">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-170">Parameters</span></span>

| <span data-ttu-id="ac649-171">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-171">Parameter</span></span> | <span data-ttu-id="ac649-172">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-172">Required</span></span> | <span data-ttu-id="ac649-173">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-173">Type</span></span> | <span data-ttu-id="ac649-174">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-175">operand1</span><span class="sxs-lookup"><span data-stu-id="ac649-175">operand1</span></span> |<span data-ttu-id="ac649-176">예</span><span class="sxs-lookup"><span data-stu-id="ac649-176">Yes</span></span> |<span data-ttu-id="ac649-177">int</span><span class="sxs-lookup"><span data-stu-id="ac649-177">int</span></span> |<span data-ttu-id="ac649-178">나누어 사용 하는 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-178">hello number being divided.</span></span> |
| <span data-ttu-id="ac649-179">operand2</span><span class="sxs-lookup"><span data-stu-id="ac649-179">operand2</span></span> |<span data-ttu-id="ac649-180">예</span><span class="sxs-lookup"><span data-stu-id="ac649-180">Yes</span></span> |<span data-ttu-id="ac649-181">int</span><span class="sxs-lookup"><span data-stu-id="ac649-181">int</span></span> |<span data-ttu-id="ac649-182">hello 숫자 사용된 toodivide입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-182">hello number that is used toodivide.</span></span> <span data-ttu-id="ac649-183">0일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-184">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-184">Return value</span></span>

<span data-ttu-id="ac649-185">정수 나타내는 hello 나누기입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-186">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-186">Example</span></span>

<span data-ttu-id="ac649-187">다음 예제는 hello 다른 매개 변수에서 매개 변수 하나를 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-187">hello following example divides one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="ac649-188">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-189">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-189">Name</span></span> | <span data-ttu-id="ac649-190">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-190">Type</span></span> | <span data-ttu-id="ac649-191">값</span><span class="sxs-lookup"><span data-stu-id="ac649-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-192">divResult</span><span class="sxs-lookup"><span data-stu-id="ac649-192">divResult</span></span> | <span data-ttu-id="ac649-193">int</span><span class="sxs-lookup"><span data-stu-id="ac649-193">Int</span></span> | <span data-ttu-id="ac649-194">2</span><span class="sxs-lookup"><span data-stu-id="ac649-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="ac649-195">float</span><span class="sxs-lookup"><span data-stu-id="ac649-195">float</span></span>
`float(arg1)`

<span data-ttu-id="ac649-196">Hello 값 tooa 부동 소수점 숫자로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="ac649-197">논리 앱 같은 tooan 응용 프로그램을 사용자 지정 매개 변수를 전달할 때만이 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-198">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-198">Parameters</span></span>

| <span data-ttu-id="ac649-199">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-199">Parameter</span></span> | <span data-ttu-id="ac649-200">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-200">Required</span></span> | <span data-ttu-id="ac649-201">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-201">Type</span></span> | <span data-ttu-id="ac649-202">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-203">arg1</span><span class="sxs-lookup"><span data-stu-id="ac649-203">arg1</span></span> |<span data-ttu-id="ac649-204">예</span><span class="sxs-lookup"><span data-stu-id="ac649-204">Yes</span></span> |<span data-ttu-id="ac649-205">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="ac649-205">string or int</span></span> |<span data-ttu-id="ac649-206">hello 값 tooconvert tooa 부동 소수점 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-207">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-207">Return value</span></span>
<span data-ttu-id="ac649-208">부동 소수점 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-209">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-209">Example</span></span>

<span data-ttu-id="ac649-210">다음 예제는 hello toouse toopass 매개 변수 tooa 논리 앱을 배치 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="ac649-211">int</span><span class="sxs-lookup"><span data-stu-id="ac649-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="ac649-212">지정 된 값 tooan 정수 hello 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-213">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-213">Parameters</span></span>

| <span data-ttu-id="ac649-214">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-214">Parameter</span></span> | <span data-ttu-id="ac649-215">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-215">Required</span></span> | <span data-ttu-id="ac649-216">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-216">Type</span></span> | <span data-ttu-id="ac649-217">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="ac649-218">valueToConvert</span></span> |<span data-ttu-id="ac649-219">예</span><span class="sxs-lookup"><span data-stu-id="ac649-219">Yes</span></span> |<span data-ttu-id="ac649-220">문자열 또는 int</span><span class="sxs-lookup"><span data-stu-id="ac649-220">string or int</span></span> |<span data-ttu-id="ac649-221">hello tooconvert tooan 정수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-222">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-222">Return value</span></span>

<span data-ttu-id="ac649-223">Hello의 정수 값을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-224">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-224">Example</span></span>

<span data-ttu-id="ac649-225">hello 다음 예제에서는 변환 hello 사용자가 제공한 매개 변수 값 toointeger 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

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

<span data-ttu-id="ac649-226">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-227">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-227">Name</span></span> | <span data-ttu-id="ac649-228">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-228">Type</span></span> | <span data-ttu-id="ac649-229">값</span><span class="sxs-lookup"><span data-stu-id="ac649-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-230">intResult</span><span class="sxs-lookup"><span data-stu-id="ac649-230">intResult</span></span> | <span data-ttu-id="ac649-231">int</span><span class="sxs-lookup"><span data-stu-id="ac649-231">Int</span></span> | <span data-ttu-id="ac649-232">4</span><span class="sxs-lookup"><span data-stu-id="ac649-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="ac649-233">Min</span><span class="sxs-lookup"><span data-stu-id="ac649-233">min</span></span>
`min (arg1)`

<span data-ttu-id="ac649-234">반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최소 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-235">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-235">Parameters</span></span>

| <span data-ttu-id="ac649-236">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-236">Parameter</span></span> | <span data-ttu-id="ac649-237">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-237">Required</span></span> | <span data-ttu-id="ac649-238">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-238">Type</span></span> | <span data-ttu-id="ac649-239">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-240">arg1</span><span class="sxs-lookup"><span data-stu-id="ac649-240">arg1</span></span> |<span data-ttu-id="ac649-241">예</span><span class="sxs-lookup"><span data-stu-id="ac649-241">Yes</span></span> |<span data-ttu-id="ac649-242">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="ac649-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="ac649-243">hello 컬렉션 tooget hello 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-244">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-244">Return value</span></span>

<span data-ttu-id="ac649-245">Hello 컬렉션에서 최소 값을 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-246">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-246">Example</span></span>

<span data-ttu-id="ac649-247">hello 방법을 예제와 다음 toouse min 배열 및 정수 목록:</span><span class="sxs-lookup"><span data-stu-id="ac649-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="ac649-248">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-249">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-249">Name</span></span> | <span data-ttu-id="ac649-250">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-250">Type</span></span> | <span data-ttu-id="ac649-251">값</span><span class="sxs-lookup"><span data-stu-id="ac649-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="ac649-252">arrayOutput</span></span> | <span data-ttu-id="ac649-253">int</span><span class="sxs-lookup"><span data-stu-id="ac649-253">Int</span></span> | <span data-ttu-id="ac649-254">0</span><span class="sxs-lookup"><span data-stu-id="ac649-254">0</span></span> |
| <span data-ttu-id="ac649-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="ac649-255">intOutput</span></span> | <span data-ttu-id="ac649-256">int</span><span class="sxs-lookup"><span data-stu-id="ac649-256">Int</span></span> | <span data-ttu-id="ac649-257">0</span><span class="sxs-lookup"><span data-stu-id="ac649-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="ac649-258">max</span><span class="sxs-lookup"><span data-stu-id="ac649-258">max</span></span>
`max (arg1)`

<span data-ttu-id="ac649-259">반환 hello 정수 배열 또는 정수 쉼표로 구분 된 목록에서 최대 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-260">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-260">Parameters</span></span>

| <span data-ttu-id="ac649-261">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-261">Parameter</span></span> | <span data-ttu-id="ac649-262">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-262">Required</span></span> | <span data-ttu-id="ac649-263">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-263">Type</span></span> | <span data-ttu-id="ac649-264">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-265">arg1</span><span class="sxs-lookup"><span data-stu-id="ac649-265">arg1</span></span> |<span data-ttu-id="ac649-266">예</span><span class="sxs-lookup"><span data-stu-id="ac649-266">Yes</span></span> |<span data-ttu-id="ac649-267">정수 배열 또는 쉼표로 구분된 정수 목록</span><span class="sxs-lookup"><span data-stu-id="ac649-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="ac649-268">hello 컬렉션 tooget hello 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-269">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-269">Return value</span></span>

<span data-ttu-id="ac649-270">Hello 컬렉션에서 hello 최 댓 값을 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-271">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-271">Example</span></span>

<span data-ttu-id="ac649-272">hello 방법을 예제와 다음 toouse 배열 및 정수 목록이 사용 하 여 최대:</span><span class="sxs-lookup"><span data-stu-id="ac649-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="ac649-273">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-274">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-274">Name</span></span> | <span data-ttu-id="ac649-275">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-275">Type</span></span> | <span data-ttu-id="ac649-276">값</span><span class="sxs-lookup"><span data-stu-id="ac649-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="ac649-277">arrayOutput</span></span> | <span data-ttu-id="ac649-278">int</span><span class="sxs-lookup"><span data-stu-id="ac649-278">Int</span></span> | <span data-ttu-id="ac649-279">5</span><span class="sxs-lookup"><span data-stu-id="ac649-279">5</span></span> |
| <span data-ttu-id="ac649-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="ac649-280">intOutput</span></span> | <span data-ttu-id="ac649-281">int</span><span class="sxs-lookup"><span data-stu-id="ac649-281">Int</span></span> | <span data-ttu-id="ac649-282">5</span><span class="sxs-lookup"><span data-stu-id="ac649-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="ac649-283">mod</span><span class="sxs-lookup"><span data-stu-id="ac649-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="ac649-284">제공 된 정수 두 개 hello를 사용 하 여 hello 정수 나누기의 hello 나머지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-285">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-285">Parameters</span></span>

| <span data-ttu-id="ac649-286">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-286">Parameter</span></span> | <span data-ttu-id="ac649-287">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-287">Required</span></span> | <span data-ttu-id="ac649-288">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-288">Type</span></span> | <span data-ttu-id="ac649-289">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-290">operand1</span><span class="sxs-lookup"><span data-stu-id="ac649-290">operand1</span></span> |<span data-ttu-id="ac649-291">예</span><span class="sxs-lookup"><span data-stu-id="ac649-291">Yes</span></span> |<span data-ttu-id="ac649-292">int</span><span class="sxs-lookup"><span data-stu-id="ac649-292">int</span></span> |<span data-ttu-id="ac649-293">나누어 사용 하는 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-293">hello number being divided.</span></span> |
| <span data-ttu-id="ac649-294">operand2</span><span class="sxs-lookup"><span data-stu-id="ac649-294">operand2</span></span> |<span data-ttu-id="ac649-295">예</span><span class="sxs-lookup"><span data-stu-id="ac649-295">Yes</span></span> |<span data-ttu-id="ac649-296">int</span><span class="sxs-lookup"><span data-stu-id="ac649-296">int</span></span> |<span data-ttu-id="ac649-297">hello를 사용 하는 toodivide 0 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-298">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-298">Return value</span></span>
<span data-ttu-id="ac649-299">정수 나타내는 hello 나머지입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-300">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-300">Example</span></span>

<span data-ttu-id="ac649-301">hello 다음 예제에서는 반환 hello 나눈 나머지를 다른 매개 변수는 하나의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="ac649-302">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-303">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-303">Name</span></span> | <span data-ttu-id="ac649-304">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-304">Type</span></span> | <span data-ttu-id="ac649-305">값</span><span class="sxs-lookup"><span data-stu-id="ac649-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-306">modResult</span><span class="sxs-lookup"><span data-stu-id="ac649-306">modResult</span></span> | <span data-ttu-id="ac649-307">int</span><span class="sxs-lookup"><span data-stu-id="ac649-307">Int</span></span> | <span data-ttu-id="ac649-308">1</span><span class="sxs-lookup"><span data-stu-id="ac649-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="ac649-309">mul</span><span class="sxs-lookup"><span data-stu-id="ac649-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="ac649-310">반환 hello hello 두 제공 된 정수의 곱입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-311">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-311">Parameters</span></span>

| <span data-ttu-id="ac649-312">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-312">Parameter</span></span> | <span data-ttu-id="ac649-313">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-313">Required</span></span> | <span data-ttu-id="ac649-314">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-314">Type</span></span> | <span data-ttu-id="ac649-315">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-316">operand1</span><span class="sxs-lookup"><span data-stu-id="ac649-316">operand1</span></span> |<span data-ttu-id="ac649-317">예</span><span class="sxs-lookup"><span data-stu-id="ac649-317">Yes</span></span> |<span data-ttu-id="ac649-318">int</span><span class="sxs-lookup"><span data-stu-id="ac649-318">int</span></span> |<span data-ttu-id="ac649-319">첫 번째 숫자 toomultiply 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-319">First number toomultiply.</span></span> |
| <span data-ttu-id="ac649-320">operand2</span><span class="sxs-lookup"><span data-stu-id="ac649-320">operand2</span></span> |<span data-ttu-id="ac649-321">예</span><span class="sxs-lookup"><span data-stu-id="ac649-321">Yes</span></span> |<span data-ttu-id="ac649-322">int</span><span class="sxs-lookup"><span data-stu-id="ac649-322">int</span></span> |<span data-ttu-id="ac649-323">두 번째 숫자 toomultiply 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-324">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-324">Return value</span></span>

<span data-ttu-id="ac649-325">정수 나타내는 hello 곱하기.</span><span class="sxs-lookup"><span data-stu-id="ac649-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-326">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-326">Example</span></span>

<span data-ttu-id="ac649-327">다음 예제는 hello 다른 매개 변수에서 매개 변수 하나를 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
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

<span data-ttu-id="ac649-328">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-329">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-329">Name</span></span> | <span data-ttu-id="ac649-330">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-330">Type</span></span> | <span data-ttu-id="ac649-331">값</span><span class="sxs-lookup"><span data-stu-id="ac649-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="ac649-332">mulResult</span></span> | <span data-ttu-id="ac649-333">int</span><span class="sxs-lookup"><span data-stu-id="ac649-333">Int</span></span> | <span data-ttu-id="ac649-334">15</span><span class="sxs-lookup"><span data-stu-id="ac649-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="ac649-335">sub</span><span class="sxs-lookup"><span data-stu-id="ac649-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="ac649-336">반환 hello 빼기 hello 두 개의 제공 된 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="ac649-337">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac649-337">Parameters</span></span>

| <span data-ttu-id="ac649-338">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-338">Parameter</span></span> | <span data-ttu-id="ac649-339">필수</span><span class="sxs-lookup"><span data-stu-id="ac649-339">Required</span></span> | <span data-ttu-id="ac649-340">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-340">Type</span></span> | <span data-ttu-id="ac649-341">설명</span><span class="sxs-lookup"><span data-stu-id="ac649-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ac649-342">operand1</span><span class="sxs-lookup"><span data-stu-id="ac649-342">operand1</span></span> |<span data-ttu-id="ac649-343">예</span><span class="sxs-lookup"><span data-stu-id="ac649-343">Yes</span></span> |<span data-ttu-id="ac649-344">int</span><span class="sxs-lookup"><span data-stu-id="ac649-344">int</span></span> |<span data-ttu-id="ac649-345">hello 숫자에서 뺀입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="ac649-346">operand2</span><span class="sxs-lookup"><span data-stu-id="ac649-346">operand2</span></span> |<span data-ttu-id="ac649-347">예</span><span class="sxs-lookup"><span data-stu-id="ac649-347">Yes</span></span> |<span data-ttu-id="ac649-348">int</span><span class="sxs-lookup"><span data-stu-id="ac649-348">int</span></span> |<span data-ttu-id="ac649-349">hello 숫자를 뺀입니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ac649-350">반환 값</span><span class="sxs-lookup"><span data-stu-id="ac649-350">Return value</span></span>
<span data-ttu-id="ac649-351">정수 나타내는 hello 빼기 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="ac649-352">예제</span><span class="sxs-lookup"><span data-stu-id="ac649-352">Example</span></span>

<span data-ttu-id="ac649-353">다음 예제는 hello 다른 매개 변수에서 매개 변수를 하나를 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-353">hello following example subtracts one parameter from another parameter.</span></span>

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
                "description": "Integer toosubtract"
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

<span data-ttu-id="ac649-354">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="ac649-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ac649-355">이름</span><span class="sxs-lookup"><span data-stu-id="ac649-355">Name</span></span> | <span data-ttu-id="ac649-356">형식</span><span class="sxs-lookup"><span data-stu-id="ac649-356">Type</span></span> | <span data-ttu-id="ac649-357">값</span><span class="sxs-lookup"><span data-stu-id="ac649-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ac649-358">subResult</span><span class="sxs-lookup"><span data-stu-id="ac649-358">subResult</span></span> | <span data-ttu-id="ac649-359">int</span><span class="sxs-lookup"><span data-stu-id="ac649-359">Int</span></span> | <span data-ttu-id="ac649-360">4</span><span class="sxs-lookup"><span data-stu-id="ac649-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac649-361">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac649-361">Next steps</span></span>
* <span data-ttu-id="ac649-362">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ac649-363">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="ac649-364">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="ac649-365">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac649-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

