---
title: "Azure 관리-Microsoft 위협 모델링 도구-aaaSession | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>보안 프레임: 세션 관리 | Articles 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Azure AD를 사용하는 경우에 ADAL 메서드를 사용하여 적절한 로그아웃 구현](#logout-adal)</li></ul> |
| IoT 장치 | <ul><li>[생성된 SaS 토큰에 대해 한정된 수명 사용](#finite-tokens)</li></ul> |
| **Azure Document DB** | <ul><li>[생성된 리소스 토큰에 대해 최소 토큰 수명 사용](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[ADFS를 사용하는 경우에 WsFederation 메서드를 사용하여 적절한 로그아웃 구현](#wsfederation-logout)</li></ul> |
| **Identity Server** | <ul><li>[ID 서버를 사용하는 경우 적절한 로그아웃 구현](#proper-logout)</li></ul> |
| **웹 응용 프로그램** | <ul><li>[HTTPS를 통해 사용할 수 있는 응용 프로그램은 보안 쿠키를 사용해야 함](#https-secure-cookies)</li><li>[모든 http 기반 응용 프로그램은 쿠키 정의에 대해서 http만을 지정해야 함](#cookie-definition)</li><li>[ASP.NET 웹 페이지에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화](#csrf-asp)</li><li>[비활성 수명에 대한 세션 설정](#inactivity-lifetime)</li><li>[Hello 응용 프로그램에서 적절 한 로그 아웃 구현](#proper-app-logout)</li></ul> |
| **앱 API** | <ul><li>[ASP.NET Web API에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화](#csrf-api)</li></ul> |

## <a id="logout-adal">Azure AD를 사용하는 경우에 ADAL 메서드를 사용하여 적절한 로그아웃 구현</a>

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure AD | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello 로그 아웃 이벤트 처리기를 호출 해야 hello 응용 프로그램이 Azure AD에서 발급 하는 액세스 토큰을 사용 하는 경우 |

### <a name="example"></a>예제
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>예제
Session.Abandon() 메서드를 호출하여 사용자의 세션을 삭제해야 합니다. 다음 메서드에서는 사용자 로그아웃의 보안 구현을 보여 줍니다.
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>생성된 SaS 토큰에 대해 한정된 수명 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | IoT 장치 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | IoT Hub tooAzure 인증에 대해 생성 된 SaS 토큰 유한한 만료 기간이 있어야 합니다. Hello SaS 토큰 수명 tooa 최소 toolimit hello 양을 hello 토큰이 손상 된 경우에 재생 될 시간을 유지 합니다.|

## <a id="resource-tokens"></a>생성된 리소스 토큰에 대해 최소 토큰 수명 사용

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Azure Document DB | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 리소스 토큰 tooa 필요한 최소값의 hello timespan을 줄입니다. 리소스 토큰은 기본 1시간의 유효한 시간을 갖습니다.|

## <a id="wsfederation-logout"></a>ADFS를 사용하는 경우에 WsFederation 메서드를 사용하여 적절한 로그아웃 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ADFS | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | Hello 응용 프로그램 ad FS에서 발급 한 STS 토큰을 사용 하는 경우 아웃 hello 사용자 WSFederationAuthenticationModule.FederatedSignOut() 메서드 toolog hello 로그 아웃 이벤트 처리기에 호출 해야 합니다. 또한 hello 현재 세션 제거 되어야 할지, 및 hello 세션 토큰 값 다시 설정 하 고 있어 해야 합니다.|

### <a name="example"></a>예제
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>ID 서버를 사용하는 경우 적절한 로그아웃 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | ID 서버 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [IdentityServer3-페더레이션된 로그아웃](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **단계** | 외부 id 공급자와 hello 기능 toofederate IdentityServer을 지원합니다. 사용자가 업스트림 id 공급자에서 로그 오프을 사용 하는 hello 프로토콜에 따라 것 가능한 tooreceive 알림을 hello 사용자가 로그 아웃 하는 경우. IdentityServer toonotify도를 서명할 수 있으므로 여기에 클라이언트 hello 아웃 사용자 수 있습니다. Hello 구현 세부 사항에 대 한 hello references 섹션에 hello 설명서를 참조 합니다.|

## <a id="https-secure-cookies"></a>HTTPS를 통해 사용할 수 있는 응용 프로그램은 보안 쿠키를 사용해야 함

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | EnvironmentType - OnPrem |
| **참조**              | [httpCookies 요소(ASP.NET 설정 스키마)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure 속성](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **단계** | 쿠키는 일반적으로 범위가 지정 된만 액세스할 수 있는 toohello 도메인입니다. 안타깝게도, "도메인"의 hello 정의 HTTPS를 통해 생성 되는 쿠키는 HTTP를 통해 액세스할 수 있도록 hello 프로토콜을 포함 되지 않습니다. hello "보안" 특성은 쿠키를 hello toohello 브라우저만 사용 가능 해야 HTTPS를 통해 나타냅니다. HTTPS를 통해 설정 된 모든 쿠키 hello를 사용 하는지 확인 **보안** 특성입니다. hello 요구 사항 hello requireSSL 특성 tootrue를 설정 하 여 hello web.config 파일에 적용 될 수 있습니다. Hello hello를 적용 하기 때문에 접근 방식을 선호는 **보안** 추가 코드 변경 내용을 hello 필요 toomake 없이 모든 현재 및 미래의 쿠키에 대 한 특성입니다.|

### <a name="example"></a>예제
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
hello 설정은 HTTP 사용 되는 tooaccess hello 응용 프로그램은 경우에 적용 됩니다. HTTP를 사용 하는 경우 tooaccess hello 응용 프로그램을 hello hello 응용 프로그램 hello 보안 특성과 hello 브라우저와 hello 쿠키 설정을 보내지 않으므로 해당 설정을 나누기 다시 toohello 응용 프로그램.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 웹 양식, MVC5 |
| **특성**              | EnvironmentType - OnPrem |
| **참조**              | 해당 없음  |
| **단계** | requireSSL tooTrue 설정 하 여 hello FedAuth 토큰의 보안 특성을 구성할 수 hello 웹 응용 프로그램은 신뢰 당사자 hello hello IdP는 ADFS 서버를 `system.identityModel.services` web.config의 섹션:|

### <a name="example"></a>예제
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>모든 http 기반 응용 프로그램은 쿠키 정의에 대해서 http만을 지정해야 함

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [보안 쿠키 특성](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **단계** | toomitigate hello 정보 공개 위험을 교차 사이트 스크립팅 (XSS) 공격을 새 특성-httpOnly-도입된 toocookies가 있으며 모든 주요 브라우저에서 지원 됩니다. hello 특성 쿠키에 스크립트를 통해 액세스할 수 있는지를 지정 합니다. 웹 응용 프로그램 HttpOnly 쿠키를 사용 하 여 hello 가능성 hello 쿠키에 포함 된 중요 한 정보가 스크립트를 통해 도난 및 tooan 공격자의 웹 사이트에 전송 될 수를 줄입니다. |

### <a name="example"></a>예제
쿠키를 사용 하는 모든 HTTP 기반 응용 프로그램은 HttpOnly 다음 web.config에서 구성을 구현 하 여 hello 쿠키 정의에 지정 해야 합니다.
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 웹 양식 |
| **특성**              | 해당 없음  |
| **참조**              | [FormsAuthentication.RequireSSL 속성](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **단계** | hello RequireSSL 속성 값은 hello 구성 요소의 hello requireSSL 특성을 사용 하 여 ASP.NET 응용 프로그램에 대 한 hello 구성 파일에 설정 됩니다. 지정할 수 있습니다 hello Web.config 파일에서 ASP.NET 응용 프로그램에 대 한 SSL (Secure Sockets Layer) hello requireSSL 특성을 설정 하 여 필요한 tooreturn hello 폼 인증 쿠키 toohello 서버 인지 합니다.|

### <a name="example"></a>예제 
hello 다음 코드 예제에서는 hello requireSSL 특성 hello Web.config 파일에 있습니다.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5 |
| **특성**              | EnvironmentType - OnPrem |
| **참조**              | [WIF(Windows Identity Foundation) 구성 – 2부](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **단계** | tooset httpOnly 특성 FedAuth 쿠키, hideFromCsript 특성 값을 설정 해야 tooTrue 합니다. |

### <a name="example"></a>예제
다음 구성은 hello 올바른 구성을 보여 줍니다.
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>ASP.NET 웹 페이지에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 교차 사이트 요청 위조 (CSRF 또는 XSRF)는 hello 보안 컨텍스트에서 다른 사용자의 웹 사이트에서 설정 된 세션의 동작 하면 공격자가 수행할 수 있는 공격의 형식입니다. hello 목표 toomodify 또는 hello 대상된 웹 사이트는 세션 쿠키 tooauthenticate 받은 요청에서 단독으로 사용 하는 경우 콘텐츠를 삭제 합니다. 공격자에 hello 사용자가 이미 로그인 취약 한 사이트를 다른 사용자의 브라우저 tooload 명령 사용 하 여 URL을 가져와이 취약점을 악용할 수 있습니다. 여러 가지 방법으로 공격자가 toodo,와 같은 다른 웹 사이트를 호스트 하 여 하에서 리소스를 로드 hello 취약 한 서버 또는 가져오는 hello 사용자 tooclick 링크에 대 한 합니다. hello 서버 추가 토큰 toohello 클라이언트 전송, 모든 향후 요청에서 해당 토큰 클라이언트 tooinclude hello 및 앞으로 모든 요청에 관련 된 toohello 현재 세션 등으로 토큰 포함 확인 필요 경우 hello 공격을 방지할 수 있습니다. hello AntiForgeryToken ASP.NET ViewState를 사용합니다. |

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET MVC 및 웹 페이지에서 XSRF/CSRF 방지](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **단계** | 앤티 CSRF 및 ASP.NET MVC 폼에서 사용 하 여 hello `AntiForgeryToken` ; 축 자를 뷰에 대 한 도우미 메서드는 `Html.AntiForgeryToken()` hello 양식으로|

### <a name="example"></a>예제
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>예제
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>예제
Hello에 이와 Html.AntiForgeryToken() 제공 hello 방문자 쿠키 __RequestVerificationToken 위에 표시 된 hello 임의의 숨겨진된 값과 같은 값인 hello로 호출 합니다. 다음으로, 들어오는 폼 게시, toovalidate hello [ValidateAntiForgeryToken] 필터 toohello 대상 작업 메서드를 추가 합니다. 예:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
다음을 확인하는 권한 부여 필터:
* hello 들어오는 요청에 __RequestVerificationToken 라는 쿠키
* hello 들어오는 요청에는 `Request.Form` __RequestVerificationToken 라는 항목
* 이러한 쿠키 및 `Request.Form` 가정 모든 값 일치가 잘, hello 요청은 정상적으로 합니다. 하지만 그렇지 않으면 "필수 위조 방지 토큰을 제공하지 않았거나 올바르지 않습니다."라는 메시지와 함께 인증이 실패합니다. 

### <a name="example"></a>예제
앤티 CSRF 및 AJAX: hello 폼 토큰 AJAX 요청 JSON 데이터를 HTML 양식 데이터가 아닌으로 보낼 수 있으므로 AJAX 요청에 대 한 문제가 될 수 있습니다. 한 가지 해결 방법은 사용자 지정 HTTP 헤더에서 toosend hello 토큰입니다. hello 다음 코드 Razor 구문 toogenerate hello 토큰을 사용 하 고 hello 토큰 tooan AJAX 요청을 추가 합니다. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>예제
Hello 요청을 처리할 때 hello 요청 헤더에서 hello 토큰을 추출 합니다. 다음 toovalidate hello 토큰 hello AntiForgery.Validate 메서드를 호출 합니다. Validate 메서드 hello hello 토큰이 유효 하지 않은 경우 예외가 throw 됩니다.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 웹 양식 |
| **특성**              | 해당 없음  |
| **참조**              | [Take 이점은의 ASP.NET 기본 제공 기능 tooFend 오프 웹 공격](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **단계** | 각 사용자-사용자 ID에 대해 달라 지는 ViewStateUserKey tooa 임의 문자열을 설정 하 여 WebForm 기반 응용 프로그램에서 CSRF 공격을 완화할 수 있습니다 또는 더 잘 아직 세션 id입니다. 다양한 기술적 및 사회적 원인으로 인해 세션 ID가 예측할 수 있고 시간이 초과하며 각 사용자에 따라 다르기 때문에 훨씬 더 적합합니다.|

### <a name="example"></a>예제
모든 페이지에 toohave 필요한 hello 코드는 다음과 같습니다.
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>비활성 수명에 대한 세션 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [HttpSessionState.Timeout 속성](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **단계** | 세션 제한 시간 hello 사용자를 수행 하지 않는 모든 작업 웹 사이트 (웹 서버에 의해 정의 됨) 간격 동안 때 이벤트 발생을 나타냅니다. 서버 쪽에서 이벤트 hello hello 사용자 세션 too'invalid의 hello 상태 변경,' (예를 들어 "더 이상 사용 되지") 하 고 하도록 명령 hello 웹 서버 toodestroy (에 포함 된 모든 데이터가 삭제) 합니다. hello 다음 코드 예제에서는 hello 시간 제한 세션 특성 too15 분 hello Web.config 파일에 있습니다.|

### <a name="example"></a>예제
```XML 코드 <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 웹 양식 |
| **특성**              | 해당 없음  |
| **참조**              | [인증(ASP.NET 설정 스키마)에 대한 양식 요소](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **단계** | Forms 인증 쿠키 시간 제한 too15 hello 분 설정|

### <a name="example"></a>예제
```XML 코드 <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>예제
또한 SAML 클레임 토큰의 수명을 발급 ADFS too15 설정 해야 하는 hello hello 다음 hello ADFS 서버에서 powershell 명령을 실행 하 여 분:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Hello 응용 프로그램에서 적절 한 로그 아웃 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 사용자가 로그 아웃 단추가 적절 한 로그 아웃 hello 응용 프로그램에서 수행 합니다. 로그아웃 시 응용 프로그램은 사용자의 세션을 삭제하고 인증 쿠키 값을 다시 설정하고 무효화하는 동시에 세션 쿠키 값을 다시 설정하고 무효화해야 합니다. 또한 여러 세션 제한은 tooa 단일 사용자 id 인 경우 이러한 전체적으로 끝나야 hello 서버 쪽 제한 시간 또는 로그 아웃 합니다. 마지막으로 로그아웃 기능을 모든 페이지에 사용할 수 있는지 확인합니다. |

## <a id="csrf-api"></a>ASP.NET Web API에서 CSRF(교차 사이트 요청 위조) 공격에 대해 완화

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | 교차 사이트 요청 위조 (CSRF 또는 XSRF)는 hello 보안 컨텍스트에서 다른 사용자의 웹 사이트에서 설정 된 세션의 동작 하면 공격자가 수행할 수 있는 공격의 형식입니다. hello 목표 toomodify 또는 hello 대상된 웹 사이트는 세션 쿠키 tooauthenticate 받은 요청에서 단독으로 사용 하는 경우 콘텐츠를 삭제 합니다. 공격자에 hello 사용자가 이미 로그인 취약 한 사이트를 다른 사용자의 브라우저 tooload 명령 사용 하 여 URL을 가져와이 취약점을 악용할 수 있습니다. 여러 가지 방법으로 공격자가 toodo,와 같은 다른 웹 사이트를 호스트 하 여 하에서 리소스를 로드 hello 취약 한 서버 또는 가져오는 hello 사용자 tooclick 링크에 대 한 합니다. hello 서버 추가 토큰 toohello 클라이언트 전송, 모든 향후 요청에서 해당 토큰 클라이언트 tooinclude hello 및 앞으로 모든 요청에 관련 된 toohello 현재 세션 등으로 토큰 포함 확인 필요 경우 hello 공격을 방지할 수 있습니다. hello AntiForgeryToken ASP.NET ViewState를 사용합니다. |

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET Web API에서 CSRF(교차 사이트 요청 위조) 공격 방지](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **단계** | 앤티 CSRF 및 AJAX: hello 폼 토큰 AJAX 요청 JSON 데이터를 HTML 양식 데이터가 아닌으로 보낼 수 있으므로 AJAX 요청에 대 한 문제가 될 수 있습니다. 한 가지 해결 방법은 사용자 지정 HTTP 헤더에서 toosend hello 토큰입니다. hello 다음 코드 Razor 구문 toogenerate hello 토큰을 사용 하 고 hello 토큰 tooan AJAX 요청을 추가 합니다. |

### <a name="example"></a>예제
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>예제
Hello 요청을 처리할 때 hello 요청 헤더에서 hello 토큰을 추출 합니다. 다음 toovalidate hello 토큰 hello AntiForgery.Validate 메서드를 호출 합니다. Validate 메서드 hello hello 토큰이 유효 하지 않은 경우 예외가 throw 됩니다.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>예제
앤티 CSRF 및 ASP.NET MVC 양식-사용 하 여 hello 뷰의; AntiForgeryToken 도우미 메서드 예를 들어 hello 양식에 Html.AntiForgeryToken() 배치
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>예제
위의 hello 예제는 hello 다음과 같은 내용이 출력 됩니다.
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>예제
Hello에 이와 Html.AntiForgeryToken() 제공 hello 방문자 쿠키 __RequestVerificationToken 위에 표시 된 hello 임의의 숨겨진된 값과 같은 값인 hello로 호출 합니다. 다음으로, 들어오는 폼 게시, toovalidate hello [ValidateAntiForgeryToken] 필터 toohello 대상 작업 메서드를 추가 합니다. 예:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
다음을 확인하는 권한 부여 필터:
* hello 들어오는 요청에 __RequestVerificationToken 라는 쿠키
* hello 들어오는 요청에는 `Request.Form` __RequestVerificationToken 라는 항목
* 이러한 쿠키 및 `Request.Form` 가정 모든 값 일치가 잘, hello 요청은 정상적으로 합니다. 하지만 그렇지 않으면 "필수 위조 방지 토큰을 제공하지 않았거나 올바르지 않습니다."라는 메시지와 함께 인증이 실패합니다.

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC5, MVC6 |
| **특성**              | ID 공급자 - ADFS, ID 공급자 - Azure AD |
| **참조**              | [개별 계정을 사용하는 Web API 및 ASP.NET Web API 2.2에서 로컬 로그인 보호](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **단계** | 웹 API hello 보안이 설정 된 OAuth 2.0을 사용 하는 경우 다음 그에서는 전달자 토큰에서 권한 부여 요청 헤더 및 부여 액세스 toohello 요청 hello 토큰이 유효한 경우에 합니다. 브라우저는 쿠키를 기반으로 인증과 달리 hello 전달자 토큰 toorequests를 연결 하지 마십시오. hello 클라이언트 해야 tooexplicitly 요청 hello 전달자 토큰 hello 요청 헤더에 연결 합니다. 따라서 ASP.NET Web API가 OAuth 2.0을 사용하여 보호되는 경우 전달자 토큰은 CSRF 공격에 대한 방어로 간주됩니다. Hello MVC 부분의 hello 응용 프로그램에서 폼 인증 (즉, 사용 하 여 쿠키)를 사용 하는 경우 위조 방지 토큰이 hello MVC 웹 응용 프로그램에서 사용 하는 toobe note 하십시오. |

### <a name="example"></a>예제
hello 웹 API에 toobe toorely 정보를 쿠키 아니라 전달자 토큰에만 해당 합니다. 구성에 따라 hello 하 여 수행할 수 있습니다 `WebApiConfig.Register` 메서드: ' ' C 형 코드 구성 합니다. SuppressDefaultHostAuthentication(); 구성 합니다. (새 HostAuthenticationFilter(OAuthDefaults.AuthenticationType)); Filters.Add
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
