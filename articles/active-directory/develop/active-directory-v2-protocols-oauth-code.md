---
title: "OAuth 권한 부여 코드 흐름 aaaAzure AD v2.0 | Microsoft Docs"
description: "웹 응용 프로그램 빌드 hello OAuth 2.0 인증 프로토콜의 Azure AD의 구현을 사용 합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# v2.0 프로토콜 - OAuth 2.0 인증 코드 흐름
hello OAuth 2.0 인증 코드 부여는 장치 toogain tooprotected 같은 리소스에 액세스 웹 Api에 설치 된 앱에서 사용할 수 있습니다.  OAuth 2.0의 hello 앱 모델 v 2.0 구현을 사용 하 여, 로그인 및 API 액세스 tooyour 모바일 및 데스크톱 앱을 추가할 수 있습니다.  이 가이드는 언어 독립적 이며 하 고 설명 방법을 toosend 우리의 오픈 소스 라이브러리를 사용 하지 않고 HTTP 메시지를 수신 하 고 있습니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
> 
> 

OAuth 2.0 인증 코드 흐름 hello에에서 설명 하는 [섹션 4.1 hello OAuth 2.0 사양의](http://tools.ietf.org/html/rfc6749)합니다.  사용 되는 tooperform 인증 및 권한 부여 포함 하는 응용 프로그램 형식을 hello 대부분 [웹 앱](active-directory-v2-flows.md#web-apps) 및 [고유 하 게 설치 된 앱](active-directory-v2-flows.md#mobile-and-native-apps)합니다.  Toosecurely 획득 access_tokens hello v2.0 끝점을 사용 하 여 보안이 유지 되는 리소스를 사용 하는 tooaccess 될 수 있는 앱 수 있습니다.  

## 프로토콜 다이어그램
상위 수준에서 네이티브/모바일 응용 프로그램에 대 한 hello 전체 인증 흐름은 약간 다음과 같습니다.

![OAuth 인증 코드 흐름](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## 인증 코드 요청
hello 클라이언트 hello 사용자 toohello 전달로 시작 하는 hello 권한 부여 코드 흐름 `/authorize` 끝점입니다.  이 요청에서 hello 클라이언트 hello 사용자 로부터 tooacquire 필요한 hello 권한을 나타냅니다.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> 이 요청 hello tooexecute 아래에 링크를 클릭 하세요. 로그인 한 후 브라우저 리디렉션되어야 너무`https://localhost/myapp/` 와 `code` hello 주소 표시줄에 있습니다.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다.  자세한 내용은 [프로토콜 기본](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| client_id |필수 |응용 프로그램 Id는 hello 등록 포털 hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 응용 프로그램을 할당 합니다. |
| response_type |필수 |포함 해야 `code` hello 권한 부여 코드 흐름에 대 한 합니다. |
| redirect_uri |권장 |인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램의 hello redirect_uri입니다.  또한 url로 인코딩되어 있어야 점을 제외 하 고 hello 포털에 등록 된 hello redirect_uris 중 하나에 정확히 일치 해야 합니다.  네이티브 및 모바일 앱의 hello 기본값을 사용 해야 `https://login.microsoftonline.com/common/oauth2/nativeclient`합니다. |
| scope |필수 |공백으로 구분 된 목록이 [범위](active-directory-v2-scopes.md) 를 hello 사용자 tooconsent 되도록 합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 토큰 백 tooyour 앱 되어야 하는 hello 방법을 지정 합니다.  `query` 또는 `form_post`일 수 있습니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다.  원하는 모든 콘텐츠의 문자열일 수 있습니다.  일반적으로 [교차 사이트 요청 위조 공격을 방지](http://tools.ietf.org/html/rfc6749#section-10.12)하기 위해 임의로 생성된 고유 값이 사용됩니다.  hello 상태 hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |
| prompt |선택 사항 |Hello 필요한 사용자 상호 작용 유형을 나타냅니다.  이 이번에 유효한 값은 '로그인' 'none', 전용 hello 및 '승인'.  `prompt=login`force를 사용자 tooenter hello 됩니다에 단일 로그인 부정 해당 요청에 자격 증명입니다.  `prompt=none`반대 hello이 방법을 사용 하면 해당 hello 사용자 모든 대화형 프롬프트도 표시 되지 않았습니다.  Single sign-on을 통해 hello 요청을 자동으로 완료할 수 없으면, hello v2.0 끝점 오류가 반환 됩니다.  `prompt=consent`대화 상자에서는 hello 사용자가 로그인 한 후 hello 사용자 toogrant 권한 toohello 앱 타고 트리거 hello OAuth 합니다. |
| login_hint |선택 사항 |수의 hello 사용된 toopre 채우기 hello 사용자 이름/전자 메일 주소 필드 서명할 수 hello 사용자에 대 한 페이지에 자신의 사용자 이름을 미리 알고 있는 경우.  종종 앱 hello username 이전 로그인에서 추출 된 이미 있으면 다시 인증 하는 동안이 매개 변수를 사용 합니다 hello를 사용 하 여 `preferred_username` 클레임입니다. |
| domain_hint |선택 사항 |`consumers` 또는 `organizations` 중 하나일 수 있습니다.  Hello 전자 메일 기반 검색 프로세스는 건너뜁니다 포함 하는 경우 해당 사용자가을 통해 hello v 2.0 로그인 페이지를 앞에 tooa 약간 더 사용자 경험을 간소화 합니다.  종종 앱 다시 인증 하는 동안 hello를 추출 하 여에이 매개 변수를 사용 합니다 `tid` 에서 이전 로그인 합니다.  경우 hello `tid` 값은 클레임 `9188040d-6c67-4c5b-b112-36a304b66dad`를 사용 해야 `domain_hint=consumers`합니다.  그렇지 않으면 `domain_hint=organizations`를 사용합니다. |

Hello 사용자 됩니다이 시점에서 자격 증명 및 전체 hello 인증 tooenter 라는 메시지가 표시 됩니다.  hello v2.0 끝점도 방법을 사용 하면 해당 hello 사용자가 동의 hello에 표시 된 toohello 사용 권한만 `scope` 쿼리 매개 변수입니다.  Hello 사용자가 이러한 사용 권한 중 tooany 동의한 하지 것 묻습니다 hello 사용자 tooconsent toohello 필요한 사용 권한.  [사용 권한, 동의 및 다중 테넌트 앱의 세부 정보는 여기에 제공되어 있습니다](active-directory-v2-scopes.md).

Hello v2.0 끝점에 표시 된 hello 응답 tooyour 응용 프로그램을 반환 합니다 hello 사용자를 인증 하 고 동의 허용 하면 `redirect_uri`, hello에 지정 된 hello 메서드를 사용 하 여 `response_mode` 매개 변수입니다.

#### 성공적인 응답
`response_mode=query` 를 사용한 성공적인 응답은 다음과 같습니다.

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| 매개 변수를 포함해야 합니다. | 설명 |
| --- | --- |
| 코드 |응용 프로그램 요청 hello authorization_code를 hello 합니다. hello 앱 hello 대상 리소스에 대 한 hello 권한 부여 코드 toorequest 액세스 토큰을 사용할 수 있습니다.  authorization_code는 수명이 매우 짧으며, 일반적으로 약 10분 후에 만료됩니다. |
| state |State 매개 변수는 hello 응답에 동일한 값이 표시 되어야 하는 hello hello 요청에 포함 됩니다. hello 앱 hello 요청 및 응답의 hello 상태 값이 동일한 지 확인 해야 합니다. |

#### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello `redirect_uri` hello 앱 적절 하 게 처리할 수 있도록 합니다.

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

#### 권한 부여 끝점 오류에 대한 오류 코드
hello 다음 표에서 hello hello에 반환 될 수 있는 다양 한 오류 코드 `error` hello 오류 응답의 매개 변수입니다.

| 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- |
| invalid_request |프로토콜 오류(예: 필수 매개 변수 누락). |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 설정 중에 발견되는 개발 오류입니다. |
| unauthorized_client |hello 클라이언트 응용 프로그램 없으면 toorequest 인증 코드를 허용 합니다. |이 문제는 일반적으로 hello 클라이언트 응용 프로그램이 Azure AD에 등록 되어 있지 않거나 toohello 사용자의 Azure AD 테 넌 트에 추가 되지 않습니다 때 발생 합니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| access_denied |리소스 소유자가 동의 거부 |hello 클라이언트 응용 프로그램 hello 사용자가 동의 하지 않는 한 진행할 수 hello 사용자에 게 알릴 수 있습니다. |
| unsupported_response_type |hello 권한 부여 서버 hello 요청에 hello 응답 유형을 지원 하지 않습니다. |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 설정 중에 발견되는 개발 오류입니다. |
| server_error |hello 서버 오류가 발생 했습니다. |Hello 요청을 다시 시도 합니다. 이러한 오류는 일시적인 상태 때문에 발생할 수 있습니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 해당 응답은 일시적 오류로 인해 지연 합니다. |
| temporarily_unavailable |hello 서버 사용량이 많음 toohandle hello 요청 일시적으로입니다. |Hello 요청을 다시 시도 합니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 해당 응답은 일시적 상태로 인해 지연 합니다. |
| invalid_resource |hello 대상 리소스가 존재 하지 않는, Azure AD를 찾을 수 없거나 올바르게 구성 되지 않아 유효 하지 않습니다. |이 hello 리소스 있을 경우 구성 되지 않았습니다 hello 테 넌 트에 나타냅니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |

## 액세스 토큰 요청
Hello를 교환할 수 있습니다는 authorization_code 획득 했습니다 하 고 hello 사용자 권한이 부여 된 `code` 에 대 한 프로그램 `access_token` toohello 전송 하 여 리소스를 원하는 `POST` toohello 요청 `/token` 끝점:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Postman에서 이 요청을 실행해 보세요. (Tooreplace hello를 잊지 마십시오 `code`) [ ![우체부에서 실행](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다.  자세한 내용은 [프로토콜 기본](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| client_id |필수 |응용 프로그램 Id는 hello 등록 포털 hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 응용 프로그램을 할당 합니다. |
| grant_type |필수 |해야 `authorization_code` hello 권한 부여 코드 흐름에 대 한 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다.  hello 범위가이 레그에 해당 하는 tooor hello 범위의 하위 집합 요청 hello 첫 번째 레그에 요청 했습니다.  이 요청에 지정 된 hello 범위에 걸쳐 여러 리소스 서버를 hello v2.0 끝점 hello 첫 번째 범위에 지정 된 hello 리소스에 대 한 토큰을 반환 합니다.  에 대 한 범위는 보다 자세한 설명은 참조 너무[권한과 승인 범위](active-directory-v2-scopes.md)합니다. |
| 코드 |필수 |hello hello 흐름의 첫 번째 레그에서 복사한 hello authorization_code 합니다. |
| redirect_uri |필수 |사용 되는 tooacquire hello authorization_code 했던 동일한 redirect_uri 값을 hello 합니다. |
| client_secret |웹앱에 필요 |앱에 대 한 hello 응용 프로그램 등록 포털에서 만든 hello 응용 프로그램 암호입니다.  장치에 client_secret을 안정적으로 저장할 수 없으므로 네이티브 앱에서는 사용하면 안 됩니다.  웹 앱 및 웹 Api hello 서버 쪽에서 hello 기능 toostore hello client_secret를 안전 하 게 포함 하는 필수입니다. |

#### 성공적인 응답
성공적인 토큰 응답은 다음과 같습니다.

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| 매개 변수 | 설명 |
| --- | --- |
| access_token |hello 요청 된 액세스 토큰입니다. hello 앱이 토큰 tooauthenticate toohello web API와 같은 리소스에 보안을 사용할 수 있습니다. |
| token_type |Hello 토큰 형식 값을 나타냅니다. hello만 된 Azure AD가 지 원하는 형식이 전달자 |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |
| scope |access_token hello hello 범위에 대 한 유효 합니다. |
| refresh_token |OAuth 2.0 새로 고침 토큰입니다. hello 앱 צ ְ ײ이 토큰 hello 현재 액세스 토큰이 만료 된 후 추가 액세스 토큰을 획득 합니다.  Refresh_tokens는 수명이 긴 되며 오랜 시간에 사용 되는 tooretain 액세스 tooresources를 사용할 수 있습니다.  자세한 정보를 얻기 위해 toohello 참조 [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다. |
| id_token |서명되지 않은 JWT(JSON 웹 토큰)입니다. hello 앱 수 base64Url hello 사용자 로그인에 대 한이 토큰 toorequest 정보의 hello 세그먼트를 디코드합니다. hello 앱 hello 값을 캐시를 업데이트 하 고를 표시할 수 있지만 것에 의존 하지 않아야 하 보안 경계 또는 권한 부여 합니다.  Id_tokens에 대 한 자세한 내용은 참조 hello [v2.0 끝점 토큰 참조](active-directory-v2-tokens.md)합니다. |

#### 오류 응답
오류 응답은 다음과 같습니다.

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |
| error_codes |진단에 도움이 될 수 있는 STS 특정 오류 코드의 목록입니다. |
| timestamp |hello hello 오류가 발생 한 시간입니다. |
| trace_id |진단에 도움이 될 수 있는 hello 요청에 대 한 고유 식별자입니다. |
| correlation_id |구성 요소에서 진단에 도움이 될 수 있는 hello 요청에 대 한 고유 식별자입니다. |

#### 토큰 끝점 오류에 대한 오류 코드
| 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- |
| invalid_request |프로토콜 오류(예: 필수 매개 변수 누락). |수정 하 고 hello 요청을 다시 제출 하십시오. |
| invalid_grant |hello 권한 부여 코드가 잘못 되었거나 만료 되었습니다. |새 요청 toohello 시도 `/authorize` 끝점 |
| unauthorized_client |hello 인증 된 클라이언트에 권한이 없습니다 toouse이 권한이 부여 허용 형식입니다. |이 문제는 일반적으로 hello 클라이언트 응용 프로그램이 Azure AD에 등록 되어 있지 않거나 toohello 사용자의 Azure AD 테 넌 트에 추가 되지 않습니다 때 발생 합니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| invalid_client |클라이언트 인증에 실패했습니다. |hello 클라이언트 자격 증명이 올바르지 않습니다. toofix, 응용 프로그램 관리자에 게 hello 자격 증명을 업데이트합니다. |
| unsupported_grant_type |hello 권한 부여 서버 hello 권한 부여 허용 유형을 지원 하지 않습니다. |변경 hello 형식 hello 요청에 권한을 부여 합니다. 이 유형의 오류는 개발 중에만 발생하며 초기 테스트 중에 검색됩니다. |
| invalid_resource |hello 대상 리소스가 존재 하지 않는, Azure AD를 찾을 수 없거나 올바르게 구성 되지 않아 유효 하지 않습니다. |이 hello 리소스 있을 경우 구성 되지 않았습니다 hello 테 넌 트에 나타냅니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| interaction_required |hello 요청 사용자 상호 작용이 필요합니다. 예를 들어 추가 인증 단계가 필요합니다. |Hello로 hello 요청을 다시 시도 같은 리소스입니다. |
| temporarily_unavailable |hello 서버 사용량이 많음 toohandle hello 요청 일시적으로입니다. |Hello 요청을 다시 시도 합니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 해당 응답은 일시적 상태로 인해 지연 합니다. |

## Hello 액세스 토큰을 사용 하 여
성공적으로 인식 한 했으므로 `access_token`, hello에 포함 하 여 hello 토큰 요청 tooWeb Api에서에서 사용할 수 있습니다 `Authorization` 헤더:

> [!TIP]
> Postman에서 이 요청을 실행하세요. (Hello 대체 `Authorization` 헤더 첫 번째) [ ![우체부에서 실행](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Hello 액세스 토큰 새로 고침
Access_tokens 짧은 활성 이며 리소스에 액세스 하는 toocontinue를 만료 된 후 새로 고쳐야 합니다.  다른 전송 하 여 그렇게 할 수 `POST` toohello 요청 `/token` 끝점 hello를 제공 하는이 시간 `refresh_token` hello 대신 `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Postman에서 이 요청을 실행해 보세요. (Tooreplace hello를 잊지 마십시오 `refresh_token`) [ ![우체부에서 실행](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  hello 가능한 값은 `common`, `organizations`, `consumers`, 및 식별자를 테 넌 트입니다.  자세한 내용은 [프로토콜 기본](active-directory-v2-protocols.md#endpoints)을 참조하세요. |
| client_id |필수 |응용 프로그램 Id는 hello 등록 포털 hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 응용 프로그램을 할당 합니다. |
| grant_type |필수 |해야 `refresh_token` hello 권한 부여 코드 흐름의이 레그에 대 한 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다.  hello 범위가이 레그에 해당 하는 tooor hello 범위의 하위 집합 요청 hello 원래 authorization_code 요청 레그에서 요청 했습니다.  이 요청에 지정 된 hello 범위에 걸쳐 여러 리소스 서버를 hello v2.0 끝점 hello 첫 번째 범위에 지정 된 hello 리소스에 대 한 토큰을 반환 합니다.  에 대 한 범위는 보다 자세한 설명은 참조 너무[권한과 승인 범위](active-directory-v2-scopes.md)합니다. |
| refresh_token |필수 |hello hello 흐름의 두 번째 레그에서 복사한 hello refresh_token입니다. |
| redirect_uri |필수 |사용 되는 tooacquire hello authorization_code 했던 동일한 redirect_uri 값을 hello 합니다. |
| client_secret |웹앱에 필요 |앱에 대 한 hello 응용 프로그램 등록 포털에서 만든 hello 응용 프로그램 암호입니다.  장치에 client_secret을 안정적으로 저장할 수 없으므로 네이티브 앱에서는 사용하면 안 됩니다.  웹 앱 및 웹 Api hello 서버 쪽에서 hello 기능 toostore hello client_secret를 안전 하 게 포함 하는 필수입니다. |

#### 성공적인 응답
성공적인 토큰 응답은 다음과 같습니다.

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| 매개 변수 | 설명 |
| --- | --- |
| access_token |hello 요청 된 액세스 토큰입니다. hello 앱이 토큰 tooauthenticate toohello web API와 같은 리소스에 보안을 사용할 수 있습니다. |
| token_type |Hello 토큰 형식 값을 나타냅니다. hello만 된 Azure AD가 지 원하는 형식이 전달자 |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |
| scope |access_token hello hello 범위에 대 한 유효 합니다. |
| refresh_token |새 OAuth 2.0 새로 고침 토큰입니다. 이전 새로 고침 hello를 교체 해야이 새로 얻은 새로 고침 토큰 tooensure와 토큰 새로 고침 토큰이 유효한 상태를 유지 가능한 한 오랫동안 합니다. |
| id_token |서명되지 않은 JWT(JSON 웹 토큰)입니다. hello 앱 수 base64Url hello 사용자 로그인에 대 한이 토큰 toorequest 정보의 hello 세그먼트를 디코드합니다. hello 앱 hello 값을 캐시를 업데이트 하 고를 표시할 수 있지만 것에 의존 하지 않아야 하 보안 경계 또는 권한 부여 합니다.  Id_tokens에 대 한 자세한 내용은 참조 hello [v2.0 끝점 토큰 참조](active-directory-v2-tokens.md)합니다. |

#### 오류 응답
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열 사용된 tooclassify 유형의 오류가 발생 하는 수 있으며 사용 되는 tooreact tooerrors 수입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |
| error_codes |진단에 도움이 될 수 있는 STS 특정 오류 코드의 목록입니다. |
| timestamp |hello hello 오류가 발생 한 시간입니다. |
| trace_id |진단에 도움이 될 수 있는 hello 요청에 대 한 고유 식별자입니다. |
| correlation_id |구성 요소에서 진단에 도움이 될 수 있는 hello 요청에 대 한 고유 식별자입니다. |

에 대 한 설명은 hello 오류 코드 및 hello 권장 되는 클라이언트 작업을 참조 하세요 [토큰 끝점 오류에 대 한 오류 코드](#error-codes-for-token-endpoint-errors)합니다.

