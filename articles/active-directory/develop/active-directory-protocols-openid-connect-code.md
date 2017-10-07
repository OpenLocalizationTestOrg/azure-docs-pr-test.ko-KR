---
title: "Azure AD에서 인증 코드 흐름 OpenID Connect aaaUnderstand hello | Microsoft Docs"
description: "이 문서에서는 toouse HTTP 메시지 tooauthorize tooweb 응용 프로그램 및 Azure Active Directory 및 OpenID Connect를 사용 하 여 테 넌 트의 웹 Api에 액세스 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# OpenID Connect와 Azure Active Directory를 사용 하 여 tooweb 응용 프로그램 액세스 권한 부여
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) hello OAuth 2.0 프로토콜을 기반으로 구축 된 간단한 identity 계층입니다. OAuth 2.0 메커니즘 tooobtain 및 사용 하 여 정의 **액세스 토큰** tooaccess 보호 된 리소스, 하지만 표준 메서드 tooprovide id 정보를 정의 하지 않습니다. OpenID Connect 확장 toohello OAuth 2.0 권한 부여 프로세스도 인증을 구현합니다. Hello 형태로 hello 최종 사용자에 대 한 정보를 제공는 `id_token` hello 사용자의 hello id를 확인 하 고 hello 사용자에 대 한 기본 프로필 정보를 제공 합니다.

OpenID Connect는 서버에서 호스트되고 브라우저를 통해 액세스되는 웹 응용 프로그램을 빌드하는 경우 권장 사항입니다.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## OpenID Connect를 사용하는 인증 흐름
로그인 흐름에 단계를 수행 하는 hello-아래에서 자세히 설명 되어 각각의 가장 기본적인 사용 되는 번호입니다.

