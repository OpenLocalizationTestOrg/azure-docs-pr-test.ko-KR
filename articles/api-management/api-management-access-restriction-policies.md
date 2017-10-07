---
title: "aaaAzure API 관리 액세스 제한 정책 | Microsoft Docs"
description: "Azure API 관리에 사용할 수 있는 hello 액세스 제한 정책에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>API Management 액세스 제한 정책
이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.  
  
##  <a name="AccessRestrictionPolicies"></a> 액세스 제한 정책  
  
-   [HTTP 헤더 확인](api-management-access-restriction-policies.md#CheckHTTPHeader) - HTTP 헤더의 존재 및/또는 값을 적용합니다.  
  
-   [구독으로 호출 속도 제한](api-management-access-restriction-policies.md#LimitCallRate) - 구독을 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.  
  
-   [키로 호출 속도 제한](#LimitCallRateByKey) - 키를 기준으로 호출 속도를 제한하여 API 사용량 급증을 방지합니다.  
  
-   [호출자 IP 제한](api-management-access-restriction-policies.md#RestrictCallerIPs) - 특정 IP 주소 및/또는 주소 범위의 호출을 필터링(허용/거부)합니다.  
  
-   [구독에 의해 할당량 설정](api-management-access-restriction-policies.md#SetUsageQuota) -구독 별로에서 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 허용 합니다.  
  
-   [키로 할당량 설정](#SetUsageQuotaByKey) -당 키 단위로 허용 tooenforce 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량을 지정 합니다.  
  
-   [JWT 유효성 검사](api-management-access-restriction-policies.md#ValidateJWT) - 지정된 HTTP 헤더 또는 지정된 쿼리 매개 변수에서 추출된 JWT의 존재 및 유효성을 적용합니다.  
  
##  <a name="CheckHTTPHeader"></a> HTTP 헤더 확인  
 사용 하 여 hello `check-header` 정책 tooenforce 요청이 지정한 HTTP 헤더에 있습니다. 필요에 따라 hello 헤더에 특정 값 또는 허용 된 값의 범위에 대 한 확인 toosee를 확인할 수 있습니다. Hello 확인이 실패 하면 hello 정책 요청 처리를 종료 하 고 hello HTTP 상태 코드 및 오류 메시지 hello 정책에 지정 된을 반환 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>예  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|check-header|루트 요소입니다.|예|  
|값|허용된 HTTP 헤더 값입니다. 여러 값 요소가 지정 된 hello 값 중 하나는 일치 하는 경우 hello 검사는 성공을 간주 됩니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|Hello 헤더 존재 하지 않거나 잘못 된 값이 hello HTTP 응답 본문에 오류 메시지 tooreturn 합니다. 이 메시지는 적절히 이스케이프된 특수 문자를 포함해야 합니다.|예|해당 없음|  
|failed-check-httpcode|HTTP 상태 코드 tooreturn hello 헤더 존재 하지 않거나 잘못 된 값입니다.|예|해당 없음|  
|header-name|HTTP 헤더 toocheck hello의 hello 이름입니다.|예|해당 없음|  
|ignore-case|TooTrue 또는 false로 설정할 수 있습니다. 이면 set tooTrue 케이스 hello 집합이 허용 되는 값에 대해 hello 헤더 값을 비교 하는 경우 무시 됩니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="LimitCallRate"></a> 구독으로 호출 속도 제한  
 hello `rate-limit` 정책으로 인해 API 사용 급증을 hello를 제한 하 여 구독 별로 지정 된 시간 동안 당 번호 지정 된 속도 tooa 호출 합니다. 이 정책은 트리거될 때 hello 호출자가 받을 `429 Too Many Requests` 응답 상태 코드입니다.  
  
> [!IMPORTANT]
>  이 정책은 정책 문서당 한 번만 사용할 수 있습니다.  
>   
>  [정책 식](api-management-policy-expressions.md) 이 정책에 대 한 hello 정책 특성에 사용할 수 없습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|set-limit|루트 요소입니다.|예|  
|api|이러한 요소 tooimpose 호출 속도 제한 중 하나 이상을 hello 제품 내에서 Api에 추가 합니다. 제품 및 API 호출 속도 제한은 독립적으로 적용됩니다.|아니요|  
|operation|API 내의 작업에 하나 이상의 이러한 요소 tooimpose 호출 속도 제한 추가 합니다. 제품, API 및 작업 호출 속도 제한은 독립적으로 적용됩니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|name|어떤 tooapply hello 속도 제한에 대 한 hello 이름 hello API입니다.|예|해당 없음|  
|calls|hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.|예|해당 없음|  
|renewal-period|hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** product  
  
##  <a name="LimitCallRateByKey"></a> 키로 호출 속도 제한  
 hello `rate-limit-by-key` 정책에는 API를 사용 하지 못하도록 스파이크 hello를 제한 하 여 키 당 기준 당 지정 된 시간 동안 숫자 속도 tooa 지정 된 호출 합니다. hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다. 선택적 증분 조건 toospecify hello 제한에 대해 계산 되도록 요청을 추가할 수 있습니다. 이 정책은 트리거될 때 hello 호출자가 받을 `429 Too Many Requests` 응답 상태 코드입니다.  
  
 이 정책에 대한 자세한 내용과 예제는 [Azure API Management로 고급 요청 제한](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)을 참조하세요.  
  
> [!IMPORTANT]
>  이 정책은 정책 문서당 한 번만 사용할 수 있습니다.  
  
### <a name="policy-statement"></a>정책 문:  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>예제  
 다음 예제는 hello, hello 속도 한도 hello 호출자 IP 주소를 통해 키가 지정 됩니다.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|set-limit|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|calls|hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.|예|해당 없음|  
|counter-key|hello hello 속도 제한 정책에 대 한 키 toouse 합니다.|예|해당 없음|  
|increment-condition|hello hello 요청 hello 할당량으로 간주 해야 하는 경우를 지정 하는 부울 식 (`true`).|아니요|해당 없음|  
|renewal-period|hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="RestrictCallerIPs"></a> 호출자 IP 제한  
 hello `ip-filter` 정책에서 특정 IP 주소 및/또는 주소 범위의 호출 (허용/거부)를 필터링 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>예  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|ip-filter|루트 요소입니다.|예|  
|address|어떤 toofilter에 단일 IP 주소를 지정합니다.|하나 이상의 `address` 또는 `address-range` 요소가 필요합니다.|  
|address-range from="address" to="address"|어떤 toofilter에 범위의 IP 주소를 지정합니다.|하나 이상의 `address` 또는 `address-range` 요소가 필요합니다.|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|IP 범위 tooallow 해결 하거나에 대 한 액세스를 거부 합니다.|필요한 경우 hello `address-range` 요소를 사용 합니다.|해당 없음|  
|ip-filter action="allow &#124; forbid"|호출을 허용할지 하지 hello에 대 한 IP 주소와 범위를 지정 하는지 여부를 지정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="SetUsageQuota"></a> 구독으로 사용 할당량 설정  
 hello `quota` 정책 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량 구독 별로에 적용 합니다.  
  
> [!IMPORTANT]
>  이 정책은 정책 문서당 한 번만 사용할 수 있습니다.  
>   
>  [정책 식](api-management-policy-expressions.md) 이 정책에 대 한 hello 정책 특성에 사용할 수 없습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|quota|루트 요소입니다.|예|  
|api|이러한 요소 tooimpose 할당량 중 하나 이상을 hello 제품 내에서 Api에 추가 합니다. 제품 및 API 할당량은 독립적으로 적용됩니다.|아니요|  
|operation|API 내의 작업에 대해 하나 이상의 이러한 요소 tooimpose 할당량을 추가 합니다. 제품, API 및 작업 할당량은 독립적으로 적용됩니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|name|hello API 또는 할당량에 적용 되는 hello에 대 한 작업의 hello 이름입니다.|예|해당 없음|  
|bandwidth|hello에 지정 된 hello 시간 간격 동안 허용 되는 (킬로바이트)의 최대 총 수를 hello `renewal-period`합니다.|`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.|해당 없음|  
|calls|hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.|`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.|해당 없음|  
|renewal-period|hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** product  
  
##  <a name="SetUsageQuotaByKey"></a> 키로 사용 할당량 설정  
 hello `quota-by-key` 정책은 되도록 갱신 가능 하거나 영구적인 호출 볼륨 및/또는 대역폭 할당량 키 당 기준입니다. hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다. 선택적 증분 조건 toospecify hello 할당량으로 계산 되도록 요청을 추가할 수 있습니다.  
  
 이 정책에 대한 자세한 내용과 예제는 [Azure API Management로 고급 요청 제한](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/)을 참조하세요.  
  
> [!IMPORTANT]
>  이 정책은 정책 문서당 한 번만 사용할 수 있습니다.  
>   
>  [정책 식](api-management-policy-expressions.md) 이 정책에 대 한 hello 정책 특성에 사용할 수 없습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>예제  
 다음 예제는 hello, hello 할당량은 hello 호출자 IP 주소를 통해 키가 지정 됩니다.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|quota|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|bandwidth|hello에 지정 된 hello 시간 간격 동안 허용 되는 (킬로바이트)의 최대 총 수를 hello `renewal-period`합니다.|`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.|해당 없음|  
|calls|hello에 지정 된 hello 시간 간격 동안 허용 된 호출의 최대 총 수를 hello `renewal-period`합니다.|`calls`, `bandwidth` 또는 둘 다 함께 지정해야 합니다.|해당 없음|  
|counter-key|hello hello 할당량 정책에 대 한 키 toouse 합니다.|예|해당 없음|  
|increment-condition|hello hello 요청 hello 할당량으로 간주 해야 하는 경우를 지정 하는 부울 식 (`true`)|아니요|해당 없음|  
|renewal-period|hello 기간 (초)이 지나면 hello 할당량이 다시 설정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="ValidateJWT"></a> JWT 유효성 검사  
 hello `validate-jwt` 정책 적용 존재 하 고 HTTP 헤더 또는 쿼리 매개 변수는 지정한에서 추출 된 JWT의 유효성을 검사 합니다.  
  
> [!IMPORTANT]
>  hello `validate-jwt` 정책에 따라 해당 hello `exp` 등록 된 클레임은 hello JWT 토큰에 포함 하지 않는 한 `require-expiration-time` 특성이 지정 되 고도`false`합니다.  
> hello `validate-jwt` 정책 HS256 및 RS256 서명 알고리즘을 지원 합니다. HS256에 대 한 hello 키 인라인 hello 정책 hello base64 인코딩 형식으로 내 제공 되어야 합니다. RS256에 대 한 hello 키에 toobe Open ID 구성 끝점을 통해 제공 됩니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>예  
  
#### <a name="azure-mobile-services-token-validation"></a>Azure Mobile Services 토큰 유효성 검사  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Azure Active Directory 토큰 유효성 검사  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Azure Active Directory B2C 토큰 유효성 검사  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>토큰 클레임을 기반으로 하는 액세스 toooperations 권한 부여  
 이 예에서는 어떻게 toouse hello [JWT의 유효성을 검사](api-management-access-restriction-policies.md#ValidateJWT) 정책 toopre-토큰 클레임을 기반으로 하는 액세스 toooperations 권한을 부여 합니다. 구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too13:50 빨리 감기 및 합니다. Hello 정책 편집기에 구성 된 toosee hello 정책이 too15:00를 빨리 감기 및 too18:50 모두와 사용 하지 않는 hello hello 개발자 포털에서 호출 하는 작업의 데모에 대 한 권한 부여 토큰을 필요로 하는 다음 합니다.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|validate-jwt|루트 요소입니다.|예|  
|audiences|Hello 토큰에 포함 될 수 있는 허용 가능한 대상 그룹 클레임 목록을 포함 합니다. 여러 대상 그룹 값이 있는 경우 각 값은 모든 값이 소진(이 경우 유효성 검사 실패)되거나 한 값이 성공할 때까지 시도됩니다. 한 명 이상의 대상 그룹을 지정해야 합니다.|아니요|  
|issuer-signing-keys|목록이 사용 되는 키 toovalidate Base64 인코딩 보안 토큰을 서명합니다. 보안 키가 여러 개 있는 경우 각 키는 모든 키가 소진(이 경우 유효성 검사 실패)되거나 한 개 키가 성공할 때까지 시도됩니다(토큰 롤오버에 유용함). 주요 요소는 선택적 `id` 에 대해 사용 되는 특성 toomatch `kid` 클레임입니다.|아니요|  
|issuers|목록 hello 토큰을 발급 한 허용 가능한 보안 주체입니다. 여러 발급자 값이 있는 경우 각 값은 모든 값이 소진(이 경우 유효성 검사 실패)되거나 한 값이 성공할 때까지 시도됩니다.|아니요|  
|openid-config|서명 키 및 발급자 생성 수 있는 수는 호환 Open ID 구성 끝점을 지정 하는 데 사용 되는 hello 요소입니다.|아니요|  
|required-claims|목록이 대 한 hello 토큰에 있는 필요로 하는 클레임 toobe toobe 유효한 것으로 간주 합니다. Hello 때 `match` 특성이 너무 설정 된`all` hello 정책에 있는 모든 클레임 값 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다. Hello 때 `match` 특성이 너무 설정 된`any` 클레임이 하나 이상 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.|아니요|  
|zumo-master-key|Azure Mobile Services에서 발급한 토큰에 대한 마스터 키|아니요|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|clock-skew|Timespan입니다. Hello 토큰의 만료 클레임이 hello 토큰에 있는 고 hello 현재를 지난 경우 여유 제공 날짜 / 시간입니다.|아니요|0초|  
|failed-validation-error-message|Hello JWT 유효성 검사를 통과 하지 못하면 hello HTTP 응답 본문에 오류 메시지 tooreturn 합니다. 이 메시지는 적절히 이스케이프된 특수 문자를 포함해야 합니다.|아니요|기본 오류 메시지는 유효성 검사 문제에 따라 달라집니다(예: "JWT not present(JWT 없음)").|  
|failed-validation-httpcode|HTTP 상태 코드 tooreturn hello JWT 유효성 검사를 통과 하지 않습니다.|아니요|401|  
|header-name|hello 토큰을 보유 하는 hello HTTP 헤더의 hello 이름입니다.|`header-name` 또는 `query-paremeter-name`를 지정해야 하며 둘 다 함께 지정할 수 없습니다.|해당 없음|  
|id|hello `id` hello에 대 한 특성 `key` 요소에 대해 일치 시킬 toospecify hello 문자열을 사용 하면 `kid` 서명 유효성 검사에 대 한 적절 한 키 toouse hello 아웃 토큰 (있는 경우) toofind hello에에서 대 한 클레임입니다.|아니요|해당 없음|  
|match|hello `match` hello에 대 한 특성 `claim` 요소 hello 정책에 있는 모든 클레임 값에 대 한 유효성 검사 toosucceed hello 토큰에 존재 해야 하는지 여부를 지정 합니다. 가능한 값은 다음과 같습니다.<br /><br /> -                          `all`-hello 정책에 있는 모든 클레임 값 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.<br /><br /> -                          `any`-하나 이상의 클레임 값 유효성 검사 toosucceed hello 토큰에 존재 해야 합니다.|아니요|모두|  
|query-paremeter-name|hello 이름 hello hello 쿼리 매개 변수를 보유 hello 토큰입니다.|`header-name` 또는 `query-paremeter-name`를 지정해야 하며 둘 다 함께 지정할 수 없습니다.|해당 없음|  
|require-expiration-time|부울 값입니다. Hello 토큰에 만료 클레임이 필요한 지를 지정 합니다.|아니요|true|
|require-scheme|hello 토큰 구성표의 이름 예: hello "Bearer"). 이 특성이 설정 되 면 hello 정책은 스키마가 있는 hello 권한 부여 헤더 값에에서 지정를 확인 합니다.|아니요|해당 없음|
|require-signed-tokens|부울 값입니다. 토큰 서명 필요 toobe 인지 여부를 지정 합니다.|아니요|true|  
|url|Open ID 구성 메타데이터를 가져올 수 있는 Open ID 구성 끝점 URL입니다. Azure Active Directory에 대 한 url hello를 사용 하 여: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` 예: 사용자 디렉터리 테 넌 트 이름으로 대체 `contoso.onmicrosoft.com`합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** global, product, API, operation  
  
## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  
