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
# <a name="azure-api-management-policy-reference"></a>Azure API 관리 정책 참조
이 섹션에서는 hello에 hello 정책에 대 한 인덱스를 제공 [API 관리 정책 참조][API Management policy reference]합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API Management 정책][Policies in API Management]을 참조하세요.

정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다. Hello와 같은 일부 정책은 [제어 흐름] [ Control flow] 및 [변수 설정] [ Set variable] 정책은 정책 식을 기반으로 합니다. 자세한 내용은 [고급 정책][Advanced policies] 및 [정책 식][Policy expressions]을 참조하세요.

## <a name="policy-reference-index"></a>정책 참조 인덱스
* [액세스 제한 정책][Access restriction policies]
  * [HTTP 헤더 확인][Check HTTP header] - HTTP 헤더의 존재 및/또는 값을 적용합니다.
  * [구독으로 호출 속도 제한][Limit call rate by subscription] - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.
  * [키로 호출 속도 제한](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.
  * [호출자 IP 제한][Restrict caller IPs] - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.
  * [구독에 의해 할당량 설정] [ Set usage quota by subscription] -구독 별로에서 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 허용 합니다.
  * [키로 할당량 설정](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -당 키 단위로 허용 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 지정 합니다.
  * [JWT 유효성 검사][Validate JWT] - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.
* [고급 정책][Advanced policies]
  * [제어 흐름] [ Control flow] -조건부로 hello 부울의 hello 평가 결과에 따라 정책 문을 적용 [식][expressions]합니다.
  * [요청 전달] [ Forward request] -hello 요청 toohello 백 엔드 서비스에 전달 합니다.
  * [허브 tooEvent 로그] [ Log tooEvent Hub] -에 정의 된 hello 지정 된 형식 tooa 메시지 대상에 메시지를 보냅니다는 [로 거](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) 엔터티.
  * [다시 시도](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -hello 재시도 실행 고 hello 조건이 충족 될 때까지 정책 문을 포함 합니다. 지정 된 시간 간격을 hello 및 다시 시도 횟수를 지정 하는 toohello 실행에서 반복 됩니다.
  * [응답을 반환](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -지정 된 지시 파일 중단 파이프라인 실행 및 반환 hello 직접 toohello 호출자입니다.
  * [한 가지 방법은 요청 보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -요청 toohello 지정한 URL 응답을 받기 위해 대기 하지 않고 보냅니다.
  * [요청 보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -요청 toohello 지정한 URL을 보냅니다.
  * [요청 하는 방법을 설정](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -toochange hello HTTP 메서드는 요청에 대 한 있습니다.
  * [상태 설정](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -변경 hello HTTP 상태 코드 toohello 값을 지정 합니다.
  * [변수 설정][Set variable] - 나중에 액세스할 수 있도록 명명된 [context][context] 변수의 값을 유지합니다.
  * [추적](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -hello에 문자열을 추가 [API 검사기](api-management-howto-api-inspector.md) 출력 합니다.
  * [대기](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) -캐시에서 값을 가져올 괄호로 묶은 송신 대기 요청 하거나 계속 진행 하기 전에 정책 toocomplete 흐름을 제어 합니다.
* [인증 정책][Authentication policies]
  * [기본 사용 인증][Authenticate with Basic] - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.
  * [클라이언트 인증서 사용 인증][Authenticate with client certificate] - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.
* [캐싱 정책][Caching policies] 
  * [캐시에서 가져오기][Get from cache] - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.
  * [Toocache 저장] [ Store toocache] -toohello에 따라 캐시 응답 캐시 제어 구성을 지정 합니다.
  * [캐시에서 값 가져오기](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.
  * [값을 캐시에 저장](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -hello 캐시에 항목을 키로 저장 합니다.
  * [캐시에서 값을 제거](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -키별로 hello 캐시에 항목을 제거 합니다.
* [도메인 간 정책][Cross domain policies] 
  * [도메인 간 호출을 허용] [ Allow cross-domain calls] -Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 hello API에 액세스할 수 있게 합니다.
  * [CORS] [ CORS] -브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 또는 tooan 작업을 지원 크로스-원본 자원 공유 (CORS)를 추가 합니다.
  * [JSONP] [ JSONP] -JSON with padding (JSONP) 지원 tooan 작업이 추가 하거나는 API tooallow 도메인 간 JavaScript 브라우저 기반 클라이언트에서 호출 합니다.
* [변환 정책][Transformation policies] 
  * [JSON tooXML 변환] [ Convert JSON tooXML] -요청으로 변환 하거나 JSON tooXML에서 응답 본문입니다.
  * [XML tooJSON 변환] [ Convert XML tooJSON] -변환 요청 또는 응답 본문에서 XML tooJSON 합니다.
  * [본문 문자열 찾기 및 바꾸기][Find and replace string in body] - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.
  * [콘텐츠의 Url 마스킹] [ Mask URLs in content] -다시 작성 (마스킹) 링크 hello에 대 한 응답 본문 toohello hello 게이트웨이 통해 동일한 링크를 가리킵니다.
  * [백 엔드 서비스 설정] [ Set backend service] -들어오는 요청에 대 한 hello 백 엔드 서비스를 변경 합니다.
  * [본문 설정] [ Set body] -들어오는 요청과 나가는 요청에 대 한 hello 메시지 본문을 설정 합니다.
  * [HTTP 헤더 설정] [ Set HTTP header] -값 tooan 기존 응답 및/또는 요청 헤더를 할당 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.
  * [쿼리 문자열 매개 변수 설정][Set query string parameter] - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.
  * [URL 재작성] [ Rewrite URL] -요청 URL hello 웹 서비스에서 공용 형식 toohello 형식에서 변환 합니다.

## <a name="next-steps"></a>다음 단계
정책 식에 대 한 자세한 내용은 hello 다음 비디오를 참조 하세요.

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


