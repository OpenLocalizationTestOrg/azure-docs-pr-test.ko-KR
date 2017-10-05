---
title: "Azure API Management 변환 정책 | Microsoft Docs"
description: "Azure API Management에서 사용할 수 있는 변환 정책에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="ba550-103">API Management 변환 정책</span><span class="sxs-lookup"><span data-stu-id="ba550-103">API Management transformation policies</span></span>
<span data-ttu-id="ba550-104">이 문서에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="ba550-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="ba550-106"><a name="TransformationPolicies"></a> 변환 정책</span><span class="sxs-lookup"><span data-stu-id="ba550-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="ba550-107">[XML로 JSON 변환](api-management-transformation-policies.md#ConvertJSONtoXML) - 요청 또는 응답 본문을 JSON에서 XML로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="ba550-108">[JSON으로 XML 변환](api-management-transformation-policies.md#ConvertXMLtoJSON) - 요청 또는 응답 본문을 XML에서 JSON으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="ba550-109">[본문 문자열 찾기 및 바꾸기](api-management-transformation-policies.md#Findandreplacestringinbody) - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="ba550-110">[콘텐츠의 URL 마스킹](api-management-transformation-policies.md#MaskURLSContent) - 응답 본문의 링크를 다시 써서(마스킹) 게이트웨이를 통해 동일한 링크를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="ba550-111">[백 엔드 서비스 설정](api-management-transformation-policies.md#SetBackendService) - 들어오는 요청의 백 엔드 서비스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="ba550-112">[본문 설정](api-management-transformation-policies.md#SetBody) -들어오고 나가는 요청의 메시지 본문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="ba550-113">[HTTP 헤더 설정](api-management-transformation-policies.md#SetHTTPheader) - 기존 응답 및/또는 요청 헤더에 값을 할당하거나 새로운 응답 및/또는 요청 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="ba550-114">[쿼리 문자열 매개 변수 설정](api-management-transformation-policies.md#SetQueryStringParameter) - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="ba550-115">[URL 다시 쓰기](api-management-transformation-policies.md#RewriteURL) - 요청 URL을 공용 양식에서 웹 서비스에 필요한 양식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="ba550-116">[XSLT를 사용하여 XML 변환](api-management-transformation-policies.md#XSLTransform) - 요청 또는 응답 본문의 XML에 XSL 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="ba550-117"><a name="ConvertJSONtoXML"></a> XML로 JSON 변환</span><span class="sxs-lookup"><span data-stu-id="ba550-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="ba550-118">`json-to-xml` 정책은 요청 또는 응답 본문을 JSON에서 XML로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-119">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-120">예</span><span class="sxs-lookup"><span data-stu-id="ba550-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ba550-121">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-121">Elements</span></span>  
  
|<span data-ttu-id="ba550-122">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-122">Name</span></span>|<span data-ttu-id="ba550-123">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-123">Description</span></span>|<span data-ttu-id="ba550-124">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="ba550-125">json-to-xml</span></span>|<span data-ttu-id="ba550-126">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-126">Root element.</span></span>|<span data-ttu-id="ba550-127">예</span><span class="sxs-lookup"><span data-stu-id="ba550-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ba550-128">특성</span><span class="sxs-lookup"><span data-stu-id="ba550-128">Attributes</span></span>  
  
|<span data-ttu-id="ba550-129">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-129">Name</span></span>|<span data-ttu-id="ba550-130">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-130">Description</span></span>|<span data-ttu-id="ba550-131">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-131">Required</span></span>|<span data-ttu-id="ba550-132">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-133">apply</span><span class="sxs-lookup"><span data-stu-id="ba550-133">apply</span></span>|<span data-ttu-id="ba550-134">속성은 다음 값 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-135">- always: 항상 전환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="ba550-136">- content-type-json: 응답 Content-Type 헤더에서 JSON의 존재를 나타내는 경우에만 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="ba550-137">예</span><span class="sxs-lookup"><span data-stu-id="ba550-137">Yes</span></span>|<span data-ttu-id="ba550-138">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-138">N/A</span></span>|  
|<span data-ttu-id="ba550-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="ba550-139">consider-accept-header</span></span>|<span data-ttu-id="ba550-140">속성은 다음 값 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-141">- true: 요청 Accept 헤더에서 JSON을 요청하는 경우 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="ba550-142">- false: 항상 전환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="ba550-143">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-143">No</span></span>|<span data-ttu-id="ba550-144">true</span><span class="sxs-lookup"><span data-stu-id="ba550-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-145">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-145">Usage</span></span>  
 <span data-ttu-id="ba550-146">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-147">**정책 섹션:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="ba550-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="ba550-148">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-149"><a name="ConvertXMLtoJSON"></a> JSON으로 XML 변환</span><span class="sxs-lookup"><span data-stu-id="ba550-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="ba550-150">`xml-to-json` 정책은 요청 또는 응답 본문을 XML에서 JSON으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="ba550-151">이 정책은 XML 전용 백 엔드 웹 서비스를 기반으로 하는 API를 최신 형식으로 변환하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-152">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-153">예</span><span class="sxs-lookup"><span data-stu-id="ba550-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ba550-154">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-154">Elements</span></span>  
  
|<span data-ttu-id="ba550-155">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-155">Name</span></span>|<span data-ttu-id="ba550-156">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-156">Description</span></span>|<span data-ttu-id="ba550-157">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="ba550-158">xml-to-json</span></span>|<span data-ttu-id="ba550-159">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-159">Root element.</span></span>|<span data-ttu-id="ba550-160">예</span><span class="sxs-lookup"><span data-stu-id="ba550-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ba550-161">특성</span><span class="sxs-lookup"><span data-stu-id="ba550-161">Attributes</span></span>  
  
|<span data-ttu-id="ba550-162">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-162">Name</span></span>|<span data-ttu-id="ba550-163">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-163">Description</span></span>|<span data-ttu-id="ba550-164">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-164">Required</span></span>|<span data-ttu-id="ba550-165">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-166">kind</span><span class="sxs-lookup"><span data-stu-id="ba550-166">kind</span></span>|<span data-ttu-id="ba550-167">속성은 다음 값 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-168">- javascript-friendly: 변환된 JSON에는 JavaScript 개발자에게 익숙한 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="ba550-169">- direct: 변환된 JSON은 원래 XML 문서의 구조를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="ba550-170">예</span><span class="sxs-lookup"><span data-stu-id="ba550-170">Yes</span></span>|<span data-ttu-id="ba550-171">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-171">N/A</span></span>|  
|<span data-ttu-id="ba550-172">apply</span><span class="sxs-lookup"><span data-stu-id="ba550-172">apply</span></span>|<span data-ttu-id="ba550-173">속성은 다음 값 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-174">- always: 항상 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-174">-   always - convert always.</span></span><br /><span data-ttu-id="ba550-175">- content-type-xml: 응답 Content-Type 헤더에서 XML의 존재를 나타내는 경우에만 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="ba550-176">예</span><span class="sxs-lookup"><span data-stu-id="ba550-176">Yes</span></span>|<span data-ttu-id="ba550-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-177">N/A</span></span>|  
|<span data-ttu-id="ba550-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="ba550-178">consider-accept-header</span></span>|<span data-ttu-id="ba550-179">속성은 다음 값 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-180">- true: 요청 Accept 헤더에서 XML을 요청하는 경우 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="ba550-181">- false: 항상 전환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="ba550-182">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-182">No</span></span>|<span data-ttu-id="ba550-183">true</span><span class="sxs-lookup"><span data-stu-id="ba550-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-184">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-184">Usage</span></span>  
 <span data-ttu-id="ba550-185">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-186">**정책 섹션:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="ba550-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="ba550-187">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-188"><a name="Findandreplacestringinbody"></a> 본문 문자열 찾기 및 바꾸기</span><span class="sxs-lookup"><span data-stu-id="ba550-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="ba550-189">`find-and-replace` 정책은 요청 또는 응답 하위 문자열을 찾고 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-190">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-191">예</span><span class="sxs-lookup"><span data-stu-id="ba550-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="ba550-192">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-192">Elements</span></span>  
  
|<span data-ttu-id="ba550-193">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-193">Name</span></span>|<span data-ttu-id="ba550-194">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-194">Description</span></span>|<span data-ttu-id="ba550-195">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="ba550-196">find-and-replace</span></span>|<span data-ttu-id="ba550-197">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-197">Root element.</span></span>|<span data-ttu-id="ba550-198">예</span><span class="sxs-lookup"><span data-stu-id="ba550-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ba550-199">특성</span><span class="sxs-lookup"><span data-stu-id="ba550-199">Attributes</span></span>  
  
|<span data-ttu-id="ba550-200">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-200">Name</span></span>|<span data-ttu-id="ba550-201">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-201">Description</span></span>|<span data-ttu-id="ba550-202">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-202">Required</span></span>|<span data-ttu-id="ba550-203">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-204">from</span><span class="sxs-lookup"><span data-stu-id="ba550-204">from</span></span>|<span data-ttu-id="ba550-205">검색할 문자열</span><span class="sxs-lookup"><span data-stu-id="ba550-205">The string to search for.</span></span>|<span data-ttu-id="ba550-206">예</span><span class="sxs-lookup"><span data-stu-id="ba550-206">Yes</span></span>|<span data-ttu-id="ba550-207">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-207">N/A</span></span>|  
|<span data-ttu-id="ba550-208">to</span><span class="sxs-lookup"><span data-stu-id="ba550-208">to</span></span>|<span data-ttu-id="ba550-209">대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-209">The replacement string.</span></span> <span data-ttu-id="ba550-210">검색 문자열을 제거하려면 길이가 0인 대체 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="ba550-211">예</span><span class="sxs-lookup"><span data-stu-id="ba550-211">Yes</span></span>|<span data-ttu-id="ba550-212">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-213">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-213">Usage</span></span>  
 <span data-ttu-id="ba550-214">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-215">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ba550-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ba550-216">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-217"><a name="MaskURLSContent"></a> 콘텐츠의 URL 마스킹</span><span class="sxs-lookup"><span data-stu-id="ba550-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="ba550-218">`redirect-content-urls` 정책은 응답 본문에 링크를 다시 작성(마스킹)하여 게이트웨이를 통해 동등한 링크를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="ba550-219">outbound 섹션에서 응답 본문 링크를 다시 작성하여 게이트웨이를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="ba550-220">반대 효과를 가져오려면 inbound 섹션에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ba550-221">이 정책은 `Location` 헤더와 같은 헤더 값을 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="ba550-222">헤더 값을 변경하려면 [set-header](api-management-transformation-policies.md#SetHTTPheader) 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-223">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-224">예</span><span class="sxs-lookup"><span data-stu-id="ba550-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="ba550-225">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-225">Elements</span></span>  
  
|<span data-ttu-id="ba550-226">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-226">Name</span></span>|<span data-ttu-id="ba550-227">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-227">Description</span></span>|<span data-ttu-id="ba550-228">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="ba550-229">redirect-content-urls</span></span>|<span data-ttu-id="ba550-230">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-230">Root element.</span></span>|<span data-ttu-id="ba550-231">예</span><span class="sxs-lookup"><span data-stu-id="ba550-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-232">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-232">Usage</span></span>  
 <span data-ttu-id="ba550-233">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-234">**정책 섹션:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="ba550-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="ba550-235">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-236"><a name="SetBackendService"></a> 백 엔드 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="ba550-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="ba550-237">`set-backend-service` 정책을 사용하여 들어오는 요청을 해당 작업의 API 설정에 지정된 것과 다른 백 엔드로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="ba550-238">이 정책은 들어오는 요청의 백 엔드 서비스 기준 URL을 정책에 지정된 URL로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-239">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-240">예</span><span class="sxs-lookup"><span data-stu-id="ba550-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="ba550-241">이 예제에서 백 엔드 서비스 설정 정책은 쿼리 문자열에 전달된 버전 값에 기반한 요청을 API에 지정된 것과 다른 백 엔드 서비스로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="ba550-242">처음에는 백 엔드 서비스 기준 URL이 API 설정에서 파생되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="ba550-243">따라서 `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` 요청 URL은 `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`가 되고, 여기서 `http://contoso.com/api/10.4/`는 API 설정에 지정된 백 엔드 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="ba550-244">[<choose\>](api-management-advanced-policies.md#choose) 정책 문을 적용하면 백 엔드 서비스 기준 URL은 버전 요청 쿼리 매개 변수의 값에 따라 `http://contoso.com/api/8.2` 또는 `http://contoso.com/api/9.1`로 다시 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="ba550-245">예를 들어 값이 `"2013-15"`이면 최종 요청 URL은 `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="ba550-246">추가 변환 요청이 필요한 경우 다른 [변환 정책](api-management-transformation-policies.md#TransformationPolicies)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="ba550-247">예를 들어 요청이 버전 특정 백 엔드로 라우팅되고 있어 버전 쿼리 매개 변수를 제거하려면 [쿼리 문자열 설정 매개 변수](api-management-transformation-policies.md#SetQueryStringParameter) 정책을 사용하여 현재의 중복 버전 특성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="ba550-248">예제</span><span class="sxs-lookup"><span data-stu-id="ba550-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="ba550-249">이 예제에서 정책은 userId 쿼리 문자열을 파티션 키로 사용하고 파티션의 주 복제본을 사용하여 서비스 패브릭 백 엔드로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="ba550-250">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-250">Elements</span></span>  
  
|<span data-ttu-id="ba550-251">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-251">Name</span></span>|<span data-ttu-id="ba550-252">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-252">Description</span></span>|<span data-ttu-id="ba550-253">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="ba550-254">set-backend-service</span></span>|<span data-ttu-id="ba550-255">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-255">Root element.</span></span>|<span data-ttu-id="ba550-256">예</span><span class="sxs-lookup"><span data-stu-id="ba550-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ba550-257">특성</span><span class="sxs-lookup"><span data-stu-id="ba550-257">Attributes</span></span>  
  
|<span data-ttu-id="ba550-258">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-258">Name</span></span>|<span data-ttu-id="ba550-259">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-259">Description</span></span>|<span data-ttu-id="ba550-260">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-260">Required</span></span>|<span data-ttu-id="ba550-261">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-262">base-url</span><span class="sxs-lookup"><span data-stu-id="ba550-262">base-url</span></span>|<span data-ttu-id="ba550-263">새 백 엔드 서비스 기준 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-263">New backend service base URL.</span></span>|<span data-ttu-id="ba550-264">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-264">No</span></span>|<span data-ttu-id="ba550-265">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-265">N/A</span></span>|  
|<span data-ttu-id="ba550-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="ba550-266">backend-id</span></span>|<span data-ttu-id="ba550-267">라우팅할 백 엔드의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="ba550-268">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-268">No</span></span>|<span data-ttu-id="ba550-269">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-269">N/A</span></span>|  
|<span data-ttu-id="ba550-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="ba550-270">sf-partition-key</span></span>|<span data-ttu-id="ba550-271">백 엔드가 Service Fabric 서비스이고 'backend-id'를 사용하여 지정된 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="ba550-272">이름 확인 서비스에서 특정 파티션을 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="ba550-273">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-273">No</span></span>|<span data-ttu-id="ba550-274">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-274">N/A</span></span>|  
|<span data-ttu-id="ba550-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="ba550-275">sf-replica-type</span></span>|<span data-ttu-id="ba550-276">백 엔드가 Service Fabric 서비스이고 'backend-id'를 사용하여 지정된 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="ba550-277">요청이 파티션의 주 복제본으로 이동되는지, 보조 복제본으로 이동되는지를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="ba550-278">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-278">No</span></span>|<span data-ttu-id="ba550-279">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-279">N/A</span></span>|    
|<span data-ttu-id="ba550-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="ba550-280">sf-resolve-condition</span></span>|<span data-ttu-id="ba550-281">백 엔드가 Service Fabric 서비스인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="ba550-282">새로 확인할 때마다 Service Fabric 백 엔드에 대한 호출을 반복해야 하는지를 식별하는 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="ba550-283">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-283">No</span></span>|<span data-ttu-id="ba550-284">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-284">N/A</span></span>|    
|<span data-ttu-id="ba550-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="ba550-285">sf-service-instance-name</span></span>|<span data-ttu-id="ba550-286">백 엔드가 Service Fabric 서비스인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="ba550-287">런타임에 서비스 인스턴스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="ba550-288">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-288">No</span></span>|<span data-ttu-id="ba550-289">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="ba550-290">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-290">Usage</span></span>  
 <span data-ttu-id="ba550-291">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-292">**정책 섹션:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="ba550-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="ba550-293">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-294"><a name="SetBody"></a> 본문 설정</span><span class="sxs-lookup"><span data-stu-id="ba550-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="ba550-295">`set-body` 정책을 사용하여 들어오고 나가는 요청의 메시지 본문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="ba550-296">메시지 본문에 액세스하려면 정책이 inbound 또는 outbound 섹션에 있는지에 따라 `context.Request.Body` 또는 `context.Response.Body` 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="ba550-297">기본적으로 `context.Request.Body` 또는 `context.Response.Body`를 사용하여 메시지 본문에 액세스하면 원래 메시지 본문이 손실되며 해당 본문을 식으로 다시 반환하여 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="ba550-298">본문 내용을 보존하려면 메시지에 액세스할 때 `preserveContent` 매개 변수를 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="ba550-299">`preserveContent`가 `true`로 설정되고 식에서 다른 본문이 반환되면 반환된 본문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="ba550-300">`set-body` 정책을 사용할 때 다음을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="ba550-301">`set-body` 정책을 사용하여 새 본문 또는 업데이트된 본문을 반환하는 경우 명시적으로 새 본문 내용을 제공하므로 `preserveContent`를 `true`로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="ba550-302">인바운드 파이프라인에서 응답 내용을 보존하는 것은 아직 응답이 없기 때문에 이치에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="ba550-303">아웃바운드 파이프라인에서 요청 내용을 보존하는 것은 이 시점에서 요청을 이미 백 엔드로 보냈기 때문에 이치에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="ba550-304">인바운드 GET에서와 같이 메시지 본문이 없을 때 이 정책을 사용하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="ba550-305">자세한 내용은 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables) 표의 `context.Request.Body`, `context.Response.Body` 및 `IMessage` 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-306">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="ba550-307">예</span><span class="sxs-lookup"><span data-stu-id="ba550-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="ba550-308">리터럴 텍스트 예제</span><span class="sxs-lookup"><span data-stu-id="ba550-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="ba550-309">문자열로 액세스하는 예제</span><span class="sxs-lookup"><span data-stu-id="ba550-309">Example accessing the body as a string.</span></span> <span data-ttu-id="ba550-310">파이프라인에서 나중에 액세스할 수 있도록 원래 요청 본문을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="ba550-311">JObject로 본문에 액세스하는 예제</span><span class="sxs-lookup"><span data-stu-id="ba550-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="ba550-312">원래 요청 본문을 보존하지 않으므로 파이프라인에서 나중에 액세스하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="ba550-313">제품 기준 응답 필터링</span><span class="sxs-lookup"><span data-stu-id="ba550-313">Filter response based on product</span></span>  
 <span data-ttu-id="ba550-314">이 예제에서는 `Starter` 제품을 사용할 때 백 엔드 서비스에서 받은 응답의 데이터 요소를 제거하여 콘텐츠 필터링을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="ba550-315">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 34분 30초 재생 시점까지 빨리 진행하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="ba550-316">31분 50초 재생 시점에서 시작하는 [Dark Sky Forecast API](https://developer.forecast.io/)(영문) 개요를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="ba550-317">본문이 설정된 Liquid 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="ba550-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="ba550-318">[Liquid](https://shopify.github.io/liquid/basics/introduction/) 템플릿 언어를 사용하여 요청 또는 응답의 본문을 변환하도록 `set-body` 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="ba550-319">이 방법은 메시지 형식을 완전히 바꾸어야 하는 경우에 매우 효과적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba550-320">`set-body` 정책에 사용되는 Liquid 구현은 'C# 모드'로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="ba550-321">이러한 방식은 필터링과 같은 작업을 수행하는 경우에 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="ba550-322">예를 들어 날짜 필터를 사용하려면 다음과 같이 파스칼식 대/소문자 및 C# 날짜 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="ba550-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="ba550-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba550-324">Liquid 템플릿을 사용하여 XML 본문에 올바르게 바인딩하려면 `set-header` 정책을 사용하여 Content-Type을 application/xml, text/xml(또는 +xml로 끝나는 임의 형식)로 설정하세요. JSON 본문의 경우에는 application/json, text/json(또는 +json으로 끝나는 임의 형식)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="ba550-325">Liquid 템플릿을 사용하여 JSON을 SOAP으로 변환</span><span class="sxs-lookup"><span data-stu-id="ba550-325">Convert JSON to SOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="ba550-326">Liquid 템플릿을 사용하여 JSON 변환</span><span class="sxs-lookup"><span data-stu-id="ba550-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="ba550-327">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-327">Elements</span></span>  
  
|<span data-ttu-id="ba550-328">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-328">Name</span></span>|<span data-ttu-id="ba550-329">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-329">Description</span></span>|<span data-ttu-id="ba550-330">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-331">set-body</span><span class="sxs-lookup"><span data-stu-id="ba550-331">set-body</span></span>|<span data-ttu-id="ba550-332">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-332">Root element.</span></span> <span data-ttu-id="ba550-333">본문 텍스트 또는 본문을 반환하는 식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="ba550-334">예</span><span class="sxs-lookup"><span data-stu-id="ba550-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="ba550-335">속성</span><span class="sxs-lookup"><span data-stu-id="ba550-335">Properties</span></span>  
  
|<span data-ttu-id="ba550-336">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-336">Name</span></span>|<span data-ttu-id="ba550-337">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-337">Description</span></span>|<span data-ttu-id="ba550-338">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-338">Required</span></span>|<span data-ttu-id="ba550-339">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-340">template</span><span class="sxs-lookup"><span data-stu-id="ba550-340">template</span></span>|<span data-ttu-id="ba550-341">본문 설정 정책이 실행될 템플릿 모드를 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="ba550-342">현재 지원되는 유일한 값:</span><span class="sxs-lookup"><span data-stu-id="ba550-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="ba550-343">- liquid - 본문 설정 정책은 liquid 템플릿 엔진을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="ba550-344">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-344">No</span></span>|<span data-ttu-id="ba550-345">liquid</span><span class="sxs-lookup"><span data-stu-id="ba550-345">liquid</span></span>|  

<span data-ttu-id="ba550-346">요청 및 응답에 대한 정보에 액세스할 수 있도록 Liquid 템플릿은 다음 속성을 갖는 컨텍스트 개체에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="ba550-347">사용</span><span class="sxs-lookup"><span data-stu-id="ba550-347">Usage</span></span>  
 <span data-ttu-id="ba550-348">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-349">**정책 섹션:** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="ba550-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="ba550-350">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-351"><a name="SetHTTPheader"></a> HTTP 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="ba550-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="ba550-352">`set-header` 정책은 기존 응답 및/또는 요청 헤더에 값을 할당하거나 새 응답 및/또는 요청 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="ba550-353">HTTP 헤더 목록을 HTTP 메시지에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="ba550-354">이 정책을 인바운드 파이프라인에 지정하면 이 정책은 대상 서비스로 전달되는 요청의 HTTP 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="ba550-355">이 정책은 아웃바운드 파이프라인에 배치되는 경우 게이트웨이의 클라이언트로 보내는 응답의 HTTP 헤더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-356">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="ba550-357">예</span><span class="sxs-lookup"><span data-stu-id="ba550-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="ba550-358">예</span><span class="sxs-lookup"><span data-stu-id="ba550-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="ba550-359">컨텍스트 정보를 백 엔드 서비스로 전달</span><span class="sxs-lookup"><span data-stu-id="ba550-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="ba550-360">이 예제에서는 백 엔드 서비스에 컨텍스트 정보를 제공하기 위해 API 수준에서 정책을 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="ba550-361">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 10분 30초 재생 시점까지 빨리 진행하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="ba550-362">12분 10초 재생 시점에는 개발자 포털에서 작업을 호출하는 데모가 있으며, 여기서 작동 중인 정책을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="ba550-363">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="ba550-364">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-364">Elements</span></span>  
  
|<span data-ttu-id="ba550-365">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-365">Name</span></span>|<span data-ttu-id="ba550-366">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-366">Description</span></span>|<span data-ttu-id="ba550-367">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-368">set-header</span><span class="sxs-lookup"><span data-stu-id="ba550-368">set-header</span></span>|<span data-ttu-id="ba550-369">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-369">Root element.</span></span>|<span data-ttu-id="ba550-370">예</span><span class="sxs-lookup"><span data-stu-id="ba550-370">Yes</span></span>|  
|<span data-ttu-id="ba550-371">값</span><span class="sxs-lookup"><span data-stu-id="ba550-371">value</span></span>|<span data-ttu-id="ba550-372">설정할 헤더의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="ba550-373">동일한 이름을 가진 여러 헤더에 대해서는 추가 `value` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="ba550-374">예</span><span class="sxs-lookup"><span data-stu-id="ba550-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="ba550-375">속성</span><span class="sxs-lookup"><span data-stu-id="ba550-375">Properties</span></span>  
  
|<span data-ttu-id="ba550-376">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-376">Name</span></span>|<span data-ttu-id="ba550-377">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-377">Description</span></span>|<span data-ttu-id="ba550-378">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-378">Required</span></span>|<span data-ttu-id="ba550-379">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="ba550-380">exists-action</span></span>|<span data-ttu-id="ba550-381">헤더가 이미 지정되어 있는 경우 수행할 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="ba550-382">이 특성에는 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-383">- override: 기존 헤더 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="ba550-384">- skip: 기존 헤더 값을 바꾸지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="ba550-385">- append: 기존 헤더 값에 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="ba550-386">- delete: 요청에서 헤더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="ba550-387">`override`로 설정할 때 동일한 이름의 여러 항목을 등록하면 모든 항목(여러 번 나열됨)에 따라 헤더가 설정되며, 나열된 값만 결과에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="ba550-388">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-388">No</span></span>|<span data-ttu-id="ba550-389">override</span><span class="sxs-lookup"><span data-stu-id="ba550-389">override</span></span>|  
|<span data-ttu-id="ba550-390">name</span><span class="sxs-lookup"><span data-stu-id="ba550-390">name</span></span>|<span data-ttu-id="ba550-391">설정할 헤더의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="ba550-392">예</span><span class="sxs-lookup"><span data-stu-id="ba550-392">Yes</span></span>|<span data-ttu-id="ba550-393">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-394">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-394">Usage</span></span>  
 <span data-ttu-id="ba550-395">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-396">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ba550-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ba550-397">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-398"><a name="SetQueryStringParameter"></a> 쿼리 문자열 매개 변수 설정</span><span class="sxs-lookup"><span data-stu-id="ba550-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="ba550-399">`set-query-parameter` 정책은 요청 쿼리 문자열 매개 변수의 추가, 값 바꾸기 또는 삭제를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="ba550-400">백 엔드 서비스에 필요한 쿼리 매개 변수를 전달하는 데 사용하며, 이러한 매개 변수는 선택적이거나 요청에 절대로 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-401">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="ba550-402">예</span><span class="sxs-lookup"><span data-stu-id="ba550-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="ba550-403">예</span><span class="sxs-lookup"><span data-stu-id="ba550-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="ba550-404">컨텍스트 정보를 백 엔드 서비스로 전달</span><span class="sxs-lookup"><span data-stu-id="ba550-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="ba550-405">이 예제에서는 백 엔드 서비스에 컨텍스트 정보를 제공하기 위해 API 수준에서 정책을 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="ba550-406">이 정책을 구성하고 사용하는 데모는 [클라우드 표지 에피소드 177: Vlad Vinogradsky와 함께 하는 추가 API Management 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/)(영문)에서 10분 30초 재생 시점까지 빨리 진행하면서 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="ba550-407">12분 10초 재생 시점에는 개발자 포털에서 작업을 호출하는 데모가 있으며, 여기서 작동 중인 정책을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="ba550-408">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="ba550-409">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-409">Elements</span></span>  
  
|<span data-ttu-id="ba550-410">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-410">Name</span></span>|<span data-ttu-id="ba550-411">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-411">Description</span></span>|<span data-ttu-id="ba550-412">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="ba550-413">set-query-parameter</span></span>|<span data-ttu-id="ba550-414">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-414">Root element.</span></span>|<span data-ttu-id="ba550-415">예</span><span class="sxs-lookup"><span data-stu-id="ba550-415">Yes</span></span>|  
|<span data-ttu-id="ba550-416">값</span><span class="sxs-lookup"><span data-stu-id="ba550-416">value</span></span>|<span data-ttu-id="ba550-417">설정할 쿼리 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="ba550-418">동일한 이름을 가진 여러 쿼리 매개 변수에 대해서는 추가 `value` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="ba550-419">예</span><span class="sxs-lookup"><span data-stu-id="ba550-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="ba550-420">속성</span><span class="sxs-lookup"><span data-stu-id="ba550-420">Properties</span></span>  
  
|<span data-ttu-id="ba550-421">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-421">Name</span></span>|<span data-ttu-id="ba550-422">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-422">Description</span></span>|<span data-ttu-id="ba550-423">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-423">Required</span></span>|<span data-ttu-id="ba550-424">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="ba550-425">exists-action</span></span>|<span data-ttu-id="ba550-426">쿼리 매개 변수가 이미 지정되어 있는 경우 수행할 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="ba550-427">이 특성에는 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="ba550-428">- override: 기존 쿼리 매개 변수 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="ba550-429">- skip: 기존 쿼리 매개 변수 값을 바꾸지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="ba550-430">- append: 기존 쿼리 매개 변수 값에 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="ba550-431">- delete: 요청에서 쿼리 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="ba550-432">`override`로 설정할 때 동일한 이름의 여러 항목을 등록하면 모든 항목(여러 번 나열됨)에 따라 쿼리 매개 변수가 설정되며, 나열된 값만 결과에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="ba550-433">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-433">No</span></span>|<span data-ttu-id="ba550-434">override</span><span class="sxs-lookup"><span data-stu-id="ba550-434">override</span></span>|  
|<span data-ttu-id="ba550-435">name</span><span class="sxs-lookup"><span data-stu-id="ba550-435">name</span></span>|<span data-ttu-id="ba550-436">설정할 쿼리 매개 변수의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="ba550-437">예</span><span class="sxs-lookup"><span data-stu-id="ba550-437">Yes</span></span>|<span data-ttu-id="ba550-438">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-439">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-439">Usage</span></span>  
 <span data-ttu-id="ba550-440">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-441">**정책 섹션:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="ba550-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="ba550-442">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-443"><a name="RewriteURL"></a> URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="ba550-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="ba550-444">`rewrite-uri` 정책은 다음 예제와 같이 요청 URL을 공용 양식에서 웹 서비스에 필요한 양식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="ba550-445">공용 URL - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="ba550-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="ba550-446">요청 URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="ba550-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="ba550-447">이 정책은 사람 및/또는 브라우저에 친숙한 URL을 웹 서비스에 필요한 URL 형식으로 변환해야 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="ba550-448">이 정책은 쿼리 문자열을 포함하지 않고 리소스 경로(체계 및 권한 뒤)만 포함하는 전적으로 구조적인 URL인 간편 URL, RESTful URL, 사용자에게 친숙한 URL 또는 SEO 지원 URL과 같은 대체 URL 형식을 표시할 때만 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="ba550-449">보통 미학, 사용 편의성 또는 SEO(검색 엔진 최적화)를 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ba550-450">정책을 사용하여 쿼리 문자열 매개 변수만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="ba550-451">다시 쓰기 URL에 추가 템플릿 경로 매개 변수를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="ba550-452">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-453">예</span><span class="sxs-lookup"><span data-stu-id="ba550-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="ba550-454">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-454">Elements</span></span>  
  
|<span data-ttu-id="ba550-455">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-455">Name</span></span>|<span data-ttu-id="ba550-456">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-456">Description</span></span>|<span data-ttu-id="ba550-457">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="ba550-458">rewrite-uri</span></span>|<span data-ttu-id="ba550-459">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-459">Root element.</span></span>|<span data-ttu-id="ba550-460">예</span><span class="sxs-lookup"><span data-stu-id="ba550-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ba550-461">특성</span><span class="sxs-lookup"><span data-stu-id="ba550-461">Attributes</span></span>  
  
|<span data-ttu-id="ba550-462">특성</span><span class="sxs-lookup"><span data-stu-id="ba550-462">Attribute</span></span>|<span data-ttu-id="ba550-463">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-463">Description</span></span>|<span data-ttu-id="ba550-464">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-464">Required</span></span>|<span data-ttu-id="ba550-465">기본값</span><span class="sxs-lookup"><span data-stu-id="ba550-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ba550-466">template</span><span class="sxs-lookup"><span data-stu-id="ba550-466">template</span></span>|<span data-ttu-id="ba550-467">모든 쿼리 문자열 매개 변수가 포함된 실제 웹 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="ba550-468">식을 사용하는 경우 전체 값이 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="ba550-469">예</span><span class="sxs-lookup"><span data-stu-id="ba550-469">Yes</span></span>|<span data-ttu-id="ba550-470">해당 없음</span><span class="sxs-lookup"><span data-stu-id="ba550-470">N/A</span></span>|  
|<span data-ttu-id="ba550-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="ba550-471">copy-unmatched-params</span></span>|<span data-ttu-id="ba550-472">원본 URL 템플릿에 없는 들어오는 요청의 쿼리 매개 변수가 re-write 템플릿에 의해 정의된 URL에 추가되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="ba550-473">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-473">No</span></span>|<span data-ttu-id="ba550-474">true</span><span class="sxs-lookup"><span data-stu-id="ba550-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-475">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-475">Usage</span></span>  
 <span data-ttu-id="ba550-476">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-477">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="ba550-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ba550-478">**정책 범위:** product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="ba550-479"><a name="XSLTransform"></a> XSLT를 사용하여 XML 변환</span><span class="sxs-lookup"><span data-stu-id="ba550-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="ba550-480">`Transform XML using an XSLT` 정책은 요청 또는 응답 본문의 XML에 XSL 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ba550-481">정책 문</span><span class="sxs-lookup"><span data-stu-id="ba550-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="ba550-482">예</span><span class="sxs-lookup"><span data-stu-id="ba550-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ba550-483">요소</span><span class="sxs-lookup"><span data-stu-id="ba550-483">Elements</span></span>  
  
|<span data-ttu-id="ba550-484">이름</span><span class="sxs-lookup"><span data-stu-id="ba550-484">Name</span></span>|<span data-ttu-id="ba550-485">설명</span><span class="sxs-lookup"><span data-stu-id="ba550-485">Description</span></span>|<span data-ttu-id="ba550-486">필수</span><span class="sxs-lookup"><span data-stu-id="ba550-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="ba550-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="ba550-487">xsl-transform</span></span>|<span data-ttu-id="ba550-488">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-488">Root element.</span></span>|<span data-ttu-id="ba550-489">예</span><span class="sxs-lookup"><span data-stu-id="ba550-489">Yes</span></span>|  
|<span data-ttu-id="ba550-490">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ba550-490">parameter</span></span>|<span data-ttu-id="ba550-491">변환에 사용되는 변수를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="ba550-492">아니요</span><span class="sxs-lookup"><span data-stu-id="ba550-492">No</span></span>|  
|<span data-ttu-id="ba550-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="ba550-493">xsl:stylesheet</span></span>|<span data-ttu-id="ba550-494">루트 스타일시트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-494">Root stylesheet element.</span></span> <span data-ttu-id="ba550-495">표준 [XSLT 사양](http://www.w3.org/TR/xslt)(영문)에 정의된 모든 요소와 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="ba550-496">예</span><span class="sxs-lookup"><span data-stu-id="ba550-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ba550-497">사용 현황</span><span class="sxs-lookup"><span data-stu-id="ba550-497">Usage</span></span>  
 <span data-ttu-id="ba550-498">이 정책은 다음과 같은 정책 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba550-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ba550-499">**정책 섹션:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="ba550-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="ba550-500">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="ba550-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ba550-501">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba550-501">Next steps</span></span>
<span data-ttu-id="ba550-502">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba550-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
