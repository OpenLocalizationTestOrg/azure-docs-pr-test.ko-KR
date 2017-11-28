---
title: "관리 되는 응용 프로그램 aaaAzure UI 정의 함수를 만들 | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 UI 정의 생성할 때 hello 함수 toouse 설명"
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
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="64e6b-103">CreateUiDefinition 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="64e6b-104">이 섹션에는 CreateUiDefinition의 지원 되는 모든 함수에 대 한 hello 서명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="64e6b-105">toouse는 함수를 대괄호로 서라운드 hello 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="64e6b-106">예:</span><span class="sxs-lookup"><span data-stu-id="64e6b-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="64e6b-107">문자열 및 기타 함수를 함수에 대한 매개 변수로 참조할 수 있지만 문자열을 따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="64e6b-108">예:</span><span class="sxs-lookup"><span data-stu-id="64e6b-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="64e6b-109">해당 되는 경우에 hello 점 연산자를 사용 하 여 함수 hello 출력의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="64e6b-110">예:</span><span class="sxs-lookup"><span data-stu-id="64e6b-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="64e6b-111">참조 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-111">Referencing functions</span></span>
<span data-ttu-id="64e6b-112">이러한 함수는 hello 속성 또는 CreateUiDefinition의 컨텍스트에서 사용 되는 tooreference 출력 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="64e6b-113">기본 사항</span><span class="sxs-lookup"><span data-stu-id="64e6b-113">basics</span></span>
<span data-ttu-id="64e6b-114">Hello 기본적인 단계에 정의 된 요소의 hello 출력 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="64e6b-115">hello 다음 예제에서는 출력을 반환 hello 라는 hello 요소의 `foo` hello 기본 사항 단계에서:</span><span class="sxs-lookup"><span data-stu-id="64e6b-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="64e6b-116">단계</span><span class="sxs-lookup"><span data-stu-id="64e6b-116">steps</span></span>
<span data-ttu-id="64e6b-117">단계를 지정된 하는 hello에 정의 된 요소의 hello 출력 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="64e6b-118">hello 기본적인 단계에 있는 요소의 tooget hello 출력 값에 사용 하 여 `basics()` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="64e6b-119">hello 다음 예제에서는 출력을 반환 hello 라는 hello 요소의 `bar` hello 단계 라는 `foo`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="64e6b-120">location</span><span class="sxs-lookup"><span data-stu-id="64e6b-120">location</span></span>
<span data-ttu-id="64e6b-121">Hello 현재 컨텍스트 또는 hello 기본 사항 단계에서 선택한 hello 위치를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="64e6b-122">hello 다음 예제에서는 반환 될 수 `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="64e6b-123">문자열 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-123">String functions</span></span>
<span data-ttu-id="64e6b-124">이러한 함수는 JSON 문자열하고만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="64e6b-125">concat</span><span class="sxs-lookup"><span data-stu-id="64e6b-125">concat</span></span>
<span data-ttu-id="64e6b-126">하나 이상의 문자열을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="64e6b-127">예를 들어 hello 출력 값의 `element1` 경우 `"bar"`, hello 문자열을 반환 하는이 예에서는 다음 `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="64e6b-128">substring</span><span class="sxs-lookup"><span data-stu-id="64e6b-128">substring</span></span>
<span data-ttu-id="64e6b-129">지정 된 hello의 hello 부분 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="64e6b-130">hello 지정 된 인덱스에서 시작 된 hello 부분 문자열을이 hello 길이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="64e6b-131">hello 다음 예제에서는 반환 `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="64e6b-132">replace</span><span class="sxs-lookup"><span data-stu-id="64e6b-132">replace</span></span>
<span data-ttu-id="64e6b-133">Hello 발견 되는 모든 문자열 hello 현재 문자열에 문자열을 지정 된 반환 된 다른 문자열로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="64e6b-134">hello 다음 예제에서는 반환 `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="64e6b-135">GUID</span><span class="sxs-lookup"><span data-stu-id="64e6b-135">guid</span></span>
<span data-ttu-id="64e6b-136">전역적으로 고유한 문자열(GUID)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="64e6b-137">hello 다음 예제에서는 반환 될 수 `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="64e6b-138">toLower</span><span class="sxs-lookup"><span data-stu-id="64e6b-138">toLower</span></span>
<span data-ttu-id="64e6b-139">변환 된 문자열 toolowercase를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="64e6b-140">hello 다음 예제에서는 반환 `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="64e6b-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="64e6b-141">toUpper</span></span>
<span data-ttu-id="64e6b-142">변환 된 문자열 toouppercase를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="64e6b-143">hello 다음 예제에서는 반환 `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="64e6b-144">컬렉션 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-144">Collection functions</span></span>
<span data-ttu-id="64e6b-145">이러한 함수는 JSON 문자열, 배열, 개체 등의 컬렉션과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="64e6b-146">contains</span><span class="sxs-lookup"><span data-stu-id="64e6b-146">contains</span></span>
<span data-ttu-id="64e6b-147">반환 `true` 문자열에 포함 된 경우 지정 된 부분 문자열 hello, 배열에 포함 되어 hello 지정한 키가 들어 있는 개체 또는 hello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-148">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-148">Example 1: string</span></span>
<span data-ttu-id="64e6b-149">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-150">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-150">Example 2: array</span></span>
<span data-ttu-id="64e6b-151">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-152">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-153">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-153">Example 3: object</span></span>
<span data-ttu-id="64e6b-154">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="64e6b-155">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="64e6b-156">length</span><span class="sxs-lookup"><span data-stu-id="64e6b-156">length</span></span>
<span data-ttu-id="64e6b-157">문자열, 배열에는 값의 hello 수 또는 키 개체에 hello 수의 문자 수가 hello를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-158">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-158">Example 1: string</span></span>
<span data-ttu-id="64e6b-159">hello 다음 예제에서는 반환 `6`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-160">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-160">Example 2: array</span></span>
<span data-ttu-id="64e6b-161">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-162">hello 다음 예제에서는 반환 `3`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-163">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-163">Example 3: object</span></span>
<span data-ttu-id="64e6b-164">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="64e6b-165">hello 다음 예제에서는 반환 `2`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="64e6b-166">empty</span><span class="sxs-lookup"><span data-stu-id="64e6b-166">empty</span></span>
<span data-ttu-id="64e6b-167">반환 `true` hello 문자열, 배열 또는 개체가 null 이거나 비어 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-168">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-168">Example 1: string</span></span>
<span data-ttu-id="64e6b-169">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-170">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-170">Example 2: array</span></span>
<span data-ttu-id="64e6b-171">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-172">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-173">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-173">Example 3: object</span></span>
<span data-ttu-id="64e6b-174">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="64e6b-175">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="64e6b-176">예제 4: null 및 undefined</span><span class="sxs-lookup"><span data-stu-id="64e6b-176">Example 4: null and undefined</span></span>
<span data-ttu-id="64e6b-177">`element1`이 `null` 또는 undefined라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="64e6b-178">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="64e6b-179">first</span><span class="sxs-lookup"><span data-stu-id="64e6b-179">first</span></span>
<span data-ttu-id="64e6b-180">지정 된 문자열의 hello 반환 hello 첫 번째 문자가 지정 된 배열 hello;의 첫 번째 값 또는 첫 번째 키와 hello 지정된 개체의 값을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-181">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-181">Example 1: string</span></span>
<span data-ttu-id="64e6b-182">hello 다음 예제에서는 반환 `"f"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-183">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-183">Example 2: array</span></span>
<span data-ttu-id="64e6b-184">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-185">hello 다음 예제에서는 반환 `1`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-186">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-186">Example 3: object</span></span>
<span data-ttu-id="64e6b-187">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="64e6b-188">hello 다음 예제에서는 반환 `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="64e6b-189">last</span><span class="sxs-lookup"><span data-stu-id="64e6b-189">last</span></span>
<span data-ttu-id="64e6b-190">지정 된 hello 반환 hello 마지막 문자는 문자열, hello hello 지정 배열의 마지막 값 또는 hello 마지막 키와 hello 지정된 개체의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-191">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-191">Example 1: string</span></span>
<span data-ttu-id="64e6b-192">hello 다음 예제에서는 반환 `"r"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-193">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-193">Example 2: array</span></span>
<span data-ttu-id="64e6b-194">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-195">hello 다음 예제에서는 반환 `2`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-196">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-196">Example 3: object</span></span>
<span data-ttu-id="64e6b-197">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="64e6b-198">hello 다음 예제에서는 반환 `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="64e6b-199">take</span><span class="sxs-lookup"><span data-stu-id="64e6b-199">take</span></span>
<span data-ttu-id="64e6b-200">지정된 된 수의 hello hello 문자열 시작에서 연속 된 문자, 지정된 된 수의 hello 배열의 hello 시작에서 인접 하는 값 또는 지정 된 개수의 연속 키와 hello 시작 hello 개체의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-201">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-201">Example 1: string</span></span>
<span data-ttu-id="64e6b-202">hello 다음 예제에서는 반환 `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-203">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-203">Example 2: array</span></span>
<span data-ttu-id="64e6b-204">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-205">hello 다음 예제에서는 반환 `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-206">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-206">Example 3: object</span></span>
<span data-ttu-id="64e6b-207">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="64e6b-208">hello 다음 예제에서는 반환 `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="64e6b-209">skip</span><span class="sxs-lookup"><span data-stu-id="64e6b-209">skip</span></span>
<span data-ttu-id="64e6b-210">지정 된 된 수는 컬렉션의 요소를 무시 하 고 나머지 요소의 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="64e6b-211">예제 1: 문자열</span><span class="sxs-lookup"><span data-stu-id="64e6b-211">Example 1: string</span></span>
<span data-ttu-id="64e6b-212">hello 다음 예제에서는 반환 `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="64e6b-213">예제 2: 배열</span><span class="sxs-lookup"><span data-stu-id="64e6b-213">Example 2: array</span></span>
<span data-ttu-id="64e6b-214">`element1`이 `[1, 2, 3]`을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="64e6b-215">hello 다음 예제에서는 반환 `[3]`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="64e6b-216">예제 3: 개체</span><span class="sxs-lookup"><span data-stu-id="64e6b-216">Example 3: object</span></span>
<span data-ttu-id="64e6b-217">`element1`이 다음을 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="64e6b-218">hello 다음 예제에서는 반환 `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="64e6b-219">논리 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-219">Logical functions</span></span>
<span data-ttu-id="64e6b-220">조건문에서 이러한 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="64e6b-221">일부 함수는 모든 JSON 데이터 형식을 지원하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="64e6b-222">equals</span><span class="sxs-lookup"><span data-stu-id="64e6b-222">equals</span></span>
<span data-ttu-id="64e6b-223">반환 `true` 두 매개 변수에 있는 hello 동일한 입력 한 값 경우.</span><span class="sxs-lookup"><span data-stu-id="64e6b-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="64e6b-224">이 함수는 모든 JSON 데이터 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="64e6b-225">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="64e6b-226">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="64e6b-227">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="64e6b-228">less</span><span class="sxs-lookup"><span data-stu-id="64e6b-228">less</span></span>
<span data-ttu-id="64e6b-229">반환 `true` hello 첫 번째 매개 변수가 이면 hello 두 번째 매개 변수 보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="64e6b-230">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="64e6b-231">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="64e6b-232">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="64e6b-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="64e6b-233">lessOrEquals</span></span>
<span data-ttu-id="64e6b-234">반환 `true` hello 첫 번째 매개 변수 보다 작거나 같은 경우 toohello 두 번째 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="64e6b-235">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="64e6b-236">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="64e6b-237">greater</span><span class="sxs-lookup"><span data-stu-id="64e6b-237">greater</span></span>
<span data-ttu-id="64e6b-238">반환 `true` hello 첫 번째 매개 변수가 엄격 하 게 hello 두 번째 매개 변수 보다 큰 경우.</span><span class="sxs-lookup"><span data-stu-id="64e6b-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="64e6b-239">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="64e6b-240">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="64e6b-241">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="64e6b-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="64e6b-242">greaterOrEquals</span></span>
<span data-ttu-id="64e6b-243">반환 `true` hello 첫 번째 매개 변수 보다 크거나 같은 toohello 두 번째 매개 변수인 경우.</span><span class="sxs-lookup"><span data-stu-id="64e6b-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="64e6b-244">이 함수는 숫자 및 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="64e6b-245">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="64e6b-246">and</span><span class="sxs-lookup"><span data-stu-id="64e6b-246">and</span></span>
<span data-ttu-id="64e6b-247">반환 `true` 모든 hello 매개 변수가 너무 평가 되 면`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="64e6b-248">이 함수는 두 개 이상의 부울 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="64e6b-249">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="64e6b-250">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="64e6b-251">또는</span><span class="sxs-lookup"><span data-stu-id="64e6b-251">or</span></span>
<span data-ttu-id="64e6b-252">반환 `true` hello 매개 변수 중 하나 이상이 너무 평가 되 면`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="64e6b-253">이 함수는 두 개 이상의 부울 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="64e6b-254">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="64e6b-255">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="64e6b-256">not</span><span class="sxs-lookup"><span data-stu-id="64e6b-256">not</span></span>
<span data-ttu-id="64e6b-257">반환 `true` hello 매개 변수가 너무 평가 하는 경우`false`합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="64e6b-258">이 함수는 부울 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="64e6b-259">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="64e6b-260">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="64e6b-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="64e6b-261">coalesce</span></span>
<span data-ttu-id="64e6b-262">반환 hello hello 첫 번째 null이 아닌 매개 변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="64e6b-263">이 함수는 모든 JSON 데이터 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="64e6b-264">`element1` 및 `element2`를 undefined로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="64e6b-265">hello 다음 예제에서는 반환 `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="64e6b-266">변환 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-266">Conversion functions</span></span>
<span data-ttu-id="64e6b-267">이러한 함수에는 JSON 데이터 형식 및 인코딩에서 간에 사용 되는 tooconvert 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="64e6b-268">int</span><span class="sxs-lookup"><span data-stu-id="64e6b-268">int</span></span>
<span data-ttu-id="64e6b-269">Hello tooan 정수 매개 변수를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="64e6b-270">이 함수는 숫자 및 문자열 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="64e6b-271">hello 다음 예제에서는 반환 `1`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="64e6b-272">hello 다음 예제에서는 반환 `2`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="64e6b-273">float</span><span class="sxs-lookup"><span data-stu-id="64e6b-273">float</span></span>
<span data-ttu-id="64e6b-274">Hello 매개 변수 tooa 부동 소수점 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="64e6b-275">이 함수는 숫자 및 문자열 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="64e6b-276">hello 다음 예제에서는 반환 `1.0`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="64e6b-277">hello 다음 예제에서는 반환 `2.9`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="64e6b-278">string</span><span class="sxs-lookup"><span data-stu-id="64e6b-278">string</span></span>
<span data-ttu-id="64e6b-279">Hello 매개 변수 tooa 문자열을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="64e6b-280">이 함수는 모든 JSON 데이터 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="64e6b-281">hello 다음 예제에서는 반환 `"1"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="64e6b-282">hello 다음 예제에서는 반환 `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="64e6b-283">hello 다음 예제에서는 반환 `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="64e6b-284">hello 다음 예제에서는 반환 `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="64e6b-285">bool</span><span class="sxs-lookup"><span data-stu-id="64e6b-285">bool</span></span>
<span data-ttu-id="64e6b-286">Hello 매개 변수 tooa 부울 값으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="64e6b-287">이 함수는 숫자, 문자열 및 부울 형식의 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="64e6b-288">JavaScript 제외한 모든 값에에서 비슷한 tooBooleans `0` 또는 `'false'` 반환 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="64e6b-289">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="64e6b-290">hello 다음 예제에서는 반환 `false`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="64e6b-291">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="64e6b-292">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="64e6b-293">parse</span><span class="sxs-lookup"><span data-stu-id="64e6b-293">parse</span></span>
<span data-ttu-id="64e6b-294">Hello 매개 변수 tooa 네이티브 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="64e6b-295">즉,이 함수는의 hello 역 `string()`합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="64e6b-296">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="64e6b-297">hello 다음 예제에서는 반환 `1`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="64e6b-298">hello 다음 예제에서는 반환 `true`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="64e6b-299">hello 다음 예제에서는 반환 `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="64e6b-300">hello 다음 예제에서는 반환 `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="64e6b-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="64e6b-301">encodeBase64</span></span>
<span data-ttu-id="64e6b-302">Hello 매개 변수 tooa e-64로 인코딩된 문자열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="64e6b-303">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="64e6b-304">hello 다음 예제에서는 반환 `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="64e6b-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="64e6b-305">decodeBase64</span></span>
<span data-ttu-id="64e6b-306">Hello 매개 변수를에서 e-64로 인코딩된 문자열을 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="64e6b-307">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="64e6b-308">hello 다음 예제에서는 반환 `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="64e6b-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="64e6b-309">encodeUriComponent</span></span>
<span data-ttu-id="64e6b-310">Hello 매개 변수 tooa URL로 인코딩된 문자열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="64e6b-311">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="64e6b-312">hello 다음 예제에서는 반환 `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="64e6b-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="64e6b-313">decodeUriComponent</span></span>
<span data-ttu-id="64e6b-314">Hello 매개 변수를를 URL로 인코딩된 문자열로 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="64e6b-315">이 함수는 문자열 형식의 매개 변수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="64e6b-316">hello 다음 예제에서는 반환 `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="64e6b-317">수학 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="64e6b-318">추가</span><span class="sxs-lookup"><span data-stu-id="64e6b-318">add</span></span>
<span data-ttu-id="64e6b-319">두 숫자를 추가 하 고 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="64e6b-320">hello 다음 예제에서는 반환 `3`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="64e6b-321">sub</span><span class="sxs-lookup"><span data-stu-id="64e6b-321">sub</span></span>
<span data-ttu-id="64e6b-322">Hello hello 첫 번째 숫자에서 두 번째 숫자를 뺍니다 하 고 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="64e6b-323">hello 다음 예제에서는 반환 `1`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="64e6b-324">mul</span><span class="sxs-lookup"><span data-stu-id="64e6b-324">mul</span></span>
<span data-ttu-id="64e6b-325">두 숫자를 곱합니다 하 고 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="64e6b-326">hello 다음 예제에서는 반환 `6`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="64e6b-327">div</span><span class="sxs-lookup"><span data-stu-id="64e6b-327">div</span></span>
<span data-ttu-id="64e6b-328">첫 번째 숫자 hello hello 두 번째 숫자를 나누고 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="64e6b-329">hello 결과 항상는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-329">hello result is always an integer.</span></span>

