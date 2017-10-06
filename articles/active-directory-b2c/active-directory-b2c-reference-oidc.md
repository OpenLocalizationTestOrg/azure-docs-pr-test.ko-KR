---
title: "OpenID Connect를 사용하는 웹 로그인 - Azure AD B2C | Microsoft Docs"
description: "Hello OpenID Connect 인증 프로토콜의 hello Azure Active Directory 구현을 사용 하 여 웹 응용 프로그램 빌드"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: OpenID Connect로 웹 로그인
OpenID Connect는 OAuth 2.0 사용된 toosecurely tooweb 응용 프로그램에서 사용자를 로그인 일 수 있는 기반으로 하는 인증 프로토콜, 합니다. Hello Azure Active Directory B2C (Azure AD B2C) 구현 OpenID Connect를 사용 하 여 등록, 로그인을 아웃소싱하 수 및 기타 id 관리 웹 응용 프로그램 tooAzure Active Directory (Azure AD)에 발생 합니다. 이 가이드에서는 toodo 언어에 관계 없이 등입니다. 설명 방법을 toosend 우리의 오픈 소스 라이브러리를 사용 하지 않고 HTTP 메시지를 수신 하 고 있습니다.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) hello OAuth 2.0 확장 *권한 부여* 로 사용 하기 위해 프로토콜은 *인증* 프로토콜입니다. 이 OAuth를 사용 하 여 tooperform single sign on 허용 합니다. Hello 개념을 도입는 *ID 토큰*, hello 사용자의 id를 hello hello 클라이언트 tooverify 허용 하는 보안 토큰 변수가 고 hello 사용자에 대 한 기본 프로필 정보를 가져옵니다.

