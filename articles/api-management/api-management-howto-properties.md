---
title: "Azure API 관리 정책에 aaaHow toouse 속성"
description: "자세한 내용은 방법 Azure API 관리 정책에 toouse 속성입니다."
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
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="7ee29-103">어떻게 Azure API 관리 정책에 toouse 속성</span><span class="sxs-lookup"><span data-stu-id="7ee29-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="7ee29-104">API 관리 정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 hello 시스템의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="7ee29-105">정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="7ee29-106">정책 설명은 리터럴 텍스트 값, 정책 식 및 속성을 사용하여 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="7ee29-107">각 API 관리 서비스 인스턴스는 전역 toohello 서비스 인스턴스가 포함 된 키/값 쌍의 properties 컬렉션.</span><span class="sxs-lookup"><span data-stu-id="7ee29-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="7ee29-108">이러한 속성에는 모든 API 구성 및 정책에서 상수 문자열 값을 사용 하는 toomanage 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="7ee29-109">각 속성에는 hello 특성 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="7ee29-110">특성</span><span class="sxs-lookup"><span data-stu-id="7ee29-110">Attribute</span></span> | <span data-ttu-id="7ee29-111">형식</span><span class="sxs-lookup"><span data-stu-id="7ee29-111">Type</span></span> | <span data-ttu-id="7ee29-112">설명</span><span class="sxs-lookup"><span data-stu-id="7ee29-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ee29-113">Name</span><span class="sxs-lookup"><span data-stu-id="7ee29-113">Name</span></span> |<span data-ttu-id="7ee29-114">string</span><span class="sxs-lookup"><span data-stu-id="7ee29-114">string</span></span> |<span data-ttu-id="7ee29-115">hello 속성의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-115">hello name of hello property.</span></span> <span data-ttu-id="7ee29-116">문자, 숫자, 마침표, 대시 및 밑줄 문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="7ee29-117">값</span><span class="sxs-lookup"><span data-stu-id="7ee29-117">Value</span></span> |<span data-ttu-id="7ee29-118">string</span><span class="sxs-lookup"><span data-stu-id="7ee29-118">string</span></span> |<span data-ttu-id="7ee29-119">hello hello 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-119">hello value of hello property.</span></span> <span data-ttu-id="7ee29-120">비워 두거나 공백만으로 구성될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="7ee29-121">Secret</span><span class="sxs-lookup"><span data-stu-id="7ee29-121">Secret</span></span> |<span data-ttu-id="7ee29-122">부울</span><span class="sxs-lookup"><span data-stu-id="7ee29-122">boolean</span></span> |<span data-ttu-id="7ee29-123">여부 hello 값 암호 이며을 암호화할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="7ee29-124">태그들</span><span class="sxs-lookup"><span data-stu-id="7ee29-124">Tags</span></span> |<span data-ttu-id="7ee29-125">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="7ee29-125">array of string</span></span> |<span data-ttu-id="7ee29-126">선택 사항 태그를 삽입 하는 사용 되는 toofilter hello 속성 목록 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="7ee29-127">속성은 hello hello 게시자 포털에 구성 **속성** 탭 합니다. 다음 예제는 hello, 세 가지 속성이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![properties][api-management-properties]

