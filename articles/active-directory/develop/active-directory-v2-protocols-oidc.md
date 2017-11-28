---
title: "Active Directory v2.0 hello OpenID Connect 프로토콜 aaaAzure | Microsoft Docs"
description: "Hello OpenID Connect 인증 프로토콜의 v2.0 구현 hello Azure AD 사용 하 여 웹 응용 프로그램을 작성 합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 및 hello OpenID Connect 프로토콜
OpenID Connect 사용자 tooa 웹 응용 프로그램에서 toosecurely 기호를 사용할 수 있는 OAuth 2.0 인증 프로토콜입니다. Hello v 2.0 끝점의 OpenID Connect 구현을 사용 하는 경우에 로그인 및 API 액세스 tooyour 웹 기반 앱을 추가할 수 있습니다. 이 문서에서는 보여줍니다 어떻게 toodo이 언어와 독립적입니다. 설명 방법을 toosend 및 모든 Microsoft 오픈 소스 라이브러리를 사용 하지 않고 HTTP 메시지를 수신 합니다.

> [!NOTE]
> hello v2.0 끝점에는 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다. 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) hello OAuth 2.0 확장 *권한 부여* 프로토콜 toouse로는 *인증* 단일 수행할 수 있도록 프로토콜 OAuth를 사용 하 여 sign-on 합니다. OpenID Connect의 hello 개념을 소개는 *ID 토큰*, hello 클라이언트 hello 사용자의 tooverify hello id를 허용 하는 보안 토큰은입니다. hello ID 토큰은 또한 hello 사용자에 대 한 기본 프로필 정보를 가져옵니다. 응용 프로그램을 안전 하 게 얻을 수 OpenID Connect 확장 하는 OAuth 2.0 때문에 *액세스 토큰*, 의해 보안 되는 리소스를 사용 하는 tooaccess 수는 [권한 부여 서버](active-directory-v2-protocols.md#the-basics)합니다. 서버에서 호스트되고 브라우저를 통해 액세스되는 [웹 응용 프로그램](active-directory-v2-flows.md#web-apps) 을 빌드하는 경우 OpenID Connect를 사용하는 것이 좋습니다.

## 프로토콜 다이어그램: 로그인
hello 가장 기본적인 로그인 흐름 hello 단계는 hello 다음 다이어그램에 표시 합니다. 이 문서에서는 각 단계를 자세히 설명합니다.

![OpenID Connect 프로토콜: 로그인](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Hello OpenID Connect 메타 데이터 문서를 인출 합니다.
OpenID Connect 대부분의 프로그램 앱 tooperform 로그인에 필요한 hello 정보를 포함 하는 메타 데이터 문서에 설명 합니다. 여기에 hello Url toouse hello 서비스의 공개 서명 키의 hello 위치 등의 정보가 포함 됩니다. Hello v2.0 끝점에 대 한이 파일은 hello OpenID Connect 메타 데이터 문서를 사용 해야 합니다.

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

hello `{tenant}` 4 개의 값 중 하나를 수행 합니다.

| 값 | 설명 |
| --- | --- |
| `common` |모두 개인 Microsoft 계정 및 Azure Active Directory (Azure AD)에서 회사 또는 학교 계정을 사용 하 여 사용자가 toohello 응용 프로그램에 서명할 수 있습니다. |
| `organizations` |있는 사용자만 작업 또는 학교 계정을 Azure AD에서 toohello 응용 프로그램에 로그인 할 수 있습니다. |
| `consumers` |개인 Microsoft 계정 가진 사용자만 toohello 응용 프로그램 로그인 수 있습니다. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 또는 `contoso.onmicrosoft.com` |사용자만 특정 Azure AD에서 회사 또는 학교 계정을 사용 하 여 테 넌 트 수 toohello 응용 프로그램에 로그인 합니다. 도메인 이름이 hello hello Azure AD 테 넌 트 또는 hello 테 넌 트의 GUID 식별자를 사용할 수 있습니다. |

hello 메타 데이터는 간단한 개체 JSON (JavaScript Notation) 문서. 다음 예에 대 한 조각 hello를 참조 하십시오. hello 조각의 내용을에서 자세히 설명 hello [OpenID Connect 사양](https://openid.net)합니다.

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

이 메타 데이터 문서 tooconfigure OpenID Connect 라이브러리 하거나 SDK;을 사용 하는 일반적으로 hello 라이브러리의 작업 메타 데이터 toodo hello를 사용 합니다. 그러나 빌드 전 OpenID Connect 라이브러리를 사용 하지 않는 hello v2.0 끝점을 사용 하 여이 문서 tooperform 로그인 웹 앱에서의 hello 나머지의 hello 단계를 수행 수입니다.

## Hello 로그인 요청 보내기
웹 앱 tooauthenticate hello 사용자 하면 디렉션할 수 있습니다 hello 사용자 toohello `/authorize` 끝점입니다. 이 요청은 hello 비슷한 toohello 첫 번째 다리 [OAuth 2.0 인증 코드 흐름](active-directory-v2-protocols-oauth-code.md), 이러한 중요 한 차이가 있습니다.

* hello 요청 hello에 포함 되어야 `openid` hello에 대 한 범위 `scope` 매개 변수입니다.
* hello `response_type` 매개 변수에 포함 되어야 `id_token`합니다.
* hello 요청 hello에 포함 되어야 `nonce` 매개 변수입니다.

예:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> 다음 링크 tooexecute hello이이 요청을 클릭 합니다. 에 로그인 한 후 브라우저 hello 주소 표시줄에 ID 토큰으로 리디렉션된 toohttps://localhost/myapp/ 됩니다. 이 요청은 `response_mode=query`를 사용합니다(학습 용도로만). `response_mode=form_post`를 사용하는 것이 좋습니다.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| 매개 변수 | 조건 | 설명 |
| --- | --- | --- |
| tenant |필수 |Hello를 사용할 수 있습니다 `{tenant}` toohello 응용 프로그램에 로그인 할 수 있는 hello 요청 toocontrol의 hello 경로에 값입니다. hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다. 자세한 내용은 [프로토콜 기본 사항](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| client_id |필수 |hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| response_type |필수 |OpenID Connect 로그인을 위한 `id_token` 이 포함되어야 합니다. `code`와 같은 다른 `response_types` 값을 포함할 수도 있습니다. |
| redirect_uri |권장 |hello 리디렉션 URI 인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램입니다. 또한 hello 리디렉션 URL 이어야 한다는 hello 포털에 등록 된 Uri 인코딩 중 하나에 정확히 일치 해야 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다. OpenID Connect hello 범위 포함 해야 `openid`, 이것은 hello 동의 UI에는 "로그인" 권한이 toohello 해석 합니다. 동의를 요청하기 위해 이 요청에 다른 범위를 포함할 수도 있습니다. |
| nonce |필수 |클레임으로 hello 결과 id_token 값에 포함 될 hello 앱에서 생성 하는 hello 요청에 포함 하는 값입니다. hello 앱이 값 toomitigate 토큰 재생 공격을 확인할 수 있습니다. 일반적으로 hello 값은 사용 되는 tooidentify hello 원점 hello 요청 될 수 있는 임의 고유 문자열을 사용 합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 권한 부여 코드 백 tooyour 앱 되어야 하는 hello 방법을 지정 합니다. `query`, `form_post` 또는 `fragment` 중 하나일 수 있습니다. 웹 응용 프로그램에 사용할 수 있는 권장 `response_mode=form_post`, tooensure hello 토큰 tooyour 응용 프로그램의 가장 안전 하 게 전송 합니다. |
| state |권장 |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. 임의로 생성 된 고유한 값을 일반적으로 사용 됩니다 너무[교차 사이트 요청 위조 공격을 방지](http://tools.ietf.org/html/rfc6749#section-10.12)합니다. hello도 상태가 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode hello 인증 요청이 발생 하기 전에 hello 페이지 또는 보기 hello 사용자가 같은입니다. |
| prompt |옵션 |Hello 필요한 사용자 상호 작용 유형을 나타냅니다. hello이 이번에만 유효한 값은 `login`, `none`, 및 `consent`합니다. hello `prompt=login` 강제로 hello 사용자 tooenter single sign on 부 정하고 해당 요청에 자격 증명 클레임입니다. hello `prompt=none` 클레임은 hello 반대입니다. 이 클레임 해당 hello 사용자 모든 대화형 프롬프트도 표시 되지 것을 보장 합니다. Hello 요청에서 single sign-on을 통해 자동으로 완료할 수 없습니다, hello v2.0 끝점 오류를 반환 합니다. hello `prompt=consent` hello 사용자가 로그인 한 후 트리거 hello OAuth 동의 대화 상자를 클레임 합니다. hello 대화 상자 hello 사용자 toogrant 권한 toohello 앱 있습니다. |
| login_hint |옵션 |Hello username 미리 알고 있는 경우이 매개 변수 toopre 채우기 hello 사용자 이름 및 전자 메일 주소 필드 hello 로그인 페이지의 hello 사용자에 대해 사용할 수 있습니다. 응용 프로그램 이미 hello를 사용 하 여 hello username는 이전 로그인에서 추출한 다음 다시 인증 하는 동안이 매개 변수를 사용 하는 경우가 많습니다 `preferred_username` 클레임입니다. |
| domain_hint |옵션 |이 값은 `consumers` 또는 `organizations`일 수 있습니다. Hello 전자 메일 기반 검색 프로세스를 건너뜁니다 포함 하는 경우 해당 hello 사용자 hello v 2.0 로그인 페이지에 대해 약간 더 효율적인된 사용자 환경을 통해 이동 합니다. 종종, 앱이 매개이 변수 사용 다시 인증 하는 동안 hello를 추출 하 여 `tid` hello ID 토큰에서 클레임입니다. 경우 hello `tid` 값은 클레임 `9188040d-6c67-4c5b-b112-36a304b66dad`를 사용 하 여 `domain_hint=consumers`합니다. 그렇지 않으면 `domain_hint=organizations`를 사용합니다. |

이 시점에서 hello 사용자 자격 증명 및 전체 hello 인증 프롬프트 tooenter 됩니다. hello v2.0 끝점 확인 해당 hello 사용자가 동의 hello에 표시 된 toohello 사용 권한만 `scope` 쿼리 매개 변수입니다. Hello 사용자가 이러한 사용 권한 중 tooany 동의 하지, hello v2.0 끝점 hello 사용자 tooconsent toohello 필요한 권한을 라는 메시지가 나타납니다. [권한, 동의 및 다중 테넌트 앱](active-directory-v2-scopes.md)에 대해 자세히 알아볼 수 있습니다.

Hello에 지정 된 hello 메서드를 사용 하 여 hello v2.0 끝점 반환 hello에 대 한 응답 tooyour 응용 프로그램에 표시 된 리디렉션 URI hello 사용자를 인증 하 동의 허용 하는 후 `response_mode` 매개 변수입니다.

### 성공적인 응답
`response_mode=form_post`를 사용할 때의 성공적인 응답은 다음과 같습니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| 매개 변수 | 설명 |
| --- | --- |
| id_token |ID 토큰을 요청 하는 응용 프로그램 hello hello 합니다. Hello를 사용할 수 있습니다 `id_token` 매개 변수 tooverify 사용자의 id를 hello 및 hello 사용자와 세션을 시작 합니다. ID 토큰 및 해당 내용에 대 한 자세한 내용은 참조 hello [v2.0 끝점 참조 토큰](active-directory-v2-tokens.md)합니다. |
| state |경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 앱 hello 요청 및 응답의 hello 상태 값이 동일한 지 확인 해야 합니다. |

### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello 리디렉션 URI hello 앱 처리할 수 있도록 합니다. 오류 응답은 다음과 같습니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |발생 하는 오류 및 tooreact tooerrors tooclassify 형식을 사용할 수 있습니다는 오류 코드 문자열입니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |

### 권한 부여 끝점 오류에 대한 오류 코드
hello 다음 표에서 hello에 반환 될 수 있는 오류 코드 `error` hello 오류 응답의 매개 변수:

| 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- |
| invalid_request |프로토콜 오류(예: 필수 매개 변수 누락)입니다. |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 설정 중에 발견되는 개발 오류입니다. |
| unauthorized_client |hello 클라이언트 응용 프로그램이 인증 코드를 요청할 수 없습니다. |이 문제는 일반적으로 hello 클라이언트 응용 프로그램이 Azure AD에 등록 되어 있지 않거나 toohello 사용자의 Azure AD 테 넌 트에 추가 되지 않습니다 때 발생 합니다. hello 응용 프로그램 hello 사용자 지침 tooinstall hello 응용 프로그램과 메시지를 표시 하 고 AD tooAzure 추가할 수 있습니다. |
| access_denied |hello 리소스 소유자가 동의 거부 했습니다. |hello 클라이언트 응용 프로그램 hello 사용자가 동의 하지 않는 한 진행할 수 hello 사용자에 게 알릴 수 있습니다. |
| unsupported_response_type |hello 권한 부여 서버 hello 요청에 hello 응답 유형을 지원 하지 않습니다. |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 설정 중에 발견되는 개발 오류입니다. |
| server_error |hello 서버 오류가 발생 했습니다. |Hello 요청을 다시 시도 합니다. 이러한 오류는 일시적인 상태 때문에 발생할 수 있습니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 해당 응답은 tooa 일시적 오류로 인해 지연 합니다. |
| temporarily_unavailable |hello 서버 사용량이 많음 toohandle hello 요청 일시적으로입니다. |Hello 요청을 다시 시도 합니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 tooa 일시적 상태로 인해 응답이 지연 된다고는 됩니다. |
| invalid_resource |존재 하지 않는, Azure AD를 찾을 수 없거나 올바르게 구성 되지 않은 hello 대상 리소스가 유효 하지 않습니다. |이 hello 리소스 있을 경우 구성 되지 않았습니다 hello 테 넌 트에 나타냅니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 지침이 hello 사용자를 요구할 수 있습니다. |

## Hello ID 토큰 유효성 검사
ID 토큰을 받는 충분 한 tooauthenticate hello 사용자가 아닙니다. 또한 hello ID 토큰 서명의 유효성을 검사 하 고 응용 프로그램의 요구 사항에 따라 hello 토큰의 hello 클레임을 확인 해야 합니다. 사용 하 여 hello v2.0 끝점 [JSON 웹 토큰 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) 및 공개 키 암호화 toosign 토큰 및 유효한 지 확인 합니다.

클라이언트 코드에서 toovalidate hello ID 토큰을 선택할 수 있지만 일반적으로 toosend hello ID 토큰 tooa 백 엔드 서버 이며 있습니다 hello 유효성 검사를 수행 합니다. Hello hello ID 토큰 서명의 유효성을 검사 한 후에 몇 가지 클레임을 tooverify 필요 합니다. 를 비롯 한 자세한 내용은 더에 대 한 [토큰 유효성 검사](active-directory-v2-tokens.md#validating-tokens) 및 [서명 키 롤오버에 대 한 중요 한 정보](active-directory-v2-tokens.md#validating-tokens), hello 참조 [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다. 사용할 수 있는 라이브러리 tooparse 권장 하 고 토큰의 유효성을 검사 합니다. 이러한 라이브러리 중 하나 이상을 대부분의 언어 및 플랫폼에 사용할 수 있습니다.
<!--TODO: Improve hello information on this-->

또한 시나리오에 따라 toovalidate 추가 클레임 할 수 있습니다. 몇 가지 일반적인 유효성 검사는 다음과 같습니다.

* hello 사용자 또는 조직에 등록 하 여 hello 앱을 확인 합니다.
* 해당 hello 사용자 권한 부여 또는 권한이 필요한 확인 합니다.
* 다단계 인증과 같은 특정 강도의 인증이 발생했는지 확인합니다.

ID 토큰의 클레임을 hello에 대 한 자세한 내용은 참조 hello [v2.0 끝점 참조 토큰](active-directory-v2-tokens.md)합니다.

ID 토큰 hello를 완전히 확인 한 후에 hello 사용자와 세션을 시작할 수 있습니다. 응용 프로그램에서 사용자 hello에 대 한 hello ID 토큰 tooget 정보에서 hello 클레임을 사용 합니다. 이 정보를 표시, 레코드, 권한 부여 등에 사용할 수 있습니다.

## 로그아웃 요청 보내기
Toosign hello 사용자 응용 프로그램에서 원하는 없는 충분 한 tooclear 응용 프로그램의 쿠키 또는 그렇지 않으면 hello 사용자의 세션을 종료 합니다. 또한 out hello 사용자 toohello v2.0 끝점 toosign을 리디렉션해야 합니다. 이렇게 하지 않으면 경우 hello 사용자 재인증 절차 tooyour 앱 자격 증명을 다시 입력 하지 않고 유효한 단일 로그인 세션 hello v2.0 끝점과 했기 때문에 합니다.

Hello 사용자 toohello 리디렉션할 수 `end_session_endpoint` hello OpenID Connect 메타 데이터 문서에 나열 된:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| 매개 변수 | 조건 | 설명 |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | 권장 | 사용자 hello hello URL이 리디렉션된 tooafter 성공적으로 로그 아웃 합니다. Hello 매개 변수를 포함 하지 않을 경우 hello 사용자 hello v2.0 끝점에 의해 생성 되는 일반 메시지를 표시 됩니다. 이 URL hello 리디렉션 hello 응용 프로그램 등록 포털에서 응용 프로그램에 대해 등록 된 Uri 중 하 나와 일치 해야 합니다.  |

## Single Sign-Out
Hello 사용자 toohello 리디렉션하면 `end_session_endpoint`, hello v2.0 끝점 hello 브라우저에서 hello 사용자의 세션을 지웁니다. 그러나 hello 사용자 인증에 대 한 Microsoft 계정을 사용 하는 tooother 응용 프로그램에서 로그인 여전히 수 있습니다. tooenable 출력 hello v2.0 끝점 동시에 이러한 응용 프로그램 toosign hello 사용자 보냅니다 등록 하는 HTTP GET 요청 toohello `LogoutUrl` 모든 hello 응용 프로그램의 해당 hello 사용자가 현재에 로그인 합니다. 응용 프로그램을 반환 하 고 hello 사용자를 식별 하는 모든 세션을 선택 취소 하 여 toothis 요청 응답 해야는 `200` 응답 합니다.  이러한 구현 해야 응용 프로그램에서 로그 아웃 toosupport 단일 기호를 원하는 경우는 `LogoutUrl` 응용 프로그램의 코드에서.  Hello를 설정할 수 있습니다 `LogoutUrl` hello 응용 프로그램 등록 포털에서 합니다.

## 프로토콜 다이어그램: 토큰 가져오기
여러 웹 응용 프로그램 OAuth를 사용 하 여, toonot 유일한 기호 hello 사용자 뿐만 아니라 tooaccess hello 사용자를 대신 하 여 웹 서비스를 필요 합니다. 이 시나리오를 결합 OpenID Connect 사용자 인증, 인증을 동시에 가져오는 동안 tooget 액세스를 사용할 수 있는 코드 토큰 hello OAuth 인증 코드 흐름을 사용 하는 경우.

hello 전체 OpenID Connect에 로그인 하 고 토큰 획득 흐름 비슷한 toohello 다음 다이어그램을 찾습니다. 각 단계 hello hello 문서의 다음 섹션에서 자세히 설명 합니다.

![OpenID Connect 프로토콜: 토큰 획득](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## 액세스 토큰 가져오기
tooacquire 액세스 토큰 hello 로그인 요청을 수정 합니다.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> 다음 링크 tooexecute hello이이 요청을 클릭 합니다. 에 로그인 한 후 브라우저 ID 토큰 및 hello 주소 표시줄에 코드를 사용 하 여 리디렉션된 toohttps://localhost/myapp/입니다. 이 요청은 `response_mode=query`를 사용합니다(학습 용도로만). `response_mode=form_post`를 사용하는 것이 좋습니다.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

Hello 요청에서 하 고 사용 하 여 사용 권한 범위를 포함 하 여 `response_type=id_token code`, hello v2.0 끝점 해당 hello 사용자가 동의 hello에 표시 된 toohello 사용 권한을 사용 하면 `scope` 쿼리 매개 변수입니다. 액세스 토큰에 대 한 권한 부여 코드 tooyour 앱 tooexchange를 반환합니다.

### 성공적인 응답
`response_mode=form_post`를 사용할 때의 성공적인 응답은 다음과 같습니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| 매개 변수 | 설명 |
| --- | --- |
| id_token |ID 토큰을 요청 하는 응용 프로그램 hello hello 합니다. Hello ID 토큰 tooverify hello 사용자 id를 사용 하 여 수 있으며 hello 사용자와 세션을 시작할 수 있습니다. Hello에 ID 토큰 및 해당 내용에 대 한 자세한 정보를 찾을 수 [v2.0 끝점 참조 토큰](active-directory-v2-tokens.md)합니다. |
| 코드 |응용 프로그램 요청 hello는 hello 권한 부여 코드입니다. hello 앱 hello 대상 리소스에 대 한 hello 권한 부여 코드 toorequest 액세스 토큰을 사용할 수 있습니다. 권한 부여 코드는 매우 일시적으로 존재합니다. 일반적으로 권한 부여 코드는 약 10분 후에 만료됩니다. |
| state |State 매개 변수는 hello 응답에 동일한 값이 표시 되어야 하는 hello hello 요청에 포함 됩니다. hello 앱 hello 요청 및 응답의 hello 상태 값이 동일한 지 확인 해야 합니다. |

### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello 리디렉션 URI hello 응용 프로그램 수를 적절히 처리 되도록 합니다. 오류 응답은 다음과 같습니다.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |발생 하는 오류 및 tooreact tooerrors tooclassify 형식을 사용할 수 있습니다는 오류 코드 문자열입니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |

가능한 오류 코드 및 권장되는 클라이언트 응답에 대한 설명은 [권한 부여 끝점 오류에 대한 오류 코드](#error-codes-for-authorization-endpoint-errors)를 참조하세요.

ID 토큰 및 인증 코드를 있는 경우 hello 사용자 로그인 수 있으며 대신 액세스 토큰을 가져옵니다. toosign hello 사용자 hello ID 토큰을 확인 해야 합니다 [설명 된 대로 정확히](#validate-the-id-token)합니다. tooget 액세스 토큰에 설명 된 hello 단계에 따라 우리의 [OAuth 프로토콜 설명서](active-directory-v2-protocols-oauth-code.md#request-an-access-token)합니다.
