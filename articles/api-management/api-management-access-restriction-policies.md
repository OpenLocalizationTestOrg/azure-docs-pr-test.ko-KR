---
title: "aaaAzure API 관리 액세스 제한 정책 | Microsoft Docs"
description: "Azure API 관리에 사용할 수 있는 hello 액세스 제한 정책에 알아봅니다."
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
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="896a7-103">API Management 액세스 제한 정책</span><span class="sxs-lookup"><span data-stu-id="896a7-103">API Management access restriction policies</span></span>
<span data-ttu-id="896a7-104">이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="896a7-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="896a7-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="896a7-106"><a name="AccessRestrictionPolicies"></a> 액세스 제한 정책</span><span class="sxs-lookup"><span data-stu-id="896a7-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="896a7-107">[HTTP 헤더 확인](api-management-access-restriction-policies.md#CheckHTTPHeader) - HTTP 헤더의 존재 및/또는 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="896a7-108">[구독으로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRate) - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="896a7-109">[키로 호출 속도 제한](#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="896a7-110">[호출자 IP 제한](api-management-access-restriction-policies.md#RestrictCallerIPs) - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="896a7-111">[구독에 의해 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuota) -구독 별로에서 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="896a7-112">[키로 할당량 설정](#SetUsageQuotaByKey) -당 키 단위로 허용 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="896a7-113">[JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="896a7-114"><a name="CheckHTTPHeader"></a> HTTP 헤더 확인</span><span class="sxs-lookup"><span data-stu-id="896a7-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="896a7-115">사용 하 여 hello `check-header` 정책 tooenforce 요청이 지정한 HTTP 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="896a7-116">필요에 따라 hello 헤더에 특정 값 또는 허용 된 값의 범위에 대 한 확인 toosee를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="896a7-117">Hello 확인이 실패 하면 hello 정책 요청 처리를 종료 하 고 hello HTTP 상태 코드 및 오류 메시지 hello 정책에 지정 된을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-118">정책 문</span><span class="sxs-lookup"><span data-stu-id="896a7-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="896a7-119">예</span><span class="sxs-lookup"><span data-stu-id="896a7-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="896a7-120">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-120">Elements</span></span>  
  
|<span data-ttu-id="896a7-121">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-121">Name</span></span>|<span data-ttu-id="896a7-122">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-122">Description</span></span>|<span data-ttu-id="896a7-123">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="896a7-124">check-header</span><span class="sxs-lookup"><span data-stu-id="896a7-124">check-header</span></span>|<span data-ttu-id="896a7-125">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-125">Root element.</span></span>|<span data-ttu-id="896a7-126">예</span><span class="sxs-lookup"><span data-stu-id="896a7-126">Yes</span></span>|  
|<span data-ttu-id="896a7-127">값</span><span class="sxs-lookup"><span data-stu-id="896a7-127">value</span></span>|<span data-ttu-id="896a7-128">허용된 HTTP 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-128">Allowed HTTP header value.</span></span> <span data-ttu-id="896a7-129">여러 값 요소가 지정 된 hello 값 중 하나는 일치 하는 경우 hello 검사는 성공을 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="896a7-130">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-131">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-131">Attributes</span></span>  
  
