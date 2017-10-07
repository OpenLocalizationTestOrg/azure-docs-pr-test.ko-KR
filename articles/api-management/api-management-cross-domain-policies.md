---
title: "API 관리 도메인 간 정책 aaaAzure | Microsoft Docs"
description: "도메인 간 정책 Azure API 관리에 사용할 수 있는 hello에 알아봅니다."
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
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="3705e-103">도메인 정책 간 API 관리</span><span class="sxs-lookup"><span data-stu-id="3705e-103">API Management cross domain policies</span></span>
<span data-ttu-id="3705e-104">이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="3705e-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3705e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="3705e-106"><a name="CrossDomainPolicies"></a> 도메인 간 정책</span><span class="sxs-lookup"><span data-stu-id="3705e-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="3705e-107">[도메인 간 호출을 허용](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 hello API에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="3705e-108">[CORS](api-management-cross-domain-policies.md#CORS) -브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 또는 tooan 작업을 지원 크로스-원본 자원 공유 (CORS)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="3705e-109">[JSONP](api-management-cross-domain-policies.md#JSONP) -JSON with padding (JSONP) 지원 tooan 작업이 추가 하거나는 API tooallow 도메인 간 JavaScript 브라우저 기반 클라이언트에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="3705e-110"><a name="AllowCrossDomainCalls"></a> 도메인 간 호출 허용</span><span class="sxs-lookup"><span data-stu-id="3705e-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="3705e-111">사용 하 여 hello `cross-domain` 정책 toomake hello API Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3705e-112">정책 문</span><span class="sxs-lookup"><span data-stu-id="3705e-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="3705e-113">예</span><span class="sxs-lookup"><span data-stu-id="3705e-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="3705e-114">요소</span><span class="sxs-lookup"><span data-stu-id="3705e-114">Elements</span></span>  
  
|<span data-ttu-id="3705e-115">이름</span><span class="sxs-lookup"><span data-stu-id="3705e-115">Name</span></span>|<span data-ttu-id="3705e-116">설명</span><span class="sxs-lookup"><span data-stu-id="3705e-116">Description</span></span>|<span data-ttu-id="3705e-117">필수</span><span class="sxs-lookup"><span data-stu-id="3705e-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3705e-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="3705e-118">cross-domain</span></span>|<span data-ttu-id="3705e-119">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-119">Root element.</span></span> <span data-ttu-id="3705e-120">자식 요소 toohello 따라야 [Adobe 도메인 간 정책 파일 사양](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="3705e-121">예</span><span class="sxs-lookup"><span data-stu-id="3705e-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3705e-122">사용</span><span class="sxs-lookup"><span data-stu-id="3705e-122">Usage</span></span>  
 <span data-ttu-id="3705e-123">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3705e-124">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="3705e-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3705e-125">**정책 범위:** global</span><span class="sxs-lookup"><span data-stu-id="3705e-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="3705e-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="3705e-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="3705e-127">hello `cors` tooan 작업을 지원 크로스-원본 자원 공유 (CORS) 또는 브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 정책을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="3705e-128">CORS는 브라우저와 서버 toointeract 있으며 tooallow 특정 교차 원본 요청 (예:: 웹 페이지 tooother 도메인에는 JavaScript에서 수행한는 XMLHttpRequests 호출) 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="3705e-129">따라서 동일 원본의 요청만 허용하는 것보다 유연성이 더 뛰어나며 모든 원본 간 요청을 허용하는 것보다 보안도 더 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3705e-130">정책 문:</span><span class="sxs-lookup"><span data-stu-id="3705e-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="3705e-131">예제</span><span class="sxs-lookup"><span data-stu-id="3705e-131">Example</span></span>  
 <span data-ttu-id="3705e-132">이 예제에서는 사용자 지정 헤더 나 메서드 GET 및 POST 이외의 항목과 같이 toosupport 사전 비행 요청 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="3705e-133">toosupport 사용자 지정 헤더 및 추가 HTTP 동사를 사용 하 여 hello `allowed-methods` 및 `allowed-headers` hello 다음 예제와 같이 섹션.</span><span class="sxs-lookup"><span data-stu-id="3705e-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="3705e-134">요소</span><span class="sxs-lookup"><span data-stu-id="3705e-134">Elements</span></span>  
  
|<span data-ttu-id="3705e-135">이름</span><span class="sxs-lookup"><span data-stu-id="3705e-135">Name</span></span>|<span data-ttu-id="3705e-136">설명</span><span class="sxs-lookup"><span data-stu-id="3705e-136">Description</span></span>|<span data-ttu-id="3705e-137">필수</span><span class="sxs-lookup"><span data-stu-id="3705e-137">Required</span></span>|<span data-ttu-id="3705e-138">기본값</span><span class="sxs-lookup"><span data-stu-id="3705e-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3705e-139">cors</span><span class="sxs-lookup"><span data-stu-id="3705e-139">cors</span></span>|<span data-ttu-id="3705e-140">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-140">Root element.</span></span>|<span data-ttu-id="3705e-141">예</span><span class="sxs-lookup"><span data-stu-id="3705e-141">Yes</span></span>|<span data-ttu-id="3705e-142">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-142">N/A</span></span>|  
|<span data-ttu-id="3705e-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="3705e-143">allowed-origins</span></span>|<span data-ttu-id="3705e-144">포함 `origin` 도메인 간 요청에 대 한 원본을 허용 하는 hello를 설명 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="3705e-145">`allowed-origins`단일 포함 될 수 있습니다 `origin` 지정 하는 요소 `*` tooallow 모든 원본 또는 하나 이상의 `origin` URI를 포함 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="3705e-146">예</span><span class="sxs-lookup"><span data-stu-id="3705e-146">Yes</span></span>|<span data-ttu-id="3705e-147">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-147">N/A</span></span>|  
|<span data-ttu-id="3705e-148">원본</span><span class="sxs-lookup"><span data-stu-id="3705e-148">origin</span></span>|<span data-ttu-id="3705e-149">hello 값일 수 하나 `*` tooallow 모든 원본을 또는 단일 원본을 지정 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="3705e-150">hello URI 구성표, 호스트 및 포트를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="3705e-151">예</span><span class="sxs-lookup"><span data-stu-id="3705e-151">Yes</span></span>|<span data-ttu-id="3705e-152">Hello 포트를 URI에서 생략 된 경우 포트 80은 HTTP에 대 한 사용 및 HTTPS에 포트 443 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="3705e-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="3705e-153">allowed-methods</span></span>|<span data-ttu-id="3705e-154">GET 또는 POST 이외의 메서드가 허용되는 경우 이 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="3705e-155">포함 `method` hello 지원 HTTP 동사를 지정 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="3705e-156">아니요</span><span class="sxs-lookup"><span data-stu-id="3705e-156">No</span></span>|<span data-ttu-id="3705e-157">이 섹션이 없으면 GET 및 POST가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="3705e-158">메서드</span><span class="sxs-lookup"><span data-stu-id="3705e-158">method</span></span>|<span data-ttu-id="3705e-159">HTTP 동사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="3705e-160">하나 이상의 `method` 경우 hello 요소는 필수 `allowed-methods` 섹션은 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="3705e-161">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-161">N/A</span></span>|  
|<span data-ttu-id="3705e-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="3705e-162">allowed-headers</span></span>|<span data-ttu-id="3705e-163">이 요소는 포함 `header` hello 요청에 포함 될 수 있는 hello 헤더의 이름을 지정 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="3705e-164">아니요</span><span class="sxs-lookup"><span data-stu-id="3705e-164">No</span></span>|<span data-ttu-id="3705e-165">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-165">N/A</span></span>|  
|<span data-ttu-id="3705e-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="3705e-166">expose-headers</span></span>|<span data-ttu-id="3705e-167">이 요소는 포함 `header` hello 클라이언트에서 액세스할 수 있는 hello 헤더의 이름을 지정 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="3705e-168">아니요</span><span class="sxs-lookup"><span data-stu-id="3705e-168">No</span></span>|<span data-ttu-id="3705e-169">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-169">N/A</span></span>|  
|<span data-ttu-id="3705e-170">머리글</span><span class="sxs-lookup"><span data-stu-id="3705e-170">header</span></span>|<span data-ttu-id="3705e-171">헤더 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-171">Specifies a header name.</span></span>|<span data-ttu-id="3705e-172">하나 이상의 `header` 요소에 필요한 `allowed-headers` 또는 `expose-headers` hello 섹션은 포함 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3705e-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="3705e-173">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3705e-174">특성</span><span class="sxs-lookup"><span data-stu-id="3705e-174">Attributes</span></span>  
  
|<span data-ttu-id="3705e-175">이름</span><span class="sxs-lookup"><span data-stu-id="3705e-175">Name</span></span>|<span data-ttu-id="3705e-176">설명</span><span class="sxs-lookup"><span data-stu-id="3705e-176">Description</span></span>|<span data-ttu-id="3705e-177">필수</span><span class="sxs-lookup"><span data-stu-id="3705e-177">Required</span></span>|<span data-ttu-id="3705e-178">기본값</span><span class="sxs-lookup"><span data-stu-id="3705e-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3705e-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="3705e-179">allow-credentials</span></span>|<span data-ttu-id="3705e-180">hello `Access-Control-Allow-Credentials` hello에 대 한 실행 전 응답 헤더 집합 toohello 값이이 특성의 되며 도메인 간 요청에서 hello 클라이언트 기능 toosubmit 자격 증명에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="3705e-181">아니요</span><span class="sxs-lookup"><span data-stu-id="3705e-181">No</span></span>|<span data-ttu-id="3705e-182">false</span><span class="sxs-lookup"><span data-stu-id="3705e-182">false</span></span>|  
|<span data-ttu-id="3705e-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="3705e-183">preflight-result-max-age</span></span>|<span data-ttu-id="3705e-184">hello `Access-Control-Max-Age` hello에 대 한 실행 전 응답 헤더 집합 toohello 값이이 특성의 되며 hello 사용자 에이전트의 기능 toocache 전 응답에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="3705e-185">아니요</span><span class="sxs-lookup"><span data-stu-id="3705e-185">No</span></span>|<span data-ttu-id="3705e-186">0</span><span class="sxs-lookup"><span data-stu-id="3705e-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3705e-187">사용</span><span class="sxs-lookup"><span data-stu-id="3705e-187">Usage</span></span>  
 <span data-ttu-id="3705e-188">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3705e-189">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="3705e-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3705e-190">**정책 범위:** API, operation</span><span class="sxs-lookup"><span data-stu-id="3705e-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="3705e-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="3705e-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="3705e-192">hello `jsonp` 정책 안쪽 여백 (JSONP) 지원 tooan 작업이 나 JavaScript 브라우저 기반 클라이언트에서 API tooallow 도메인 간 호출 된 JSON을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="3705e-193">JSONP는 다른 도메인에 서버에서 JavaScript 프로그램 toorequest 데이터에서 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="3705e-194">Hello에 대 한 액세스 tooweb 페이지를 사용 해야 하는 대부분 웹 브라우저에 의해 적용 하는 hello 제한을 무시 동일한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3705e-195">정책 문</span><span class="sxs-lookup"><span data-stu-id="3705e-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="3705e-196">예제</span><span class="sxs-lookup"><span data-stu-id="3705e-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="3705e-197">Hello 콜백 매개 변수 없이 hello 메서드를 호출 하는 경우? cb = XXX (함수 호출 래퍼가) 없이 일반 JSON을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="3705e-198">Hello 콜백 매개 변수를 추가 하는 경우 `?cb=XXX` hello hello 콜백 함수 처럼 원래 JSON 결과 래핑하는 JSONP 결과가 반환 됩니다`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="3705e-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="3705e-199">요소</span><span class="sxs-lookup"><span data-stu-id="3705e-199">Elements</span></span>  
  
|<span data-ttu-id="3705e-200">이름</span><span class="sxs-lookup"><span data-stu-id="3705e-200">Name</span></span>|<span data-ttu-id="3705e-201">설명</span><span class="sxs-lookup"><span data-stu-id="3705e-201">Description</span></span>|<span data-ttu-id="3705e-202">필수</span><span class="sxs-lookup"><span data-stu-id="3705e-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3705e-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="3705e-203">jsonp</span></span>|<span data-ttu-id="3705e-204">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-204">Root element.</span></span>|<span data-ttu-id="3705e-205">예</span><span class="sxs-lookup"><span data-stu-id="3705e-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3705e-206">특성</span><span class="sxs-lookup"><span data-stu-id="3705e-206">Attributes</span></span>  
  
|<span data-ttu-id="3705e-207">이름</span><span class="sxs-lookup"><span data-stu-id="3705e-207">Name</span></span>|<span data-ttu-id="3705e-208">설명</span><span class="sxs-lookup"><span data-stu-id="3705e-208">Description</span></span>|<span data-ttu-id="3705e-209">필수</span><span class="sxs-lookup"><span data-stu-id="3705e-209">Required</span></span>|<span data-ttu-id="3705e-210">기본값</span><span class="sxs-lookup"><span data-stu-id="3705e-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3705e-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="3705e-211">callback-parameter-name</span></span>|<span data-ttu-id="3705e-212">hello 도메인 간 JavaScript 함수 호출 hello 정규화 된 도메인 이름을 접두사로 hello 함수 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="3705e-213">예</span><span class="sxs-lookup"><span data-stu-id="3705e-213">Yes</span></span>|<span data-ttu-id="3705e-214">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3705e-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3705e-215">사용</span><span class="sxs-lookup"><span data-stu-id="3705e-215">Usage</span></span>  
 <span data-ttu-id="3705e-216">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="3705e-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3705e-217">**정책 섹션:** outbound</span><span class="sxs-lookup"><span data-stu-id="3705e-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="3705e-218">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="3705e-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="3705e-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3705e-219">Next steps</span></span>
<span data-ttu-id="3705e-220">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3705e-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  