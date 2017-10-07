---
title: "aaaAzure API 관리 캐싱 정책 | Microsoft Docs"
description: "Azure API 관리에서 사용 하기 위해 사용할 수 있는 정책을 캐싱 hello에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>API Management 캐싱 정책
이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.  
  
##  <a name="CachingPolicies"></a> 캐싱 정책  
  
-   응답 캐싱 정책  
  
    -   [캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) - 캐시 조회를 수행하여 사용 가능한 경우 올바르게 캐시된 응답을 반환합니다.  
  
    -   [Toocache 저장](api-management-caching-policies.md#StoreToCache) -toohello 지정 된 캐시 제어 구성에 따라 캐시 응답 합니다.  
  
-   값 캐싱 정책  
  
    -   [캐시에서 값 가져오기](#GetFromCacheByKey) - 키로 캐시된 항목을 검색합니다.  
  
    -   [값을 캐시에 저장](#StoreToCacheByKey) -hello 캐시에 항목을 키로 저장 합니다.  
  
    -   [캐시에서 값을 제거](#RemoveCacheByKey) -키별로 hello 캐시에 항목을 제거 합니다.  
  
##  <a name="GetFromCache"></a> 캐시에서 가져오기  
 사용 하 여 hello `cache-lookup` 정책 tooperform 캐시 조회 및 사용 가능한 경우 유효한 캐시 된 응답을 반환 합니다. 이 정책은 응답 콘텐츠가 일정 기간 동안 정적 상태인 경우 적용해야 합니다. 응답 캐시 대역폭 줄어들고 hello 백 엔드 웹 서버와 낮추고 체감 대기 시간이 API 소비자에 처리 요구 사항을 적용 합니다.  
  
> [!NOTE]
>  이 정책은 해당 있어야 [저장소 toocache](api-management-caching-policies.md#StoreToCache) 정책입니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>예  
  
#### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>정책 식을 사용하는 예제  
 캐싱 기간 일치 hello에 지정 된 대로 hello 백 엔드 서비스의 응답 캐시 hello는 tootooconfigure API 관리 응답 서비스의 백업 하는 방법을 보여 주는이 예제 `Cache-Control` 지시문입니다. 구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too25:25 빨리 감기 및 합니다.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|cache-lookup|루트 요소입니다.|예|  
|vary-by-header|지정된 헤더 값당 시작 캐싱 응답입니다(예: Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match).|아니요|  
|vary-by-query-parameter|지정된 쿼리 매개 변수의 값에 따라 응답 캐싱을 시작합니다. 단일 또는 여러 매개 변수를 입력합니다. 세미콜론을 구분 기호로 사용합니다. 지정하지 않은 경우 모든 쿼리 매개 변수가 사용됩니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|설정 된 경우 너무`true`, 권한 부여 헤더를 포함 하는 요청의 캐싱을 허용 합니다.|아니요|false|  
|downstream-caching-type|이 특성의 다음 값에는 hello tooone를 설정 되어야 합니다.<br /><br /> -   none - 다운스트림 캐싱이 허용되지 않습니다.<br />-   private - 다운스트림 캐싱이 허용됩니다.<br />-   public - 개인 및 공유 다운스트림 캐싱이 허용됩니다.|아니요|없음|  
|must-revalidate|다운스트림 캐싱을 사용 하는 경우이 특성을 설정 또는 해제 hello `must-revalidate` 게이트웨이 응답에서 캐시 제어 지시문입니다.|아니요|true|  
|vary-by-developer|도`true` 개발자 키별로 toocache 응답 합니다.|아니요|false|  
|vary-by-developer-groups|도`true` 사용자 역할별로 toocache 응답 합니다.|아니요|false|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** API, operation, product  
  
##  <a name="StoreToCache"></a>저장소 toocache  
 hello `cache-store` toohello에 따라 정책 캐시 응답 캐시 설정을 지정 합니다. 이 정책은 응답 콘텐츠가 일정 기간 동안 정적 상태인 경우 적용해야 합니다. 응답 캐시 대역폭 줄어들고 hello 백 엔드 웹 서버와 낮추고 체감 대기 시간이 API 소비자에 처리 요구 사항을 적용 합니다.  
  
> [!NOTE]
>  이 정책에는 해당하는 [캐시에서 가져오기](api-management-caching-policies.md#GetFromCache) 정책이 있어야 합니다.  
  
### <a name="policy-statement"></a>정책 문:  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>예  
  
#### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>정책 식을 사용하는 예제  
 캐싱 기간 일치 hello에 지정 된 대로 hello 백 엔드 서비스의 응답 캐시 hello는 tootooconfigure API 관리 응답 서비스의 백업 하는 방법을 보여 주는이 예제 `Cache-Control` 지시문입니다. 구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too25:25 빨리 감기 및 합니다.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|cache-store|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|duration|Time-to-live hello의 시간 (초)에 지정 된 항목을 캐시 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** outbound  
  
-   **정책 범위:** API, operation, product  
  
##  <a name="GetFromCacheByKey"></a> 캐시에서 값 가져오기  
 사용 하 여 hello `cache-lookup-value` 정책 tooperform 키 조회를 캐시 하 고 캐시 된 값을 반환 합니다. hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.  
  
> [!NOTE]
>  이 정책에는 해당하는 [값을 캐시에 저장](#StoreToCacheByKey) 정책이 있어야 합니다.  
  
### <a name="policy-statement"></a>정책 문:  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>예  
 이 정책에 대한 자세한 내용과 예제는 [Azure API Management의 사용자 지정 캐싱](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)을 참조하세요.  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|cache-lookup-value|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|default-value|할당할 toohello 변수 hello 캐시 키 조회 결과 누락 값입니다. 이 특성을 지정하지 않으면 `null`이 할당됩니다.|아니요|`null`|  
|key|키 값 toouse hello 조회에서를 캐시 합니다.|예|해당 없음|  
|variable-name|Hello의 이름 [컨텍스트 변수의](api-management-policy-expressions.md#ContextVariables) 조회에 성공 하면 값을 조회 하는 hello에 할당 됩니다. 조회 누락에 결과가 hello 변수 hello의 hello 값이 할당 됩니다 `default-value` 특성 또는 `null`경우 hello `default-value` 특성을 생략 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** global, API, operation, product  
  
##  <a name="StoreToCacheByKey"></a> 값을 캐시에 저장  
 hello `cache-store-value` 키로 캐시 저장소를 수행 합니다. hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.  
  
> [!NOTE]
>  이 정책에는 해당하는 [캐시에서 값 가져오기](#GetFromCacheByKey) 정책이 있어야 합니다.  
  
### <a name="policy-statement"></a>정책 문:  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>예  
 이 정책에 대한 자세한 내용과 예제는 [Azure API Management의 사용자 지정 캐싱](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/)을 참조하세요.  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|cache-store-value|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|duration|값은 초 단위로 지정 하는 기간 값을 제공 하는 hello에 대 한 캐시 됩니다.|예|해당 없음|  
|key|캐시 키 hello 값 아래에 저장 됩니다.|예|해당 없음|  
|값|hello 값 toobe 캐시 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** global, API, operation, product  
  
###  <a name="RemoveCacheByKey"></a> 캐시에서 값 제거  
 hello `cache-remove-value` 해당 키로 식별 된 캐시 된 항목을 삭제 합니다. hello 키 임의의 문자열 값을 가질 수와 정책 식을 사용 하 여 제공 됩니다.  
  
#### <a name="policy-statement"></a>정책 문  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>예  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|cache-remove-value|루트 요소입니다.|예|  
  
#### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|key|hello의 hello 키 값 toobe hello 캐시에서 제거를 이전에 캐시 합니다.|예|해당 없음|  
  
#### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) 합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** global, API, operation, product  
  

## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  