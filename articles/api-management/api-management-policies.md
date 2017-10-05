---
title: "Azure API Management 정책 | Microsoft Docs"
description: "Azure API Management에 사용할 수 있는 정책에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="5a97a-103">API 관리 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-103">API Management policies</span></span>
<span data-ttu-id="5a97a-104">이 섹션에서는 다음 API Management 정책에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="5a97a-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a97a-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="5a97a-106">정책은 게시자가 구성을 통해 API 동작을 변경할 수 있도록 하는 시스템의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="5a97a-107">정책은 API의 요청이나 응답에 따라 순차적으로 실행되는 명령문의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="5a97a-108">많이 사용되는 명령문에는 XML에서 JSON으로 형식 변환, 개발자로부터 들어오는 호출의 양을 제한하는 호출 비율 제한 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="5a97a-109">다양한 다른 정책도 바로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="5a97a-110">정책이 다르게 지정하지 않는 한 정책 식은 어떤 API 관리 정책에서든 특성 값 또는 텍스트 값으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="5a97a-111">[제어 흐름](api-management-advanced-policies.md#choose) 및 [변수 설정](api-management-advanced-policies.md#set-variable) 정책 등의 일부 정책은 정책 식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="5a97a-112">자세한 내용은 [고급 정책](api-management-advanced-policies.md#AdvancedPolicies) 및 [정책 식](api-management-policy-expressions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a97a-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="5a97a-113"><a name="ProxyPolicies"></a> 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="5a97a-114">액세스 제한 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="5a97a-115">[HTTP 헤더 확인](api-management-access-restriction-policies.md#CheckHTTPHeader) - HTTP 헤더의 존재 및/또는 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="5a97a-116">[구독으로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRate) - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="5a97a-117">[키로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="5a97a-118">[호출자 IP 제한](api-management-access-restriction-policies.md#RestrictCallerIPs) - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="5a97a-119">[구독으로 사용 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuota) - 구독을 기준으로 갱신 가능 또는 수명 호출 볼륨 및/또는 대역폭 할당량을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="5a97a-120">[키로 사용 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - 키를 기준으로 갱신 가능 또는 수명 호출 볼륨 및/또는 대역폭 할당량을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="5a97a-121">[JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="5a97a-122">고급 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="5a97a-123">[제어 흐름](api-management-advanced-policies.md#choose) - 부울 식의 평가 결과에 따라 정책 문을 조건부로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="5a97a-124">[요청 전달](api-management-advanced-policies.md#ForwardRequest) - 백 엔드 서비스에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="5a97a-125">[이벤트 허브에 기록](api-management-advanced-policies.md#log-to-eventhub) - 로거 엔터티가 정의한 메시지 대상에 지정된 형식으로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="5a97a-126">[다시 시도](api-management-advanced-policies.md#Retry) - 조건이 충족될 때까지 포함된 정책 문을 실행하도록 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="5a97a-127">실행은 지정된 시간 간격으로 최대 지정된 재시도 횟수까지 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="5a97a-128">[응답 반환](api-management-advanced-policies.md#ReturnResponse) - 파이프라인 실행을 중단하고 호출자에게 직접 지정된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="5a97a-129">[단방향 요청 전송](api-management-advanced-policies.md#SendOneWayRequest) - 지정된 URL에 대한 응답을 기다리지 않고 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="5a97a-130">[요청 전송](api-management-advanced-policies.md#SendRequest) - 지정된 URL로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="5a97a-131">[변수 설정](api-management-advanced-policies.md#set-variable) - 나중에 액세스할 수 있도록 명명된 context 변수의 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="5a97a-132">[요청 메서드 설정](api-management-advanced-policies.md#SetRequestMethod) - 요청에 대한 HTTP 메서드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="5a97a-133">[상태 코드 설정](api-management-advanced-policies.md#SetStatus) - 지정된 값으로 HTTP 상태 코드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="5a97a-134">[추적](api-management-advanced-policies.md#Trace) - [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력에 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="5a97a-135">[대기](api-management-advanced-policies.md#Wait) - 계속하기 전에 완료할 포함된 [요청 전송](api-management-advanced-policies.md#SendRequest), [캐시에서 값 가져오기](api-management-caching-policies.md#GetFromCacheByKey) 또는 [흐름 제어](api-management-advanced-policies.md#choose) 정책 등을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="5a97a-136">인증 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="5a97a-137">[기본 사용 인증](api-management-authentication-policies.md#Basic) - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="5a97a-138">[클라이언트 인증서 사용 인증](api-management-authentication-policies.md#ClientCertificate) - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="5a97a-139">캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="5a97a-140">[캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="5a97a-141">[캐시에 저장](api-management-caching-policies.md#StoreToCache) - 지정된 캐시 제어 구성에 따라 응답을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="5a97a-142">[캐시에서 값 가져오기](api-management-caching-policies.md#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="5a97a-143">[값을 캐시에 저장](api-management-caching-policies.md#StoreToCacheByKey) - 키로 캐시에 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="5a97a-144">[캐시에서 값을 제거](api-management-caching-policies.md#RemoveCacheByKey) - 키로 캐시에서 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="5a97a-145">도메인 간 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="5a97a-146">[도메인 간 호출 허용](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - API를 Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="5a97a-147">[CORS](api-management-cross-domain-policies.md#CORS) - CORS(Cross-Origin Resource Sharing) 지원을 작업 또는 API에 추가하여 브라우저 기반 클라이언트의 도메인 간 호출을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="5a97a-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - 패딩이 있는 JSON(JSONP) 지원을 작업 또는 API에 추가하여 JavaScript 브라우저 기반 클라이언트의 도메인 간 호출을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="5a97a-149">변환 정책</span><span class="sxs-lookup"><span data-stu-id="5a97a-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="5a97a-150">[XML로 JSON 변환](api-management-transformation-policies.md#ConvertJSONtoXML) - 요청 또는 응답 본문을 JSON에서 XML로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="5a97a-151">[JSON으로 XML 변환](api-management-transformation-policies.md#ConvertXMLtoJSON) - 요청 또는 응답 본문을 XML에서 JSON으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="5a97a-152">[본문 문자열 찾기 및 바꾸기](api-management-transformation-policies.md#Findandreplacestringinbody) - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="5a97a-153">[콘텐츠의 URL 마스킹](api-management-transformation-policies.md#MaskURLSContent) - 응답 본문의 링크를 다시 써서(마스킹) 게이트웨이를 통해 동일한 링크를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="5a97a-154">[백 엔드 서비스 설정](api-management-transformation-policies.md#SetBackendService) - 들어오는 요청의 백 엔드 서비스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="5a97a-155">[본문 설정](api-management-transformation-policies.md#SetBody) -들어오고 나가는 요청의 메시지 본문을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="5a97a-156">[HTTP 헤더 설정](api-management-transformation-policies.md#SetHTTPheader) - 기존 응답 및/또는 요청 헤더에 값을 할당하거나 새로운 응답 및/또는 요청 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="5a97a-157">[쿼리 문자열 매개 변수 설정](api-management-transformation-policies.md#SetQueryStringParameter) - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="5a97a-158">[URL 다시 쓰기](api-management-transformation-policies.md#RewriteURL) - 요청 URL을 공용 양식에서 웹 서비스에 필요한 양식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="5a97a-159">[XSLT를 사용하여 XML 변환](api-management-transformation-policies.md#XSLTransform) - 요청 또는 응답 본문의 XML에 XSL 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a97a-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="5a97a-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a97a-160">Next steps</span></span>
<span data-ttu-id="5a97a-161">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a97a-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
