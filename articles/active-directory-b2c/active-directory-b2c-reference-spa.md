---
title: "Azure Active Directory B2C: 암시적 흐름을 사용하는 단일 페이지 앱 | Microsoft Docs"
description: "Toobuild 단일 페이지 앱 직접 암시적 OAuth 2.0을 사용 하 여 흐름 방식으로 Azure Active Directory B2C에 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C: OAuth 2.0 암시적 흐름을 사용하여 단일 페이지 앱 로그인

> [!NOTE]
> 이 기능은 미리 보기로 제공됩니다.
> 

대부분의 최신 앱에는 주로 Javascript로 작성되고 AngularJS, Ember.js, Durandal 등과 같은 프레임워크로도 작성되는 종종 hello 앱은 AngularJS, Ember.js, 또는 Durandal와 같은 프레임 워크를 사용 하 여 기록 됩니다. 주로 브라우저에서 실행되는 단일 페이지 앱 및 기타 JavaScript 앱에는 인증에 대한 몇 가지 추가 과제가 있습니다.

* 이러한 앱의 hello 보안 특성은 일반적인 서버 기반 웹 응용 프로그램 크게 다릅니다.
* 많은 권한 부여 서버 및 ID 공급자에서 CORS(원본 간 리소스 공유) 요청을 지원하지 않습니다.
* Hello 응용 프로그램에서 전체 페이지 브라우저 이동 크게 침투 적 toohello 사용자 경험을 수 있습니다.

