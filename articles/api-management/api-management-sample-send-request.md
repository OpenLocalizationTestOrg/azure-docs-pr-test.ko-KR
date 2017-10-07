---
title: "aaaUsing API 관리 서비스 HTTP toogenerate 요청"
description: "API에서 API 관리 toocall 외부 서비스에서 toouse 요청 및 응답 정책에 알아봅니다"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Hello Azure API 관리 서비스에서에서 외부 서비스를 사용 하 여
hello 정책 Azure API 관리 서비스에서 사용할 수 있는 다양 한 범위의 hello 들어오는 요청, hello 보내는 응답 및 기본 구성 정보에만 따라야 하는 유용한 작업을 수행할 수 있습니다. 그러나 API 관리에서 외부 서비스와 수 toointeract 되 고 정책을 열어서 많은 기회를 더 합니다.

어떻게 hello 상호 작용 하려면 이전에 관찰 한 [로깅, 모니터링 및 분석에 대 한 Azure 이벤트 허브 서비스](api-management-log-to-eventhub-sample.md)합니다. 이 문서에서 모든 외부 http toointeract를 허용 하는 정책 기반 서비스 보여 줍니다. 이러한 정책은 사용 하는 toomanipulate hello 원래 요청과 응답 어떤 방식으로든에서 될 정보를 검색 또는 원격 이벤트를 트리거할 기준이 사용할 수 있습니다.

## <a name="send-one-way-request"></a>일방-요청-보내기
예를 들어 hello 가장 간단한 외부 상호 작용이 hello 화재 하 고 잊어 스타일은 외부 서비스 toobe 중요 한 이벤트의 몇 가지 종류의 알림을 허용 하는 요청입니다. Hello 제어 흐름 정책은 사용할 수 `choose` hello를 사용 하 여 외부 HTTP 요청을 위해 모든 종류의 관심 있는 경우 hello 다음, 조건 및 조건이 충족 되는 toodetect [한 방식으로 요청 보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) 정책입니다. Hipchat 또는 여유 시간 또는 SendGrid 또는 MailChimp과 같은 메일 API와 같은 시스템 메시징 요청 tooa 이거나 PagerDuty 다음과 같은 중요 한 지원 요청에 대 한이 있습니다. 이러한 메시징 시스템에는 모두 쉽게 호출할 수 있는 간단한 HTTP API가 있습니다.

### <a name="alerting-with-slack"></a>Slack에 경고
다음 예제는 hello 메시지 tooa toosend hello HTTP 응답 상태 코드 보다 큰 경우 대화방 여유 또는 too500 값이 방법을 보여 줍니다. 500 범위 오류 우리의 백 엔드 API와 클라이언트 API의 hello 하는 문제 자체를 확인할 수 없는 것을 나타냅니다. 일반적으로 일부에 일종의 개입이 필요합니다.  

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

Slack에 인바운드 웹 후크 hello 개념이 있습니다. 인바운드 웹 후크를 구성할 때 Slack hello Slack 채널에 toodo 간단한 POST 요청 및 toopass 메시지 수 있는 특수 URL을 생성 합니다. hello 작성 하는 JSON 본문 Slack에 정의 된 형식을 기반으로 합니다.

