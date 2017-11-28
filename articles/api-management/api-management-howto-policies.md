---
title: "Azure API 관리에서 aaaPolicies | Microsoft Docs"
description: "Toocreate, 편집 하 고 API 관리에서 정책을 구성 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="7ffe5-103">Azure API 관리의 정책</span><span class="sxs-lookup"><span data-stu-id="7ffe5-103">Policies in Azure API Management</span></span>
<span data-ttu-id="7ffe5-104">Azure API 관리에서 정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 hello 시스템의 강력한 기능이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="7ffe5-105">정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="7ffe5-106">인기 있는 문은 XML tooJSON에서 형식 변환을 포함 하 고 호출 toorestrict hello 양을 개발자 로부터 들어오는 호출 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="7ffe5-107">더 많은 정책을 hello 상자 바로 사용할 수 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="7ffe5-108">Hello 참조 [정책 참조] [ Policy Reference] 정책 설명 및 해당 설정의 전체 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="7ffe5-109">Hello API 소비자 및 관리 하는 hello API 사이 있는 hello 게이트웨이 내 정책이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="7ffe5-110">hello 게이트웨이 모든 요청을 수신 하 고 일반적으로 변경 되지 않은 상태로 전달 toohello API 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="7ffe5-111">그러나 변경 내용 tooboth hello 인바운드 요청과 아웃 바운드 응답에 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="7ffe5-112">정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="7ffe5-113">Hello와 같은 일부 정책은 [제어 흐름] [ Control flow] 및 [변수 설정] [ Set variable] 정책은 정책 식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="7ffe5-114">자세한 내용은 [고급 정책][Advanced policies] 및 [정책 식][Policy expressions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="7ffe5-115"><a name="scopes"></a>어떻게 tooconfigure 정책</span><span class="sxs-lookup"><span data-stu-id="7ffe5-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="7ffe5-116">전역으로 또는의 hello 범위에서 정책을 구성할 수 있습니다는 [제품][Product], [API] [ API] 또는 [작업] [Operation].</span><span class="sxs-lookup"><span data-stu-id="7ffe5-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="7ffe5-117">클라이언트는 정책을 tooconfigure hello 게시자 포털에서 toohello 정책 편집기를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![정책 메뉴][policies-menu]

<span data-ttu-id="7ffe5-119">3 개의 주요 구역인 hello 정책 편집기로 구성 됩니다: hello 정책 범위의 (최상위) hello 정책 정의 여기서 정책 (왼쪽) 편집 하 고 hello 문 목록 (오른쪽):</span><span class="sxs-lookup"><span data-stu-id="7ffe5-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![정책 편집기][policies-editor]

<span data-ttu-id="7ffe5-121">toobegin는 hello에 정책을 적용 해야 하는 hello 범위를 먼저 선택 해야 하는 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="7ffe5-122">Hello 아래 스크린샷에서 hello **스타터** 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="7ffe5-123">Note 해당 hello 정사각형 기호 다음 toohello 정책 이름 정책을이 수준에서 적용 이미 되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![범위][policies-scope]

<span data-ttu-id="7ffe5-125">정책이 이미 적용 된 이후 hello 구성은 hello 정의 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![구성][policies-configure]

<span data-ttu-id="7ffe5-127">hello 정책 읽기 전용으로 표시 되는지 처음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="7ffe5-128">순서 tooedit hello 정의 클릭 hello **정책 구성** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![편집][policies-edit]

<span data-ttu-id="7ffe5-130">hello 정책 정의 인바운드 및 아웃 바운드 문의 시퀀스를 설명 하는 간단한 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="7ffe5-131">hello XML hello 정의 창에서 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="7ffe5-132">문 목록 toohello 오른쪽 및 문 적용 가능한 toohello 현재 범위는 활성화 강조; 제공 되며 hello에 나타난 것 처럼 **호출 속도 제한을** 또한 위의 스크린 샷에서 hello에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="7ffe5-133">활성화 된 문을 클릭 하면 추가 됩니다 hello 정의 뷰에 hello 커서의 hello 위치에서 적절 한 XML hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="7ffe5-134">Tooadd hello 정책을 사용 하지 않는 경우 해당 정책에 대 한 hello 올바른 범위에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="7ffe5-135">각 정책 문은 특정 범위 및 정책 섹션에서 사용하도록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="7ffe5-136">tooreview hello 정책 섹션 및 정책에 대 한 범위 확인 hello **사용량** hello에서 해당 정책에 대 한 섹션 [정책 참조][Policy Reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="7ffe5-137">정책 설명의 전체 목록과 해당 설정을 hello에서 사용할 수 있는 [정책 참조][Policy Reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="7ffe5-138">Hello의 hello 콘텐츠 내 hello 커서를 tooadd 들어오는 새 문 toorestrict toospecified IP 주소를 요청 하는 예를 들어 `inbound` XML 요소와 클릭 hello **Restrict 호출자 Ip** 문.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![제한 정책][policies-restrict]

<span data-ttu-id="7ffe5-140">XML 조각 toohello 추가 합니다. `inbound` tooconfigure 문을 hello 하는 방법에 지침을 제공 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="7ffe5-141">toolimit 인바운드 요청 क र च 1.2.3.4는 IP 주소에서 항목만 hello XML을 다음과 같이 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![저장][policies-save]

<span data-ttu-id="7ffe5-143">완료 hello 정책에 대 한 hello 문을 구성 되 면 **저장** hello 변경은 전파 toohello API 관리 게이트웨이 즉시 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="7ffe5-144"><a name="sections"> </a>정책 구성 이해</span><span class="sxs-lookup"><span data-stu-id="7ffe5-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="7ffe5-145">정책은 요청 및 응답의 순서로 실행되는 일련의 명령문입니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="7ffe5-146">hello 구성으로 적절 하 게 나뉘어 `inbound`, `backend`, `outbound`, 및 `on-error` 같은 구성이 hello에 나와 있는 것 처럼 섹션.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="7ffe5-147">Hello에서 hello 요청을 처리 하는 동안 오류가 발생 하는 경우 모든 나머지 단계를 `inbound`, `backend`, 또는 `outbound` 섹션 건너뛰고 hello에 toohello 문 실행이 이동 `on-error` 섹션.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="7ffe5-148">Hello에 정책 문을 배치 하 여 `on-error` 섹션 hello를 사용 하 여 hello 오류를 검토할 수 있습니다 `context.LastError` 속성을 검사 하 고 hello를 사용 하 여 hello 오류 응답을 사용자 지정 `set-body` 정책을 하 고 오류가 발생 한 경우 수행 되는 작업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="7ffe5-149">오류 코드에 대 한 기본 제공 단계 및 hello 정책 문 처리 하는 동안 발생할 수 있는 오류에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="7ffe5-150">자세한 내용은 [API Management 정책에서 오류 처리](https://msdn.microsoft.com/library/azure/mt629506.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="7ffe5-151">정책 (전역, 제품, api 및 작업)의 서로 다른 수준에서 지정할 수 있으므로 hello 구성을 사용 하면 있습니다 toospecify hello 순서 존중 toohello 부모 정책을 사용 하 여 hello 정책 정의 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="7ffe5-152">정책 범위 hello 순서에 따라 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="7ffe5-153">전역 범위</span><span class="sxs-lookup"><span data-stu-id="7ffe5-153">Global scope</span></span>
2. <span data-ttu-id="7ffe5-154">제품 범위</span><span class="sxs-lookup"><span data-stu-id="7ffe5-154">Product scope</span></span>
3. <span data-ttu-id="7ffe5-155">API 범위</span><span class="sxs-lookup"><span data-stu-id="7ffe5-155">API scope</span></span>
4. <span data-ttu-id="7ffe5-156">작업 범위</span><span class="sxs-lookup"><span data-stu-id="7ffe5-156">Operation scope</span></span>

<span data-ttu-id="7ffe5-157">hello 그 안에서 문에서 hello toohello 배치에 따라 `base` 요소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="7ffe5-158">부모 정책 없음 및 hello를 사용 하 여 글로벌 정책에 `<base>` 에 요소에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="7ffe5-159">예를 들어 hello 전역 수준 및 API에 대해 구성 된 정책에서 정책을 경우 다음 해당 특정 API가 사용 될 때마다 두 정책이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="7ffe5-160">API 관리의 결합 된 정책 문을 hello 기본 요소를 통해 결정적 순서 지정을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="7ffe5-161">Hello 예제 정책 정의에 위의 hello `cross-domain` 차례로 하는 더 높은 정책을 hello 올 수 전에 문을 실행 합니다 `find-and-replace` 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="7ffe5-162">hello hello 정책 편집기에서 현재 범위에서 toosee hello 정책 클릭 **선택한 범위에 대 한 실제 정책 다시 계산**합니다.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ffe5-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ffe5-163">Next steps</span></span>
<span data-ttu-id="7ffe5-164">다음과 같은 정책 식 관련 비디오를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7ffe5-164">Check out following video on policy expressions.</span></span>

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
