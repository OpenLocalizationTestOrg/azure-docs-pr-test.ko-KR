---
title: "Azure AD hello v 2.0 암시적 흐름을 사용 하 여 단일 페이지 응용 프로그램 aaaSecure | Microsoft Docs"
description: "Azure AD의 v2.0 구현의 hello 암시적 흐름을 사용 하 여 단일 페이지 응용 프로그램에 대 한 구성 웹 응용 프로그램."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# 프로토콜-hello 암시적 흐름을 사용 하 여 SPAs v2.0
Hello v2.0 끝점과 Microsoft의 개인 정보와 작업/학교 계정 사용 하 여 단일 페이지 앱에 사용자가 서명할 수 있습니다.  단일 페이지와 주목할 만한 몇 가지 과제 때 브라우저 얼굴 기본적으로에서 실행 하는 다른 JavaScript 앱 tooauthentication 제공 됩니다.

* 이러한 앱의 hello 보안 특성은 일반적인 서버 기반 웹 응용 프로그램 크게 다릅니다.
* 다수의 인증 서버 및 ID 공급자는 CORS 요청을 지원하지 않습니다.
* 전체 페이지 브라우저 리디렉션 hello 앱에서 특히 침투 적 toohello 사용자 경험을 수 있습니다.

이러한 응용 프로그램에 대 한 (생각: AngularJS, Ember.js, React.js, 등) Azure AD에서는 hello OAuth 2.0 Implicit Grant 흐름을 지원 합니다.  hello 암시적 흐름 hello에 설명 되어 [OAuth 2.0 사양](http://tools.ietf.org/html/rfc6749#section-4.2)합니다.  주요 이점은 백 엔드 서버 자격 증명 교환을 수행 하지 않고 hello 앱 tooget 토큰 Azure AD에서 수 있다는 점입니다.  이렇게 하면 hello 앱 toosign hello 사용자에서, 세션을 유지 관리 있고 tooother 웹 Api hello 클라이언트 JavaScript 코드 내에서 토큰을 가져옵니다.  특히 약 hello 암시적 흐름-를 사용 하면 계정에 몇 가지 중요 한 보안 고려 사항 tootake 됩니다 [클라이언트](http://tools.ietf.org/html/rfc6749#section-10.3) 및 [사용자 가장](http://tools.ietf.org/html/rfc6749#section-10.3)합니다.

Toouse hello 암시적 흐름 및 Azure AD tooadd 인증 tooyour JavaScript 앱을 원하는 경우 우리의 오픈 소스 JavaScript 라이브러리를 사용 하는 것이 좋습니다 [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js)합니다.  사용할 수 있는 몇 가지 AngularJS 자습서 없는 [여기](active-directory-appmodel-v2-overview.md#getting-started) toohelp 시작 하는 데 있습니다.  

그러나 사용 하려는 라이브러리 toouse 하지 단일 페이지 응용 프로그램 및 송신 프로토콜 메시지에서 직접 아래 hello 일반 단계를 수행 합니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

## 프로토콜 다이어그램
hello 전체 암시적 로그인 흐름 다음과 같은-각 hello 단계 아래에 자세히 설명 합니다.

![OpenId Connect 스윔 레인](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Hello 로그인 요청 보내기
tooinitially 기호 앱에 사용자를 hello, 보낼 수 있습니다는 [OpenID Connect](active-directory-v2-protocols-oidc.md) 권한 부여 요청 및 get는 `id_token` hello v2.0 끝점에서:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> 이 요청 hello tooexecute 아래에 링크를 클릭 하세요. 로그인 한 후 브라우저 리디렉션되어야 너무`https://localhost/myapp/` 와 `id_token` hello 주소 표시줄에 있습니다.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다.  자세한 내용은 [프로토콜 기본](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| client_id |필수 |응용 프로그램 Id는 hello 등록 포털 hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 응용 프로그램을 할당 합니다. |
| response_type |필수 |OpenID Connect 로그인을 위한 `id_token` 이 포함되어야 합니다.  Hello response_type 포함 될 수도 있습니다 `token`합니다. 사용 하 여 `token` 여기을 사용 하면 두 번째 요청 toohello 권한을 부여 toomake 필요 없이 권한 부여 끝점 hello에서 즉시 액세스 토큰에 응용 프로그램 tooreceive 끝점입니다.  Hello를 사용 하는 경우 `token` response_type, hello `scope` 매개 변수는 리소스 tooissue hello에 대 한 토큰을 나타내는 범위를 포함 해야 합니다. |
| redirect_uri |권장 |인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램의 hello redirect_uri입니다.  또한 url로 인코딩되어 있어야 점을 제외 하 고 hello 포털에 등록 된 hello redirect_uris 중 하나에 정확히 일치 해야 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다.  OpenID Connect hello 범위 포함 해야 `openid`, 이것은 hello 동의 UI에는 "로그인" 권한이 toohello 해석 합니다.  필요에 따라 할 수 있습니다 tooinclude hello `email` 또는 `profile` [범위](active-directory-v2-scopes.md) 까지 tooadditional 사용자 데이터에 액세스 합니다.  동의 toovarious 리소스를 요청에 대 한이 요청에 다른 범위를 포함할 수도 있습니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 토큰 백 tooyour 앱 되어야 하는 hello 방법을 지정 합니다.  해야 `fragment` hello 암시적 흐름에 대 한 합니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다.  원하는 모든 콘텐츠의 문자열일 수 있습니다.  일반적으로 [교차 사이트 요청 위조 공격을 방지](http://tools.ietf.org/html/rfc6749#section-10.12)하기 위해 임의로 생성된 고유 값이 사용됩니다.  hello 상태 hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |
| nonce |필수 |클레임으로 결과 id_token hello에에서 포함 될 hello 앱에서 생성 하는 hello 요청에 포함 하는 값입니다.  hello 앱이 값 toomitigate 토큰 재생 공격 확인할 수 있습니다.  hello 값은 대개 임의 고유 문자열 사용된 tooidentify hello 원점 hello 요청의 수입니다. |
| prompt |선택 사항 |Hello 필요한 사용자 상호 작용 유형을 나타냅니다.  이 이번에 유효한 값은 '로그인' 'none', 전용 hello 및 '승인'.  `prompt=login`force를 사용자 tooenter hello 됩니다에 단일 로그인 부정 해당 요청에 자격 증명입니다.  `prompt=none`반대 hello이 방법을 사용 하면 해당 hello 사용자 모든 대화형 프롬프트도 표시 되지 않았습니다.  Single sign-on을 통해 hello 요청을 자동으로 완료할 수 없으면, hello v2.0 끝점 오류가 반환 됩니다.  `prompt=consent`대화 상자에서는 hello 사용자가 로그인 한 후 hello 사용자 toogrant 권한 toohello 앱 타고 트리거 hello OAuth 합니다. |
| login_hint |선택 사항 |수의 hello 사용된 toopre 채우기 hello 사용자 이름/전자 메일 주소 필드 서명할 수 hello 사용자에 대 한 페이지에 자신의 사용자 이름을 미리 알고 있는 경우.  종종 앱 hello username 이전 로그인에서 추출 된 이미 있으면 다시 인증 하는 동안이 매개 변수를 사용 합니다 hello를 사용 하 여 `preferred_username` 클레임입니다. |
| domain_hint |선택 사항 |`consumers` 또는 `organizations` 중 하나일 수 있습니다.  Hello 전자 메일 기반 검색 프로세스는 건너뜁니다 포함 하는 경우 해당 사용자가을 통해 hello v 2.0 로그인 페이지를 앞에 tooa 약간 더 사용자 경험을 간소화 합니다.  종종 앱 다시 인증 하는 동안 hello를 추출 하 여에이 매개 변수를 사용 합니다 `tid` hello id_token에서 클레임입니다.  경우 hello `tid` 값은 클레임 `9188040d-6c67-4c5b-b112-36a304b66dad`를 사용 해야 `domain_hint=consumers`합니다.  그렇지 않으면 `domain_hint=organizations`를 사용합니다. |

Hello 사용자 됩니다이 시점에서 자격 증명 및 전체 hello 인증 tooenter 라는 메시지가 표시 됩니다.  hello v2.0 끝점도 방법을 사용 하면 해당 hello 사용자가 동의 hello에 표시 된 toohello 사용 권한만 `scope` 쿼리 매개 변수입니다.  Hello 사용자가 이러한 사용 권한 중 tooany 동의한 하지 것 묻습니다 hello 사용자 tooconsent toohello 필요한 사용 권한.  [사용 권한, 동의 및 다중 테넌트 앱의 세부 정보는 여기에 제공되어 있습니다](active-directory-v2-scopes.md).

Hello v2.0 끝점에 표시 된 hello 응답 tooyour 응용 프로그램을 반환 합니다 hello 사용자를 인증 하 고 동의 허용 하면 `redirect_uri`, hello에 지정 된 hello 메서드를 사용 하 여 `response_mode` 매개 변수입니다.

#### 성공적인 응답
사용 하 여 성공적인 응답 `response_mode=fragment` 및 `response_type=id_token+token` 쉽게 읽을 수 있도록 줄 바꿈 hello 다음과 같습니다.

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| 매개 변수 | 설명 |
| --- | --- |
| access_token |`response_type`이 `token`을 포함하는 경우 포함됩니다. 응용 프로그램 요청 hello hello 액세스 토큰이 경우에 대 한 hello 만들어집니다.  hello 액세스 토큰을 디코딩할 되거나 기타 방식으로 검사 되지 않아야, 불투명 문자열로 처리 될 수 있습니다. |
| token_type |`response_type`이 `token`을 포함하는 경우 포함됩니다.  항상 `Bearer`입니다. |
| expires_in |`response_type`이 `token`을 포함하는 경우 포함됩니다.  hello 토큰이 캐싱 목적으로 유효한 시간 (초) hello 수를 나타냅니다. |
| scope |`response_type`이 `token`을 포함하는 경우 포함됩니다.  Hello 범위에서 어떤 hello에 대 한 access_token를 사용할 수를 나타냅니다. |
| id_token |응용 프로그램 요청 hello id_token을 hello 합니다. Hello id_token tooverify hello 사용자 id를 사용 하 여 수 있으며 hello 사용자와 세션을 시작할 수 있습니다.  Id_tokens와 해당 내용에 대 한 자세한 내용은 hello에 연결 되어 [v2.0 끝점 토큰 참조](active-directory-v2-tokens.md)합니다. |
| state |State 매개 변수는 hello 응답에 동일한 값이 표시 되어야 하는 hello hello 요청에 포함 됩니다. hello 앱 hello 요청 및 응답의 hello 상태 값이 동일한 지 확인 해야 합니다. |

#### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello `redirect_uri` hello 앱 적절 하 게 처리할 수 있도록 합니다.

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

## Hello id_token 유효성 검사
방금는 id_token 수신은 충분 한 tooauthenticate hello 사용자; 없습니다. hello id_token 서명을 확인 하 고 응용 프로그램의 요구 사항에 따라 hello 토큰의 hello 클레임을 확인 해야 합니다.  사용 하 여 hello v2.0 끝점 [JSON 웹 토큰 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) 및 공개 키 암호화 toosign 토큰 및 유효한 지 확인 합니다.

Toovalidate hello를 선택할 수 있습니다 `id_token` 클라이언트 코드에서 일반적으로 toosend hello 하지만 `id_token` tooa 백 엔드 서버 있습니다 hello 유효성 검사를 수행 하 고 있습니다.  Hello id_token hello 서명의 유효성을 검사 한 후 몇 가지 클레임 필요한 tooverify 사용할 수 있습니다.  Hello 참조 [v2.0 토큰 참조](active-directory-v2-tokens.md) 자세한 내용은 포함 하 여 [토큰 유효성 검사](active-directory-v2-tokens.md#validating-tokens) 및 [중요 한 정보에 대 한 서명 키 롤오버](active-directory-v2-tokens.md#validating-tokens)합니다.  대부분의 언어 및 플랫폼에서 사용할 수 있는 하나 이상의 토큰의 구문 분석 및 유효성 검사에 대한 라이브러리를 사용하는 것이 좋습니다.
<!--TODO: Improve hello information on this-->

라면 toovalidate 추가 클레임 시나리오에 따라 합니다.  몇 가지 일반적인 유효성 검사는 다음과 같습니다.

* 확인 hello 사용자/조직에 등록 하 여 hello 앱에 대 한 합니다.
* 보장 hello 사용자에 게 적절 한 인증/권한
* 다단계 인증과 같은 특정 강도의 인증이 발생했는지 확인

에 id_token hello 클레임에 대 한 자세한 내용은 참조 hello [v2.0 끝점 토큰 참조](active-directory-v2-tokens.md)합니다.

Hello id_token 완전히 유효성 검사 hello 사용자와 세션을 시작할 수 있으며 응용 프로그램에서 hello 클레임 hello 사용자에 대 한 hello id_token tooobtain 정보에 사용.  이 정보는 표시, 레코드, 권한 부여 등에 사용될 수 있습니다.

## 액세스 토큰 가져오기
호출 웹 hello와 같은 Azure AD에서 보호 하는 Api에 대 한 액세스 토큰을 얻을 수 hello 사용자 단일 페이지 응용 프로그램에 등록 한, 했으므로 [Microsoft Graph](https://graph.microsoft.io)합니다.  Hello를 사용 하 여 토큰을 이미 수신 하는 경우에 `token` response_type, 다시 tooredirect hello 사용자 toosign 필요 없이이 메서드 tooacquire 토큰 tooadditional 리소스를 사용할 수 있습니다.

Hello 일반 OpenID Connect/OAuth 흐름에서는 설정 하려는 요청 toohello v2.0 함으로써 `/token` 끝점입니다.  하지만 hello v2.0 끝점 하므로 tooget 호출 AJAX 수행 하 고 새로 고침 토큰 hello 질문 벗어났습니다 지원 CORS 요청 하지 않습니다.  대신, 다른 웹 Api에 대 한 숨겨진된 iframe tooget 새 토큰의 hello 암시적 흐름을 사용할 수 있습니다. 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> 복사 및 브라우저 탭에 요청 아래 hello를 붙여 넣어 보세요! (Tooreplace hello를 잊지 마십시오 `domain_hint` 및 hello `login_hint` 회원님의 사용자에 대 한 값을 수정 하는 hello 사용 하 여 값)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다.  자세한 내용은 [프로토콜 기본](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| client_id |필수 |응용 프로그램 Id는 hello 등록 포털 hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 응용 프로그램을 할당 합니다. |
| response_type |필수 |OpenID Connect 로그인을 위한 `id_token` 이 포함되어야 합니다.  `code`와 같은 다른 response_types을 포함할 수도 있습니다. |
| redirect_uri |권장 |인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램의 hello redirect_uri입니다.  또한 url로 인코딩되어 있어야 점을 제외 하 고 hello 포털에 등록 된 hello redirect_uris 중 하나에 정확히 일치 해야 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다.  토큰을 가져오는 데 필요한 모든 포함 [범위](active-directory-v2-scopes.md) 관심 있는 hello 리소스에 대 한 필요 합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 토큰 백 tooyour 앱 되어야 하는 hello 방법을 지정 합니다.  `query`, `form_post` 또는 `fragment` 중 하나일 수 있습니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다.  원하는 모든 콘텐츠의 문자열일 수 있습니다.  일반적으로 교차 사이트 요청 위조 공격을 방지하기 위해 임의로 생성된 고유 값이 사용됩니다.  hello 상태 hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |
| nonce |필수 |클레임으로 결과 id_token hello에에서 포함 될 hello 앱에서 생성 하는 hello 요청에 포함 하는 값입니다.  hello 앱이 값 toomitigate 토큰 재생 공격 확인할 수 있습니다.  hello 값은 대개 임의 고유 문자열 사용된 tooidentify hello 원점 hello 요청의 수입니다. |
| prompt |필수 |새로 고침 & 숨겨진된 iframe의 토큰을 가져오기 위해 사용 해야 `prompt=none` iframe hello tooensure hello v 2.0 로그인 페이지에 충돌 하지을 즉시 반환 합니다. |
| login_hint |필수 |새로 고침 & 숨겨진된 iframe의 토큰을 가져오기, 시간에 지정 된 시점 hello 사용자 있을 수 있으며 여러 세션 간에 toodistinguish 순서에에서이 힌트에 hello 사용자의 hello 사용자를 포함 해야 합니다. 이전 로그인에서 hello 사용자 이름을 추출할 수 있습니다 hello를 사용 하 여 `preferred_username` 클레임입니다. |
| domain_hint |필수 |`consumers` 또는 `organizations` 중 하나일 수 있습니다.  새로 고침 & 숨겨진된 iframe의 토큰을 가져오기에 대 한 hello domain_hint hello 요청에 포함 해야 합니다.  Hello를 추출 하도록 `tid` 이전 로그인 toodetermine의 hello id_token에서 어떤 값 toouse 클레임입니다.  경우 hello `tid` 값은 클레임 `9188040d-6c67-4c5b-b112-36a304b66dad`를 사용 해야 `domain_hint=consumers`합니다.  그렇지 않으면 `domain_hint=organizations`를 사용합니다. |

Toohello 작성할 `prompt=none` 매개 변수를이 요청 중 하나 성공 또는 실패 즉시 하 고 됩니다 tooyour 응용 프로그램을 반환 합니다.  성공적인 응답 받게 될 tooyour 응용 프로그램에 표시 된 hello `redirect_uri`, hello에 지정 된 hello 메서드를 사용 하 여 `response_mode` 매개 변수입니다.

#### 성공적인 응답
`response_mode=fragment` 를 사용한 성공적인 응답은 다음과 같습니다.

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| 매개 변수를 포함해야 합니다. | 설명 |
| --- | --- |
| access_token |응용 프로그램 요청 hello는 hello 토큰입니다. |
| token_type |항상 `Bearer`입니다. |
| state |State 매개 변수는 hello 응답에 동일한 값이 표시 되어야 하는 hello hello 요청에 포함 됩니다. hello 앱 hello 요청 및 응답의 hello 상태 값이 동일한 지 확인 해야 합니다. |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |
| scope |액세스 토큰을 hello hello 범위에 대 한 유효 합니다. |

#### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello `redirect_uri` hello 앱 적절 하 게 처리할 수 있도록 합니다.  Hello 경우에서 `prompt=none`, 예상 된 오류 수 있습니다.

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

Hello iframe 요청에이 오류가 나타나면 hello 사용자 대화형으로 로그인 해야 다시 tooretrieve 새 토큰을 합니다.  Toohandle이이 경우 응용 프로그램에 적합 한 방식으로에서 선택할 수 있습니다.

## 토큰 새로 고침
둘 다 `id_token`s 및 `access_token`toorefresh 앱 준비 해야 하므로 이러한 토큰을 주기적으로, s 짧은 기간 후 만료 됩니다.  토큰의 입력 하거나 toorefresh, hello 수행할 수 있습니다 hello를 사용 하 여 위쪽부터 같은 숨겨진된 iframe 요청 `prompt=none` toocontrol Azure AD의 동작 매개 변수입니다.  새 tooreceive 하려는 경우 `id_token`, 있는지 toouse 수 `response_type=id_token` 및 `scope=openid`, 및 `nonce` 매개 변수입니다.

## 로그아웃 요청 보내기
OpenIdConnect hello `end_session_endpoint` 앱 toosend hello v2.0 끝점에서 사용자의 세션 및 명확한 쿠키 설정 요청 toohello v2.0 끝점 tooend 수 있습니다.  toofully 서명 웹 응용 프로그램에서 사용자를 제거, 응용 프로그램 해야 hello 사용자와 자체 세션 (보통 하 여 토큰 캐시를 지우거 나 쿠키를 삭제 하는 중), 종료 및 hello 브라우저를 리디렉션합니다.

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다.  자세한 내용은 [프로토콜 기본](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| post_logout_redirect_uri | 권장 | 로그 아웃 tooafter 완료 사용자 hello hello URL이 반환 되도록 합니다. 이 값 hello 리디렉션 hello 응용 프로그램에 대해 등록 된 Uri 중 하 나와 일치 해야 합니다. 지정 하지 않은 경우 hello 사용자 hello v2.0 끝점에서 일반 메시지를 표시 됩니다. |
