---
title: "Azure AD toohello v2.0 끝점 aaaChanges | Microsoft Docs"
description: "Toohello 앱 모델 v2.0 공개 미리 보기 프로토콜 수행 된 변경 내용에 대 한 설명"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>중요 한 업데이트 toohello v 2.0 인증 프로토콜
개발자들은 주목하세요! Hello를 통해 다음 2 주, 수행할 예정 몇 가지 업데이트 tooour v 2.0 인증 프로토콜 집합 의미할 수 있습니다. 주요 우리의 미리 보기 기간 중 작성 한 모든 앱에 대 한 변경 내용입니다.  

## <a name="who-does-this-affect"></a>어떤 것이 영향을 받습니까?
인증 끝점 수렴 되었습니다 toouse hello v2.0 기록 된 모든 앱

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Hello v2.0 끝점에 대 한 자세한 내용은 있습니다 [여기](active-directory-appmodel-v2-overview.md)합니다.

우리의 OAuth 또는 OpenID Connect 웹 middlewares 중 하나를 사용 하 여 직접 toohello v 2.0 프로토콜을 코딩 하 여 hello v2.0 끝점을 사용 하는 응용 프로그램 작성 한 또는 다른 3rd 파티 라이브러리 tooperform 인증을 사용 해야 하는 경우 프로젝트 및 확인 tootest 준비 필요한 경우 변경 합니다.

## <a name="who-doesnt-this-affect"></a>어떤 것이 영향을 받지 않습니까?
Hello 프로덕션 Azure AD 인증 끝점에 대해 기록 된 모든 앱

```
https://login.microsoftonline.com/common/oauth2/authorize
```

이 프로토콜은 확정되었으며 어떠한 변경도 발생하지 않습니다.

또한 경우 앱 **만** 우리의 ADAL 라이브러리 tooperform 인증을 사용 하 여 toochange 아무 것도 없습니다.  ADAL은 hello 변경 된 내용에서 앱을 차폐 했습니다.  

## <a name="what-are-hello-changes"></a>Hello 변경이 합니까?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>JWT 헤더에서 hello x5t 값 제거
hello v2.0 끝점이 사용 JWT 토큰을 광범위 하 게 hello 토큰에 대 한 관련 메타 데이터가 있는 헤더 매개 변수 섹션을 포함 하는 합니다.  현재이 Jwt 중 하나의 hello 헤더를 디코딩할 다음과 같이 찾습니다.

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Hello OpenID Connect 메타 데이터 끝점에서 검색 된 대로 hello "x5t" 및 "kid" 속성이 모두 hello 공개 키를 식별 하는 위치를 사용 하는 toovalidate hello 토큰의 서명에 이어야 합니다.

여기 진행 중인 hello 변경은 tooremove "x5t" hello 속성입니다.  동일한 메커니즘 toovalidate 토큰에 있지만 사용 해야 hello "kid" 속성 tooretrieve hello 올바른 공개 키, OpenID Connect 프로토콜에 지정 된 hello로 toouse hello를 계속할 수 있습니다. 

> [!IMPORTANT]
> **작업: 앱 hello hello x5t 값이 있는지 여부에 종속 되지 않습니다.**
> 
> 

### <a name="removing-profileinfo"></a>profile_info 제거
이전에 hello v2.0 끝점에 되었습니다 반환 base64 인코딩된 JSON 개체로 호출 하는 토큰 응답에 `profile_info`합니다.  요청을 전송 하 여 hello v2.0 끝점에서 액세스 토큰을 요청:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

hello 응답은 JSON 개체를 수행 하는 hello와 같습니다.

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

hello `profile_info` hello 사용자 hello 앱의 표시 이름, 이름, 성, 전자 메일 주소, 식별자 및 등을 로그인에 대 한 정보가 포함 된 값입니다.  기본적으로, hello `profile_info` 토큰 캐싱에 사용 된 및 표시 합니다.

이제 hello 제거 `profile_info` 값-하지만 걱정 하지 마십시오 약간 다른 위치에이 정보 toodevelopers를 제공 하 고 계속 합니다.  대신 `profile_info`, hello v2.0 끝점은 이제 반환는 `id_token` 각 토큰 응답에:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