<span data-ttu-id="7ee29-129">속성 값은 리터럴 문자열 및 [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx)을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="7ee29-130">hello 다음 표에 hello 이전 세 샘플 속성 및 해당 특성 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="7ee29-131">값을 hello `ExpressionProperty` 은 포함 하는 문자열을 반환 하는 정책 식을 hello 현재 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="7ee29-132">속성을 hello `ContosoHeaderValue` 은 표시 되어는 암호로 있으므로 해당 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="7ee29-133">이름</span><span class="sxs-lookup"><span data-stu-id="7ee29-133">Name</span></span> | <span data-ttu-id="7ee29-134">값</span><span class="sxs-lookup"><span data-stu-id="7ee29-134">Value</span></span> | <span data-ttu-id="7ee29-135">Secret</span><span class="sxs-lookup"><span data-stu-id="7ee29-135">Secret</span></span> | <span data-ttu-id="7ee29-136">태그</span><span class="sxs-lookup"><span data-stu-id="7ee29-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7ee29-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="7ee29-137">ContosoHeader</span></span> |<span data-ttu-id="7ee29-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="7ee29-138">TrackingId</span></span> |<span data-ttu-id="7ee29-139">False</span><span class="sxs-lookup"><span data-stu-id="7ee29-139">False</span></span> |<span data-ttu-id="7ee29-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="7ee29-140">Contoso</span></span> |
| <span data-ttu-id="7ee29-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="7ee29-141">ContosoHeaderValue</span></span> |<span data-ttu-id="7ee29-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="7ee29-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="7ee29-143">True</span><span class="sxs-lookup"><span data-stu-id="7ee29-143">True</span></span> |<span data-ttu-id="7ee29-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="7ee29-144">Contoso</span></span> |
| <span data-ttu-id="7ee29-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="7ee29-145">ExpressionProperty</span></span> |<span data-ttu-id="7ee29-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="7ee29-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="7ee29-147">False</span><span class="sxs-lookup"><span data-stu-id="7ee29-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="7ee29-148">toouse 속성</span><span class="sxs-lookup"><span data-stu-id="7ee29-148">toouse a property</span></span>
<span data-ttu-id="7ee29-149">정책에서 속성 toouse와 같은 이중 중괄호 쌍 내 위치 hello 속성 이름은 `{{ContosoHeader}}`hello 다음 예제에에서 나온 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="7ee29-150">이 예제에서는 `ContosoHeader` 에 헤더의 hello 이름으로 사용 되는 `set-header` 정책 및 `ContosoHeaderValue` 해당 헤더의 hello 값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="7ee29-151">이 정책은 요청 또는 응답 toohello API 관리 게이트웨이 중 평가 되는 경우 `{{ContosoHeader}}` 및 `{{ContosoHeaderValue}}` 해당 각 속성 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="7ee29-152">전체 특성 또는 요소 값 hello 앞의 예제에 표시 된 대로 속성을 사용할 수 있지만 수에 삽입 하거나 수도 hello 다음 예제와 같이 리터럴 텍스트 식의 일부와 결합:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="7ee29-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="7ee29-153">또한 속성은 정책 식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="7ee29-154">다음 예제는 hello에서 hello `ExpressionProperty` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="7ee29-155">이 정책을 평가할 때 `{{ExpressionProperty}}`는 해당 값 `@(DateTime.Now.ToString())`으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="7ee29-156">Hello 값에는 정책 식 이므로 hello 식이 계산 되 고 hello 정책 실행을 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="7ee29-157">에서 테스트할 수 있습니다이 out hello 개발자 포털에 속성을 가진 정책이 범위에는 작업을 호출 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="7ee29-158">다음 예제는 hello, 작업 hello 두 개의 이전 예제와 호출 `set-header` 속성을 사용 하 여 정책을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="7ee29-159">참고 hello 응답 속성을 가진 정책을 사용 하 여 구성 된 두 개의 사용자 지정 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![개발자 포털][api-management-send-results]

<span data-ttu-id="7ee29-161">Hello 보면 [관리자 API 추적](api-management-howto-api-inspector.md) hello 두 이전 샘플 정책을 속성을 포함 하는 호출에 대 한 두 hello를 볼 수 있습니다 `set-header` hello 정책 식 뿐만 아니라 삽입 된 hello 속성 값을 사용 하 여 정책을 hello 정책 식을 포함 하는 hello 속성에 대 한 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![API 검사기 추적][api-management-api-inspector-trace]

<span data-ttu-id="7ee29-163">속성 값은 정책 식을 포함할 수 있지만 다른 속성을 포함할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="7ee29-164">속성 참조가 포함 된 텍스트와 같은 속성 값에 사용 되 면 `Property value text {{MyProperty}}`, 속성 참조 되지 및 hello 속성 값의 일부분으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="7ee29-165">toocreate 속성</span><span class="sxs-lookup"><span data-stu-id="7ee29-165">toocreate a property</span></span>
<span data-ttu-id="7ee29-166">toocreate 속성을 클릭 하 여 **속성 추가** hello에 **속성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![속성 추가][api-management-properties-add-property-menu]

