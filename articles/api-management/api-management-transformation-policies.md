---
title: "API 관리 변환 정책 aaaAzure | Microsoft Docs"
description: "Azure API 관리에 사용할 수 있는 hello 변환 정책에 알아봅니다."
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
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="e8130-103">API Management 변환 정책</span><span class="sxs-lookup"><span data-stu-id="e8130-103">API Management transformation policies</span></span>
<span data-ttu-id="e8130-104">이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="e8130-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8130-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e8130-106"><a name="TransformationPolicies"></a> 변환 정책</span><span class="sxs-lookup"><span data-stu-id="e8130-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="e8130-107">[JSON tooXML 변환](api-management-transformation-policies.md#ConvertJSONtoXML) -요청으로 변환 하거나 JSON tooXML에서 응답 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="e8130-108">[XML tooJSON 변환](api-management-transformation-policies.md#ConvertXMLtoJSON) -변환 요청 또는 응답 본문에서 XML tooJSON 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="e8130-109">[본문 문자열 찾기 및 바꾸기](api-management-transformation-policies.md#Findandreplacestringinbody) - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="e8130-110">[콘텐츠의 Url 마스킹](api-management-transformation-policies.md#MaskURLSContent) -다시 작성 (마스킹) 링크 hello에 대 한 응답 본문 toohello hello 게이트웨이 통해 동일한 링크를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="e8130-111">[백 엔드 서비스 설정](api-management-transformation-policies.md#SetBackendService) -들어오는 요청에 대 한 hello 백 엔드 서비스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="e8130-112">[본문 설정](api-management-transformation-policies.md#SetBody) -들어오는 요청과 나가는 요청에 대 한 hello 메시지 본문을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="e8130-113">[HTTP 헤더 설정](api-management-transformation-policies.md#SetHTTPheader) -값 tooan 기존 응답 및/또는 요청 헤더를 할당 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="e8130-114">[쿼리 문자열 매개 변수 설정](api-management-transformation-policies.md#SetQueryStringParameter) - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="e8130-115">[URL 재작성](api-management-transformation-policies.md#RewriteURL) -요청 URL hello 웹 서비스에서 공용 형식 toohello 형식에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="e8130-116">[XSLT를 사용 하 여 XML 변형](api-management-transformation-policies.md#XSLTransform) -는 XSL 변환을 tooXML hello 요청 또는 응답 본문에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="e8130-117"><a name="ConvertJSONtoXML"></a>JSON tooXML 변환</span><span class="sxs-lookup"><span data-stu-id="e8130-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="e8130-118">hello `json-to-xml` JSON tooXML에서 요청 또는 응답 본문을 변환 하는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-119">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="e8130-120">예</span><span class="sxs-lookup"><span data-stu-id="e8130-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e8130-121">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-121">Elements</span></span>  
  
|<span data-ttu-id="e8130-122">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-122">Name</span></span>|<span data-ttu-id="e8130-123">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-123">Description</span></span>|<span data-ttu-id="e8130-124">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="e8130-125">json-to-xml</span></span>|<span data-ttu-id="e8130-126">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-126">Root element.</span></span>|<span data-ttu-id="e8130-127">예</span><span class="sxs-lookup"><span data-stu-id="e8130-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e8130-128">특성</span><span class="sxs-lookup"><span data-stu-id="e8130-128">Attributes</span></span>  
  
|<span data-ttu-id="e8130-129">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-129">Name</span></span>|<span data-ttu-id="e8130-130">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-130">Description</span></span>|<span data-ttu-id="e8130-131">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-131">Required</span></span>|<span data-ttu-id="e8130-132">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-133">apply</span><span class="sxs-lookup"><span data-stu-id="e8130-133">apply</span></span>|<span data-ttu-id="e8130-134">다음 값에는 hello tooone hello 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-135">- always: 항상 전환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="e8130-136">- content-type-json: 응답 Content-Type 헤더에서 JSON의 존재를 나타내는 경우에만 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="e8130-137">예</span><span class="sxs-lookup"><span data-stu-id="e8130-137">Yes</span></span>|<span data-ttu-id="e8130-138">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-138">N/A</span></span>|  
|<span data-ttu-id="e8130-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="e8130-139">consider-accept-header</span></span>|<span data-ttu-id="e8130-140">다음 값에는 hello tooone hello 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-141">- true: 요청 Accept 헤더에서 JSON을 요청하는 경우 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="e8130-142">- false: 항상 전환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="e8130-143">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-143">No</span></span>|<span data-ttu-id="e8130-144">true</span><span class="sxs-lookup"><span data-stu-id="e8130-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-145">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-145">Usage</span></span>  
 <span data-ttu-id="e8130-146">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-147">**정책 섹션:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="e8130-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="e8130-148">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-149"><a name="ConvertXMLtoJSON"></a>XML tooJSON 변환</span><span class="sxs-lookup"><span data-stu-id="e8130-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="e8130-150">hello `xml-to-json` 정책 XML tooJSON에서 요청 또는 응답 본문을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="e8130-151">이 정책을 사용 하는 toomodernize XML 전용 백 엔드 웹 서비스를 기반으로 Api 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-152">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="e8130-153">예</span><span class="sxs-lookup"><span data-stu-id="e8130-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e8130-154">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-154">Elements</span></span>  
  
