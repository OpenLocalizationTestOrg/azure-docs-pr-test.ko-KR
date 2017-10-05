---
title: "Azure Managed Application UI 정의 만들기 함수 | Microsoft Docs"
description: "Azure Managed Applications에 대한 UI 정의를 생성할 때 사용하는 함수에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="0abf4-103">CreateUiDefinition 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="0abf4-104">이 섹션에는 CreateUiDefinition의 지원되는 모든 함수에 대한 서명이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="0abf4-105">함수를 사용하려면 선언을 대괄호로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="0abf4-106">예:</span><span class="sxs-lookup"><span data-stu-id="0abf4-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="0abf4-107">문자열 및 기타 함수를 함수에 대한 매개 변수로 참조할 수 있지만 문자열을 따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="0abf4-108">예:</span><span class="sxs-lookup"><span data-stu-id="0abf4-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="0abf4-109">해당하는 경우 점 연산자를 사용하여 함수 출력의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="0abf4-110">예:</span><span class="sxs-lookup"><span data-stu-id="0abf4-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="0abf4-111">참조 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-111">Referencing functions</span></span>
<span data-ttu-id="0abf4-112">이러한 함수를 사용하여 CreateUiDefinition의 속성 또는 컨텍스트 출력을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="0abf4-113">기본 사항</span><span class="sxs-lookup"><span data-stu-id="0abf4-113">basics</span></span>
<span data-ttu-id="0abf4-114">기본 사항 단계에서 정의된 요소의 출력 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="0abf4-115">다음 예제에서는 기본 사항 단계의 `foo` 요소 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="0abf4-116">단계</span><span class="sxs-lookup"><span data-stu-id="0abf4-116">steps</span></span>
<span data-ttu-id="0abf4-117">지정된 단계에서 정의된 요소의 출력 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="0abf4-118">기본 사항 단계의 요소 출력 값을 가져오려면 `basics()`를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="0abf4-119">다음 예제에서는 `foo` 단계의 `bar` 요소 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="0abf4-120">location</span><span class="sxs-lookup"><span data-stu-id="0abf4-120">location</span></span>
<span data-ttu-id="0abf4-121">기본 사항 단계 또는 현재 컨텍스트에서 선택한 위치를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="0abf4-122">다음 예제에서는 `"westus"`를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="0abf4-123">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-123">String functions</span></span>
<span data-ttu-id="0abf4-124">이러한 함수는 JSON 문자열하고만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="0abf4-125">concat</span><span class="sxs-lookup"><span data-stu-id="0abf4-125">concat</span></span>
<span data-ttu-id="0abf4-126">하나 이상의 문자열을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="0abf4-127">예를 들어 `element1`의 출력 값이 `"bar"`인 경우 이 예제에서는 `"foobar!"` 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="0abf4-128">substring</span><span class="sxs-lookup"><span data-stu-id="0abf4-128">substring</span></span>
<span data-ttu-id="0abf4-129">지정된 문자열의 부분 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="0abf4-130">부분 문자열은 지정된 인덱스에서 시작하고 지정된 길이를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="0abf4-131">다음 예제는 `"ftw"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="0abf4-132">replace</span><span class="sxs-lookup"><span data-stu-id="0abf4-132">replace</span></span>
<span data-ttu-id="0abf4-133">현재 문자열에서 지정된 문자열의 모든 항목이 다른 문자열로 바뀐 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="0abf4-134">다음 예제는 `"Everything is awesome!"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="0abf4-135">GUID</span><span class="sxs-lookup"><span data-stu-id="0abf4-135">guid</span></span>
<span data-ttu-id="0abf4-136">전역적으로 고유한 문자열(GUID)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="0abf4-137">다음 예제에서는 `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="0abf4-138">toLower</span><span class="sxs-lookup"><span data-stu-id="0abf4-138">toLower</span></span>
<span data-ttu-id="0abf4-139">소문자로 변환된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="0abf4-140">다음 예제는 `"foobar"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="0abf4-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="0abf4-141">toUpper</span></span>
<span data-ttu-id="0abf4-142">대문자로 변환된 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="0abf4-143">다음 예제는 `"FOOBAR"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="0abf4-144">컬렉션 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-144">Collection functions</span></span>
<span data-ttu-id="0abf4-145">이러한 함수는 JSON 문자열, 배열, 개체 등의 컬렉션과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="0abf4-146">contains</span><span class="sxs-lookup"><span data-stu-id="0abf4-146">contains</span></span>
<span data-ttu-id="0abf4-147">문자열에 지정된 부분 문자열이 포함되어 있거나, 배열에 지정된 값이 포함되어 있거나, 개체에 지정된 키가 포함되어 있으면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-148">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-148">Example 1: string</span></span>
<span data-ttu-id="0abf4-149">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-150">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-150">Example 2: array</span></span>
<span data-ttu-id="0abf4-151">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-152">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-153">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-153">Example 3: object</span></span>
<span data-ttu-id="0abf4-154">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="0abf4-155">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="0abf4-156">length</span><span class="sxs-lookup"><span data-stu-id="0abf4-156">length</span></span>
<span data-ttu-id="0abf4-157">문자열의 문자 수, 배열의 값 수 또는 개체의 키 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-158">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-158">Example 1: string</span></span>
<span data-ttu-id="0abf4-159">다음 예제는 `6`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-160">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-160">Example 2: array</span></span>
<span data-ttu-id="0abf4-161">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-162">다음 예제는 `3`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-163">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-163">Example 3: object</span></span>
<span data-ttu-id="0abf4-164">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="0abf4-165">다음 예제는 `2`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="0abf4-166">empty</span><span class="sxs-lookup"><span data-stu-id="0abf4-166">empty</span></span>
<span data-ttu-id="0abf4-167">문자열, 배열 또는 개체가 null이거나 비어 있으면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-168">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-168">Example 1: string</span></span>
<span data-ttu-id="0abf4-169">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-170">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-170">Example 2: array</span></span>
<span data-ttu-id="0abf4-171">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-172">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-173">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-173">Example 3: object</span></span>
<span data-ttu-id="0abf4-174">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="0abf4-175">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="0abf4-176">예제 4: null 및 undefined</span><span class="sxs-lookup"><span data-stu-id="0abf4-176">Example 4: null and undefined</span></span>
<span data-ttu-id="0abf4-177">`element1`이 `null` 또는 undefined라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="0abf4-178">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="0abf4-179">first</span><span class="sxs-lookup"><span data-stu-id="0abf4-179">first</span></span>
<span data-ttu-id="0abf4-180">지정된 문자열의 첫 번째 문자, 지정된 배열의 첫 번째 값 또는 지정된 개체의 첫 번째 키와 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-181">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-181">Example 1: string</span></span>
<span data-ttu-id="0abf4-182">다음 예제는 `"f"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-183">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-183">Example 2: array</span></span>
<span data-ttu-id="0abf4-184">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-185">다음 예제는 `1`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-186">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-186">Example 3: object</span></span>
<span data-ttu-id="0abf4-187">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="0abf4-188">다음 예제는 `{"key1": "foobar"}`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="0abf4-189">last</span><span class="sxs-lookup"><span data-stu-id="0abf4-189">last</span></span>
<span data-ttu-id="0abf4-190">지정된 문자열의 마지막 문자, 지정된 배열의 마지막 값 또는 지정된 개체의 마지막 키와 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-191">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-191">Example 1: string</span></span>
<span data-ttu-id="0abf4-192">다음 예제는 `"r"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-193">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-193">Example 2: array</span></span>
<span data-ttu-id="0abf4-194">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-195">다음 예제는 `2`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-196">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-196">Example 3: object</span></span>
<span data-ttu-id="0abf4-197">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="0abf4-198">다음 예제는 `{"key2": "raboof"}`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="0abf4-199">take</span><span class="sxs-lookup"><span data-stu-id="0abf4-199">take</span></span>
<span data-ttu-id="0abf4-200">문자열의 시작 부분부터 지정된 개수의 연속 문자, 배열의 시작 부분부터 지정된 개수의 연속 값 또는 개체의 시작 부분부터 지정된 개수의 연속 키와 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-201">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-201">Example 1: string</span></span>
<span data-ttu-id="0abf4-202">다음 예제는 `"foo"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-203">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-203">Example 2: array</span></span>
<span data-ttu-id="0abf4-204">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-205">다음 예제는 `[1, 2]`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-206">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-206">Example 3: object</span></span>
<span data-ttu-id="0abf4-207">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="0abf4-208">다음 예제는 `{"key1": "foobar"}`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="0abf4-209">skip</span><span class="sxs-lookup"><span data-stu-id="0abf4-209">skip</span></span>
<span data-ttu-id="0abf4-210">컬렉션에서 지정된 개수의 요소를 건너뛴 다음 나머지 요소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="0abf4-211">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="0abf4-211">Example 1: string</span></span>
<span data-ttu-id="0abf4-212">다음 예제는 `"bar"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="0abf4-213">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="0abf4-213">Example 2: array</span></span>
<span data-ttu-id="0abf4-214">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="0abf4-215">다음 예제는 `[3]`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="0abf4-216">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="0abf4-216">Example 3: object</span></span>
<span data-ttu-id="0abf4-217">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="0abf4-218">다음 예제는 `{"key2": "raboof"}`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="0abf4-219">논리 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-219">Logical functions</span></span>
<span data-ttu-id="0abf4-220">조건문에서 이러한 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="0abf4-221">일부 함수는 모든 JSON 데이터 형식을 지원하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="0abf4-222">equals</span><span class="sxs-lookup"><span data-stu-id="0abf4-222">equals</span></span>
<span data-ttu-id="0abf4-223">두 매개 변수의 형식과 값이 같으면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="0abf4-224">이 함수는 모든 JSON 데이터 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="0abf4-225">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="0abf4-226">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="0abf4-227">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="0abf4-228">less</span><span class="sxs-lookup"><span data-stu-id="0abf4-228">less</span></span>
<span data-ttu-id="0abf4-229">첫 번째 매개 변수가 두 번째 매개 변수보다 엄격하게 작으면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="0abf4-230">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="0abf4-231">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="0abf4-232">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="0abf4-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="0abf4-233">lessOrEquals</span></span>
<span data-ttu-id="0abf4-234">첫 번째 매개 변수가 두 번째 매개 변수보다 작거나 같으면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="0abf4-235">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="0abf4-236">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="0abf4-237">greater</span><span class="sxs-lookup"><span data-stu-id="0abf4-237">greater</span></span>
<span data-ttu-id="0abf4-238">첫 번째 매개 변수가 두 번째 매개 변수보다 엄격하게 크면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="0abf4-239">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="0abf4-240">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="0abf4-241">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="0abf4-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="0abf4-242">greaterOrEquals</span></span>
<span data-ttu-id="0abf4-243">첫 번째 매개 변수가 두 번째 매개 변수보다 크거나 같으면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="0abf4-244">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="0abf4-245">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="0abf4-246">and</span><span class="sxs-lookup"><span data-stu-id="0abf4-246">and</span></span>
<span data-ttu-id="0abf4-247">모든 매개 변수가 `true`로 평가되면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="0abf4-248">이 함수는 두 개 이상의 부울 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="0abf4-249">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="0abf4-250">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="0abf4-251">또는</span><span class="sxs-lookup"><span data-stu-id="0abf4-251">or</span></span>
<span data-ttu-id="0abf4-252">매개 변수 중 하나 이상이 `true`로 평가되면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="0abf4-253">이 함수는 두 개 이상의 부울 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="0abf4-254">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="0abf4-255">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="0abf4-256">not</span><span class="sxs-lookup"><span data-stu-id="0abf4-256">not</span></span>
<span data-ttu-id="0abf4-257">매개 변수가 `false`로 평가되면 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="0abf4-258">이 함수는 부울 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="0abf4-259">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="0abf4-260">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="0abf4-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="0abf4-261">coalesce</span></span>
<span data-ttu-id="0abf4-262">null이 아닌 첫 번째 매개 변수의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="0abf4-263">이 함수는 모든 JSON 데이터 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="0abf4-264">`element1` 및 `element2`를 undefined로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="0abf4-265">다음 예제는 `"foobar"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="0abf4-266">변환 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-266">Conversion functions</span></span>
<span data-ttu-id="0abf4-267">이러한 함수를 사용하여 JSON 데이터 형식 및 인코딩 간에 값을 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="0abf4-268">int</span><span class="sxs-lookup"><span data-stu-id="0abf4-268">int</span></span>
<span data-ttu-id="0abf4-269">매개 변수를 정수로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="0abf4-270">이 함수는 숫자 및 문자열 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="0abf4-271">다음 예제는 `1`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="0abf4-272">다음 예제는 `2`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="0abf4-273">float</span><span class="sxs-lookup"><span data-stu-id="0abf4-273">float</span></span>
<span data-ttu-id="0abf4-274">매개 변수를 부동 소수점으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="0abf4-275">이 함수는 숫자 및 문자열 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="0abf4-276">다음 예제는 `1.0`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="0abf4-277">다음 예제는 `2.9`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="0abf4-278">string</span><span class="sxs-lookup"><span data-stu-id="0abf4-278">string</span></span>
<span data-ttu-id="0abf4-279">매개 변수를 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-279">Converts the parameter to a string.</span></span> <span data-ttu-id="0abf4-280">이 함수는 모든 JSON 데이터 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="0abf4-281">다음 예제는 `"1"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="0abf4-282">다음 예제는 `"2.9"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="0abf4-283">다음 예제는 `"[1,2,3]"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="0abf4-284">다음 예제는 `"{"foo":"bar"}"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="0abf4-285">bool</span><span class="sxs-lookup"><span data-stu-id="0abf4-285">bool</span></span>
<span data-ttu-id="0abf4-286">매개 변수를 부울로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="0abf4-287">이 함수는 숫자, 문자열 및 부울 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="0abf4-288">JavaScript의 부울과 마찬가지로 `0` 또는 `'false'` 이외의 모든 값은 `true`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="0abf4-289">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="0abf4-290">다음 예제는 `false`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="0abf4-291">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="0abf4-292">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="0abf4-293">parse</span><span class="sxs-lookup"><span data-stu-id="0abf4-293">parse</span></span>
<span data-ttu-id="0abf4-294">매개 변수를 네이티브 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="0abf4-295">즉, 이 함수는 `string()`의 역함수입니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="0abf4-296">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="0abf4-297">다음 예제는 `1`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="0abf4-298">다음 예제는 `true`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="0abf4-299">다음 예제는 `[1,2,3]`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="0abf4-300">다음 예제는 `{"foo":"bar"}`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="0abf4-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="0abf4-301">encodeBase64</span></span>
<span data-ttu-id="0abf4-302">매개 변수를 base-64로 인코드된 문자열로 인코드합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="0abf4-303">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="0abf4-304">다음 예제는 `"Zm9vYmFy"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="0abf4-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="0abf4-305">decodeBase64</span></span>
<span data-ttu-id="0abf4-306">매개 변수를 base-64로 인코드된 문자열에서 디코드합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="0abf4-307">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="0abf4-308">다음 예제는 `"foobar"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="0abf4-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="0abf4-309">encodeUriComponent</span></span>
<span data-ttu-id="0abf4-310">매개 변수를 URL로 인코드된 문자열로 인코드합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="0abf4-311">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="0abf4-312">다음 예제는 `"https%3A%2F%2Fportal.azure.com%2F"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="0abf4-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="0abf4-313">decodeUriComponent</span></span>
<span data-ttu-id="0abf4-314">매개 변수를 URL로 인코드된 문자열에서 디코드합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="0abf4-315">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="0abf4-316">다음 예제는 `"https://portal.azure.com/"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="0abf4-317">수학 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="0abf4-318">추가</span><span class="sxs-lookup"><span data-stu-id="0abf4-318">add</span></span>
<span data-ttu-id="0abf4-319">두 숫자를 더한 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="0abf4-320">다음 예제는 `3`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="0abf4-321">sub</span><span class="sxs-lookup"><span data-stu-id="0abf4-321">sub</span></span>
<span data-ttu-id="0abf4-322">첫 번째 숫자에서 두 번째 숫자를 뺀 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="0abf4-323">다음 예제는 `1`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="0abf4-324">mul</span><span class="sxs-lookup"><span data-stu-id="0abf4-324">mul</span></span>
<span data-ttu-id="0abf4-325">두 숫자를 곱한 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="0abf4-326">다음 예제는 `6`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="0abf4-327">div</span><span class="sxs-lookup"><span data-stu-id="0abf4-327">div</span></span>
<span data-ttu-id="0abf4-328">첫 번째 숫자를 두 번째 숫자로 나눈 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="0abf4-329">결과는 항상 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-329">The result is always an integer.</span></span>