디코딩하고 hello id_token를 구문 분석할 수 있습니다 tooretrieve hello profile_info에서 받은 동일한 정보입니다.  hello id_token JWT JSON 웹 토큰 (), OpenID Connect로 지정 된 내용으로입니다.  hello 이렇게 하는 것에 대 한 코드와 매우 유사 이며, 하기만 tooextract hello 중간 세그먼트 (hello 본문) hello id_token 및 base64 디코딩해야 내 tooaccess hello JSON 개체입니다.

Hello를 통해 다음 2 주, 코드를 작성 해야 앱 tooretrieve hello 사용자 정보가 두 hello에서 `id_token` 또는 `profile_info`; 존재 하는 중입니다.  이런 방식으로 hello 변경 될 때 앱에서 hello 전환을 처리할 원활 하 게 수 `profile_info` 너무`id_token` 중단 없이 합니다.

> [!IMPORTANT]
> **작업: 응용 프로그램의 hello hello 존재 여부에 종속 되지 않는 있는지 확인 `profile_info` 값입니다.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Id_token_expires_in 제거
비슷한 너무`profile_info`, hello 제거도 `id_token_expires_in` 응답에서 매개 변수입니다.  Hello v2.0 끝점 반환에 대 한 값 이전에 `id_token_expires_in` authorize 응답의 예를 들어 각 id_token 응답과 함께:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

반환합니다.

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

hello `id_token_expires_in` 값은 hello 수가 hello id_token은에 대 한 유효한 상태로 유지 하는 시간 (초) 나타냅니다.  Hello 제거 이제 `id_token_expires_in` 완전히 값입니다.  대신, hello OpenID Connect 표준을 사용할 수 있습니다 `nbf` 및 `exp` 는 id_token의 tooexamine hello 유효성 클레임입니다.  Hello 참조 [v2.0 토큰 참조](active-directory-v2-tokens.md) 이러한 클레임에 대 한 자세한 내용은 합니다.

> [!IMPORTANT]
> **작업: 응용 프로그램의 hello hello 존재 여부에 종속 되지 않는 있는지 확인 `id_token_expires_in` 값입니다.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>범위에서 반환 된 hello 클레임 변경 openid =
이 변경 됩니다. 가장 중요 한 – hello 실제로으로 hello v2.0 끝점을 사용 하는 거의 모든 앱에 영향을 줍니다.  Hello를 사용 하 여 많은 응용 프로그램이 송신 요청 toohello v2.0 끝점 `openid` 같은 범위:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Hello 사용자 hello에 대 한 동의 허용 하는 경우 현재 `openid` 범위 앱 다양 한 hello 사용자에 대 한 정보 id_token으로 인해 발생 하는 hello에 받습니다.  이러한 클레임에는 이름, 기본 설정된 사용자 이름, 전자 메일 주소, 개체 ID 등이 있습니다.

이 업데이트에서 변경 하 고 hello 정보는 hello `openid` 범위 hello 사양 OpenID Connect로 toobetter comform에 응용 프로그램 액세스를 제공 합니다.  hello `openid` 범위만을 통해 앱 toosign hello 사용자가 되며 hello 사용자에 대 한 응용 프로그램별 식별자 hello에 수신 `sub` hello id_token의 청구 합니다.  id_token의 클레임만 hello로 hello `openid` 부여 범위 개인 식별 정보 보내게 됩니다.  예시 id_token 클레임은 다음과 같습니다.

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Hello 사용자에 대 한 응용 프로그램에서 tooobtain 개인 식별이 가능한 정보 (PII)를 원하는 경우 응용 프로그램에 hello 사용자 로부터 toorequest 추가 권한이 필요 합니다.  도입 새 범위 두에 대 한 지원을 hello OpenID Connect 사양-에서 hello `email` 및 `profile` 수 있게 해 주는 toodo 하므로 범위 – 합니다.

* hello `email` 범위는 매우 단순 – hello 통해 응용 프로그램 액세스 toohello 사용자 기본 전자 메일 주소를 허용 `email` hello id_token에 클레임입니다.  해당 hello 참고 `email` 클레임 항상 누락 될 id_tokens에-만 포함 됩니다 hello 사용자의 프로필에 사용할 수 있는 경우.
* hello `profile` ID, 개체 범위는 응용 프로그램 액세스 tooall hello 사용자-해당 이름, 기본 사용자 이름에 대 한 다른 기본 정보를 제공 합니다.

