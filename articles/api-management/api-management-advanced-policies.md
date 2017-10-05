---
title: "Azure API Management 고급 정책 | Microsoft Docs"
description: "Azure API Management에 사용할 수 있는 고급 정책에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="cd644-103">API Management 고급 정책</span><span class="sxs-lookup"><span data-stu-id="cd644-103">API Management advanced policies</span></span>
<span data-ttu-id="cd644-104">이 항목에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="cd644-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="cd644-106"><a name="AdvancedPolicies"></a> 고급 정책</span><span class="sxs-lookup"><span data-stu-id="cd644-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="cd644-107">[흐름 제어](api-management-advanced-policies.md#choose) - 부울 [식](api-management-policy-expressions.md)의 평가 결과에 따라 정책 문을 조건부로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="cd644-108">[요청 전달](#ForwardRequest) - 백 엔드 서비스에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="cd644-109">[동시성 제한](#LimitConcurrency) - 지정된 정책이 한 번에 지정된 요청 수를 초과해서 실행하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="cd644-110">[이벤트 허브에 기록](#log-to-eventhub) - 로거 엔터티가 정의한 이벤트 허브에 지정된 형식으로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="cd644-111">[모의 응답](#mock-response) - 파이프라인 실행을 중단하고 호출자에게 직접 모의 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="cd644-112">[다시 시도](#Retry) - 조건이 충족될 때까지 포함된 정책 문을 실행하도록 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="cd644-113">실행은 지정된 시간 간격으로 최대 지정된 재시도 횟수까지 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="cd644-114">[응답 반환](#ReturnResponse) - 파이프라인 실행을 중단하고 호출자에게 직접 지정된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="cd644-115">[단방향 요청 전송](#SendOneWayRequest) - 지정된 URL에 대한 응답을 기다리지 않고 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="cd644-116">[요청 전송](#SendRequest) - 지정된 URL로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="cd644-117">[HTTP 프록시 설정](#SetHttpProxy) - HTTP 프록시를 통해 전달되는 요청을 라우팅할수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="cd644-118">[요청 메서드 설정](#SetRequestMethod) - 요청에 대한 HTTP 메서드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="cd644-119">[상태 코드 설정](#SetStatus) - 지정된 값으로 HTTP 상태 코드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="cd644-120">[변수 설정](api-management-advanced-policies.md#set-variable) - 나중에 액세스할 수 있도록 명명된 [context](api-management-policy-expressions.md#ContextVariables) 변수의 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="cd644-121">[추적](#Trace) - [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력에 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="cd644-122">[대기](#Wait) - 계속하기 전에 완료할 포함된 [요청 전송](api-management-advanced-policies.md#SendRequest), [캐시에서 값 가져오기](api-management-caching-policies.md#GetFromCacheByKey) 또는 [제어 흐름](api-management-advanced-policies.md#choose) 정책 등을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="cd644-123"><a name="choose"></a> 흐름 제어</span><span class="sxs-lookup"><span data-stu-id="cd644-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="cd644-124">`choose` 정책은 프로그래밍 언어의 if-then-else 또는 switch 생성과 마찬가지로 Boolean 식의 평가 결과에 따라 포함된 정책 문을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="cd644-125"><a name="ChoosePolicyStatement"></a> 정책 문</span><span class="sxs-lookup"><span data-stu-id="cd644-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="cd644-126">제어 흐름 정책에는 `<when/>` 요소가 하나 이상 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="cd644-127">`<otherwise/>` 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="cd644-128">정책 내에 표시되는 순서대로 `<when/>` 요소의 조건이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="cd644-129">조건 특성이 `true`인 첫 번째 `<when/>` 요소 내에 포함된 정책 문이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="cd644-130">모든 `<when/>` 요소 조건 특성이 `false`인 경우 `<otherwise/>` 요소 내에 포함된 정책(있는 경우)이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="cd644-131">예</span><span class="sxs-lookup"><span data-stu-id="cd644-131">Examples</span></span>  
  
####  <span data-ttu-id="cd644-132"><a name="ChooseExample"></a> 예</span><span class="sxs-lookup"><span data-stu-id="cd644-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="cd644-133">다음 예에서는 [set-variable](api-management-advanced-policies.md#set-variable) 정책과 두 개의 제어 흐름 정책을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="cd644-134">변수 설정 정책은 인바운드 섹션에 있으며 `User-Agent` 요청 헤더에 `iPad` 또는 `iPhone` 텍스트가 포함되는 경우 true로 설정되는 `isMobile` 부울 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="cd644-135">첫 번째 제어 흐름 정책도 인바운드 섹션에 있으며 `isMobile` 컨텍스트 변수 값에 따라 두 [쿼리 문자열 매개 변수 설정](api-management-transformation-policies.md#SetQueryStringParameter) 정책 중 하나를 조건부로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="cd644-136">두 번째 제어 흐름 정책은 아웃바운드 섹션에 있으며 `isMobile`이 `true`로 설정될 때 [XML을 JSON으로 변환](api-management-transformation-policies.md#ConvertXMLtoJSON) 정책을 조건부로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="cd644-137">예</span><span class="sxs-lookup"><span data-stu-id="cd644-137">Example</span></span>  
 <span data-ttu-id="cd644-138">이 예에서는 `Starter` 제품을 사용할 때 백 엔드 서비스에서 수신한 응답에서 데이터 요소를 제거하여 콘텐츠 필터링을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="cd644-139">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 34분 30초 재생 시점까지 빨리 진행하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="cd644-140">31분 50초 재생 시점에서 시작하는 [Dark Sky Forecast API](https://developer.forecast.io/)(영문) 개요를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-141">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-141">Elements</span></span>  
  
|<span data-ttu-id="cd644-142">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-142">Element</span></span>|<span data-ttu-id="cd644-143">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-143">Description</span></span>|<span data-ttu-id="cd644-144">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-145">choose</span><span class="sxs-lookup"><span data-stu-id="cd644-145">choose</span></span>|<span data-ttu-id="cd644-146">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-146">Root element.</span></span>|<span data-ttu-id="cd644-147">예</span><span class="sxs-lookup"><span data-stu-id="cd644-147">Yes</span></span>|  
|<span data-ttu-id="cd644-148">when</span><span class="sxs-lookup"><span data-stu-id="cd644-148">when</span></span>|<span data-ttu-id="cd644-149">`choose` 정책의 `if` 또는 `ifelse` 부분에 사용할 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="cd644-150">`choose` 정책에 여러 `when` 섹션이 있는 경우 순차적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="cd644-151">when 요소의 `condition`이 `true`로 평가되면 `when` 조건이 더 이상 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="cd644-152">예</span><span class="sxs-lookup"><span data-stu-id="cd644-152">Yes</span></span>|  
|<span data-ttu-id="cd644-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="cd644-153">otherwise</span></span>|<span data-ttu-id="cd644-154">`true`로 평가되는 `when` 조건이 없으면 사용할 정책 조각을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="cd644-155">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-156">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-156">Attributes</span></span>  
  
|<span data-ttu-id="cd644-157">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-157">Attribute</span></span>|<span data-ttu-id="cd644-158">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-158">Description</span></span>|<span data-ttu-id="cd644-159">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="cd644-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="cd644-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="cd644-161">포함하는 `when` 정책 문이 평가될 때 평가할 Boolean 식 또는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="cd644-162">예</span><span class="sxs-lookup"><span data-stu-id="cd644-162">Yes</span></span>|  
  
###  <span data-ttu-id="cd644-163"><a name="ChooseUsage"></a> 사용 방법</span><span class="sxs-lookup"><span data-stu-id="cd644-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="cd644-164">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-165">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-166">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-167"><a name="ForwardRequest"></a> 요청 전달</span><span class="sxs-lookup"><span data-stu-id="cd644-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="cd644-168">`forward-request` 정책은 들어오는 요청을 요청 [컨텍스트](api-management-policy-expressions.md#ContextVariables)에 지정된 백 엔드 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="cd644-169">백 엔드 서비스 URL이 API [설정](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings)에 지정되고 [백 엔드 서비스 설정](api-management-transformation-policies.md) 정책을 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="cd644-170">요청에서 이 정책을 제거하면 백 엔드 서비스로 전달되지 않고 인바운드 섹션에 있는 정책이 성공적으로 완료되는 즉시 아웃바운드 섹션에 있는 정책이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-171">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="cd644-172">예</span><span class="sxs-lookup"><span data-stu-id="cd644-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="cd644-173">예제</span><span class="sxs-lookup"><span data-stu-id="cd644-173">Example</span></span>  
 <span data-ttu-id="cd644-174">다음 API 수준 정책은 60초의 시간 초과 간격으로 모든 요청을 백 엔드 서비스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="cd644-175">예</span><span class="sxs-lookup"><span data-stu-id="cd644-175">Example</span></span>  
 <span data-ttu-id="cd644-176">이 작업 수준 정책은 `base` 요소를 사용하여 상위 API 수준 범위에서 백 엔드 정책을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="cd644-177">예</span><span class="sxs-lookup"><span data-stu-id="cd644-177">Example</span></span>  
 <span data-ttu-id="cd644-178">이 작업 수준 정책은 120의 시간 초과로 모든 요청을 백 엔드 서비스로 명시적으로 전달하며 상위 API 수준 백 엔드 정책을 상속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="cd644-179">예제</span><span class="sxs-lookup"><span data-stu-id="cd644-179">Example</span></span>  
 <span data-ttu-id="cd644-180">이 작업 수준 정책은 요청을 백 엔드 서비스로 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-181">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-181">Elements</span></span>  
  
|<span data-ttu-id="cd644-182">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-182">Element</span></span>|<span data-ttu-id="cd644-183">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-183">Description</span></span>|<span data-ttu-id="cd644-184">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="cd644-185">forward-request</span></span>|<span data-ttu-id="cd644-186">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-186">Root element.</span></span>|<span data-ttu-id="cd644-187">예</span><span class="sxs-lookup"><span data-stu-id="cd644-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-188">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-188">Attributes</span></span>  
  
|<span data-ttu-id="cd644-189">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-189">Attribute</span></span>|<span data-ttu-id="cd644-190">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-190">Description</span></span>|<span data-ttu-id="cd644-191">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-191">Required</span></span>|<span data-ttu-id="cd644-192">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="cd644-193">timeout="integer"</span></span>|<span data-ttu-id="cd644-194">백 엔드 서비스 호출이 실패하는 시간 초과 간격(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="cd644-195">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-195">No</span></span>|<span data-ttu-id="cd644-196">시간 초과 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-196">No timeout</span></span>|  
|<span data-ttu-id="cd644-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="cd644-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="cd644-198">백 엔드 서비스의 리디렉션 뒤에 게이트웨이가 있는지 또는 호출자에게 반환되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="cd644-199">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-199">No</span></span>|<span data-ttu-id="cd644-200">false</span><span class="sxs-lookup"><span data-stu-id="cd644-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-201">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-201">Usage</span></span>  
 <span data-ttu-id="cd644-202">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-203">**정책 섹션:** backend</span><span class="sxs-lookup"><span data-stu-id="cd644-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="cd644-204">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-205"><a name="LimitConcurrency"></a> 동시성 제한</span><span class="sxs-lookup"><span data-stu-id="cd644-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="cd644-206">`limit-concurrency` 정책이 한 번에 지정된 요청 수를 초과해서 실행하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="cd644-207">임계값을 초과할 때 최대 큐 길이가 될 때까지 새 요청이 큐에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="cd644-208">큐가 고갈되면 새 요청은 즉시 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="cd644-209"><a name="LimitConcurrencyStatement"></a> 정책 문</span><span class="sxs-lookup"><span data-stu-id="cd644-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="cd644-210">예</span><span class="sxs-lookup"><span data-stu-id="cd644-210">Examples</span></span>  
  
####  <span data-ttu-id="cd644-211"><a name="ChooseExample"></a> 예</span><span class="sxs-lookup"><span data-stu-id="cd644-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="cd644-212">다음 예제에서는 컨텍스트 변수 값에 따라 백 엔드로 전달되는 요청 수를 제한하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="cd644-213">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-213">Elements</span></span>  
  
|<span data-ttu-id="cd644-214">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-214">Element</span></span>|<span data-ttu-id="cd644-215">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-215">Description</span></span>|<span data-ttu-id="cd644-216">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="cd644-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="cd644-217">limit-concurrency</span></span>|<span data-ttu-id="cd644-218">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-218">Root element.</span></span>|<span data-ttu-id="cd644-219">예</span><span class="sxs-lookup"><span data-stu-id="cd644-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-220">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-220">Attributes</span></span>  
  
|<span data-ttu-id="cd644-221">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-221">Attribute</span></span>|<span data-ttu-id="cd644-222">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-222">Description</span></span>|<span data-ttu-id="cd644-223">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-223">Required</span></span>|<span data-ttu-id="cd644-224">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="cd644-225">key</span><span class="sxs-lookup"><span data-stu-id="cd644-225">key</span></span>|<span data-ttu-id="cd644-226">문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-226">A string.</span></span> <span data-ttu-id="cd644-227">허용되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-227">Expression allowed.</span></span> <span data-ttu-id="cd644-228">동시성 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="cd644-229">여러 정책에서 공유될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="cd644-230">예</span><span class="sxs-lookup"><span data-stu-id="cd644-230">Yes</span></span>|<span data-ttu-id="cd644-231">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-231">N/A</span></span>|  
|<span data-ttu-id="cd644-232">max-count</span><span class="sxs-lookup"><span data-stu-id="cd644-232">max-count</span></span>|<span data-ttu-id="cd644-233">정수입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-233">An integer.</span></span> <span data-ttu-id="cd644-234">정책에 들어올 수 있는 요청의 최대 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="cd644-235">예</span><span class="sxs-lookup"><span data-stu-id="cd644-235">Yes</span></span>|<span data-ttu-id="cd644-236">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-236">N/A</span></span>|  
|<span data-ttu-id="cd644-237">시간 제한</span><span class="sxs-lookup"><span data-stu-id="cd644-237">timeout</span></span>|<span data-ttu-id="cd644-238">정수입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-238">An integer.</span></span> <span data-ttu-id="cd644-239">허용되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-239">Expression allowed.</span></span> <span data-ttu-id="cd644-240">요청이 "403 너무 많은 요청"을 표시하며 실패하기 전에 범위에 포함되기 위해 대기해야 하는 시간(초)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="cd644-241">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-241">No</span></span>|<span data-ttu-id="cd644-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="cd644-242">Infinity</span></span>|  
|<span data-ttu-id="cd644-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="cd644-243">max-queue-length</span></span>|<span data-ttu-id="cd644-244">정수입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-244">An integer.</span></span> <span data-ttu-id="cd644-245">허용되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-245">Expression allowed.</span></span> <span data-ttu-id="cd644-246">최대 큐 길이를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="cd644-247">큐가 고갈되는 즉시, 이 정책에 들어오려고 하는 수신 요청은 "403 너무 많은 요청"을 나타내며 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="cd644-248">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-248">No</span></span>|<span data-ttu-id="cd644-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="cd644-249">Infinity</span></span>|  
  
###  <span data-ttu-id="cd644-250"><a name="ChooseUsage"></a> 사용 방법</span><span class="sxs-lookup"><span data-stu-id="cd644-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="cd644-251">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-252">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-253">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="cd644-254"><a name="log-to-eventhub"></a> 이벤트 허브에 기록</span><span class="sxs-lookup"><span data-stu-id="cd644-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="cd644-255">`log-to-eventhub` 정책은 로거 엔터티가 정의한 이벤트 허브에 지정된 형식으로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="cd644-256">이름에서 알 수 있듯이 이 정책은 온라인 또는 오프라인 분석을 위해 선택한 요청 또는 응답 컨텍스트 정보를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="cd644-257">이벤트 허브 구성 및 이벤트 로깅에 대한 단계별 가이드는 [Azure Event Hubs로 API Management 이벤트를 기록하는 방법](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-258">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-259">예</span><span class="sxs-lookup"><span data-stu-id="cd644-259">Example</span></span>  
 <span data-ttu-id="cd644-260">Event Hubs에 기록할 값으로 모든 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="cd644-261">이 예제에서는 모든 인바운드 호출에 대한 날짜 및 시간, 배포 서비스 이름, 요청 ID, IP 주소, 작업 이름이 `contoso-logger` ID로 등록된 이벤트 허브 로거에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-262">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-262">Elements</span></span>  
  
|<span data-ttu-id="cd644-263">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-263">Element</span></span>|<span data-ttu-id="cd644-264">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-264">Description</span></span>|<span data-ttu-id="cd644-265">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="cd644-266">log-to-eventhub</span></span>|<span data-ttu-id="cd644-267">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-267">Root element.</span></span> <span data-ttu-id="cd644-268">이 요소 값은 이벤트 허브에 기록할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="cd644-269">예</span><span class="sxs-lookup"><span data-stu-id="cd644-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-270">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-270">Attributes</span></span>  
  
|<span data-ttu-id="cd644-271">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-271">Attribute</span></span>|<span data-ttu-id="cd644-272">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-272">Description</span></span>|<span data-ttu-id="cd644-273">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="cd644-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="cd644-274">logger-id</span></span>|<span data-ttu-id="cd644-275">API Management 서비스에 등록된 로거 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="cd644-276">예</span><span class="sxs-lookup"><span data-stu-id="cd644-276">Yes</span></span>|  
|<span data-ttu-id="cd644-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="cd644-277">partition-id</span></span>|<span data-ttu-id="cd644-278">메시지가 전송된 파티션의 인덱스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="cd644-279">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-279">Optional.</span></span> <span data-ttu-id="cd644-280">`partition-key`가 사용된 경우에는 이 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="cd644-281">파티션 키</span><span class="sxs-lookup"><span data-stu-id="cd644-281">partition-key</span></span>|<span data-ttu-id="cd644-282">메시지가 전송된 파티션 할당에 사용된 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="cd644-283">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-283">Optional.</span></span> <span data-ttu-id="cd644-284">`partition-id`가 사용된 경우에는 이 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-285">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-285">Usage</span></span>  
 <span data-ttu-id="cd644-286">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-287">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-288">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="cd644-289"><a name="mock-response"></a> 모의 응답</span><span class="sxs-lookup"><span data-stu-id="cd644-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="cd644-290">이름에서 알 수 있듯이 `mock-response`는 모의 API 및 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="cd644-291">정상적인 파이프라인 실행을 중단하고 호출자에게 모의 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="cd644-292">정책에서 항상 최고 충실도의 응답을 반환하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="cd644-293">가능한 경우 응답 콘텐츠 예제를 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="cd644-294">스키마가 제공되고 예제가 제공되지 않은 경우 스키마에서 샘플 응답을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="cd644-295">예제와 스키마가 둘 다 없는 경우 콘텐츠가 없는 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-296">정책 문</span><span class="sxs-lookup"><span data-stu-id="cd644-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="cd644-297">예</span><span class="sxs-lookup"><span data-stu-id="cd644-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-298">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-298">Elements</span></span>  
  
|<span data-ttu-id="cd644-299">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-299">Element</span></span>|<span data-ttu-id="cd644-300">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-300">Description</span></span>|<span data-ttu-id="cd644-301">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="cd644-302">mock-response</span></span>|<span data-ttu-id="cd644-303">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-303">Root element.</span></span>|<span data-ttu-id="cd644-304">예</span><span class="sxs-lookup"><span data-stu-id="cd644-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-305">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-305">Attributes</span></span>  
  
|<span data-ttu-id="cd644-306">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-306">Attribute</span></span>|<span data-ttu-id="cd644-307">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-307">Description</span></span>|<span data-ttu-id="cd644-308">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-308">Required</span></span>|<span data-ttu-id="cd644-309">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="cd644-310">status-code</span><span class="sxs-lookup"><span data-stu-id="cd644-310">status-code</span></span>|<span data-ttu-id="cd644-311">응답 상태 코드를 지정하며, 해당 예제 또는 스키마를 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="cd644-312">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-312">No</span></span>|<span data-ttu-id="cd644-313">200</span><span class="sxs-lookup"><span data-stu-id="cd644-313">200</span></span>|  
|<span data-ttu-id="cd644-314">content-type</span><span class="sxs-lookup"><span data-stu-id="cd644-314">content-type</span></span>|<span data-ttu-id="cd644-315">`Content-Type` 응답 헤더 값을 지정하며, 해당 예제 또는 스키마를 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="cd644-316">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-316">No</span></span>|<span data-ttu-id="cd644-317">없음</span><span class="sxs-lookup"><span data-stu-id="cd644-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-318">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-318">Usage</span></span>  
 <span data-ttu-id="cd644-319">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-320">**정책 섹션:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="cd644-321">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="cd644-322"><a name="Retry"></a> 다시 시도</span><span class="sxs-lookup"><span data-stu-id="cd644-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="cd644-323">`retry` 정책은 하위 정책을 한 번 실행한 후 재시도 `condition`이 `false`가 되거나 재시도 `count`를 모두 사용할 때까지 실행을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-324">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-325">예</span><span class="sxs-lookup"><span data-stu-id="cd644-325">Example</span></span>  
 <span data-ttu-id="cd644-326">다음 예에서는 지수 재시도 알고리즘을 사용하여 요청 전달을 최대 10회까지 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="cd644-327">`first-fast-retry`가 false로 설정되므로 모든 재시도 횟수에는 지수 재시도 알고리즘이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-328">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-328">Elements</span></span>  
  
|<span data-ttu-id="cd644-329">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-329">Element</span></span>|<span data-ttu-id="cd644-330">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-330">Description</span></span>|<span data-ttu-id="cd644-331">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-332">retry</span><span class="sxs-lookup"><span data-stu-id="cd644-332">retry</span></span>|<span data-ttu-id="cd644-333">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-333">Root element.</span></span> <span data-ttu-id="cd644-334">자식 요소로 다른 정책을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="cd644-335">예</span><span class="sxs-lookup"><span data-stu-id="cd644-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-336">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-336">Attributes</span></span>  
  
|<span data-ttu-id="cd644-337">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-337">Attribute</span></span>|<span data-ttu-id="cd644-338">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-338">Description</span></span>|<span data-ttu-id="cd644-339">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-339">Required</span></span>|<span data-ttu-id="cd644-340">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-341">condition</span><span class="sxs-lookup"><span data-stu-id="cd644-341">condition</span></span>|<span data-ttu-id="cd644-342">재시도를 중지(`false`) 또는 진행(`true`)해야 하는지 여부를 지정하는 부울 리터럴 또는 [식](api-management-policy-expressions.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="cd644-343">예</span><span class="sxs-lookup"><span data-stu-id="cd644-343">Yes</span></span>|<span data-ttu-id="cd644-344">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-344">N/A</span></span>|  
|<span data-ttu-id="cd644-345">count</span><span class="sxs-lookup"><span data-stu-id="cd644-345">count</span></span>|<span data-ttu-id="cd644-346">최대 재시도 횟수를 지정하는 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="cd644-347">예</span><span class="sxs-lookup"><span data-stu-id="cd644-347">Yes</span></span>|<span data-ttu-id="cd644-348">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-348">N/A</span></span>|  
|<span data-ttu-id="cd644-349">interval</span><span class="sxs-lookup"><span data-stu-id="cd644-349">interval</span></span>|<span data-ttu-id="cd644-350">재시도 횟수 간에 대기 간격을 지정하는 양수(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="cd644-351">예</span><span class="sxs-lookup"><span data-stu-id="cd644-351">Yes</span></span>|<span data-ttu-id="cd644-352">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-352">N/A</span></span>|  
|<span data-ttu-id="cd644-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="cd644-353">max-interval</span></span>|<span data-ttu-id="cd644-354">재시도 횟수 간에 최대 대기 간격을 지정하는 양수(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="cd644-355">지수 재시도 알고리즘을 구현하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="cd644-356">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-356">No</span></span>|<span data-ttu-id="cd644-357">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-357">N/A</span></span>|  
|<span data-ttu-id="cd644-358">delta</span><span class="sxs-lookup"><span data-stu-id="cd644-358">delta</span></span>|<span data-ttu-id="cd644-359">대기 간격 증분을 지정하는 양수(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="cd644-360">선형 및 지수 재시도 알고리즘을 구현하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="cd644-361">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-361">No</span></span>|<span data-ttu-id="cd644-362">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-362">N/A</span></span>|  
|<span data-ttu-id="cd644-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="cd644-363">first-fast-retry</span></span>|<span data-ttu-id="cd644-364">`true`로 설정하면 첫 번째 재시도가 즉시 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="cd644-365">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="cd644-366">`interval`만 지정된 경우, **고정된** 간격 재시도가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="cd644-367">`interval` 및 `delta`만 지정된 경우 **선형** 간격 재시도 알고리즘이 사용되며 이 경우 재시도 간 대기 시간은 `interval + (count - 1)*delta` 수식에 따라 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="cd644-368">`interval`, `max-interval` 및 `delta`가 지정된 경우 **지수** 간격 재시도 알고리즘이 적용되며 이 경우 재시도 간 대기 시간은 `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)` 수식에 따라 `interval` 값에서 `max-interval` 값으로 기하급수적으로 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cd644-369">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-369">Usage</span></span>  
 <span data-ttu-id="cd644-370">다음 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에 이 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="cd644-371">이 정책에 의해 자식 정책 사용 제한이 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="cd644-372">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-373">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-374"><a name="ReturnResponse"></a> 반환 응답</span><span class="sxs-lookup"><span data-stu-id="cd644-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="cd644-375">`return-response` 정책은 파이프라인 실행을 중단하고 호출자에게 기본 또는 사용자 지정된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="cd644-376">기본 응답은 본문 없는 `200 OK`입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="cd644-377">컨텍스트 변수나 정책 문을 통해 사용자 지정 응답을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="cd644-378">둘 다 제공되는 경우 컨텍스트 변수 내에 포함된 응답은 호출자로 반환하기 전에 정책 문으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-379">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-380">예</span><span class="sxs-lookup"><span data-stu-id="cd644-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-381">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-381">Elements</span></span>  
  
|<span data-ttu-id="cd644-382">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-382">Element</span></span>|<span data-ttu-id="cd644-383">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-383">Description</span></span>|<span data-ttu-id="cd644-384">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-385">return-response</span><span class="sxs-lookup"><span data-stu-id="cd644-385">return-response</span></span>|<span data-ttu-id="cd644-386">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-386">Root element.</span></span>|<span data-ttu-id="cd644-387">예</span><span class="sxs-lookup"><span data-stu-id="cd644-387">Yes</span></span>|  
|<span data-ttu-id="cd644-388">set-header</span><span class="sxs-lookup"><span data-stu-id="cd644-388">set-header</span></span>|<span data-ttu-id="cd644-389">[set-header](api-management-transformation-policies.md#SetHTTPheader) 정책 문.</span><span class="sxs-lookup"><span data-stu-id="cd644-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="cd644-390">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-390">No</span></span>|  
|<span data-ttu-id="cd644-391">set-body</span><span class="sxs-lookup"><span data-stu-id="cd644-391">set-body</span></span>|<span data-ttu-id="cd644-392">[set-body](api-management-transformation-policies.md#SetBody) 정책 문.</span><span class="sxs-lookup"><span data-stu-id="cd644-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="cd644-393">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-393">No</span></span>|  
|<span data-ttu-id="cd644-394">set-status</span><span class="sxs-lookup"><span data-stu-id="cd644-394">set-status</span></span>|<span data-ttu-id="cd644-395">[set-status](api-management-advanced-policies.md#SetStatus) 정책 문.</span><span class="sxs-lookup"><span data-stu-id="cd644-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="cd644-396">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-397">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-397">Attributes</span></span>  
  
|<span data-ttu-id="cd644-398">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-398">Attribute</span></span>|<span data-ttu-id="cd644-399">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-399">Description</span></span>|<span data-ttu-id="cd644-400">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="cd644-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="cd644-401">response-variable-name</span></span>|<span data-ttu-id="cd644-402">참조하는 컨텍스트 변수 이름(예: 업스트림 [send-request](api-management-advanced-policies.md#SendRequest) 정책 및 `Response` 개체 포함)</span><span class="sxs-lookup"><span data-stu-id="cd644-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="cd644-403">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-404">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-404">Usage</span></span>  
 <span data-ttu-id="cd644-405">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-406">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-407">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-408"><a name="SendOneWayRequest"></a> 단방향 요청 전송</span><span class="sxs-lookup"><span data-stu-id="cd644-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="cd644-409">`send-one-way-request` 정책은 지정된 URL에 대한 제공된 응답을 기다리지 않고 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-410">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-411">예</span><span class="sxs-lookup"><span data-stu-id="cd644-411">Example</span></span>  
 <span data-ttu-id="cd644-412">이 샘플 정책에서는 HTTP 응답 코드가 500 이상인 경우 `send-one-way-request` 정책을 사용하여 Slack 대화방에 메시지를 보내는 방법에 대한 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="cd644-413">이 샘플에 대한 자세한 내용은 [Azure API Management 서비스에서 외부 서비스 사용](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-414">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-414">Elements</span></span>  
  
|<span data-ttu-id="cd644-415">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-415">Element</span></span>|<span data-ttu-id="cd644-416">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-416">Description</span></span>|<span data-ttu-id="cd644-417">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="cd644-418">send-one-way-request</span></span>|<span data-ttu-id="cd644-419">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-419">Root element.</span></span>|<span data-ttu-id="cd644-420">예</span><span class="sxs-lookup"><span data-stu-id="cd644-420">Yes</span></span>|  
|<span data-ttu-id="cd644-421">url</span><span class="sxs-lookup"><span data-stu-id="cd644-421">url</span></span>|<span data-ttu-id="cd644-422">요청의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-422">The URL of the request.</span></span>|<span data-ttu-id="cd644-423">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="cd644-424">메서드</span><span class="sxs-lookup"><span data-stu-id="cd644-424">method</span></span>|<span data-ttu-id="cd644-425">요청에 대한 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-425">The HTTP method for the request.</span></span>|<span data-ttu-id="cd644-426">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="cd644-427">머리글</span><span class="sxs-lookup"><span data-stu-id="cd644-427">header</span></span>|<span data-ttu-id="cd644-428">요청 헤더.</span><span class="sxs-lookup"><span data-stu-id="cd644-428">Request header.</span></span> <span data-ttu-id="cd644-429">여러 요청 헤더에 여러 헤더 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="cd644-430">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-430">No</span></span>|  
|<span data-ttu-id="cd644-431">body</span><span class="sxs-lookup"><span data-stu-id="cd644-431">body</span></span>|<span data-ttu-id="cd644-432">요청 본문.</span><span class="sxs-lookup"><span data-stu-id="cd644-432">The request body.</span></span>|<span data-ttu-id="cd644-433">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-434">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-434">Attributes</span></span>  
  
|<span data-ttu-id="cd644-435">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-435">Attribute</span></span>|<span data-ttu-id="cd644-436">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-436">Description</span></span>|<span data-ttu-id="cd644-437">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-437">Required</span></span>|<span data-ttu-id="cd644-438">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="cd644-439">mode="string"</span></span>|<span data-ttu-id="cd644-440">새 요청인지 현재 요청의 복사본인지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="cd644-441">아웃바운드 모드에서 mode=copy는 요청 본문을 초기화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="cd644-442">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-442">No</span></span>|<span data-ttu-id="cd644-443">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="cd644-443">New</span></span>|  
|<span data-ttu-id="cd644-444">name</span><span class="sxs-lookup"><span data-stu-id="cd644-444">name</span></span>|<span data-ttu-id="cd644-445">설정할 헤더의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="cd644-446">예</span><span class="sxs-lookup"><span data-stu-id="cd644-446">Yes</span></span>|<span data-ttu-id="cd644-447">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-447">N/A</span></span>|  
|<span data-ttu-id="cd644-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="cd644-448">exists-action</span></span>|<span data-ttu-id="cd644-449">헤더가 이미 지정되어 있는 경우 수행할 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="cd644-450">이 특성에는 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="cd644-451">- override: 기존 헤더 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="cd644-452">- skip: 기존 헤더 값을 바꾸지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="cd644-453">- append: 기존 헤더 값에 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="cd644-454">- delete: 요청에서 헤더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="cd644-455">`override`로 설정할 때 동일한 이름의 여러 항목을 등록하면 모든 항목(여러 번 나열됨)에 따라 헤더가 설정되며, 나열된 값만 결과에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="cd644-456">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-456">No</span></span>|<span data-ttu-id="cd644-457">재정의</span><span class="sxs-lookup"><span data-stu-id="cd644-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-458">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-458">Usage</span></span>  
 <span data-ttu-id="cd644-459">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-460">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-461">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-462"><a name="SendRequest"></a> 요청 전송</span><span class="sxs-lookup"><span data-stu-id="cd644-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="cd644-463">`send-request` 정책은 지정된 URL에 대한 제공된 응답을 설정된 시간 초과 값 이상으로 기다리지 않고 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-464">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-465">예</span><span class="sxs-lookup"><span data-stu-id="cd644-465">Example</span></span>  
 <span data-ttu-id="cd644-466">이 예에서는 권한 부여 서버에서 참조 토큰을 확인하는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="cd644-467">이 샘플에 대한 자세한 내용은 [Azure API Management 서비스에서 외부 서비스 사용](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-468">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-468">Elements</span></span>  
  
|<span data-ttu-id="cd644-469">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-469">Element</span></span>|<span data-ttu-id="cd644-470">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-470">Description</span></span>|<span data-ttu-id="cd644-471">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-472">send-request</span><span class="sxs-lookup"><span data-stu-id="cd644-472">send-request</span></span>|<span data-ttu-id="cd644-473">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-473">Root element.</span></span>|<span data-ttu-id="cd644-474">예</span><span class="sxs-lookup"><span data-stu-id="cd644-474">Yes</span></span>|  
|<span data-ttu-id="cd644-475">url</span><span class="sxs-lookup"><span data-stu-id="cd644-475">url</span></span>|<span data-ttu-id="cd644-476">요청의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-476">The URL of the request.</span></span>|<span data-ttu-id="cd644-477">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="cd644-478">메서드</span><span class="sxs-lookup"><span data-stu-id="cd644-478">method</span></span>|<span data-ttu-id="cd644-479">요청에 대한 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-479">The HTTP method for the request.</span></span>|<span data-ttu-id="cd644-480">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="cd644-481">머리글</span><span class="sxs-lookup"><span data-stu-id="cd644-481">header</span></span>|<span data-ttu-id="cd644-482">요청 헤더.</span><span class="sxs-lookup"><span data-stu-id="cd644-482">Request header.</span></span> <span data-ttu-id="cd644-483">여러 요청 헤더에 여러 헤더 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="cd644-484">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-484">No</span></span>|  
|<span data-ttu-id="cd644-485">body</span><span class="sxs-lookup"><span data-stu-id="cd644-485">body</span></span>|<span data-ttu-id="cd644-486">요청 본문.</span><span class="sxs-lookup"><span data-stu-id="cd644-486">The request body.</span></span>|<span data-ttu-id="cd644-487">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-488">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-488">Attributes</span></span>  
  
|<span data-ttu-id="cd644-489">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-489">Attribute</span></span>|<span data-ttu-id="cd644-490">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-490">Description</span></span>|<span data-ttu-id="cd644-491">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-491">Required</span></span>|<span data-ttu-id="cd644-492">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="cd644-493">mode="string"</span></span>|<span data-ttu-id="cd644-494">새 요청인지 현재 요청의 복사본인지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="cd644-495">아웃바운드 모드에서 mode=copy는 요청 본문을 초기화하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="cd644-496">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-496">No</span></span>|<span data-ttu-id="cd644-497">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="cd644-497">New</span></span>|  
|<span data-ttu-id="cd644-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="cd644-498">response-variable-name="string"</span></span>|<span data-ttu-id="cd644-499">없는 경우 `context.Response`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="cd644-500">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-500">No</span></span>|<span data-ttu-id="cd644-501">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-501">N/A</span></span>|  
|<span data-ttu-id="cd644-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="cd644-502">timeout="integer"</span></span>|<span data-ttu-id="cd644-503">URL 호출이 실패하는 시간 초과 간격(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="cd644-504">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-504">No</span></span>|<span data-ttu-id="cd644-505">60</span><span class="sxs-lookup"><span data-stu-id="cd644-505">60</span></span>|  
|<span data-ttu-id="cd644-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="cd644-506">ignore-error</span></span>|<span data-ttu-id="cd644-507">true인 경우 요청 결과 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="cd644-508">-   response-variable-name이 지정된 경우 null 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="cd644-509">-   response-variable-name이 지정되지 않은 경우 context.Request가 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="cd644-510">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-510">No</span></span>|<span data-ttu-id="cd644-511">false</span><span class="sxs-lookup"><span data-stu-id="cd644-511">false</span></span>|  
|<span data-ttu-id="cd644-512">name</span><span class="sxs-lookup"><span data-stu-id="cd644-512">name</span></span>|<span data-ttu-id="cd644-513">설정할 헤더의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="cd644-514">예</span><span class="sxs-lookup"><span data-stu-id="cd644-514">Yes</span></span>|<span data-ttu-id="cd644-515">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-515">N/A</span></span>|  
|<span data-ttu-id="cd644-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="cd644-516">exists-action</span></span>|<span data-ttu-id="cd644-517">헤더가 이미 지정되어 있는 경우 수행할 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="cd644-518">이 특성에는 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="cd644-519">- override: 기존 헤더 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="cd644-520">- skip: 기존 헤더 값을 바꾸지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="cd644-521">- append: 기존 헤더 값에 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="cd644-522">- delete: 요청에서 헤더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="cd644-523">`override`로 설정할 때 동일한 이름의 여러 항목을 등록하면 모든 항목(여러 번 나열됨)에 따라 헤더가 설정되며, 나열된 값만 결과에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="cd644-524">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-524">No</span></span>|<span data-ttu-id="cd644-525">재정의</span><span class="sxs-lookup"><span data-stu-id="cd644-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-526">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-526">Usage</span></span>  
 <span data-ttu-id="cd644-527">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-528">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-529">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-530"><a name="SetHttpProxy"></a> HTTP 프록시 설정</span><span class="sxs-lookup"><span data-stu-id="cd644-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="cd644-531">`proxy` 정책은 HTTP 프록시를 통해 백 엔드에 전달된 요청을 라우팅하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="cd644-532">게이트웨이와 프록시 간에 HTTP(HTTPS 아님)만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="cd644-533">기본 및 NTLM 인증만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-534">정책 문</span><span class="sxs-lookup"><span data-stu-id="cd644-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-535">예제</span><span class="sxs-lookup"><span data-stu-id="cd644-535">Example</span></span>  
<span data-ttu-id="cd644-536">사용자 이름 및 암호의 값으로 [속성](api-management-howto-properties.md)을 사용하면 정책 문서에 중요한 정보를 저장하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-537">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-537">Elements</span></span>  
  
|<span data-ttu-id="cd644-538">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-538">Element</span></span>|<span data-ttu-id="cd644-539">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-539">Description</span></span>|<span data-ttu-id="cd644-540">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-541">proxy</span><span class="sxs-lookup"><span data-stu-id="cd644-541">proxy</span></span>|<span data-ttu-id="cd644-542">루트 요소</span><span class="sxs-lookup"><span data-stu-id="cd644-542">Root element</span></span>|<span data-ttu-id="cd644-543">예</span><span class="sxs-lookup"><span data-stu-id="cd644-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="cd644-544">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-544">Attributes</span></span>  
  
|<span data-ttu-id="cd644-545">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-545">Attribute</span></span>|<span data-ttu-id="cd644-546">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-546">Description</span></span>|<span data-ttu-id="cd644-547">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-547">Required</span></span>|<span data-ttu-id="cd644-548">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-549">url="문자열"</span><span class="sxs-lookup"><span data-stu-id="cd644-549">url="string"</span></span>|<span data-ttu-id="cd644-550">http://host:port 형식의 프록시 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="cd644-551">예</span><span class="sxs-lookup"><span data-stu-id="cd644-551">Yes</span></span>|<span data-ttu-id="cd644-552">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-552">N/A</span></span>|  
|<span data-ttu-id="cd644-553">사용자 이름="문자열"</span><span class="sxs-lookup"><span data-stu-id="cd644-553">username="string"</span></span>|<span data-ttu-id="cd644-554">프록시 인증에 사용할 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="cd644-555">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-555">No</span></span>|<span data-ttu-id="cd644-556">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-556">N/A</span></span>|  
|<span data-ttu-id="cd644-557">암호="문자열"</span><span class="sxs-lookup"><span data-stu-id="cd644-557">password="string"</span></span>|<span data-ttu-id="cd644-558">프록시 인증에 사용할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="cd644-559">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-559">No</span></span>|<span data-ttu-id="cd644-560">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="cd644-561">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-561">Usage</span></span>  
 <span data-ttu-id="cd644-562">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-563">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="cd644-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="cd644-564">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="cd644-565"><a name="SetRequestMethod"></a> 요청 메서드 설정</span><span class="sxs-lookup"><span data-stu-id="cd644-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="cd644-566">`set-method` 정책을 통해 요청에 대한 HTTP 메서드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-567">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-568">예제</span><span class="sxs-lookup"><span data-stu-id="cd644-568">Example</span></span>  
 <span data-ttu-id="cd644-569">이 샘플 정책은 `set-method` 정책을 사용하며 HTTP 응답 코드가 500 이상인 경우 Slack 대화방에 메시지를 보내는 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="cd644-570">이 샘플에 대한 자세한 내용은 [Azure API Management 서비스에서 외부 서비스 사용](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-571">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-571">Elements</span></span>  
  
|<span data-ttu-id="cd644-572">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-572">Element</span></span>|<span data-ttu-id="cd644-573">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-573">Description</span></span>|<span data-ttu-id="cd644-574">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-575">set-method</span><span class="sxs-lookup"><span data-stu-id="cd644-575">set-method</span></span>|<span data-ttu-id="cd644-576">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-576">Root element.</span></span> <span data-ttu-id="cd644-577">이 요소 값은 HTTP 메서드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="cd644-578">예</span><span class="sxs-lookup"><span data-stu-id="cd644-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-579">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-579">Usage</span></span>  
 <span data-ttu-id="cd644-580">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-581">**정책 섹션:** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="cd644-582">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-583"><a name="SetStatus"></a> 상태 코드 설정</span><span class="sxs-lookup"><span data-stu-id="cd644-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="cd644-584">`set-status` 정책은 HTTP 상태 코드를 지정된 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-585">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-586">예</span><span class="sxs-lookup"><span data-stu-id="cd644-586">Example</span></span>  
 <span data-ttu-id="cd644-587">이 예에서는 인증 토큰이 유효하지 않은 경우 401 응답을 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="cd644-588">자세한 내용은 [Azure API Management 서비스에서 외부 서비스 사용](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-589">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-589">Elements</span></span>  
  
|<span data-ttu-id="cd644-590">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-590">Element</span></span>|<span data-ttu-id="cd644-591">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-591">Description</span></span>|<span data-ttu-id="cd644-592">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-593">set-status</span><span class="sxs-lookup"><span data-stu-id="cd644-593">set-status</span></span>|<span data-ttu-id="cd644-594">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-594">Root element.</span></span>|<span data-ttu-id="cd644-595">예</span><span class="sxs-lookup"><span data-stu-id="cd644-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-596">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-596">Attributes</span></span>  
  
|<span data-ttu-id="cd644-597">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-597">Attribute</span></span>|<span data-ttu-id="cd644-598">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-598">Description</span></span>|<span data-ttu-id="cd644-599">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-599">Required</span></span>|<span data-ttu-id="cd644-600">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="cd644-601">code="integer"</span></span>|<span data-ttu-id="cd644-602">반환할 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-602">The HTTP status code to return.</span></span>|<span data-ttu-id="cd644-603">예</span><span class="sxs-lookup"><span data-stu-id="cd644-603">Yes</span></span>|<span data-ttu-id="cd644-604">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-604">N/A</span></span>|  
|<span data-ttu-id="cd644-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="cd644-605">reason="string"</span></span>|<span data-ttu-id="cd644-606">상태 코드를 반환하는 이유에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="cd644-607">예</span><span class="sxs-lookup"><span data-stu-id="cd644-607">Yes</span></span>|<span data-ttu-id="cd644-608">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-609">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-609">Usage</span></span>  
 <span data-ttu-id="cd644-610">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-611">**정책 섹션:** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-612">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="cd644-613"><a name="set-variable"></a> 변수 설정</span><span class="sxs-lookup"><span data-stu-id="cd644-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="cd644-614">`set-variable` 정책은 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 변수를 선언하고 [식](api-management-policy-expressions.md) 또는 문자열 리터럴을 통해 지정된 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="cd644-615">식에 리터럴이 포함된 경우 리터럴은 문자열로 변환되고 값 형식은 `System.String`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="cd644-616"><a name="set-variablePolicyStatement"></a> 정책 문</span><span class="sxs-lookup"><span data-stu-id="cd644-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="cd644-617"><a name="set-variableExample"></a> 예</span><span class="sxs-lookup"><span data-stu-id="cd644-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="cd644-618">다음 예는 인바운드 섹션에 변수 설정 정책이 있는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="cd644-619">이 변수 설정 정책은 `User-Agent` 요청 헤더에 `iPad` 또는 `iPhone` 텍스트가 포함되는 경우 true로 설정되는 `isMobile` 부울 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-620">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-620">Elements</span></span>  
  
|<span data-ttu-id="cd644-621">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-621">Element</span></span>|<span data-ttu-id="cd644-622">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-622">Description</span></span>|<span data-ttu-id="cd644-623">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="cd644-624">set-variable</span></span>|<span data-ttu-id="cd644-625">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-625">Root element.</span></span>|<span data-ttu-id="cd644-626">예</span><span class="sxs-lookup"><span data-stu-id="cd644-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-627">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-627">Attributes</span></span>  
  
|<span data-ttu-id="cd644-628">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-628">Attribute</span></span>|<span data-ttu-id="cd644-629">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-629">Description</span></span>|<span data-ttu-id="cd644-630">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="cd644-631">name</span><span class="sxs-lookup"><span data-stu-id="cd644-631">name</span></span>|<span data-ttu-id="cd644-632">변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-632">The name of the variable.</span></span>|<span data-ttu-id="cd644-633">예</span><span class="sxs-lookup"><span data-stu-id="cd644-633">Yes</span></span>|  
|<span data-ttu-id="cd644-634">값</span><span class="sxs-lookup"><span data-stu-id="cd644-634">value</span></span>|<span data-ttu-id="cd644-635">변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-635">The value of the variable.</span></span> <span data-ttu-id="cd644-636">식 또는 리터럴 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="cd644-637">예</span><span class="sxs-lookup"><span data-stu-id="cd644-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-638">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-638">Usage</span></span>  
 <span data-ttu-id="cd644-639">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-640">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-641">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="cd644-642"><a name="set-variableAllowedTypes"></a> 허용 형식</span><span class="sxs-lookup"><span data-stu-id="cd644-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="cd644-643">`set-variable` 정책에 사용된 식은 다음 기본 형식 중 하나를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="cd644-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="cd644-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="cd644-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="cd644-645">System.SByte</span></span>  
  
-   <span data-ttu-id="cd644-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="cd644-646">System.Byte</span></span>  
  
-   <span data-ttu-id="cd644-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="cd644-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="cd644-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="cd644-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="cd644-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="cd644-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="cd644-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="cd644-650">System.Int16</span></span>  
  
-   <span data-ttu-id="cd644-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="cd644-651">System.Int32</span></span>  
  
-   <span data-ttu-id="cd644-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="cd644-652">System.Int64</span></span>  
  
-   <span data-ttu-id="cd644-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="cd644-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="cd644-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="cd644-654">System.Single</span></span>  
  
-   <span data-ttu-id="cd644-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="cd644-655">System.Double</span></span>  
  
-   <span data-ttu-id="cd644-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="cd644-656">System.Guid</span></span>  
  
-   <span data-ttu-id="cd644-657">System.String</span><span class="sxs-lookup"><span data-stu-id="cd644-657">System.String</span></span>  
  
-   <span data-ttu-id="cd644-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="cd644-658">System.Char</span></span>  
  
-   <span data-ttu-id="cd644-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="cd644-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="cd644-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="cd644-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="cd644-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="cd644-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="cd644-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="cd644-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="cd644-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="cd644-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="cd644-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="cd644-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="cd644-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="cd644-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="cd644-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="cd644-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="cd644-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="cd644-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="cd644-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="cd644-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="cd644-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="cd644-669">System.Single?</span></span>  
  
-   <span data-ttu-id="cd644-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="cd644-670">System.Double?</span></span>  
  
-   <span data-ttu-id="cd644-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="cd644-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="cd644-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="cd644-672">System.String?</span></span>  
  
-   <span data-ttu-id="cd644-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="cd644-673">System.Char?</span></span>  
  
-   <span data-ttu-id="cd644-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="cd644-674">System.DateTime?</span></span>  

##  <span data-ttu-id="cd644-675"><a name="Trace"></a> 추적</span><span class="sxs-lookup"><span data-stu-id="cd644-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="cd644-676">`trace` 정책은 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력에 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="cd644-677">이 정책은 추적이 트리거된 경우에만 실행됩니다(즉, `Ocp-Apim-Trace` 요청 헤더가 있고 `true`로 설정된 경우 및 `Ocp-Apim-Subscription-Key` 요청 헤더가 있고 관리자 계정에 연결된 유효한 키를 보유하는 경우).</span><span class="sxs-lookup"><span data-stu-id="cd644-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-678">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-679">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-679">Elements</span></span>  
  
|<span data-ttu-id="cd644-680">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-680">Element</span></span>|<span data-ttu-id="cd644-681">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-681">Description</span></span>|<span data-ttu-id="cd644-682">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-683">추적</span><span class="sxs-lookup"><span data-stu-id="cd644-683">trace</span></span>|<span data-ttu-id="cd644-684">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-684">Root element.</span></span>|<span data-ttu-id="cd644-685">예</span><span class="sxs-lookup"><span data-stu-id="cd644-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-686">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-686">Attributes</span></span>  
  
|<span data-ttu-id="cd644-687">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-687">Attribute</span></span>|<span data-ttu-id="cd644-688">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-688">Description</span></span>|<span data-ttu-id="cd644-689">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-689">Required</span></span>|<span data-ttu-id="cd644-690">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-691">원본</span><span class="sxs-lookup"><span data-stu-id="cd644-691">source</span></span>|<span data-ttu-id="cd644-692">추적 뷰어에 의미있고 메시지 원본을 지정하는 문자열 리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="cd644-693">예</span><span class="sxs-lookup"><span data-stu-id="cd644-693">Yes</span></span>|<span data-ttu-id="cd644-694">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cd644-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-695">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-695">Usage</span></span>  
 <span data-ttu-id="cd644-696">다음 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에 이 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="cd644-697">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="cd644-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="cd644-698">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="cd644-699"><a name="Wait"></a> 대기</span><span class="sxs-lookup"><span data-stu-id="cd644-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="cd644-700">`wait` 정책은 직계 자식 정책을 병렬로 실행하고 정책이 완료되기 전에 직계 자식 정책 전체 또는 하나가 완료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="cd644-701">대기 정책은 직계 자식 정책으로 [요청 전송](api-management-advanced-policies.md#SendRequest), [캐시에서 값 가져오기](api-management-caching-policies.md#GetFromCacheByKey), [제어 흐름](api-management-advanced-policies.md#choose) 정책을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="cd644-702">정책 문:</span><span class="sxs-lookup"><span data-stu-id="cd644-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="cd644-703">예</span><span class="sxs-lookup"><span data-stu-id="cd644-703">Example</span></span>  
 <span data-ttu-id="cd644-704">다음 예에는 `wait` 정책의 직계 자식 정책으로 두 개의 `choose` 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="cd644-705">이러한 각 `choose` 정책이 병렬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="cd644-706">각 `choose` 정책은 캐시된 값의 검색을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="cd644-707">캐시가 누락된 경우 값을 제공하기 위해 백 엔드 서비스가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="cd644-708">이 예에서는 `for` 특성이 `all`로 설정되어 있으므로 `wait` 정책은 모든 직계 자식 정책이 완료되어야 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="cd644-709">이 예에서 컨텍스트 변수 (`execute-branch-one`, `value-one`, `execute-branch-two`, `value-two`)는 이 예제 정책 범위 밖에 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="cd644-710">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-710">Elements</span></span>  
  
|<span data-ttu-id="cd644-711">요소</span><span class="sxs-lookup"><span data-stu-id="cd644-711">Element</span></span>|<span data-ttu-id="cd644-712">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-712">Description</span></span>|<span data-ttu-id="cd644-713">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="cd644-714">wait</span><span class="sxs-lookup"><span data-stu-id="cd644-714">wait</span></span>|<span data-ttu-id="cd644-715">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-715">Root element.</span></span> <span data-ttu-id="cd644-716">자식 요소로 `send-request`, `cache-lookup-value`, `choose` 정책만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="cd644-717">예</span><span class="sxs-lookup"><span data-stu-id="cd644-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="cd644-718">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-718">Attributes</span></span>  
  
|<span data-ttu-id="cd644-719">특성</span><span class="sxs-lookup"><span data-stu-id="cd644-719">Attribute</span></span>|<span data-ttu-id="cd644-720">설명</span><span class="sxs-lookup"><span data-stu-id="cd644-720">Description</span></span>|<span data-ttu-id="cd644-721">필수</span><span class="sxs-lookup"><span data-stu-id="cd644-721">Required</span></span>|<span data-ttu-id="cd644-722">기본값</span><span class="sxs-lookup"><span data-stu-id="cd644-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="cd644-723">for</span><span class="sxs-lookup"><span data-stu-id="cd644-723">for</span></span>|<span data-ttu-id="cd644-724">`wait` 정책에서 모든 직계 자식 정책 또는 한 정책이 완료될 때까지 대기할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="cd644-725">허용되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="cd644-726">-   `all` - 모든 직계 자식 정책이 완료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="cd644-727">-   any - 임의의 직계 자식 정책이 완료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="cd644-728">첫 번째 직계 자식 정책이 완료되면 `wait` 정책이 완료되고 다른 직계 자식 정책의 실행이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="cd644-729">아니요</span><span class="sxs-lookup"><span data-stu-id="cd644-729">No</span></span>|<span data-ttu-id="cd644-730">모두</span><span class="sxs-lookup"><span data-stu-id="cd644-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="cd644-731">사용 현황</span><span class="sxs-lookup"><span data-stu-id="cd644-731">Usage</span></span>  
 <span data-ttu-id="cd644-732">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd644-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="cd644-733">**정책 섹션:** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="cd644-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="cd644-734">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="cd644-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="cd644-735">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd644-735">Next steps</span></span>
<span data-ttu-id="cd644-736">정책으로 작업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd644-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="cd644-737">API 관리의 정책</span><span class="sxs-lookup"><span data-stu-id="cd644-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="cd644-738">정책 식</span><span class="sxs-lookup"><span data-stu-id="cd644-738">Policy expressions</span></span>](api-management-policy-expressions.md)
