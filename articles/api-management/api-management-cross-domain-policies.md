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
# <a name="api-management-cross-domain-policies"></a>도메인 정책 간 API 관리
이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.  
  
##  <a name="CrossDomainPolicies"></a> 도메인 간 정책  
  
-   [도메인 간 호출을 허용](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 hello API에 액세스할 수 있게 합니다.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 또는 tooan 작업을 지원 크로스-원본 자원 공유 (CORS)를 추가 합니다.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) -JSON with padding (JSONP) 지원 tooan 작업이 추가 하거나는 API tooallow 도메인 간 JavaScript 브라우저 기반 클라이언트에서 호출 합니다.  
  
##  <a name="AllowCrossDomainCalls"></a> 도메인 간 호출 허용  
 사용 하 여 hello `cross-domain` 정책 toomake hello API Adobe Flash 및 Microsoft Silverlight 브라우저 기반 클라이언트에서 액세스할 수 있습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>예  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|cross-domain|루트 요소입니다. 자식 요소 toohello 따라야 [Adobe 도메인 간 정책 파일 사양](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)합니다.|예|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** global  
  
##  <a name="CORS"></a> CORS  
 hello `cors` tooan 작업을 지원 크로스-원본 자원 공유 (CORS) 또는 브라우저 기반 클라이언트에서 호출 하는 API tooallow 도메인 간 정책을 추가 합니다.  
  
 CORS는 브라우저와 서버 toointeract 있으며 tooallow 특정 교차 원본 요청 (예:: 웹 페이지 tooother 도메인에는 JavaScript에서 수행한는 XMLHttpRequests 호출) 여부를 결정 합니다. 따라서 동일 원본의 요청만 허용하는 것보다 유연성이 더 뛰어나며 모든 원본 간 요청을 허용하는 것보다 보안도 더 높아집니다.  
  
### <a name="policy-statement"></a>정책 문:  
  
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
  
### <a name="example"></a>예제  
 이 예제에서는 사용자 지정 헤더 나 메서드 GET 및 POST 이외의 항목과 같이 toosupport 사전 비행 요청 방법을 보여 줍니다. toosupport 사용자 지정 헤더 및 추가 HTTP 동사를 사용 하 여 hello `allowed-methods` 및 `allowed-headers` hello 다음 예제와 같이 섹션.  
  
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
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|cors|루트 요소입니다.|예|해당 없음|  
|allowed-origins|포함 `origin` 도메인 간 요청에 대 한 원본을 허용 하는 hello를 설명 하는 요소입니다. `allowed-origins`단일 포함 될 수 있습니다 `origin` 지정 하는 요소 `*` tooallow 모든 원본 또는 하나 이상의 `origin` URI를 포함 하는 요소입니다.|예|해당 없음|  
|원본|hello 값일 수 하나 `*` tooallow 모든 원본을 또는 단일 원본을 지정 하는 URI입니다. hello URI 구성표, 호스트 및 포트를 포함 해야 합니다.|예|Hello 포트를 URI에서 생략 된 경우 포트 80은 HTTP에 대 한 사용 및 HTTPS에 포트 443 사용 됩니다.|  
|allowed-methods|GET 또는 POST 이외의 메서드가 허용되는 경우 이 요소가 필요합니다. 포함 `method` hello 지원 HTTP 동사를 지정 하는 요소입니다.|아니요|이 섹션이 없으면 GET 및 POST가 지원됩니다.|  
|메서드|HTTP 동사를 지정합니다.|하나 이상의 `method` 경우 hello 요소는 필수 `allowed-methods` 섹션은 포함 되어 있습니다.|해당 없음|  
|allowed-headers|이 요소는 포함 `header` hello 요청에 포함 될 수 있는 hello 헤더의 이름을 지정 하는 요소입니다.|아니요|해당 없음|  
|expose-headers|이 요소는 포함 `header` hello 클라이언트에서 액세스할 수 있는 hello 헤더의 이름을 지정 하는 요소입니다.|아니요|해당 없음|  
|머리글|헤더 이름을 지정합니다.|하나 이상의 `header` 요소에 필요한 `allowed-headers` 또는 `expose-headers` hello 섹션은 포함 하는 경우.|해당 없음|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|hello `Access-Control-Allow-Credentials` hello에 대 한 실행 전 응답 헤더 집합 toohello 값이이 특성의 되며 도메인 간 요청에서 hello 클라이언트 기능 toosubmit 자격 증명에 영향을 줍니다.|아니요|false|  
|preflight-result-max-age|hello `Access-Control-Max-Age` hello에 대 한 실행 전 응답 헤더 집합 toohello 값이이 특성의 되며 hello 사용자 에이전트의 기능 toocache 전 응답에 영향을 줍니다.|아니요|0|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** API, operation  
  
##  <a name="JSONP"></a> JSONP  
 hello `jsonp` 정책 안쪽 여백 (JSONP) 지원 tooan 작업이 나 JavaScript 브라우저 기반 클라이언트에서 API tooallow 도메인 간 호출 된 JSON을 추가 합니다. JSONP는 다른 도메인에 서버에서 JavaScript 프로그램 toorequest 데이터에서 사용 하는 방법입니다. Hello에 대 한 액세스 tooweb 페이지를 사용 해야 하는 대부분 웹 브라우저에 의해 적용 하는 hello 제한을 무시 동일한 도메인입니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>예제  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Hello 콜백 매개 변수 없이 hello 메서드를 호출 하는 경우? cb = XXX (함수 호출 래퍼가) 없이 일반 JSON을 반환 합니다.  
  
 Hello 콜백 매개 변수를 추가 하는 경우 `?cb=XXX` hello hello 콜백 함수 처럼 원래 JSON 결과 래핑하는 JSONP 결과가 반환 됩니다`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|jsonp|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|hello 도메인 간 JavaScript 함수 호출 hello 정규화 된 도메인 이름을 접두사로 hello 함수 상주 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** outbound  
  
-   **정책 범위:** global, product, API, operation  
  
## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  