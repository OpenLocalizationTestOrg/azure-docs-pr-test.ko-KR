---
title: "Azure Active Directory B2C: 토큰 참조 | Microsoft Docs"
description: "hello 유형의 Azure Active Directory B2C에 발급 된 토큰"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C: 토큰 참조
Azure AD B2C(Azure Active Directory B2C)는 각 [인증 흐름](active-directory-b2c-apps.md)을 처리할 때 여러 형식의 보안 토큰을 내보냅니다. 이 문서에서는 hello 형식, 보안 특성 및 각 유형의 토큰의 내용을 설명 합니다.

## <a name="types-of-tokens"></a>토큰 형식
Azure AD B2C 지원 hello [OAuth 2.0 권한 부여 프로토콜](active-directory-b2c-reference-protocols.md)를 사용 하는 둘 다의 액세스 토큰 및 새로 고침 토큰입니다. 또한 인증 및 로그인을 통해 지원 [OpenID Connect](active-directory-b2c-reference-protocols.md), 세 번째 토큰 유형의 도입: hello ID 토큰입니다. 이러한 토큰은 각각 전달자 토큰으로 표시됩니다.

전달자 토큰은 보호 된 리소스를 부여 "전달자" 액세스 tooa hello 하는 경량 보안 토큰입니다. hello 전달자 hello 토큰을 제공할 수 있는 당사자입니다. Azure AD에서 전달자 토큰을 받으려면 먼저 당사자를 인증해야 합니다. 하지만 hello 필요한 단계는 전송 및 저장에서 toosecure hello 토큰을 따르지 않은 경우 차단 하 고 수 있습니다는 의도 하지 않은 당사자에서 사용 하는. 일부 보안 토큰에는 권한이 없는 당사자가 토큰을 사용하는 것을 막는 메커니즘이 기본으로 제공되지만 전달자 토큰에는 이 메커니즘이 없습니다. 전송 계층 보안(HTTPS) 등의 보안 채널에서 전송해야 합니다.

전달자 토큰에 보안 채널 외부 전송 경우 악의적인 사용자 중간자 개입 공격 tooacquire hello 토큰을 사용할 수 있으며 toogain 무단 액세스 tooa 보호 된 리소스를 사용 합니다. hello 전달자 토큰을 저장 하거나 나중에 캐시 하는 경우 동일한 보안 원칙이 적용 됩니다. 항상 앱이 안전한 방식으로 전달자 토큰을 전송하고 저장하도록 합니다.

전달자 토큰의 보안 고려 사항을 자세히 알아보려면 [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750)를 참조하세요.