toosupport 이러한 응용 프로그램을 Azure Active Directory B2C (Azure AD B2C) hello OAuth 2.0 암시적 흐름을 사용 합니다. hello OAuth 2.0 인증 암시적 부여 흐름에 설명 되어 [4.2 hello OAuth 2.0 사양의 섹션](http://tools.ietf.org/html/rfc6749)합니다. 암시적 흐름에서 hello 앱에서 hello에서 직접 토큰을 수신 Azure Active Directory (Azure AD)에 모든 서버 간 교환 하지 않고 끝점 권한을 부여 합니다. 모든 인증 논리 및 세션 처리는 전적으로 추가 하는 페이지 리디렉션도 없이 hello JavaScript 클라이언트에서 수행 됩니다.

Azure AD B2C hello 표준 OAuth 2.0 암시적 흐름 toomore 단순 인증 및 권한 부여 보다를 확장합니다. Azure AD B2C 소개 hello [정책 매개 변수](active-directory-b2c-reference-policies.md)합니다. Hello 정책 매개 변수와 함께 OAuth 2.0 tooadd 사용자와 같은 tooyour 앱 환경을 사용할 수 있습니다, 등록 및 프로필 관리에 로그인 합니다. 이 문서에서는 보여줍니다 toouse 암시적 흐름 및 Azure AD tooimplement 각 단일 페이지 응용 프로그램에서 이러한 환경의 hello 하는 방법. 시작 하려면 toohelp 살펴보세요 우리의 [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) 및 [MICROSOFT.NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) 샘플.

Hello이 문서의 예제에서는 HTTP 요청을 사용 하 여이 샘플을 Azure AD B2C 디렉터리 **fabrikamb2c.onmicrosoft.com**합니다. 또한 고유한 샘플 응용 프로그램 및 정책도 사용합니다. 이러한 값을 사용 하 여 사용자가 직접 hello 요청을 시도할 수 있습니다 또는 사용자 고유의 값으로 바꿀 수 있습니다.
너무 방법에 대해 알아봅니다[자신의 Azure AD B2C 디렉터리, 응용 프로그램 및 정책을 가져올](#use-your-own-b2c-tenant)합니다.


## <a name="protocol-diagram"></a>프로토콜 다이어그램

hello 암시적 로그인 흐름은 다음 그림 hello 합니다. 각 단계는 hello 문서의 뒷부분에 자세히 설명 되어 있습니다.

![OpenID Connect 스윔 레인](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>인증 요청 보내기
Hello 사용자 toohello tooauthenticate hello 사용자 필요 하 고 정책을 실행 하는 웹 앱을 직접 보냅니다 `/authorize` 끝점입니다. Hello 사용자 이루어지는 hello 정책에 따라 hello 흐름의 hello 대화형 부분입니다. hello 사용자 hello Azure AD 끝점에서 토큰 ID를 가져옵니다.

이 요청에서 hello 클라이언트 hello에 나타냅니다 `scope` 필요 하다 고 tooacquire hello 사용자 로부터 매개 변수 hello 사용 권한. Hello에 `p` 매개 변수를 hello 정책 tooexecute 나타냅니다. hello 다음 세 가지 예 (읽기 쉽도록 줄 바꿈) 각 다른 정책을 사용 합니다. 각 요청 작동 방식에 대 한 느낌 tooget 브라우저와 실행에 붙여넣기 hello 요청을 시도 하십시오.

### <a name="use-a-sign-in-policy"></a>로그인 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>등록 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>편집 프로필 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| client_id |필수 |hello에서 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 ID [Azure 포털](https://portal.azure.com)합니다. |
| response_type |필수 |OpenID Connect 로그인을 위한 `id_token` 이 포함되어야 합니다. Hello 응답 유형을 포함할 수 `token`합니다. 사용 하는 경우 `token`, 앱 hello에서 즉시 액세스 토큰을 받을 수 권한 부여 끝점 두 번째 요청 toohello 하지 않고 끝점에 권한을 부여 합니다.  Hello를 사용 하는 경우 `token` 응답 유형, hello `scope` 매개 변수는 리소스 tooissue hello에 대 한 토큰을 나타내는 범위를 포함 해야 합니다. |
| redirect_uri |권장 |hello 리디렉션 URI 인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램입니다. 정확히 일치 해야 하나 hello 리디렉션 hello 포털에 등록 하는 Uri는 URL로 인코딩된 여야 합니다. |
| response_mode |권장 |Hello 메서드 toouse toosend hello 결과 토큰 백 tooyour 앱을 지정합니다.  암시적 흐름의 경우 `fragment`를 사용합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다. 단일 범위 값이 요청 되는 hello 사용 권한 모두 AD tooAzure를 나타냅니다. hello `openid` 범위 ID 토큰의 hello 형태로 hello 사용자에 대 한 사용자 및 get 데이터 hello 권한 toosign을 나타냅니다. (알아보겠습니다이 대 한 hello 문서의 뒷부분에 보다.) hello `offline_access` 범위는 웹 앱에 대 한 선택 사항입니다. 수명이 긴 액세스 tooresources에 대 한 응용 프로그램 새로 고침 토큰이 필요 함을 나타냅니다. |
| state |권장 |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 원하는 toouse 콘텐츠 문자열 수 있습니다. 임의로 생성 되 고 고유 값이 사용 하는 일반적으로 tooprevent 교차 사이트 요청 위조 공격입니다. hello를 사용 하는 tooencode 정보 hello 앱에서 hello 사용자의 상태에 대 한 hello 인증 요청이 발생 하기 전에 hello 페이지 처럼에 있는 것입니다. |
| nonce |필수 |클레임으로 hello 결과 ID 토큰에 포함 된 hello 요청 (hello 앱에서 생성)에 포함 하는 값입니다. hello 앱이 값 toomitigate 토큰 재생 공격 확인할 수 있습니다. 일반적으로 hello 값은 임의 고유 문자열을 사용 사용된 tooidentify hello 원점 hello 요청의 수입니다. |
| p |필수 |hello 정책 tooexecute 합니다. hello는 하는 정책의 이름을 Azure AD B2C 테 넌 트에 만들어집니다. 정책 이름 값 hello로 시작 해야 **b2c\_1\_**합니다. 자세한 내용은 [Azure AD B2C 기본 제공 정책](active-directory-b2c-reference-policies.md)을 참조하세요. |
| prompt |옵션 |hello 유형의 있으면 사용자 상호 작용 합니다. 현재 hello만 유효한 값은 `login`합니다. 이렇게 하면 hello 사용자 tooenter 자격 증명에이 요청 됩니다. Single Sign-On은 적용되지 않습니다. |

이 시점에서 hello 사용자 toocomplete hello 정책 워크플로 요청. 그러면 hello 디렉터리 또는 단계의 다른 모든 숫자에 등록 한 소셜 id를 사용 하 여 로그인 hello 사용자 이름과 암호를 입력 만들어질 수 있습니다. 사용자 작업 hello 정책 정의 되는 방식에 따라 달라 집니다.

Azure AD에 사용한 hello 값에서 응답 tooyour 앱 반환 hello 사용자 hello 정책 완료 된 후 `redirect_uri`합니다. Hello에 지정 된 hello 방법을 사용 하 여 `response_mode` 매개 변수입니다. hello 응답은 각 hello 사용자 작업 시나리오를 독립적으로 실행 된 hello 정책에 대 한 동일한 hello 정확 하 게 합니다.

### <a name="successful-response"></a>성공적인 응답
사용 하는 성공적인 응답 `response_mode=fragment` 및 `response_type=id_token+token` 쉽게 읽을 수 있도록 줄 바꿈 hello 다음과 같습니다.

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| 매개 변수 | 설명 |
| --- | --- |
| access_token |응용 프로그램 요청 hello hello 액세스 토큰입니다.  hello 액세스 토큰을 디코딩할 수 하거나 기타 방식으로 검사 해야 합니다. 불투명 문자열로 처리할 수 있습니다. |
| token_type |hello 토큰 유형 값입니다. hello는만 Azure AD에서는 전달자를 입력 합니다. |
| expires_in |액세스 토큰을 hello는 시간의 hello 길이 (초)에서 유효 합니다. |
| scope |토큰 hello hello 범위에 대 한 유효 합니다. 나중에 사용할 toocache 토큰 범위를 사용할 수도 있습니다. |
| id_token |ID 토큰을 요청 하는 응용 프로그램 hello hello 합니다. Hello ID 토큰 tooverify hello 사용자 id를 사용 하 여 수 있으며 hello 사용자와 세션을 시작할 수 있습니다. ID 토큰 및 해당 내용에 대 한 자세한 내용은 참조 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. |
| state |경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다. |

### <a name="error-response"></a>오류 응답
오류 응답도 보낼 수 toohello 리디렉션 URI hello 응용 프로그램 수를 적절히 처리 되도록 합니다.

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| 매개 변수 | 설명 |
| --- | --- |
| error |오류 코드 문자열을 사용 하는 tooclassify 형식의 발생 하는 오류입니다. 오류 처리에 대 한 hello 오류 코드를 사용할 수도 있습니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |
| state |Hello hello 앞에 테이블에에서 전체 설명을 참조 하십시오. 경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다.|

## <a name="validate-hello-id-token"></a>Hello ID 토큰 유효성 검사
ID 토큰을 받는 충분 한 tooauthenticate hello 사용자가 아닙니다. Hello ID 토큰 서명의 유효성을 검사 하 고 응용 프로그램의 요구 사항에 따라 hello 토큰의 hello 클레임을 확인 해야 합니다. 사용 하 여 azure AD B2C [JSON 웹 토큰 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) 및 공개 키 암호화 toosign 토큰 및 유효한 지 확인 합니다.

여러 오픈 소스 라이브러리를 Jwt의 유효성 검사에 사용할 수, toouse hello 언어에 따라 선호 합니다. 사용자 고유의 유효성 검사 논리를 구현하는 대신 사용 가능한 오픈 소스 라이브러리를 탐색하는 것이 좋습니다. Hello 정보를 사용 하려면이 문서 toohelp 배웁니다 tooproperly 해당 라이브러리를 사용 하는 방법입니다.

Azure AD B2C에는 OpenID Connect 메타데이터 끝점이 있습니다. 앱에서 런타임에 Azure AD B2C에 대 한 hello 끝점 toofetch 정보를 사용할 수 있습니다. 이 정보에는 끝점, 토큰 콘텐츠 및 토큰 서명 키가 포함됩니다. Azure AD B2C 테넌트의 각 정책에 대한 JSON 메타데이터 문서가 있습니다. 예를 들어 hello fabrikamb2c.onmicrosoft.com 테 넌 트의 hello b2c_1_sign_in 정책에 대 한 hello 메타 데이터 문서는에 있습니다.

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

이 구성 문서의 hello 속성 중 하나는 hello `jwks_uri`합니다. 동일한 정책 것 hello에 대 한 hello 값:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

정책에서 사용 되는 toosign ID 토큰 (및 여기서 toofetch hello에서 메타 데이터) toodetermine 두 가지 옵션이 있습니다. 첫째, hello 정책 이름을 ´ â hello `acr` 의 `id_token`합니다. Tooparse hello ID 토큰에서 요구 하는 방법에 대 한 내용은 hello 참조 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. 다른 옵션은 hello hello 값에서 tooencode hello 정책 `state` hello 요청을 실행할 때 매개 변수입니다. 그런 다음 hello를 디코딩할 `state` 매개 변수 toodetermine 정책 사용 되었습니다. 두 방법 중 하나는 유효합니다.

Hello OpenID Connect 메타 데이터 끝점에서 메타 데이터 문서 hello를 구입한 후 hello ID 토큰의 hello 256 RSA 공개 키 (이 끝점에 있는) toovalidate hello 서명에 사용할 수 있습니다. 지정된 시간에 이 끝점에 나열된 키가 여러 개 있을 수 있으며, 각 키는 `kid`로 식별됩니다. hello 헤더 `id_token` 도 포함 되어는 `kid` 클레임입니다. 이러한 키 중 어떤가 사용 되는 toosign hello ID 토큰을 나타냅니다. 에 대 한 학습을 포함 하는 자세한 내용은 [토큰 유효성 검사](active-directory-b2c-reference-tokens.md#token-validation), hello 참조 [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.
<!--TODO: Improve hello information on this-->

Hello hello ID 토큰 서명의 유효성을 검사 하면 여러 클레임 확인을 요청 합니다. 예:

* Hello 유효성을 검사 `nonce` tooprevent 토큰 재생 공격을 주장 합니다. Hello 로그인 요청에 지정 된 해당 값 이어야 합니다.
* Hello 유효성을 검사 `aud` 클레임 ID 토큰 hello tooensure 응용 프로그램에 대해 실행 되었습니다. 해당 값에는 응용 프로그램의 응용 프로그램 ID hello 이어야 합니다.
* Hello 유효성을 검사 `iat` 및 `exp` 클레임 ID 토큰 hello tooensure가 만료 되지 않았습니다.

수행 해야 하는 몇 가지 더 많은 유효성 검사 hello에 자세히 설명 되어 [OpenID 연결 핵심 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다. 시나리오에 따라 toovalidate 추가 클레임을 할 수 있습니다. 몇 가지 일반적인 유효성 검사는 다음과 같습니다.

* 확인 hello 사용자나 조직에 등록 하 여 hello 앱에 대 한 합니다.
* 해당 hello 사용자에 게 적절 한 권한 부여 및 사용 권한 확인 합니다.
* Azure Multi-Factor Authentication을 사용하는 것과 같이 특정 강도의 인증이 발생했는지 확인합니다.

ID 토큰의 클레임을 hello에 대 한 자세한 내용은 참조 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다.

ID 토큰 hello를 완전히 확인 한 후에 hello 사용자와 세션을 시작할 수 있습니다. 응용 프로그램에서 hello 사용자에 대 한 hello ID 토큰 tooobtain 정보 hello 클레임을 사용 합니다. 이 정보는 표시, 레코드, 권한 부여 등에 사용될 수 있습니다.

## <a name="get-access-tokens"></a>액세스 토큰 가져오기
Hello 하는지만 웹 응용 프로그램 요구 toodo 프로그램은 정책 실행을 건너뛸 수 있습니다 다음 몇 개 섹션 hello 합니다. hello 정보 hello 다음 섹션에에서는 적용 가능한 tooweb 앱만 필요로 하는 인증 toomake 호출 tooa 웹 API 및 Azure AD B2C로 보호 되는 합니다.

Hello 사용자 tooyour 단일 페이지 응용 프로그램에서 로그를 Azure AD를 통해 보안이 유지 되는 Api 호출 웹에 대 한 액세스 토큰을 얻을 수 있습니다. Hello를 사용 하 여 토큰을 이미 받은 경우에 `token` 응답 유형 없이 사용할 수 있습니다이 메서드 tooacquire 토큰 추가 리소스에 대 한 hello 사용자 toosign에서 다시 리디렉션합니다.

일반적인 웹 앱 흐름에서 설정 하려는 요청 toohello 함으로써 `/token` 끝점입니다.  하지만 hello 끝점 tooget 호출 AJAX 하 고 새로 고침 토큰 옵션이 아닙니다. 지원 CORS 요청 하지 않습니다. 대신, 다른 웹 Api에 대 한 한 숨겨진된 HTML iframe 요소 tooget 새 토큰의 hello 암시적 흐름을 사용할 수 있습니다. 다음은 쉽게 읽을 수 있도록 줄 바꿈을 적용한 예제입니다.

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| client_id |필수 |hello에서 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 ID [Azure 포털](https://portal.azure.com)합니다. |
| response_type |필수 |OpenID Connect 로그인을 위한 `id_token` 이 포함되어야 합니다.  Hello 응답 유형이 포함 될 수 있습니다 `token`합니다. 사용 하는 경우 `token` 여기에서 앱 즉시에서 받을 수는 액세스 토큰 hello 권한 부여 끝점 두 번째 요청 toohello 하지 않고 끝점에 권한을 부여 합니다. Hello를 사용 하는 경우 `token` 응답 유형, hello `scope` 매개 변수는 리소스 tooissue hello에 대 한 토큰을 나타내는 범위를 포함 해야 합니다. |
| redirect_uri |권장 |hello 리디렉션 URI 인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램입니다. 정확히 일치 해야 하나 hello 리디렉션 hello 포털에 등록 된 Uri는 URL로 인코딩된 여야 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다.  토큰을 가져오기 위한 hello 의도 한 리소스에 대 한 필요한 모든 범위를 포함 합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 토큰 백 tooyour 앱 hello 방법을 지정 합니다.  `query`, `form_post` 또는 `fragment`일 수 있습니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다.  원하는 toouse 콘텐츠 문자열 수 있습니다.  임의로 생성 되 고 고유 값이 사용 하는 일반적으로 tooprevent 교차 사이트 요청 위조 공격입니다.  hello도 상태가 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode hello 인증 요청이 발생 하기 전입니다. 예를 들어 hello 페이지 또는 보기 hello 사용자가 있습니다. |
| nonce |필수 |클레임으로 hello 결과 ID 토큰에 포함 된 hello 앱에서 생성 하는 hello 요청에 포함 하는 값입니다.  hello 앱이 값 toomitigate 토큰 재생 공격 확인할 수 있습니다. 일반적으로 hello 기간은 hello 요청의 hello 출처를 식별 하는 임의 고유 문자열입니다. |
| prompt |필수 |toorefresh 및 get 토큰에 숨겨진된 iframe 사용 하 여 `prompt=none` iframe hello tooensure hello 로그인 페이지 중단 되지 않는 한 다음 즉시 반환 합니다. |
| login_hint |필수 |toorefresh 및 get 토큰 숨겨진된 iframe에 지정된 된 시간에 hello, 사용자가 여러 세션 간에이 힌트 toodistinguish에 hello 사용자의 hello 사용자를 포함 합니다. Hello를 사용 하 여 hello username는 이전 로그인에서 추출할 수 있습니다 `preferred_username` 클레임입니다. |
| domain_hint |필수 |`consumers` 또는 `organizations`일 수 있습니다.  새로 고침 및 숨겨진된 iframe의 토큰을 가져오기, 포함 해야 hello `domain_hint` hello 요청의 값입니다.  Hello 추출 `tid` 어떤 값 toouse는 이전 로그인 toodetermine의 hello ID 토큰에서 클레임입니다.  경우 hello `tid` 값은 클레임 `9188040d-6c67-4c5b-b112-36a304b66dad`를 사용 하 여 `domain_hint=consumers`합니다.  그렇지 않으면 `domain_hint=organizations`를 사용합니다. |

Hello 설정 하 여 `prompt=none` 매개 변수를이 요청 중 하나에 성공 또는 실패를 즉시 하 고 tooyour 응용 프로그램을 반환 합니다.  성공적인 응답 tooyour 앱 보내집니다 hello에 지정 된 hello 메서드를 사용 하 여 리디렉션 URI를 표시 하는 hello에 `response_mode` 매개 변수입니다.

### <a name="successful-response"></a>성공적인 응답
`response_mode=fragment`를 사용한 성공적인 응답은 다음과 같습니다.

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| 매개 변수 | 설명 |
| --- | --- |
| access_token |응용 프로그램 요청 hello는 hello 토큰입니다. |
| token_type |토큰 유형이 hello 항상 전달자 됩니다. |
| state |경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다. |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |
| scope |액세스 토큰을 hello hello 범위에 대 한 유효 합니다. |

### <a name="error-response"></a>오류 응답
오류 응답도 수 전송 toohello 리디렉션 URI hello 응용 프로그램 수를 적절히 처리 되도록.  `prompt=none`의 경우 예상되는 오류는 다음과 같습니다.

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| 매개 변수 | 설명 |
| --- | --- |
| error |사용 되는 tooclassify 유형의 오류가 발생 하는 일 수 있는 오류 코드 문자열입니다. Hello 문자열 tooreact tooerrors를 사용할 수도 있습니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |

Hello iframe 요청에이 오류가 나타나면 hello 사용자 대화형으로 로그인 해야 다시 tooretrieve 새 토큰을 합니다. 응용 프로그램에 적합한 방식으로 이 작업을 처리할 수 있습니다.

## <a name="refresh-tokens"></a>새로 고침 토큰
ID 토큰 및 액세스 토큰은 모두 짧은 기간 후에 만료됩니다. 응용 프로그램은 이러한 토큰을 주기적으로 toorefresh를 준비 되어야 합니다.  toorefresh 토큰 유형 중 하나를 수행 hello를 사용 하 여 이전 예제에서 사용한 동일한 숨겨진된 iframe 요청 hello `prompt=none` toocontrol Azure AD 단계 매개 변수입니다.  새 tooreceive `id_token` 있는지 toouse 수, 값 `response_type=id_token` 및 `scope=openid`, 및 `nonce` 매개 변수입니다.

## <a name="send-a-sign-out-request"></a>로그아웃 요청 보내기
Hello 앱 중 toosign hello 사용자 하려는 경우 아웃 hello 사용자 tooAzure AD toosign을 리디렉션하십시오. 이렇게 하지 않으면 hello 사용자 자격 증명을 다시 입력 하지 않아도 수 tooreauthenticate tooyour 앱 수 있습니다. 이는 Azure AD를 사용하는 유효한 Single Sign-On 세션이 있기 때문입니다.

Hello 사용자 toohello 단순히 리디렉션할 수 있습니다 `end_session_endpoint` 에 설명 된 동일한 OpenID Connect 메타 데이터 문서에 나열 된 hello 즉 [hello ID 토큰 유효성 검사](#validate-the-id-token)합니다. 예:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| p |필수 |hello 정책 toouse toosign hello 사용자 응용 프로그램의입니다. |
| post_logout_redirect_uri |권장 |hello URL hello 사용자 수 있어야 리디렉션된 tooafter 성공적으로 로그 아웃 합니다. 포함 되지 않은 경우 Azure AD B2C 일반 메시지 toohello 사용자를 표시 합니다. |

> [!NOTE]
> Hello 사용자 toohello 전달 `end_session_endpoint` hello 사용자의 single sign on 상태와 Azure AD B2C 중 일부를 지웁니다. 그러나 hello 사용자 hello 사용자의 소셜 id 공급자 세션 중에 서명 하지 않습니다 것입니다. Hello 사용자가 hello를 선택 하는 경우 후속 로그인 하는 동안 공급자를 식별 동일, 자격 증명을 입력 하지 않고, hello 사용자 다시 인증 합니다. 사용자가 Azure AD B2C 응용 프로그램의 toosign을 반드시 그렇다고 예를 들어 자신의 Facebook 계정을 toocompletely 기호 원하는 합니다. 그러나 로컬 계정에 대 한 hello 사용자 세션이 종료 됩니다 제대로 합니다.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>사용자 고유의 Azure AD B2C 테넌트 사용
이러한 요청을 직접 완료 tootry hello 세 단계를 수행 합니다. 고유한 값으로이 문서에서 사용 하 여 hello 예제 값을 바꿉니다.

1. [Azure AD B2C 테넌트를 만듭니다](active-directory-b2c-get-started.md). Hello 요청에서 테 넌 트 이름 hello를 사용 합니다.
2. [응용 프로그램 만들기](active-directory-b2c-app-registration.md) tooobtain 응용 프로그램 ID와 `redirect_uri` 값입니다. 앱에 웹앱 또는 Web API를 포함합니다. 필요에 따라 응용 프로그램 비밀을 만들 수 있습니다.
3. [정책 만들기](active-directory-b2c-reference-policies.md) tooobtain 정책 이름입니다.

## <a name="samples"></a>샘플

* [Node.js를 사용하여 단일 페이지 앱 만들기](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)(영문)
* [.NET을 사용하여 단일 페이지 앱 만들기](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)(영문)