|<span data-ttu-id="896a7-132">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-132">Name</span></span>|<span data-ttu-id="896a7-133">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-133">Description</span></span>|<span data-ttu-id="896a7-134">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-134">Required</span></span>|<span data-ttu-id="896a7-135">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="896a7-136">failed-check-error-message</span></span>|<span data-ttu-id="896a7-137">Hello 헤더 존재 하지 않거나 잘못 된 값이 hello HTTP 응답 본문에 오류 메시지 tooreturn 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="896a7-138">이 메시지는 적절히 이스케이프된 특수 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="896a7-139">예</span><span class="sxs-lookup"><span data-stu-id="896a7-139">Yes</span></span>|<span data-ttu-id="896a7-140">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-140">N/A</span></span>|  
|<span data-ttu-id="896a7-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="896a7-141">failed-check-httpcode</span></span>|<span data-ttu-id="896a7-142">HTTP 상태 코드 tooreturn hello 헤더 존재 하지 않거나 잘못 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="896a7-143">예</span><span class="sxs-lookup"><span data-stu-id="896a7-143">Yes</span></span>|<span data-ttu-id="896a7-144">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-144">N/A</span></span>|  
|<span data-ttu-id="896a7-145">header-name</span><span class="sxs-lookup"><span data-stu-id="896a7-145">header-name</span></span>|<span data-ttu-id="896a7-146">HTTP 헤더 toocheck hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="896a7-147">예</span><span class="sxs-lookup"><span data-stu-id="896a7-147">Yes</span></span>|<span data-ttu-id="896a7-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-148">N/A</span></span>|  
|<span data-ttu-id="896a7-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="896a7-149">ignore-case</span></span>|<span data-ttu-id="896a7-150">TooTrue 또는 false로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="896a7-151">이면 set tooTrue 케이스 hello 집합이 허용 되는 값에 대해 hello 헤더 값을 비교 하는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="896a7-152">예</span><span class="sxs-lookup"><span data-stu-id="896a7-152">Yes</span></span>|<span data-ttu-id="896a7-153">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-154">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-154">Usage</span></span>  
 <span data-ttu-id="896a7-155">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-156">**정책 섹션:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="896a7-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="896a7-157">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="896a7-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="896a7-158"><a name="LimitCallRate"></a> 구독으로 호출 속도 제한</span><span class="sxs-lookup"><span data-stu-id="896a7-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="896a7-159">hello `rate-limit` 정책으로 인해 API 사용 급증을 hello를 제한 하 여 구독 별로 지정 된 시간 동안 당 번호 지정 된 속도 tooa 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="896a7-160">이 정책은 트리거될 때 hello 호출자가 받을 `429 Too Many Requests` 응답 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="896a7-161">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="896a7-162">[정책 식](api-management-policy-expressions.md) 이 정책에 대 한 hello 정책 특성에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-163">정책 문</span><span class="sxs-lookup"><span data-stu-id="896a7-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="896a7-164">예</span><span class="sxs-lookup"><span data-stu-id="896a7-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="896a7-165">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-165">Elements</span></span>  
  
|<span data-ttu-id="896a7-166">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-166">Name</span></span>|<span data-ttu-id="896a7-167">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-167">Description</span></span>|<span data-ttu-id="896a7-168">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="896a7-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="896a7-169">set-limit</span></span>|<span data-ttu-id="896a7-170">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-170">Root element.</span></span>|<span data-ttu-id="896a7-171">예</span><span class="sxs-lookup"><span data-stu-id="896a7-171">Yes</span></span>|  
|<span data-ttu-id="896a7-172">api</span><span class="sxs-lookup"><span data-stu-id="896a7-172">api</span></span>|<span data-ttu-id="896a7-173">이러한 요소 tooimpose 호출 속도 제한 중 하나 이상을 hello 제품 내에서 Api에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="896a7-174">제품 및 API 호출 속도 제한은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="896a7-175">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-175">No</span></span>|  
|<span data-ttu-id="896a7-176">operation</span><span class="sxs-lookup"><span data-stu-id="896a7-176">operation</span></span>|<span data-ttu-id="896a7-177">API 내의 작업에 하나 이상의 이러한 요소 tooimpose 호출 속도 제한 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="896a7-178">제품, API 및 작업 호출 속도 제한은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="896a7-179">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-180">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-180">Attributes</span></span>  
  
