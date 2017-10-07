---
title: "Azure API 관리 정책에 처리 aaaError | Microsoft Docs"
description: "어떻게 하는 동안 발생할 수 있는 toorespond tooerror 조건을 hello Azure API 관리에서 요청을 처리에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>API Management 정책에서 오류 처리
Azure API 관리를 사용 하면 게시자를 제공 하 여 요청 toohello 프록시의 hello 처리 하는 동안 발생할 수 있는 toorespond tooerror 조건을 `ProxyError` 개체입니다. hello `ProxyError` hello를 통해 개체가 액세스 되 [컨텍스트. LastError](api-management-policy-expressions.md#ContextVariables) 속성 hello에 대 한 정책에서 사용할 수 있습니다 및 `on-error` 정책 섹션. 이 항목에서는 참조 hello 오류에 대 한 Azure API 관리에서 처리 기능.  
  
## <a name="error-handling-in-api-management"></a>API Management에서 오류 처리  
 Azure API 관리의 정책으로 나뉩니다 `inbound`, `backend`, `outbound`, 및 `on-error` hello 다음 예제와 같이 섹션.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 요청의 hello 처리 하는 동안 기본 제공 단계 hello 요청에 대 한 범위에 있는 모든 정책을 함께 실행 됩니다. 오류가 발생 하면 즉시 처리 toohello 바로 이동 `on-error` 정책 섹션. hello `on-error` 정책 섹션을 두 범위 모두에서 사용할 수 있으며 API 게시자 hello 오류 tooevent 허브 로깅 또는 새 응답 tooreturn toohello 호출자 생성과 같은 사용자 지정 동작을 구성할 수 있습니다.  
  
> [!NOTE]
>  hello `on-error` 섹션은 기본적으로는 정책에 포함 되지 않습니다. tooadd hello `on-error` tooa 정책 섹션 hello 정책 편집기에서 원하는 toohello 정책 찾아 추가 합니다. 정책 구성에 대한 자세한 내용은 [API Management에서 정책](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/)을 참조하세요.  
>   
>  `on-error` 섹션이 없는 경우 오류 조건이 발생하면 호출자는 400 또는 500 HTTP 응답 메시지를 수신하게 됩니다.  
  
### <a name="policies-allowed-in-on-error"></a>오류 발생 시 허용되는 정책  
 hello 다음 정책에서에서 사용할 수 있습니다 hello `on-error` 정책 섹션.  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 때 오류가 발생 하 고 제어가 이동 toohello `on-error` 정책 섹션 hello 오류에 저장 된 [컨텍스트. LastError](api-management-policy-expressions.md#ContextVariables) hello에 대 한 정책에 의해 액세스할 수 있는 속성 `on-error` 섹션 및 다음과 같은 속성 hello 했습니다.  
  
|이름|형식|설명|필수|  
|----------|----------|-----------------|--------------|  
|원본|string|이름은 hello 요소 hello 오류가 발생 합니다. 정책 또는 기본 제공 파이프라인 단계 이름일 수 있습니다.|예|  
|이유|string|오류 처리에 사용될 수 있는 컴퓨터에 익숙한 오류 코드입니다.|아니요|  
|Message|string|사람이 읽을 수 있는 오류 설명입니다.|예|  
|범위|string|여기서 hello 오류가 발생 했으며 작업이 "전역", "product", "api" 또는 "작업이" 중 하나가 hello 범위의 이름|아니요|  
|섹션|string|오류가 발생한 섹션 이름으로 "inbound", "backend", "outbound" 또는 "on-error" 중 하나일 수 있습니다.|아니요|  
|Path|string|중첩된 정책(예: "choose[3]/when[2]")을 지정합니다.|아니요|  
|PolicyId|string|값의 hello `id` 특성이 hello 고객 오류가 발생 하는 hello 정책에 의해 지정 된 경우이 특성|아니요|  
  
> [!NOTE]
>  모든 정책에는 선택적 있습니까 `id` hello 정책 toohello 루트 요소를 추가할 수 있는 특성입니다. Hello 특성의 값을 hello hello를 사용 하 여 검색할 수 있으면이 특성이 정책에서 오류 조건이 발생할 때 `context.LastError.PolicyId` 속성입니다.  
  
## <a name="predefined-errors-for-built-in-steps"></a>기본 제공 단계에 대해 미리 정의된 오류  
 hello 다음과 같은 오류가 미리 정의 된 기본 제공 처리 단계의 hello 평가 하는 동안 발생할 수 있는 오류 조건에 대 한 합니다.  
  
|원본|조건|이유|Message|  
|------------|---------------|------------|-------------|  
|구성|Tooany Api 또는 작업 Uri와 일치 하지 않습니다.|OperationNotFound|없습니다 toomatch 들어오는 요청 tooan 작업입니다.|  
|권한 부여|구독 키가 제공되지 않음|SubscriptionKeyNotFound|액세스가 toomissing 구독 키 인해 거부 되었습니다. 요청 toothis API를 만들 때 있는지 tooinclude 구독 키를 확인 합니다.|  
|권한 부여|구독 키 값이 잘못됨|SubscriptionKeyInvalid|액세스가 tooinvalid 구독 키 인해 거부 되었습니다. 활성 구독에 대 한 유효한 키 tooprovide 있는지를 확인 합니다.|  
  
## <a name="predefined-errors-for-policies"></a>정책에 대해 미리 정의된 오류  
 hello 다음과 같은 오류는 미리 정의 되어 정책 평가 하는 동안 발생할 수 있는 오류 조건에 대 한 합니다.  
  
|원본|조건|이유|Message|  
|------------|---------------|------------|-------------|  
|rate-limit|속도 제한 초과|RateLimitExceeded|속도 제한을 초과했습니다.|  
|quota|할당량이 초과됨|QuotaExceeded|호출 볼륨 할당량을 초과했습니다. 할당량이 xx:xx:xx에서 보충됩니다. 또는 대역폭 할당량을 초과했습니다. 할당량이 xx:xx:xx에서 보충됩니다.|  
|jsonp|콜백 매개 변수 값이 잘못되었습니다(잘못된 문자 포함).|CallbackParameterInvalid|콜백 매개 변수 {callback-parameter-name} 값이 올바른 JavaScript 식별자가 아닙니다.|  
|ip-filter|요청에서 실패 한 tooparse 호출자 IP|FailedToParseCallerIP|Hello 호출자에 대 한 tooestablish IP 주소에 실패 했습니다. 액세스가 거부되었습니다.|  
|ip-filter|호출자 IP가 허용 목록에 없음|CallerIpNotAllowed|호출자 IP 주소 {ip-address}이(가) 허용되지 않습니다. 액세스가 거부되었습니다.|  
|ip-filter|호출자 IP가 차단 목록에 있음|CallerIpBlocked|호출자 IP 주소가 차단되었습니다. 액세스가 거부되었습니다.|  
|check-header|필수 헤더가 없거나 값이 누락됨|HeaderNotFound|Hello 요청에 헤더 {헤더-name을 (를) 찾지 못했습니다. 액세스가 거부되었습니다.|  
|check-header|필수 헤더가 없거나 값이 누락됨|HeaderValueNotAllowed|{header-value}의 헤더 {header-name} 값이 허용되지 않습니다. 액세스가 거부되었습니다.|  
|validate-jwt|요청에 Jwt 토큰이 없음|TokenNotFound|JWT hello 요청에서 찾을 수 없습니다. 액세스가 거부되었습니다.|  
|validate-jwt|서명 유효성 검사에 실패|TokenSignatureInvalid|<jwt 라이브러리의 메시지\>. 액세스가 거부되었습니다.|  
|validate-jwt|잘못된 대상 그룹|TokenAudienceNotAllowed|<jwt 라이브러리의 메시지\>. 액세스가 거부되었습니다.|  
|validate-jwt|잘못된 발급자|TokenIssuerNotAllowed|<jwt 라이브러리의 메시지\>. 액세스가 거부되었습니다.|  
|validate-jwt|토큰 만료됨|TokenExpired|<jwt 라이브러리의 메시지\>. 액세스가 거부되었습니다.|  
|validate-jwt|서명 키가 ID로 확인되지 않았음|TokenSignatureKeyNotFound|<jwt 라이브러리의 메시지\>. 액세스가 거부되었습니다.|  
|validate-jwt|토큰에서 필수 클레임이 누락됨|TokenClaimNotFound|JWT 토큰 클레임에 따라 hello 없습니다: < c1\>, < c2\>,... 액세스가 거부되었습니다.|  
|validate-jwt|클레임 값이 일치하지 않음|TokenClaimValueNotAllowed|{claim-value}의 클레임 {claim-name} 값이 허용되지 않습니다. 액세스가 거부되었습니다.|  
|validate-jwt|기타 유효성 검사 실패|JwtInvalid|<jwt 라이브러리의 메시지\>|

## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  