이렇게 하면 toocode 최소 공개 방식-앱의 정보는 앱에 필요한 toodo 작업 집합에만 hello에 대 한 hello 사용자를 요청할 수 있습니다.  Hello 전체 집합이 현재 응용 프로그램을 수신 하는 사용자 정보를 가져오는 toocontinue를 원하는 경우에 권한 부여 요청에서 모든 세 가지 범위를 포함 해야:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Hello 보내는 응용 프로그램을 시작할 수 `email` 및 `profile` 범위를 즉시 인과 hello v2.0 끝점은 이러한 두 범위를 수락 하 고 필요에 따라 사용자 로부터 권한 요청을 시작 합니다.  Hello hello의 hello 해석에 변경 하는 반면 `openid` 범위 내용이 적용 되지 것입니다 몇 주 동안 발생 합니다.

> [!IMPORTANT]
> **작업: hello 추가 `profile` 및 `email` 앱 hello 사용자에 대 한 정보를 요구 하는 경우의 범위가 지정 합니다.**  ADAL은 기본적으로 요청에 이러한 권한을 모두 포함하게 됩니다. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Hello 발급자 후행 슬래시를 제거 합니다.
이전에 hello 발급자 값 hello v2.0 끝점에서 토큰에 표시 되는 데 걸린 hello 양식

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

여기서 hello guid hello 토큰을 발급 한 hello Azure AD 테 넌 트의 tenantId hello 되었습니다.  이러한 변경 내용으로 hello 발급자 값은

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

hello OpenID Connect 검색 문서 및 두 토큰에 있습니다.

> [!IMPORTANT]
> **작업: 앱 발급자 유효성 검사 중 hello 발급자 값 모두와 사용 하지 않는 끝에 슬래시를 수락 하 고 있는지 확인 합니다.**
> 
> 

## <a name="why-change"></a>변경한 이유는 무엇입니까?
이러한 변경 내용을 도입 하는 데 기본 동기 hello toobe hello OpenID Connect 표준 사양 준수입니다.  OpenID Connect 규격 됨으로써 toominimize 다른 id 서비스 hello 업계의 Microsoft id 서비스와 통합 차이점 하시기 바랍니다.  원하는 tooenable 개발자 toouse 해당 즐겨 찾는 오픈 소스 인증 라이브러리 tooalter hello 라이브러리 tooaccommodate Microsoft 차이 필요 없이 합니다.

## <a name="what-can-you-do"></a>어떻게 해야 합니까?
현재로 서 모든 위에서 설명한 hello 변경 하기 시작할 수 있습니다.  다음은 즉시 수행해야 합니다.

1. **Hello에서 모든 종속성을 제거 `x5t` header 매개 변수입니다.**
2. **hello 전환을 정상적으로 처리할 `profile_info` 너무`id_token` 토큰 응답에 있습니다.**
3. **Hello에서 모든 종속성을 제거 `id_token_expires_in` 응답 매개 변수입니다.**
4. **Hello 추가 `profile` 및 `email` 범위 tooyour 앱 응용 프로그램에 기본 사용자 정보가 필요한 경우.**
5. **토큰에 후행 슬래시가 있는 발급자 값과 없는 발급자 값을 모두 수락합니다.**

우리의 [v2.0 프로토콜 설명서](active-directory-v2-protocols.md) 는 이미 사용 되었으므로 업데이트 tooreflect 이러한 변경 내용을 코드를 업데이트 하는 데 대 한 참조로 사용할 수 있습니다.

Hello hello 변경 범위에 추가 질문이 있으면 언제 라도 무료 tooreach 아웃에서 Twitter에서 toous @AzureAD합니다.

## <a name="how-often-will-protocol-changes-occur"></a>프로토콜은 얼마나 자주 변경합니까?
추가 주요 toohello 인증 프로토콜을 변경 하지 않는 것으로 예상 합니다.  의도적으로이 유형의 업데이트 프로세스를 통해 toogo 언제 든 지 곧 않아도 되도록 한 릴리스에 이러한 변경 내용을 번들로 म 합니다.  Tooadd 기능 toohello 계속 것 물론, v2.0 인증 서비스를 이용할 수 있는 수렴 형 않지만 해당 변경 내용을 누적 및 기존 코드를 중단 하지 포함 되어야 합니다.

마지막으로, toosay 주셔서 hello 미리 보기 기간 동안 작업을 시도해 하겠습니다.  hello insights 및 우리의 조기 채택자의 경험 되지 않은 귀중 한 지금까지 하 고 계속 해 서 tooshare 의견과 아이디어 하시기 바랍니다.

즐거운 코딩 작업이 되길 바랍니다!

Microsoft Identity 나누기 hello