![OpenId Connect 인증 흐름](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## OpenID Connect 메타데이터 문서

OpenID Connect 대부분의 프로그램 앱 tooperform 로그인에 필요한 hello 정보를 포함 하는 메타 데이터 문서에 설명 합니다. 여기에 hello Url toouse hello 서비스의 공개 서명 키의 hello 위치 등의 정보가 포함 됩니다. hello OpenID Connect 메타 데이터 문서에서 찾을 수 있습니다.

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
hello 메타 데이터는 간단한 개체 JSON (JavaScript Notation) 문서. 다음 예에 대 한 조각 hello를 참조 하십시오. hello 조각의 내용을에서 자세히 설명 hello [OpenID Connect 사양](https://openid.net)합니다.

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Hello 로그인 요청 보내기
웹 응용 프로그램 tooauthenticate hello 사용자, 사용자 toohello hello를 지시 해야 `/authorize` 끝점입니다. 이 요청은 hello 비슷한 toohello 첫 번째 다리 [OAuth 2.0 권한 부여 코드 흐름](active-directory-protocols-oauth-code.md), 몇 가지 중요 한 차이가 있습니다.

* hello 요청 hello 범위에 포함 되어야 `openid` hello에 `scope` 매개 변수입니다.
* hello `response_type` 매개 변수에 포함 되어야 `id_token`합니다.
* hello 요청 hello에 포함 되어야 `nonce` 매개 변수입니다.

따라서 샘플 요청은 다음과 같습니다.

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  값은 테 넌 트 식별자, 예를 들어 hello 허용 `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 또는 `contoso.onmicrosoft.com` 또는 `common` 테 넌 트 독립적 토큰에 대 한 |
| client_id |필수 |hello 응용 프로그램 Id 할당된 tooyour 때 응용 프로그램 Azure AD에 등록 합니다. Hello Azure 포털에서에서이 찾을 수 있습니다. 클릭 **Azure Active Directory**, 클릭 **앱 등록**를 hello 응용 프로그램을 선택 하 고 hello 응용 프로그램 페이지에서 응용 프로그램 Id hello를 찾습니다. |
| response_type |필수 |OpenID Connect 로그인을 위한 `id_token` 이 포함되어야 합니다.  `code`와 같은 다른 response_types를 포함할 수도 있습니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다.  OpenID Connect hello 범위 포함 해야 `openid`, 이것은 hello 동의 UI에는 "로그인" 권한이 toohello 해석 합니다.  동의를 요청하기 위해 이 요청에 다른 범위를 포함할 수도 있습니다. |
| nonce |필수 |Hello 결과에 포함 된 hello 앱에서 생성 하는 hello 요청에 포함 된 값 `id_token` 을 클레임으로 합니다.  hello 앱이 값 toomitigate 토큰 재생 공격 확인할 수 있습니다.  일반적으로 hello 값은 임의 고유 문자열 또는 hello 요청의 사용된 tooidentify hello 원본 일 수 있는 GUID입니다. |
| redirect_uri |권장 |인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램의 hello redirect_uri입니다.  또한 url로 인코딩되어 있어야 점을 제외 하 고 hello 포털에 등록 된 hello redirect_uris 중 하나에 정확히 일치 해야 합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 authorization_code 백 tooyour 앱 되어야 하는 hello 방법을 지정 합니다.  지원되는 값은 *HTTP 폼 게시*의 경우 `form_post`이고 *URL 조각*의 경우 `fragment`입니다.  웹 응용 프로그램에 사용할 수 있는 권장 `response_mode=form_post` tooensure hello 토큰 tooyour 응용 프로그램의 가장 안전 하 게 전송 합니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다.  원하는 모든 콘텐츠의 문자열일 수 있습니다.  일반적으로 [교차 사이트 요청 위조 공격을 방지](http://tools.ietf.org/html/rfc6749#section-10.12)하기 위해 임의로 생성된 고유 값이 사용됩니다.  hello 상태 hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |
| prompt |선택 사항 |Hello 필요한 사용자 상호 작용 유형을 나타냅니다.  현재 유효한 값은 '로그인' 'none', 전용 hello 및 '승인'.  `prompt=login`hello 사용자 tooenter 자격 증명 요청을 부정 single sign-on에 강제로 적용 합니다.  `prompt=none`이 반대 hello-해당 hello 사용자와 모든 대화형 프롬프트 어떠한 나타나지 않으면 되도록 조정 합니다.  Single sign-on을 통해 hello 요청을 자동으로 완료할 수 없습니다, hello 끝점 오류를 반환 합니다.  `prompt=consent`hello OAuth 동의 대화 상자를에서는 hello 사용자가 로그인 한 후 hello 사용자 toogrant 권한 toohello 응용 프로그램 요청을 트리거합니다. |
| login_hint |선택 사항 |자신의 사용자 이름을 미리 알고 있는 경우 hello 사용자에 대 한 hello 로그인 페이지의 사용된 toopre 채우기 hello 사용자 이름/전자 메일 주소 필드 수 있습니다.  종종 앱이 매개이 변수를 사용 하 여 hello username 이전 로그인에서 추출 된 이미 있으면 다시 인증 하는 동안 hello를 사용 하 여 `preferred_username` 클레임입니다. |

이 시점에서 hello 사용자가 자격 증명 및 전체 hello 인증 tooenter를 요청 합니다.

### 샘플 응답
샘플 응답 hello 사용자가 인증 이후에 다음과 같습니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| 매개 변수 | 설명 |
| --- | --- |
| id_token |hello `id_token` 요청 hello 앱. Hello를 사용할 수 있습니다 `id_token` tooverify 사용자의 id를 hello 및 hello 사용자와 세션을 시작 합니다. |
| state |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 일반적으로 [교차 사이트 요청 위조 공격을 방지](http://tools.ietf.org/html/rfc6749#section-10.12)하기 위해 임의로 생성된 고유 값이 사용됩니다.  hello 상태 hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |

### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello `redirect_uri` hello 앱 적절 하 게 처리할 수 있도록 합니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

#### 권한 부여 끝점 오류에 대한 오류 코드
hello 다음 표에서 hello hello에 반환 될 수 있는 다양 한 오류 코드 `error` hello 오류 응답의 매개 변수입니다.

| 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- |
| invalid_request |프로토콜 오류(예: 필수 매개 변수 누락). |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 테스트 중에 발견되는 개발 오류입니다. |
| unauthorized_client |hello 클라이언트 응용 프로그램 없으면 toorequest 인증 코드를 허용 합니다. |이 문제는 일반적으로 hello 클라이언트 응용 프로그램이 Azure AD에 등록 되어 있지 않거나 toohello 사용자의 Azure AD 테 넌 트에 추가 되지 않습니다 때 발생 합니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| access_denied |리소스 소유자가 동의 거부 |hello 클라이언트 응용 프로그램 hello 사용자가 동의 하지 않는 한 진행할 수 hello 사용자에 게 알릴 수 있습니다. |
| unsupported_response_type |hello 권한 부여 서버 hello 요청에 hello 응답 유형을 지원 하지 않습니다. |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 테스트 중에 발견되는 개발 오류입니다. |
| server_error |hello 서버 오류가 발생 했습니다. |Hello 요청을 다시 시도 합니다. 이러한 오류는 일시적인 상태 때문에 발생할 수 있습니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 해당 응답은 tooa 일시적 오류로 인해 지연 합니다. |
| temporarily_unavailable |hello 서버 사용량이 많음 toohandle hello 요청 일시적으로입니다. |Hello 요청을 다시 시도 합니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 tooa 일시적 상태로 인해 응답이 지연 된다고는 됩니다. |
| invalid_resource |hello 대상 리소스가 존재 하지 않는, Azure AD를 찾을 수 없거나 올바르게 구성 되지 않아 유효 하지 않습니다. |이 hello 리소스 있을 경우 구성 되지 않았습니다 hello 테 넌 트에 나타냅니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |

## Hello id_token 유효성 검사
방금 받기는 `id_token` 충분 한 tooauthenticate hello 사용자;가 아닌 hello 서명을 확인 하 고 hello의 hello 클레임을 확인 해야 `id_token` 응용 프로그램의 요구 사항에 따라 합니다. hello Azure AD 끝점 JSON 웹 토큰 (Jwt) 및 공개 키 암호화 toosign 토큰을 사용 하 고 유효한 지 확인 합니다.

Toovalidate hello를 선택할 수 있습니다 `id_token` 클라이언트 코드에서 일반적으로 toosend hello 하지만 `id_token` tooa 백 엔드 서버 있습니다 hello 유효성 검사를 수행 하 고 있습니다. Hello hello 서명의 유효성을 검사 한 후 `id_token`, 필요한 tooverify는 몇 가지 클레임 가지입니다.

라면 toovalidate 추가 클레임 시나리오에 따라 합니다. 몇 가지 일반적인 유효성 검사는 다음과 같습니다.

* 확인 hello 사용자/조직에 등록 하 여 hello 앱에 대 한 합니다.
* 보장 hello 사용자에 게 적절 한 인증/권한
* 다단계 인증과 같은 특정 강도의 인증이 발생했는지 확인

Hello 유효성 검사 `id_token`, hello 사용자와의 세션을 시작 하 고 hello 클레임을 사용 하 여 hello에 `id_token` hello 사용자 응용 프로그램에 대 한 tooobtain 정보입니다. 이 정보는 표시, 레코드, 권한 부여 등에 사용될 수 있습니다. 클레임과 토큰 형식을 hello에 대 한 자세한 내용은 [지원 되는 토큰 및 클레임 유형](active-directory-token-and-claims.md)합니다.

## 로그아웃 요청 보내기
Hello 앱 중 toosign hello 사용자 할 때 충분 하지 않습니다 tooclear 응용 프로그램의 쿠키 또는 그렇지 않은 경우 hello 사용자와 hello 세션을 종료 됩니다.  Hello 사용자 toohello 리디렉션해야 `end_session_endpoint` 에 대 한 로그 아웃 합니다.  따라서 toodo를 실패할 경우 유효한 single sign on 세션 hello Azure AD 끝점을 사용 했기 때문에 hello 사용자가 자격 증명을 다시 입력 하지 않고 수 tooreauthenticate tooyour 응용 프로그램을 됩니다.

Hello 사용자 toohello 단순히 리디렉션할 수 있습니다 `end_session_endpoint` hello OpenID Connect 메타 데이터 문서에 나열 된:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| post_logout_redirect_uri |권장 |사용자 hello hello URL 리디렉션된 tooafter 성공적으로 로그 아웃 해야 합니다.  지정 하지 않은 경우 hello 사용자 일반 메시지를 표시 됩니다. |

## Single Sign-Out
Hello 사용자 toohello 리디렉션하면 `end_session_endpoint`, Azure AD hello 브라우저에서 hello 사용자의 세션을 지웁니다. 그러나 hello 사용자 인증을 위해 Azure AD를 사용 하는 tooother 응용 프로그램에서 로그인 여전히 수 있습니다. tooenable 해당 응용 프로그램 toosign 아웃 사용자를 동시에 hello, Azure AD에 등록 하는 HTTP GET 요청 toohello 보냅니다 `LogoutUrl` 모든 hello 응용 프로그램의 해당 hello 사용자가 현재에 로그인 합니다. 응용 프로그램을 반환 하 고 hello 사용자를 식별 하는 모든 세션을 선택 취소 하 여 toothis 요청 응답 해야는 `200` 응답 합니다.  이러한 구현 해야 응용 프로그램에서 로그 아웃 toosupport 단일 기호를 원하는 경우는 `LogoutUrl` 응용 프로그램의 코드에서.  Hello를 설정할 수 있습니다 `LogoutUrl` hello Azure 포털에서에서:

1. Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.
2. Hello hello 페이지의 맨 위 오른쪽 모서리에 있는 사용자 계정을 클릭 하 여 Active Directory를 선택 합니다.
3. Hello 왼쪽 탐색 패널에서 선택 **Azure Active Directory**를 눌러 **앱 등록** 응용 프로그램을 선택 하 고 있습니다.
4. 클릭 **속성** hello 및 **로그 아웃 URL** 입력란. 

## 토큰 획득
여러 웹 응용 프로그램 toonot만 기호 hello의 사용자에 필요는 없지만 OAuth를 사용 하 여 해당 사용자를 대신 하 여 웹 서비스에 액세스할 수도 있습니다. 이 시나리오를 결합 OpenID Connect 사용자 인증 동시에 가져오는 동안에 `authorization_code` 사용된 tooget 일 수 있는 `access_tokens` OAuth 권한 부여 코드 흐름 hello를 사용 하 여 합니다.

## 액세스 토큰 가져오기
tooacquire 액세스 토큰 toomodify hello 로그인 요청 위쪽에서 필요합니다.

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Hello 요청에 사용 권한 범위를 포함 하 고 사용 하 여 `response_type=code+id_token`, hello `authorize` 끝점 해당 hello 사용자가 동의 hello에 표시 된 toohello 사용 권한을 통해 `scope` 매개 변수를 쿼리하고 앱 권한 부여 코드 반환 액세스 토큰에 대 한 tooexchange 합니다.

### 성공적인 응답
`response_mode=form_post` 를 사용한 성공적인 응답은 다음과 같습니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| 매개 변수를 포함해야 합니다. | 설명 |
| --- | --- |
| id_token |hello `id_token` 요청 hello 앱. Hello를 사용할 수 있습니다 `id_token` tooverify 사용자의 id를 hello 및 hello 사용자와 세션을 시작 합니다. |
| 코드 |응용 프로그램 요청 hello authorization_code를 hello 합니다. hello 앱 hello 대상 리소스에 대 한 hello 권한 부여 코드 toorequest 액세스 토큰을 사용할 수 있습니다. authorization_code는 수명이 매우 짧으며, 일반적으로 약 10분 후에 만료됩니다. |
| state |State 매개 변수는 hello 응답에 동일한 값이 표시 되어야 하는 hello hello 요청에 포함 됩니다. hello 앱 hello 요청 및 응답의 hello 상태 값이 동일한 지 확인 해야 합니다. |

### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello `redirect_uri` hello 앱 적절 하 게 처리할 수 있도록 합니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

Hello 가능한 오류 코드는 권장 되는 클라이언트 작업에 대 한 설명, 참조 [권한 부여 끝점 오류에 대 한 오류 코드](#error-codes-for-authorization-endpoint-errors)합니다.

권한 부여 참조 되 면 `code` 및 `id_token`, hello 사용자를 로그인 하 고 대신 액세스 토큰을 받을 수 있습니다.  toosign hello 사용자 hello 확인 해야 합니다 `id_token` 위에 설명 된 대로 정확 하 게 합니다. tooget 액세스 토큰의 hello "hello 권한 부여 코드 toorequest 액세스 토큰 사용" 섹션에 설명 된 hello 단계를 실행 하려면 우리의 [OAuth 프로토콜 설명서](active-directory-protocols-oauth-code.md)합니다.