OAuth 2.0을 확장 하기 때문에를 통해 있습니다 toosecurely 획득 한 앱 *액세스 토큰*합니다. 의해 보안 되는 access_tokens tooaccess 리소스를 사용할 수는 [권한 부여 서버](active-directory-b2c-reference-protocols.md#the-basics)합니다. OpenID Connect는 서버에서 호스트되고 브라우저를 통해 액세스되는 웹 응용 프로그램을 빌드하는 경우에 권장됩니다. Azure AD B2C를 사용 하 여 tooadd identity 관리 tooyour 모바일 또는 데스크톱 응용 프로그램을 원하는 경우 사용 해야 [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) OpenID Connect 대신 합니다.

Azure AD B2C hello 표준 OpenID Connect 프로토콜 toodo 둘 이상의 단순 인증 및 권한 부여를 확장합니다. Hello 도입 [정책 매개 변수](active-directory-b2c-reference-policies.md), 있습니다 toouse OpenID Connect tooadd의 사용자 환경을-와 같은 등록, 로그인 및 프로필 관리-tooyour 응용 프로그램입니다. 여기에 대해서도 소개 어떻게 toouse OpenID Connect 및 정책 tooimplement 이러한 각 웹 응용 프로그램에서 발생 합니다. 또한 보여줍니다 어떻게 tooget 액세스 토큰에 액세스 하기 위한 web Api입니다.

hello 다음 섹션의 예에서는 HTTP 요청 hello 우리의 샘플 B2C 디렉터리, fabrikamb2c.onmicrosoft.com,으로 샘플 응용 프로그램, https://aadb2cplayground.azurewebsites.net, 및 정책을 사용 합니다. 자유 다 hello 아웃 tootry 직접 이러한 값을 사용 하 여 요청 또는 사용자의 정보로 바꿀 수 있습니다.
너무 방법에 대해 알아봅니다[B2C 테 넌 트, 응용 프로그램 및 정책을](#use-your-own-b2c-directory)합니다.

## <a name="send-authentication-requests"></a>인증 요청 보내기
Tooauthenticate hello 사용자 필요 하 고 정책을 실행 하는 웹 앱을 디렉션할 수 있습니다 hello 사용자 toohello `/authorize` 끝점입니다. Hello 사용자 이루어지는 hello 정책에 따라 hello 흐름의 hello 대화형 부분입니다.

이 요청 hello 클라이언트 hello에 hello 사용자 로부터 tooacquire 필요 함을 hello 사용 권한을 나타냅니다. `scope` hello에 매개 변수 및 hello 정책 tooexecute `p` 매개 변수입니다. 각각 다른 정책을 사용 하 여 다음 섹션 (줄 바꿈 가독성을 높이기 위해)를 포함 하는 hello에 세 가지 예제 제공 됩니다. 각 요청 작동 방식에 대 한 느낌 tooget 브라우저와 실행에 붙여넣기 hello 요청을 시도 하십시오.

#### <a name="use-a-sign-in-policy"></a>로그인 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>등록 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>편집 프로필 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| client_id |필수 |hello 응용 프로그램 ID는 hello [Azure 포털](https://portal.azure.com/) tooyour 응용 프로그램을 할당 합니다. |
| response_type |필수 |OpenID Connect에 대 한 ID 토큰을 포함 해야 하는 hello 응답 유형입니다. 웹 API를 호출하기 위한 토큰이 웹앱에 필요한 경우 여기서 수행한 대로 `code+id_token`을 사용할 수 있습니다. |
| redirect_uri |권장 |hello `redirect_uri` 인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램의 매개 변수입니다. Hello 중 하 나와 정확히 일치 해야 `redirect_uri` URL로 인코딩되어 있어야 한다는 hello 포털에서 등록 하는 매개 변수입니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다. 단일 범위 값이 요청 되는 권한을 모두 tooAzure AD를 나타냅니다. hello `openid` 범위 ID 토큰 (자세한. toocome hello 문서의 뒷부분에 나오는이 됨)의 hello 형태로 hello 사용자에 대 한 사용자 및 get 데이터 hello 권한 toosign을 나타냅니다. hello `offline_access` 범위는 웹 앱에 대 한 선택 사항입니다. 앱에서 필요한 나타냅니다는 *새로 고침 토큰* 수명이 긴 액세스 tooresources에 대 한 합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 권한 부여 코드 백 tooyour 앱 되어야 하는 hello 메서드. `query`, `form_post` 또는 `fragment` 중 하나일 수 있습니다.  hello `form_post` 응답 모드는 최상의 보안 권장 합니다. |
| state |권장 |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. 일반적으로 교차 사이트 요청 위조 공격을 방지하기 위해 임의로 생성된 고유 값이 사용됩니다. hello 상태 hello 페이지에 있는 것 처럼 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |
| nonce |필수 |클레임으로 hello 결과 ID 토큰에 포함 됩니다 (hello 앱에서 생성) hello 요청에 포함 하는 값입니다. hello 앱이 값 toomitigate 토큰 재생 공격 확인할 수 있습니다. hello 값은 일반적으로 사용 되는 tooidentify hello 원점 hello 요청의 수 있는 고유 문자열로 서 임의 합니다. |
| p |필수 |실행 될 hello 정책입니다. B2C 테 넌 트에서 생성 하는 정책의 hello 이름입니다. 정책 이름 값 hello로 시작 해야 `b2c\_1\_`합니다. 정책 및 hello에 대 한 자세한 정보에 대해 알아봅니다 [확장 가능한 정책 프레임 워크](active-directory-b2c-reference-policies.md)합니다. |
| prompt |옵션 |필요한 사용자 상호 작용의 hello 형식입니다. hello이 이번에만 유효한 값은 `login`, 어떤 강제로 hello 사용자 tooenter 해당 요청에 자격 증명입니다. Single Sign-On은 적용되지 않습니다. |

이 시점에서 hello 사용자 toocomplete hello 정책 워크플로 요청. 그러면 hello 디렉터리 또는 hello 정책 정의 되는 방식에 따라 단계의 다른 모든 숫자에 등록 한 소셜 id를 사용 하 여 로그인 hello 사용자 이름과 암호를 입력 만들어질 수 있습니다.

Azure AD에 표시 된 hello에서 응답 tooyour 앱 반환 hello 사용자 hello 정책 완료 된 후 `redirect_uri` hello에 지정 된 hello 메서드를 사용 하 여 매개 변수를 `response_mode` 매개 변수입니다. hello 응답 각 앞의 경우 실행 되는 hello 정책 무관 hello에 대 한 동일한 hello 됩니다.

`response_mode=fragment` 를 사용한 성공적인 응답은 다음과 같습니다.

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| 매개 변수 | 설명 |
| --- | --- |
| id_token |ID 토큰을 요청 하는 응용 프로그램 hello hello 합니다. Hello ID 토큰 tooverify hello 사용자 id를 사용 하 여 수 있으며 hello 사용자와 세션을 시작할 수 있습니다. ID 토큰 및 해당 내용에 대 한 자세한 내용은 hello에 포함 된 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. |
| 코드 |hello 권한 부여 코드 요청 hello 앱 사용 하는 경우 `response_type=code+id_token`합니다. hello 앱 대상 리소스에 대 한 hello 권한 부여 코드 toorequest 액세스 토큰을 사용할 수 있습니다. 인증 코드는 수명이 매우 짧습니다. 일반적으로 약 10분 후에 만료됩니다. |
| state |경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다. |

오류 응답 toohello 전송 되기도 `redirect_uri` hello 앱 적절 하 게 처리할 수 있도록 매개 변수:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| 매개 변수 | 설명 |
| --- | --- |
| error |사용 되는 tooclassify 유형의 오류가 발생 하 고 사용 하는 tooreact tooerrors 일 수 있는 일 수 있는 오류 코드 문자열입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |
| state |이 섹션의 hello 첫 번째 테이블의 hello 전체 설명을 참조 하십시오. 경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다. |

## <a name="validate-hello-id-token"></a>Hello ID 토큰 유효성 검사
ID 토큰을 받는 방금 충분 한 tooauthenticate hello 사용자가 아닙니다. Hello ID 토큰 서명의 유효성을 검사 하 고 응용 프로그램의 요구 사항에 따라 hello 토큰의 hello 클레임을 확인 해야 합니다. 사용 하 여 azure AD B2C [JSON 웹 토큰 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) 및 공개 키 암호화 toosign 토큰 및 유효한 지 확인 합니다.

기본 설정의 언어에 따라 JWT의 유효성 검사에 사용할 수 있는 다양한 공개 소스 라이브러리가 있습니다. 고유한 유효성 검사 논리를 구현하는 것보다 이러한 옵션을 탐색하는 것이 좋습니다. 여기에 hello 정보는 tooproperly 해당 라이브러리를 사용 하는 방법을 파악 유용 합니다.

Azure AD B2C 런타임 시 Azure AD B2C에 대 한 앱 toofetch 정보가 있는에서는 OpenID Connect 메타 데이터 끝점을 있습니다. 이 정보에는 끝점, 토큰 콘텐츠 및 토큰 서명 키가 포함됩니다. B2C 테넌트에서 각 정책에 대한 JSON 메타데이터 문서가 있습니다. Hello에 대 한 메타 데이터 문서의 예를 들어 hello `b2c_1_sign_in` 에서 정책을 `fabrikamb2c.onmicrosoft.com` 에:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

이 구성 문서의 hello 속성 중 하나는 `jwks_uri`, 동일한 정책을 것 hello에 대 한 값:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

정책을 사용한 toodetermine ID 토큰에 서명 하 고 여기서 toofetch hello 메타 데이터에서를 두 가지 옵션이 있습니다. 첫째, hello 정책 이름을 ´ â hello `acr` hello ID 토큰에서 클레임입니다. 참조 hello tooparse hello ID 토큰에서 요구 하는 방법에 대 한 내용은 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. 다른 옵션은 hello hello 값에서 tooencode hello 정책 `state` hello 요청을 발급 하 고 정책을 사용한 toodetermine 디코딩할 때 매개 변수입니다. 두 방법 중 하나는 유효합니다.

Hello OpenID Connect 메타 데이터 끝점에서 메타 데이터 문서 hello를 구입한 후 hello 256 RSA 공개 키 (이 끝점에)을 사용할 수 있습니다 hello ID 토큰의 toovalidate hello 서명을 합니다. 지정된 시점에 이 끝점에 나열된 키가 여러 개 있을 수 있으며, 각 키는 `kid` 클레임으로 식별됩니다. hello hello ID 토큰의 헤더도 포함 되어는 `kid` 클레임 이러한 키 중 어떤 토큰이 사용 되는 toosign hello ID 나타냅니다. 자세한 내용은 참조 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md) (섹션에 hello [토큰 유효성을 검사 하](active-directory-b2c-reference-tokens.md#token-validation), 특히).
<!--TODO: Improve hello information on this-->

Hello hello ID 토큰 서명의 유효성을 검사 한 후에 다음과 같은 여러 클레임 tooverify 해야 하는. 예:

* Hello 유효성을 검사 해야 `nonce` tooprevent 토큰 재생 공격을 주장 합니다. Hello 로그인 요청에 지정 된 해당 값 이어야 합니다.
* Hello 유효성을 검사 해야 `aud` 클레임 ID 토큰 hello tooensure 응용 프로그램에 대해 실행 되었습니다. 해당 값에는 응용 프로그램의 응용 프로그램 ID hello 이어야 합니다.
* Hello 유효성을 검사 해야 `iat` 및 `exp` 클레임 ID 토큰 hello tooensure가 만료 되지 않았습니다.

또한 수행해야 하는 몇 가지 추가 유효성 검사가 있습니다. Hello에 자세히 설명 되어 [OpenID 연결 핵심 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다.  시나리오에 따라 toovalidate 추가 클레임을 할 수 있습니다. 몇 가지 일반적인 유효성 검사는 다음과 같습니다.

* 확인 하는 hello 사용자/조직에 등록 하 여 hello 앱에 대 한 합니다.
* 해당 hello 사용자에 게 적절 한 인증/권한 확인 합니다.
* Azure Multi-Factor Authentication과 같은 특정 강도의 인증이 발생했는지 확인

ID 토큰에서 클레임 hello에 대 한 자세한 내용은 참조 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.

Hello ID 토큰을 검사 한 후에 hello 사용자와 세션을 시작할 수 있습니다. 응용 프로그램에서 hello 사용자에 대 한 hello ID 토큰 tooobtain 정보 hello 클레임을 사용할 수 있습니다. 이 정보의 용도로 표시, 레코드 및 권한 부여가 있습니다.

## <a name="get-a-token"></a>토큰 가져오기
정책 실행를 건너뛸 수 웹 응용 프로그램 tooonly가 필요한 경우 다음 섹션에서는 hello 합니다. 이러한 섹션은 적용 가능한 유일한 tooweb 앱 필요한 인증 toomake 호출 tooa 웹 API 및 Azure AD B2C로도 보호입니다.

복사한 hello 인증 코드를 교환할 수 있습니다 (사용 하 여 `response_type=code+id_token`) 전송 하 여 토큰 toohello 필요한 리소스는 `POST` toohello 요청 `/token` 끝점입니다. 현재 hello에 대 한 토큰을 요청할 수 있는 리소스에만 응용 프로그램 자체의 백 엔드 웹 API. 요청 토큰 tooyourself hello 규칙은 toouse hello 범위와 앱의 클라이언트 ID입니다.

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| p |필수 |사용 하는 tooacquire hello 권한 부여 정책 hello 코드입니다. 이 요청에 다른 정책을 사용할 수 없습니다. 이 매개 변수 toohello 쿼리 문자열, 하지 toohello를 추가할 `POST` 본문입니다. |
| client_id |필수 |hello 응용 프로그램 ID는 hello [Azure 포털](https://portal.azure.com/) tooyour 응용 프로그램을 할당 합니다. |
| grant_type |필수 |해야 하는 권한 부여 유형을 hello `authorization_code` hello 권한 부여 코드 흐름에 대 한 합니다. |
| scope |권장 |공백으로 구분된 범위 목록입니다. 단일 범위 값이 요청 되는 권한을 모두 tooAzure AD를 나타냅니다. hello `openid` 범위 hello id_token 매개 변수 형식으로의 hello 사용자에 대 한 사용자 및 get 데이터 hello 권한 toosign을 나타냅니다. 사용 되는 tooget 토큰 tooyour 응용 프로그램 자체의 백 엔드 웹 API를 hello 요소로 표시 되는 것 hello 클라이언트와 같은 응용 프로그램 ID입니다. hello `offline_access` 앱 새로 고침 토큰 수명이 긴 액세스 tooresources에 대 한에서 필요한 범위를 나타냅니다. |
| 코드 |필수 |hello hello 흐름의 첫 번째 레그에서 복사한 hello 권한 부여 코드입니다. |
| redirect_uri |필수 |hello `redirect_uri` hello 인증 코드를 받는 hello 응용 프로그램의 매개 변수입니다. |
| client_secret |필수 |hello에 생성 된 hello 응용 프로그램 암호 [Azure 포털](https://portal.azure.com/)합니다. 이 응용 프로그램 암호는 중요한 보안 아티팩트입니다. 서버에 안전하게 저장해야 합니다. 또한 이 클라이언트 비밀도 정기적으로 회전해야 합니다. |

성공적인 토큰 응답은 다음과 같습니다.

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| 매개 변수 | 설명 |
| --- | --- |
| not_before |hello 시간은 hello에 토큰은 유효한 것으로 간주, epoch 시간에서입니다. |
| token_type |hello 토큰 유형 값입니다. Azure AD에서는 형식만 hello `Bearer`합니다. |
| access_token |hello 사용자가 요청한 JWT 토큰을 서명 합니다. |
| scope |hello 범위는 hello에 대 한 토큰은 유효 합니다. 나중에 사용할 수 있도록 토큰 캐싱에 사용할 수 있습니다. |
| expires_in |액세스 토큰을 hello는 시간의 hello 길이 (초)에서 유효 합니다. |
| refresh_token |OAuth 2.0 새로 고침 토큰입니다. hello 앱 hello 현재 토큰 만료 된 후이 토큰 tooacquire 추가 토큰을 사용할 수 있습니다. 새로 고침 토큰 수명이 긴 되며 오랜 시간에 사용 되는 tooretain 액세스 tooresources를 사용할 수 있습니다. 자세한 내용은 참조 toohello [B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. 참고 해야 사용 hello 범위 `offline_access` hello 권한 부여와 토큰 요청 순서 tooreceive에 새로 고침 토큰입니다. |

오류 응답은 다음과 같습니다.

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 매개 변수 | 설명 |
| --- | --- |
| error |사용 되는 tooclassify 유형의 오류가 발생 하 고 사용 하는 tooreact tooerrors 일 수 있는 일 수 있는 오류 코드 문자열입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

## <a name="use-hello-token"></a>Hello 토큰을 사용 하 여
Hello에 포함 하 여 hello 토큰을 사용할 요청 tooyour 백 엔드 웹 Api에에서 수 있는 액세스 토큰을 획득 성공적으로 했습니다 이제 `Authorization` 헤더:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Hello 토큰 새로 고침
ID 토큰은 수명이 짧습니다. 수 tooaccess 리소스 되 고 toocontinue를 만료 된 후 해당를 새로 고쳐야 합니다. 다른 전송 하 여 그렇게 할 수 `POST` toohello 요청 `/token` 끝점입니다. 이 시간 제공 hello `refresh_token` hello 대신 매개 변수 `code` 매개 변수:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| 매개 변수 | 필수 | 설명 |
| --- | --- | --- |
| p |필수 |사용 되는 tooacquire hello 원래 새로 고침 토큰을 hello 정책입니다. 이 요청에 다른 정책을 사용할 수 없습니다. 이 매개 변수 toohello 쿼리 문자열, toohello POST 본문 아닌 추가 하면 note 합니다. |
| client_id |필수 |hello 응용 프로그램 ID는 hello [Azure 포털](https://portal.azure.com/) tooyour 응용 프로그램을 할당 합니다. |
| grant_type |필수 |hello 유형의 grant으로,이 다리 hello 권한 부여 코드 흐름의에 대 한 새로 고침 토큰 이어야 합니다. |
| scope |권장 |공백으로 구분된 범위 목록입니다. 단일 범위 값이 요청 되는 권한을 모두 tooAzure AD를 나타냅니다. hello `openid` 범위 ID 토큰의 hello 형태로 hello 사용자에 대 한 사용자 및 get 데이터 hello 권한 toosign을 나타냅니다. 사용 되는 tooget 토큰 tooyour 응용 프로그램 자체의 백 엔드 웹 API를 hello 요소로 표시 되는 것 hello 클라이언트와 같은 응용 프로그램 ID입니다. hello `offline_access` 앱 새로 고침 토큰 수명이 긴 액세스 tooresources에 대 한에서 필요한 범위를 나타냅니다. |
| redirect_uri |권장 |hello `redirect_uri` hello 인증 코드를 받는 hello 응용 프로그램의 매개 변수입니다. |
| refresh_token |필수 |hello 원래 새로 고침 토큰 hello hello 흐름의 두 번째 레그에서 복사한입니다. 참고 해야 사용 hello 범위 `offline_access` hello 권한 부여와 토큰 요청 순서 tooreceive에 새로 고침 토큰입니다. |
| client_secret |필수 |hello에 생성 된 hello 응용 프로그램 암호 [Azure 포털](https://portal.azure.com/)합니다. 이 응용 프로그램 암호는 중요한 보안 아티팩트입니다. 서버에 안전하게 저장해야 합니다. 또한 이 클라이언트 비밀도 정기적으로 회전해야 합니다. |

성공적인 토큰 응답은 다음과 같습니다.

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| 매개 변수 | 설명 |
| --- | --- |
| not_before |hello 시간은 hello에 토큰은 유효한 것으로 간주, epoch 시간에서입니다. |
| token_type |hello 토큰 유형 값입니다. Azure AD에서는 형식만 hello `Bearer`합니다. |
| access_token |hello 사용자가 요청한 JWT 토큰을 서명 합니다. |
| scope |토큰 hello hello 범위에 대해 올바른지, 나중에 사용할 토큰 캐싱 사용할 수 있는. |
| expires_in |액세스 토큰을 hello는 시간의 hello 길이 (초)에서 유효 합니다. |
| refresh_token |OAuth 2.0 새로 고침 토큰입니다. hello 앱 hello 현재 토큰 만료 된 후이 토큰 tooacquire 추가 토큰을 사용할 수 있습니다.  새로 고침 토큰 수명이 긴 되며 오랜 시간에 사용 되는 tooretain 액세스 tooresources를 사용할 수 있습니다. 자세한 정보를 얻기 위해 toohello 참조 [B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. |

오류 응답은 다음과 같습니다.

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 매개 변수 | 설명 |
| --- | --- |
| error |사용 되는 tooclassify 유형의 오류가 발생 하 고 사용 하는 tooreact tooerrors 일 수 있는 일 수 있는 오류 코드 문자열입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 개발자 데 도움이 되는 특정 오류 메시지입니다. |

## <a name="send-a-sign-out-request"></a>로그아웃 요청 보내기
Hello 앱 외 toosign hello 사용자를 원하는 때 부족 tooclear 응용 프로그램의 쿠키 또는 그렇지 않은 경우 hello 사용자와 hello 세션을 종료 됩니다. 또한 out hello 사용자 tooAzure AD toosign을 리디렉션해야 합니다. Toodo를 따라서 실패 한 경우 hello 사용자 수 tooreauthenticate tooyour 앱 자격 증명을 다시 입력 하지 않아도 될 수 있습니다. 이는 Azure AD를 사용하는 유효한 Single Sign-On 세션이 있기 때문입니다.

Hello 사용자 toohello 단순히 리디렉션할 수 있습니다 `end_session` "hello ID 토큰 유효성 검사" 섹션 hello 앞부분에 설명 된 hello OpenID Connect 메타 데이터 문서에 나열 된 끝점:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| p |필수 |hello 정책 응용 프로그램의 toouse toosign hello 사용자 한다는 것입니다. |
| post_logout_redirect_uri |권장 |hello URL hello 사용자 수 있어야 리디렉션된 tooafter 성공적으로 로그 아웃 합니다. Azure AD B2C 포함 되지 않은 일반 메시지 hello 사용자를 보여 줍니다. |

> [!NOTE]
> Hello 사용자 toohello 파일로 전송 되지만 `end_session` 끝점 일부 hello 사용자의 single sign on 상태와 Azure AD B2C 지워집니다, 소셜 id 공급자 (IDP) 세션 중 hello 사용자를 서명 하지 것입니다. Hello 사용자가을 선택 하는 경우 후속 로그인 하는 동안 동일한 IDP hello은 됩니다 다시 인증할 수, 자격 증명을 입력 하지 않고 있습니다. 사용자가 B2C 응용 프로그램의 toosign을 반드시 그렇다고 자신의 Facebook 계정을 toosign 원하는 합니다. 그러나 로컬 계정의 경우 hello hello 사용자 세션이 종료 됩니다 제대로 합니다.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>사용자 고유의 B2C 테넌트 사용
자신에 대 한 이러한 요청 tootry 경우 먼저이 세 단계를 수행 하 고 자신의 앞에서 설명한 hello 예제 값을 대체:

1. [B2C 테 넌 트 만들기](active-directory-b2c-get-started.md), 고 hello 요청에 테 넌 트의 hello 이름을 사용 합니다.
2. [응용 프로그램 만들기](active-directory-b2c-app-registration.md) tooobtain 응용 프로그램 ID 앱에 웹앱/웹 API를 포함합니다. 선택적으로 응용 프로그램 비밀을 만듭니다.
3. [정책 만들기](active-directory-b2c-reference-policies.md) tooobtain 정책 이름입니다.

