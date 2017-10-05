---
title: "Azure API 관리 정책에 속성을 사용하는 방법"
description: "Azure API 관리 정책에 속성을 사용하는 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="e3d90-103">Azure API 관리 정책에 속성을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e3d90-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="e3d90-104">API 관리 정책은 게시자가 구성을 통해 API 동작을 변경할 수 있도록 하는 시스템의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="e3d90-105">정책은 API의 요청이나 응답에 따라 순차적으로 실행되는 명령문의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="e3d90-106">정책 설명은 리터럴 텍스트 값, 정책 식 및 속성을 사용하여 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="e3d90-107">각 API 관리 서비스 인스턴스에는 해당 서비스 인스턴스에 전역인 키/값 쌍의 속성 컬렉션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="e3d90-108">이러한 속성을 사용하여 모든 API 구성 및 정책에서 상수 문자열 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="e3d90-109">각 속성에는 다음과 같은 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="e3d90-110">특성</span><span class="sxs-lookup"><span data-stu-id="e3d90-110">Attribute</span></span> | <span data-ttu-id="e3d90-111">형식</span><span class="sxs-lookup"><span data-stu-id="e3d90-111">Type</span></span> | <span data-ttu-id="e3d90-112">설명</span><span class="sxs-lookup"><span data-stu-id="e3d90-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3d90-113">Name</span><span class="sxs-lookup"><span data-stu-id="e3d90-113">Name</span></span> |<span data-ttu-id="e3d90-114">string</span><span class="sxs-lookup"><span data-stu-id="e3d90-114">string</span></span> |<span data-ttu-id="e3d90-115">속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-115">The name of the property.</span></span> <span data-ttu-id="e3d90-116">문자, 숫자, 마침표, 대시 및 밑줄 문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="e3d90-117">값</span><span class="sxs-lookup"><span data-stu-id="e3d90-117">Value</span></span> |<span data-ttu-id="e3d90-118">string</span><span class="sxs-lookup"><span data-stu-id="e3d90-118">string</span></span> |<span data-ttu-id="e3d90-119">속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-119">The value of the property.</span></span> <span data-ttu-id="e3d90-120">비워 두거나 공백만으로 구성될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="e3d90-121">Secret</span><span class="sxs-lookup"><span data-stu-id="e3d90-121">Secret</span></span> |<span data-ttu-id="e3d90-122">부울</span><span class="sxs-lookup"><span data-stu-id="e3d90-122">boolean</span></span> |<span data-ttu-id="e3d90-123">값이 암호인지, 그리고 암호화해야 하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="e3d90-124">태그</span><span class="sxs-lookup"><span data-stu-id="e3d90-124">Tags</span></span> |<span data-ttu-id="e3d90-125">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="e3d90-125">array of string</span></span> |<span data-ttu-id="e3d90-126">제공된 경우 속성 목록을 필터링하는 데 사용할 수 있는 선택적 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="e3d90-127">속성은 게시자 포털의 **속성** 탭에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="e3d90-128">다음 예제에는 세 가지 속성이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-128">In the following example, three properties are configured.</span></span>

![속성][api-management-properties]

<span data-ttu-id="e3d90-130">속성 값은 리터럴 문자열 및 [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx)을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="e3d90-131">다음 표에서는 위의 세 가지 샘플 속성 및 해당 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="e3d90-132">`ExpressionProperty` 값은 현재 날짜 및 시간이 포함된 문자열을 반환하는 정책 식입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="e3d90-133">`ContosoHeaderValue` 속성은 암호 표식이 있으므로 해당 값이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="e3d90-134">Name</span><span class="sxs-lookup"><span data-stu-id="e3d90-134">Name</span></span> | <span data-ttu-id="e3d90-135">값</span><span class="sxs-lookup"><span data-stu-id="e3d90-135">Value</span></span> | <span data-ttu-id="e3d90-136">Secret</span><span class="sxs-lookup"><span data-stu-id="e3d90-136">Secret</span></span> | <span data-ttu-id="e3d90-137">태그</span><span class="sxs-lookup"><span data-stu-id="e3d90-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e3d90-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="e3d90-138">ContosoHeader</span></span> |<span data-ttu-id="e3d90-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="e3d90-139">TrackingId</span></span> |<span data-ttu-id="e3d90-140">False</span><span class="sxs-lookup"><span data-stu-id="e3d90-140">False</span></span> |<span data-ttu-id="e3d90-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="e3d90-141">Contoso</span></span> |
| <span data-ttu-id="e3d90-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="e3d90-142">ContosoHeaderValue</span></span> |<span data-ttu-id="e3d90-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="e3d90-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="e3d90-144">True</span><span class="sxs-lookup"><span data-stu-id="e3d90-144">True</span></span> |<span data-ttu-id="e3d90-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="e3d90-145">Contoso</span></span> |
| <span data-ttu-id="e3d90-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="e3d90-146">ExpressionProperty</span></span> |<span data-ttu-id="e3d90-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="e3d90-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="e3d90-148">False</span><span class="sxs-lookup"><span data-stu-id="e3d90-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="e3d90-149">속성을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="e3d90-149">To use a property</span></span>
<span data-ttu-id="e3d90-150">정책에서 속성을 사용하려면 다음 예제와 같이 이중 중괄호 쌍 안에 속성 이름을 배치합니다(예: `{{ContosoHeader}}`).</span><span class="sxs-lookup"><span data-stu-id="e3d90-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="e3d90-151">이 예제에서 `ContosoHeader`는 `set-header` 정책의 헤더 이름으로 사용되고, `ContosoHeaderValue`는 해당 헤더의 값으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="e3d90-152">API 관리 게이트웨이에 대한 요청이나 응답 중에 이 정책을 평가하는 경우 `{{ContosoHeader}}` 및 `{{ContosoHeaderValue}}`는 해당 속성 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="e3d90-153">속성은 위 예제에 표시된 대로 전체 특성 또는 요소 값으로 사용될 수 있지만 다음 예제와 같이 리터럴 텍스트 식의 일부로 삽입되거나 결합될 수도 있습니다. `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="e3d90-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="e3d90-154">또한 속성은 정책 식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="e3d90-155">다음 예제에서는 `ExpressionProperty`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="e3d90-156">이 정책을 평가할 때 `{{ExpressionProperty}}`는 해당 값 `@(DateTime.Now.ToString())`으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="e3d90-157">이 값은 정책 식이므로 식이 계산되고 정책이 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="e3d90-158">범위에 속성이 포함된 정책이 있는 작업을 호출하여 개발자 포털에서 이를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="e3d90-159">다음 예제에서는 속성이 있는 이전 두 예제 `set-header` 정책으로 작업이 호출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="e3d90-160">응답에 속성이 있는 정책을 사용하여 구성된 두 개의 사용자 지정 헤더가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![개발자 포털][api-management-send-results]

