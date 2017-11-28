---
title: "API 관리 고급 정책 aaaAzure | Microsoft Docs"
description: "Hello Azure API 관리에서 사용 하기 위해 사용할 수 있는 정책을 고급 방법을 알아봅니다."
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
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="bf4d1-103">API Management 고급 정책</span><span class="sxs-lookup"><span data-stu-id="bf4d1-103">API Management advanced policies</span></span>
<span data-ttu-id="bf4d1-104">이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="bf4d1-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="bf4d1-106"><a name="AdvancedPolicies"></a> 고급 정책</span><span class="sxs-lookup"><span data-stu-id="bf4d1-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="bf4d1-107">[제어 흐름](api-management-advanced-policies.md#choose) -조건부로 hello 부울의 hello 평가 결과에 따라 정책 문을 적용 [식](api-management-policy-expressions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="bf4d1-108">[요청 전달](#ForwardRequest) -hello 요청 toohello 백 엔드 서비스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="bf4d1-109">[동시성을 제한](#LimitConcurrency) -방지에서 한 번에 지정 된 요청 수를 hello 보다 더 많은 하 여 실행 정책을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="bf4d1-110">[허브 tooEvent 로그](#log-to-eventhub) -hello에 메시지를 보내고 형식 tooan로 거 엔터티에 의해 정의 된 이벤트 허브를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="bf4d1-111">[응답의 모의 알림](#mock-response) -중단 파이프라인 실행 모의 응답을 반환 하 고 직접 toohello 호출자입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="bf4d1-112">[다시 시도](#Retry) -hello 재시도 실행 고 hello 조건이 충족 될 때까지 정책 문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="bf4d1-113">지정 된 시간 간격을 hello 및 다시 시도 횟수를 지정 하는 toohello 실행에서 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="bf4d1-114">[응답을 반환](#ReturnResponse) -지정 된 지시 파일 중단 파이프라인 실행 및 반환 hello 직접 toohello 호출자입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="bf4d1-115">[한 가지 방법은 요청 보내기](#SendOneWayRequest) -요청 toohello 지정한 URL 응답을 받기 위해 대기 하지 않고 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="bf4d1-116">[요청 보내기](#SendRequest) -요청 toohello 지정한 URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="bf4d1-117">[HTTP 프록시 설정](#SetHttpProxy) -HTTP 프록시를 통해 전달 tooroute 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="bf4d1-118">[요청 하는 방법을 설정](#SetRequestMethod) -toochange hello HTTP 메서드는 요청에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="bf4d1-119">[상태 코드를 설정](#SetStatus) -변경 hello HTTP 상태 코드 toohello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="bf4d1-120">[변수 설정](api-management-advanced-policies.md#set-variable) - 나중에 액세스할 수 있도록 명명된 [context](api-management-policy-expressions.md#ContextVariables) 변수의 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="bf4d1-121">[추적](#Trace) -hello에 문자열을 추가 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="bf4d1-122">[대기](#Wait) -묶인 때까지 대기 [보내기 요청](api-management-advanced-policies.md#SendRequest), [캐시에서 값을 가져올](api-management-caching-policies.md#GetFromCacheByKey), 또는 [제어 흐름](api-management-advanced-policies.md#choose) 계속 진행 하기 전에 정책 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="bf4d1-123"><a name="choose"></a> 흐름 제어</span><span class="sxs-lookup"><span data-stu-id="bf4d1-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="bf4d1-124">hello `choose` 정책이 포함 된 정책 hello 평가 결과에 부울 식, if then 다른 유사한 tooan 또는 스위치를 기반으로 문을 프로그래밍 언어의 구문에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="bf4d1-125"><a name="ChoosePolicyStatement"></a> 정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="bf4d1-126">hello 제어 흐름 정책은 해야 하나 이상 포함 `<when/>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="bf4d1-127">hello `<otherwise/>` 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="bf4d1-128">`<when/>` 요소 hello 정책 내에서 표시 되는 순서 대로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="bf4d1-129">먼저 hello 내에 포함 된 정책 문이 `<when/>` 특성 = 조건 가진 요소가 `true` 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="bf4d1-130">Hello 내에 포함 된 정책을 `<otherwise/>` 모든 요소를 사용할 수 있는 경우를 적용할의 hello `<when/>` 요소 조건 특성이 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="bf4d1-131">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-131">Examples</span></span>  
  
####  <span data-ttu-id="bf4d1-132"><a name="ChooseExample"></a> 예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="bf4d1-133">hello 다음 예제에서는 한 [변수 설정](api-management-advanced-policies.md#set-variable) 정책 및 제어 흐름 정책 두 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="bf4d1-134">hello set-variable 정책은 만들고 inbound 섹션 hello 중인는 `isMobile` 부울 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 경우 hello tootrue 설정 된 변수 `User-Agent` 요청 헤더에 hello 텍스트 `iPad` 또는 `iPhone`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="bf4d1-135">첫 번째 제어 흐름 정책은 hello는 역시 inbound 섹션 hello 및 두 가지 중 하나를 조건부로 적용 [쿼리 문자열 매개 변수를 설정](api-management-transformation-policies.md#SetQueryStringParameter) hello hello 값에 따라 정책을 `isMobile` 컨텍스트 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="bf4d1-136">두 번째 제어 흐름 정책은 hello hello outbound 섹션 이므로 hello 조건부로 적용 [XML 변환 tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) 정책 때 `isMobile` 너무 설정`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="bf4d1-137">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-137">Example</span></span>  
 <span data-ttu-id="bf4d1-138">이 예제에서는 어떻게 hello 응답에서 데이터 요소를 제거 하 여 tooperform 콘텐츠 필터링 서비스에서 받은 hello 백 엔드 hello를 사용 하는 경우 `Starter` 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="bf4d1-139">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too34:30 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="bf4d1-140">개요 31:50 toosee부터 시작 [어두운 Sky 예측 API hello](https://developer.forecast.io/) 이 데모에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-141">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-141">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-142">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-142">Element</span></span>|<span data-ttu-id="bf4d1-143">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-143">Description</span></span>|<span data-ttu-id="bf4d1-144">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-145">choose</span><span class="sxs-lookup"><span data-stu-id="bf4d1-145">choose</span></span>|<span data-ttu-id="bf4d1-146">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-146">Root element.</span></span>|<span data-ttu-id="bf4d1-147">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-147">Yes</span></span>|  
|<span data-ttu-id="bf4d1-148">when</span><span class="sxs-lookup"><span data-stu-id="bf4d1-148">when</span></span>|<span data-ttu-id="bf4d1-149">hello에 대 한 조건 toouse hello `if` 또는 `ifelse` hello 부분의 `choose` 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="bf4d1-150">경우 hello `choose` 정책에 여러 개의 `when` 섹션을 순서 대로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="bf4d1-151">한 번 hello `condition` when 요소 평가 너무`true`, 더 이상 없으면 `when` 조건이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="bf4d1-152">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-152">Yes</span></span>|  
|<span data-ttu-id="bf4d1-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="bf4d1-153">otherwise</span></span>|<span data-ttu-id="bf4d1-154">없으면 hello를 사용 하는 hello 정책 조각 toobe 포함 `when` 조건이 너무`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="bf4d1-155">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-156">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-156">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-157">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-157">Attribute</span></span>|<span data-ttu-id="bf4d1-158">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-158">Description</span></span>|<span data-ttu-id="bf4d1-159">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="bf4d1-161">hello 부울 식 또는 포함 된 경우 hello 상수 tooevaluated `when` 정책 문을 평가할 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="bf4d1-162">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-162">Yes</span></span>|  
  
###  <span data-ttu-id="bf4d1-163"><a name="ChooseUsage"></a> 사용 방법</span><span class="sxs-lookup"><span data-stu-id="bf4d1-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="bf4d1-164">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-165">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-166">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-167"><a name="ForwardRequest"></a> 요청 전달</span><span class="sxs-lookup"><span data-stu-id="bf4d1-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="bf4d1-168">hello `forward-request` 정책 hello 들어오는 요청 toohello 백 엔드 서비스 hello 요청에 지정 된 전달 [컨텍스트](api-management-policy-expressions.md#ContextVariables)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="bf4d1-169">hello 백 엔드 서비스 URL에에서 지정 된 API hello [설정](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) hello를 사용 하 여 변경할 수 [백 엔드 서비스 설정](api-management-transformation-policies.md) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bf4d1-170">Hello outbound 섹션에서 toohello 백 엔드 서비스 및 hello 정책 전달 되지 않고 hello 요청에서이 정책 결과 hello의 hello 정책 hello 성공적으로 완료 시 즉시 평가 되 제거 섹션 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-171">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="bf4d1-172">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bf4d1-173">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-173">Example</span></span>  
 <span data-ttu-id="bf4d1-174">hello 다음 API 수준 정책을 모든 요청 전달 toohello 백 엔드 서비스의 제한 시간 간격은 60 초입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="bf4d1-175">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-175">Example</span></span>  
 <span data-ttu-id="bf4d1-176">이 작업 수준 정책 hello를 사용 하 여 `base` hello 부모 API 수준 범위에서 요소 tooinherit hello 백 엔드 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="bf4d1-177">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-177">Example</span></span>  
 <span data-ttu-id="bf4d1-178">명시적으로이 작업 수준 정책 120 시간 제한은 모든 toohello 백 엔드 서비스 요청을 전달 하 고 hello 부모 수준의 백 엔드 API 정책을 상속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bf4d1-179">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-179">Example</span></span>  
 <span data-ttu-id="bf4d1-180">이 작업 수준 정책 요청을 전달 하지 않는 toohello 백 엔드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf4d1-181">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-181">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-182">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-182">Element</span></span>|<span data-ttu-id="bf4d1-183">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-183">Description</span></span>|<span data-ttu-id="bf4d1-184">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="bf4d1-185">forward-request</span></span>|<span data-ttu-id="bf4d1-186">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-186">Root element.</span></span>|<span data-ttu-id="bf4d1-187">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-188">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-188">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-189">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-189">Attribute</span></span>|<span data-ttu-id="bf4d1-190">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-190">Description</span></span>|<span data-ttu-id="bf4d1-191">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-191">Required</span></span>|<span data-ttu-id="bf4d1-192">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-193">timeout="integer"</span></span>|<span data-ttu-id="bf4d1-194">hello 시간 제한 간격 (초)를 hello 전화 toohello 백 엔드 서비스에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="bf4d1-195">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-195">No</span></span>|<span data-ttu-id="bf4d1-196">시간 초과 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-196">No timeout</span></span>|  
|<span data-ttu-id="bf4d1-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="bf4d1-198">Hello 백 엔드 서비스 로부터의 리디렉션 hello 게이트웨이 뒤 되는지 또는 toohello 호출자에 게 반환을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="bf4d1-199">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-199">No</span></span>|<span data-ttu-id="bf4d1-200">false</span><span class="sxs-lookup"><span data-stu-id="bf4d1-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-201">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-201">Usage</span></span>  
 <span data-ttu-id="bf4d1-202">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-203">**정책 섹션:** backend</span><span class="sxs-lookup"><span data-stu-id="bf4d1-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="bf4d1-204">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-205"><a name="LimitConcurrency"></a> 동시성 제한</span><span class="sxs-lookup"><span data-stu-id="bf4d1-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="bf4d1-206">hello `limit-concurrency` 정책에서 실행 하 여 지정된 된 시간에 지정 된 요청 수를 hello 보다 더 많은 괄호로 묶은 정책으로 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="bf4d1-207">Hello 임계값 초과, 시 hello 최대 큐 길이 얻을 때까지 새 요청 tooa 큐에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="bf4d1-208">큐가 고갈되면 새 요청은 즉시 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="bf4d1-209"><a name="LimitConcurrencyStatement"></a> 정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="bf4d1-210">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-210">Examples</span></span>  
  
####  <span data-ttu-id="bf4d1-211"><a name="ChooseExample"></a> 예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="bf4d1-212">hello 다음 예제 요청 수가 toolimit hello 컨텍스트 변수 값에 따라 tooa 백 엔드를 전달 하는 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="bf4d1-213">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-213">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-214">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-214">Element</span></span>|<span data-ttu-id="bf4d1-215">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-215">Description</span></span>|<span data-ttu-id="bf4d1-216">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="bf4d1-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="bf4d1-217">limit-concurrency</span></span>|<span data-ttu-id="bf4d1-218">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-218">Root element.</span></span>|<span data-ttu-id="bf4d1-219">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-220">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-220">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-221">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-221">Attribute</span></span>|<span data-ttu-id="bf4d1-222">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-222">Description</span></span>|<span data-ttu-id="bf4d1-223">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-223">Required</span></span>|<span data-ttu-id="bf4d1-224">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="bf4d1-225">key</span><span class="sxs-lookup"><span data-stu-id="bf4d1-225">key</span></span>|<span data-ttu-id="bf4d1-226">문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-226">A string.</span></span> <span data-ttu-id="bf4d1-227">허용되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-227">Expression allowed.</span></span> <span data-ttu-id="bf4d1-228">Hello 동시성 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="bf4d1-229">여러 정책에서 공유될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="bf4d1-230">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-230">Yes</span></span>|<span data-ttu-id="bf4d1-231">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-231">N/A</span></span>|  
|<span data-ttu-id="bf4d1-232">max-count</span><span class="sxs-lookup"><span data-stu-id="bf4d1-232">max-count</span></span>|<span data-ttu-id="bf4d1-233">정수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-233">An integer.</span></span> <span data-ttu-id="bf4d1-234">허용 되는 tooenter hello 정책 요청의 최대 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="bf4d1-235">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-235">Yes</span></span>|<span data-ttu-id="bf4d1-236">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-236">N/A</span></span>|  
|<span data-ttu-id="bf4d1-237">시간 제한</span><span class="sxs-lookup"><span data-stu-id="bf4d1-237">timeout</span></span>|<span data-ttu-id="bf4d1-238">정수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-238">An integer.</span></span> <span data-ttu-id="bf4d1-239">허용되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-239">Expression allowed.</span></span> <span data-ttu-id="bf4d1-240">Hello 요청 tooenter는 범위와 함께 실패 하기 전에 대기 해야 하는 시간 (초) 수를 지정 "403 너무 많은 요청"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="bf4d1-241">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-241">No</span></span>|<span data-ttu-id="bf4d1-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="bf4d1-242">Infinity</span></span>|  
|<span data-ttu-id="bf4d1-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="bf4d1-243">max-queue-length</span></span>|<span data-ttu-id="bf4d1-244">정수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-244">An integer.</span></span> <span data-ttu-id="bf4d1-245">허용되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-245">Expression allowed.</span></span> <span data-ttu-id="bf4d1-246">Hello 최대 큐 길이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="bf4d1-247">들어오는 요청 tooenter 시도 된이 정책을 종료 됩니다 "403 너무 많은 요청" hello 큐 소진 되 면 즉시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="bf4d1-248">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-248">No</span></span>|<span data-ttu-id="bf4d1-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="bf4d1-249">Infinity</span></span>|  
  
###  <span data-ttu-id="bf4d1-250"><a name="ChooseUsage"></a> 사용 방법</span><span class="sxs-lookup"><span data-stu-id="bf4d1-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="bf4d1-251">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-252">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-253">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf4d1-254"><a name="log-to-eventhub"></a>로그 tooEvent 허브</span><span class="sxs-lookup"><span data-stu-id="bf4d1-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="bf4d1-255">hello `log-to-eventhub` hello 메시지 형식 tooan 이벤트 허브로 거 엔터티에 의해 정의 된 지정 된 정책 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="bf4d1-256">이름에서 알 수 있듯이 온라인 또는 오프 라인 분석을 위해 선택한 요청 또는 응답 컨텍스트 정보를 저장 하기 위한 hello 정책이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bf4d1-257">이벤트 허브 및 이벤트 로깅 구성에 단계별 가이드를 참조 하십시오. [어떻게 Azure 이벤트 허브 API 관리 이벤트 toolog](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-258">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-259">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-259">Example</span></span>  
 <span data-ttu-id="bf4d1-260">이벤트 허브에 기록 하는 hello 값 toobe로 모든 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="bf4d1-261">이 예에서 hello 날짜 및 시간, 배포 서비스 이름, 요청 id, ip 주소 및 모든 인바운드 통화에 대 한 작업 이름을 로깅된 toohello 이벤트 허브로 거 hello로 등록 `contoso-logger` id입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-262">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-262">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-263">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-263">Element</span></span>|<span data-ttu-id="bf4d1-264">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-264">Description</span></span>|<span data-ttu-id="bf4d1-265">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="bf4d1-266">log-to-eventhub</span></span>|<span data-ttu-id="bf4d1-267">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-267">Root element.</span></span> <span data-ttu-id="bf4d1-268">이 요소의 값이 hello는 hello 문자열 toolog tooyour 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="bf4d1-269">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-270">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-270">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-271">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-271">Attribute</span></span>|<span data-ttu-id="bf4d1-272">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-272">Description</span></span>|<span data-ttu-id="bf4d1-273">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="bf4d1-274">logger-id</span></span>|<span data-ttu-id="bf4d1-275">hello의 hello id로 거 API 관리 서비스에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="bf4d1-276">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-276">Yes</span></span>|  
|<span data-ttu-id="bf4d1-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="bf4d1-277">partition-id</span></span>|<span data-ttu-id="bf4d1-278">메시지를 보낼 위치 hello 파티션의 hello 인덱스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="bf4d1-279">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-279">Optional.</span></span> <span data-ttu-id="bf4d1-280">`partition-key`가 사용된 경우에는 이 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="bf4d1-281">파티션 키</span><span class="sxs-lookup"><span data-stu-id="bf4d1-281">partition-key</span></span>|<span data-ttu-id="bf4d1-282">메시지를 보낼 경우 파티션 할당을 위해 사용 되는 hello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="bf4d1-283">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-283">Optional.</span></span> <span data-ttu-id="bf4d1-284">`partition-id`가 사용된 경우에는 이 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-285">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-285">Usage</span></span>  
 <span data-ttu-id="bf4d1-286">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-287">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-288">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf4d1-289"><a name="mock-response"></a> 모의 응답</span><span class="sxs-lookup"><span data-stu-id="bf4d1-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="bf4d1-290">hello `mock-response`의미 hello 이름으로,은, toomock Api 및 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="bf4d1-291">일반 파이프라인 실행을 중단 하 고 모의 응답 toohello 호출자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="bf4d1-292">hello 정책에는 항상 가장 높은 충실도의 tooreturn 응답 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="bf4d1-293">가능한 경우 응답 콘텐츠 예제를 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="bf4d1-294">스키마가 제공되고 예제가 제공되지 않은 경우 스키마에서 샘플 응답을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="bf4d1-295">예제와 스키마가 둘 다 없는 경우 콘텐츠가 없는 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-296">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="bf4d1-297">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="bf4d1-298">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-298">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-299">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-299">Element</span></span>|<span data-ttu-id="bf4d1-300">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-300">Description</span></span>|<span data-ttu-id="bf4d1-301">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="bf4d1-302">mock-response</span></span>|<span data-ttu-id="bf4d1-303">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-303">Root element.</span></span>|<span data-ttu-id="bf4d1-304">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-305">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-305">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-306">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-306">Attribute</span></span>|<span data-ttu-id="bf4d1-307">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-307">Description</span></span>|<span data-ttu-id="bf4d1-308">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-308">Required</span></span>|<span data-ttu-id="bf4d1-309">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="bf4d1-310">status-code</span><span class="sxs-lookup"><span data-stu-id="bf4d1-310">status-code</span></span>|<span data-ttu-id="bf4d1-311">응답 상태 코드를 지정 하 고 해당 예제에 사용 되는 tooselect 또는 스키마는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="bf4d1-312">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-312">No</span></span>|<span data-ttu-id="bf4d1-313">200</span><span class="sxs-lookup"><span data-stu-id="bf4d1-313">200</span></span>|  
|<span data-ttu-id="bf4d1-314">content-type</span><span class="sxs-lookup"><span data-stu-id="bf4d1-314">content-type</span></span>|<span data-ttu-id="bf4d1-315">지정 `Content-Type` 응답 헤더 값 및 해당 예제에 사용 되는 tooselect 또는 스키마와 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="bf4d1-316">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-316">No</span></span>|<span data-ttu-id="bf4d1-317">없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-318">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-318">Usage</span></span>  
 <span data-ttu-id="bf4d1-319">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-320">**정책 섹션:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-321">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="bf4d1-322"><a name="Retry"></a> 다시 시도</span><span class="sxs-lookup"><span data-stu-id="bf4d1-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="bf4d1-323">hello `retry` 자식 정책에 한 번 실행 하 고 hello 재시도까지 실행을 다시 시도 정책 `condition` 됩니다 `false` 을 다시 시도 또는 `count` 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-324">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="bf4d1-325">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-325">Example</span></span>  
 <span data-ttu-id="bf4d1-326">Hello에 다음 예제 요청 forewarding tooten 지 수의 다시 시도 알고리즘을 사용 하 여 시간을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="bf4d1-327">이후 `first-fast-retry` toofalse, 설정 된 모든 다시 시도 횟수는 주체 toohello exponsntial 다시 시도 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-328">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-328">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-329">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-329">Element</span></span>|<span data-ttu-id="bf4d1-330">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-330">Description</span></span>|<span data-ttu-id="bf4d1-331">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-332">retry</span><span class="sxs-lookup"><span data-stu-id="bf4d1-332">retry</span></span>|<span data-ttu-id="bf4d1-333">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-333">Root element.</span></span> <span data-ttu-id="bf4d1-334">자식 요소로 다른 정책을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="bf4d1-335">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-336">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-336">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-337">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-337">Attribute</span></span>|<span data-ttu-id="bf4d1-338">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-338">Description</span></span>|<span data-ttu-id="bf4d1-339">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-339">Required</span></span>|<span data-ttu-id="bf4d1-340">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-341">condition</span><span class="sxs-lookup"><span data-stu-id="bf4d1-341">condition</span></span>|<span data-ttu-id="bf4d1-342">재시도를 중지(`false`) 또는 진행(`true`)해야 하는지 여부를 지정하는 부울 리터럴 또는 [식](api-management-policy-expressions.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="bf4d1-343">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-343">Yes</span></span>|<span data-ttu-id="bf4d1-344">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-344">N/A</span></span>|  
|<span data-ttu-id="bf4d1-345">count</span><span class="sxs-lookup"><span data-stu-id="bf4d1-345">count</span></span>|<span data-ttu-id="bf4d1-346">재시도 tooattempt hello 최대 수를 지정 하는 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="bf4d1-347">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-347">Yes</span></span>|<span data-ttu-id="bf4d1-348">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-348">N/A</span></span>|  
|<span data-ttu-id="bf4d1-349">interval</span><span class="sxs-lookup"><span data-stu-id="bf4d1-349">interval</span></span>|<span data-ttu-id="bf4d1-350">양수 hello 재시도 사이의 hello 대기 간격 (초)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="bf4d1-351">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-351">Yes</span></span>|<span data-ttu-id="bf4d1-352">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-352">N/A</span></span>|  
|<span data-ttu-id="bf4d1-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="bf4d1-353">max-interval</span></span>|<span data-ttu-id="bf4d1-354">양수 hello 재시도 사이의 hello 최대 대기 간격 (초)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="bf4d1-355">지 수 재시도 알고리즘 tooimplement를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="bf4d1-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="bf4d1-356">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-356">No</span></span>|<span data-ttu-id="bf4d1-357">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-357">N/A</span></span>|  
|<span data-ttu-id="bf4d1-358">delta</span><span class="sxs-lookup"><span data-stu-id="bf4d1-358">delta</span></span>|<span data-ttu-id="bf4d1-359">양수에 hello 대기 간격 증가 지정 하는 시간 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="bf4d1-360">사용 되는 tooimplement hello 선형 및 지 수 재시도 알고리즘은</span><span class="sxs-lookup"><span data-stu-id="bf4d1-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="bf4d1-361">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-361">No</span></span>|<span data-ttu-id="bf4d1-362">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-362">N/A</span></span>|  
|<span data-ttu-id="bf4d1-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="bf4d1-363">first-fast-retry</span></span>|<span data-ttu-id="bf4d1-364">경우 너무 설정 `true` , 첫 번째 다시 시도 hello 즉시 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="bf4d1-365">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="bf4d1-366">Hello만 경우 `interval` 지정 된 **고정** 간격은 다시 시도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="bf4d1-367">때만 hello `interval` 및 `delta` 지정는 **선형** 다시 시도 작업 사이의 대기 시간에 따라 계산 된 hello 인 간격은 다시 시도 알고리즘을 사용 다음 수식을- `interval + (count - 1)*delta`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="bf4d1-368">Hello 때 `interval`, `max-interval` 및 `delta` 지정 된 **지 수** 간격은 다시 시도 알고리즘 적용 hello 다시 시도 작업 사이의 대기 시간 hello 의hello값에서기하급수적으로증가`interval`toohello 값 `max-interval` toohello 다음에 따라 forumula- `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-369">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-369">Usage</span></span>  
 <span data-ttu-id="bf4d1-370">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="bf4d1-371">이 정책에 의해 자식 정책 사용 제한이 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="bf4d1-372">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-373">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-374"><a name="ReturnResponse"></a> 반환 응답</span><span class="sxs-lookup"><span data-stu-id="bf4d1-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="bf4d1-375">hello `return-response` 정책 파이프라인 실행을 중단 하 고 기본 또는 사용자 지정 응답 toohello 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="bf4d1-376">기본 응답은 본문 없는 `200 OK`입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="bf4d1-377">컨텍스트 변수나 정책 문을 통해 사용자 지정 응답을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="bf4d1-378">둘 다 제공 되는 경우 hello 컨텍스트 변수 내에 포함 된 hello 응답 toohello 호출자에 게 반환 하기 전에 hello 정책 문에 의해 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-379">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-380">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf4d1-381">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-381">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-382">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-382">Element</span></span>|<span data-ttu-id="bf4d1-383">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-383">Description</span></span>|<span data-ttu-id="bf4d1-384">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-385">return-response</span><span class="sxs-lookup"><span data-stu-id="bf4d1-385">return-response</span></span>|<span data-ttu-id="bf4d1-386">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-386">Root element.</span></span>|<span data-ttu-id="bf4d1-387">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-387">Yes</span></span>|  
|<span data-ttu-id="bf4d1-388">set-header</span><span class="sxs-lookup"><span data-stu-id="bf4d1-388">set-header</span></span>|<span data-ttu-id="bf4d1-389">[set-header](api-management-transformation-policies.md#SetHTTPheader) 정책 문.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="bf4d1-390">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-390">No</span></span>|  
|<span data-ttu-id="bf4d1-391">set-body</span><span class="sxs-lookup"><span data-stu-id="bf4d1-391">set-body</span></span>|<span data-ttu-id="bf4d1-392">[set-body](api-management-transformation-policies.md#SetBody) 정책 문.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="bf4d1-393">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-393">No</span></span>|  
|<span data-ttu-id="bf4d1-394">set-status</span><span class="sxs-lookup"><span data-stu-id="bf4d1-394">set-status</span></span>|<span data-ttu-id="bf4d1-395">[set-status](api-management-advanced-policies.md#SetStatus) 정책 문.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="bf4d1-396">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-397">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-397">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-398">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-398">Attribute</span></span>|<span data-ttu-id="bf4d1-399">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-399">Description</span></span>|<span data-ttu-id="bf4d1-400">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="bf4d1-401">response-variable-name</span></span>|<span data-ttu-id="bf4d1-402">hello hello 컨텍스트 변수 이름에서 참조, 예를 들어, 업스트림 [보내기 요청](api-management-advanced-policies.md#SendRequest) 정책 및를 포함 하는 `Response` 개체</span><span class="sxs-lookup"><span data-stu-id="bf4d1-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="bf4d1-403">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-404">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-404">Usage</span></span>  
 <span data-ttu-id="bf4d1-405">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-406">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-407">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-408"><a name="SendOneWayRequest"></a> 단방향 요청 전송</span><span class="sxs-lookup"><span data-stu-id="bf4d1-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="bf4d1-409">hello `send-one-way-request` 정책 toohello 응답을 받기 위해 대기 하지 않고 URL을 지정 하는 hello 제공 된 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-410">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-411">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-411">Example</span></span>  
 <span data-ttu-id="bf4d1-412">이 샘플 정책 hello를 사용 하는 예제를 보여 줍니다. `send-one-way-request` 정책 toosend 메시지 tooa Slack: 채트 방 hello HTTP 응답 코드는 too500 보다 크거나 같은 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="bf4d1-413">이 예제에 대 한 자세한 내용은 참조 하십시오. [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-414">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-414">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-415">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-415">Element</span></span>|<span data-ttu-id="bf4d1-416">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-416">Description</span></span>|<span data-ttu-id="bf4d1-417">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="bf4d1-418">send-one-way-request</span></span>|<span data-ttu-id="bf4d1-419">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-419">Root element.</span></span>|<span data-ttu-id="bf4d1-420">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-420">Yes</span></span>|  
|<span data-ttu-id="bf4d1-421">url</span><span class="sxs-lookup"><span data-stu-id="bf4d1-421">url</span></span>|<span data-ttu-id="bf4d1-422">hello 요청의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-422">hello URL of hello request.</span></span>|<span data-ttu-id="bf4d1-423">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf4d1-424">메서드</span><span class="sxs-lookup"><span data-stu-id="bf4d1-424">method</span></span>|<span data-ttu-id="bf4d1-425">hello hello 요청에 대 한 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="bf4d1-426">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf4d1-427">머리글</span><span class="sxs-lookup"><span data-stu-id="bf4d1-427">header</span></span>|<span data-ttu-id="bf4d1-428">요청 헤더.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-428">Request header.</span></span> <span data-ttu-id="bf4d1-429">여러 요청 헤더에 여러 헤더 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="bf4d1-430">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-430">No</span></span>|  
|<span data-ttu-id="bf4d1-431">body</span><span class="sxs-lookup"><span data-stu-id="bf4d1-431">body</span></span>|<span data-ttu-id="bf4d1-432">hello 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-432">hello request body.</span></span>|<span data-ttu-id="bf4d1-433">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-434">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-434">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-435">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-435">Attribute</span></span>|<span data-ttu-id="bf4d1-436">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-436">Description</span></span>|<span data-ttu-id="bf4d1-437">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-437">Required</span></span>|<span data-ttu-id="bf4d1-438">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-439">mode="string"</span></span>|<span data-ttu-id="bf4d1-440">새 요청 또는 hello 현재 요청의 복사본 인지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="bf4d1-441">아웃 바운드 모드로 모드 = 복사 hello 요청 본문을 초기화 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="bf4d1-442">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-442">No</span></span>|<span data-ttu-id="bf4d1-443">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="bf4d1-443">New</span></span>|  
|<span data-ttu-id="bf4d1-444">name</span><span class="sxs-lookup"><span data-stu-id="bf4d1-444">name</span></span>|<span data-ttu-id="bf4d1-445">Hello hello 헤더 toobe 집합 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="bf4d1-446">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-446">Yes</span></span>|<span data-ttu-id="bf4d1-447">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-447">N/A</span></span>|  
|<span data-ttu-id="bf4d1-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="bf4d1-448">exists-action</span></span>|<span data-ttu-id="bf4d1-449">Hello 헤더가 이미 지정 되어 때 어떤 작업 tootake를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="bf4d1-450">이 특성 hello 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="bf4d1-451">-재정의할-hello 기존 헤더의 hello 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="bf4d1-452">-skip-기존 헤더 값 hello를 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="bf4d1-453">-추가-hello 값 toohello 기존 헤더 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="bf4d1-454">-delete-hello 요청에서 hello 헤더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="bf4d1-455">설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 헤더에 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="bf4d1-456">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-456">No</span></span>|<span data-ttu-id="bf4d1-457">재정의</span><span class="sxs-lookup"><span data-stu-id="bf4d1-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-458">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-458">Usage</span></span>  
 <span data-ttu-id="bf4d1-459">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-460">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-461">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-462"><a name="SendRequest"></a> 요청 전송</span><span class="sxs-lookup"><span data-stu-id="bf4d1-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="bf4d1-463">hello `send-request` 정책 toohello hello 시간 제한 값을 설정 하는 보다 더 이상 대기 URL을 지정 하는 hello 제공 된 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-464">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-465">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-465">Example</span></span>  
 <span data-ttu-id="bf4d1-466">이 예제는 한 가지 방법은 tooverify 권한 부여 서버와 참조 토큰을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="bf4d1-467">이 예제에 대 한 자세한 내용은 참조 하십시오. [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-468">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-468">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-469">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-469">Element</span></span>|<span data-ttu-id="bf4d1-470">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-470">Description</span></span>|<span data-ttu-id="bf4d1-471">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-472">send-request</span><span class="sxs-lookup"><span data-stu-id="bf4d1-472">send-request</span></span>|<span data-ttu-id="bf4d1-473">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-473">Root element.</span></span>|<span data-ttu-id="bf4d1-474">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-474">Yes</span></span>|  
|<span data-ttu-id="bf4d1-475">url</span><span class="sxs-lookup"><span data-stu-id="bf4d1-475">url</span></span>|<span data-ttu-id="bf4d1-476">hello 요청의 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-476">hello URL of hello request.</span></span>|<span data-ttu-id="bf4d1-477">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf4d1-478">메서드</span><span class="sxs-lookup"><span data-stu-id="bf4d1-478">method</span></span>|<span data-ttu-id="bf4d1-479">hello hello 요청에 대 한 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="bf4d1-480">mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf4d1-481">머리글</span><span class="sxs-lookup"><span data-stu-id="bf4d1-481">header</span></span>|<span data-ttu-id="bf4d1-482">요청 헤더.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-482">Request header.</span></span> <span data-ttu-id="bf4d1-483">여러 요청 헤더에 여러 헤더 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="bf4d1-484">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-484">No</span></span>|  
|<span data-ttu-id="bf4d1-485">body</span><span class="sxs-lookup"><span data-stu-id="bf4d1-485">body</span></span>|<span data-ttu-id="bf4d1-486">hello 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-486">hello request body.</span></span>|<span data-ttu-id="bf4d1-487">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-488">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-488">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-489">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-489">Attribute</span></span>|<span data-ttu-id="bf4d1-490">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-490">Description</span></span>|<span data-ttu-id="bf4d1-491">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-491">Required</span></span>|<span data-ttu-id="bf4d1-492">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-493">mode="string"</span></span>|<span data-ttu-id="bf4d1-494">새 요청 또는 hello 현재 요청의 복사본 인지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="bf4d1-495">아웃 바운드 모드로 모드 = 복사 hello 요청 본문을 초기화 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="bf4d1-496">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-496">No</span></span>|<span data-ttu-id="bf4d1-497">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="bf4d1-497">New</span></span>|  
|<span data-ttu-id="bf4d1-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-498">response-variable-name="string"</span></span>|<span data-ttu-id="bf4d1-499">없는 경우 `context.Response`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="bf4d1-500">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-500">No</span></span>|<span data-ttu-id="bf4d1-501">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-501">N/A</span></span>|  
|<span data-ttu-id="bf4d1-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-502">timeout="integer"</span></span>|<span data-ttu-id="bf4d1-503">hello 제한 시간 간격 (초) hello 호출 전에 toohello URL 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="bf4d1-504">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-504">No</span></span>|<span data-ttu-id="bf4d1-505">60</span><span class="sxs-lookup"><span data-stu-id="bf4d1-505">60</span></span>|  
|<span data-ttu-id="bf4d1-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-506">ignore-error</span></span>|<span data-ttu-id="bf4d1-507">True 및 hello 요청 하면 오류가 발생 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="bf4d1-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="bf4d1-508">-   response-variable-name이 지정된 경우 null 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="bf4d1-509">-   response-variable-name이 지정되지 않은 경우 context.Request가 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="bf4d1-510">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-510">No</span></span>|<span data-ttu-id="bf4d1-511">false</span><span class="sxs-lookup"><span data-stu-id="bf4d1-511">false</span></span>|  
|<span data-ttu-id="bf4d1-512">name</span><span class="sxs-lookup"><span data-stu-id="bf4d1-512">name</span></span>|<span data-ttu-id="bf4d1-513">Hello hello 헤더 toobe 집합 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="bf4d1-514">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-514">Yes</span></span>|<span data-ttu-id="bf4d1-515">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-515">N/A</span></span>|  
|<span data-ttu-id="bf4d1-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="bf4d1-516">exists-action</span></span>|<span data-ttu-id="bf4d1-517">Hello 헤더가 이미 지정 되어 때 어떤 작업 tootake를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="bf4d1-518">이 특성 hello 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="bf4d1-519">-재정의할-hello 기존 헤더의 hello 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="bf4d1-520">-skip-기존 헤더 값 hello를 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="bf4d1-521">-추가-hello 값 toohello 기존 헤더 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="bf4d1-522">-delete-hello 요청에서 hello 헤더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="bf4d1-523">설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 헤더에 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="bf4d1-524">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-524">No</span></span>|<span data-ttu-id="bf4d1-525">재정의</span><span class="sxs-lookup"><span data-stu-id="bf4d1-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-526">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-526">Usage</span></span>  
 <span data-ttu-id="bf4d1-527">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-528">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-529">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-530"><a name="SetHttpProxy"></a> HTTP 프록시 설정</span><span class="sxs-lookup"><span data-stu-id="bf4d1-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="bf4d1-531">hello `proxy` 정책을 사용 하면 HTTP 프록시를 통해 전달 요청 toobackends tooroute 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="bf4d1-532">Hello 게이트웨이와 hello 프록시 간의 HTTP (HTTPS)만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="bf4d1-533">기본 및 NTLM 인증만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-534">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-535">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-535">Example</span></span>  
<span data-ttu-id="bf4d1-536">Hello 사용 [속성](api-management-howto-properties.md) hello 사용자 이름 및 암호 tooavoid hello 정책 문서에 중요 한 정보를 저장의 값으로.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf4d1-537">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-537">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-538">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-538">Element</span></span>|<span data-ttu-id="bf4d1-539">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-539">Description</span></span>|<span data-ttu-id="bf4d1-540">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-541">proxy</span><span class="sxs-lookup"><span data-stu-id="bf4d1-541">proxy</span></span>|<span data-ttu-id="bf4d1-542">루트 요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-542">Root element</span></span>|<span data-ttu-id="bf4d1-543">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="bf4d1-544">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-544">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-545">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-545">Attribute</span></span>|<span data-ttu-id="bf4d1-546">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-546">Description</span></span>|<span data-ttu-id="bf4d1-547">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-547">Required</span></span>|<span data-ttu-id="bf4d1-548">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-549">url="문자열"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-549">url="string"</span></span>|<span data-ttu-id="bf4d1-550">Http://host:port hello 형태로 프록시 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="bf4d1-551">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-551">Yes</span></span>|<span data-ttu-id="bf4d1-552">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-552">N/A</span></span>|  
|<span data-ttu-id="bf4d1-553">사용자 이름="문자열"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-553">username="string"</span></span>|<span data-ttu-id="bf4d1-554">사용자 이름 toobe hello 프록시 인증에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="bf4d1-555">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-555">No</span></span>|<span data-ttu-id="bf4d1-556">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-556">N/A</span></span>|  
|<span data-ttu-id="bf4d1-557">암호="문자열"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-557">password="string"</span></span>|<span data-ttu-id="bf4d1-558">암호 toobe hello 프록시 인증에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="bf4d1-559">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-559">No</span></span>|<span data-ttu-id="bf4d1-560">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="bf4d1-561">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-561">Usage</span></span>  
 <span data-ttu-id="bf4d1-562">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-563">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="bf4d1-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="bf4d1-564">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf4d1-565"><a name="SetRequestMethod"></a> 요청 메서드 설정</span><span class="sxs-lookup"><span data-stu-id="bf4d1-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="bf4d1-566">hello `set-method` 정책을 사용 하면 한 요청에 대 한 toochange hello HTTP 요청 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-567">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-568">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-568">Example</span></span>  
 <span data-ttu-id="bf4d1-569">Hello를 사용 하 여이 샘플 정책을 `set-method` 정책 메시지 tooa Slack 채트 방 hello HTTP 응답 코드 보다 큰 경우 보내거나 같은 too500 모양의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="bf4d1-570">이 예제에 대 한 자세한 내용은 참조 하십시오. [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-571">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-571">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-572">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-572">Element</span></span>|<span data-ttu-id="bf4d1-573">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-573">Description</span></span>|<span data-ttu-id="bf4d1-574">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-575">set-method</span><span class="sxs-lookup"><span data-stu-id="bf4d1-575">set-method</span></span>|<span data-ttu-id="bf4d1-576">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-576">Root element.</span></span> <span data-ttu-id="bf4d1-577">hello 요소의 hello 값 hello HTTP 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="bf4d1-578">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-579">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-579">Usage</span></span>  
 <span data-ttu-id="bf4d1-580">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-581">**정책 섹션:** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-582">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-583"><a name="SetStatus"></a> 상태 코드 설정</span><span class="sxs-lookup"><span data-stu-id="bf4d1-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="bf4d1-584">hello `set-status` 정책 집합 hello HTTP 상태 코드 toohello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-585">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-586">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-586">Example</span></span>  
 <span data-ttu-id="bf4d1-587">이 예에서는 어떻게 tooreturn hello 권한 부여 토큰이 유효 하지 않을 경우 401 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="bf4d1-588">자세한 내용은 참조 [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="bf4d1-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-589">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-589">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-590">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-590">Element</span></span>|<span data-ttu-id="bf4d1-591">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-591">Description</span></span>|<span data-ttu-id="bf4d1-592">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-593">set-status</span><span class="sxs-lookup"><span data-stu-id="bf4d1-593">set-status</span></span>|<span data-ttu-id="bf4d1-594">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-594">Root element.</span></span>|<span data-ttu-id="bf4d1-595">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-596">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-596">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-597">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-597">Attribute</span></span>|<span data-ttu-id="bf4d1-598">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-598">Description</span></span>|<span data-ttu-id="bf4d1-599">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-599">Required</span></span>|<span data-ttu-id="bf4d1-600">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-601">code="integer"</span></span>|<span data-ttu-id="bf4d1-602">hello HTTP 상태 코드 tooreturn 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="bf4d1-603">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-603">Yes</span></span>|<span data-ttu-id="bf4d1-604">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-604">N/A</span></span>|  
|<span data-ttu-id="bf4d1-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="bf4d1-605">reason="string"</span></span>|<span data-ttu-id="bf4d1-606">Hello 이유 hello 상태 코드를 반환 하는 것에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="bf4d1-607">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-607">Yes</span></span>|<span data-ttu-id="bf4d1-608">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-609">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-609">Usage</span></span>  
 <span data-ttu-id="bf4d1-610">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-611">**정책 섹션:** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-612">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf4d1-613"><a name="set-variable"></a> 변수 설정</span><span class="sxs-lookup"><span data-stu-id="bf4d1-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="bf4d1-614">hello `set-variable` 정책 선언는 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 변수를 통해 지정 된 값을 할당 하 고는 [식](api-management-policy-expressions.md) 또는 문자열 리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="bf4d1-615">hello 식은 변환 리터럴을 포함 되어 있으면 tooa 문자열과 hello hello 값 됩니다 `System.String`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="bf4d1-616"><a name="set-variablePolicyStatement"></a> 정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="bf4d1-617"><a name="set-variableExample"></a> 예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="bf4d1-618">hello 다음 예제에서는 hello의 set-variable 정책을 인바운드 섹션.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="bf4d1-619">이 set-variable 정책은 만듭니다는 `isMobile` 부울 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 경우 hello tootrue 설정 된 변수 `User-Agent` 요청 헤더에 hello 텍스트 `iPad` 또는 `iPhone`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="bf4d1-620">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-620">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-621">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-621">Element</span></span>|<span data-ttu-id="bf4d1-622">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-622">Description</span></span>|<span data-ttu-id="bf4d1-623">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="bf4d1-624">set-variable</span></span>|<span data-ttu-id="bf4d1-625">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-625">Root element.</span></span>|<span data-ttu-id="bf4d1-626">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-627">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-627">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-628">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-628">Attribute</span></span>|<span data-ttu-id="bf4d1-629">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-629">Description</span></span>|<span data-ttu-id="bf4d1-630">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-631">name</span><span class="sxs-lookup"><span data-stu-id="bf4d1-631">name</span></span>|<span data-ttu-id="bf4d1-632">hello 변수의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-632">hello name of hello variable.</span></span>|<span data-ttu-id="bf4d1-633">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-633">Yes</span></span>|  
|<span data-ttu-id="bf4d1-634">값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-634">value</span></span>|<span data-ttu-id="bf4d1-635">hello 변수의 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-635">hello value of hello variable.</span></span> <span data-ttu-id="bf4d1-636">식 또는 리터럴 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="bf4d1-637">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-638">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-638">Usage</span></span>  
 <span data-ttu-id="bf4d1-639">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-640">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-641">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="bf4d1-642"><a name="set-variableAllowedTypes"></a> 허용 형식</span><span class="sxs-lookup"><span data-stu-id="bf4d1-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="bf4d1-643">Hello에 사용 된 식은 `set-variable` 정책 hello 기본 형식 다음 중 하나를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="bf4d1-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="bf4d1-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="bf4d1-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="bf4d1-645">System.SByte</span></span>  
  
-   <span data-ttu-id="bf4d1-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="bf4d1-646">System.Byte</span></span>  
  
-   <span data-ttu-id="bf4d1-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="bf4d1-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="bf4d1-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="bf4d1-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="bf4d1-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="bf4d1-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="bf4d1-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="bf4d1-650">System.Int16</span></span>  
  
-   <span data-ttu-id="bf4d1-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="bf4d1-651">System.Int32</span></span>  
  
-   <span data-ttu-id="bf4d1-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="bf4d1-652">System.Int64</span></span>  
  
-   <span data-ttu-id="bf4d1-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="bf4d1-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="bf4d1-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="bf4d1-654">System.Single</span></span>  
  
-   <span data-ttu-id="bf4d1-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="bf4d1-655">System.Double</span></span>  
  
-   <span data-ttu-id="bf4d1-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="bf4d1-656">System.Guid</span></span>  
  
-   <span data-ttu-id="bf4d1-657">System.String</span><span class="sxs-lookup"><span data-stu-id="bf4d1-657">System.String</span></span>  
  
-   <span data-ttu-id="bf4d1-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="bf4d1-658">System.Char</span></span>  
  
-   <span data-ttu-id="bf4d1-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="bf4d1-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="bf4d1-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="bf4d1-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="bf4d1-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="bf4d1-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="bf4d1-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="bf4d1-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="bf4d1-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="bf4d1-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="bf4d1-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="bf4d1-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="bf4d1-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-669">System.Single?</span></span>  
  
-   <span data-ttu-id="bf4d1-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-670">System.Double?</span></span>  
  
-   <span data-ttu-id="bf4d1-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="bf4d1-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-672">System.String?</span></span>  
  
-   <span data-ttu-id="bf4d1-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-673">System.Char?</span></span>  
  
-   <span data-ttu-id="bf4d1-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="bf4d1-674">System.DateTime?</span></span>  

##  <span data-ttu-id="bf4d1-675"><a name="Trace"></a> 추적</span><span class="sxs-lookup"><span data-stu-id="bf4d1-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="bf4d1-676">hello `trace` hello에 문자열을 추가 하는 정책 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="bf4d1-677">hello 정책 실행될지만 추적 트리거될 때, 즉, `Ocp-Apim-Trace` 존재 하며 너무 설정 되 고 요청 헤더`true` 및 `Ocp-Apim-Subscription-Key` 요청 헤더가 있고 hello 관리자 계정과 연결 된 유효한 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-678">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf4d1-679">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-679">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-680">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-680">Element</span></span>|<span data-ttu-id="bf4d1-681">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-681">Description</span></span>|<span data-ttu-id="bf4d1-682">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-683">추적</span><span class="sxs-lookup"><span data-stu-id="bf4d1-683">trace</span></span>|<span data-ttu-id="bf4d1-684">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-684">Root element.</span></span>|<span data-ttu-id="bf4d1-685">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-686">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-686">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-687">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-687">Attribute</span></span>|<span data-ttu-id="bf4d1-688">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-688">Description</span></span>|<span data-ttu-id="bf4d1-689">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-689">Required</span></span>|<span data-ttu-id="bf4d1-690">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-691">원본</span><span class="sxs-lookup"><span data-stu-id="bf4d1-691">source</span></span>|<span data-ttu-id="bf4d1-692">문자열 리터럴 의미 있는 toohello 추적 뷰어 및 hello 메시지의 hello 원본을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="bf4d1-693">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-693">Yes</span></span>|<span data-ttu-id="bf4d1-694">해당 없음</span><span class="sxs-lookup"><span data-stu-id="bf4d1-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-695">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-695">Usage</span></span>  
 <span data-ttu-id="bf4d1-696">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="bf4d1-697">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="bf4d1-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf4d1-698">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf4d1-699"><a name="Wait"></a> 대기</span><span class="sxs-lookup"><span data-stu-id="bf4d1-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="bf4d1-700">hello `wait` 정책 직계 자식 정책의 병렬로 실행 하 고 완료 되기 전에 전체 또는 해당 직계 자식 정책 toocomplete 중 하나에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="bf4d1-701">hello 대기 정책으로 가질 수 직계 자식 정책의 [보내기 요청](api-management-advanced-policies.md#SendRequest), [캐시에서 값을 가져올](api-management-caching-policies.md#GetFromCacheByKey), 및 [제어 흐름](api-management-advanced-policies.md#choose) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf4d1-702">정책 문</span><span class="sxs-lookup"><span data-stu-id="bf4d1-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf4d1-703">예제</span><span class="sxs-lookup"><span data-stu-id="bf4d1-703">Example</span></span>  
 <span data-ttu-id="bf4d1-704">다음 예제는 hello에는 두 개의 `choose` hello의 직계 자식 정책으로는 정책 `wait` 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="bf4d1-705">이러한 각 `choose` 정책이 병렬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="bf4d1-706">각 `choose` 정책 tooretrieve 캐시 된 값을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="bf4d1-707">캐시 누락 하는 경우 백 엔드 서비스 tooprovide hello 값을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="bf4d1-708">이 예제에서는 hello에 `wait` 정책에 완료 되지 않으면 모든 직계 자식 정책의 완료 될 때까지 때문에 hello `for` 특성이 너무 설정 된`all`합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="bf4d1-709">이 예제에서는 hello 컨텍스트 변수에서 (`execute-branch-one`, `value-one`, `execute-branch-two`, 및 `value-two`)이 예에서는 정책 hello 범위 외부에서 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="bf4d1-710">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-710">Elements</span></span>  
  
|<span data-ttu-id="bf4d1-711">요소</span><span class="sxs-lookup"><span data-stu-id="bf4d1-711">Element</span></span>|<span data-ttu-id="bf4d1-712">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-712">Description</span></span>|<span data-ttu-id="bf4d1-713">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf4d1-714">wait</span><span class="sxs-lookup"><span data-stu-id="bf4d1-714">wait</span></span>|<span data-ttu-id="bf4d1-715">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-715">Root element.</span></span> <span data-ttu-id="bf4d1-716">자식 요소로 `send-request`, `cache-lookup-value`, `choose` 정책만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="bf4d1-717">예</span><span class="sxs-lookup"><span data-stu-id="bf4d1-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf4d1-718">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-718">Attributes</span></span>  
  
|<span data-ttu-id="bf4d1-719">특성</span><span class="sxs-lookup"><span data-stu-id="bf4d1-719">Attribute</span></span>|<span data-ttu-id="bf4d1-720">설명</span><span class="sxs-lookup"><span data-stu-id="bf4d1-720">Description</span></span>|<span data-ttu-id="bf4d1-721">필수</span><span class="sxs-lookup"><span data-stu-id="bf4d1-721">Required</span></span>|<span data-ttu-id="bf4d1-722">기본값</span><span class="sxs-lookup"><span data-stu-id="bf4d1-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf4d1-723">for</span><span class="sxs-lookup"><span data-stu-id="bf4d1-723">for</span></span>|<span data-ttu-id="bf4d1-724">같은지 hello `wait` 정책이 모든 직계 자식 정책 toobe 완료 될 때까지 대기 또는 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="bf4d1-725">허용되는 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="bf4d1-726">-   `all`-모든 직계 자식 정책 toocomplete 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="bf4d1-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="bf4d1-727">-모든-모든 직계 자식 정책 toocomplete 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="bf4d1-728">첫 번째 직계 자식 정책은 hello 완료 되 면 hello `wait` 정책 완료 되 고 다른 직계 자식 정책의 실행이 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="bf4d1-729">아니요</span><span class="sxs-lookup"><span data-stu-id="bf4d1-729">No</span></span>|<span data-ttu-id="bf4d1-730">모두</span><span class="sxs-lookup"><span data-stu-id="bf4d1-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf4d1-731">사용</span><span class="sxs-lookup"><span data-stu-id="bf4d1-731">Usage</span></span>  
 <span data-ttu-id="bf4d1-732">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf4d1-733">**정책 섹션:** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="bf4d1-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="bf4d1-734">**정책 범위:** 모든 범위</span><span class="sxs-lookup"><span data-stu-id="bf4d1-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bf4d1-735">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf4d1-735">Next steps</span></span>
<span data-ttu-id="bf4d1-736">정책으로 작업하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf4d1-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="bf4d1-737">API 관리의 정책</span><span class="sxs-lookup"><span data-stu-id="bf4d1-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="bf4d1-738">정책 식</span><span class="sxs-lookup"><span data-stu-id="bf4d1-738">Policy expressions</span></span>](api-management-policy-expressions.md)
