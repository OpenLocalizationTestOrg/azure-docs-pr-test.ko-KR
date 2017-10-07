---
title: "API 관리 고급 정책 aaaAzure | Microsoft Docs"
description: "Hello Azure API 관리에서 사용 하기 위해 사용할 수 있는 정책을 고급 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>API Management 고급 정책
이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.  
  
##  <a name="AdvancedPolicies"></a> 고급 정책  
  
-   [제어 흐름](api-management-advanced-policies.md#choose) -조건부로 hello 부울의 hello 평가 결과에 따라 정책 문을 적용 [식](api-management-policy-expressions.md)합니다.  
  
-   [요청 전달](#ForwardRequest) -hello 요청 toohello 백 엔드 서비스에 전달 합니다.

-   [동시성을 제한](#LimitConcurrency) -방지에서 한 번에 지정 된 요청 수를 hello 보다 더 많은 하 여 실행 정책을 포함 합니다.
  
-   [허브 tooEvent 로그](#log-to-eventhub) -hello에 메시지를 보내고 형식 tooan로 거 엔터티에 의해 정의 된 이벤트 허브를 지정 합니다. 

-   [응답의 모의 알림](#mock-response) -중단 파이프라인 실행 모의 응답을 반환 하 고 직접 toohello 호출자입니다.
  
-   [다시 시도](#Retry) -hello 재시도 실행 고 hello 조건이 충족 될 때까지 정책 문을 포함 합니다. 지정 된 시간 간격을 hello 및 다시 시도 횟수를 지정 하는 toohello 실행에서 반복 됩니다.  
  
-   [응답을 반환](#ReturnResponse) -지정 된 지시 파일 중단 파이프라인 실행 및 반환 hello 직접 toohello 호출자입니다. 
  
-   [한 가지 방법은 요청 보내기](#SendOneWayRequest) -요청 toohello 지정한 URL 응답을 받기 위해 대기 하지 않고 보냅니다.  
  
-   [요청 보내기](#SendRequest) -요청 toohello 지정한 URL을 보냅니다.  

-   [HTTP 프록시 설정](#SetHttpProxy) -HTTP 프록시를 통해 전달 tooroute 요청을 허용 합니다.  

-   [요청 하는 방법을 설정](#SetRequestMethod) -toochange hello HTTP 메서드는 요청에 대 한 있습니다.  
  
-   [상태 코드를 설정](#SetStatus) -변경 hello HTTP 상태 코드 toohello 값을 지정 합니다.  
  
-   [변수 설정](api-management-advanced-policies.md#set-variable) - 나중에 액세스할 수 있도록 명명된 [context](api-management-policy-expressions.md#ContextVariables) 변수의 값을 유지합니다.  

-   [추적](#Trace) -hello에 문자열을 추가 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력 합니다.  
  
-   [대기](#Wait) -묶인 때까지 대기 [보내기 요청](api-management-advanced-policies.md#SendRequest), [캐시에서 값을 가져올](api-management-caching-policies.md#GetFromCacheByKey), 또는 [제어 흐름](api-management-advanced-policies.md#choose) 계속 진행 하기 전에 정책 toocomplete 합니다.  
  
##  <a name="choose"></a> 흐름 제어  
 hello `choose` 정책이 포함 된 정책 hello 평가 결과에 부울 식, if then 다른 유사한 tooan 또는 스위치를 기반으로 문을 프로그래밍 언어의 구문에 적용 됩니다.  
  
###  <a name="ChoosePolicyStatement"></a> 정책 문  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 hello 제어 흐름 정책은 해야 하나 이상 포함 `<when/>` 요소입니다. hello `<otherwise/>` 요소는 선택 사항입니다. `<when/>` 요소 hello 정책 내에서 표시 되는 순서 대로 평가 됩니다. 먼저 hello 내에 포함 된 정책 문이 `<when/>` 특성 = 조건 가진 요소가 `true` 적용 됩니다. Hello 내에 포함 된 정책을 `<otherwise/>` 모든 요소를 사용할 수 있는 경우를 적용할의 hello `<when/>` 요소 조건 특성이 `false`합니다.  
  
### <a name="examples"></a>예  
  
####  <a name="ChooseExample"></a> 예  
 hello 다음 예제에서는 한 [변수 설정](api-management-advanced-policies.md#set-variable) 정책 및 제어 흐름 정책 두 개 있습니다.  
  
 hello set-variable 정책은 만들고 inbound 섹션 hello 중인는 `isMobile` 부울 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 경우 hello tootrue 설정 된 변수 `User-Agent` 요청 헤더에 hello 텍스트 `iPad` 또는 `iPhone`합니다.  
  
 첫 번째 제어 흐름 정책은 hello는 역시 inbound 섹션 hello 및 두 가지 중 하나를 조건부로 적용 [쿼리 문자열 매개 변수를 설정](api-management-transformation-policies.md#SetQueryStringParameter) hello hello 값에 따라 정책을 `isMobile` 컨텍스트 변수입니다.  
  
 두 번째 제어 흐름 정책은 hello hello outbound 섹션 이므로 hello 조건부로 적용 [XML 변환 tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) 정책 때 `isMobile` 너무 설정`true`합니다.  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a>예제  
 이 예제에서는 어떻게 hello 응답에서 데이터 요소를 제거 하 여 tooperform 콘텐츠 필터링 서비스에서 받은 hello 백 엔드 hello를 사용 하는 경우 `Starter` 제품입니다. 구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too34:30 빨리 감기 및 합니다. 개요 31:50 toosee부터 시작 [어두운 Sky 예측 API hello](https://developer.forecast.io/) 이 데모에 사용 합니다.  
  
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
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|choose|루트 요소입니다.|예|  
|when|hello에 대 한 조건 toouse hello `if` 또는 `ifelse` hello 부분의 `choose` 정책입니다. 경우 hello `choose` 정책에 여러 개의 `when` 섹션을 순서 대로 평가 됩니다. 한 번 hello `condition` when 요소 평가 너무`true`, 더 이상 없으면 `when` 조건이 평가 됩니다.|예|  
|otherwise|없으면 hello를 사용 하는 hello 정책 조각 toobe 포함 `when` 조건이 너무`true`합니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|  
|---------------|-----------------|--------------|  
|condition="Boolean expression &#124; Boolean constant"|hello 부울 식 또는 포함 된 경우 hello 상수 tooevaluated `when` 정책 문을 평가할 합니다.|예|  
  
###  <a name="ChooseUsage"></a> 사용 방법  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="ForwardRequest"></a> 요청 전달  
 hello `forward-request` 정책 hello 들어오는 요청 toohello 백 엔드 서비스 hello 요청에 지정 된 전달 [컨텍스트](api-management-policy-expressions.md#ContextVariables)합니다. hello 백 엔드 서비스 URL에에서 지정 된 API hello [설정](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) hello를 사용 하 여 변경할 수 [백 엔드 서비스 설정](api-management-transformation-policies.md) 정책입니다.  
  
> [!NOTE]
>  Hello outbound 섹션에서 toohello 백 엔드 서비스 및 hello 정책 전달 되지 않고 hello 요청에서이 정책 결과 hello의 hello 정책 hello 성공적으로 완료 시 즉시 평가 되 제거 섹션 인바운드 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>예  
  
#### <a name="example"></a>예제  
 hello 다음 API 수준 정책을 모든 요청 전달 toohello 백 엔드 서비스의 제한 시간 간격은 60 초입니다.  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>예제  
 이 작업 수준 정책 hello를 사용 하 여 `base` hello 부모 API 수준 범위에서 요소 tooinherit hello 백 엔드 정책입니다.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>예제  
 명시적으로이 작업 수준 정책 120 시간 제한은 모든 toohello 백 엔드 서비스 요청을 전달 하 고 hello 부모 수준의 백 엔드 API 정책을 상속 되지 않습니다.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>예제  
 이 작업 수준 정책 요청을 전달 하지 않는 toohello 백 엔드 서비스입니다.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|forward-request|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|timeout="integer"|hello 시간 제한 간격 (초)를 hello 전화 toohello 백 엔드 서비스에 오류가 발생합니다.|아니요|시간 초과 없음|  
|follow-redirects="true &#124; false"|Hello 백 엔드 서비스 로부터의 리디렉션 hello 게이트웨이 뒤 되는지 또는 toohello 호출자에 게 반환을 지정 합니다.|아니요|false|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** backend  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="LimitConcurrency"></a> 동시성 제한  
 hello `limit-concurrency` 정책에서 실행 하 여 지정된 된 시간에 지정 된 요청 수를 hello 보다 더 많은 괄호로 묶은 정책으로 인해 합니다. Hello 임계값 초과, 시 hello 최대 큐 길이 얻을 때까지 새 요청 tooa 큐에 추가 됩니다. 큐가 고갈되면 새 요청은 즉시 실패합니다.
  
###  <a name="LimitConcurrencyStatement"></a> 정책 문  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>예  
  
####  <a name="ChooseExample"></a> 예  
 hello 다음 예제 요청 수가 toolimit hello 컨텍스트 변수 값에 따라 tooa 백 엔드를 전달 하는 방법을입니다.
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|    
|limit-concurrency|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|--------------|  
|key|문자열입니다. 허용되는 식입니다. Hello 동시성 범위를 지정합니다. 여러 정책에서 공유될 수 있습니다.|예|해당 없음|  
|max-count|정수입니다. 허용 되는 tooenter hello 정책 요청의 최대 수를 지정 합니다.|예|해당 없음|  
|시간 제한|정수입니다. 허용되는 식입니다. Hello 요청 tooenter는 범위와 함께 실패 하기 전에 대기 해야 하는 시간 (초) 수를 지정 "403 너무 많은 요청"|아니요|Infinity|  
|max-queue-length|정수입니다. 허용되는 식입니다. Hello 최대 큐 길이 지정합니다. 들어오는 요청 tooenter 시도 된이 정책을 종료 됩니다 "403 너무 많은 요청" hello 큐 소진 되 면 즉시 합니다.|아니요|Infinity|  
  
###  <a name="ChooseUsage"></a> 사용 방법  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  

##  <a name="log-to-eventhub"></a>로그 tooEvent 허브  
 hello `log-to-eventhub` hello 메시지 형식 tooan 이벤트 허브로 거 엔터티에 의해 정의 된 지정 된 정책 보냅니다. 이름에서 알 수 있듯이 온라인 또는 오프 라인 분석을 위해 선택한 요청 또는 응답 컨텍스트 정보를 저장 하기 위한 hello 정책이 사용 됩니다.  
  
> [!NOTE]
>  이벤트 허브 및 이벤트 로깅 구성에 단계별 가이드를 참조 하십시오. [어떻게 Azure 이벤트 허브 API 관리 이벤트 toolog](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/)합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>예제  
 이벤트 허브에 기록 하는 hello 값 toobe로 모든 문자열을 사용할 수 있습니다. 이 예에서 hello 날짜 및 시간, 배포 서비스 이름, 요청 id, ip 주소 및 모든 인바운드 통화에 대 한 작업 이름을 로깅된 toohello 이벤트 허브로 거 hello로 등록 `contoso-logger` id입니다.  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|log-to-eventhub|루트 요소입니다. 이 요소의 값이 hello는 hello 문자열 toolog tooyour 이벤트 허브입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|  
|---------------|-----------------|--------------|  
|logger-id|hello의 hello id로 거 API 관리 서비스에 등록 합니다.|예|  
|partition-id|메시지를 보낼 위치 hello 파티션의 hello 인덱스를 지정 합니다.|선택 사항입니다. `partition-key`가 사용된 경우에는 이 특성을 사용할 수 없습니다.|  
|파티션 키|메시지를 보낼 경우 파티션 할당을 위해 사용 되는 hello 값을 지정 합니다.|선택 사항입니다. `partition-id`가 사용된 경우에는 이 특성을 사용할 수 없습니다.|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  

##  <a name="mock-response"></a> 모의 응답  
hello `mock-response`의미 hello 이름으로,은, toomock Api 및 작업을 사용 합니다. 일반 파이프라인 실행을 중단 하 고 모의 응답 toohello 호출자를 반환 합니다. hello 정책에는 항상 가장 높은 충실도의 tooreturn 응답 시도합니다. 가능한 경우 응답 콘텐츠 예제를 선호합니다. 스키마가 제공되고 예제가 제공되지 않은 경우 스키마에서 샘플 응답을 생성합니다. 예제와 스키마가 둘 다 없는 경우 콘텐츠가 없는 응답이 반환됩니다.
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>예  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|mock-response|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|--------------|  
|status-code|응답 상태 코드를 지정 하 고 해당 예제에 사용 되는 tooselect 또는 스키마는 키를 누릅니다.|아니요|200|  
|content-type|지정 `Content-Type` 응답 헤더 값 및 해당 예제에 사용 되는 tooselect 또는 스키마와 합니다.|아니요|없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, on-error  
  
-   **정책 범위:** 모든 범위

##  <a name="Retry"></a> 다시 시도  
 hello `retry` 자식 정책에 한 번 실행 하 고 hello 재시도까지 실행을 다시 시도 정책 `condition` 됩니다 `false` 을 다시 시도 또는 `count` 사용 되었습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a>예제  
 Hello에 다음 예제 요청 forewarding tooten 지 수의 다시 시도 알고리즘을 사용 하 여 시간을 다시 시도 합니다. 이후 `first-fast-retry` toofalse, 설정 된 모든 다시 시도 횟수는 주체 toohello exponsntial 다시 시도 알고리즘입니다.  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|retry|루트 요소입니다. 자식 요소로 다른 정책을 포함할 수 있습니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|condition|재시도를 중지(`false`) 또는 진행(`true`)해야 하는지 여부를 지정하는 부울 리터럴 또는 [식](api-management-policy-expressions.md)입니다.|예|해당 없음|  
|count|재시도 tooattempt hello 최대 수를 지정 하는 양수입니다.|예|해당 없음|  
|interval|양수 hello 재시도 사이의 hello 대기 간격 (초)에서입니다.|예|해당 없음|  
|max-interval|양수 hello 재시도 사이의 hello 최대 대기 간격 (초)에서입니다. 지 수 재시도 알고리즘 tooimplement를 사용 하는 경우|아니요|해당 없음|  
|delta|양수에 hello 대기 간격 증가 지정 하는 시간 (초)입니다. 사용 되는 tooimplement hello 선형 및 지 수 재시도 알고리즘은|아니요|해당 없음|  
|first-fast-retry|경우 너무 설정 `true` , 첫 번째 다시 시도 hello 즉시 수행 됩니다.|아니요|`false`|  
  
> [!NOTE]
>  Hello만 경우 `interval` 지정 된 **고정** 간격은 다시 시도 수행 합니다.  
>  때만 hello `interval` 및 `delta` 지정는 **선형** 다시 시도 작업 사이의 대기 시간에 따라 계산 된 hello 인 간격은 다시 시도 알고리즘을 사용 다음 수식을- `interval + (count - 1)*delta`합니다.  
>  Hello 때 `interval`, `max-interval` 및 `delta` 지정 된 **지 수** 간격은 다시 시도 알고리즘 적용 hello 다시 시도 작업 사이의 대기 시간 hello 의hello값에서기하급수적으로증가`interval`toohello 값 `max-interval` toohello 다음에 따라 forumula- `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`합니다.  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) 합니다. 이 정책에 의해 자식 정책 사용 제한이 상속됩니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="ReturnResponse"></a> 반환 응답  
 hello `return-response` 정책 파이프라인 실행을 중단 하 고 기본 또는 사용자 지정 응답 toohello 호출자에 게 반환 합니다. 기본 응답은 본문 없는 `200 OK`입니다. 컨텍스트 변수나 정책 문을 통해 사용자 지정 응답을 지정할 수 있습니다. 둘 다 제공 되는 경우 hello 컨텍스트 변수 내에 포함 된 hello 응답 toohello 호출자에 게 반환 하기 전에 hello 정책 문에 의해 수정 됩니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>예  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|return-response|루트 요소입니다.|예|  
|set-header|[set-header](api-management-transformation-policies.md#SetHTTPheader) 정책 문.|아니요|  
|set-body|[set-body](api-management-transformation-policies.md#SetBody) 정책 문.|아니요|  
|set-status|[set-status](api-management-advanced-policies.md#SetStatus) 정책 문.|아니요|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|  
|---------------|-----------------|--------------|  
|response-variable-name|hello hello 컨텍스트 변수 이름에서 참조, 예를 들어, 업스트림 [보내기 요청](api-management-advanced-policies.md#SendRequest) 정책 및를 포함 하는 `Response` 개체|선택 사항입니다.|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="SendOneWayRequest"></a> 단방향 요청 전송  
 hello `send-one-way-request` 정책 toohello 응답을 받기 위해 대기 하지 않고 URL을 지정 하는 hello 제공 된 요청을 보냅니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>예제  
 이 샘플 정책 hello를 사용 하는 예제를 보여 줍니다. `send-one-way-request` 정책 toosend 메시지 tooa Slack: 채트 방 hello HTTP 응답 코드는 too500 보다 크거나 같은 경우입니다. 이 예제에 대 한 자세한 내용은 참조 하십시오. [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)합니다.  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|send-one-way-request|루트 요소입니다.|예|  
|url|hello 요청의 hello URL입니다.|mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.|  
|메서드|hello hello 요청에 대 한 HTTP 메서드입니다.|mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.|  
|머리글|요청 헤더. 여러 요청 헤더에 여러 헤더 요소를 사용합니다.|아니요|  
|body|hello 요청 본문입니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|새 요청 또는 hello 현재 요청의 복사본 인지 여부를 결정 합니다. 아웃 바운드 모드로 모드 = 복사 hello 요청 본문을 초기화 하지 않습니다.|아니요|새로 만들기|  
|name|Hello hello 헤더 toobe 집합 이름을 지정합니다.|예|해당 없음|  
|exists-action|Hello 헤더가 이미 지정 되어 때 어떤 작업 tootake를 지정 합니다. 이 특성 hello 다음 값 중 하나가 있어야 합니다.<br /><br /> -재정의할-hello 기존 헤더의 hello 값으로 바꿉니다.<br />-skip-기존 헤더 값 hello를 대체 하지 않습니다.<br />-추가-hello 값 toohello 기존 헤더 값을 추가 합니다.<br />-delete-hello 요청에서 hello 헤더를 제거합니다.<br /><br /> 설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 헤더에 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.|아니요|재정의|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="SendRequest"></a> 요청 전송  
 hello `send-request` 정책 toohello hello 시간 제한 값을 설정 하는 보다 더 이상 대기 URL을 지정 하는 hello 제공 된 요청을 보냅니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>예제  
 이 예제는 한 가지 방법은 tooverify 권한 부여 서버와 참조 토큰을 보여줍니다. 이 예제에 대 한 자세한 내용은 참조 하십시오. [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)합니다.  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|send-request|루트 요소입니다.|예|  
|url|hello 요청의 hello URL입니다.|mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.|  
|메서드|hello hello 요청에 대 한 HTTP 메서드입니다.|mode=copy인 경우 아니요이고 그렇지 않은 경우 예입니다.|  
|머리글|요청 헤더. 여러 요청 헤더에 여러 헤더 요소를 사용합니다.|아니요|  
|body|hello 요청 본문입니다.|아니요|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|새 요청 또는 hello 현재 요청의 복사본 인지 여부를 결정 합니다. 아웃 바운드 모드로 모드 = 복사 hello 요청 본문을 초기화 하지 않습니다.|아니요|새로 만들기|  
|response-variable-name="string"|없는 경우 `context.Response`가 사용됩니다.|아니요|해당 없음|  
|timeout="integer"|hello 제한 시간 간격 (초) hello 호출 전에 toohello URL 실패합니다.|아니요|60|  
|ignore-error|True 및 hello 요청 하면 오류가 발생 하는 경우:<br /><br /> -   response-variable-name이 지정된 경우 null 값을 포함합니다.<br />-   response-variable-name이 지정되지 않은 경우 context.Request가 업데이트되지 않습니다.|아니요|false|  
|name|Hello hello 헤더 toobe 집합 이름을 지정합니다.|예|해당 없음|  
|exists-action|Hello 헤더가 이미 지정 되어 때 어떤 작업 tootake를 지정 합니다. 이 특성 hello 다음 값 중 하나가 있어야 합니다.<br /><br /> -재정의할-hello 기존 헤더의 hello 값으로 바꿉니다.<br />-skip-기존 헤더 값 hello를 대체 하지 않습니다.<br />-추가-hello 값 toohello 기존 헤더 값을 추가 합니다.<br />-delete-hello 요청에서 hello 헤더를 제거합니다.<br /><br /> 설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 헤더에 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.|아니요|재정의|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="SetHttpProxy"></a> HTTP 프록시 설정  
 hello `proxy` 정책을 사용 하면 HTTP 프록시를 통해 전달 요청 toobackends tooroute 합니다. Hello 게이트웨이와 hello 프록시 간의 HTTP (HTTPS)만 사용할 수 있습니다. 기본 및 NTLM 인증만 해당됩니다.
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>예제  
Hello 사용 [속성](api-management-howto-properties.md) hello 사용자 이름 및 암호 tooavoid hello 정책 문서에 중요 한 정보를 저장의 값으로.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|proxy|루트 요소|예|  

### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|url="문자열"|Http://host:port hello 형태로 프록시 URL입니다.|예|해당 없음|  
|사용자 이름="문자열"|사용자 이름 toobe hello 프록시 인증에 사용 합니다.|아니요|해당 없음|  
|암호="문자열"|암호 toobe hello 프록시 인증에 사용 합니다.|아니요|해당 없음|  

### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** 모든 범위  

##  <a name="SetRequestMethod"></a> 요청 메서드 설정  
 hello `set-method` 정책을 사용 하면 한 요청에 대 한 toochange hello HTTP 요청 메서드입니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>예제  
 Hello를 사용 하 여이 샘플 정책을 `set-method` 정책 메시지 tooa Slack 채트 방 hello HTTP 응답 코드 보다 큰 경우 보내거나 같은 too500 모양의 예제가 나와 있습니다. 이 예제에 대 한 자세한 내용은 참조 하십시오. [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)합니다.  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|set-method|루트 요소입니다. hello 요소의 hello 값 hello HTTP 메서드를 지정 합니다.|예|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="SetStatus"></a> 상태 코드 설정  
 hello `set-status` 정책 집합 hello HTTP 상태 코드 toohello 값을 지정 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>예제  
 이 예에서는 어떻게 tooreturn hello 권한 부여 토큰이 유효 하지 않을 경우 401 응답 합니다. 자세한 내용은 참조 [hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|set-status|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|code="integer"|hello HTTP 상태 코드 tooreturn 합니다.|예|해당 없음|  
|reason="string"|Hello 이유 hello 상태 코드를 반환 하는 것에 대 한 설명입니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  

##  <a name="set-variable"></a> 변수 설정  
 hello `set-variable` 정책 선언는 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 변수를 통해 지정 된 값을 할당 하 고는 [식](api-management-policy-expressions.md) 또는 문자열 리터럴입니다. hello 식은 변환 리터럴을 포함 되어 있으면 tooa 문자열과 hello hello 값 됩니다 `System.String`합니다.  
  
###  <a name="set-variablePolicyStatement"></a> 정책 문  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a> 예  
 hello 다음 예제에서는 hello의 set-variable 정책을 인바운드 섹션. 이 set-variable 정책은 만듭니다는 `isMobile` 부울 [컨텍스트](api-management-policy-expressions.md#ContextVariables) 경우 hello tootrue 설정 된 변수 `User-Agent` 요청 헤더에 hello 텍스트 `iPad` 또는 `iPhone`합니다.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|set-variable|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|  
|---------------|-----------------|--------------|  
|name|hello 변수의 hello 이름입니다.|예|  
|값|hello 변수의 hello 값입니다. 식 또는 리터럴 값일 수 있습니다.|예|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
###  <a name="set-variableAllowedTypes"></a> 허용 형식  
 Hello에 사용 된 식은 `set-variable` 정책 hello 기본 형식 다음 중 하나를 반환 합니다.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a> 추적  
 hello `trace` hello에 문자열을 추가 하는 정책 [API 검사기](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) 출력 합니다. hello 정책 실행될지만 추적 트리거될 때, 즉, `Ocp-Apim-Trace` 존재 하며 너무 설정 되 고 요청 헤더`true` 및 `Ocp-Apim-Subscription-Key` 요청 헤더가 있고 hello 관리자 계정과 연결 된 유효한 키를 보유 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|추적|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|원본|문자열 리터럴 의미 있는 toohello 추적 뷰어 및 hello 메시지의 hello 원본을 지정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) 합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** 모든 범위  
  
##  <a name="Wait"></a> 대기  
 hello `wait` 정책 직계 자식 정책의 병렬로 실행 하 고 완료 되기 전에 전체 또는 해당 직계 자식 정책 toocomplete 중 하나에 대 한 대기 합니다. hello 대기 정책으로 가질 수 직계 자식 정책의 [보내기 요청](api-management-advanced-policies.md#SendRequest), [캐시에서 값을 가져올](api-management-caching-policies.md#GetFromCacheByKey), 및 [제어 흐름](api-management-advanced-policies.md#choose) 정책입니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>예제  
 다음 예제는 hello에는 두 개의 `choose` hello의 직계 자식 정책으로는 정책 `wait` 정책입니다. 이러한 각 `choose` 정책이 병렬로 실행됩니다. 각 `choose` 정책 tooretrieve 캐시 된 값을 시도 합니다. 캐시 누락 하는 경우 백 엔드 서비스 tooprovide hello 값을 이라고 합니다. 이 예제에서는 hello에 `wait` 정책에 완료 되지 않으면 모든 직계 자식 정책의 완료 될 때까지 때문에 hello `for` 특성이 너무 설정 된`all`합니다.   이 예제에서는 hello 컨텍스트 변수에서 (`execute-branch-one`, `value-one`, `execute-branch-two`, 및 `value-two`)이 예에서는 정책 hello 범위 외부에서 선언 됩니다.  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a>요소  
  
|요소|설명|필수|  
|-------------|-----------------|--------------|  
|wait|루트 요소입니다. 자식 요소로 `send-request`, `cache-lookup-value`, `choose` 정책만 포함할 수 있습니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|for|같은지 hello `wait` 정책이 모든 직계 자식 정책 toobe 완료 될 때까지 대기 또는 하나만 있습니다. 허용되는 값은 다음과 같습니다.<br /><br /> -   `all`-모든 직계 자식 정책 toocomplete 때까지 대기<br />-모든-모든 직계 자식 정책 toocomplete 기다립니다. 첫 번째 직계 자식 정책은 hello 완료 되 면 hello `wait` 정책 완료 되 고 다른 직계 자식 정책의 실행이 종료 되었습니다.|아니요|모두|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend  
  
-   **정책 범위:** 모든 범위  
  
## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 다음을 참조하세요.
-   [API 관리의 정책](api-management-howto-policies.md) 
-   [정책 식](api-management-policy-expressions.md)