|<span data-ttu-id="e8130-155">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-155">Name</span></span>|<span data-ttu-id="e8130-156">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-156">Description</span></span>|<span data-ttu-id="e8130-157">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="e8130-158">xml-to-json</span></span>|<span data-ttu-id="e8130-159">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-159">Root element.</span></span>|<span data-ttu-id="e8130-160">예</span><span class="sxs-lookup"><span data-stu-id="e8130-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e8130-161">특성</span><span class="sxs-lookup"><span data-stu-id="e8130-161">Attributes</span></span>  
  
|<span data-ttu-id="e8130-162">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-162">Name</span></span>|<span data-ttu-id="e8130-163">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-163">Description</span></span>|<span data-ttu-id="e8130-164">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-164">Required</span></span>|<span data-ttu-id="e8130-165">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-166">kind</span><span class="sxs-lookup"><span data-stu-id="e8130-166">kind</span></span>|<span data-ttu-id="e8130-167">다음 값에는 hello tooone hello 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-168">javascript-활용이 편한-hello 변환 JSON 양식 tooJavaScript 친숙 한 개발자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="e8130-169">-직접-hello 변환 된 JSON 구조를 반영 hello 원래 XML 문서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="e8130-170">예</span><span class="sxs-lookup"><span data-stu-id="e8130-170">Yes</span></span>|<span data-ttu-id="e8130-171">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-171">N/A</span></span>|  
|<span data-ttu-id="e8130-172">apply</span><span class="sxs-lookup"><span data-stu-id="e8130-172">apply</span></span>|<span data-ttu-id="e8130-173">다음 값에는 hello tooone hello 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-174">- always: 항상 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-174">-   always - convert always.</span></span><br /><span data-ttu-id="e8130-175">- content-type-xml: 응답 Content-Type 헤더에서 XML의 존재를 나타내는 경우에만 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="e8130-176">예</span><span class="sxs-lookup"><span data-stu-id="e8130-176">Yes</span></span>|<span data-ttu-id="e8130-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-177">N/A</span></span>|  
|<span data-ttu-id="e8130-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="e8130-178">consider-accept-header</span></span>|<span data-ttu-id="e8130-179">다음 값에는 hello tooone hello 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-180">- true: 요청 Accept 헤더에서 XML을 요청하는 경우 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="e8130-181">- false: 항상 전환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="e8130-182">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-182">No</span></span>|<span data-ttu-id="e8130-183">true</span><span class="sxs-lookup"><span data-stu-id="e8130-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-184">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-184">Usage</span></span>  
 <span data-ttu-id="e8130-185">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-186">**정책 섹션:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="e8130-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="e8130-187">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-188"><a name="Findandreplacestringinbody"></a> 본문 문자열 찾기 및 바꾸기</span><span class="sxs-lookup"><span data-stu-id="e8130-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="e8130-189">hello `find-and-replace` 정책 요청 또는 응답 하위 문자열을 찾아서 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-190">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="e8130-191">예</span><span class="sxs-lookup"><span data-stu-id="e8130-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="e8130-192">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-192">Elements</span></span>  
  
|<span data-ttu-id="e8130-193">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-193">Name</span></span>|<span data-ttu-id="e8130-194">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-194">Description</span></span>|<span data-ttu-id="e8130-195">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="e8130-196">find-and-replace</span></span>|<span data-ttu-id="e8130-197">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-197">Root element.</span></span>|<span data-ttu-id="e8130-198">예</span><span class="sxs-lookup"><span data-stu-id="e8130-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e8130-199">특성</span><span class="sxs-lookup"><span data-stu-id="e8130-199">Attributes</span></span>  
  