<span data-ttu-id="7ee29-168">**이름** 및 **값**은 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="7ee29-169">이 속성 값이 되는 암호를 확인 hello **이 암호는** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="7ee29-170">속성을 구성 된 하나 이상의 선택적 태그 toohelp를 입력 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![속성 추가][api-management-properties-add-property]

<span data-ttu-id="7ee29-172">새 속성을 저장할 때 hello **검색 속성** 텍스트 상자는 hello 새 속성의 hello 이름으로 채워지고 hello 새 속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="7ee29-173">모든 속성의 선택을 취소 toodisplay hello **검색 속성** textbox enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![properties][api-management-properties-property-saved]

<span data-ttu-id="7ee29-175">Hello REST API를 사용 하는 속성을 만드는 방법에 대 한 정보를 참조 하십시오. [hello REST API를 사용 하 여 속성을 만들](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="7ee29-176">tooedit 속성</span><span class="sxs-lookup"><span data-stu-id="7ee29-176">tooedit a property</span></span>
<span data-ttu-id="7ee29-177">tooedit 속성을 클릭 하 여 **편집** hello 속성 tooedit 옆에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![속성 편집][api-management-properties-edit]

<span data-ttu-id="7ee29-179">원하는 항목을 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="7ee29-180">Hello 속성 이름을 변경 하면 해당 속성을 참조 하는 모든 정책은 자동으로 업데이트 된 toouse hello에 대 한 새 이름을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![속성 편집][api-management-properties-edit-property]

<span data-ttu-id="7ee29-182">Hello REST API를 사용 하는 속성을 편집에 대 한 자세한 내용은 참조 하십시오. [hello REST API를 사용 하는 속성을 편집](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="7ee29-183">toodelete 속성</span><span class="sxs-lookup"><span data-stu-id="7ee29-183">toodelete a property</span></span>
<span data-ttu-id="7ee29-184">toodelete 속성을 클릭 하 여 **삭제** hello 속성 toodelete 옆에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![속성 삭제][api-management-properties-delete]

<span data-ttu-id="7ee29-186">클릭 **예, 삭제할** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-186">Click **Yes, delete it** tooconfirm.</span></span>

![삭제 확인][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="7ee29-188">Hello 속성은 정책에 의해 참조 되는 경우 수 없게 됩니다 toosuccessfully가 hello 속성을 사용 하는 모든 정책에서 제거할 때까지 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="7ee29-189">Hello REST API를 사용 하는 속성을 삭제에 대 한 정보를 참조 하십시오. [hello REST API를 사용 하 여 속성 삭제](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="7ee29-190">toosearch 및 필터 속성</span><span class="sxs-lookup"><span data-stu-id="7ee29-190">toosearch and filter properties</span></span>
<span data-ttu-id="7ee29-191">hello **속성** 탭 검색 및 필터링 기능 toohelp 프로그램 속성 관리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="7ee29-192">hello에 검색 용어를 입력 하는 속성 이름으로 toofilter hello 속성 목록 **검색 속성** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="7ee29-193">모든 속성의 선택을 취소 toodisplay hello **검색 속성** textbox enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![검색][api-management-properties-search]

<span data-ttu-id="7ee29-195">태그 값으로 toofilter hello 속성 목록 hello에 하나 이상의 태그를 입력 **태그로 필터** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="7ee29-196">모든 속성의 선택을 취소 toodisplay hello **태그로 필터** textbox enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ee29-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filter][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="7ee29-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ee29-198">Next steps</span></span>
* <span data-ttu-id="7ee29-199">정책 작업에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7ee29-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="7ee29-200">API 관리의 정책</span><span class="sxs-lookup"><span data-stu-id="7ee29-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="7ee29-201">정책 참조</span><span class="sxs-lookup"><span data-stu-id="7ee29-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="7ee29-202">정책 식</span><span class="sxs-lookup"><span data-stu-id="7ee29-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="7ee29-203">비디오 개요 보기</span><span class="sxs-lookup"><span data-stu-id="7ee29-203">Watch a video overview</span></span>
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

