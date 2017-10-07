---
title: "인증 코드 흐름 - Azure AD B2C | Microsoft Docs"
description: "Toobuild Azure AD B2C 및 OpenID Connect 인증 프로토콜을 사용 하 여 앱을 웹 하는 방법에 대해 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: OAuth 2.0 인증 코드 흐름
장치 toogain tooprotected 같은 리소스에 액세스 웹 Api에 설치 된 앱의 hello OAuth 2.0 인증 코드 부여를 사용할 수 있습니다. OAuth 2.0의 Azure Active Directory B2C hello (Azure AD B2C) 구현을 사용 하 여 등록, 로그인을 추가할 수 있습니다 및 기타 id 관리 작업 tooyour 모바일 및 데스크톱 앱. 이 문서는 언어 독립적입니다. Hello 문서에서 설명 방법을 toosend 및 오픈 소스 라이브러리를 사용 하지 않고 HTTP 메시지를 수신 합니다.

<!-- TODO: Need link toolibraries -->

OAuth 2.0 인증 코드 흐름 hello에 설명 되어 [섹션 4.1 hello OAuth 2.0 사양의](http://tools.ietf.org/html/rfc6749)합니다. [웹앱](active-directory-b2c-apps.md#web-apps) 및 [기본적으로 설치된 앱](active-directory-b2c-apps.md#mobile-and-native-apps)을 포함하여 대부분의 앱 형식에서 인증 및 권한 부여에 사용할 수 있습니다. OAuth 2.0 권한 부여 코드 흐름 toosecurely 획득 hello를 사용할 수 있습니다 *액세스 토큰* 응용 프로그램에 의해 보안 되는 리소스를 사용 하는 tooaccess 될 수 있습니다는 [권한 부여 서버](active-directory-b2c-reference-protocols.md#the-basics)합니다.

이 문서에서는 hello **공용 클라이언트** OAuth 2.0 인증 코드 흐름. 공용 클라이언트는 신뢰할 수 있는 toosecurely 수 없는 모든 클라이언트 응용 프로그램 보안 암호의 hello 무결성을 유지 합니다. 모바일 앱, 데스크톱 앱 및 장치에서 실행 되 고 tooget 액세스 토큰을 요구 하는 응용 프로그램 기본적으로이 포함 됩니다. 

> [!NOTE]
> Azure AD B2C 사용을 사용 하 여 tooadd identity management tooa 웹 앱 [OpenID Connect](active-directory-b2c-reference-oidc.md) OAuth 2.0 대신 합니다.

Azure AD B2C toodo 단순 인증 및 권한 부여 보다 더 많은 hello 표준 OAuth 2.0 흐름을 확장 합니다. Hello 도입 [정책 매개 변수](active-directory-b2c-reference-policies.md)합니다. 기본 제공 정책을 사용 하 여 OAuth 2.0 tooadd 사용자와 같은 tooyour 앱 환경을 사용할 수 있습니다, 등록 및 프로필 관리에 로그인 합니다. 이 문서에서는 보여줍니다 어떻게 toouse OAuth 2.0 및 정책 tooimplement 네이티브 응용 프로그램에서 이러한 각 발생 합니다. 또한 보여줍니다 어떻게 tooget 액세스 토큰에 액세스 하기 위한 web Api.

Hello이 문서의 예제에서는 HTTP 요청을 사용 하 여이 샘플을 Azure AD B2C 디렉터리 **fabrikamb2c.onmicrosoft.com**합니다. 또한 응용 프로그램 예제 및 정책도 사용합니다. 이러한 값을 사용 하 여 사용자가 직접 hello 요청을 시도할 수 있습니다 또는 사용자 고유의 값으로 바꿀 수 있습니다.
너무 방법에 대해 알아봅니다[자신의 Azure AD B2C 디렉터리, 응용 프로그램 및 정책을 가져올](#use-your-own-azure-ad-b2c-directory)합니다.

## <a name="1-get-an-authorization-code"></a>1. 권한 부여 코드 가져오기
hello 클라이언트 hello 사용자 toohello 전달로 시작 하는 hello 권한 부여 코드 흐름 `/authorize` 끝점입니다. Hello 사용자가 작업 수행 hello 흐름의 hello 대화형 부분입니다. 이 요청에서 hello 클라이언트 hello에 나타냅니다 `scope` 필요 하다 고 tooacquire hello 사용자 로부터 매개 변수 hello 사용 권한. Hello에 `p` 매개 변수를 hello 정책 tooexecute 나타냅니다. hello 다음 세 가지 예 (읽기 쉽도록 줄 바꿈) 각 다른 정책을 사용 합니다.

### <a name="use-a-sign-in-policy"></a>로그인 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>등록 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>편집 프로필 정책 사용
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| client_id |필수 |hello에서 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 ID [Azure 포털](https://portal.azure.com)합니다. |
| response_type |필수 |포함 해야 하는 hello 응답 유형 `code` hello 권한 부여 코드 흐름에 대 한 합니다. |
| redirect_uri |필수 |hello 리디렉션 URI 앱 인증 응답 보내고 응용 프로그램에서 수신 위치입니다. 정확히 일치 해야 하나 hello 리디렉션 hello 포털에 등록 하는 Uri는 URL로 인코딩된 여야 합니다. |
| scope |필수 |공백으로 구분된 범위 목록입니다. 단일 범위 값에는 Active Directory (Azure AD) 모두 요청 되는 hello 권한의 tooAzure 나타냅니다. 같은 클라이언트 ID를 hello ID hello 범위 따르면 응용 프로그램 서비스 또는 웹 API에 대해 사용할 수 있는 액세스 토큰이 필요 함을 나타내는 hello 클라이언트를 사용 하 여  hello `offline_access` 범위 응용 프로그램 수명이 긴 액세스 tooresources에 대 한 새로 고침 토큰을 해야 함을 나타냅니다. Hello 사용할 수도 있습니다 `openid` 범위 toorequest Azure AD B2C에서 ID 토큰입니다. |
| response_mode |권장 |toosend hello 결과 권한 부여 코드 백 tooyour 앱을 사용 하는 hello 메서드. `query`, `form_post` 또는 `fragment`일 수 있습니다. |
| state |권장 |Hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 원하는 toouse 콘텐츠 문자열 수 있습니다. 임의로 생성 된 고유 값이 사용 하는 일반적으로 tooprevent 교차 사이트 요청 위조 공격입니다. hello도 상태가 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode hello 인증 요청이 발생 하기 전입니다. 예를 들어 hello 페이지 hello 사용자 설정 되어 있는 또는 실행 중 이었던 정책 hello 합니다. |
| p |필수 |실행 되는 hello 정책입니다. hello는 하는 정책의 이름을 Azure AD B2C 디렉터리에 만들어집니다. 정책 이름 값 hello로 시작 해야 **b2c\_1\_**합니다. 정책에 대해 자세히 toolearn 참조 [Azure AD B2C 기본 제공 정책](active-directory-b2c-reference-policies.md)합니다. |
| prompt |옵션 |필요한 사용자 상호 작용의 hello 형식입니다. Hello 유일한 유효 값은 현재 `login`이며 강제로 hello 사용자 tooenter 해당 요청에 자격 증명입니다. Single Sign-On은 적용되지 않습니다. |

이 시점에서 hello 사용자 toocomplete hello 정책 워크플로 요청. 그러면 hello 디렉터리 또는 단계의 다른 모든 숫자에 등록 한 소셜 id를 사용 하 여 로그인 hello 사용자 이름과 암호를 입력 만들어질 수 있습니다. 사용자 작업 hello 정책 정의 되는 방식에 따라 달라 집니다.

Azure AD에 사용한 hello 값에서 응답 tooyour 앱 반환 hello 사용자 hello 정책 완료 된 후 `redirect_uri`합니다. Hello에 지정 된 hello 방법을 사용 하 여 `response_mode` 매개 변수입니다. hello 응답은 각 hello 사용자 작업 시나리오를 독립적으로 실행 된 hello 정책에 대 한 동일한 hello 정확 하 게 합니다.

`response_mode=query`를 사용하는 성공적인 응답은 다음과 같습니다.

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| 매개 변수 | 설명 |
| --- | --- |
| 코드 |응용 프로그램 요청 hello는 hello 권한 부여 코드입니다. hello 앱 대상 리소스에 대 한 hello 권한 부여 코드 toorequest 액세스 토큰을 사용할 수 있습니다. 인증 코드는 수명이 매우 짧습니다. 일반적으로 약 10분 후에 만료됩니다. |
| state |Hello hello 섹션 앞의 hello 테이블에 전체 설명을 참조 하십시오. 경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다. |

오류 응답도 보낼 수 toohello 리디렉션 URI hello 응용 프로그램 수를 적절히 처리 되도록 합니다.

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| 매개 변수 | 설명 |
| --- | --- |
| error |Tooclassify hello 유형의 발생 하는 오류를 사용할 수는 오류 코드 문자열입니다. Hello 문자열 tooreact tooerrors를 사용할 수도 있습니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |
| state |Hello hello 앞에 테이블에에서 전체 설명을 참조 하십시오. 경우는 `state` hello 동일한 값이 표시 hello 응답 매개 변수 hello 요청에 포함 되어 있습니다. hello 응용 프로그램을 확인 해야 해당 hello `state` hello 요청 및 응답에는 값이 동일 합니다. |

## <a name="2-get-a-token"></a>2. 토큰 가져오기
Hello를 교환할 수 있습니다는 인증 코드를 구입한 했으므로 `code` 토큰 toohello POST 요청 toohello 전송 하 여 리소스 사용에 대 한 `/token` 끝점입니다. Azure AD B2C hello만 리소스에 대 한 토큰을 요청할 수 있는 응용 프로그램 자체의 백 엔드 web API입니다. 토큰 tooyourself를 요청 하는 데 사용 되는 hello 규칙은 toouse hello 범위와 앱의 클라이언트 ID입니다.

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| p |필수 |사용 하는 tooacquire hello 권한 부여 정책 hello 코드입니다. 이 요청에 다른 정책을 사용할 수 없습니다. 이 매개 변수 toohello를 추가할 *쿼리 문자열*, hello 게시물 본문에 없습니다. |
| client_id |필수 |hello에서 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 ID [Azure 포털](https://portal.azure.com)합니다. |
| grant_type |필수 |권한 부여의 hello 유형입니다. 권한 부여 코드 흐름 hello에 대 한 hello grant 유형 이어야 합니다 `authorization_code`합니다. |
| scope |권장 |공백으로 구분된 범위 목록입니다. 단일 범위 값이 요청 되는 hello 사용 권한 모두 AD tooAzure를 나타냅니다. 같은 클라이언트 ID를 hello ID hello 범위 따르면 응용 프로그램 서비스 또는 웹 API에 대해 사용할 수 있는 액세스 토큰이 필요 함을 나타내는 hello 클라이언트를 사용 하 여  hello `offline_access` 범위 응용 프로그램 수명이 긴 액세스 tooresources에 대 한 새로 고침 토큰을 해야 함을 나타냅니다.  Hello 사용할 수도 있습니다 `openid` 범위 toorequest Azure AD B2C에서 ID 토큰입니다. |
| 코드 |필수 |hello hello 흐름의 첫 번째 레그에서 복사한 hello 권한 부여 코드입니다. |
| redirect_uri |필수 |hello 리디렉션 URI는 hello 인증 코드를 수신 하는 hello 응용 프로그램입니다. |

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
| 매개 변수를 포함해야 합니다. | 설명 |
| --- | --- |
| not_before |hello 시간은 hello에 토큰은 유효한 것으로 간주, epoch 시간에서입니다. |
| token_type |hello 토큰 유형 값입니다. hello는만 Azure AD에서는 전달자를 입력 합니다. |
| access_token |hello는 JSON 웹 토큰 (JWT) 사용자가 요청한 서명 합니다. |
| scope |토큰 hello hello 범위에 대 한 유효 합니다. 나중에 사용할 toocache 토큰 범위를 사용할 수도 있습니다. |
| expires_in |토큰 hello는 시간의 hello 길이 (초)에서 유효 합니다. |
| refresh_token |OAuth 2.0 새로 고침 토큰입니다. hello 앱 hello 현재 토큰 만료 된 후이 토큰 tooacquire 추가 토큰을 사용할 수 있습니다. 새로 고침 토큰은 장기적으로 존재합니다. 사용할 수 있습니다 tooretain 액세스 tooresources 오랜 시간에 대 한 합니다. 자세한 내용은 참조 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. |

오류 응답은 다음과 같습니다.

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 매개 변수 | 설명 |
| --- | --- |
| error |Tooclassify hello 유형의 발생 하는 오류를 사용할 수는 오류 코드 문자열입니다. Hello 문자열 tooreact tooerrors를 사용할 수도 있습니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |

## <a name="3-use-hello-token"></a>3. Hello 토큰을 사용 하 여
Hello에 포함 하 여 hello 토큰을 사용할 요청 tooyour 백 엔드 웹 Api에에서 수 있는 액세스 토큰을 획득 성공적으로 했습니다 이제 `Authorization` 헤더:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Hello 토큰 새로 고침
액세스 토큰 및 ID 토큰은 수명이 짧습니다. 만료 되기 후 새로 고쳐야 하 toocontinue tooaccess 리소스. toodo이를 다른 POST 요청 toohello 제출 `/token` 끝점입니다. 이 시간 제공 hello `refresh_token` hello 대신 `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| p |필수 |사용 되는 tooacquire hello 원래 새로 고침 토큰을 hello 정책입니다. 이 요청에 다른 정책을 사용할 수 없습니다. 이 매개 변수 toohello를 추가할 *쿼리 문자열*, hello 게시물 본문에 없습니다. |
| client_id |권장 |hello에서 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 ID [Azure 포털](https://portal.azure.com)합니다. |
| grant_type |필수 |권한 부여의 hello 유형입니다. 이 다리 hello 권한 부여 코드 흐름의 hello grant 유형 이어야 합니다 `refresh_token`합니다. |
| scope |권장 |공백으로 구분된 범위 목록입니다. 단일 범위 값이 요청 되는 hello 사용 권한 모두 AD tooAzure를 나타냅니다. 같은 클라이언트 ID를 hello ID hello 범위 따르면 응용 프로그램 서비스 또는 웹 API에 대해 사용할 수 있는 액세스 토큰이 필요 함을 나타내는 hello 클라이언트를 사용 하 여  hello `offline_access` 앱 새로 고침 토큰 수명이 긴 액세스 tooresources에 대 한에서 필요한 범위를 나타냅니다.  Hello 사용할 수도 있습니다 `openid` 범위 toorequest Azure AD B2C에서 ID 토큰입니다. |
| redirect_uri |옵션 |hello 리디렉션 URI는 hello 인증 코드를 수신 하는 hello 응용 프로그램입니다. |
| refresh_token |필수 |hello 원래 새로 고침 토큰 hello hello 흐름의 두 번째 레그에서 복사한입니다. |

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
| 매개 변수를 포함해야 합니다. | 설명 |
| --- | --- |
| not_before |hello 시간은 hello에 토큰은 유효한 것으로 간주, epoch 시간에서입니다. |
| token_type |hello 토큰 유형 값입니다. hello는만 Azure AD에서는 전달자를 입력 합니다. |
| access_token |hello 사용자가 요청한 JWT를 서명 합니다. |
| scope |토큰 hello hello 범위에 대 한 유효 합니다. 나중에 사용할 hello 범위 toocache 토큰 사용할 수도 있습니다. |
| expires_in |토큰 hello는 시간의 hello 길이 (초)에서 유효 합니다. |
| refresh_token |OAuth 2.0 새로 고침 토큰입니다. hello 앱 hello 현재 토큰 만료 된 후이 토큰 tooacquire 추가 토큰을 사용할 수 있습니다. 새로 고침 토큰 수명이 긴 되며 오랜 시간에 사용 되는 tooretain 액세스 tooresources를 사용할 수 있습니다. 자세한 내용은 참조 hello [Azure AD B2C 토큰 참조](active-directory-b2c-reference-tokens.md)합니다. |

오류 응답은 다음과 같습니다.

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 매개 변수 | 설명 |
| --- | --- |
| error |발생 하는 오류의 tooclassify 종류를 사용할 수 있는 오류 코드 문자열입니다. Hello 문자열 tooreact tooerrors를 사용할 수도 있습니다. |
| error_description |수 있는 특정 오류 메시지를 인증 오류의 hello 근본 원인을 식별 합니다. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>사용자 고유의 Azure AD B2C 디렉터리 사용
이러한 요청을 직접 수행 하는 전체 hello tootry 안내 합니다. 고유한 값으로이 문서에서 사용 하는 hello 예제 값을 대체 합니다.

1. [Azure AD B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md). 디렉터리의 이름을 hello를 사용 하 여 hello 요청에서.
2. [응용 프로그램 만들기](active-directory-b2c-app-registration.md) tooobtain 응용 프로그램 ID 및 리디렉션 URI입니다. 앱에 네이티브 클라이언트를 포함합니다.
3. [정책 만들기](active-directory-b2c-reference-policies.md) tooobtain 정책 이름입니다.