다양 한 Azure AD B2C 발급 하는 hello 토큰 JSON 웹 토큰 (Jwt)로 구현 됩니다. JWT는 두 요소 간에 정보를 전송하는 URL로부터 안전한 간단한 수단입니다. JWT는 클레임이라고 하는 정보를 포함합니다. 이들은 hello 전달자에 대 한 정보 어설션 및 hello 토큰의 주체 hello입니다. Jwt의 hello 클레임은 인코딩된 및 전송을 위해 serialize 되는 JSON 개체입니다. JWT toodebug hello 내용을 검사 하 고 쉽게 수 hello Azure AD B2C에서 발급 한 Jwt 서명 아니라 암호화 되지 때문에 해당 합니다. 이 작업을 수행하는 데 [calebb.net](http://calebb.net)을 포함하여 여러 도구를 사용할 수 있습니다. Jwt에 대 한 자세한 내용은 참조 너무[JWT 사양](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)합니다.

### <a name="id-tokens"></a>ID 토큰
ID 토큰은 앱이 Azure AD B2C hello에서 수신 하는 보안 토큰의 형태 `authorize` 및 `token` 끝점입니다. ID 토큰으로 표시 됩니다 [Jwt](#types-of-tokens), 하며 tooidentify 사용자가 앱에서 사용할 수 있는 클레임을 포함 합니다. Hello에서 ID 토큰 획득 때 `authorize` 끝점이 되어 있어 사용자가 tooweb 응용 프로그램에서 사용 되는 toosign 합니다. Hello에서 ID 토큰 획득 때 `token` 끝점을 보낼 수 있습니다 HTTP 요청 시에서 hello의 두 구성 요소 간 통신 중 동일한 응용 프로그램 또는 서비스입니다. 원하는 대로 hello 클레임 ID 토큰에서 사용할 수 있습니다. 자주 사용 되는 toodisplay 계정 정보 또는 toomake 액세스 제어 결정에 서 응용 프로그램에서 됩니다.  

ID 토큰은 서명되어 있지만, 현재 암호화되지 않습니다. 응용 프로그램 또는 API ID 토큰을 받으면 다음 조건을 충족 해야 [hello 서명 유효성 검사](#token-validation) 토큰 hello tooprove은 진짜 콘텐츠입니다. 응용 프로그램 또는 API 해야 hello 토큰 tooprove 올바른지의 몇 가지 클레임을 확인할 수도 있습니다. Hello 시나리오 요구 사항에 따라 응용 프로그램에서 유효성을 검사 하는 hello 클레임 바뀔 수 있지만, 응용 프로그램 일부를 수행 해야 [일반 클레임 유효성 검사](#token-validation) 모든 시나리오에서.

#### <a name="sample-id-token"></a>샘플 ID 토큰
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>액세스 토큰
액세스 토큰이 앱이 Azure AD B2C hello에서 수신 하는 보안 토큰의 형태 이기도 `authorize` 및 `token` 끝점입니다. 액세스 토큰으로도 표현 됩니다 [Jwt](#types-of-tokens), 하며 tooidentify hello 부여 권한을 tooyour Api를 사용할 수 있는 클레임을 포함 합니다. 액세스 토큰은 서명되어 있지만, 현재 암호화되지 않습니다. 액세스 토큰에 사용 되는 tooprovide 액세스 tooAPIs 및 리소스 서버 여야 합니다. 너무 방법에 대 한 자세한[액세스 토큰을 사용 하 여](active-directory-b2c-access-tokens.md)합니다. 

API 액세스 토큰을 받으면 다음 조건을 충족 해야 [hello 서명 유효성 검사](#token-validation) 토큰 hello tooprove은 진짜 콘텐츠입니다. 사용자가 API는 hello 토큰 tooprove 올바른지의 몇 가지 클레임을 확인도 해야 합니다. Hello 시나리오 요구 사항에 따라 응용 프로그램에서 유효성을 검사 하는 hello 클레임 바뀔 수 있지만, 응용 프로그램 일부를 수행 해야 [일반 클레임 유효성 검사](#token-validation) 모든 시나리오에서.

### <a name="claims-in-id-and-access-tokens"></a>ID 및 액세스 토큰의 클레임
Azure AD B2C를 사용 하면 사용자가 토큰의 hello 콘텐츠에 대 한 세분화 된 제어를 해야 합니다. 구성할 수 있습니다 [정책](active-directory-b2c-reference-policies.md) toosend 특정 앱에 필요한 작업에 대 한 클레임의 사용자 데이터의 집합입니다. 이러한 클레임 hello 사용자와 같은 표준 속성을 포함할 수 있습니다 `displayName` 및 `emailAddress`합니다. 또한 B2C 디렉터리에서 정의할 수 있는 [사용자 지정 특성](active-directory-b2c-reference-custom-attr.md) 도 포함할 수 있습니다. 받는 모든 ID 및 액세스 토큰에는 보안 관련 클레임의 특정 집합이 포함되어 있습니다. 응용 프로그램 toosecurely 사용자 및 요청을 인증 하 이러한 클레임을 사용할 수 있습니다.

특정 순서로 hello 토큰의에서 클레임 ID 가져오지는 참고 사항 또한 언제든지 새 클레임을 ID 토큰에 도입할 수 있습니다. 새 클레임이 도입되므로 앱을 해제하지 말아야 합니다. Hello 클레임 tooexist Azure AD B2C에서 발급 한 ID 및 액세스 토큰에서 예상 되는 다음과 같습니다. 모든 추가 클레임은 정책에 따라 결정됩니다. 연습에 붙여 넣어 여 hello 샘플 ID 토큰의 클레임이 hello 검사를 시도 [calebb.net](http://calebb.net)합니다. Hello에 자세한 정보를 찾을 수 [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다.

| 이름 | 클레임 | 예제 값 | 설명 |
| --- | --- | --- | --- |
| 대상 |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |대상 그룹 클레임 hello 토큰의 hello 의도 한 받는 사람을 식별합니다. Azure AD B2C에 대 한 hello 대상 그룹은 hello 응용 프로그램 등록 포털에 할당 된 tooyour 응용 프로그램으로 응용 프로그램의 응용 프로그램 ID입니다. 앱이이 값의 유효성을 검사 하 고 일치 하지 않으면 hello 토큰을 거부 해야 합니다. |
| 발급자 |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |이 클레임 식별 hello 보안 토큰 서비스 (STS)를 생성 하 고 hello 토큰을 반환 합니다. 또한 사용자가 인증 된 어떤 hello hello Azure AD 디렉터리를 식별 합니다. 앱 토큰 hello tooensure hello Azure Active Directory v2.0 끝점에서 제공 하는 hello 발급자 클레임 유효성을 검사 해야 합니다. |
| 발급 시간 |`iat` |`1438535543` |이러한 클레임은 hello는 hello에 토큰이 발급 된 시간, epoch 시간으로 표현 합니다. |
| 만료 시간 |`exp` |`1438539443` |hello 만료 시간 클레임은 hello 시간부터 hello 토큰이 잘못 됨, epoch 시간으로 표현 합니다. 앱이 클레임 tooverify hello의 유효성을 검사 토큰 수명 hello 사용 해야 합니다. |
| 이전이 아님 |`nbf` |`1438535543` |이러한 클레임은 hello 시간부터 hello 토큰이 유효 하 고 epoch 시간으로 표현 합니다. 이 일반적으로 hello 같은 hello 시간 hello 토큰 발급 되었습니다. 앱이 클레임 tooverify hello의 유효성을 검사 토큰 수명 hello 사용 해야 합니다. |
| 버전 |`ver` |`1.0` |Azure AD에 의해 정의 된 대로 hello ID 토큰의 hello 버전입니다. |
| 코드 해시 |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |OAuth 2.0 권한 부여 코드와 함께 hello 토큰이 발급 될 경우에 코드 해시 ID 토큰에 포함 됩니다. 해시 코드를 권한 부여 코드의 사용된 toovalidate hello 신뢰성 될 수 있습니다. 방법에 대 한 자세한 내용은 tooperform이 유효성이 검사를 hello 참조 [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다.  |
| 액세스 토큰 해시 |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |OAuth 2.0 액세스 토큰 함께 hello 토큰이 발급 될 경우에 액세스 토큰 해시 ID 토큰에 포함 됩니다. 액세스 토큰 해시 액세스 토큰의 hello 신뢰성 toovalidate 사용된 될 수 있습니다. 방법에 대 한 자세한 내용은 tooperform이 유효성이 검사를 hello 참조 [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)  |
| nonce |`nonce` |`12345` |Nonce는 toomitigate 토큰 재생 공격을 사용 하는 전략입니다. 앱 hello를 사용 하 여 권한 부여 요청에서 nonce에 지정할 수 `nonce` 쿼리 매개 변수입니다. hello에 수정 되지 않은 hello 값 hello 요청에서 제공 하는 발생 `nonce` 만 ID 토큰의 클레임입니다. 이렇게 하면 지정 된 ID 토큰을 hello 응용 프로그램의 세션을 연결 하는 hello 요청에 지정 된 hello 값에 대 한 사용자가 앱 tooverify hello 값. 앱은 hello ID 토큰 유효성 검사 프로세스 중이 유효성 검사를 수행 해야 합니다. |
| 제목 |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Hello 보안 주체는 hello에 대 한 토큰 어설션 응용 프로그램의 hello 사용자 등의 정보입니다. 이 값은 변경할 수 없으며 재할당 또는 재사용할 수 없습니다. 을 안전 하 게 경우와 같이 hello 토큰 사용 되는 tooaccess 리소스 권한 부여 확인을 사용 하는 tooperform 수 있습니다. 기본적으로 hello 주체 클레임 hello 디렉터리의 hello 사용자의 개체 ID hello 채워집니다. toolearn 더 참조 [Azure Active Directory B2C: 토큰, 세션 및 single sign on 구성](active-directory-b2c-token-session-sso.md)합니다. |
| 인증 컨텍스트 클래스 참조 |`acr` |해당 없음 |이전 정책의 hello 경우를 제외 하 고 현재 사용 하지 않을 경우. toolearn 더 참조 [Azure Active Directory B2C: 토큰, 세션 및 single sign on 구성](active-directory-b2c-token-session-sso.md)합니다. |
| 보안 프레임워크 정책 |`tfp` |`b2c_1_sign_in` |사용 되는 tooacquire hello ID 토큰을가 하는 hello 정책의 hello 이름입니다. |
| 인증 시간 |`auth_time` |`1438535543` |이러한 클레임은 hello 시간 시간을 사용자 마지막 입력 한 자격 epoch 시간으로 표시 합니다. |

### <a name="refresh-tokens"></a>새로 고침 토큰
새로 고침 토큰은 보안 토큰 앱 tooacquire 새 ID 토큰을 사용 하 고 액세스는 OAuth 2.0 흐름 토큰 수입니다. 응용 프로그램에 제공 장기 액세스 tooresources 사용자를 대신 하 여 해당 사용자와 상호 작용 없이 합니다.

토큰 응답에 새로 고침 토큰 tooreceive 앱 hello를 요청 해야 `offline_acesss` 범위입니다. hello에 대 한 자세한 toolearn `offline_access` 범위, toohello 참조 [Azure AD B2C 프로토콜 참조](active-directory-b2c-reference-protocols.md)합니다.

새로 고침 토큰 및 완전히 불투명 tooyour 응용 프로그램은 항상 됩니다. 새로 고침 토큰은 Azure AD에서 발급되며 Azure AD에서만 검사 및 해석될 수 있습니다. 수명이 긴 않지만 응용 프로그램을 작성 하 여 새로 고침 토큰은 특정 시간 동안 지속 되는 hello 가정 하 하지 않아야 합니다. 다양한 이유로 언제든지 새로 고침 토큰이 무효화될 수 있기 때문입니다. 새로 고침 토큰이 유효한 경우 응용 프로그램 tooknow 프로그램에 대 한 방법은 tooattempt tooredeem만 hello 토큰 요청 tooAzure AD 함으로써 것입니다.

새 토큰에 대 한 새로 고침 토큰을 교환할 때 (hello 응용 프로그램에 게 부여 되 고 `offline_access` 범위)를 hello 토큰 응답에서 새로운 새로 고침 토큰을 받게 됩니다. 새로 발급 하는 hello 새로 고침 토큰을 저장 해야 합니다. 이전에 hello 요청에 사용 하는 hello 새로 고침 토큰을 바꿔야 합니다. 이렇게 하면 새로 고침 토큰이 최대한 오랫동안 유효한 상태로 유지되도록 할 수 있습니다.

## <a name="token-validation"></a>토큰 유효성 검사
토큰 toovalidate 앱 hello 서명과 hello 토큰의 클레임을 확인 해야 합니다.

기본 설정의 언어에 따라 JWT의 유효성 검사에 다양한 오픈 소스 라이브러리를 사용할 수 있습니다. 고유한 유효성 검사 논리보다는 이러한 옵션을 탐색하는 것이 좋습니다. 이 가이드의 hello 정보 tooproperly 해당 라이브러리를 사용 하는 방법을 배울 수 있습니다.

### <a name="validate-hello-signature"></a>Hello 서명 유효성 검사
Hello로 구분 하는 세 개의 세그먼트를 포함 하는 JWT `.` 문자입니다. hello 첫 번째 세그먼트는 hello *헤더*, 두 번째는 hello hello *본문*, 세 번째는 hello hello 및 *서명*합니다. 앱에서 신뢰할 수 있도록 hello 서명 세그먼트 hello 토큰의 사용된 toovalidate hello 신뢰성을 수 있습니다.

Azure AD B2C 토큰은 RSA 256 등의 업계 표준 비대칭 암호화 알고리즘을 사용하여 서명됩니다. hello 토큰의 hello 헤더 hello 키에 대 한 정보를 포함 하 고 toosign hello 토큰을 사용 하는 암호화 방법.

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

hello `alg` 클레임 토큰이 사용 되는 toosign hello hello 알고리즘을 나타냅니다. hello `kid` 클레임 hello 특정 공개 키를 사용 하는 toosign hello 토큰을 나타냅니다.

Azure AD는 특정 시점에서 공개-개인 키 쌍의 특정 집합 중 하나를 사용하여 토큰에 서명할 수 있습니다. Azure AD 앱 작성 toohandle 해당 키를 자동으로 변경 해야 하므로 hello 가능한 키 집합을 정기적으로 회전 합니다. Azure AD에서 사용 되는 업데이트 toohello 공개 키에 대 한 적절 한 주파수 toocheck 매 24 시간입니다.

Azure AD B2C에는 OpenID Connect 메타데이터 끝점이 있습니다. 이렇게 하면 응용 프로그램 런타임 시 Azure AD B2C에 대 한 toofetch 정보. 이 정보에는 끝점, 토큰 콘텐츠 및 토큰 서명 키가 포함됩니다. B2C 디렉터리에 각 정책에 대한 JSON 메타데이터 문서가 있습니다. Hello에 대 한 메타 데이터 문서의 예를 들어 hello `b2c_1_sign_in` 에서 정책을 `fabrikamb2c.onmicrosoft.com` 에:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`tooauthenticate hello 사용자를 사용 하는 hello B2C 디렉터리 및 `b2c_1_sign_in` hello 정책 tooacquire hello 토큰을 사용 합니다. 정책에서 사용 되는 toosign 토큰 (및 여기서 toogo toofetch hello 메타 데이터) toodetermine 두 가지 옵션이 있습니다. 첫째, hello 정책 이름을 ´ â hello `acr` hello 토큰에서 클레임입니다. Base64 디코딩 hello 본문으로 hello JWT의 hello 본문 밖으로 클레임을 구문 분석할 수 있습니다 및 JSON 문자열 hello를 역직렬화 하는 동안 해당 결과입니다. hello `acr` 클레임 토큰이 사용 되는 tooissue hello hello 정책의 hello 이름이 됩니다.  다른 옵션은 hello hello 값에서 tooencode hello 정책 `state` hello 요청을 발급 하 고 정책을 사용한 toodetermine 디코딩할 때 매개 변수입니다. 두 방법 중 하나는 유효합니다.

hello 메타 데이터 문서는 몇 가지 유용한 정보를 포함 하는 JSON 개체입니다. 이러한 hello 끝점 필요한 tooperform OpenID Connect 인증의 hello 위치를 포함 합니다. 또한 포함 `jwks_uri`, hello 집합이 사용 되는 toosign 토큰은 공개 키의 hello 위치를 제공 하는 합니다. 해당 위치는 여기에 제공 된 이지만 최상의 toofetch hello 위치 동적으로 구문 분석 및 hello 메타 데이터 문서를 사용 하 여 `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

이 URL에 있는 hello JSON 문서 hello 공개 키에 있는 모든 정보는 특정 순간에 사용 하 여 포함 합니다. 앱 hello צ ְ ײ `kid` hello JWT 헤더 tooselect hello 공개 키에 사용 되는 toosign hello JSON 문서에서 특정 토큰 클레임입니다. Hello 올바른 공개 키와 hello 표시 된 알고리즘을 사용 하 여 서명 유효성 검사를 수행한 다음 것입니다.

Tooperform 서명 유효성 검사 방법은이 문서의 hello 범위 외부의 설명입니다. 여러 오픈 소스 라이브러리는이 경우가는 필요한 사용 가능한 toohelp입니다.

### <a name="validate-hello-claims"></a>Hello 클레임의 유효성 검사
응용 프로그램 또는 API ID 토큰을 받으면 hello ID 토큰에서 hello 클레임에 대 한 여러 검사를 수행 해야 것입니다. 포함하지만 다음과 같이 제한되지 않습니다.

* hello **audience** 클레임:이 확인이 hello ID 토큰 의도 한 toobe tooyour 응용 프로그램을 제공 합니다.
* hello **날짜부터** 및 **만료 시간** 클레임: 이러한 해당 hello ID 토큰이 만료 되지 않았는지 확인 하십시오.
* hello **발급자** 클레임: hello 토큰이 Azure AD에서 발급 된 tooyour 앱 확인 합니다.
* hello **nonce**: 토큰 재생 공격 완화 하기 위한 전략입니다.

응용 프로그램에서 수행 해야 하는 유효성 검사 목록은 전체 참조 toohello [OpenID Connect 사양](https://openid.net)합니다. 이러한 클레임에 대 한 hello 예상 값의 세부 정보는 hello 앞에 포함 된 [섹션 토큰](#types-of-tokens)합니다.  

## <a name="token-lifetimes"></a>토큰 수명
토큰 수명 다음 hello는 toofurther 지식을 제공 합니다. 디버그 앱을 개발할 때 도움이 될 수 있습니다. 앱 되지 않아야 하는 이러한 수명 tooremain 상수 중 tooexpect을 기록 합니다. 언제든지 변경될 수 있고 변경됩니다. Hello에 대 한 자세한 [토큰 수명에 대 한 사용자 지정](active-directory-b2c-token-session-sso.md) Azure AD B2C에 있습니다.

| 위임 | 수명 | 설명 |
| --- | --- | --- |
| ID 토큰 |1시간 |ID 토큰은 일반적으로 1시간 동안 유효합니다. 웹 앱이 수명 toomaintain צ ְ ײ 자체 세션 (권장) 사용자가을 합니다. 다른 세션 수명을 선택할 수도 있습니다. 앱 tooget 새 ID 토큰을 필요한 경우 단순히 필요한 toomake 새 로그인 요청 tooAzure AD 합니다. 사용자가 Azure AD와 올바른 브라우저 세션을 경우 해당 사용자 아닐 필요한 tooenter 자격 증명 다시. |
| 새로 고침 토큰 |Too14 일 수를 |단일 새로 고침 토큰이 최대 14일 동안 유효합니다. 그러나 새로 고침 토큰은 여러 가지 이유로 언제든지 무효화될 수 있습니다. Hello 요청이 실패 될 때까지 또는 응용 프로그램 새 hello 새로 고침 토큰으로 대체 될 때까지 앱 tootry toouse 새로 고침 토큰을 계속 해야 합니다. 또한 새로 고침 토큰 90 일이 경과 hello 사용자 마지막 자격 증명을 입력 하는 경우에 잘못 될 수 있습니다. |
| 권한 부여 코드 |5분 |권한 부여 코드는 의도적으로 수명이 단기입니다. 권한 부여 코드가 수신되면 액세스 토큰, ID 토큰 또는 새로 고침 토큰에 대해 즉시 교환해야 합니다. |