<span data-ttu-id="0abf4-330">다음 예제는 `2`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="0abf4-331">mod</span><span class="sxs-lookup"><span data-stu-id="0abf4-331">mod</span></span>
<span data-ttu-id="0abf4-332">첫 번째 숫자를 두 번째 숫자로 나눈 나머지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="0abf4-333">다음 예제는 `0`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="0abf4-334">다음 예제는 `2`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="0abf4-335">Min</span><span class="sxs-lookup"><span data-stu-id="0abf4-335">min</span></span>
<span data-ttu-id="0abf4-336">두 숫자 중 작은 숫자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="0abf4-337">다음 예제는 `1`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="0abf4-338">max</span><span class="sxs-lookup"><span data-stu-id="0abf4-338">max</span></span>
<span data-ttu-id="0abf4-339">두 숫자 중 큰 숫자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="0abf4-340">다음 예제는 `2`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="0abf4-341">range</span><span class="sxs-lookup"><span data-stu-id="0abf4-341">range</span></span>
<span data-ttu-id="0abf4-342">지정된 범위 내의 정수 시퀀스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="0abf4-343">다음 예제는 `[1,2,3]`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="0abf4-344">rand</span><span class="sxs-lookup"><span data-stu-id="0abf4-344">rand</span></span>
<span data-ttu-id="0abf4-345">지정된 범위 내의 임의 정수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="0abf4-346">이 함수는 암호화하여 보안 설정된 난수를 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="0abf4-347">다음 예제에서는 `42`를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="0abf4-348">floor</span><span class="sxs-lookup"><span data-stu-id="0abf4-348">floor</span></span>
<span data-ttu-id="0abf4-349">지정한 숫자보다 작거나 같은 가장 큰 정수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="0abf4-350">다음 예제는 `3`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="0abf4-351">ceil</span><span class="sxs-lookup"><span data-stu-id="0abf4-351">ceil</span></span>
<span data-ttu-id="0abf4-352">지정한 숫자보다 크거나 같은 가장 큰 정수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="0abf4-353">다음 예제는 `4`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="0abf4-354">날짜 함수</span><span class="sxs-lookup"><span data-stu-id="0abf4-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="0abf4-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="0abf4-355">utcNow</span></span>
<span data-ttu-id="0abf4-356">로컬 컴퓨터의 현재 날짜 및 시간 문자열을 ISO 8601 형식으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="0abf4-357">다음 예제에서는 `"1990-12-31T23:59:59.000Z"`를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="0abf4-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="0abf4-358">addSeconds</span></span>
<span data-ttu-id="0abf4-359">지정된 타임스탬프에 시간(초)에 대한 정수를 더합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="0abf4-360">다음 예제는 `"1991-01-01T00:00:00.000Z"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="0abf4-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="0abf4-361">addMinutes</span></span>
<span data-ttu-id="0abf4-362">지정된 타임스탬프에 시간(분)에 대한 정수를 더합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="0abf4-363">다음 예제는 `"1991-01-01T00:00:59.000Z"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="0abf4-364">addHours</span><span class="sxs-lookup"><span data-stu-id="0abf4-364">addHours</span></span>
<span data-ttu-id="0abf4-365">지정된 타임스탬프에 시간(시)에 대한 정수를 더합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="0abf4-366">다음 예제는 `"1991-01-01T00:59:59.000Z"`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0abf4-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="0abf4-367">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0abf4-367">Next steps</span></span>
* <span data-ttu-id="0abf4-368">Azure Resource Manager에 대한 소개는 [Azure Resource Manager 개요](resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0abf4-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