<span data-ttu-id="64e6b-330">hello 다음 예제에서는 반환 `2`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="64e6b-331">mod</span><span class="sxs-lookup"><span data-stu-id="64e6b-331">mod</span></span>
<span data-ttu-id="64e6b-332">첫 번째 숫자 hello hello 두 번째 숫자를 나누고 hello 나머지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="64e6b-333">hello 다음 예제에서는 반환 `0`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="64e6b-334">hello 다음 예제에서는 반환 `2`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="64e6b-335">Min</span><span class="sxs-lookup"><span data-stu-id="64e6b-335">min</span></span>
<span data-ttu-id="64e6b-336">반환 hello hello 두 숫자의 작은 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="64e6b-337">hello 다음 예제에서는 반환 `1`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="64e6b-338">max</span><span class="sxs-lookup"><span data-stu-id="64e6b-338">max</span></span>
<span data-ttu-id="64e6b-339">반환 hello hello 두 숫자 중 더 큰 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="64e6b-340">hello 다음 예제에서는 반환 `2`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="64e6b-341">range</span><span class="sxs-lookup"><span data-stu-id="64e6b-341">range</span></span>
<span data-ttu-id="64e6b-342">정수 시퀀스를 생성 hello 내에서 숫자 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="64e6b-343">hello 다음 예제에서는 반환 `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="64e6b-344">rand</span><span class="sxs-lookup"><span data-stu-id="64e6b-344">rand</span></span>
<span data-ttu-id="64e6b-345">임의 반환 hello 내의 정수 계열 숫자 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="64e6b-346">이 함수는 암호화하여 보안 설정된 난수를 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="64e6b-347">hello 다음 예제에서는 반환 될 수 `42`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="64e6b-348">floor</span><span class="sxs-lookup"><span data-stu-id="64e6b-348">floor</span></span>
<span data-ttu-id="64e6b-349">보다 작거나 같은 최대 정수 hello 반환 toohello 번호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="64e6b-350">hello 다음 예제에서는 반환 `3`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="64e6b-351">ceil</span><span class="sxs-lookup"><span data-stu-id="64e6b-351">ceil</span></span>
<span data-ttu-id="64e6b-352">반환 hello 보다 큰 가장 큰 정수 또는 같은 toohello 번호를 지정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="64e6b-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="64e6b-353">hello 다음 예제에서는 반환 `4`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="64e6b-354">날짜 함수</span><span class="sxs-lookup"><span data-stu-id="64e6b-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="64e6b-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="64e6b-355">utcNow</span></span>
<span data-ttu-id="64e6b-356">ISO 8601 서식의 hello hello 로컬 컴퓨터의 현재 날짜 및 시간 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="64e6b-357">hello 다음 예제에서는 반환 될 수 `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="64e6b-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="64e6b-358">addSeconds</span></span>
<span data-ttu-id="64e6b-359">지정 된 시간 (초) toohello의 정수가 추가 하는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="64e6b-360">hello 다음 예제에서는 반환 `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="64e6b-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="64e6b-361">addMinutes</span></span>
<span data-ttu-id="64e6b-362">지정 된 시간 (분) toohello의 정수가 추가 하는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="64e6b-363">hello 다음 예제에서는 반환 `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="64e6b-364">addHours</span><span class="sxs-lookup"><span data-stu-id="64e6b-364">addHours</span></span>
<span data-ttu-id="64e6b-365">지정 된 시간 toohello의 정수가 추가 하는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="64e6b-366">hello 다음 예제에서는 반환 `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="64e6b-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="64e6b-367">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64e6b-367">Next steps</span></span>
* <span data-ttu-id="64e6b-368">리소스 관리자에는 소개 tooAzure 참조 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64e6b-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