<span data-ttu-id="e3d90-162">속성이 있는 이전 두 샘플 정책이 포함된 호출에 대한 [API 검사기 추적](api-management-howto-api-inspector.md)을 살펴보면 속성 값이 삽입된 두 개의 `set-header` 정책과 정책 식을 포함하는 속성에 대한 정책 식 계산을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![API 검사기 추적][api-management-api-inspector-trace]

<span data-ttu-id="e3d90-164">속성 값은 정책 식을 포함할 수 있지만 다른 속성을 포함할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="e3d90-165">속성 참조를 포함하는 텍스트가 속성 값에 사용된 경우(예: `Property value text {{MyProperty}}`) 해당 속성 참조는 바뀌지 않으며 속성 값의 일부로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="e3d90-166">속성을 만들려면</span><span class="sxs-lookup"><span data-stu-id="e3d90-166">To create a property</span></span>
<span data-ttu-id="e3d90-167">속성을 만들려면 **속성** 탭에서 **속성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![속성 추가][api-management-properties-add-property-menu]

<span data-ttu-id="e3d90-169">**이름** 및 **값**은 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="e3d90-170">이 속성 값이 암호인 경우 **암호임** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="e3d90-171">속성을 구성하는 데 도움이 되도록 하나 이상의 선택적 태그를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![속성 추가][api-management-properties-add-property]

<span data-ttu-id="e3d90-173">새 속성을 저장하면 **속성 검색** 텍스트 상자가 새 속성의 이름으로 채워지고 새 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="e3d90-174">모든 속성을 표시하려면 **속성 검색** 텍스트 상자를 지우고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![속성][api-management-properties-property-saved]

<span data-ttu-id="e3d90-176">REST API를 사용하여 속성을 만드는 방법에 대한 자세한 내용은 [REST API를 사용하여 속성 만들기](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3d90-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="e3d90-177">속성을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="e3d90-177">To edit a property</span></span>
<span data-ttu-id="e3d90-178">속성을 편집하려면 편집할 속성 옆의 **편집** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![속성 편집][api-management-properties-edit]

<span data-ttu-id="e3d90-180">원하는 항목을 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="e3d90-181">속성 이름을 변경한 경우 해당 속성을 참조하는 모든 정책이 새 이름을 사용하도록 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![속성 편집][api-management-properties-edit-property]

<span data-ttu-id="e3d90-183">REST API를 사용하여 속성을 편집하는 방법에 대한 자세한 내용은 [REST API를 사용하여 속성 편집](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3d90-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="e3d90-184">속성을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="e3d90-184">To delete a property</span></span>
<span data-ttu-id="e3d90-185">속성을 삭제하려면 삭제할 속성 옆의 **삭제** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![속성 삭제][api-management-properties-delete]

<span data-ttu-id="e3d90-187">**예, 삭제합니다.** 를 클릭하여 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-187">Click **Yes, delete it** to confirm.</span></span>

![삭제 확인][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="e3d90-189">속성을 참조하는 정책이 있는 경우 이러한 모든 정책에서 속성을 제거할 때까지 속성을 성공적으로 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="e3d90-190">REST API를 사용하여 속성을 삭제하는 방법에 대한 자세한 내용은 [REST API를 사용하여 속성 삭제](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3d90-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="e3d90-191">속성을 검색하고 필터링하려면</span><span class="sxs-lookup"><span data-stu-id="e3d90-191">To search and filter properties</span></span>
<span data-ttu-id="e3d90-192">**속성** 탭에는 속성을 관리하는 데 유용한 검색 및 필터링 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="e3d90-193">속성 이름으로 속성 목록을 필터링하려면 **속성 검색** 텍스트 상자에 검색 용어를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="e3d90-194">모든 속성을 표시하려면 **속성 검색** 텍스트 상자를 지우고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![검색][api-management-properties-search]

<span data-ttu-id="e3d90-196">태그 값으로 속성 목록을 필터링하려면 **태그로 필터링** 텍스트 상자에 하나 이상의 태그를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="e3d90-197">모든 속성을 표시하려면 **태그로 필터링** 텍스트 상자를 지우고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3d90-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filter][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="e3d90-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3d90-199">Next steps</span></span>
* <span data-ttu-id="e3d90-200">정책 작업에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e3d90-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="e3d90-201">API 관리의 정책</span><span class="sxs-lookup"><span data-stu-id="e3d90-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="e3d90-202">정책 참조</span><span class="sxs-lookup"><span data-stu-id="e3d90-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="e3d90-203">정책 식</span><span class="sxs-lookup"><span data-stu-id="e3d90-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="e3d90-204">비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="e3d90-204">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

