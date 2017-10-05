---
title: "Azure API Management 도메인 간 정책 | Microsoft Docs"
description: "Azure API Management에 사용할 수 있는 도메인 간 정책에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="b7050-103">도메인 정책 간 API 관리</span><span class="sxs-lookup"><span data-stu-id="b7050-103">API Management cross domain policies</span></span>
<span data-ttu-id="b7050-104">이 항목에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="b7050-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7050-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="b7050-106"><a name="CrossDomainPolicies"></a> 도메인 간 정책</span><span class="sxs-lookup"><span data-stu-id="b7050-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="b7050-107">[도메인 간 호출 허용](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - API를 Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="b7050-108">[CORS](api-management-cross-domain-policies.md#CORS) - CORS(Cross-Origin Resource Sharing) 지원을 작업 또는 API에 추가하여 브라우저 기반 클라이언트의 도메인 간 호출을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="b7050-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - 패딩이 있는 JSON(JSONP) 지원을 작업 또는 API에 추가하여 JavaScript 브라우저 기반 클라이언트의 도메인 간 호출을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="b7050-110"><a name="AllowCrossDomainCalls"></a> 도메인 간 호출 허용</span><span class="sxs-lookup"><span data-stu-id="b7050-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="b7050-111">`cross-domain` 정책을 사용하여 API를 Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 액세스할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b7050-112">정책 문:</span><span class="sxs-lookup"><span data-stu-id="b7050-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="b7050-113">예</span><span class="sxs-lookup"><span data-stu-id="b7050-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="b7050-114">요소</span><span class="sxs-lookup"><span data-stu-id="b7050-114">Elements</span></span>  
  
|<span data-ttu-id="b7050-115">이름</span><span class="sxs-lookup"><span data-stu-id="b7050-115">Name</span></span>|<span data-ttu-id="b7050-116">설명</span><span class="sxs-lookup"><span data-stu-id="b7050-116">Description</span></span>|<span data-ttu-id="b7050-117">필수</span><span class="sxs-lookup"><span data-stu-id="b7050-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b7050-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="b7050-118">cross-domain</span></span>|<span data-ttu-id="b7050-119">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-119">Root element.</span></span> <span data-ttu-id="b7050-120">자식 요소는 [Adobe 도메인 간 정책 파일 사양](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="b7050-121">예</span><span class="sxs-lookup"><span data-stu-id="b7050-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b7050-122">사용 현황</span><span class="sxs-lookup"><span data-stu-id="b7050-122">Usage</span></span>  
 <span data-ttu-id="b7050-123">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b7050-124">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="b7050-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b7050-125">**정책 범위:** global</span><span class="sxs-lookup"><span data-stu-id="b7050-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="b7050-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="b7050-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="b7050-127">`cors` 정책은 CORS(Cross-Origin Resource Sharing) 지원을 작업 또는 API에 추가하여 브라우저 기반 클라이언트의 도메인 간 호출을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="b7050-128">CORS를 통해 브라우저와 서버가 상호 작용하여 특정 원본 간 요청(즉, 웹 페이지의 JavaScript에서 다른 도메인으로 실행한 XMLHttpRequests 호출)을 허용할지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="b7050-129">따라서 동일 원본의 요청만 허용하는 것보다 유연성이 더 뛰어나며 모든 원본 간 요청을 허용하는 것보다 보안도 더 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b7050-130">정책 문:</span><span class="sxs-lookup"><span data-stu-id="b7050-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="b7050-131">예</span><span class="sxs-lookup"><span data-stu-id="b7050-131">Example</span></span>  
 <span data-ttu-id="b7050-132">이 예제에서는 GET 및 POST 이외의 메서드 또는 사용자 지정 헤더를 비롯하여 사전 요청을 지원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="b7050-133">사용자 지정 헤더 및 추가 HTTP 동사를 지원하려면 다음 예제와 같이 `allowed-methods` 및 `allowed-headers` 섹션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b7050-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="b7050-134">요소</span><span class="sxs-lookup"><span data-stu-id="b7050-134">Elements</span></span>  
  
|<span data-ttu-id="b7050-135">이름</span><span class="sxs-lookup"><span data-stu-id="b7050-135">Name</span></span>|<span data-ttu-id="b7050-136">설명</span><span class="sxs-lookup"><span data-stu-id="b7050-136">Description</span></span>|<span data-ttu-id="b7050-137">필수</span><span class="sxs-lookup"><span data-stu-id="b7050-137">Required</span></span>|<span data-ttu-id="b7050-138">기본값</span><span class="sxs-lookup"><span data-stu-id="b7050-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b7050-139">cors</span><span class="sxs-lookup"><span data-stu-id="b7050-139">cors</span></span>|<span data-ttu-id="b7050-140">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-140">Root element.</span></span>|<span data-ttu-id="b7050-141">예</span><span class="sxs-lookup"><span data-stu-id="b7050-141">Yes</span></span>|<span data-ttu-id="b7050-142">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-142">N/A</span></span>|  
|<span data-ttu-id="b7050-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="b7050-143">allowed-origins</span></span>|<span data-ttu-id="b7050-144">도메인 간 요청에 대해 허용되는 원본을 설명하는 `origin` 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="b7050-145">`allowed-origins`는 모든 원본을 허용하도록 `*`를 지정하는 단일 `origin` 요소 또는 URI를 포함하는 하나 이상의 `origin` 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="b7050-146">예</span><span class="sxs-lookup"><span data-stu-id="b7050-146">Yes</span></span>|<span data-ttu-id="b7050-147">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-147">N/A</span></span>|  
|<span data-ttu-id="b7050-148">원본</span><span class="sxs-lookup"><span data-stu-id="b7050-148">origin</span></span>|<span data-ttu-id="b7050-149">값은 모든 원본을 허용하는 `*`이거나 단일 원본을 지정하는 URI일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="b7050-150">URI에는 체계, 호스트 및 포트가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="b7050-151">예</span><span class="sxs-lookup"><span data-stu-id="b7050-151">Yes</span></span>|<span data-ttu-id="b7050-152">URI에서 포트를 생략하면 HTTP에 포트 80이 사용되고 HTTPS에 포트 443이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="b7050-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="b7050-153">allowed-methods</span></span>|<span data-ttu-id="b7050-154">GET 또는 POST 이외의 메서드가 허용되는 경우 이 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="b7050-155">지원되는 HTTP 동사를 지정하는 `method`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="b7050-156">아니요</span><span class="sxs-lookup"><span data-stu-id="b7050-156">No</span></span>|<span data-ttu-id="b7050-157">이 섹션이 없으면 GET 및 POST가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="b7050-158">메서드</span><span class="sxs-lookup"><span data-stu-id="b7050-158">method</span></span>|<span data-ttu-id="b7050-159">HTTP 동사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="b7050-160">`allowed-methods` 섹션이 있는 경우 하나 이상의 `method` 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="b7050-161">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-161">N/A</span></span>|  
|<span data-ttu-id="b7050-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="b7050-162">allowed-headers</span></span>|<span data-ttu-id="b7050-163">이 요소는 요청에 포함할 수 있는 헤더 이름을 지정하는 `header` 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="b7050-164">아니요</span><span class="sxs-lookup"><span data-stu-id="b7050-164">No</span></span>|<span data-ttu-id="b7050-165">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-165">N/A</span></span>|  
|<span data-ttu-id="b7050-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="b7050-166">expose-headers</span></span>|<span data-ttu-id="b7050-167">이 요소는 클라이언트가 액세스할 수 있는 헤더 이름을 지정하는 `header` 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="b7050-168">아니요</span><span class="sxs-lookup"><span data-stu-id="b7050-168">No</span></span>|<span data-ttu-id="b7050-169">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-169">N/A</span></span>|  
|<span data-ttu-id="b7050-170">머리글</span><span class="sxs-lookup"><span data-stu-id="b7050-170">header</span></span>|<span data-ttu-id="b7050-171">헤더 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-171">Specifies a header name.</span></span>|<span data-ttu-id="b7050-172">섹션이 있는 경우 `allowed-headers` 또는 `expose-headers`에 하나 이상의 `header` 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="b7050-173">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b7050-174">특성</span><span class="sxs-lookup"><span data-stu-id="b7050-174">Attributes</span></span>  
  
|<span data-ttu-id="b7050-175">이름</span><span class="sxs-lookup"><span data-stu-id="b7050-175">Name</span></span>|<span data-ttu-id="b7050-176">설명</span><span class="sxs-lookup"><span data-stu-id="b7050-176">Description</span></span>|<span data-ttu-id="b7050-177">필수</span><span class="sxs-lookup"><span data-stu-id="b7050-177">Required</span></span>|<span data-ttu-id="b7050-178">기본값</span><span class="sxs-lookup"><span data-stu-id="b7050-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b7050-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="b7050-179">allow-credentials</span></span>|<span data-ttu-id="b7050-180">사전 응답의 `Access-Control-Allow-Credentials` 헤더가 이 특성 값으로 설정되고 도메인 간 요청에서 자격 증명을 제출하는 클라이언트 기능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="b7050-181">아니요</span><span class="sxs-lookup"><span data-stu-id="b7050-181">No</span></span>|<span data-ttu-id="b7050-182">false</span><span class="sxs-lookup"><span data-stu-id="b7050-182">false</span></span>|  
|<span data-ttu-id="b7050-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="b7050-183">preflight-result-max-age</span></span>|<span data-ttu-id="b7050-184">사전 응답의 `Access-Control-Max-Age` 헤더가 이 특성 값으로 설정되고 사전 응답을 캐싱하는 사용자 에이전트 기능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="b7050-185">아니요</span><span class="sxs-lookup"><span data-stu-id="b7050-185">No</span></span>|<span data-ttu-id="b7050-186">0</span><span class="sxs-lookup"><span data-stu-id="b7050-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b7050-187">사용 현황</span><span class="sxs-lookup"><span data-stu-id="b7050-187">Usage</span></span>  
 <span data-ttu-id="b7050-188">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b7050-189">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="b7050-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b7050-190">**정책 범위:** API, operation</span><span class="sxs-lookup"><span data-stu-id="b7050-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="b7050-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="b7050-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="b7050-192">`jsonp` 정책은 패딩이 있는 JSON(JSONP) 지원을 작업 또는 API에 추가하여 JavaScript 브라우저 기반 클라이언트의 도메인 간 호출을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="b7050-193">JSONP는 JavaScript 프로그램에서 다른 도메인의 서버로부터 데이터를 요청하는 데 사용하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="b7050-194">JSONP는 웹 페이지에 대한 액세스 권한이 동일한 도메인 내에 있어야 하는 경우 대부분의 웹 브라우저에서 적용하는 제한을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b7050-195">정책 문:</span><span class="sxs-lookup"><span data-stu-id="b7050-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="b7050-196">예</span><span class="sxs-lookup"><span data-stu-id="b7050-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="b7050-197">콜백 매개 변수 ?cb=XXX 없이 메서드를 호출하는 경우 일반 JSON(함수 호출 래퍼 없이)이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="b7050-198">콜백 매개 변수 `?cb=XXX`를 추가한 경우 `XYZ('<json result goes here>');`와 같이 콜백 함수 주위에 원래 JSON 결과를 래핑한 JSONP 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="b7050-199">요소</span><span class="sxs-lookup"><span data-stu-id="b7050-199">Elements</span></span>  
  
|<span data-ttu-id="b7050-200">이름</span><span class="sxs-lookup"><span data-stu-id="b7050-200">Name</span></span>|<span data-ttu-id="b7050-201">설명</span><span class="sxs-lookup"><span data-stu-id="b7050-201">Description</span></span>|<span data-ttu-id="b7050-202">필수</span><span class="sxs-lookup"><span data-stu-id="b7050-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b7050-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="b7050-203">jsonp</span></span>|<span data-ttu-id="b7050-204">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-204">Root element.</span></span>|<span data-ttu-id="b7050-205">예</span><span class="sxs-lookup"><span data-stu-id="b7050-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b7050-206">특성</span><span class="sxs-lookup"><span data-stu-id="b7050-206">Attributes</span></span>  
  
|<span data-ttu-id="b7050-207">이름</span><span class="sxs-lookup"><span data-stu-id="b7050-207">Name</span></span>|<span data-ttu-id="b7050-208">설명</span><span class="sxs-lookup"><span data-stu-id="b7050-208">Description</span></span>|<span data-ttu-id="b7050-209">필수</span><span class="sxs-lookup"><span data-stu-id="b7050-209">Required</span></span>|<span data-ttu-id="b7050-210">기본값</span><span class="sxs-lookup"><span data-stu-id="b7050-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b7050-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="b7050-211">callback-parameter-name</span></span>|<span data-ttu-id="b7050-212">함수가 상주하는 정규화된 도메인 이름이 접두사로 지정된 도메인 간 JavaScript 함수 호출</span><span class="sxs-lookup"><span data-stu-id="b7050-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="b7050-213">예</span><span class="sxs-lookup"><span data-stu-id="b7050-213">Yes</span></span>|<span data-ttu-id="b7050-214">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b7050-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b7050-215">사용 현황</span><span class="sxs-lookup"><span data-stu-id="b7050-215">Usage</span></span>  
 <span data-ttu-id="b7050-216">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7050-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b7050-217">**정책 섹션:** outbound</span><span class="sxs-lookup"><span data-stu-id="b7050-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="b7050-218">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="b7050-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b7050-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7050-219">Next steps</span></span>
<span data-ttu-id="b7050-220">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7050-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  