---
title: "Azure API 관리의 정책 | Microsoft Docs"
description: "API 관리에서 정책을 만들고 편집하고 구성하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="85998-103">Azure API 관리의 정책</span><span class="sxs-lookup"><span data-stu-id="85998-103">Policies in Azure API Management</span></span>
<span data-ttu-id="85998-104">Azure API 관리에서 정책은 게시자가 구성을 통해 API 동작을 변경할 수 있도록 하는 시스템의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="85998-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="85998-105">정책은 API의 요청이나 응답에 따라 순차적으로 실행되는 명령문의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="85998-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="85998-106">많이 사용되는 명령문에는 XML에서 JSON으로 형식 변환, 개발자로부터 들어오는 호출의 양을 제한하는 호출 비율 제한 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="85998-107">다양한 다른 정책도 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="85998-108">정책 명령문 및 설정의 전체 목록은 [정책 참조][Policy Reference] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="85998-109">정책은 API 소비자와 관리되는 API 간에 있는 게이트웨이 내에서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="85998-110">게이트웨이는 모든 요청을 수신하고 보통 변경하지 않은 상태로 기본 API에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="85998-111">그러나 정책은 인바운드 요청과 아웃바운드 응답 모두에 변경 내용을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="85998-112">정책이 다르게 지정하지 않는 한 정책 식은 어떤 API 관리 정책에서든 특성 값 또는 텍스트 값으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="85998-113">[제어 흐름][Control flow] 및 [변수 설정][Set variable] 정책 등의 일부 정책은 정책 식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="85998-114">자세한 내용은 [고급 정책][Advanced policies] 및 [정책 식][Policy expressions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="85998-115"><a name="scopes"> </a>정책을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="85998-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="85998-116">정책을 글로벌로 구성하거나 [제품][Product], [API][API] 또는 [작업][Operation] 범위로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="85998-117">정책을 구성하려면 게시자 포털의 정책 편집기로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![정책 메뉴][policies-menu]

<span data-ttu-id="85998-119">정책 편집기는 정책 범위(위쪽), 정책이 편집되는 정책 정의(왼쪽), 설명 목록(오른쪽)의 세 가지 주 섹션으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![정책 편집기][policies-editor]

<span data-ttu-id="85998-121">정책을 구성하려면 먼저 정책을 적용할 범위를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="85998-122">아래 스크린샷에서는 **Starter** 제품이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="85998-123">정책 이름 옆의 사각형 기호는 정책이 이 수준에서 이미 적용되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85998-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![범위][policies-scope]

<span data-ttu-id="85998-125">정책이 이미 적용되었으므로 구성은 정의 뷰에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![구성][policies-configure]

<span data-ttu-id="85998-127">정책은 처음에 읽기 전용으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="85998-128">정의를 편집하려면 **정책 구성** 작업을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![편집][policies-edit]

<span data-ttu-id="85998-130">정책 정의는 일련의 인바운드 및 아웃바운드 명령문을 설명하는 단순한 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="85998-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="85998-131">정의 창에서 XML을 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="85998-132">명령문 목록이 오른쪽에 제공되고 현재 범위에 적용할 수 있는 명령문이 사용 가능해지며 강조 표시됩니다. 위의 스크린샷에서는 **호출 비율 제한** 문이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="85998-133">사용할 수 있는 명령문을 클릭하면 정의 뷰에서 커서의 위치에 적절한 XML이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="85998-134">추가하려는 정책이 활성화되지 않는 경우 해당 정책의 올바른 범위에 속하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="85998-135">각 정책 문은 특정 범위 및 정책 섹션에서 사용하도록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="85998-136">정책의 정책 섹션 및 범위를 검토하려면 **정책 참조** 에서 해당 정책에 대한 [사용][Policy Reference]섹션을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="85998-137">정책 명령문 및 설정의 전체 목록은 [정책 참조][Policy Reference]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="85998-138">예를 들어 들어오는 요청을 지정된 IP 주소로 제한하는 새로운 문을 추가하려면 `inbound` XML 요소의 콘텐츠 바로 안에 커서를 놓고 **호출자 IP 제한** 문을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![제한 정책][policies-restrict]

<span data-ttu-id="85998-140">그러면 명령문을 구성하는 방법에 대한 참고 자료를 제공하는 XML 코드 조각이 `inbound` 요소에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="85998-141">인바운드 요청을 제한하여 1.2.3.4의 IP 주소에서 들어오는 요청만 허용하려면 다음과 같이 XML을 수정하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![저장][policies-save]

<span data-ttu-id="85998-143">정책에 대한 명령문을 구성한 후에는 **저장**을 클릭합니다. 그러면 변경 내용이 바로 API Management 게이트웨이에 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="85998-144"><a name="sections"> </a>정책 구성 이해</span><span class="sxs-lookup"><span data-stu-id="85998-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="85998-145">정책은 요청 및 응답의 순서로 실행되는 일련의 명령문입니다.</span><span class="sxs-lookup"><span data-stu-id="85998-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="85998-146">다음 구성에서 표시된 대로 `inbound`, `backend`, `outbound` 및 `on-error` 섹션으로 적절히 구성을 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="85998-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="85998-147">요청을 처리하는 동안 오류가 발생하는 경우 `inbound`, `backend` 또는 `outbound` 섹션에 남아 있는 모든 단계를 건너뛰고 `on-error` 섹션의 문을 바로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="85998-148">`on-error` 섹션에 정책 문을 배치하면 `context.LastError` 속성을 사용하여 오류를 검토할 수 있으며 `set-body` 정책을 사용하여 오류 응답을 검사하고 사용자 지정할 수 있습니다. 그리고 오류가 발생하면 수행할 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="85998-149">기본 제공 단계에 대한 오류 코드와 정책 문을 처리하는 동안 발생할 수 있는 오류에 대한 오류 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="85998-150">자세한 내용은 [API Management 정책에서 오류 처리](https://msdn.microsoft.com/library/azure/mt629506.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="85998-151">정책은 여러 수준(전역, 제품, api 및 작업)으로 지정할 수 있으므로, 구성을 통해 부모 정책과 관련하여 정책 정의의 명령문이 실행되는 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="85998-152">정책 범위는 다음 순서로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="85998-153">전역 범위</span><span class="sxs-lookup"><span data-stu-id="85998-153">Global scope</span></span>
2. <span data-ttu-id="85998-154">제품 범위</span><span class="sxs-lookup"><span data-stu-id="85998-154">Product scope</span></span>
3. <span data-ttu-id="85998-155">API 범위</span><span class="sxs-lookup"><span data-stu-id="85998-155">API scope</span></span>
4. <span data-ttu-id="85998-156">작업 범위</span><span class="sxs-lookup"><span data-stu-id="85998-156">Operation scope</span></span>

<span data-ttu-id="85998-157">정책 범위 내의 문은 `base` 요소(있는 경우)의 위치에 따라 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="85998-158">글로벌 정책에는 부모 정책이 없으며 해당 정책 안의 `<base>` 요소를 사용해도 아무 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85998-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="85998-159">예를 들어 글로벌 수준의 정책 및 API에 대해 구성된 정책이 있는 경우 특정 API가 사용될 때마다 두 정책이 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="85998-160">API 관리는 기본 요소를 통해 결합된 정책 명령문의 결정적인 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="85998-161">위의 정책 정의 예제에서는 상위 정책 전에 `cross-domain` 문이 실행된 다음 `find-and-replace` 정책이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="85998-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="85998-162">정책 편집기에서 현재 범위의 정책을 보려면 **Recalculate effective policy for selected scope**(선택한 범위에 대한 실제 정책 다시 계산)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85998-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85998-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85998-163">Next steps</span></span>
<span data-ttu-id="85998-164">다음과 같은 정책 식 관련 비디오를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="85998-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