|<span data-ttu-id="e8130-200">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-200">Name</span></span>|<span data-ttu-id="e8130-201">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-201">Description</span></span>|<span data-ttu-id="e8130-202">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-202">Required</span></span>|<span data-ttu-id="e8130-203">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-204">from</span><span class="sxs-lookup"><span data-stu-id="e8130-204">from</span></span>|<span data-ttu-id="e8130-205">hello에 대 한 문자열 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-205">hello string toosearch for.</span></span>|<span data-ttu-id="e8130-206">예</span><span class="sxs-lookup"><span data-stu-id="e8130-206">Yes</span></span>|<span data-ttu-id="e8130-207">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-207">N/A</span></span>|  
|<span data-ttu-id="e8130-208">to</span><span class="sxs-lookup"><span data-stu-id="e8130-208">to</span></span>|<span data-ttu-id="e8130-209">hello 대체 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-209">hello replacement string.</span></span> <span data-ttu-id="e8130-210">빈 대체 문자열 tooremove hello 검색 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="e8130-211">예</span><span class="sxs-lookup"><span data-stu-id="e8130-211">Yes</span></span>|<span data-ttu-id="e8130-212">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-213">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-213">Usage</span></span>  
 <span data-ttu-id="e8130-214">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-215">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="e8130-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e8130-216">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-217"><a name="MaskURLSContent"></a> 콘텐츠의 URL 마스킹</span><span class="sxs-lookup"><span data-stu-id="e8130-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="e8130-218">hello `redirect-content-urls` toohello hello 게이트웨이 통해 동일한 링크를 가리키는지 있도록 정책 hello 응답 본문에 (마스킹) 링크를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="e8130-219">Hello outbound 섹션 toore 쓰기 응답 본문 링크 toomake의 해당 지점 toohello 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="e8130-220">Hello에서 사용 하 여 인바운드 반대의 결과 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="e8130-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e8130-221">이 정책은 `Location` 헤더와 같은 헤더 값을 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="e8130-222">toochange 헤더 값을 사용 하 여 hello [집합 헤더](api-management-transformation-policies.md#SetHTTPheader) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-223">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="e8130-224">예</span><span class="sxs-lookup"><span data-stu-id="e8130-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="e8130-225">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-225">Elements</span></span>  
  