![Slack 웹 후크](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>자체 유도로 충분합니까?
자체 유도 스타일의 요청을 사용할 때 장단점이 있습니다. 어떤 이유로 든 원하는 경우에 hello 요청이 실패 후 hello 오류가 보고 되지 않습니다. 이 특정 상황에서는 hello 복잡 한 보조 오류 보고 시스템와 hello 응답을 기다리는 hello 추가 성능 비용을 문제가 발생 해야 합니다. 필수 toocheck hello 응답이 시나리오에 대 한 hello [보내기 요청](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 정책 것이 더 좋습니다.

## <a name="send-request"></a>전송-요청
hello `send-request` 복잡 한 함수 및 추가 정책 처리에 사용할 수 있는 반환 데이터 toohello API 관리 서비스를 처리 하는 외부 서비스 tooperform를 사용 하 여 정책 사용 하도록 설정 합니다.

### <a name="authorizing-reference-tokens"></a>참조 토큰 권한 부여
API 관리의 주요 기능은 백 엔드 리소스를 보호하는 것입니다. API에서 사용 하는 hello 권한 부여 서버를 만드는 경우 [JWT 토큰](http://jwt.io/) 해당 OAuth2 흐름의 일환으로으로 [Azure Active Directory](../active-directory/active-directory-aadconnect.md) hello를 사용할 수 있습니다는 `validate-jwt` tooverify hello 정책 유효성 hello 토큰입니다. 그러나 일부 권한 부여 서버는 만들 [토큰](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) 호출 백 toohello 권한 부여 서버를 만들지 않고 확인할 수 없습니다.

### <a name="standardized-introspection"></a>표준화된 검사
지난 hello에는 표준화 된 권한 부여 서버와 참조 토큰을 확인할 방법이 없어 있었습니다. 그러나 최근에 제안 된 표준 [RFC 7662](https://tools.ietf.org/html/rfc7662) hello 리소스 서버는 토큰의 hello 유효성을 확인할 수는 방법을 정의 하는 IETF에서 게시 하였습니다.

### <a name="extracting-hello-token"></a>Hello 토큰을 추출합니다.
hello 첫 번째 단계는 hello 권한 부여 헤더에서 tooextract hello 토큰입니다. hello 헤더 값 hello 서식이 지정 되어야 `Bearer` 기준으로 권한 부여 체계, 공백 하나 및 다음 hello 권한 부여 토큰 [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1)합니다. 그러나 hello 권한 부여 체계를 생략 하면 경우가 있습니다. 이 대 한 tooaccount 나눌 문자열 배열을 반환 하는 hello에서 마지막 문자열 선택 hello와 공간 hello 헤더 값을 구문 분석할 때. 잘못된 형식의 권한 부여 헤더에 대한 해결 방법을 제공합니다.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Hello 유효성 검사 요청을 만드는
Hello 인증 토큰을 있으면 hello 요청 toovalidate hello 토큰을 만들 수 것입니다. RFC 7662이 프로세스 검사를 호출 하 고 있어야 하면 `POST` HTML 양식 toohello 검사 리소스입니다. HTML 폼 hello hello 키가 있는 키/값 쌍 이상 포함 되어야 `token`합니다. 이 요청 toohello 권한 부여 서버는 악의적인 클라이언트가 올바른 토큰에 대 한 trawling 이동 수 없는 인증된 tooensure 수도 있어야 합니다.

```xml
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
```

### <a name="checking-hello-response"></a>Hello 응답을 확인 하는 중
hello `response-variable-name` 특성은 사용 되는 toogive 액세스 hello 응답을 반환 합니다. hello이 속성에 정의 된 이름을 사용할 수 있습니다를 키로 hello `context.Variables` 사전 tooaccess hello `IResponse` 개체입니다.

Hello 본문 hello 응답 개체에서 검색할 수 있게 및 RFC 7622 알려줍니다. hello 응답 JSON 개체 여야 하 고 라는 속성이 하나 이상 있어야 합니다. `active` 부울 값입니다. 때 `active` hello 토큰은 유효한 것으로 간주 그렇습니다.

### <a name="reporting-failure"></a>오류 보고
사용 하 여 한 `<choose>` 정책 toodetect hello 토큰이 유효 하지 않을 경우 그리고 있다면 반환 401 응답 합니다.

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

기준으로 [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) 설명 하는 방법을 `bearer` 토큰 쓰일 수 또한 반환는 `WWW-Authenticate` hello 401 응답 헤더입니다. Www-authenticate hello은 의도 한 tooinstruct 방법에 대 한 클라이언트 요청을 적절 한 권한이 있는 tooconstruct 합니다. 광범위 한 접근 방식을 hello OAuth2 프레임 워크와 가능한 toohello, 기한 어렵습니다 toocommunicate hello 모든 필요한 정보와 합니다. 다행히 없는 노력 진행 toohelp [클라이언트 tooproperly 요청 tooa 리소스 서버를 인증 하는 방법을 검색](http://tools.ietf.org/html/draft-jones-oauth-discovery-00)합니다.

### <a name="final-solution"></a>최종 솔루션
모든 hello 조각을 결합을 얻을 수 있는 정책에 따라 hello:

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

이 여러 가지 방법 중 하나에 hello `send-request` 정책 요청 및 응답 hello API 관리 서비스를 통해 흐르는 hello 프로세스에 유용한 외부 서비스를 사용 하는 toointegrate 될 수 있습니다.

## <a name="response-composition"></a>응답 컴퍼지션
hello `send-request` 정책 hello 앞의 예제에서 살펴본 하거나 hello 백 엔드 호출에 대 한 전체 바꾸기로 사용 될 수 주 요청 tooa 백 엔드 시스템을 향상 시키는 데 사용할 수 있습니다. 이 기술을 사용하여 여러 다른 시스템에서 집계되는 복합 리소스를 쉽게 만들 수 있습니다.

### <a name="building-a-dashboard"></a>대시보드 작성
Toobe 수 tooexpose 정보 여러 백 엔드 시스템에 있는 예를 들어 toodrive 대시보드는 경우가 있습니다. hello Kpi는 모든 다른 백 엔드가, 하지만 하지 tooprovide 직접 액세스 toothem 방법을 하 있으며 좋을 단일 요청에서 모든 hello 정보를 검색할 수 없습니다. 아마도 hello 백 엔드 정보의 일부 일부 분할 및 분할 및 먼저 약간 정리 해야 합니다! Hello 백 엔드 복합 리소스 유용한 tooreduce 수 있다고 수 toocache 되 고 사용자가을 할애 하 여 underperforming 메트릭 변경 될 수 있습니다 하는 경우에 순서 toosee hello F5 키를 만들던 알고 로드 합니다.    

### <a name="faking-hello-resource"></a>Hello 리소스를 가장합니다.
첫 번째 단계 toobuilding hello 대시보드 리소스가 인지 tooconfigure hello API 관리 게시자 포털에서 새 작업을 합니다. 이 우리의 컴퍼지션 정책 toobuild 자리 표시자 사용 되는 작업 tooconfigure 됩니다 동적 리소스입니다.

![대시보드 작업](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Hello 요청
한 번 hello `dashboard` 작업이 만든 구체적으로 해당 작업에 대 한 정책을 구성할 수 있습니다. 

![대시보드 작업](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

hello 첫 번째 단계는 tooextract hello 들어오는 요청에서 모든 쿼리 매개 변수 이므로 tooour 백 엔드 전달할 수 있습니다. 이 예에서 대시보드는 시간의 경과에 따라 정보를 보여주며 따라서 `fromDate` 및 `toDate` 매개 변수가 있습니다. 사용 하는 hello `set-variable` hello 요청 URL에서 정책 tooextract hello 정보입니다.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

이 정보가 있으면 tooall hello 백 엔드 시스템 요청을 만들 수 있습니다. 각 요청 hello 매개 변수 정보를 사용 하 여 새 URL을 생성 하 고,에서 관련 서버를 호출 하 고, 상황에 맞는 변수에 저장 하는 hello 응답.

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

이러한 요청은 순서 대로 실행되며 이는 가장 좋은 방법은 아닙니다. 예정 된 릴리스에서 우리는 도입 해야 이라는 새 정책을 `wait` 모두 동시에 이러한 요청 tooexecute 수 있도록 합니다.

### <a name="responding"></a>응답
사용 하는 hello tooconstruct hello 복합 응답 [반환 응답](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) 정책. hello `set-body` 요소 식 tooconstruct צ ְ ײ 새 `JObject` 속성으로 포함 된 모든 hello 구성 요소 표현 합니다.

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

hello 완성 된 정책 모양은 다음과 같습니다.

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

구성 하 여 hello 자리 표시자 작업의 hello 구성 hello 대시보드 리소스 toobe 캐시에 대 한 최소한 1 시간 것은 한 시간에 만료 충분히 적용 됩니다 하는 경우에 hello 데이터의 hello 특성 의미 하는 점을 이해 하기 때문에 tooconvey 귀중 한 정보 toohello 사용자입니다.

## <a name="summary"></a>요약
선택적으로 될 수 있는 유연한 정책이 적용 tooHTTP 트래픽 하며 백 엔드 서비스의 조합 수 있도록 하는 azure API 관리 서비스입니다. 원하는 tooenhance 함수, 확인, 유효성 검사 기능 경고와 API 게이트웨이 또는 여러 백 엔드 서비스에 따라 새 복합 리소스 만들기를 hello `send-request` 관련된 정책 새로운 가능성을 엽니다.

## <a name="watch-a-video-overview-of-these-policies"></a>이러한 정책에 대한 동영상 개요 시청
Hello에 대 한 자세한 내용은 [한 방식으로 요청 보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [보내기 요청](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), 및 [반환 응답](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) 이 문서에서 다루는 정책을 hello 다음 비디오를 참조 하십시오.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