|<span data-ttu-id="896a7-181">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-181">Name</span></span>|<span data-ttu-id="896a7-182">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-182">Description</span></span>|<span data-ttu-id="896a7-183">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-183">Required</span></span>|<span data-ttu-id="896a7-184">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-185">name</span><span class="sxs-lookup"><span data-stu-id="896a7-185">name</span></span>|<span data-ttu-id="896a7-186">어떤 tooapply hello 속도 제한에 대 한 hello 이름 hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="896a7-187">예</span><span class="sxs-lookup"><span data-stu-id="896a7-187">Yes</span></span>|<span data-ttu-id="896a7-188">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-188">N/A</span></span>|  
|<span data-ttu-id="896a7-189">calls</span><span class="sxs-lookup"><span data-stu-id="896a7-189">calls</span></span>|<span data-ttu-id="896a7-190">hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="896a7-191">예</span><span class="sxs-lookup"><span data-stu-id="896a7-191">Yes</span></span>|<span data-ttu-id="896a7-192">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-192">N/A</span></span>|  
|<span data-ttu-id="896a7-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="896a7-193">renewal-period</span></span>|<span data-ttu-id="896a7-194">hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="896a7-195">예</span><span class="sxs-lookup"><span data-stu-id="896a7-195">Yes</span></span>|<span data-ttu-id="896a7-196">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-197">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-197">Usage</span></span>  
 <span data-ttu-id="896a7-198">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-199">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="896a7-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="896a7-200">**정책 범위:** product</span><span class="sxs-lookup"><span data-stu-id="896a7-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="896a7-201"><a name="LimitCallRateByKey"></a> 키로 호출 속도 제한</span><span class="sxs-lookup"><span data-stu-id="896a7-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="896a7-202">hello `rate-limit-by-key` 정책에는 API를 사용 하지 못하도록 스파이크 hello를 제한 하 여 키 당 기준 당 지정 된 시간 동안 숫자 속도 tooa 지정 된 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="896a7-203">hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="896a7-204">선택적 증분 조건 toospecify hello 제한에 대해 계산 되도록 요청을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="896a7-205">이 정책은 트리거될 때 hello 호출자가 받을 `429 Too Many Requests` 응답 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="896a7-206">이 정책에 대한 자세한 내용과 예제는 [Azure API Management로 고급 요청 제한](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="896a7-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="896a7-207">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-208">정책 문:</span><span class="sxs-lookup"><span data-stu-id="896a7-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="896a7-209">예제</span><span class="sxs-lookup"><span data-stu-id="896a7-209">Example</span></span>  
 <span data-ttu-id="896a7-210">다음 예제는 hello, hello 속도 한도 hello 호출자 IP 주소를 통해 키가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="896a7-211">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-211">Elements</span></span>  
  
|<span data-ttu-id="896a7-212">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-212">Name</span></span>|<span data-ttu-id="896a7-213">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-213">Description</span></span>|<span data-ttu-id="896a7-214">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="896a7-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="896a7-215">set-limit</span></span>|<span data-ttu-id="896a7-216">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-216">Root element.</span></span>|<span data-ttu-id="896a7-217">예</span><span class="sxs-lookup"><span data-stu-id="896a7-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-218">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-218">Attributes</span></span>  
  
|<span data-ttu-id="896a7-219">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-219">Name</span></span>|<span data-ttu-id="896a7-220">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-220">Description</span></span>|<span data-ttu-id="896a7-221">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-221">Required</span></span>|<span data-ttu-id="896a7-222">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-223">calls</span><span class="sxs-lookup"><span data-stu-id="896a7-223">calls</span></span>|<span data-ttu-id="896a7-224">hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="896a7-225">예</span><span class="sxs-lookup"><span data-stu-id="896a7-225">Yes</span></span>|<span data-ttu-id="896a7-226">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-226">N/A</span></span>|  
|<span data-ttu-id="896a7-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="896a7-227">counter-key</span></span>|<span data-ttu-id="896a7-228">hello hello 속도 제한 정책에 대 한 키 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="896a7-229">예</span><span class="sxs-lookup"><span data-stu-id="896a7-229">Yes</span></span>|<span data-ttu-id="896a7-230">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-230">N/A</span></span>|  
|<span data-ttu-id="896a7-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="896a7-231">increment-condition</span></span>|<span data-ttu-id="896a7-232">hello hello 요청 hello 할당량으로 간주 해야 하는 경우를 지정 하는 부울 식 (`true`).</span><span class="sxs-lookup"><span data-stu-id="896a7-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="896a7-233">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-233">No</span></span>|<span data-ttu-id="896a7-234">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-234">N/A</span></span>|  
|<span data-ttu-id="896a7-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="896a7-235">renewal-period</span></span>|<span data-ttu-id="896a7-236">hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="896a7-237">예</span><span class="sxs-lookup"><span data-stu-id="896a7-237">Yes</span></span>|<span data-ttu-id="896a7-238">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-239">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-239">Usage</span></span>  
 <span data-ttu-id="896a7-240">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-241">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="896a7-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="896a7-242">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="896a7-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="896a7-243"><a name="RestrictCallerIPs"></a> 호출자 IP 제한</span><span class="sxs-lookup"><span data-stu-id="896a7-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="896a7-244">hello `ip-filter` 정책에서 특정 IP 주소 및/또는 주소 범위의 호출 (허용/거부)를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-245">정책 문</span><span class="sxs-lookup"><span data-stu-id="896a7-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="896a7-246">예</span><span class="sxs-lookup"><span data-stu-id="896a7-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="896a7-247">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-247">Elements</span></span>  
  
|<span data-ttu-id="896a7-248">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-248">Name</span></span>|<span data-ttu-id="896a7-249">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-249">Description</span></span>|<span data-ttu-id="896a7-250">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="896a7-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="896a7-251">ip-filter</span></span>|<span data-ttu-id="896a7-252">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-252">Root element.</span></span>|<span data-ttu-id="896a7-253">예</span><span class="sxs-lookup"><span data-stu-id="896a7-253">Yes</span></span>|  
|<span data-ttu-id="896a7-254">address</span><span class="sxs-lookup"><span data-stu-id="896a7-254">address</span></span>|<span data-ttu-id="896a7-255">어떤 toofilter에 단일 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="896a7-256">하나 이상의 `address` 또는 `address-range` 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="896a7-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="896a7-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="896a7-258">어떤 toofilter에 범위의 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="896a7-259">하나 이상의 `address` 또는 `address-range` 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-260">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-260">Attributes</span></span>  
  
|<span data-ttu-id="896a7-261">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-261">Name</span></span>|<span data-ttu-id="896a7-262">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-262">Description</span></span>|<span data-ttu-id="896a7-263">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-263">Required</span></span>|<span data-ttu-id="896a7-264">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="896a7-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="896a7-266">IP 범위 tooallow 해결 하거나에 대 한 액세스를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="896a7-267">필요한 경우 hello `address-range` 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="896a7-268">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-268">N/A</span></span>|  
|<span data-ttu-id="896a7-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="896a7-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="896a7-270">호출을 허용할지 하지 hello에 대 한 IP 주소와 범위를 지정 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="896a7-271">예</span><span class="sxs-lookup"><span data-stu-id="896a7-271">Yes</span></span>|<span data-ttu-id="896a7-272">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-273">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-273">Usage</span></span>  
 <span data-ttu-id="896a7-274">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-275">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="896a7-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="896a7-276">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="896a7-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="896a7-277"><a name="SetUsageQuota"></a> 구독으로 사용 할당량 설정</span><span class="sxs-lookup"><span data-stu-id="896a7-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="896a7-278">hello `quota` 정책 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량 구독 별로에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="896a7-279">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="896a7-280">[정책 식](api-management-policy-expressions.md) 이 정책에 대 한 hello 정책 특성에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-281">정책 문</span><span class="sxs-lookup"><span data-stu-id="896a7-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="896a7-282">예</span><span class="sxs-lookup"><span data-stu-id="896a7-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="896a7-283">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-283">Elements</span></span>  
  
|<span data-ttu-id="896a7-284">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-284">Name</span></span>|<span data-ttu-id="896a7-285">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-285">Description</span></span>|<span data-ttu-id="896a7-286">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="896a7-287">quota</span><span class="sxs-lookup"><span data-stu-id="896a7-287">quota</span></span>|<span data-ttu-id="896a7-288">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-288">Root element.</span></span>|<span data-ttu-id="896a7-289">예</span><span class="sxs-lookup"><span data-stu-id="896a7-289">Yes</span></span>|  
|<span data-ttu-id="896a7-290">api</span><span class="sxs-lookup"><span data-stu-id="896a7-290">api</span></span>|<span data-ttu-id="896a7-291">이러한 요소 tooimpose 할당량 중 하나 이상을 hello 제품 내에서 Api에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="896a7-292">제품 및 API 할당량은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="896a7-293">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-293">No</span></span>|  
|<span data-ttu-id="896a7-294">operation</span><span class="sxs-lookup"><span data-stu-id="896a7-294">operation</span></span>|<span data-ttu-id="896a7-295">API 내의 작업에 대해 하나 이상의 이러한 요소 tooimpose 할당량을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="896a7-296">제품, API 및 작업 할당량은 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="896a7-297">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-298">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-298">Attributes</span></span>  
  
|<span data-ttu-id="896a7-299">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-299">Name</span></span>|<span data-ttu-id="896a7-300">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-300">Description</span></span>|<span data-ttu-id="896a7-301">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-301">Required</span></span>|<span data-ttu-id="896a7-302">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-303">name</span><span class="sxs-lookup"><span data-stu-id="896a7-303">name</span></span>|<span data-ttu-id="896a7-304">hello API 또는 할당량에 적용 되는 hello에 대 한 작업의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="896a7-305">예</span><span class="sxs-lookup"><span data-stu-id="896a7-305">Yes</span></span>|<span data-ttu-id="896a7-306">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-306">N/A</span></span>|  
|<span data-ttu-id="896a7-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="896a7-307">bandwidth</span></span>|<span data-ttu-id="896a7-308">hello에 지정 된 hello 시간 간격 동안 허용 되는 (킬로바이트)의 최대 총 수를 hello `renewal-period`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="896a7-309">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="896a7-310">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-310">N/A</span></span>|  
|<span data-ttu-id="896a7-311">calls</span><span class="sxs-lookup"><span data-stu-id="896a7-311">calls</span></span>|<span data-ttu-id="896a7-312">hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="896a7-313">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="896a7-314">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-314">N/A</span></span>|  
|<span data-ttu-id="896a7-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="896a7-315">renewal-period</span></span>|<span data-ttu-id="896a7-316">hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="896a7-317">예</span><span class="sxs-lookup"><span data-stu-id="896a7-317">Yes</span></span>|<span data-ttu-id="896a7-318">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-319">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-319">Usage</span></span>  
 <span data-ttu-id="896a7-320">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-321">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="896a7-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="896a7-322">**정책 범위:** product</span><span class="sxs-lookup"><span data-stu-id="896a7-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="896a7-323"><a name="SetUsageQuotaByKey"></a> 키로 사용 할당량 설정</span><span class="sxs-lookup"><span data-stu-id="896a7-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="896a7-324">hello `quota-by-key` 정책은 되도록 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량 키 당 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="896a7-325">hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="896a7-326">선택적 증분 조건 toospecify hello 할당량으로 계산 되도록 요청을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="896a7-327">이 정책에 대한 자세한 내용과 예제는 [Azure API Management로 고급 요청 제한](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="896a7-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="896a7-328">이 정책은 정책 문서당 한 번만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="896a7-329">[정책 식](api-management-policy-expressions.md) 이 정책에 대 한 hello 정책 특성에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-330">정책 문</span><span class="sxs-lookup"><span data-stu-id="896a7-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="896a7-331">예제</span><span class="sxs-lookup"><span data-stu-id="896a7-331">Example</span></span>  
 <span data-ttu-id="896a7-332">다음 예제는 hello, hello 할당량은 hello 호출자 IP 주소를 통해 키가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="896a7-333">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-333">Elements</span></span>  
  
|<span data-ttu-id="896a7-334">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-334">Name</span></span>|<span data-ttu-id="896a7-335">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-335">Description</span></span>|<span data-ttu-id="896a7-336">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="896a7-337">quota</span><span class="sxs-lookup"><span data-stu-id="896a7-337">quota</span></span>|<span data-ttu-id="896a7-338">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-338">Root element.</span></span>|<span data-ttu-id="896a7-339">예</span><span class="sxs-lookup"><span data-stu-id="896a7-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-340">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-340">Attributes</span></span>  
  
|<span data-ttu-id="896a7-341">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-341">Name</span></span>|<span data-ttu-id="896a7-342">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-342">Description</span></span>|<span data-ttu-id="896a7-343">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-343">Required</span></span>|<span data-ttu-id="896a7-344">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="896a7-345">bandwidth</span></span>|<span data-ttu-id="896a7-346">hello에 지정 된 hello 시간 간격 동안 허용 되는 (킬로바이트)의 최대 총 수를 hello `renewal-period`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="896a7-347">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="896a7-348">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-348">N/A</span></span>|  
|<span data-ttu-id="896a7-349">calls</span><span class="sxs-lookup"><span data-stu-id="896a7-349">calls</span></span>|<span data-ttu-id="896a7-350">hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="896a7-351">`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="896a7-352">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-352">N/A</span></span>|  
|<span data-ttu-id="896a7-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="896a7-353">counter-key</span></span>|<span data-ttu-id="896a7-354">hello hello 할당량 정책에 대 한 키 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="896a7-355">예</span><span class="sxs-lookup"><span data-stu-id="896a7-355">Yes</span></span>|<span data-ttu-id="896a7-356">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-356">N/A</span></span>|  
|<span data-ttu-id="896a7-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="896a7-357">increment-condition</span></span>|<span data-ttu-id="896a7-358">hello hello 요청 hello 할당량으로 간주 해야 하는 경우를 지정 하는 부울 식 (`true`)</span><span class="sxs-lookup"><span data-stu-id="896a7-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="896a7-359">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-359">No</span></span>|<span data-ttu-id="896a7-360">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-360">N/A</span></span>|  
|<span data-ttu-id="896a7-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="896a7-361">renewal-period</span></span>|<span data-ttu-id="896a7-362">hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="896a7-363">예</span><span class="sxs-lookup"><span data-stu-id="896a7-363">Yes</span></span>|<span data-ttu-id="896a7-364">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-365">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-365">Usage</span></span>  
 <span data-ttu-id="896a7-366">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-367">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="896a7-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="896a7-368">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="896a7-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="896a7-369"><a name="ValidateJWT"></a> JWT 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="896a7-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="896a7-370">hello `validate-jwt` 정책 적용 존재 하 고 HTTP 헤더 또는 쿼리 매개 변수는 지정한에서 추출 된 JWT의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="896a7-371">hello `validate-jwt` 정책에 따라 해당 hello `exp` 등록 된 클레임은 hello JWT 토큰에 포함 하지 않는 한 `require-expiration-time` 특성이 지정 되 고도`false`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="896a7-372">hello `validate-jwt` 정책 HS256 및 RS256 서명 알고리즘을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="896a7-373">HS256에 대 한 hello 키 인라인 hello 정책 hello base64 인코딩 형식으로 내 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="896a7-374">RS256에 대 한 hello 키에 toobe Open ID 구성 끝점을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="896a7-375">정책 문</span><span class="sxs-lookup"><span data-stu-id="896a7-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
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
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="896a7-376">예</span><span class="sxs-lookup"><span data-stu-id="896a7-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="896a7-377">Azure Mobile Services 토큰 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="896a7-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="896a7-378">Azure Active Directory 토큰 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="896a7-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="896a7-379">Azure Active Directory B2C 토큰 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="896a7-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="896a7-380">토큰 클레임을 기반으로 하는 액세스 toooperations 권한 부여</span><span class="sxs-lookup"><span data-stu-id="896a7-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="896a7-381">이 예에서는 어떻게 toouse hello [JWT의 유효성을 검사](api-management-access-restriction-policies.md#ValidateJWT) 정책 toopre-토큰 클레임을 기반으로 하는 액세스 toooperations 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="896a7-382">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too13:50 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="896a7-383">Hello 정책 편집기에 구성 된 toosee hello 정책이 too15:00를 빨리 감기 및 too18:50 모두와 사용 하지 않는 hello hello 개발자 포털에서 호출 하는 작업의 데모에 대 한 권한 부여 토큰을 필요로 하는 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="896a7-384">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-384">Elements</span></span>  
  
|<span data-ttu-id="896a7-385">요소</span><span class="sxs-lookup"><span data-stu-id="896a7-385">Element</span></span>|<span data-ttu-id="896a7-386">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-386">Description</span></span>|<span data-ttu-id="896a7-387">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="896a7-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="896a7-388">validate-jwt</span></span>|<span data-ttu-id="896a7-389">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-389">Root element.</span></span>|<span data-ttu-id="896a7-390">예</span><span class="sxs-lookup"><span data-stu-id="896a7-390">Yes</span></span>|  
|<span data-ttu-id="896a7-391">audiences</span><span class="sxs-lookup"><span data-stu-id="896a7-391">audiences</span></span>|<span data-ttu-id="896a7-392">Hello 토큰에 포함 될 수 있는 허용 가능한 대상 그룹 클레임 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="896a7-393">여러 대상 그룹 값이 있는 경우 각 값은 모든 값이 소진(이 경우 유효성 검사 실패)되거나 한 값이 성공할 때까지 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="896a7-394">한 명 이상의 대상 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-394">At least one audience must be specified.</span></span>|<span data-ttu-id="896a7-395">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-395">No</span></span>|  
|<span data-ttu-id="896a7-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="896a7-396">issuer-signing-keys</span></span>|<span data-ttu-id="896a7-397">목록이 사용 되는 키 toovalidate Base64 인코딩 보안 토큰을 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="896a7-398">보안 키가 여러 개 있는 경우 각 키는 모든 키가 소진(이 경우 유효성 검사 실패)되거나 한 개 키가 성공할 때까지 시도됩니다(토큰 롤오버에 유용함).</span><span class="sxs-lookup"><span data-stu-id="896a7-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="896a7-399">주요 요소는 선택적 `id` 에 대해 사용 되는 특성 toomatch `kid` 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="896a7-400">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-400">No</span></span>|  
|<span data-ttu-id="896a7-401">issuers</span><span class="sxs-lookup"><span data-stu-id="896a7-401">issuers</span></span>|<span data-ttu-id="896a7-402">목록 hello 토큰을 발급 한 허용 가능한 보안 주체입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="896a7-403">여러 발급자 값이 있는 경우 각 값은 모든 값이 소진(이 경우 유효성 검사 실패)되거나 한 값이 성공할 때까지 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="896a7-404">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-404">No</span></span>|  
|<span data-ttu-id="896a7-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="896a7-405">openid-config</span></span>|<span data-ttu-id="896a7-406">서명 키 및 발급자 생성 수 있는 수는 호환 Open ID 구성 끝점을 지정 하는 데 사용 되는 hello 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="896a7-407">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-407">No</span></span>|  
|<span data-ttu-id="896a7-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="896a7-408">required-claims</span></span>|<span data-ttu-id="896a7-409">목록이 대 한 hello 토큰에 있는 필요로 하는 클레임 toobe toobe 유효한 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="896a7-410">Hello 때 `match` 특성이 너무 설정 된`all` hello 정책에 있는 모든 클레임 값 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="896a7-411">Hello 때 `match` 특성이 너무 설정 된`any` 클레임이 하나 이상 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="896a7-412">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-412">No</span></span>|  
|<span data-ttu-id="896a7-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="896a7-413">zumo-master-key</span></span>|<span data-ttu-id="896a7-414">Azure Mobile Services에서 발급한 토큰에 대한 마스터 키</span><span class="sxs-lookup"><span data-stu-id="896a7-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="896a7-415">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="896a7-416">특성</span><span class="sxs-lookup"><span data-stu-id="896a7-416">Attributes</span></span>  
  
|<span data-ttu-id="896a7-417">이름</span><span class="sxs-lookup"><span data-stu-id="896a7-417">Name</span></span>|<span data-ttu-id="896a7-418">설명</span><span class="sxs-lookup"><span data-stu-id="896a7-418">Description</span></span>|<span data-ttu-id="896a7-419">필수</span><span class="sxs-lookup"><span data-stu-id="896a7-419">Required</span></span>|<span data-ttu-id="896a7-420">기본값</span><span class="sxs-lookup"><span data-stu-id="896a7-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="896a7-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="896a7-421">clock-skew</span></span>|<span data-ttu-id="896a7-422">Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-422">Timespan.</span></span> <span data-ttu-id="896a7-423">Hello 토큰의 만료 클레임이 hello 토큰에 있는 고 hello 현재를 지난 경우 여유 제공 날짜 / 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="896a7-424">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-424">No</span></span>|<span data-ttu-id="896a7-425">0초</span><span class="sxs-lookup"><span data-stu-id="896a7-425">0 seconds</span></span>|  
|<span data-ttu-id="896a7-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="896a7-426">failed-validation-error-message</span></span>|<span data-ttu-id="896a7-427">Hello JWT 유효성 검사를 통과 하지 못하면 hello HTTP 응답 본문에 오류 메시지 tooreturn 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="896a7-428">이 메시지는 적절히 이스케이프된 특수 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="896a7-429">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-429">No</span></span>|<span data-ttu-id="896a7-430">기본 오류 메시지는 유효성 검사 문제에 따라 달라집니다(예: "JWT not present(JWT 없음)").</span><span class="sxs-lookup"><span data-stu-id="896a7-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="896a7-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="896a7-431">failed-validation-httpcode</span></span>|<span data-ttu-id="896a7-432">HTTP 상태 코드 tooreturn hello JWT 유효성 검사를 통과 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="896a7-433">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-433">No</span></span>|<span data-ttu-id="896a7-434">401</span><span class="sxs-lookup"><span data-stu-id="896a7-434">401</span></span>|  
|<span data-ttu-id="896a7-435">header-name</span><span class="sxs-lookup"><span data-stu-id="896a7-435">header-name</span></span>|<span data-ttu-id="896a7-436">hello 토큰을 보유 하는 hello HTTP 헤더의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="896a7-437">`header-name` 또는 `query-paremeter-name`를 지정해야 하며 둘 다 함께 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="896a7-438">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-438">N/A</span></span>|  
|<span data-ttu-id="896a7-439">id</span><span class="sxs-lookup"><span data-stu-id="896a7-439">id</span></span>|<span data-ttu-id="896a7-440">hello `id` hello에 대 한 특성 `key` 요소에 대해 일치 시킬 toospecify hello 문자열을 사용 하면 `kid` 서명 유효성 검사에 대 한 적절 한 키 toouse hello 아웃 토큰 (있는 경우) toofind hello에에서 대 한 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="896a7-441">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-441">No</span></span>|<span data-ttu-id="896a7-442">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-442">N/A</span></span>|  
|<span data-ttu-id="896a7-443">match</span><span class="sxs-lookup"><span data-stu-id="896a7-443">match</span></span>|<span data-ttu-id="896a7-444">hello `match` hello에 대 한 특성 `claim` 요소 hello 정책에 있는 모든 클레임 값에 대 한 유효성 검사 toosucceed hello 토큰에 존재 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="896a7-445">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="896a7-446">-                          `all`-hello 정책에 있는 모든 클레임 값 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="896a7-447">-                          `any`-하나 이상의 클레임 값 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="896a7-448">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-448">No</span></span>|<span data-ttu-id="896a7-449">모두</span><span class="sxs-lookup"><span data-stu-id="896a7-449">all</span></span>|  
|<span data-ttu-id="896a7-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="896a7-450">query-paremeter-name</span></span>|<span data-ttu-id="896a7-451">hello 이름 hello hello 쿼리 매개 변수를 보유 hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="896a7-452">`header-name` 또는 `query-paremeter-name`를 지정해야 하며 둘 다 함께 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="896a7-453">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-453">N/A</span></span>|  
|<span data-ttu-id="896a7-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="896a7-454">require-expiration-time</span></span>|<span data-ttu-id="896a7-455">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-455">Boolean.</span></span> <span data-ttu-id="896a7-456">Hello 토큰에 만료 클레임이 필요한 지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="896a7-457">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-457">No</span></span>|<span data-ttu-id="896a7-458">true</span><span class="sxs-lookup"><span data-stu-id="896a7-458">true</span></span>|
|<span data-ttu-id="896a7-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="896a7-459">require-scheme</span></span>|<span data-ttu-id="896a7-460">hello 토큰 구성표의 이름 예: hello "Bearer").</span><span class="sxs-lookup"><span data-stu-id="896a7-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="896a7-461">이 특성이 설정 되 면 hello 정책은 스키마가 있는 hello 권한 부여 헤더 값에에서 지정를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="896a7-462">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-462">No</span></span>|<span data-ttu-id="896a7-463">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-463">N/A</span></span>|
|<span data-ttu-id="896a7-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="896a7-464">require-signed-tokens</span></span>|<span data-ttu-id="896a7-465">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-465">Boolean.</span></span> <span data-ttu-id="896a7-466">토큰 서명 필요 toobe 인지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="896a7-467">아니요</span><span class="sxs-lookup"><span data-stu-id="896a7-467">No</span></span>|<span data-ttu-id="896a7-468">true</span><span class="sxs-lookup"><span data-stu-id="896a7-468">true</span></span>|  
|<span data-ttu-id="896a7-469">url</span><span class="sxs-lookup"><span data-stu-id="896a7-469">url</span></span>|<span data-ttu-id="896a7-470">Open ID 구성 메타데이터를 가져올 수 있는 Open ID 구성 끝점 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="896a7-471">Azure Active Directory에 대 한 url hello를 사용 하 여: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` 예: 사용자 디렉터리 테 넌 트 이름으로 대체 `contoso.onmicrosoft.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="896a7-472">예</span><span class="sxs-lookup"><span data-stu-id="896a7-472">Yes</span></span>|<span data-ttu-id="896a7-473">해당 없음</span><span class="sxs-lookup"><span data-stu-id="896a7-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="896a7-474">사용</span><span class="sxs-lookup"><span data-stu-id="896a7-474">Usage</span></span>  
 <span data-ttu-id="896a7-475">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="896a7-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="896a7-476">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="896a7-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="896a7-477">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="896a7-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="896a7-478">다음 단계</span><span class="sxs-lookup"><span data-stu-id="896a7-478">Next steps</span></span>
<span data-ttu-id="896a7-479">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="896a7-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
