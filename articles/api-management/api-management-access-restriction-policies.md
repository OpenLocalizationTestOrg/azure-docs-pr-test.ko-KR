---
title: "Azure API Management 액세스 제한 정책 | Microsoft Docs"
description: "Azure API Management에 사용할 수 있는 액세스 제한 정책에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="858ee-103">API Management 액세스 제한 정책</span><span class="sxs-lookup"><span data-stu-id="858ee-103">API Management access restriction policies</span></span>
<span data-ttu-id="858ee-104">이 항목에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="858ee-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="858ee-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="858ee-106"><a name="AccessRestrictionPolicies"></a> 액세스 제한 정책</span><span class="sxs-lookup"><span data-stu-id="858ee-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="858ee-107">[HTTP 헤더 확인](api-management-access-restriction-policies.md#CheckHTTPHeader) - HTTP 헤더의 존재 및/또는 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="858ee-108">[구독으로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRate) - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="858ee-109">[키로 호출 속도 제한](#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="858ee-110">[호출자 IP 제한](api-management-access-restriction-policies.md#RestrictCallerIPs) - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="858ee-111">[구독으로 사용 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuota) - 구독을 기준으로 갱신 가능 또는 수명 호출 볼륨 및/또는 대역폭 할당량을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="858ee-112">[키로 사용 할당량 설정](#SetUsageQuotaByKey) - 키를 기준으로 갱신 가능 또는 수명 호출 볼륨 및/또는 대역폭 할당량을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="858ee-113">[JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="858ee-114"><a name="CheckHTTPHeader"></a> HTTP 헤더 확인</span><span class="sxs-lookup"><span data-stu-id="858ee-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="858ee-115">`check-header` 정책을 사용하여 요청에 HTTP 헤더가 지정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="858ee-116">필요에 따라 헤더에 특정 값이 있는지, 허용되는 범위의 값인지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="858ee-117">확인에 실패하면 정책에서 요청 처리를 종료하고 정책에 지정된 HTTP 상태 코드 및 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-118">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="858ee-119">예</span><span class="sxs-lookup"><span data-stu-id="858ee-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-120">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-120">Elements</span></span>  
  
|<span data-ttu-id="858ee-121">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-121">Name</span></span>|<span data-ttu-id="858ee-122">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-122">Description</span></span>|<span data-ttu-id="858ee-123">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="858ee-124">check-header</span><span class="sxs-lookup"><span data-stu-id="858ee-124">check-header</span></span>|<span data-ttu-id="858ee-125">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-125">Root element.</span></span>|<span data-ttu-id="858ee-126">예</span><span class="sxs-lookup"><span data-stu-id="858ee-126">Yes</span></span>|  
|<span data-ttu-id="858ee-127">값</span><span class="sxs-lookup"><span data-stu-id="858ee-127">value</span></span>|<span data-ttu-id="858ee-128">허용된 HTTP 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-128">Allowed HTTP header value.</span></span> <span data-ttu-id="858ee-129">여러 값 요소가 지정된 경우 값 중 하나와 일치하면 확인에 성공한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="858ee-130">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-131">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-131">Attributes</span></span>  
  
