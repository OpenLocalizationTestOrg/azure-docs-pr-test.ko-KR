---
title: "API 관리 변환 정책 aaaAzure | Microsoft Docs"
description: "Azure API 관리에 사용할 수 있는 hello 변환 정책에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>API Management 변환 정책
이 항목에서는 다음 API 관리 정책 hello에 대 한 대 한 참조를 제공 합니다. 정책의 추가 및 구성에 대한 자세한 내용은 [API 관리 정책](http://go.microsoft.com/fwlink/?LinkID=398186)을 참조하세요.  
  
##  <a name="TransformationPolicies"></a> 변환 정책  
  
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
  
##  <a name="ConvertJSONtoXML"></a>JSON tooXML 변환  
 hello `json-to-xml` JSON tooXML에서 요청 또는 응답 본문을 변환 하는 정책입니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|json-to-xml|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|apply|다음 값에는 hello tooone hello 특성을 설정 해야 합니다.<br /><br /> - always: 항상 전환을 적용합니다.<br />- content-type-json: 응답 Content-Type 헤더에서 JSON의 존재를 나타내는 경우에만 변환합니다.|예|해당 없음|  
|consider-accept-header|다음 값에는 hello tooone hello 특성을 설정 해야 합니다.<br /><br /> - true: 요청 Accept 헤더에서 JSON을 요청하는 경우 변환을 적용합니다.<br />- false: 항상 전환을 적용합니다.|아니요|true|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, on-error  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="ConvertXMLtoJSON"></a>XML tooJSON 변환  
 hello `xml-to-json` 정책 XML tooJSON에서 요청 또는 응답 본문을 변환 합니다. 이 정책을 사용 하는 toomodernize XML 전용 백 엔드 웹 서비스를 기반으로 Api 될 수 있습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|xml-to-json|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|kind|다음 값에는 hello tooone hello 특성을 설정 해야 합니다.<br /><br /> javascript-활용이 편한-hello 변환 JSON 양식 tooJavaScript 친숙 한 개발자가 있습니다.<br />-직접-hello 변환 된 JSON 구조를 반영 hello 원래 XML 문서의 합니다.|예|해당 없음|  
|apply|다음 값에는 hello tooone hello 특성을 설정 해야 합니다.<br /><br /> - always: 항상 변환합니다.<br />- content-type-xml: 응답 Content-Type 헤더에서 XML의 존재를 나타내는 경우에만 변환합니다.|예|해당 없음|  
|consider-accept-header|다음 값에는 hello tooone hello 특성을 설정 해야 합니다.<br /><br /> - true: 요청 Accept 헤더에서 XML을 요청하는 경우 변환을 적용합니다.<br />- false: 항상 전환을 적용합니다.|아니요|true|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, on-error  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="Findandreplacestringinbody"></a> 본문 문자열 찾기 및 바꾸기  
 hello `find-and-replace` 정책 요청 또는 응답 하위 문자열을 찾아서 다른 하위 문자열로 바꿉니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>예  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|find-and-replace|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|from|hello에 대 한 문자열 toosearch 합니다.|예|해당 없음|  
|to|hello 대체 문자열입니다. 빈 대체 문자열 tooremove hello 검색 문자열을 지정 합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="MaskURLSContent"></a> 콘텐츠의 URL 마스킹  
 hello `redirect-content-urls` toohello hello 게이트웨이 통해 동일한 링크를 가리키는지 있도록 정책 hello 응답 본문에 (마스킹) 링크를 다시 작성 합니다. Hello outbound 섹션 toore 쓰기 응답 본문 링크 toomake의 해당 지점 toohello 게이트웨이 사용 합니다. Hello에서 사용 하 여 인바운드 반대의 결과 대 한 섹션.  
  
> [!NOTE]
>  이 정책은 `Location` 헤더와 같은 헤더 값을 변경하지 않습니다. toochange 헤더 값을 사용 하 여 hello [집합 헤더](api-management-transformation-policies.md#SetHTTPheader) 정책입니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>예  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|redirect-content-urls|루트 요소입니다.|예|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="SetBackendService"></a> 백 엔드 서비스 설정  
 사용 하 여 hello `set-backend-service` 정책 tooredirect 들어오는 hello 해당 작업에 대 한 hello API 설정에 지정 된 것 보다 tooa 다른 백 엔드를 요청 합니다. 이 정책은 hello 정책에 지정 된 hello 들어오는 요청 toohello의 hello 백 엔드 서비스 기준 URL을 변경 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>예제  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
이 예제에서는 hello 집합 백 엔드 서비스 정책은 hello 하나에 지정 된 hello API 보다 hello 쿼리 문자열 tooa 다른 백 엔드 서비스에 전달 된 hello 버전 값에 따라 요청을 라우팅합니다.
  
처음 hello 백 엔드 서비스 기준 URL hello API 설정에서 파생 됩니다. 따라서 요청 URL을 hello `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` 됩니다 `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` 여기서 `http://contoso.com/api/10.4/` hello API 설정에 지정 된 hello 백 엔드 서비스 URL입니다.  
  
Hello 때 [< 선택\> ](api-management-advanced-policies.md#choose) 정책 문을 적용 hello 백 엔드 서비스 기준 URL 변경 될 수 있습니다 다시 하나 너무`http://contoso.com/api/8.2` 또는 `http://contoso.com/api/9.1`hello hello 버전 요청 쿼리 매개 변수 값에 따라 합니다. 예를 들어 hello 값은 `"2013-15"` hello 최종 요청 URL은 `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`합니다.  
  
가 있으면 추가 hello 요청의 변환 하려는 경우에 다른 [변환 정책](api-management-transformation-policies.md#TransformationPolicies) 사용할 수 있습니다. 예를 들어 tooremove hello 버전 쿼리 매개 변수 hello 요청 되 고 했으므로 라우팅된 tooa 버전별 백 엔드로, hello [쿼리 문자열 매개 변수를 설정](api-management-transformation-policies.md#SetQueryStringParameter) 정책을 사용 하는 tooremove hello 현재 중복 version 특성을 수 있습니다.  
  
### <a name="example"></a>예제  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
이 예제에서는 hello 정책 경로 hello 요청 tooa 서비스 패브릭 백 엔드에 hello 파티션 키로 hello userId 쿼리 문자열을 사용 하 고 사용 하 여 hello 파티션의 주 복제본을 hello 합니다.  

### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|set-backend-service|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|base-url|새 백 엔드 서비스 기준 URL입니다.|아니요|해당 없음|  
|backend-id|hello 백 엔드 tooroute의 식별자입니다.|아니요|해당 없음|  
|sf-partition-key|Hello 백 엔드 서비스 패브릭 서비스에 있고 ' 백 엔드-i d '를 사용 하 여 지정 된 경우에 적용할 수 있습니다. Tooresolve hello 이름 확인 서비스에서 특정 파티션을 사용합니다.|아니요|해당 없음|  
|sf-replica-type|Hello 백 엔드 서비스 패브릭 서비스에 있고 ' 백 엔드-i d '를 사용 하 여 지정 된 경우에 적용할 수 있습니다. Hello 요청이 파티션의 toohello 기본 또는 보조 복제본을 전달 해야 하는 경우를 제어 합니다. |아니요|해당 없음|    
|sf-resolve-condition|Hello 백 엔드 서비스 패브릭 서비스는 때에 적용 가능 합니다. 조건 식별 hello tooService 패브릭 백 엔드를 호출 하는 경우에 새로운 해결이 반복 toobe 있습니다.|아니요|해당 없음|    
|sf-service-instance-name|Hello 백 엔드 서비스 패브릭 서비스는 때에 적용 가능 합니다. 런타임 시 toochange 서비스 인스턴스를 허용 합니다. |아니요|해당 없음|    

### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, backend  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="SetBody"></a> 본문 설정  
 사용 하 여 hello `set-body` 들어오고 나가는 요청에 대 한 정책 tooset hello 메시지 본문입니다. tooaccess hello hello를 사용할 수 있습니다 메시지 본문 `context.Request.Body` 속성 또는 hello `context.Response.Body`hello 정책 hello 인지에 따라 인바운드 또는 아웃 바운드 섹션.  
  
> [!IMPORTANT]
>  액세스 하는 경우 기본적으로 사용 하 여 메시지 본문 hello는 `context.Request.Body` 또는 `context.Response.Body`, hello 원래 메시지 본문이 손실 되 고 hello 본문 hello 식에 다시 반환 하 여 설정 해야 합니다. toopreserve hello 본문 콘텐츠를 설정 hello `preserveContent` 매개 변수가 너무`true` hello 메시지에 액세스할 때. 경우 `preserveContent` 너무 설정`true` hello 본문 사용 되는 반환 된 다른 본문 hello 식에 의해 반환 됩니다.  
>   
>  Hello 고려 사항 hello를 사용 하는 경우 다음 사항에 유의 하세요 `set-body` 정책입니다.  
>   
>  -   Hello를 사용 하는 경우 `set-body` 정책 tooreturn tooset 않아도 새로운 또는 업데이트 된 본문 `preserveContent` 너무`true` hello 새 본문 콘텐츠를 명시적으로 제공 하는 때문에 있습니다.  
> -   Hello 인바운드 파이프라인에 대 한 응답의 hello 내용은 보존은 바람직하지 않습니다 응답이 아직 있기 때문입니다.  
> -   Hello 아웃 바운드 파이프라인에 있는 요청의 hello 내용은 보존은 바람직하지 않습니다 hello 요청이 이미 전송 되었습니다. toohello 백 엔드가 시점에서 때문에 있습니다.  
> -   인바운드 GET에서와 같이 메시지 본문이 없을 때 이 정책을 사용하면 예외가 발생합니다.  
  
 자세한 내용은 참조 hello `context.Request.Body`, `context.Response.Body`, hello 및 `IMessage` hello의 섹션 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables) 테이블 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>예  
  
#### <a name="literal-text-example"></a>리터럴 텍스트 예제  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>문자열로 서 hello 본문에 액세스 하는 예입니다. Note म hello 파이프라인의 뒷부분에 나오는 액세스할 수 있도록 hello 원래 요청 본문을 유지는 있습니다.
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Jobject 인 본문 hello를 액세스 하는 예입니다. Hello 원래 요청 본문을 액세스 하면 예외가 발생 합니다 hello 파이프라인에 나중에 예약 되지 म 이후 note입니다.  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>제품 기준 응답 필터링  
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

### <a name="using-liquid-templates-with-set-body"></a>본문이 설정된 Liquid 템플릿 사용 
hello `set-body` 정책 구성 된 toouse hello 수 [유동](https://shopify.github.io/liquid/basics/introduction/) 템플릿 언어 tootransfom hello 요청 또는 응답의 본문입니다. 메시지의 모양 변경 hello 형식 toocompletely 해야 할 경우에 매우 유용할 수 있습니다.

> [!IMPORTANT]
> hello에 사용 된 액체 구현의 hello `set-body` 정책 'C# 모드'에서 구성 됩니다. 이러한 방식은 필터링과 같은 작업을 수행하는 경우에 특히 중요합니다. 예를 들어 파스칼 hello 사용 해야 날짜 필터를 사용 하 여 대/소문자와 C# 예: 서식을 날짜:
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> 순서 toocorrectly 바인딩 tooan XML 본문에 hello 유동 템플릿을 사용 하 여 사용 하 여 한 `set-header` 정책 tooset Content-type tooeither 응용 프로그램/xml, 텍스트/x m l (또는 모든 끝나는 유형의 + xml); JSON 본문 있어야 응용 프로그램/json, json 텍스트 / (또는 모든 형식 종료 와 + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>유동 템플릿을 사용 하 여 JSON tooSOAP 변환
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>Liquid 템플릿을 사용하여 JSON 변환
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|set-body|루트 요소입니다. Hello 본문 텍스트 또는 본문을 반환 하는 식을 포함 합니다.|예|  

### <a name="properties"></a>속성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|template|Hello 본문 정책 설정 사용 되는 toochange hello 템플릿 모드에서 실행 됩니다. 현재 hello만 지원 값이입니다.<br /><br />-유동-hello 설정 본문 정책 hello 유동 템플릿 엔진을 사용 합니다. |아니요|liquid|  

Hello 유동 템플릿을 hello 요청 및 응답에 대 한 정보에 액세스 하는 것에 대 한 다음과 같은 속성 hello로 tooa 컨텍스트 개체를 바인딩할 수 있습니다.: <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="SetHTTPheader"></a> HTTP 헤더 설정  
 hello `set-header` 정책 값 tooan 기존 응답 및/또는 요청 헤더를 지정 하거나 새 응답 및/또는 요청 헤더를 추가 합니다.  
  
 HTTP 헤더 목록을 HTTP 메시지에 삽입합니다. 인바운드 파이프라인에 배치 하는 경우이 정책은 toohello 대상 서비스에 전달 되 고 hello 요청에 대 한 hello HTTP 헤더를 설정 합니다. 아웃 바운드 파이프라인에 배치 하는 경우이 정책은 toohello 게이트웨이 클라이언트에 전송 되는 hello 응답에 대 한 hello HTTP 헤더를 설정 합니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>예  
  
#### <a name="example"></a>예제  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>컨텍스트 정보 toohello 백 엔드 서비스를 전달 합니다.  
 이 예제는 hello API에서 tooapply 정책을 toosupply 컨텍스트 정보 toohello 백 엔드 서비스를 평준화 하는 방법을 보여 줍니다. 구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too10:30 빨리 감기 및 합니다. 12시 10분에는 데모 작업에서 hello 정책을 볼 수 있는 hello 개발자 포털에서 작업을 호출 합니다.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|set-header|루트 요소입니다.|예|  
|값|Hello 헤더 toobe 집합의 hello 값을 지정 합니다. 이름이 같은 hello 가진 여러 헤더에 대 한 더 추가 `value` 요소입니다.|예|  
  
### <a name="properties"></a>속성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|exists-action|Hello 헤더가 이미 지정 되어 때 어떤 작업 tootake를 지정 합니다. 이 특성 hello 다음 값 중 하나가 있어야 합니다.<br /><br /> -재정의할-hello 기존 헤더의 hello 값으로 바꿉니다.<br />-skip-기존 헤더 값 hello를 대체 하지 않습니다.<br />-추가-hello 값 toohello 기존 헤더 값을 추가 합니다.<br />-delete-hello 요청에서 hello 헤더를 제거합니다.<br /><br /> 설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 헤더에 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.|아니요|override|  
|name|Hello 헤더 toobe 집합의 이름을 지정합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound, backend, on-error  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="SetQueryStringParameter"></a> 쿼리 문자열 매개 변수 설정  
 hello `set-query-parameter` , 대체 값 정책 추가 또는 삭제 요청 쿼리 문자열 매개 변수입니다. 사용 되는 toopass 쿼리 hello 백 엔드 서비스에서 예상 하는 매개 변수는 선택 사항 또는 hello 요청에 없는 될 수 있습니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>예  
  
#### <a name="example"></a>예제  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>컨텍스트 정보 toohello 백 엔드 서비스를 전달 합니다.  
 이 예제는 hello API에서 tooapply 정책을 toosupply 컨텍스트 정보 toohello 백 엔드 서비스를 평준화 하는 방법을 보여 줍니다. 구성 하 고이 정책을 사용 하 여 데모를 보려면 참조 [클라우드 포괄 에피소드 177: Vlad Vinogradsky 통해 더 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too10:30 빨리 감기 및 합니다. 12시 10분에는 데모 작업에서 hello 정책을 볼 수 있는 hello 개발자 포털에서 작업을 호출 합니다.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 자세한 내용은 [정책 식](api-management-policy-expressions.md) 및 [컨텍스트 변수](api-management-policy-expressions.md#ContextVariables)를 참조하세요.  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|set-query-parameter|루트 요소입니다.|예|  
|값|Hello 쿼리 매개 변수 toobe 집합의 hello 값을 지정 합니다. 이름이 같은 hello로 여러 쿼리 매개 변수에 대 한 더 추가 `value` 요소입니다.|예|  
  
### <a name="properties"></a>속성  
  
|이름|설명|필수|기본값|  
|----------|-----------------|--------------|-------------|  
|exists-action|Hello 쿼리 매개 변수가 이미 지정한 경우에 어떤 작업 tootake를 지정 합니다. 이 특성 hello 다음 값 중 하나가 있어야 합니다.<br /><br /> -재정의-hello 기존 매개 변수 대체 hello 값입니다.<br />-skip-기존 hello 쿼리 매개 변수 값을 대체 하지 않습니다.<br />-추가-hello 값 toohello 기존 쿼리 매개 변수 값을 추가 합니다.<br />-delete-hello 요청에서 hello 쿼리 매개 변수를 제거합니다.<br /><br /> 설정 된 경우 너무`override` hello로 이름과 같은 이름을 결과 집합에 따라 tooall 항목 (하면 여러 번 나열) 되 고 hello 쿼리 매개 변수에서 여러 항목 나열; hello 결과에 나열 된 값만 설정 됩니다.|아니요|override|  
|name|Hello 쿼리 매개 변수 toobe 집합의 이름을 지정합니다.|예|해당 없음|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, backend  
  
-   **정책 범위:** global, product, API, operation  
  
##  <a name="RewriteURL"></a> URL 다시 쓰기  
 hello `rewrite-uri` 정책 hello 다음 예제와 같이 hello 웹 서비스에서 공용 형식 toohello 형식에서 요청 URL을 변환 합니다.  
  
-   공용 URL - `http://api.example.com/storenumber/ordernumber`  
  
-   요청 URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 이 정책은 hello 웹 서비스에 필요한 hello URL 형식으로 변환 해야 하는 사용자 및/또는 브라우저에 친숙 한 URL 때 사용할 수 있습니다. 이 정책은 toobe 클린 Url, RESTful Url, 사용자에 게 친숙 한 Url 또는 SEO에 게 친숙 한 Url을 쿼리 문자열을 포함 하지 않으며 대신 hello의만 hello 경로 포함 하는 등의 다른 URL 형식으로 노출 하는 경우 적용 필요 hello 체계 및 기관 hello) (이후 리소스입니다. 보통 미학, 사용 편의성 또는 SEO(검색 엔진 최적화)를 위해 사용합니다.  
  
> [!NOTE]
>  만 hello 정책을 사용 하 여 쿼리 문자열 매개 변수를 추가할 수 있습니다. 추가 템플릿 경로 매개 변수 hello에 URL 재작성을 추가할 수 없습니다.  

### <a name="policy-statement"></a>정책 문  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>예  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|rewrite-uri|루트 요소입니다.|예|  
  
### <a name="attributes"></a>특성  
  
|특성|설명|필수|기본값|  
|---------------|-----------------|--------------|-------------|  
|template|쿼리 문자열 매개 변수와 hello 실제 웹 서비스 URL입니다. 식을 사용 하는 경우 hello 전체 값 식 이어야 합니다.|예|해당 없음|  
|copy-unmatched-params|Toohello URL hello에 정의 된 서식 파일을 다시 작성 hello 원본 URL 서식 파일에 없는 hello 들어오는 요청의 쿼리 매개 변수가 추가 되는지 여부를 지정합니다|아니요|true|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound  
  
-   **정책 범위:** product, API, operation  
  
##  <a name="XSLTransform"></a> XSLT를 사용하여 XML 변환  
 hello `Transform XML using an XSLT` 정책은 XSL 변환을 tooXML hello 요청 또는 응답 본문에 적용 됩니다.  
  
### <a name="policy-statement"></a>정책 문  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>예  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>요소  
  
|이름|설명|필수|  
|----------|-----------------|--------------|  
|xsl-transform|루트 요소입니다.|예|  
|매개 변수|Hello 변환에서 사용 되는 사용 되는 toodefine 변수|아니요|  
|xsl:stylesheet|루트 스타일시트 요소입니다. 모든 요소와 특성 내에 정의 된 hello 표준에 따라 [XSLT 사양](http://www.w3.org/TR/xslt)|예|  
  
### <a name="usage"></a>사용  
 이 정책은 hello 정책 뒤에 사용할 수 있습니다 [섹션](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) 및 [범위](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)합니다.  
  
-   **정책 섹션:** inbound, outbound  
  
-   **정책 범위:** global, product, API, operation  
  
## <a name="next-steps"></a>다음 단계
정책으로 작업하는 방법에 대한 자세한 내용은 [API Management의 정책](api-management-howto-policies.md)을 참조하세요.  
