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
# <a name="api-management-policies"></a>API 관리 정책
이 섹션에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](api-management-howto-policies.md)을 참조하세요.  
  
 정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 hello 시스템의 강력한 기능입니다. 정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다. 인기 있는 문은 XML tooJSON에서 형식 변환을 포함 하 고 호출 toorestrict hello 양을 개발자 로부터 들어오는 호출 속도입니다. 더 많은 정책을 hello 상자 바로 사용할 수 있는 됩니다.  
  
 정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다. Hello와 같은 일부 정책은 [제어 흐름](api-management-advanced-policies.md#choose) 및 [변수 설정](api-management-advanced-policies.md#set-variable) 정책은 정책 식을 기반으로 합니다. 자세한 내용은 [고급 정책](api-management-advanced-policies.md#AdvancedPolicies) 및 [정책 식](api-management-policy-expressions.md)을 참조하세요.  
  
##  <a name="ProxyPolicies"></a> 정책  
  
-   [액세스 제한 정책](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [HTTP 헤더 확인](api-management-access-restriction-policies.md#CheckHTTPHeader) - HTTP 헤더의 존재 및/또는 값을 적용합니다.  
  
    -   [구독으로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRate) - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.  
  
    -   [키로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.  
  
    -   [호출자 IP 제한](api-management-access-restriction-policies.md#RestrictCallerIPs) - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.  
  
    -   [구독에 의해 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuota) -구독 별로에서 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 허용 합니다.  
  
    -   [키로 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -당 키 단위로 허용 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 지정 합니다.  
  
    -   [JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.  
  
-   [고급 정책](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [제어 흐름](api-management-advanced-policies.md#choose) 조건부로-부울 표현식의 hello 평가에 따라 정책 문을 적용 합니다.  
  
    -   [요청 전달](api-management-advanced-policies.md#ForwardRequest) -hello 요청 toohello 백 엔드 서비스에 전달 합니다.  
  
    -   [허브 tooEvent 로그](api-management-advanced-policies.md#log-to-eventhub) -는 거 엔터티에 의해 정의 된 hello 지정 된 형식 tooa 메시지 대상에 메시지를 보냅니다.  
  
    -   [다시 시도](api-management-advanced-policies.md#Retry) -hello 재시도 실행 고 hello 조건이 충족 될 때까지 정책 문을 포함 합니다. 지정 된 시간 간격을 hello 및 다시 시도 횟수를 지정 하는 toohello 실행에서 반복 됩니다.  
  
    -   [응답을 반환](api-management-advanced-policies.md#ReturnResponse) -지정 된 지시 파일 중단 파이프라인 실행 및 반환 hello 직접 toohello 호출자입니다.  
  
    -   [한 가지 방법은 요청 보내기](api-management-advanced-policies.md#SendOneWayRequest) -요청 toohello 지정한 URL 응답을 받기 위해 대기 하지 않고 보냅니다.  
  
    -   [요청 보내기](api-management-advanced-policies.md#SendRequest) -요청 toohello 지정한 URL을 보냅니다.  
  
    -   [변수 설정](api-management-advanced-policies.md#set-variable) - 나중에 액세스할 수 있도록 명명된 context 변수의 값을 유지합니다.  
  
    -   [요청 하는 방법을 설정](api-management-advanced-policies.md#SetRequestMethod) -toochange hello HTTP 메서드는 요청에 대 한 있습니다.  
  
    -   [상태 코드를 설정](api-management-advanced-policies.md#SetStatus) -변경 hello HTTP 상태 코드 toohello 값을 지정 합니다.  
  
    -   [추적](api-management-advanced-policies.md#Trace) -hello에 문자열을 추가 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력 합니다.  
  
    -   [대기](api-management-advanced-policies.md#Wait) -묶인 때까지 대기 [보내기 요청](api-management-advanced-policies.md#SendRequest), [캐시에서 값을 가져올](api-management-caching-policies.md#GetFromCacheByKey), 또는 [제어 흐름](api-management-advanced-policies.md#choose) 계속 진행 하기 전에 정책 toocomplete 합니다.  
  
-   [인증 정책](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [기본 사용 인증](api-management-authentication-policies.md#Basic) - 기본 인증을 사용하여 백 엔드 서비스를 인증합니다.  
  
    -   [클라이언트 인증서 사용 인증](api-management-authentication-policies.md#ClientCertificate) - 클라이언트 인증서를 사용하여 백 엔드 서비스를 인증합니다.  
  
-   [캐싱 정책](api-management-caching-policies.md#CachingPolicies)  
  
    -   [캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.  
  
    -   [Toocache 저장](api-management-caching-policies.md#StoreToCache) -toohello에 따라 캐시 응답 캐시 제어 구성을 지정 합니다.  
  
    -   [캐시에서 값 가져오기](api-management-caching-policies.md#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.  
  
    -   [값을 캐시에 저장](api-management-caching-policies.md#StoreToCacheByKey) -hello 캐시에 항목을 키로 저장 합니다.  
  
    -   [캐시에서 값을 제거](api-management-caching-policies.md#RemoveCacheByKey) -키별로 hello 캐시에 항목을 제거 합니다.  
  
-   [도메인 간 정책](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [도메인 간 호출을 허용](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 hello API에 액세스할 수 있게 합니다.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 또는 tooan 작업을 지원 크로스-원본 자원 공유 (CORS)를 추가 합니다.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) -JSON with padding (JSONP) 지원 tooan 작업이 추가 하거나는 API tooallow 도메인 간 JavaScript 브라우저 기반 클라이언트에서 호출 합니다.  
  
-   [변환 정책](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [JSON tooXML 변환](api-management-transformation-policies.md#ConvertJSONtoXML) -요청으로 변환 하거나 JSON tooXML에서 응답 본문입니다.  
  
    -   [XML tooJSON 변환](api-management-transformation-policies.md#ConvertXMLtoJSON) -변환 요청 또는 응답 본문에서 XML tooJSON 합니다.  
  
    -   [본문 문자열 찾기 및 바꾸기](api-management-transformation-policies.md#Findandreplacestringinbody) - 요청 또는 응답 하위 문자열을 찾아 다른 하위 문자열로 바꿉니다.  
  
    -   [콘텐츠의 Url 마스킹](api-management-transformation-policies.md#MaskURLSContent) -다시 작성 (마스킹) 링크 hello에 대 한 응답 본문 toohello hello 게이트웨이 통해 동일한 링크를 가리킵니다.  
  
    -   [백 엔드 서비스 설정](api-management-transformation-policies.md#SetBackendService) -들어오는 요청에 대 한 hello 백 엔드 서비스를 변경 합니다.  
  
    -   [본문 설정](api-management-transformation-policies.md#SetBody) -들어오는 요청과 나가는 요청에 대 한 hello 메시지 본문을 설정 합니다.  
  
    -   [HTTP 헤더 설정](api-management-transformation-policies.md#SetHTTPheader) -값 tooan 기존 응답 및/또는 요청 헤더를 할당 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.  
  
    -   [쿼리 문자열 매개 변수 설정](api-management-transformation-policies.md#SetQueryStringParameter) - 요청 쿼리 문자열 매개 변수를 추가하거나 그 값을 바꾸거나 삭제합니다.  
  
    -   [URL 재작성](api-management-transformation-policies.md#RewriteURL) -요청 URL hello 웹 서비스에서 공용 형식 toohello 형식에서 변환 합니다.  
  
    -   [XSLT를 사용 하 여 XML 변형](api-management-transformation-policies.md#XSLTransform) -는 XSL 변환을 tooXML hello 요청 또는 응답 본문에 적용 됩니다.  
  
## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  
