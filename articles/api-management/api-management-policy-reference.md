---
title: "aaaAzure API 관리 정책 참조"
description: "Hello 정책 사용할 수 있는 tooconfigure API 관리에 알아봅니다."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="0fee9-103">Azure API 관리 정책 참조</span><span class="sxs-lookup"><span data-stu-id="0fee9-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="0fee9-104">이 섹션에서는 hello에 hello 정책에 대 한 인덱스를 제공 [API 관리 정책 참조][API Management policy reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="0fee9-105">정책의 추가 및 구성에 대한 자세한 내용은 [API Management 정책][Policies in API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fee9-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="0fee9-106">정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="0fee9-107">Hello와 같은 일부 정책은 [제어 흐름] [ Control flow] 및 [변수 설정] [ Set variable] 정책은 정책 식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="0fee9-108">자세한 내용은 [고급 정책][Advanced policies] 및 [정책 식][Policy expressions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fee9-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="0fee9-109">정책 참조 인덱스</span><span class="sxs-lookup"><span data-stu-id="0fee9-109">Policy reference index</span></span>
* <span data-ttu-id="0fee9-110">[액세스 제한 정책][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="0fee9-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="0fee9-111">[HTTP 헤더 확인][Check HTTP header] - HTTP 헤더의 존재 및/또는 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="0fee9-112">[구독으로 호출 속도 제한][Limit call rate by subscription] - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="0fee9-113">[키로 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="0fee9-114">[호출자 IP 제한][Restrict caller IPs] - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="0fee9-115">[구독에 의해 할당량 설정] [ Set usage quota by subscription] -구독 별로에서 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="0fee9-116">[키로 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -당 키 단위로 허용 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="0fee9-117">[JWT 유효성 검사][Validate JWT] - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="0fee9-118">[고급 정책][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="0fee9-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="0fee9-119">[제어 흐름] [ Control flow] -조건부로 hello 부울의 hello 평가 결과에 따라 정책 문을 적용 [식][expressions]합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="0fee9-120">[요청 전달] [ Forward request] -hello 요청 toohello 백 엔드 서비스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="0fee9-121">[허브 tooEvent 로그] [ Log tooEvent Hub] -에 정의 된 hello 지정 된 형식 tooa 메시지 대상에 메시지를 보냅니다는 [로 거](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) 엔터티.</span><span class="sxs-lookup"><span data-stu-id="0fee9-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="0fee9-122">[다시 시도](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -hello 재시도 실행 고 hello 조건이 충족 될 때까지 정책 문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="0fee9-123">지정 된 시간 간격을 hello 및 다시 시도 횟수를 지정 하는 toohello 실행에서 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="0fee9-124">[응답을 반환](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -지정 된 지시 파일 중단 파이프라인 실행 및 반환 hello 직접 toohello 호출자입니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="0fee9-125">[한 가지 방법은 요청 보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -요청 toohello 지정한 URL 응답을 받기 위해 대기 하지 않고 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="0fee9-126">[요청 보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -요청 toohello 지정한 URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="0fee9-127">[요청 하는 방법을 설정](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -toochange hello HTTP 메서드는 요청에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="0fee9-128">[상태 설정](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -변경 hello HTTP 상태 코드 toohello 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="0fee9-129">[변수 설정][Set variable] - 나중에 액세스할 수 있도록 명명된 [context][context] 변수의 값을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="0fee9-130">[추적](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -hello에 문자열을 추가 [API 검사기](api-management-howto-api-inspector.md) 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="0fee9-131">[대기](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) -캐시에서 값을 가져올 괄호로 묶은 송신 대기 요청 하거나 계속 진행 하기 전에 정책 toocomplete 흐름을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="0fee9-132">[인증 정책][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="0fee9-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="0fee9-133">[기본 사용 인증][Authenticate with Basic] - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="0fee9-134">[클라이언트 인증서 사용 인증][Authenticate with client certificate] - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="0fee9-135">[캐싱 정책][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="0fee9-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="0fee9-136">[캐시에서 가져오기][Get from cache] - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="0fee9-137">[Toocache 저장] [ Store toocache] -toohello에 따라 캐시 응답 캐시 제어 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="0fee9-138">[캐시에서 값 가져오기](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="0fee9-139">[값을 캐시에 저장](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -hello 캐시에 항목을 키로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="0fee9-140">[캐시에서 값을 제거](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -키별로 hello 캐시에 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="0fee9-141">[도메인 간 정책][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="0fee9-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="0fee9-142">[도메인 간 호출을 허용] [ Allow cross-domain calls] -Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 hello API에 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="0fee9-143">[CORS] [ CORS] -브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 또는 tooan 작업을 지원 크로스-원본 자원 공유 (CORS)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="0fee9-144">[JSONP] [ JSONP] -JSON with padding (JSONP) 지원 tooan 작업이 추가 하거나는 API tooallow 도메인 간 JavaScript 브라우저 기반 클라이언트에서 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="0fee9-145">[변환 정책][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="0fee9-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="0fee9-146">[JSON tooXML 변환] [ Convert JSON tooXML] -요청으로 변환 하거나 JSON tooXML에서 응답 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="0fee9-147">[XML tooJSON 변환] [ Convert XML tooJSON] -변환 요청 또는 응답 본문에서 XML tooJSON 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="0fee9-148">[본문 문자열 찾기 및 바꾸기][Find and replace string in body] - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="0fee9-149">[콘텐츠의 Url 마스킹] [ Mask URLs in content] -다시 작성 (마스킹) 링크 hello에 대 한 응답 본문 toohello hello 게이트웨이 통해 동일한 링크를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="0fee9-150">[백 엔드 서비스 설정] [ Set backend service] -들어오는 요청에 대 한 hello 백 엔드 서비스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="0fee9-151">[본문 설정] [ Set body] -들어오는 요청과 나가는 요청에 대 한 hello 메시지 본문을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="0fee9-152">[HTTP 헤더 설정] [ Set HTTP header] -값 tooan 기존 응답 및/또는 요청 헤더를 할당 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="0fee9-153">[쿼리 문자열 매개 변수 설정][Set query string parameter] - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="0fee9-154">[URL 재작성] [ Rewrite URL] -요청 URL hello 웹 서비스에서 공용 형식 toohello 형식에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fee9-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fee9-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0fee9-155">Next steps</span></span>
<span data-ttu-id="0fee9-156">정책 식에 대 한 자세한 내용은 hello 다음 비디오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0fee9-156">For more information on policy expressions, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


