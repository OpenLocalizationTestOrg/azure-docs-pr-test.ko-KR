---
title: "API 관리 정책 aaaAzure | Microsoft Docs"
description: "Azure API 관리에 사용할 수 있는 hello 정책에 알아봅니다."
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="6a6c2-103">API 관리 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-103">API Management policies</span></span>
<span data-ttu-id="6a6c2-104">이 섹션에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="6a6c2-105">정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="6a6c2-106">정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 hello 시스템의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="6a6c2-107">정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="6a6c2-108">인기 있는 문은 XML tooJSON에서 형식 변환을 포함 하 고 호출 toorestrict hello 양을 개발자 로부터 들어오는 호출 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="6a6c2-109">더 많은 정책을 hello 상자 바로 사용할 수 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="6a6c2-110">정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="6a6c2-111">Hello와 같은 일부 정책은 [제어 흐름](api-management-advanced-policies.md#choose) 및 [변수 설정](api-management-advanced-policies.md#set-variable) 정책은 정책 식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="6a6c2-112">자세한 내용은 [고급 정책](api-management-advanced-policies.md#AdvancedPolicies) 및 [정책 식](api-management-policy-expressions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="6a6c2-113"><a name="ProxyPolicies"></a> 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="6a6c2-114">액세스 제한 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="6a6c2-115">[HTTP 헤더 확인](api-management-access-restriction-policies.md#CheckHTTPHeader) - HTTP 헤더의 존재 및/또는 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="6a6c2-116">[구독으로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRate) - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="6a6c2-117">[키로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="6a6c2-118">[호출자 IP 제한](api-management-access-restriction-policies.md#RestrictCallerIPs) - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="6a6c2-119">[구독에 의해 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuota) -구독 별로에서 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="6a6c2-120">[키로 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -당 키 단위로 허용 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="6a6c2-121">[JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="6a6c2-122">고급 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="6a6c2-123">[제어 흐름](api-management-advanced-policies.md#choose) 조건부로-부울 표현식의 hello 평가에 따라 정책 문을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="6a6c2-124">[요청 전달](api-management-advanced-policies.md#ForwardRequest) -hello 요청 toohello 백 엔드 서비스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="6a6c2-125">[허브 tooEvent 로그](api-management-advanced-policies.md#log-to-eventhub) -는 거 엔터티에 의해 정의 된 hello 지정 된 형식 tooa 메시지 대상에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="6a6c2-126">[다시 시도](api-management-advanced-policies.md#Retry) -hello 재시도 실행 고 hello 조건이 충족 될 때까지 정책 문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="6a6c2-127">지정 된 시간 간격을 hello 및 다시 시도 횟수를 지정 하는 toohello 실행에서 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="6a6c2-128">[응답을 반환](api-management-advanced-policies.md#ReturnResponse) -지정 된 지시 파일 중단 파이프라인 실행 및 반환 hello 직접 toohello 호출자입니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="6a6c2-129">[한 가지 방법은 요청 보내기](api-management-advanced-policies.md#SendOneWayRequest) -요청 toohello 지정한 URL 응답을 받기 위해 대기 하지 않고 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="6a6c2-130">[요청 보내기](api-management-advanced-policies.md#SendRequest) -요청 toohello 지정한 URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="6a6c2-131">[변수 설정](api-management-advanced-policies.md#set-variable) - 나중에 액세스할 수 있도록 명명된 context 변수의 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="6a6c2-132">[요청 하는 방법을 설정](api-management-advanced-policies.md#SetRequestMethod) -toochange hello HTTP 메서드는 요청에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="6a6c2-133">[상태 코드를 설정](api-management-advanced-policies.md#SetStatus) -변경 hello HTTP 상태 코드 toohello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="6a6c2-134">[추적](api-management-advanced-policies.md#Trace) -hello에 문자열을 추가 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="6a6c2-135">[대기](api-management-advanced-policies.md#Wait) -묶인 때까지 대기 [보내기 요청](api-management-advanced-policies.md#SendRequest), [캐시에서 값을 가져올](api-management-caching-policies.md#GetFromCacheByKey), 또는 [제어 흐름](api-management-advanced-policies.md#choose) 계속 진행 하기 전에 정책 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="6a6c2-136">인증 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="6a6c2-137">[기본 사용 인증](api-management-authentication-policies.md#Basic) - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="6a6c2-138">[클라이언트 인증서 사용 인증](api-management-authentication-policies.md#ClientCertificate) - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="6a6c2-139">캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="6a6c2-140">[캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="6a6c2-141">[Toocache 저장](api-management-caching-policies.md#StoreToCache) -toohello에 따라 캐시 응답 캐시 제어 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="6a6c2-142">[캐시에서 값 가져오기](api-management-caching-policies.md#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="6a6c2-143">[값을 캐시에 저장](api-management-caching-policies.md#StoreToCacheByKey) -hello 캐시에 항목을 키로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="6a6c2-144">[캐시에서 값을 제거](api-management-caching-policies.md#RemoveCacheByKey) -키별로 hello 캐시에 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="6a6c2-145">도메인 간 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="6a6c2-146">[도메인 간 호출을 허용](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 hello API에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="6a6c2-147">[CORS](api-management-cross-domain-policies.md#CORS) -브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 또는 tooan 작업을 지원 크로스-원본 자원 공유 (CORS)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="6a6c2-148">[JSONP](api-management-cross-domain-policies.md#JSONP) -JSON with padding (JSONP) 지원 tooan 작업이 추가 하거나는 API tooallow 도메인 간 JavaScript 브라우저 기반 클라이언트에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="6a6c2-149">변환 정책</span><span class="sxs-lookup"><span data-stu-id="6a6c2-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="6a6c2-150">[JSON tooXML 변환](api-management-transformation-policies.md#ConvertJSONtoXML) -요청으로 변환 하거나 JSON tooXML에서 응답 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="6a6c2-151">[XML tooJSON 변환](api-management-transformation-policies.md#ConvertXMLtoJSON) -변환 요청 또는 응답 본문에서 XML tooJSON 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="6a6c2-152">[본문 문자열 찾기 및 바꾸기](api-management-transformation-policies.md#Findandreplacestringinbody) - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="6a6c2-153">[콘텐츠의 Url 마스킹](api-management-transformation-policies.md#MaskURLSContent) -다시 작성 (마스킹) 링크 hello에 대 한 응답 본문 toohello hello 게이트웨이 통해 동일한 링크를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="6a6c2-154">[백 엔드 서비스 설정](api-management-transformation-policies.md#SetBackendService) -들어오는 요청에 대 한 hello 백 엔드 서비스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="6a6c2-155">[본문 설정](api-management-transformation-policies.md#SetBody) -들어오는 요청과 나가는 요청에 대 한 hello 메시지 본문을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="6a6c2-156">[HTTP 헤더 설정](api-management-transformation-policies.md#SetHTTPheader) -값 tooan 기존 응답 및/또는 요청 헤더를 할당 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="6a6c2-157">[쿼리 문자열 매개 변수 설정](api-management-transformation-policies.md#SetQueryStringParameter) - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="6a6c2-158">[URL 재작성](api-management-transformation-policies.md#RewriteURL) -요청 URL hello 웹 서비스에서 공용 형식 toohello 형식에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="6a6c2-159">[XSLT를 사용 하 여 XML 변형](api-management-transformation-policies.md#XSLTransform) -는 XSL 변환을 tooXML hello 요청 또는 응답 본문에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="6a6c2-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a6c2-160">Next steps</span></span>
<span data-ttu-id="6a6c2-161">정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a6c2-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