|<span data-ttu-id="858ee-132">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-132">Name</span></span>|<span data-ttu-id="858ee-133">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-133">Description</span></span>|<span data-ttu-id="858ee-134">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-134">Required</span></span>|<span data-ttu-id="858ee-135">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="858ee-136">failed-check-error-message</span></span>|<span data-ttu-id="858ee-137">헤더가 없거나 잘못된 값이 있는 경우 HTTP 응답 본문에 반환할 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="858ee-138">이 메시지는 적절히 이스케이프된 특수 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="858ee-139">예</span><span class="sxs-lookup"><span data-stu-id="858ee-139">Yes</span></span>|<span data-ttu-id="858ee-140">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-140">N/A</span></span>|  
|<span data-ttu-id="858ee-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="858ee-141">failed-check-httpcode</span></span>|<span data-ttu-id="858ee-142">헤더가 없거나 잘못된 값이 있는 경우 반환할 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="858ee-143">예</span><span class="sxs-lookup"><span data-stu-id="858ee-143">Yes</span></span>|<span data-ttu-id="858ee-144">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-144">N/A</span></span>|  
|<span data-ttu-id="858ee-145">header-name</span><span class="sxs-lookup"><span data-stu-id="858ee-145">header-name</span></span>|<span data-ttu-id="858ee-146">확인할 HTTP 헤더의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="858ee-147">예</span><span class="sxs-lookup"><span data-stu-id="858ee-147">Yes</span></span>|<span data-ttu-id="858ee-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-148">N/A</span></span>|  
|<span data-ttu-id="858ee-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="858ee-149">ignore-case</span></span>|<span data-ttu-id="858ee-150">True 또는 False로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-150">Can be set to True or False.</span></span> <span data-ttu-id="858ee-151">True로 설정되면 헤더 값을 허용 가능한 값 집합과 비교할 때 대소문자가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="858ee-152">예</span><span class="sxs-lookup"><span data-stu-id="858ee-152">Yes</span></span>|<span data-ttu-id="858ee-153">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-154">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-154">Usage</span></span>  
 <span data-ttu-id="858ee-155">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-156">**정책 섹션:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="858ee-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="858ee-157">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="858ee-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="858ee-158"><a name="LimitCallRate"></a> 구독으로 호출 속도 제한</span><span class="sxs-lookup"><span data-stu-id="858ee-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="858ee-159">`rate-limit` 정책은 호출 속도를 지정된 기간당 지정된 숫자로 제한하여 구독 하나당 최대 API 사용을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="858ee-160">이 정책이 트리거되는 경우 호출자는 `429 Too Many Requests` 응답 상태 코드를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="858ee-161">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="858ee-162">[정책 식](api-management-policy-expressions.md)은 이 정책에 대한 정책 특성에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-163">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="858ee-164">예</span><span class="sxs-lookup"><span data-stu-id="858ee-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-165">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-165">Elements</span></span>  
  
|<span data-ttu-id="858ee-166">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-166">Name</span></span>|<span data-ttu-id="858ee-167">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-167">Description</span></span>|<span data-ttu-id="858ee-168">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="858ee-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="858ee-169">set-limit</span></span>|<span data-ttu-id="858ee-170">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-170">Root element.</span></span>|<span data-ttu-id="858ee-171">예</span><span class="sxs-lookup"><span data-stu-id="858ee-171">Yes</span></span>|  
|<span data-ttu-id="858ee-172">api</span><span class="sxs-lookup"><span data-stu-id="858ee-172">api</span></span>|<span data-ttu-id="858ee-173">제품 내에서 API에 호출 속도 제한을 적용하려면 이러한 요소 중 하나 이상을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="858ee-174">제품 및 API 호출 속도 제한은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="858ee-175">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-175">No</span></span>|  
|<span data-ttu-id="858ee-176">operation</span><span class="sxs-lookup"><span data-stu-id="858ee-176">operation</span></span>|<span data-ttu-id="858ee-177">API 내에서 작업에 호출 속도 제한을 적용하려면 이러한 요소 중 하나 이상을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="858ee-178">제품, API 및 작업 호출 속도 제한은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="858ee-179">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-180">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-180">Attributes</span></span>  
  
