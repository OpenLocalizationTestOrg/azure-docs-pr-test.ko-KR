---
title: "aaaAzure API 관리 캐싱 정책 | Microsoft Docs"
description: "Azure API 관리에서 사용 하기 위해 사용할 수 있는 정책을 캐싱 hello에 알아봅니다."
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
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="32989-103">API Management 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="32989-103">API Management caching policies</span></span>
<span data-ttu-id="32989-104">이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="32989-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32989-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="32989-106"><a name="CachingPolicies"></a> 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="32989-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="32989-107">응답 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="32989-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="32989-108">[캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="32989-109">[Toocache 저장](api-management-caching-policies.md#StoreToCache) -toohello 지정 된 캐시 제어 구성에 따라 캐시 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="32989-110">값 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="32989-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="32989-111">[캐시에서 값 가져오기](#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="32989-112">[값을 캐시에 저장](#StoreToCacheByKey) -hello 캐시에 항목을 키로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="32989-113">[캐시에서 값을 제거](#RemoveCacheByKey) -키별로 hello 캐시에 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="32989-114"><a name="GetFromCache"></a> 캐시에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="32989-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="32989-115">사용 하 여 hello `cache-lookup` 정책 tooperform 캐시 조회 및 사용 가능한 경우 유효한 캐시 된 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="32989-116">이 정책은 응답 콘텐츠가 일정 기간 동안 정적 상태인 경우 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="32989-117">응답 캐시 대역폭 줄어들고 hello 백 엔드 웹 서버와 낮추고 체감 대기 시간이 API 소비자에 처리 요구 사항을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="32989-118">이 정책은 해당 있어야 [저장소 toocache](api-management-caching-policies.md#StoreToCache) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32989-119">정책 문</span><span class="sxs-lookup"><span data-stu-id="32989-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="32989-120">예</span><span class="sxs-lookup"><span data-stu-id="32989-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="32989-121">예</span><span class="sxs-lookup"><span data-stu-id="32989-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="32989-122">정책 식을 사용하는 예제</span><span class="sxs-lookup"><span data-stu-id="32989-122">Example using policy expressions</span></span>  
 <span data-ttu-id="32989-123">캐싱 기간 일치 hello에 지정 된 대로 hello 백 엔드 서비스의 응답 캐시 hello는 tootooconfigure API 관리 응답 서비스의 백업 하는 방법을 보여 주는이 예제 `Cache-Control` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="32989-124">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too25:25 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="32989-125">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32989-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="32989-126">요소</span><span class="sxs-lookup"><span data-stu-id="32989-126">Elements</span></span>  
  
|<span data-ttu-id="32989-127">이름</span><span class="sxs-lookup"><span data-stu-id="32989-127">Name</span></span>|<span data-ttu-id="32989-128">설명</span><span class="sxs-lookup"><span data-stu-id="32989-128">Description</span></span>|<span data-ttu-id="32989-129">필수</span><span class="sxs-lookup"><span data-stu-id="32989-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32989-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="32989-130">cache-lookup</span></span>|<span data-ttu-id="32989-131">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-131">Root element.</span></span>|<span data-ttu-id="32989-132">예</span><span class="sxs-lookup"><span data-stu-id="32989-132">Yes</span></span>|  
|<span data-ttu-id="32989-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="32989-133">vary-by-header</span></span>|<span data-ttu-id="32989-134">지정된 헤더 값당 시작 캐싱 응답입니다(예: Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match).</span><span class="sxs-lookup"><span data-stu-id="32989-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="32989-135">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-135">No</span></span>|  
|<span data-ttu-id="32989-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="32989-136">vary-by-query-parameter</span></span>|<span data-ttu-id="32989-137">지정된 쿼리 매개 변수의 값에 따라 응답 캐싱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="32989-138">단일 또는 여러 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="32989-139">세미콜론을 구분 기호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-139">Use semicolon as a separator.</span></span> <span data-ttu-id="32989-140">지정하지 않은 경우 모든 쿼리 매개 변수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="32989-141">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32989-142">특성</span><span class="sxs-lookup"><span data-stu-id="32989-142">Attributes</span></span>  
  
|<span data-ttu-id="32989-143">이름</span><span class="sxs-lookup"><span data-stu-id="32989-143">Name</span></span>|<span data-ttu-id="32989-144">설명</span><span class="sxs-lookup"><span data-stu-id="32989-144">Description</span></span>|<span data-ttu-id="32989-145">필수</span><span class="sxs-lookup"><span data-stu-id="32989-145">Required</span></span>|<span data-ttu-id="32989-146">기본값</span><span class="sxs-lookup"><span data-stu-id="32989-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32989-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="32989-147">allow-private-response-caching</span></span>|<span data-ttu-id="32989-148">설정 된 경우 너무`true`, 권한 부여 헤더를 포함 하는 요청의 캐싱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="32989-149">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-149">No</span></span>|<span data-ttu-id="32989-150">false</span><span class="sxs-lookup"><span data-stu-id="32989-150">false</span></span>|  
|<span data-ttu-id="32989-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="32989-151">downstream-caching-type</span></span>|<span data-ttu-id="32989-152">이 특성의 다음 값에는 hello tooone를 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="32989-153">-   none - 다운스트림 캐싱이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32989-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="32989-154">-   private - 다운스트림 캐싱이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="32989-155">-   public - 개인 및 공유 다운스트림 캐싱이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="32989-156">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-156">No</span></span>|<span data-ttu-id="32989-157">없음</span><span class="sxs-lookup"><span data-stu-id="32989-157">none</span></span>|  
|<span data-ttu-id="32989-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="32989-158">must-revalidate</span></span>|<span data-ttu-id="32989-159">다운스트림 캐싱을 사용 하는 경우이 특성을 설정 또는 해제 hello `must-revalidate` 게이트웨이 응답에서 캐시 제어 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="32989-160">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-160">No</span></span>|<span data-ttu-id="32989-161">true</span><span class="sxs-lookup"><span data-stu-id="32989-161">true</span></span>|  
|<span data-ttu-id="32989-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="32989-162">vary-by-developer</span></span>|<span data-ttu-id="32989-163">도`true` 개발자 키별로 toocache 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="32989-164">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-164">No</span></span>|<span data-ttu-id="32989-165">false</span><span class="sxs-lookup"><span data-stu-id="32989-165">false</span></span>|  
|<span data-ttu-id="32989-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="32989-166">vary-by-developer-groups</span></span>|<span data-ttu-id="32989-167">도`true` 사용자 역할별로 toocache 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="32989-168">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-168">No</span></span>|<span data-ttu-id="32989-169">false</span><span class="sxs-lookup"><span data-stu-id="32989-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32989-170">사용</span><span class="sxs-lookup"><span data-stu-id="32989-170">Usage</span></span>  
 <span data-ttu-id="32989-171">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32989-172">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="32989-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="32989-173">**정책 범위:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="32989-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="32989-174"><a name="StoreToCache"></a>저장소 toocache</span><span class="sxs-lookup"><span data-stu-id="32989-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="32989-175">hello `cache-store` toohello에 따라 정책 캐시 응답 캐시 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="32989-176">이 정책은 응답 콘텐츠가 일정 기간 동안 정적 상태인 경우 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="32989-177">응답 캐시 대역폭 줄어들고 hello 백 엔드 웹 서버와 낮추고 체감 대기 시간이 API 소비자에 처리 요구 사항을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="32989-178">이 정책에는 해당하는 [캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32989-179">정책 문:</span><span class="sxs-lookup"><span data-stu-id="32989-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="32989-180">예</span><span class="sxs-lookup"><span data-stu-id="32989-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="32989-181">예</span><span class="sxs-lookup"><span data-stu-id="32989-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="32989-182">정책 식을 사용하는 예제</span><span class="sxs-lookup"><span data-stu-id="32989-182">Example using policy expressions</span></span>  
 <span data-ttu-id="32989-183">캐싱 기간 일치 hello에 지정 된 대로 hello 백 엔드 서비스의 응답 캐시 hello는 tootooconfigure API 관리 응답 서비스의 백업 하는 방법을 보여 주는이 예제 `Cache-Control` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="32989-184">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too25:25 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="32989-185">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32989-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="32989-186">요소</span><span class="sxs-lookup"><span data-stu-id="32989-186">Elements</span></span>  
  
|<span data-ttu-id="32989-187">이름</span><span class="sxs-lookup"><span data-stu-id="32989-187">Name</span></span>|<span data-ttu-id="32989-188">설명</span><span class="sxs-lookup"><span data-stu-id="32989-188">Description</span></span>|<span data-ttu-id="32989-189">필수</span><span class="sxs-lookup"><span data-stu-id="32989-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32989-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="32989-190">cache-store</span></span>|<span data-ttu-id="32989-191">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-191">Root element.</span></span>|<span data-ttu-id="32989-192">예</span><span class="sxs-lookup"><span data-stu-id="32989-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32989-193">특성</span><span class="sxs-lookup"><span data-stu-id="32989-193">Attributes</span></span>  
  
|<span data-ttu-id="32989-194">이름</span><span class="sxs-lookup"><span data-stu-id="32989-194">Name</span></span>|<span data-ttu-id="32989-195">설명</span><span class="sxs-lookup"><span data-stu-id="32989-195">Description</span></span>|<span data-ttu-id="32989-196">필수</span><span class="sxs-lookup"><span data-stu-id="32989-196">Required</span></span>|<span data-ttu-id="32989-197">기본값</span><span class="sxs-lookup"><span data-stu-id="32989-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32989-198">duration</span><span class="sxs-lookup"><span data-stu-id="32989-198">duration</span></span>|<span data-ttu-id="32989-199">Time-to-live hello의 시간 (초)에 지정 된 항목을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="32989-200">예</span><span class="sxs-lookup"><span data-stu-id="32989-200">Yes</span></span>|<span data-ttu-id="32989-201">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32989-202">사용</span><span class="sxs-lookup"><span data-stu-id="32989-202">Usage</span></span>  
 <span data-ttu-id="32989-203">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32989-204">**정책 섹션:** outbound</span><span class="sxs-lookup"><span data-stu-id="32989-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="32989-205">**정책 범위:** API, operation, product</span><span class="sxs-lookup"><span data-stu-id="32989-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="32989-206"><a name="GetFromCacheByKey"></a> 캐시에서 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="32989-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="32989-207">사용 하 여 hello `cache-lookup-value` 정책 tooperform 키 조회를 캐시 하 고 캐시 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="32989-208">hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="32989-209">이 정책에는 해당하는 [값을 캐시에 저장](#StoreToCacheByKey) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32989-210">정책 문:</span><span class="sxs-lookup"><span data-stu-id="32989-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="32989-211">예</span><span class="sxs-lookup"><span data-stu-id="32989-211">Example</span></span>  
 <span data-ttu-id="32989-212">이 정책에 대한 자세한 내용과 예제는 [Azure API Management의 사용자 지정 캐싱](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32989-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="32989-213">요소</span><span class="sxs-lookup"><span data-stu-id="32989-213">Elements</span></span>  
  
|<span data-ttu-id="32989-214">이름</span><span class="sxs-lookup"><span data-stu-id="32989-214">Name</span></span>|<span data-ttu-id="32989-215">설명</span><span class="sxs-lookup"><span data-stu-id="32989-215">Description</span></span>|<span data-ttu-id="32989-216">필수</span><span class="sxs-lookup"><span data-stu-id="32989-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32989-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="32989-217">cache-lookup-value</span></span>|<span data-ttu-id="32989-218">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-218">Root element.</span></span>|<span data-ttu-id="32989-219">예</span><span class="sxs-lookup"><span data-stu-id="32989-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32989-220">특성</span><span class="sxs-lookup"><span data-stu-id="32989-220">Attributes</span></span>  
  
|<span data-ttu-id="32989-221">이름</span><span class="sxs-lookup"><span data-stu-id="32989-221">Name</span></span>|<span data-ttu-id="32989-222">설명</span><span class="sxs-lookup"><span data-stu-id="32989-222">Description</span></span>|<span data-ttu-id="32989-223">필수</span><span class="sxs-lookup"><span data-stu-id="32989-223">Required</span></span>|<span data-ttu-id="32989-224">기본값</span><span class="sxs-lookup"><span data-stu-id="32989-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32989-225">default-value</span><span class="sxs-lookup"><span data-stu-id="32989-225">default-value</span></span>|<span data-ttu-id="32989-226">할당할 toohello 변수 hello 캐시 키 조회 결과 누락 값입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="32989-227">이 특성을 지정하지 않으면 `null`이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="32989-228">아니요</span><span class="sxs-lookup"><span data-stu-id="32989-228">No</span></span>|`null`|  
|<span data-ttu-id="32989-229">key</span><span class="sxs-lookup"><span data-stu-id="32989-229">key</span></span>|<span data-ttu-id="32989-230">키 값 toouse hello 조회에서를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="32989-231">예</span><span class="sxs-lookup"><span data-stu-id="32989-231">Yes</span></span>|<span data-ttu-id="32989-232">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-232">N/A</span></span>|  
|<span data-ttu-id="32989-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="32989-233">variable-name</span></span>|<span data-ttu-id="32989-234">Hello의 이름 [컨텍스트 변수의](api-management-policy-expressions.md#ContextVariables) 조회에 성공 하면 값을 조회 하는 hello에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="32989-235">조회 누락에 결과가 hello 변수 hello의 hello 값이 할당 됩니다 `default-value` 특성 또는 `null`경우 hello `default-value` 특성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="32989-236">예</span><span class="sxs-lookup"><span data-stu-id="32989-236">Yes</span></span>|<span data-ttu-id="32989-237">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32989-238">사용</span><span class="sxs-lookup"><span data-stu-id="32989-238">Usage</span></span>  
 <span data-ttu-id="32989-239">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32989-240">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="32989-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="32989-241">**정책 범위:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="32989-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="32989-242"><a name="StoreToCacheByKey"></a> 값을 캐시에 저장</span><span class="sxs-lookup"><span data-stu-id="32989-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="32989-243">hello `cache-store-value` 키로 캐시 저장소를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="32989-244">hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="32989-245">이 정책에는 해당하는 [캐시에서 값 가져오기](#GetFromCacheByKey) 정책이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="32989-246">정책 문:</span><span class="sxs-lookup"><span data-stu-id="32989-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="32989-247">예</span><span class="sxs-lookup"><span data-stu-id="32989-247">Example</span></span>  
 <span data-ttu-id="32989-248">이 정책에 대한 자세한 내용과 예제는 [Azure API Management의 사용자 지정 캐싱](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32989-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="32989-249">요소</span><span class="sxs-lookup"><span data-stu-id="32989-249">Elements</span></span>  
  
|<span data-ttu-id="32989-250">이름</span><span class="sxs-lookup"><span data-stu-id="32989-250">Name</span></span>|<span data-ttu-id="32989-251">설명</span><span class="sxs-lookup"><span data-stu-id="32989-251">Description</span></span>|<span data-ttu-id="32989-252">필수</span><span class="sxs-lookup"><span data-stu-id="32989-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32989-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="32989-253">cache-store-value</span></span>|<span data-ttu-id="32989-254">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-254">Root element.</span></span>|<span data-ttu-id="32989-255">예</span><span class="sxs-lookup"><span data-stu-id="32989-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="32989-256">특성</span><span class="sxs-lookup"><span data-stu-id="32989-256">Attributes</span></span>  
  
|<span data-ttu-id="32989-257">이름</span><span class="sxs-lookup"><span data-stu-id="32989-257">Name</span></span>|<span data-ttu-id="32989-258">설명</span><span class="sxs-lookup"><span data-stu-id="32989-258">Description</span></span>|<span data-ttu-id="32989-259">필수</span><span class="sxs-lookup"><span data-stu-id="32989-259">Required</span></span>|<span data-ttu-id="32989-260">기본값</span><span class="sxs-lookup"><span data-stu-id="32989-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32989-261">duration</span><span class="sxs-lookup"><span data-stu-id="32989-261">duration</span></span>|<span data-ttu-id="32989-262">값은 초 단위로 지정 하는 기간 값을 제공 하는 hello에 대 한 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="32989-263">예</span><span class="sxs-lookup"><span data-stu-id="32989-263">Yes</span></span>|<span data-ttu-id="32989-264">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-264">N/A</span></span>|  
|<span data-ttu-id="32989-265">key</span><span class="sxs-lookup"><span data-stu-id="32989-265">key</span></span>|<span data-ttu-id="32989-266">캐시 키 hello 값 아래에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="32989-267">예</span><span class="sxs-lookup"><span data-stu-id="32989-267">Yes</span></span>|<span data-ttu-id="32989-268">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-268">N/A</span></span>|  
|<span data-ttu-id="32989-269">값</span><span class="sxs-lookup"><span data-stu-id="32989-269">value</span></span>|<span data-ttu-id="32989-270">hello 값 toobe 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-270">hello value toobe cached.</span></span>|<span data-ttu-id="32989-271">예</span><span class="sxs-lookup"><span data-stu-id="32989-271">Yes</span></span>|<span data-ttu-id="32989-272">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="32989-273">사용</span><span class="sxs-lookup"><span data-stu-id="32989-273">Usage</span></span>  
 <span data-ttu-id="32989-274">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="32989-275">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="32989-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="32989-276">**정책 범위:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="32989-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="32989-277"><a name="RemoveCacheByKey"></a> 캐시에서 값 제거</span><span class="sxs-lookup"><span data-stu-id="32989-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="32989-278">hello `cache-remove-value` 해당 키로 식별 된 캐시 된 항목을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="32989-279">hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32989-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="32989-280">정책 문</span><span class="sxs-lookup"><span data-stu-id="32989-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="32989-281">예</span><span class="sxs-lookup"><span data-stu-id="32989-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="32989-282">요소</span><span class="sxs-lookup"><span data-stu-id="32989-282">Elements</span></span>  
  
|<span data-ttu-id="32989-283">이름</span><span class="sxs-lookup"><span data-stu-id="32989-283">Name</span></span>|<span data-ttu-id="32989-284">설명</span><span class="sxs-lookup"><span data-stu-id="32989-284">Description</span></span>|<span data-ttu-id="32989-285">필수</span><span class="sxs-lookup"><span data-stu-id="32989-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="32989-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="32989-286">cache-remove-value</span></span>|<span data-ttu-id="32989-287">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="32989-287">Root element.</span></span>|<span data-ttu-id="32989-288">예</span><span class="sxs-lookup"><span data-stu-id="32989-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="32989-289">특성</span><span class="sxs-lookup"><span data-stu-id="32989-289">Attributes</span></span>  
  
|<span data-ttu-id="32989-290">이름</span><span class="sxs-lookup"><span data-stu-id="32989-290">Name</span></span>|<span data-ttu-id="32989-291">설명</span><span class="sxs-lookup"><span data-stu-id="32989-291">Description</span></span>|<span data-ttu-id="32989-292">필수</span><span class="sxs-lookup"><span data-stu-id="32989-292">Required</span></span>|<span data-ttu-id="32989-293">기본값</span><span class="sxs-lookup"><span data-stu-id="32989-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="32989-294">key</span><span class="sxs-lookup"><span data-stu-id="32989-294">key</span></span>|<span data-ttu-id="32989-295">hello의 hello 키 값 toobe hello 캐시에서 제거를 이전에 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="32989-296">예</span><span class="sxs-lookup"><span data-stu-id="32989-296">Yes</span></span>|<span data-ttu-id="32989-297">해당 없음</span><span class="sxs-lookup"><span data-stu-id="32989-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="32989-298">사용</span><span class="sxs-lookup"><span data-stu-id="32989-298">Usage</span></span>  
 <span data-ttu-id="32989-299">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) 합니다.</span><span class="sxs-lookup"><span data-stu-id="32989-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="32989-300">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="32989-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="32989-301">**정책 범위:** global, API, operation, product</span><span class="sxs-lookup"><span data-stu-id="32989-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="32989-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32989-302">Next steps</span></span>
<span data-ttu-id="32989-303">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32989-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  