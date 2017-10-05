---
title: "API 관리 서비스를 사용하여 HTTP 요청 생성"
description: "API 관리에서 요청 및 응답 정책을 사용하여 API에서 외부 서비스를 호출하는 방법을 알아봅니다."
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="f120c-103">Azure API 관리 서비스에서 외부 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="f120c-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="f120c-104">Azure API 관리 서비스에서 사용할 수 있는 정책은 순수하게 들어오는 요청, 보내는 응답 및 기본 구성 정보에 기반하여 다양한 범위의 유용한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="f120c-105">그러나 API 관리 정책에서 외부 서비스와 상호 작용할 수 있으면 더 많은 기회를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="f120c-106">[로깅, 모니터링 및 분석에 대한 Azure 이벤트 허브 서비스](api-management-log-to-eventhub-sample.md)와 상호 작용할 수 있는 방법은 이전에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="f120c-107">이 문서에서는 외부 HTTP 기반 서비스와 상호 작용할 수 있도록 하는 정책을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="f120c-108">이러한 정책은 원격 이벤트를 트리거하거나 원래 요청 및 응답을 몇 가지 방식으로 조작하는 데 사용할 정보를 검색하는 데에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="f120c-109">일방-요청-보내기</span><span class="sxs-lookup"><span data-stu-id="f120c-109">Send-One-Way-Request</span></span>
<span data-ttu-id="f120c-110">아마도 가장 간단한 외부 상호 작용은 외부 서비스가 일종의 중요한 이벤트 알림을 받을 수 있도록 하는 자체 유도 스타일의 요청일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="f120c-111">제어 흐름 정책 `choose` 을 사용하여 관심이 있는 모든 종류의 조건을 탐지한 다음 조건을 만족하는 경우 [일방-요청-보내기](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) 정책을 사용하여 외부 HTTP 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="f120c-112">Hipchat 및 Slack과 같은 메시징 시스템에 대한 요청이나 SendGrid 및 MailChimp와 같은 메일 API, 또는 PagerDuty와 같은 중요한 지원 인시던트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="f120c-113">이러한 메시징 시스템에는 모두 쉽게 호출할 수 있는 간단한 HTTP API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="f120c-114">Slack에 경고</span><span class="sxs-lookup"><span data-stu-id="f120c-114">Alerting with Slack</span></span>
<span data-ttu-id="f120c-115">다음 예제에서는 HTTP 응답 상태 코드가 500 이상인 경우 Slack 대화방에 메시지를 보내는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="f120c-116">500 범위 오류는 API의 클라이언트가 자체로 해결할 수 없는 백 엔드 API에 문제가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="f120c-117">일반적으로 일부에 일종의 개입이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="f120c-118">Slack에는 인바운드 웹 후크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="f120c-119">인바운드 웹 후크를 구성할 때 Slack은 간단한 게시 요청을 수행하고 Slack 채널에 메시지를 전달하는 특별한 URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="f120c-120">만든 JSON 본문은 Slack에서 정의된 형식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Slack 웹 후크](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="f120c-122">자체 유도로 충분합니까?</span><span class="sxs-lookup"><span data-stu-id="f120c-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="f120c-123">자체 유도 스타일의 요청을 사용할 때 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="f120c-124">어떤 이유가 있는 경우 요청이 실패한 다음 실패가 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="f120c-125">이 특정 상황에서는 보조 오류 보고 시스템이 가진 복잡성 및 응답을 기다리는 추가 성능 비용이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="f120c-126">응답을 확인하는 데 중요한 시나리오의 경우 [전송-요청](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 정책이 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="f120c-127">전송-요청</span><span class="sxs-lookup"><span data-stu-id="f120c-127">Send-Request</span></span>
<span data-ttu-id="f120c-128">`send-request` 정책을 사용하면 복잡한 처리 기능을 수행하는 외부 서비스를 사용할 수 있고 이후 정책 처리에 사용할 수 있는 API 관리 서비스에 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="f120c-129">참조 토큰 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f120c-129">Authorizing reference tokens</span></span>
<span data-ttu-id="f120c-130">API 관리의 주요 기능은 백 엔드 리소스를 보호하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="f120c-131">API에서 사용하는 권한 부여 서버가 [Azure Active Directory](../active-directory/active-directory-aadconnect.md)처럼 [JWT 토큰](http://jwt.io/)을 해당 OAuth2 흐름의 일부로 만드는 경우 `validate-jwt` 정책을 사용하여 토큰의 유효성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="f120c-132">그러나 일부 권한 부여 서버는 권한 부여 서버에 다시 호출하지 않으면 확인할 수 없는 [참조 토큰](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) 이라는 것을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="f120c-133">표준화된 검사</span><span class="sxs-lookup"><span data-stu-id="f120c-133">Standardized introspection</span></span>
<span data-ttu-id="f120c-134">과거에는 권한 부여 서버를 사용하여 참조 토큰을 확인하는 표준화된 방법이 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="f120c-135">그러나 최근에 제안된 표준 [RFC 7662](https://tools.ietf.org/html/rfc7662) 는 리소스 서버가 토큰의 유효성을 검사하는 방법을 정의하는 IETF에서 게시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="f120c-136">토큰 추출</span><span class="sxs-lookup"><span data-stu-id="f120c-136">Extracting the token</span></span>
<span data-ttu-id="f120c-137">첫 번째 단계는 권한 부여 헤더에서 토큰을 추출하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="f120c-138">헤더 값은 `Bearer` 권한 부여 체계, 공백 및 권한 부여 토큰을 [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1)단위로 형식이 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="f120c-139">하지만 권한 부여 체계를 생략하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="f120c-140">구문 분석할 때 이를 세려면 헤더 값을 공간에 분할하고 반환된 문자열 배열에서 마지막 문자열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="f120c-141">잘못된 형식의 권한 부여 헤더에 대한 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="f120c-142">유효성 검사 요청하기</span><span class="sxs-lookup"><span data-stu-id="f120c-142">Making the validation request</span></span>
<span data-ttu-id="f120c-143">권한 부여 토큰이 있다면 토큰의 유효성 검사를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="f120c-144">RFC 7662은 프로세스 검사를 호출하고 검사 리소스에 `POST` HTML 양식을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="f120c-145">HTML 양식은 키 `token`를 통해 적어도 키/값 쌍을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="f120c-146">또한 권한 부여 서버에 대한 요청은 인증되어 악의적인 클라이언트가 유효한 토큰을 방해할 수 없도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="f120c-147">응답 확인</span><span class="sxs-lookup"><span data-stu-id="f120c-147">Checking the response</span></span>
<span data-ttu-id="f120c-148">`response-variable-name` 특성은 반환된 응답의 액세스를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="f120c-149">이 속성에 정의된 이름은 `context.Variables` 사전에 키로 사용하여 `IResponse` 개체에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="f120c-150">응답 개체에서 본문을 검색할 수 있고 RFC 7622는 응답이 JSON 개체를 해야 하며 최소한 부울 값인 `active` 라는 속성을 포함해야 한다고 알립니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="f120c-151">`active` 가 true인 경우 토큰이 유효한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="f120c-152">오류 보고</span><span class="sxs-lookup"><span data-stu-id="f120c-152">Reporting failure</span></span>
<span data-ttu-id="f120c-153">`<choose>` 정책을 사용하여 토큰이 유효한지 감지하고 그럴 경우 401 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="f120c-154">또한 `bearer` 토큰을 사용해야 하는 방법을 설명하는 [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3)대로 401 응답을 사용하여 `WWW-Authenticate` 헤더를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="f120c-155">WWW 인증은 클라이언트에게 적절한 권한이 있는 요청을 생성하는 방법을 지시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="f120c-156">OAuth2 프레임워크에 다양한 접근 방법이 가능하기 때문에 필요한 모든 정보를 통신하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="f120c-157">다행스럽게도 [클라이언트가 리소스 서버에 대한 요청 권한을 제대로 부여하는 방법을 검색](http://tools.ietf.org/html/draft-jones-oauth-discovery-00)하도록 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="f120c-158">최종 솔루션</span><span class="sxs-lookup"><span data-stu-id="f120c-158">Final solution</span></span>
<span data-ttu-id="f120c-159">모든 요소를 결합하여 다음 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="f120c-160">`send-request` 정책이 API 관리 서비스를 통해 흐르는 요청 및 응답 프로세스에 유용한 외부 서비스를 통합하는 데 사용할 수 있는 방법에 대한 여러 가지 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="f120c-161">응답 컴퍼지션</span><span class="sxs-lookup"><span data-stu-id="f120c-161">Response Composition</span></span>
<span data-ttu-id="f120c-162">이전 예제에서 살펴본 대로 `send-request` 정책은 백 엔드 시스템에 대한 기본 요청을 개선하기 위해 사용되거나 백 엔드 호출의 전체 바꾸기로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="f120c-163">이 기술을 사용하여 여러 다른 시스템에서 집계되는 복합 리소스를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="f120c-164">대시보드 작성</span><span class="sxs-lookup"><span data-stu-id="f120c-164">Building a dashboard</span></span>
<span data-ttu-id="f120c-165">예를 들어 대시보드를 통하여 여러 백 엔드 시스템에 존재하는 정보를 노출시키려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="f120c-166">KPI는 모두 다른 백 엔드에서 가져오지만 직접 액세스를 제공하는 편을 선호하지 않으며 단일 요청에서 모든 정보를 검색할 수 있는 경우가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="f120c-167">아마도 일부 백 엔드 정보는 먼저 조각화 및 분할 및 처리가 필요합니다!</span><span class="sxs-lookup"><span data-stu-id="f120c-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="f120c-168">해당 복합 리소스를 캐시할 수 있으면 사용자는 성능이 저하된 메트릭이 변경되는지 알아보기 위해 F5 키를 계속 누르는 습관이 있기 때문에 백 엔드 부하를 줄이는데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="f120c-169">리소스 가장</span><span class="sxs-lookup"><span data-stu-id="f120c-169">Faking the resource</span></span>
<span data-ttu-id="f120c-170">대시보드 리소스를 구축하는 첫 단계는 API 관리 게시자 포털에서 새 작업을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="f120c-171">동적 리소스를 작성하는 컴퍼지션 정책을 구성하는 데 사용되는 자리 표시자 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![대시보드 작업](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="f120c-173">요청하기</span><span class="sxs-lookup"><span data-stu-id="f120c-173">Making the requests</span></span>
<span data-ttu-id="f120c-174">`dashboard` 작업이 만들어지면 해당 작업에 대해 특별히 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![대시보드 작업](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="f120c-176">첫 번째 단계는 들어오는 요청에서 쿼리 매개 변수를 추출하므로 백 엔드에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="f120c-177">이 예에서 대시보드는 시간의 경과에 따라 정보를 보여주며 따라서 `fromDate` 및 `toDate` 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="f120c-178">`set-variable` 정책을 사용하여 요청 URL에서 정보를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="f120c-179">이 정보가 있는 경우 모든 백 엔드 시스템에 요청을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="f120c-180">각 요청은 매개 변수 정보를 포함하는 새 URL을 생성하고 관련 서버를 호출하며 컨텍스트 변수의 응답을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="f120c-181">이러한 요청은 순서 대로 실행되며 이는 가장 좋은 방법은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="f120c-182">예정된 릴리스에서 이러한 요청을 병렬로 실행할 수 있도록 하는 `wait` 라는 새 정책을 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="f120c-183">응답</span><span class="sxs-lookup"><span data-stu-id="f120c-183">Responding</span></span>
<span data-ttu-id="f120c-184">복합 응답을 생성하려면 [반환-응답](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="f120c-185">`set-body` 요소는 속성으로 포함 된 모든 구성 요소 표현을 사용하여 새 `JObject`을 생성하도록 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="f120c-186">완성된 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="f120c-187">데이터의 특성이 한 시간 전에 만료되더라도 사용자에게 중요한 정보를 전달하는 데 충분히 효율적이기 때문에 자리 표시자 작업의 구성에서 대시보드 리소스를 최소 한 시간 동안 캐시되도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="f120c-188">요약</span><span class="sxs-lookup"><span data-stu-id="f120c-188">Summary</span></span>
<span data-ttu-id="f120c-189">Azure API 관리 서비스는 HTTP 트래픽에 선택적으로 적용할 수 있는 유연한 정책을 제공하고 백 엔드 서비스의 컴퍼지션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="f120c-190">함수, 확인, 유효성 검사 기능의 경고를 통해 API 게이트웨이를 개선하거나 여러 백 엔드 서비스를 기반으로 새 복합 리소스를 만들 경우 `send-request` 및 관련된 정책은 새로운 가능성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f120c-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="f120c-191">이러한 정책에 대한 동영상 개요 시청</span><span class="sxs-lookup"><span data-stu-id="f120c-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="f120c-192">이 문서에서 다루는 [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 및 [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) 정책에 대한 자세한 내용은 다음 동영상을 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="f120c-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