|<span data-ttu-id="e8130-226">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-226">Name</span></span>|<span data-ttu-id="e8130-227">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-227">Description</span></span>|<span data-ttu-id="e8130-228">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="e8130-229">redirect-content-urls</span></span>|<span data-ttu-id="e8130-230">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-230">Root element.</span></span>|<span data-ttu-id="e8130-231">예</span><span class="sxs-lookup"><span data-stu-id="e8130-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-232">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-232">Usage</span></span>  
 <span data-ttu-id="e8130-233">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-234">**정책 섹션:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="e8130-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="e8130-235">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-236"><a name="SetBackendService"></a> 백 엔드 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="e8130-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="e8130-237">사용 하 여 hello `set-backend-service` 정책 tooredirect 들어오는 hello 해당 작업에 대 한 hello API 설정에 지정 된 것 보다 tooa 다른 백 엔드를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="e8130-238">이 정책은 hello 정책에 지정 된 hello 들어오는 요청 toohello의 hello 백 엔드 서비스 기준 URL을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-239">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="e8130-240">예제</span><span class="sxs-lookup"><span data-stu-id="e8130-240">Example</span></span>  
  
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
<span data-ttu-id="e8130-241">이 예제에서는 hello 집합 백 엔드 서비스 정책은 hello 하나에 지정 된 hello API 보다 hello 쿼리 문자열 tooa 다른 백 엔드 서비스에 전달 된 hello 버전 값에 따라 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="e8130-242">처음 hello 백 엔드 서비스 기준 URL hello API 설정에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="e8130-243">따라서 요청 URL을 hello `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` 됩니다 `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` 여기서 `http://contoso.com/api/10.4/` hello API 설정에 지정 된 hello 백 엔드 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="e8130-244">Hello 때 [< 선택\> ](api-management-advanced-policies.md#choose) 정책 문을 적용 hello 백 엔드 서비스 기준 URL 변경 될 수 있습니다 다시 하나 너무`http://contoso.com/api/8.2` 또는 `http://contoso.com/api/9.1`hello hello 버전 요청 쿼리 매개 변수 값에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="e8130-245">예를 들어 hello 값은 `"2013-15"` hello 최종 요청 URL은 `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="e8130-246">가 있으면 추가 hello 요청의 변환 하려는 경우에 다른 [변환 정책](api-management-transformation-policies.md#TransformationPolicies) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="e8130-247">예를 들어 tooremove hello 버전 쿼리 매개 변수 hello 요청 되 고 했으므로 라우팅된 tooa 버전별 백 엔드로, hello [쿼리 문자열 매개 변수를 설정](api-management-transformation-policies.md#SetQueryStringParameter) 정책을 사용 하는 tooremove hello 현재 중복 version 특성을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="e8130-248">예제</span><span class="sxs-lookup"><span data-stu-id="e8130-248">Example</span></span>  
  
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
<span data-ttu-id="e8130-249">이 예제에서는 hello 정책 경로 hello 요청 tooa 서비스 패브릭 백 엔드에 hello 파티션 키로 hello userId 쿼리 문자열을 사용 하 고 사용 하 여 hello 파티션의 주 복제본을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="e8130-250">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-250">Elements</span></span>  
  
|<span data-ttu-id="e8130-251">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-251">Name</span></span>|<span data-ttu-id="e8130-252">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-252">Description</span></span>|<span data-ttu-id="e8130-253">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="e8130-254">set-backend-service</span></span>|<span data-ttu-id="e8130-255">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-255">Root element.</span></span>|<span data-ttu-id="e8130-256">예</span><span class="sxs-lookup"><span data-stu-id="e8130-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e8130-257">특성</span><span class="sxs-lookup"><span data-stu-id="e8130-257">Attributes</span></span>  
  
|<span data-ttu-id="e8130-258">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-258">Name</span></span>|<span data-ttu-id="e8130-259">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-259">Description</span></span>|<span data-ttu-id="e8130-260">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-260">Required</span></span>|<span data-ttu-id="e8130-261">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-262">base-url</span><span class="sxs-lookup"><span data-stu-id="e8130-262">base-url</span></span>|<span data-ttu-id="e8130-263">새 백 엔드 서비스 기준 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-263">New backend service base URL.</span></span>|<span data-ttu-id="e8130-264">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-264">No</span></span>|<span data-ttu-id="e8130-265">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-265">N/A</span></span>|  
|<span data-ttu-id="e8130-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="e8130-266">backend-id</span></span>|<span data-ttu-id="e8130-267">hello 백 엔드 tooroute의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="e8130-268">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-268">No</span></span>|<span data-ttu-id="e8130-269">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-269">N/A</span></span>|  
|<span data-ttu-id="e8130-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="e8130-270">sf-partition-key</span></span>|<span data-ttu-id="e8130-271">Hello 백 엔드 서비스 패브릭 서비스에 있고 ' 백 엔드-i d '를 사용 하 여 지정 된 경우에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="e8130-272">Tooresolve hello 이름 확인 서비스에서 특정 파티션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="e8130-273">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-273">No</span></span>|<span data-ttu-id="e8130-274">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-274">N/A</span></span>|  
|<span data-ttu-id="e8130-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="e8130-275">sf-replica-type</span></span>|<span data-ttu-id="e8130-276">Hello 백 엔드 서비스 패브릭 서비스에 있고 ' 백 엔드-i d '를 사용 하 여 지정 된 경우에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="e8130-277">Hello 요청이 파티션의 toohello 기본 또는 보조 복제본을 전달 해야 하는 경우를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="e8130-278">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-278">No</span></span>|<span data-ttu-id="e8130-279">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-279">N/A</span></span>|    
|<span data-ttu-id="e8130-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="e8130-280">sf-resolve-condition</span></span>|<span data-ttu-id="e8130-281">Hello 백 엔드 서비스 패브릭 서비스는 때에 적용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="e8130-282">조건 식별 hello tooService 패브릭 백 엔드를 호출 하는 경우에 새로운 해결이 반복 toobe 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="e8130-283">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-283">No</span></span>|<span data-ttu-id="e8130-284">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-284">N/A</span></span>|    
|<span data-ttu-id="e8130-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="e8130-285">sf-service-instance-name</span></span>|<span data-ttu-id="e8130-286">Hello 백 엔드 서비스 패브릭 서비스는 때에 적용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="e8130-287">런타임 시 toochange 서비스 인스턴스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="e8130-288">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-288">No</span></span>|<span data-ttu-id="e8130-289">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="e8130-290">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-290">Usage</span></span>  
 <span data-ttu-id="e8130-291">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-292">**정책 섹션:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="e8130-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="e8130-293">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-294"><a name="SetBody"></a> 본문 설정</span><span class="sxs-lookup"><span data-stu-id="e8130-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="e8130-295">사용 하 여 hello `set-body` 들어오고 나가는 요청에 대 한 정책 tooset hello 메시지 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="e8130-296">tooaccess hello hello를 사용할 수 있습니다 메시지 본문 `context.Request.Body` 속성 또는 hello `context.Response.Body`hello 정책 hello 인지에 따라 인바운드 또는 아웃 바운드 섹션.</span><span class="sxs-lookup"><span data-stu-id="e8130-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e8130-297">액세스 하는 경우 기본적으로 사용 하 여 메시지 본문 hello는 `context.Request.Body` 또는 `context.Response.Body`, hello 원래 메시지 본문이 손실 되 고 hello 본문 hello 식에 다시 반환 하 여 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="e8130-298">toopreserve hello 본문 콘텐츠를 설정 hello `preserveContent` 매개 변수가 너무`true` hello 메시지에 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="e8130-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="e8130-299">경우 `preserveContent` 너무 설정`true` hello 본문 사용 되는 반환 된 다른 본문 hello 식에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="e8130-300">Hello 고려 사항 hello를 사용 하는 경우 다음 사항에 유의 하세요 `set-body` 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="e8130-301">Hello를 사용 하는 경우 `set-body` 정책 tooreturn tooset 않아도 새로운 또는 업데이트 된 본문 `preserveContent` 너무`true` hello 새 본문 콘텐츠를 명시적으로 제공 하는 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="e8130-302">Hello 인바운드 파이프라인에 대 한 응답의 hello 내용은 보존은 바람직하지 않습니다 응답이 아직 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="e8130-303">Hello 아웃 바운드 파이프라인에 있는 요청의 hello 내용은 보존은 바람직하지 않습니다 hello 요청이 이미 전송 되었습니다. toohello 백 엔드가 시점에서 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="e8130-304">인바운드 GET에서와 같이 메시지 본문이 없을 때 이 정책을 사용하면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="e8130-305">자세한 내용은 참조 hello `context.Request.Body`, `context.Response.Body`, hello 및 `IMessage` hello의 섹션 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables) 테이블 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-306">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="e8130-307">예</span><span class="sxs-lookup"><span data-stu-id="e8130-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="e8130-308">리터럴 텍스트 예제</span><span class="sxs-lookup"><span data-stu-id="e8130-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="e8130-309">문자열로 서 hello 본문에 액세스 하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="e8130-310">Note म hello 파이프라인의 뒷부분에 나오는 액세스할 수 있도록 hello 원래 요청 본문을 유지는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
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
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="e8130-311">Jobject 인 본문 hello를 액세스 하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="e8130-312">Hello 원래 요청 본문을 액세스 하면 예외가 발생 합니다 hello 파이프라인에 나중에 예약 되지 म 이후 note입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="e8130-313">제품 기준 응답 필터링</span><span class="sxs-lookup"><span data-stu-id="e8130-313">Filter response based on product</span></span>  
 <span data-ttu-id="e8130-314">이 예제에서는 어떻게 hello 응답에서 데이터 요소를 제거 하 여 tooperform 콘텐츠 필터링 서비스에서 받은 hello 백 엔드 hello를 사용 하는 경우 `Starter` 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="e8130-315">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too34:30 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="e8130-316">개요 31:50 toosee부터 시작 [어두운 Sky 예측 API hello](https://developer.forecast.io/) 이 데모에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="e8130-317">본문이 설정된 Liquid 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="e8130-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="e8130-318">hello `set-body` 정책 구성 된 toouse hello 수 [유동](https://shopify.github.io/liquid/basics/introduction/) 템플릿 언어 tootransfom hello 요청 또는 응답의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="e8130-319">메시지의 모양 변경 hello 형식 toocompletely 해야 할 경우에 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8130-320">hello에 사용 된 액체 구현의 hello `set-body` 정책 'C# 모드'에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="e8130-321">이러한 방식은 필터링과 같은 작업을 수행하는 경우에 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="e8130-322">예를 들어 파스칼 hello 사용 해야 날짜 필터를 사용 하 여 대/소문자와 C# 예: 서식을 날짜:</span><span class="sxs-lookup"><span data-stu-id="e8130-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="e8130-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="e8130-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8130-324">순서 toocorrectly 바인딩 tooan XML 본문에 hello 유동 템플릿을 사용 하 여 사용 하 여 한 `set-header` 정책 tooset Content-type tooeither 응용 프로그램/xml, 텍스트/x m l (또는 모든 끝나는 유형의 + xml); JSON 본문 있어야 응용 프로그램/json, json 텍스트 / (또는 모든 형식 종료 와 + json).</span><span class="sxs-lookup"><span data-stu-id="e8130-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="e8130-325">유동 템플릿을 사용 하 여 JSON tooSOAP 변환</span><span class="sxs-lookup"><span data-stu-id="e8130-325">Convert JSON tooSOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="e8130-326">Liquid 템플릿을 사용하여 JSON 변환</span><span class="sxs-lookup"><span data-stu-id="e8130-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="e8130-327">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-327">Elements</span></span>  
  
|<span data-ttu-id="e8130-328">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-328">Name</span></span>|<span data-ttu-id="e8130-329">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-329">Description</span></span>|<span data-ttu-id="e8130-330">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-331">set-body</span><span class="sxs-lookup"><span data-stu-id="e8130-331">set-body</span></span>|<span data-ttu-id="e8130-332">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-332">Root element.</span></span> <span data-ttu-id="e8130-333">Hello 본문 텍스트 또는 본문을 반환 하는 식을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="e8130-334">예</span><span class="sxs-lookup"><span data-stu-id="e8130-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="e8130-335">속성</span><span class="sxs-lookup"><span data-stu-id="e8130-335">Properties</span></span>  
  
|<span data-ttu-id="e8130-336">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-336">Name</span></span>|<span data-ttu-id="e8130-337">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-337">Description</span></span>|<span data-ttu-id="e8130-338">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-338">Required</span></span>|<span data-ttu-id="e8130-339">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-340">template</span><span class="sxs-lookup"><span data-stu-id="e8130-340">template</span></span>|<span data-ttu-id="e8130-341">Hello 본문 정책 설정 사용 되는 toochange hello 템플릿 모드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="e8130-342">현재 hello만 지원 값이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="e8130-343">-유동-hello 설정 본문 정책 hello 유동 템플릿 엔진을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="e8130-344">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-344">No</span></span>|<span data-ttu-id="e8130-345">liquid</span><span class="sxs-lookup"><span data-stu-id="e8130-345">liquid</span></span>|  

<span data-ttu-id="e8130-346">Hello 유동 템플릿을 hello 요청 및 응답에 대 한 정보에 액세스 하는 것에 대 한 다음과 같은 속성 hello로 tooa 컨텍스트 개체를 바인딩할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="e8130-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="e8130-347">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-347">Usage</span></span>  
 <span data-ttu-id="e8130-348">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-349">**정책 섹션:** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="e8130-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="e8130-350">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-351"><a name="SetHTTPheader"></a> HTTP 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="e8130-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="e8130-352">hello `set-header` 정책 값 tooan 기존 응답 및/또는 요청 헤더를 지정 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="e8130-353">HTTP 헤더 목록을 HTTP 메시지에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="e8130-354">인바운드 파이프라인에 배치 하는 경우이 정책은 toohello 대상 서비스에 전달 되 고 hello 요청에 대 한 hello HTTP 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="e8130-355">아웃 바운드 파이프라인에 배치 하는 경우이 정책은 toohello 게이트웨이 클라이언트에 전송 되는 hello 응답에 대 한 hello HTTP 헤더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-356">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="e8130-357">예</span><span class="sxs-lookup"><span data-stu-id="e8130-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="e8130-358">예제</span><span class="sxs-lookup"><span data-stu-id="e8130-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="e8130-359">컨텍스트 정보 toohello 백 엔드 서비스를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="e8130-360">이 예제는 hello API에서 tooapply 정책을 toosupply 컨텍스트 정보 toohello 백 엔드 서비스를 평준화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="e8130-361">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too10:30 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="e8130-362">12시 10분에는 데모 작업에서 hello 정책을 볼 수 있는 hello 개발자 포털에서 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="e8130-363">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8130-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="e8130-364">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-364">Elements</span></span>  
  
|<span data-ttu-id="e8130-365">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-365">Name</span></span>|<span data-ttu-id="e8130-366">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-366">Description</span></span>|<span data-ttu-id="e8130-367">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-368">set-header</span><span class="sxs-lookup"><span data-stu-id="e8130-368">set-header</span></span>|<span data-ttu-id="e8130-369">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-369">Root element.</span></span>|<span data-ttu-id="e8130-370">예</span><span class="sxs-lookup"><span data-stu-id="e8130-370">Yes</span></span>|  
|<span data-ttu-id="e8130-371">값</span><span class="sxs-lookup"><span data-stu-id="e8130-371">value</span></span>|<span data-ttu-id="e8130-372">Hello 헤더 toobe 집합의 hello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="e8130-373">이름이 같은 hello 가진 여러 헤더에 대 한 더 추가 `value` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="e8130-374">예</span><span class="sxs-lookup"><span data-stu-id="e8130-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="e8130-375">속성</span><span class="sxs-lookup"><span data-stu-id="e8130-375">Properties</span></span>  
  
|<span data-ttu-id="e8130-376">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-376">Name</span></span>|<span data-ttu-id="e8130-377">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-377">Description</span></span>|<span data-ttu-id="e8130-378">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-378">Required</span></span>|<span data-ttu-id="e8130-379">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="e8130-380">exists-action</span></span>|<span data-ttu-id="e8130-381">Hello 헤더가 이미 지정 되어 때 어떤 작업 tootake를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="e8130-382">이 특성 hello 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-383">-재정의할-hello 기존 헤더의 hello 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="e8130-384">-skip-기존 헤더 값 hello를 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="e8130-385">-추가-hello 값 toohello 기존 헤더 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="e8130-386">-delete-hello 요청에서 hello 헤더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="e8130-387">설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 헤더에 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="e8130-388">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-388">No</span></span>|<span data-ttu-id="e8130-389">override</span><span class="sxs-lookup"><span data-stu-id="e8130-389">override</span></span>|  
|<span data-ttu-id="e8130-390">name</span><span class="sxs-lookup"><span data-stu-id="e8130-390">name</span></span>|<span data-ttu-id="e8130-391">Hello 헤더 toobe 집합의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="e8130-392">예</span><span class="sxs-lookup"><span data-stu-id="e8130-392">Yes</span></span>|<span data-ttu-id="e8130-393">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-394">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-394">Usage</span></span>  
 <span data-ttu-id="e8130-395">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-396">**정책 섹션:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="e8130-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e8130-397">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-398"><a name="SetQueryStringParameter"></a> 쿼리 문자열 매개 변수 설정</span><span class="sxs-lookup"><span data-stu-id="e8130-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="e8130-399">hello `set-query-parameter` , 대체 값 정책 추가 또는 삭제 요청 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="e8130-400">사용 되는 toopass 쿼리 hello 백 엔드 서비스에서 예상 하는 매개 변수는 선택 사항 또는 hello 요청에 없는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-401">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="e8130-402">예</span><span class="sxs-lookup"><span data-stu-id="e8130-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="e8130-403">예제</span><span class="sxs-lookup"><span data-stu-id="e8130-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="e8130-404">컨텍스트 정보 toohello 백 엔드 서비스를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="e8130-405">이 예제는 hello API에서 tooapply 정책을 toosupply 컨텍스트 정보 toohello 백 엔드 서비스를 평준화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="e8130-406">구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too10:30 빨리 감기 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="e8130-407">12시 10분에는 데모 작업에서 hello 정책을 볼 수 있는 hello 개발자 포털에서 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="e8130-408">자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8130-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="e8130-409">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-409">Elements</span></span>  
  
|<span data-ttu-id="e8130-410">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-410">Name</span></span>|<span data-ttu-id="e8130-411">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-411">Description</span></span>|<span data-ttu-id="e8130-412">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="e8130-413">set-query-parameter</span></span>|<span data-ttu-id="e8130-414">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-414">Root element.</span></span>|<span data-ttu-id="e8130-415">예</span><span class="sxs-lookup"><span data-stu-id="e8130-415">Yes</span></span>|  
|<span data-ttu-id="e8130-416">값</span><span class="sxs-lookup"><span data-stu-id="e8130-416">value</span></span>|<span data-ttu-id="e8130-417">Hello 쿼리 매개 변수 toobe 집합의 hello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="e8130-418">이름이 같은 hello로 여러 쿼리 매개 변수에 대 한 더 추가 `value` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="e8130-419">예</span><span class="sxs-lookup"><span data-stu-id="e8130-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="e8130-420">속성</span><span class="sxs-lookup"><span data-stu-id="e8130-420">Properties</span></span>  
  
|<span data-ttu-id="e8130-421">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-421">Name</span></span>|<span data-ttu-id="e8130-422">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-422">Description</span></span>|<span data-ttu-id="e8130-423">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-423">Required</span></span>|<span data-ttu-id="e8130-424">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="e8130-425">exists-action</span></span>|<span data-ttu-id="e8130-426">Hello 쿼리 매개 변수가 이미 지정한 경우에 어떤 작업 tootake를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="e8130-427">이 특성 hello 다음 값 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="e8130-428">-재정의-hello 기존 매개 변수 대체 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="e8130-429">-skip-기존 hello 쿼리 매개 변수 값을 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="e8130-430">-추가-hello 값 toohello 기존 쿼리 매개 변수 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="e8130-431">-delete-hello 요청에서 hello 쿼리 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="e8130-432">설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 쿼리 매개 변수에서 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="e8130-433">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-433">No</span></span>|<span data-ttu-id="e8130-434">override</span><span class="sxs-lookup"><span data-stu-id="e8130-434">override</span></span>|  
|<span data-ttu-id="e8130-435">name</span><span class="sxs-lookup"><span data-stu-id="e8130-435">name</span></span>|<span data-ttu-id="e8130-436">Hello 쿼리 매개 변수 toobe 집합의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="e8130-437">예</span><span class="sxs-lookup"><span data-stu-id="e8130-437">Yes</span></span>|<span data-ttu-id="e8130-438">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-439">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-439">Usage</span></span>  
 <span data-ttu-id="e8130-440">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-441">**정책 섹션:** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="e8130-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="e8130-442">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-443"><a name="RewriteURL"></a> URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="e8130-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="e8130-444">hello `rewrite-uri` 정책 hello 다음 예제와 같이 hello 웹 서비스에서 공용 형식 toohello 형식에서 요청 URL을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="e8130-445">공용 URL - `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="e8130-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="e8130-446">요청 URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="e8130-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="e8130-447">이 정책은 hello 웹 서비스에 필요한 hello URL 형식으로 변환 해야 하는 사용자 및/또는 브라우저에 친숙 한 URL 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="e8130-448">이 정책은 toobe 클린 Url, RESTful Url, 사용자에 게 친숙 한 Url 또는 SEO에 게 친숙 한 Url을 쿼리 문자열을 포함 하지 않으며 대신 hello의만 hello 경로 포함 하는 등의 다른 URL 형식으로 노출 하는 경우 적용 필요 hello 체계 및 기관 hello) (이후 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="e8130-449">보통 미학, 사용 편의성 또는 SEO(검색 엔진 최적화)를 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e8130-450">만 hello 정책을 사용 하 여 쿼리 문자열 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="e8130-451">추가 템플릿 경로 매개 변수 hello에 URL 재작성을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="e8130-452">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="e8130-453">예</span><span class="sxs-lookup"><span data-stu-id="e8130-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="e8130-454">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-454">Elements</span></span>  
  
|<span data-ttu-id="e8130-455">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-455">Name</span></span>|<span data-ttu-id="e8130-456">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-456">Description</span></span>|<span data-ttu-id="e8130-457">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="e8130-458">rewrite-uri</span></span>|<span data-ttu-id="e8130-459">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-459">Root element.</span></span>|<span data-ttu-id="e8130-460">예</span><span class="sxs-lookup"><span data-stu-id="e8130-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e8130-461">특성</span><span class="sxs-lookup"><span data-stu-id="e8130-461">Attributes</span></span>  
  
|<span data-ttu-id="e8130-462">특성</span><span class="sxs-lookup"><span data-stu-id="e8130-462">Attribute</span></span>|<span data-ttu-id="e8130-463">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-463">Description</span></span>|<span data-ttu-id="e8130-464">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-464">Required</span></span>|<span data-ttu-id="e8130-465">기본값</span><span class="sxs-lookup"><span data-stu-id="e8130-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="e8130-466">template</span><span class="sxs-lookup"><span data-stu-id="e8130-466">template</span></span>|<span data-ttu-id="e8130-467">쿼리 문자열 매개 변수와 hello 실제 웹 서비스 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="e8130-468">식을 사용 하는 경우 hello 전체 값 식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="e8130-469">예</span><span class="sxs-lookup"><span data-stu-id="e8130-469">Yes</span></span>|<span data-ttu-id="e8130-470">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8130-470">N/A</span></span>|  
|<span data-ttu-id="e8130-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="e8130-471">copy-unmatched-params</span></span>|<span data-ttu-id="e8130-472">Toohello URL hello에 정의 된 서식 파일을 다시 작성 hello 원본 URL 서식 파일에 없는 hello 들어오는 요청의 쿼리 매개 변수가 추가 되는지 여부를 지정합니다</span><span class="sxs-lookup"><span data-stu-id="e8130-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="e8130-473">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-473">No</span></span>|<span data-ttu-id="e8130-474">true</span><span class="sxs-lookup"><span data-stu-id="e8130-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-475">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-475">Usage</span></span>  
 <span data-ttu-id="e8130-476">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-477">**정책 섹션:** inbound</span><span class="sxs-lookup"><span data-stu-id="e8130-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e8130-478">**정책 범위:** product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="e8130-479"><a name="XSLTransform"></a> XSLT를 사용하여 XML 변환</span><span class="sxs-lookup"><span data-stu-id="e8130-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="e8130-480">hello `Transform XML using an XSLT` 정책은 XSL 변환을 tooXML hello 요청 또는 응답 본문에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e8130-481">정책 문</span><span class="sxs-lookup"><span data-stu-id="e8130-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="e8130-482">예</span><span class="sxs-lookup"><span data-stu-id="e8130-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e8130-483">요소</span><span class="sxs-lookup"><span data-stu-id="e8130-483">Elements</span></span>  
  
|<span data-ttu-id="e8130-484">이름</span><span class="sxs-lookup"><span data-stu-id="e8130-484">Name</span></span>|<span data-ttu-id="e8130-485">설명</span><span class="sxs-lookup"><span data-stu-id="e8130-485">Description</span></span>|<span data-ttu-id="e8130-486">필수</span><span class="sxs-lookup"><span data-stu-id="e8130-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e8130-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="e8130-487">xsl-transform</span></span>|<span data-ttu-id="e8130-488">루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-488">Root element.</span></span>|<span data-ttu-id="e8130-489">예</span><span class="sxs-lookup"><span data-stu-id="e8130-489">Yes</span></span>|  
|<span data-ttu-id="e8130-490">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e8130-490">parameter</span></span>|<span data-ttu-id="e8130-491">Hello 변환에서 사용 되는 사용 되는 toodefine 변수</span><span class="sxs-lookup"><span data-stu-id="e8130-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="e8130-492">아니요</span><span class="sxs-lookup"><span data-stu-id="e8130-492">No</span></span>|  
|<span data-ttu-id="e8130-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="e8130-493">xsl:stylesheet</span></span>|<span data-ttu-id="e8130-494">루트 스타일시트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-494">Root stylesheet element.</span></span> <span data-ttu-id="e8130-495">모든 요소와 특성 내에 정의 된 hello 표준에 따라 [XSLT 사양](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="e8130-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="e8130-496">예</span><span class="sxs-lookup"><span data-stu-id="e8130-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e8130-497">사용</span><span class="sxs-lookup"><span data-stu-id="e8130-497">Usage</span></span>  
 <span data-ttu-id="e8130-498">이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8130-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e8130-499">**정책 섹션:** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="e8130-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="e8130-500">**정책 범위:** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="e8130-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="e8130-501">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8130-501">Next steps</span></span>
<span data-ttu-id="e8130-502">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8130-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
