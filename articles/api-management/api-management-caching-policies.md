---
title: "Azure API Management 캐싱 정책 | Microsoft Docs"
description: "Azure API Management에 사용할 수 있는 캐싱 정책에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="5e04c-103">API Management 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="5e04c-103">API Management caching policies</span></span>
<span data-ttu-id="5e04c-104">이 항목에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="5e04c-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="5e04c-106"><a name="CachingPolicies"></a> 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="5e04c-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="5e04c-107">응답 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="5e04c-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="5e04c-108">[캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="5e04c-109">[캐시에 저장](api-management-caching-policies.md#StoreToCache) - 지정된 캐시 제어 구성에 따라 응답을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="5e04c-110">값 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="5e04c-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="5e04c-111">[캐시에서 값 가져오기](#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="5e04c-112">[값을 캐시에 저장](#StoreToCacheByKey) - 키로 캐시에 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="5e04c-113">[캐시에서 값을 제거](#RemoveCacheByKey) - 키로 캐시에서 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="5e04c-114"><a name="GetFromCache"></a> 캐시에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="5e04c-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="5e04c-115">`cache-lookup` 정책을 사용하여 캐시 조회를 수행하며 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="5e04c-116">이 정책은 응답 콘텐츠가 일정 기간 동안 정적 상태인 경우 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="5e04c-117">응답 캐싱은 백 엔드 웹 서버에 부과된 대역폭 및 처리 요구 사항을 줄이며 API 소비자가 인지하는 대기 시간을 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e04c-118">이 정책에는 해당하는 [캐시에 저장](api-management-caching-policies.md#StoreToCache) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e04c-119">정책 문:</span><span class="sxs-lookup"><span data-stu-id="5e04c-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="5e04c-120">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5e04c-121">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="5e04c-122">정책 식을 사용하는 예제</span><span class="sxs-lookup"><span data-stu-id="5e04c-122">Example using policy expressions</span></span>  
 <span data-ttu-id="5e04c-123">이 예제에서는 지원 서비스의 `Cache-Control` 지시문에 지정된 대로 백 엔드 서비스의 응답 캐싱과 일치하는 API Management 응답 캐싱 기간을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="5e04c-124">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 25:25 지점으로 빨리 감기하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="5e04c-125">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5e04c-126">요소</span><span class="sxs-lookup"><span data-stu-id="5e04c-126">Elements</span></span>  
  
|<span data-ttu-id="5e04c-127">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-127">Name</span></span>|<span data-ttu-id="5e04c-128">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-128">Description</span></span>|<span data-ttu-id="5e04c-129">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e04c-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="5e04c-130">cache-lookup</span></span>|<span data-ttu-id="5e04c-131">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-131">Root element.</span></span>|<span data-ttu-id="5e04c-132">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-132">Yes</span></span>|  
|<span data-ttu-id="5e04c-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="5e04c-133">vary-by-header</span></span>|<span data-ttu-id="5e04c-134">지정된 헤더 값당 시작 캐싱 응답입니다(예: Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match).</span><span class="sxs-lookup"><span data-stu-id="5e04c-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="5e04c-135">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-135">No</span></span>|  
|<span data-ttu-id="5e04c-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="5e04c-136">vary-by-query-parameter</span></span>|<span data-ttu-id="5e04c-137">지정된 쿼리 매개 변수의 값에 따라 응답 캐싱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="5e04c-138">단일 또는 여러 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="5e04c-139">세미콜론을 구분 기호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-139">Use semicolon as a separator.</span></span> <span data-ttu-id="5e04c-140">지정하지 않은 경우 모든 쿼리 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="5e04c-141">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e04c-142">특성</span><span class="sxs-lookup"><span data-stu-id="5e04c-142">Attributes</span></span>  
  
|<span data-ttu-id="5e04c-143">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-143">Name</span></span>|<span data-ttu-id="5e04c-144">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-144">Description</span></span>|<span data-ttu-id="5e04c-145">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-145">Required</span></span>|<span data-ttu-id="5e04c-146">기본값</span><span class="sxs-lookup"><span data-stu-id="5e04c-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e04c-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="5e04c-147">allow-private-response-caching</span></span>|<span data-ttu-id="5e04c-148">`true`로 설정하면 Authorization 헤더를 포함하는 요청의 캐싱을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="5e04c-149">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-149">No</span></span>|<span data-ttu-id="5e04c-150">false</span><span class="sxs-lookup"><span data-stu-id="5e04c-150">false</span></span>|  
|<span data-ttu-id="5e04c-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="5e04c-151">downstream-caching-type</span></span>|<span data-ttu-id="5e04c-152">이 특성은 다음 값 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="5e04c-153">-   none - 다운스트림 캐싱이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="5e04c-154">-   private - 다운스트림 캐싱이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="5e04c-155">-   public - 개인 및 공유 다운스트림 캐싱이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="5e04c-156">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-156">No</span></span>|<span data-ttu-id="5e04c-157">없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-157">none</span></span>|  
|<span data-ttu-id="5e04c-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="5e04c-158">must-revalidate</span></span>|<span data-ttu-id="5e04c-159">다운스트림 캐싱을 사용하는 경우 이 특성이 게이트웨이 응답에서 `must-revalidate` 캐시 제어 지시문을 설정 또는 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="5e04c-160">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-160">No</span></span>|<span data-ttu-id="5e04c-161">true</span><span class="sxs-lookup"><span data-stu-id="5e04c-161">true</span></span>|  
|<span data-ttu-id="5e04c-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="5e04c-162">vary-by-developer</span></span>|<span data-ttu-id="5e04c-163">개발자 키별 캐시 응답을 위해서는 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="5e04c-164">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-164">No</span></span>|<span data-ttu-id="5e04c-165">false</span><span class="sxs-lookup"><span data-stu-id="5e04c-165">false</span></span>|  
|<span data-ttu-id="5e04c-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="5e04c-166">vary-by-developer-groups</span></span>|<span data-ttu-id="5e04c-167">사용자 역할별 캐시 응답을 위해서는 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="5e04c-168">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-168">No</span></span>|<span data-ttu-id="5e04c-169">false</span><span class="sxs-lookup"><span data-stu-id="5e04c-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e04c-170">사용 현황</span><span class="sxs-lookup"><span data-stu-id="5e04c-170">Usage</span></span>  
 <span data-ttu-id="5e04c-171">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e04c-172">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="5e04c-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="5e04c-173">**정책 범위:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="5e04c-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="5e04c-174"><a name="StoreToCache"></a> 캐시에 저장</span><span class="sxs-lookup"><span data-stu-id="5e04c-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="5e04c-175">`cache-store` 정책은 지정된 캐시 설정에 따라 응답을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="5e04c-176">이 정책은 응답 콘텐츠가 일정 기간 동안 정적 상태인 경우 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="5e04c-177">응답 캐싱은 백 엔드 웹 서버에 부과된 대역폭 및 처리 요구 사항을 줄이며 API 소비자가 인지하는 대기 시간을 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e04c-178">이 정책에는 해당하는 [캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e04c-179">정책 문:</span><span class="sxs-lookup"><span data-stu-id="5e04c-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="5e04c-180">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5e04c-181">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="5e04c-182">정책 식을 사용하는 예제</span><span class="sxs-lookup"><span data-stu-id="5e04c-182">Example using policy expressions</span></span>  
 <span data-ttu-id="5e04c-183">이 예제에서는 지원 서비스의 `Cache-Control` 지시문에 지정된 대로 백 엔드 서비스의 응답 캐싱과 일치하는 API Management 응답 캐싱 기간을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="5e04c-184">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 25:25 지점으로 빨리 감기하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="5e04c-185">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5e04c-186">요소</span><span class="sxs-lookup"><span data-stu-id="5e04c-186">Elements</span></span>  
  
|<span data-ttu-id="5e04c-187">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-187">Name</span></span>|<span data-ttu-id="5e04c-188">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-188">Description</span></span>|<span data-ttu-id="5e04c-189">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e04c-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="5e04c-190">cache-store</span></span>|<span data-ttu-id="5e04c-191">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-191">Root element.</span></span>|<span data-ttu-id="5e04c-192">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e04c-193">특성</span><span class="sxs-lookup"><span data-stu-id="5e04c-193">Attributes</span></span>  
  
|<span data-ttu-id="5e04c-194">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-194">Name</span></span>|<span data-ttu-id="5e04c-195">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-195">Description</span></span>|<span data-ttu-id="5e04c-196">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-196">Required</span></span>|<span data-ttu-id="5e04c-197">기본값</span><span class="sxs-lookup"><span data-stu-id="5e04c-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e04c-198">duration</span><span class="sxs-lookup"><span data-stu-id="5e04c-198">duration</span></span>|<span data-ttu-id="5e04c-199">캐시된 항목의 TTL(Time-to-Live)로 초 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="5e04c-200">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-200">Yes</span></span>|<span data-ttu-id="5e04c-201">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e04c-202">사용 현황</span><span class="sxs-lookup"><span data-stu-id="5e04c-202">Usage</span></span>  
 <span data-ttu-id="5e04c-203">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e04c-204">**정책 섹션:** outbound</span><span class="sxs-lookup"><span data-stu-id="5e04c-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="5e04c-205">**정책 범위:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="5e04c-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="5e04c-206"><a name="GetFromCacheByKey"></a> 캐시에서 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="5e04c-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="5e04c-207">`cache-lookup-value` 정책을 사용하여 키별 캐시 조회를 수행하며 캐시된 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="5e04c-208">키는 임의의 문자열 값을 포함할 수 있으며 일반적으로 정책 식을 사용하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e04c-209">이 정책에는 해당하는 [값을 캐시에 저장](#StoreToCacheByKey) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e04c-210">정책 문:</span><span class="sxs-lookup"><span data-stu-id="5e04c-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="5e04c-211">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-211">Example</span></span>  
 <span data-ttu-id="5e04c-212">이 정책에 대한 자세한 내용과 예제는 [Azure API Management의 사용자 지정 캐싱](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="5e04c-213">요소</span><span class="sxs-lookup"><span data-stu-id="5e04c-213">Elements</span></span>  
  
|<span data-ttu-id="5e04c-214">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-214">Name</span></span>|<span data-ttu-id="5e04c-215">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-215">Description</span></span>|<span data-ttu-id="5e04c-216">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e04c-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="5e04c-217">cache-lookup-value</span></span>|<span data-ttu-id="5e04c-218">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-218">Root element.</span></span>|<span data-ttu-id="5e04c-219">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e04c-220">특성</span><span class="sxs-lookup"><span data-stu-id="5e04c-220">Attributes</span></span>  
  
|<span data-ttu-id="5e04c-221">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-221">Name</span></span>|<span data-ttu-id="5e04c-222">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-222">Description</span></span>|<span data-ttu-id="5e04c-223">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-223">Required</span></span>|<span data-ttu-id="5e04c-224">기본값</span><span class="sxs-lookup"><span data-stu-id="5e04c-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e04c-225">default-value</span><span class="sxs-lookup"><span data-stu-id="5e04c-225">default-value</span></span>|<span data-ttu-id="5e04c-226">캐시 키 조회 시 누락 항목이 있는 경우 변수에 할당할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="5e04c-227">이 특성을 지정하지 않으면 `null`이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="5e04c-228">아니요</span><span class="sxs-lookup"><span data-stu-id="5e04c-228">No</span></span>|`null`|  
|<span data-ttu-id="5e04c-229">key</span><span class="sxs-lookup"><span data-stu-id="5e04c-229">key</span></span>|<span data-ttu-id="5e04c-230">조회에 사용할 캐시 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="5e04c-231">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-231">Yes</span></span>|<span data-ttu-id="5e04c-232">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-232">N/A</span></span>|  
|<span data-ttu-id="5e04c-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="5e04c-233">variable-name</span></span>|<span data-ttu-id="5e04c-234">조회에 성공한 경우 조회된 값이 할당될 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="5e04c-235">조회 시 누락 항목이 있는 경우 변수에 `default-value` 특성 또는 `null`(`default-value` 특성이 생략된 경우)이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="5e04c-236">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-236">Yes</span></span>|<span data-ttu-id="5e04c-237">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e04c-238">사용 현황</span><span class="sxs-lookup"><span data-stu-id="5e04c-238">Usage</span></span>  
 <span data-ttu-id="5e04c-239">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e04c-240">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="5e04c-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5e04c-241">**정책 범위:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="5e04c-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="5e04c-242"><a name="StoreToCacheByKey"></a> 값을 캐시에 저장</span><span class="sxs-lookup"><span data-stu-id="5e04c-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="5e04c-243">`cache-store-value`는 키로 캐시 저장을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="5e04c-244">키는 임의의 문자열 값을 포함할 수 있으며 일반적으로 정책 식을 사용하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e04c-245">이 정책에는 해당하는 [캐시에서 값 가져오기](#GetFromCacheByKey) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e04c-246">정책 문:</span><span class="sxs-lookup"><span data-stu-id="5e04c-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="5e04c-247">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-247">Example</span></span>  
 <span data-ttu-id="5e04c-248">이 정책에 대한 자세한 내용과 예제는 [Azure API Management의 사용자 지정 캐싱](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="5e04c-249">요소</span><span class="sxs-lookup"><span data-stu-id="5e04c-249">Elements</span></span>  
  
|<span data-ttu-id="5e04c-250">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-250">Name</span></span>|<span data-ttu-id="5e04c-251">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-251">Description</span></span>|<span data-ttu-id="5e04c-252">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e04c-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="5e04c-253">cache-store-value</span></span>|<span data-ttu-id="5e04c-254">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-254">Root element.</span></span>|<span data-ttu-id="5e04c-255">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e04c-256">특성</span><span class="sxs-lookup"><span data-stu-id="5e04c-256">Attributes</span></span>  
  
|<span data-ttu-id="5e04c-257">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-257">Name</span></span>|<span data-ttu-id="5e04c-258">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-258">Description</span></span>|<span data-ttu-id="5e04c-259">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-259">Required</span></span>|<span data-ttu-id="5e04c-260">기본값</span><span class="sxs-lookup"><span data-stu-id="5e04c-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e04c-261">duration</span><span class="sxs-lookup"><span data-stu-id="5e04c-261">duration</span></span>|<span data-ttu-id="5e04c-262">제공된 기간 값 동안 값(초 단위로 지정)이 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="5e04c-263">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-263">Yes</span></span>|<span data-ttu-id="5e04c-264">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-264">N/A</span></span>|  
|<span data-ttu-id="5e04c-265">key</span><span class="sxs-lookup"><span data-stu-id="5e04c-265">key</span></span>|<span data-ttu-id="5e04c-266">값을 저장할 캐시 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="5e04c-267">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-267">Yes</span></span>|<span data-ttu-id="5e04c-268">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-268">N/A</span></span>|  
|<span data-ttu-id="5e04c-269">값</span><span class="sxs-lookup"><span data-stu-id="5e04c-269">value</span></span>|<span data-ttu-id="5e04c-270">캐시될 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-270">The value to be cached.</span></span>|<span data-ttu-id="5e04c-271">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-271">Yes</span></span>|<span data-ttu-id="5e04c-272">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e04c-273">사용 현황</span><span class="sxs-lookup"><span data-stu-id="5e04c-273">Usage</span></span>  
 <span data-ttu-id="5e04c-274">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e04c-275">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="5e04c-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5e04c-276">**정책 범위:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="5e04c-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="5e04c-277"><a name="RemoveCacheByKey"></a> 캐시에서 값 제거</span><span class="sxs-lookup"><span data-stu-id="5e04c-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="5e04c-278">`cache-remove-value`는 키로 식별된 캐시 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="5e04c-279">키는 임의의 문자열 값을 포함할 수 있으며 일반적으로 정책 식을 사용하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="5e04c-280">정책 문:</span><span class="sxs-lookup"><span data-stu-id="5e04c-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="5e04c-281">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="5e04c-282">요소</span><span class="sxs-lookup"><span data-stu-id="5e04c-282">Elements</span></span>  
  
|<span data-ttu-id="5e04c-283">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-283">Name</span></span>|<span data-ttu-id="5e04c-284">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-284">Description</span></span>|<span data-ttu-id="5e04c-285">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e04c-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="5e04c-286">cache-remove-value</span></span>|<span data-ttu-id="5e04c-287">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-287">Root element.</span></span>|<span data-ttu-id="5e04c-288">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="5e04c-289">특성</span><span class="sxs-lookup"><span data-stu-id="5e04c-289">Attributes</span></span>  
  
|<span data-ttu-id="5e04c-290">이름</span><span class="sxs-lookup"><span data-stu-id="5e04c-290">Name</span></span>|<span data-ttu-id="5e04c-291">설명</span><span class="sxs-lookup"><span data-stu-id="5e04c-291">Description</span></span>|<span data-ttu-id="5e04c-292">필수</span><span class="sxs-lookup"><span data-stu-id="5e04c-292">Required</span></span>|<span data-ttu-id="5e04c-293">기본값</span><span class="sxs-lookup"><span data-stu-id="5e04c-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e04c-294">key</span><span class="sxs-lookup"><span data-stu-id="5e04c-294">key</span></span>|<span data-ttu-id="5e04c-295">캐시에서 제거할 이전에 캐시된 값의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="5e04c-296">예</span><span class="sxs-lookup"><span data-stu-id="5e04c-296">Yes</span></span>|<span data-ttu-id="5e04c-297">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e04c-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="5e04c-298">사용 현황</span><span class="sxs-lookup"><span data-stu-id="5e04c-298">Usage</span></span>  
 <span data-ttu-id="5e04c-299">다음 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에 이 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e04c-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="5e04c-300">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="5e04c-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5e04c-301">**정책 범위:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="5e04c-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="5e04c-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e04c-302">Next steps</span></span>
<span data-ttu-id="5e04c-303">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e04c-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  