|<span data-ttu-id="858ee-181">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-181">Name</span></span>|<span data-ttu-id="858ee-182">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-182">Description</span></span>|<span data-ttu-id="858ee-183">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-183">Required</span></span>|<span data-ttu-id="858ee-184">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-185">name</span><span class="sxs-lookup"><span data-stu-id="858ee-185">name</span></span>|<span data-ttu-id="858ee-186">속도 제한을 적용할 API의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="858ee-187">예</span><span class="sxs-lookup"><span data-stu-id="858ee-187">Yes</span></span>|<span data-ttu-id="858ee-188">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-188">N/A</span></span>|  
|<span data-ttu-id="858ee-189">calls</span><span class="sxs-lookup"><span data-stu-id="858ee-189">calls</span></span>|<span data-ttu-id="858ee-190">`renewal-period`에 지정된 시간 간격 동안 허용된 전체 최대 호출 수입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="858ee-191">예</span><span class="sxs-lookup"><span data-stu-id="858ee-191">Yes</span></span>|<span data-ttu-id="858ee-192">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-192">N/A</span></span>|  
|<span data-ttu-id="858ee-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="858ee-193">renewal-period</span></span>|<span data-ttu-id="858ee-194">할당량이 재설정되는 초 단위의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="858ee-195">예</span><span class="sxs-lookup"><span data-stu-id="858ee-195">Yes</span></span>|<span data-ttu-id="858ee-196">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-197">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-197">Usage</span></span>  
 <span data-ttu-id="858ee-198">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-199">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="858ee-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="858ee-200">**정책 범위:** product</span><span class="sxs-lookup"><span data-stu-id="858ee-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="858ee-201"><a name="LimitCallRateByKey"></a> 키로 호출 속도 제한</span><span class="sxs-lookup"><span data-stu-id="858ee-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="858ee-202">`rate-limit-by-key` 정책은 호출 속도를 지정된 기간당 지정된 숫자로 제한하여 키 하나당 최대 API 사용을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="858ee-203">키는 임의의 문자열 값을 포함할 수 있으며 일반적으로 정책 식을 사용하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="858ee-204">제한에 포함될 요청을 지정하기 위해 선택적 증분 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="858ee-205">이 정책이 트리거되는 경우 호출자는 `429 Too Many Requests` 응답 상태 코드를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="858ee-206">이 정책에 대한 자세한 내용과 예제는 [Azure API Management로 고급 요청 제한](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="858ee-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="858ee-207">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-208">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="858ee-209">예</span><span class="sxs-lookup"><span data-stu-id="858ee-209">Example</span></span>  
 <span data-ttu-id="858ee-210">다음 예제에서 속도 제한은 호출자 IP 주소를 키로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-211">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-211">Elements</span></span>  
  
|<span data-ttu-id="858ee-212">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-212">Name</span></span>|<span data-ttu-id="858ee-213">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-213">Description</span></span>|<span data-ttu-id="858ee-214">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="858ee-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="858ee-215">set-limit</span></span>|<span data-ttu-id="858ee-216">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-216">Root element.</span></span>|<span data-ttu-id="858ee-217">예</span><span class="sxs-lookup"><span data-stu-id="858ee-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-218">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-218">Attributes</span></span>  
  
|<span data-ttu-id="858ee-219">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-219">Name</span></span>|<span data-ttu-id="858ee-220">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-220">Description</span></span>|<span data-ttu-id="858ee-221">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-221">Required</span></span>|<span data-ttu-id="858ee-222">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-223">calls</span><span class="sxs-lookup"><span data-stu-id="858ee-223">calls</span></span>|<span data-ttu-id="858ee-224">`renewal-period`에 지정된 시간 간격 동안 허용된 전체 최대 호출 수입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="858ee-225">예</span><span class="sxs-lookup"><span data-stu-id="858ee-225">Yes</span></span>|<span data-ttu-id="858ee-226">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-226">N/A</span></span>|  
|<span data-ttu-id="858ee-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="858ee-227">counter-key</span></span>|<span data-ttu-id="858ee-228">속도 제한 정책에 사용할 키입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="858ee-229">예</span><span class="sxs-lookup"><span data-stu-id="858ee-229">Yes</span></span>|<span data-ttu-id="858ee-230">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-230">N/A</span></span>|  
|<span data-ttu-id="858ee-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="858ee-231">increment-condition</span></span>|<span data-ttu-id="858ee-232">요청을 할당량에 포함할지를 지정하는 부울 식입니다(`true`).</span><span class="sxs-lookup"><span data-stu-id="858ee-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="858ee-233">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-233">No</span></span>|<span data-ttu-id="858ee-234">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-234">N/A</span></span>|  
|<span data-ttu-id="858ee-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="858ee-235">renewal-period</span></span>|<span data-ttu-id="858ee-236">할당량이 재설정되는 초 단위의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="858ee-237">예</span><span class="sxs-lookup"><span data-stu-id="858ee-237">Yes</span></span>|<span data-ttu-id="858ee-238">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-239">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-239">Usage</span></span>  
 <span data-ttu-id="858ee-240">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-241">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="858ee-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="858ee-242">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="858ee-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="858ee-243"><a name="RestrictCallerIPs"></a> 호출자 IP 제한</span><span class="sxs-lookup"><span data-stu-id="858ee-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="858ee-244">`ip-filter` 정책은 특정 IP 주소 및/또는 주소 범위에서 호출을 필터링(허용/거부)합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-245">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="858ee-246">예</span><span class="sxs-lookup"><span data-stu-id="858ee-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-247">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-247">Elements</span></span>  
  
|<span data-ttu-id="858ee-248">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-248">Name</span></span>|<span data-ttu-id="858ee-249">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-249">Description</span></span>|<span data-ttu-id="858ee-250">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="858ee-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="858ee-251">ip-filter</span></span>|<span data-ttu-id="858ee-252">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-252">Root element.</span></span>|<span data-ttu-id="858ee-253">예</span><span class="sxs-lookup"><span data-stu-id="858ee-253">Yes</span></span>|  
|<span data-ttu-id="858ee-254">address</span><span class="sxs-lookup"><span data-stu-id="858ee-254">address</span></span>|<span data-ttu-id="858ee-255">필터링할 단일 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="858ee-256">하나 이상의 `address` 또는 `address-range` 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="858ee-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="858ee-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="858ee-258">필터링할 IP 주소 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="858ee-259">하나 이상의 `address` 또는 `address-range` 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-260">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-260">Attributes</span></span>  
  
|<span data-ttu-id="858ee-261">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-261">Name</span></span>|<span data-ttu-id="858ee-262">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-262">Description</span></span>|<span data-ttu-id="858ee-263">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-263">Required</span></span>|<span data-ttu-id="858ee-264">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="858ee-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="858ee-266">액세스를 허용 또는 거부할 IP 주소 범위</span><span class="sxs-lookup"><span data-stu-id="858ee-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="858ee-267">`address-range` 요소가 사용될 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="858ee-268">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-268">N/A</span></span>|  
|<span data-ttu-id="858ee-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="858ee-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="858ee-270">지정된 IP 주소 및 범위에 대해 호출을 허용해야 할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="858ee-271">예</span><span class="sxs-lookup"><span data-stu-id="858ee-271">Yes</span></span>|<span data-ttu-id="858ee-272">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-273">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-273">Usage</span></span>  
 <span data-ttu-id="858ee-274">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-275">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="858ee-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="858ee-276">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="858ee-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="858ee-277"><a name="SetUsageQuota"></a> 구독으로 사용 할당량 설정</span><span class="sxs-lookup"><span data-stu-id="858ee-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="858ee-278">`quota` 정책은 구독을 기준으로 갱신 가능 또는 수명 호출 볼륨 및/또는 대역폭 할당량을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="858ee-279">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="858ee-280">[정책 식](api-management-policy-expressions.md)은 이 정책에 대한 정책 특성에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-281">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="858ee-282">예</span><span class="sxs-lookup"><span data-stu-id="858ee-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-283">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-283">Elements</span></span>  
  
|<span data-ttu-id="858ee-284">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-284">Name</span></span>|<span data-ttu-id="858ee-285">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-285">Description</span></span>|<span data-ttu-id="858ee-286">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="858ee-287">quota</span><span class="sxs-lookup"><span data-stu-id="858ee-287">quota</span></span>|<span data-ttu-id="858ee-288">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-288">Root element.</span></span>|<span data-ttu-id="858ee-289">예</span><span class="sxs-lookup"><span data-stu-id="858ee-289">Yes</span></span>|  
|<span data-ttu-id="858ee-290">api</span><span class="sxs-lookup"><span data-stu-id="858ee-290">api</span></span>|<span data-ttu-id="858ee-291">제품 내에서 API에 대한 할당량을 적용하려면 이러한 요소 중 하나 이상을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="858ee-292">제품 및 API 할당량은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="858ee-293">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-293">No</span></span>|  
|<span data-ttu-id="858ee-294">operation</span><span class="sxs-lookup"><span data-stu-id="858ee-294">operation</span></span>|<span data-ttu-id="858ee-295">API 내에서 작업에 할당량을 적용하려면 이러한 요소 중 하나 이상을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="858ee-296">제품, API 및 작업 할당량은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="858ee-297">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-298">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-298">Attributes</span></span>  
  
|<span data-ttu-id="858ee-299">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-299">Name</span></span>|<span data-ttu-id="858ee-300">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-300">Description</span></span>|<span data-ttu-id="858ee-301">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-301">Required</span></span>|<span data-ttu-id="858ee-302">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-303">name</span><span class="sxs-lookup"><span data-stu-id="858ee-303">name</span></span>|<span data-ttu-id="858ee-304">할당량이 적용되는 API 또는 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="858ee-305">예</span><span class="sxs-lookup"><span data-stu-id="858ee-305">Yes</span></span>|<span data-ttu-id="858ee-306">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-306">N/A</span></span>|  
|<span data-ttu-id="858ee-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="858ee-307">bandwidth</span></span>|<span data-ttu-id="858ee-308">`renewal-period`에 지정된 시간 간격 동안 허용된 전체 최대 킬로바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="858ee-309">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="858ee-310">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-310">N/A</span></span>|  
|<span data-ttu-id="858ee-311">calls</span><span class="sxs-lookup"><span data-stu-id="858ee-311">calls</span></span>|<span data-ttu-id="858ee-312">`renewal-period`에 지정된 시간 간격 동안 허용된 전체 최대 호출 수입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="858ee-313">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="858ee-314">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-314">N/A</span></span>|  
|<span data-ttu-id="858ee-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="858ee-315">renewal-period</span></span>|<span data-ttu-id="858ee-316">할당량이 재설정되는 초 단위의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="858ee-317">예</span><span class="sxs-lookup"><span data-stu-id="858ee-317">Yes</span></span>|<span data-ttu-id="858ee-318">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-319">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-319">Usage</span></span>  
 <span data-ttu-id="858ee-320">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-321">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="858ee-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="858ee-322">**정책 범위:** product</span><span class="sxs-lookup"><span data-stu-id="858ee-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="858ee-323"><a name="SetUsageQuotaByKey"></a> 키로 사용 할당량 설정</span><span class="sxs-lookup"><span data-stu-id="858ee-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="858ee-324">`quota-by-key` 정책은 키를 기준으로 갱신 가능 또는 수명 호출 볼륨 및/또는 대역폭 할당량을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="858ee-325">키는 임의의 문자열 값을 포함할 수 있으며 일반적으로 정책 식을 사용하여 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="858ee-326">할당량에 포함될 요청을 지정하기 위해 선택적 증분 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="858ee-327">이 정책에 대한 자세한 내용과 예제는 [Azure API Management로 고급 요청 제한](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="858ee-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="858ee-328">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="858ee-329">[정책 식](api-management-policy-expressions.md)은 이 정책에 대한 정책 특성에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-330">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="858ee-331">예</span><span class="sxs-lookup"><span data-stu-id="858ee-331">Example</span></span>  
 <span data-ttu-id="858ee-332">다음 예제에서 할당량은 호출자 IP 주소를 키로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-333">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-333">Elements</span></span>  
  
|<span data-ttu-id="858ee-334">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-334">Name</span></span>|<span data-ttu-id="858ee-335">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-335">Description</span></span>|<span data-ttu-id="858ee-336">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="858ee-337">quota</span><span class="sxs-lookup"><span data-stu-id="858ee-337">quota</span></span>|<span data-ttu-id="858ee-338">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-338">Root element.</span></span>|<span data-ttu-id="858ee-339">예</span><span class="sxs-lookup"><span data-stu-id="858ee-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-340">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-340">Attributes</span></span>  
  
|<span data-ttu-id="858ee-341">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-341">Name</span></span>|<span data-ttu-id="858ee-342">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-342">Description</span></span>|<span data-ttu-id="858ee-343">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-343">Required</span></span>|<span data-ttu-id="858ee-344">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="858ee-345">bandwidth</span></span>|<span data-ttu-id="858ee-346">`renewal-period`에 지정된 시간 간격 동안 허용된 전체 최대 킬로바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="858ee-347">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="858ee-348">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-348">N/A</span></span>|  
|<span data-ttu-id="858ee-349">calls</span><span class="sxs-lookup"><span data-stu-id="858ee-349">calls</span></span>|<span data-ttu-id="858ee-350">`renewal-period`에 지정된 시간 간격 동안 허용된 전체 최대 호출 수입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="858ee-351">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="858ee-352">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-352">N/A</span></span>|  
|<span data-ttu-id="858ee-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="858ee-353">counter-key</span></span>|<span data-ttu-id="858ee-354">할당량 정책에 사용할 키입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="858ee-355">예</span><span class="sxs-lookup"><span data-stu-id="858ee-355">Yes</span></span>|<span data-ttu-id="858ee-356">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-356">N/A</span></span>|  
|<span data-ttu-id="858ee-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="858ee-357">increment-condition</span></span>|<span data-ttu-id="858ee-358">요청을 할당량에 포함할지를 지정하는 부울 식입니다(`true`).</span><span class="sxs-lookup"><span data-stu-id="858ee-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="858ee-359">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-359">No</span></span>|<span data-ttu-id="858ee-360">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-360">N/A</span></span>|  
|<span data-ttu-id="858ee-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="858ee-361">renewal-period</span></span>|<span data-ttu-id="858ee-362">할당량이 재설정되는 초 단위의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="858ee-363">예</span><span class="sxs-lookup"><span data-stu-id="858ee-363">Yes</span></span>|<span data-ttu-id="858ee-364">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-365">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-365">Usage</span></span>  
 <span data-ttu-id="858ee-366">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-367">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="858ee-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="858ee-368">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="858ee-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="858ee-369"><a name="ValidateJWT"></a> JWT 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="858ee-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="858ee-370">`validate-jwt` 정책은 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="858ee-371">`validate-jwt` 정책에서는 `require-expiration-time` 특정이 지정되지 않았고 `false`로 설정된 경우 `exp` 등록 클레임이 JWT 토큰에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="858ee-372">`validate-jwt` 정책은 HS256 및 RS256 서명 알고리즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="858ee-373">HS256의 경우 키를 base64 인코딩 양식으로 정책 내에 인라인으로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="858ee-374">RS256의 경우 Open ID 구성 끝점을 통해 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="858ee-375">정책 문:</span><span class="sxs-lookup"><span data-stu-id="858ee-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="858ee-376">예</span><span class="sxs-lookup"><span data-stu-id="858ee-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="858ee-377">Azure Mobile Services 토큰 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="858ee-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="858ee-378">Azure Active Directory 토큰 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="858ee-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="858ee-379">Azure Active Directory B2C 토큰 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="858ee-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="858ee-380">토큰 클레임 기반 작업에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="858ee-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="858ee-381">이 예제에서는 [JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) 정책을 사용하여 토큰 클레임 기반 작업에 대해 미리 권한을 부여하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="858ee-382">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 13:50 지점으로 빨리 감기하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="858ee-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="858ee-383">15분으로 빨리 감기하여 정책 편집기에 구성된 정책을 본 다음 18분 50초로 빨리 감기하여 필수 권한 부여 토큰 포함 및 제외 모두의 경우로 개발자 포털에서 작업 호출의 데모를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="858ee-384">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-384">Elements</span></span>  
  
|<span data-ttu-id="858ee-385">요소</span><span class="sxs-lookup"><span data-stu-id="858ee-385">Element</span></span>|<span data-ttu-id="858ee-386">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-386">Description</span></span>|<span data-ttu-id="858ee-387">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="858ee-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="858ee-388">validate-jwt</span></span>|<span data-ttu-id="858ee-389">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-389">Root element.</span></span>|<span data-ttu-id="858ee-390">예</span><span class="sxs-lookup"><span data-stu-id="858ee-390">Yes</span></span>|  
|<span data-ttu-id="858ee-391">audiences</span><span class="sxs-lookup"><span data-stu-id="858ee-391">audiences</span></span>|<span data-ttu-id="858ee-392">토큰에 제공할 수 있는 허용 가능한 대상 그룹 클레임 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="858ee-393">여러 대상 그룹 값이 있는 경우 각 값은 모든 값이 소진(이 경우 유효성 검사 실패)되거나 한 값이 성공할 때까지 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="858ee-394">한 명 이상의 대상 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-394">At least one audience must be specified.</span></span>|<span data-ttu-id="858ee-395">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-395">No</span></span>|  
|<span data-ttu-id="858ee-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="858ee-396">issuer-signing-keys</span></span>|<span data-ttu-id="858ee-397">서명된 토큰의 유효성을 검사하는 데 사용되는 Base64 인코딩 보안 키의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="858ee-398">보안 키가 여러 개 있는 경우 각 키는 모든 키가 소진(이 경우 유효성 검사 실패)되거나 한 개 키가 성공할 때까지 시도됩니다(토큰 롤오버에 유용함).</span><span class="sxs-lookup"><span data-stu-id="858ee-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="858ee-399">키 요소에는 `kid` 클레임에 대한 일치에 사용된 `id` 특성(선택적)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="858ee-400">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-400">No</span></span>|  
|<span data-ttu-id="858ee-401">issuers</span><span class="sxs-lookup"><span data-stu-id="858ee-401">issuers</span></span>|<span data-ttu-id="858ee-402">토큰을 발행한 허용 가능한 보안 주체의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="858ee-403">여러 발급자 값이 있는 경우 각 값은 모든 값이 소진(이 경우 유효성 검사 실패)되거나 한 값이 성공할 때까지 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="858ee-404">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-404">No</span></span>|  
|<span data-ttu-id="858ee-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="858ee-405">openid-config</span></span>|<span data-ttu-id="858ee-406">서명 키 및 발급자를 획득할 수 있는 준수 Open ID 구성 끝점을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="858ee-407">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-407">No</span></span>|  
|<span data-ttu-id="858ee-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="858ee-408">required-claims</span></span>|<span data-ttu-id="858ee-409">유효성을 고려할 토큰에 있을 것으로 예상되는 클레임 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="858ee-410">`match` 특성이 `all`로 설정되면 유효성 검사 성공을 위해 정책에 있는 모든 클레임 값이 토큰에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="858ee-411">`match` 특성이 `any`로 설정되면 유효성 검사 성공을 위해 정책에 있는 모든 클레임 값이 토큰에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="858ee-412">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-412">No</span></span>|  
|<span data-ttu-id="858ee-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="858ee-413">zumo-master-key</span></span>|<span data-ttu-id="858ee-414">Azure Mobile Services에서 발급한 토큰에 대한 마스터 키</span><span class="sxs-lookup"><span data-stu-id="858ee-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="858ee-415">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="858ee-416">특성</span><span class="sxs-lookup"><span data-stu-id="858ee-416">Attributes</span></span>  
  
|<span data-ttu-id="858ee-417">이름</span><span class="sxs-lookup"><span data-stu-id="858ee-417">Name</span></span>|<span data-ttu-id="858ee-418">설명</span><span class="sxs-lookup"><span data-stu-id="858ee-418">Description</span></span>|<span data-ttu-id="858ee-419">필수</span><span class="sxs-lookup"><span data-stu-id="858ee-419">Required</span></span>|<span data-ttu-id="858ee-420">기본값</span><span class="sxs-lookup"><span data-stu-id="858ee-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="858ee-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="858ee-421">clock-skew</span></span>|<span data-ttu-id="858ee-422">Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-422">Timespan.</span></span> <span data-ttu-id="858ee-423">토큰의 만료 클레임이 토큰에 없고 현재 날짜/시간을 지난 경우 약간의 시간 여유를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="858ee-424">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-424">No</span></span>|<span data-ttu-id="858ee-425">0초</span><span class="sxs-lookup"><span data-stu-id="858ee-425">0 seconds</span></span>|  
|<span data-ttu-id="858ee-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="858ee-426">failed-validation-error-message</span></span>|<span data-ttu-id="858ee-427">JWT가 유효성 검사를 통과하지 못한 경우 HTTP 응답 본문에 반환할 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="858ee-428">이 메시지는 적절히 이스케이프된 특수 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="858ee-429">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-429">No</span></span>|<span data-ttu-id="858ee-430">기본 오류 메시지는 유효성 검사 문제에 따라 달라집니다(예: "JWT not present(JWT 없음)").</span><span class="sxs-lookup"><span data-stu-id="858ee-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="858ee-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="858ee-431">failed-validation-httpcode</span></span>|<span data-ttu-id="858ee-432">JWT가 유효성 검사를 통과하지 못한 경우 반환할 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="858ee-433">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-433">No</span></span>|<span data-ttu-id="858ee-434">401</span><span class="sxs-lookup"><span data-stu-id="858ee-434">401</span></span>|  
|<span data-ttu-id="858ee-435">header-name</span><span class="sxs-lookup"><span data-stu-id="858ee-435">header-name</span></span>|<span data-ttu-id="858ee-436">토큰을 보유하는 HTTP 헤더의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="858ee-437">`header-name` 또는 `query-paremeter-name`를 지정해야 하며 둘 다 함께 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="858ee-438">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-438">N/A</span></span>|  
|<span data-ttu-id="858ee-439">id</span><span class="sxs-lookup"><span data-stu-id="858ee-439">id</span></span>|<span data-ttu-id="858ee-440">`key` 요소에 있는 `id` 특성을 통해 토큰(있는 경우)에 있는 `kid` 클레임과 일치시킬 문자열을 지정하여 서명 유효성 검사에 사용할 적절한 키를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="858ee-441">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-441">No</span></span>|<span data-ttu-id="858ee-442">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-442">N/A</span></span>|  
|<span data-ttu-id="858ee-443">match</span><span class="sxs-lookup"><span data-stu-id="858ee-443">match</span></span>|<span data-ttu-id="858ee-444">`claim` 요소에 있는 `match` 특성에 따라 유효성 검사 성공을 위해 정책에 있는 모든 클레임 값이 토큰에 표시되어야 하는지가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="858ee-445">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="858ee-446">-                          `all` - 유효성 검사 성공을 위해 정책에 있는 모든 클레임 값이 토큰에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="858ee-447">-                          `any` - 유효성 검사 성공을 위해 하나 이상의 클레임 값이 토큰에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="858ee-448">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-448">No</span></span>|<span data-ttu-id="858ee-449">모두</span><span class="sxs-lookup"><span data-stu-id="858ee-449">all</span></span>|  
|<span data-ttu-id="858ee-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="858ee-450">query-paremeter-name</span></span>|<span data-ttu-id="858ee-451">토큰을 보유하는 쿼리 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="858ee-452">`header-name` 또는 `query-paremeter-name`를 지정해야 하며 둘 다 함께 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="858ee-453">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-453">N/A</span></span>|  
|<span data-ttu-id="858ee-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="858ee-454">require-expiration-time</span></span>|<span data-ttu-id="858ee-455">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-455">Boolean.</span></span> <span data-ttu-id="858ee-456">토큰에 만료 클레임이 필요한지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="858ee-457">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-457">No</span></span>|<span data-ttu-id="858ee-458">true</span><span class="sxs-lookup"><span data-stu-id="858ee-458">true</span></span>|
|<span data-ttu-id="858ee-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="858ee-459">require-scheme</span></span>|<span data-ttu-id="858ee-460">토큰 스키마의 이름입니다(예: "Bearer").</span><span class="sxs-lookup"><span data-stu-id="858ee-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="858ee-461">이 특성이 설치되면 정책은 지정된 스키마가 권한 부여 헤더 값에 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="858ee-462">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-462">No</span></span>|<span data-ttu-id="858ee-463">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-463">N/A</span></span>|
|<span data-ttu-id="858ee-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="858ee-464">require-signed-tokens</span></span>|<span data-ttu-id="858ee-465">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-465">Boolean.</span></span> <span data-ttu-id="858ee-466">토큰에 서명이 필요한지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="858ee-467">아니요</span><span class="sxs-lookup"><span data-stu-id="858ee-467">No</span></span>|<span data-ttu-id="858ee-468">true</span><span class="sxs-lookup"><span data-stu-id="858ee-468">true</span></span>|  
|<span data-ttu-id="858ee-469">url</span><span class="sxs-lookup"><span data-stu-id="858ee-469">url</span></span>|<span data-ttu-id="858ee-470">Open ID 구성 메타데이터를 가져올 수 있는 Open ID 구성 끝점 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="858ee-471">Azure Active Directory의 경우 다음 URL을 사용합니다. `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` 여기서 사용자의 디렉터리 테넌트 이름을 대체합니다(예: `contoso.onmicrosoft.com`).</span><span class="sxs-lookup"><span data-stu-id="858ee-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="858ee-472">예</span><span class="sxs-lookup"><span data-stu-id="858ee-472">Yes</span></span>|<span data-ttu-id="858ee-473">해당 없음</span><span class="sxs-lookup"><span data-stu-id="858ee-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="858ee-474">사용 현황</span><span class="sxs-lookup"><span data-stu-id="858ee-474">Usage</span></span>  
 <span data-ttu-id="858ee-475">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="858ee-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="858ee-476">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="858ee-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="858ee-477">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="858ee-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="858ee-478">다음 단계</span><span class="sxs-lookup"><span data-stu-id="858ee-478">Next steps</span></span>
<span data-ttu-id="858ee-479">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="858ee-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
