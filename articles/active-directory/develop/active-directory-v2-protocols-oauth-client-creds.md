---
title: "Azure AD aaaUse v2.0 tooaccess 사용자 개입 없이 리소스를 보호 | Microsoft Docs"
description: "Hello OAuth 2.0 인증 프로토콜의 구현 hello Azure AD 사용 하 여 웹 응용 프로그램을 작성 합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 및 hello OAuth 2.0 클라이언트 자격 증명 흐름
Hello를 사용할 수 있습니다 [OAuth 2.0 클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4)라고도 함, *OAuth 2 다리*, 응용 프로그램의 hello id를 사용 하 여 웹 호스팅 리소스 tooaccess 합니다. 이 유형의 grant 일반적으로 사용자와 직접 상호 작용 없이 hello 백그라운드에서 실행 해야 하는 서버 간 상호 작용에 사용 됩니다. 이러한 유형의 응용 프로그램에는 자주 참조 tooas 되나요 *데몬* 또는 *서비스 계정*합니다.

> [!NOTE]
> hello v2.0 끝점은 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다. 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

대부분의 일반적인 hello에 *3 다리 OAuth*, 클라이언트 응용 프로그램 특정 사용자를 대신 하 여 부여 된 권한을 tooaccess 리소스는 합니다. hello 권한이 hello 하는 동안 일반적으로 hello 사용자 toohello 응용 프로그램에서 위임 [동의](active-directory-v2-scopes.md) 프로세스입니다. 그러나 hello 클라이언트 자격 증명 흐름 권한은 부여 직접 toohello 응용 프로그램 자체입니다. Hello 앱 토큰 tooa 리소스를 사용 하는 경우 hello 리소스 자체 hello 응용 프로그램에 권한 부여 tooperform 동작 및 하지 해당 hello 사용자에 게 권한 부여를 적용 합니다.

## 프로토콜 다이어그램
hello 전체 클라이언트 자격 증명 흐름 비슷한 toohello 다음 다이어그램을 찾습니다. 이 문서의 뒷부분에 나오는 hello 단계를 각각 설명 합니다.

![클라이언트 자격 증명 흐름](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## 직접 권한 부여 가져오기
응용 프로그램 두 가지 방법 중 하나에 일반적으로 직접 권한 부여 tooaccess 리소스를 받을: hello 리소스에 액세스 제어 목록 (ACL)를 통해 또는 Azure Active Directory (Azure AD)에 응용 프로그램 사용 권한 할당을 통해. 이 두 메서드는 Azure AD에서 가장 일반적으로 hello 및 클라이언트와 hello 클라이언트 자격 증명 흐름을 수행 하는 리소스에 대 한 좋습니다. 그러나 리소스 수도 tooauthorize 여기에 클라이언트와 다른 방식으로. 각 리소스 서버 hello에 해당 응용 프로그램에 가장 적합 한 수행 하는 hello 메서드를 선택할 수 있습니다.

### 액세스 제어 목록
리소스 공급자는 특정 수준의 액세스를 알고 권한을 부여하는 응용 프로그램 ID 목록에 따라 권한 부여 확인을 적용할 수 있습니다. Hello 리소스 hello v2.0 끝점에서 토큰을 받으면 hello 토큰을 디코드 하 고 hello에서 hello 클라이언트 응용 프로그램 ID를 추출할 수 `appid` 및 `iss` 클레임입니다. 그런 다음 hello 응용 프로그램 유지 관리 하는 ACL에 대해 비교 합니다. ACL의 세분성을 hello 및 메서드 리소스 간에 크게 달라질 수 있습니다.

일반적인 사용 사례는 toouse 웹 응용 프로그램 또는 웹 API에 대 한 ACL toorun 테스트 합니다. hello 웹 API에 대 한 모든 권한 tooa 특정 클라이언트의 하위 집합만을 제공할 수 있습니다. hello API에서 종단 간 테스트를 toorun hello v2.0 끝점에서 토큰을 확보 하 고 다음 API toohello 보냅니다 하는 테스트 클라이언트를 만듭니다. hello API 다음 hello에 대 한 ACL 검사 hello toohello API의 전체 기능에 대 한 모든 액세스에 대 한 클라이언트의 응용 프로그램 ID를 테스트합니다. 이러한 종류의 ACL 사용 하는 경우 반드시 toovalidate는 뿐만 아니라 호출자의 hello `appid` 값입니다. 또한 해당 hello 유효성을 검사 `iss` hello 토큰의 값은 신뢰할 수 있는 합니다.

이 유형의 권한 부여는 일반적으로 데몬이 및 소비자 사용자 개인 Microsoft 계정을 자신이 소유한 tooaccess 데이터를 필요로 하는 서비스 계정. 조직에서 소유 하는 데이터에 대 한 응용 프로그램 사용 권한을 통해 hello 필요한 권한을 얻게 하는 것이 좋습니다.

### 응용 프로그램 사용 권한
Acl을 사용 하는 대신 Api tooexpose 응용 프로그램 사용 권한 집합을 사용할 수 있습니다. 응용 프로그램 권한은 tooan 응용 프로그램 조직의 관리자가 수행 하며 사용 되는 유일한 tooaccess 데이터가 소유할 수 해당 조직 및 해당 직원입니다. 예를 들어 Microsoft Graph는 여러 응용 프로그램 사용 권한 toodo hello 다음을 제공합니다.

* 모든 사서함에서 메일 읽기
* 모든 사서함에서 메일 읽기 및 쓰기
* 모든 사용자로 메일 보내기
* 디렉터리 데이터 읽기

응용 프로그램 사용 권한에 대 한 자세한 내용은 이동 너무[Microsoft Graph](https://graph.microsoft.io)합니다.

응용 프로그램에서 응용 프로그램 사용 권한 toouse hello 다음 섹션에서 설명 하는 단계 hello지 않습니다.

#### Hello 응용 프로그램 등록 포털에 hello 권한 요청
1. Hello에 tooyour 응용 프로그램 이동 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), 또는 [응용 프로그램을 만들](active-directory-v2-app-registration.md)아직 없는 경우, 합니다. Toouse 해야 응용 프로그램을 만들 때 하나 이상의 응용 프로그램 암호입니다.
2. Hello 찾을 **직접 응용 프로그램 사용 권한** 섹션을 앱에 필요한 hello 권한을 추가 합니다.
3. **저장** hello 앱 등록 합니다.

#### Tooyour 앱에서 로그인 hello 사용자 권장:
일반적으로 응용 프로그램 사용 권한을 사용 하는 응용 프로그램을 빌드할 때 hello 응용 프로그램 페이지 또는 보기는 hello에 관리자가 승인을 하면 hello 앱 사용 권한 필요 합니다. 이 페이지는 hello 응용 프로그램의 로그인 흐름을 hello 앱 설정의 일부로 포함 될 수 있습니다 또는 "연결" 흐름 전용 될 수 있습니다. 대부분의 경우에서 이렇게 하면 앱 tooshow hello에 대 한 사용자가 회사 또는 학교 Microsoft 계정으로 로그인 한 후에 보기를 "연결"이 있습니다.

Hello 사용자 tooyour 앱에 로그인 하는 경우에 hello 조직을 식별할 수 있습니다 toowhich hello 사용자가 속한 전에 hello 사용자 tooapprove hello 응용 프로그램 권한을 요청 합니다. 반드시 필요하지는 않지만 사용자를 위한 보다 직관적인 환경을 만드는 것이 유용할 수 있습니다. 다음에서 toosign hello 사용자 우리의 [v2.0 프로토콜 자습서](active-directory-v2-protocols.md)합니다.

#### 디렉터리 관리자 hello 사용 권한을 요청
Hello 조직의 관리자의 사용 권한을 준비 toorequest 되 면 hello 사용자 toohello v2.0 리디렉션할 수 있습니다 *관리자 동의 끝점*합니다.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| 매개 변수 | 조건 | 설명 |
| --- | --- | --- |
| tenant |필수 |hello 디렉터리 테 넌 트의 toorequest 허가 합니다. 이는 GUID 또는 친숙한 이름 형식일 수 있습니다. 테 넌 트 hello 사용자가 속한 모든 테 넌 트를 사용 하 여를 사용 하 여 로그인을 toolet 원하는 tooand 알지 못하는 경우 `common`합니다. |
| client_id |필수 |hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| redirect_uri |필수 |hello 저장할 hello 응답 toobe 앱 toohandle에 대 한 전송 URI을 리디렉션합니다. 정확히 일치 해야 하나 hello 리디렉션 hello 포털에 등록 하는 Uri URL 인코딩 이어야 한다는 및 추가 경로 세그먼트를 가질 수 있습니다. |
| state |권장 |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 된 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. hello 상태가 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전입니다. |

이 시점에서 Azure AD 테 넌 트 관리자만 toocomplete hello 요청에 서명할 수를 적용 합니다. 관리자에 게 요청한 hello 응용 프로그램 등록 포털에서 응용 프로그램에 대 한 직접 응용 프로그램 사용 권한 hello 모든 tooapprove를 묻는 메시지가 나타납니다.

##### 성공적인 응답
Admin 님 안녕하세요 응용 프로그램에 대 한 hello 권한의 승인 하는 경우 hello 성공적인 응답은 다음과 같습니다.

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| 매개 변수 | 설명 |
| --- | --- | --- |
| tenant |응용 프로그램 hello 권한을 부여 hello 디렉터리 테 넌 트와 요청한 GUID 형식에서입니다. |
| state |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 된 값입니다. 원하는 모든 콘텐츠의 문자열일 수 있습니다. hello 상태가 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전입니다. |
| admin_consent |도**true**합니다. |

##### 오류 응답
Admin 님 안녕하세요 응용 프로그램에 대 한 hello 권한을 승인 하지 않습니다, hello 실패 한 경우 응답은 다음과 같습니다.

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| 매개 변수 | 설명 |
| --- | --- | --- |
| error |Tooclassify 종류를 사용할 수 있는 오류 코드 문자열 하 고 오류의 tooreact tooerrors를 사용할 수 있습니다. |
| error_description |수 있는 특정 오류 메시지는 오류의 근본 원인 hello를 식별 합니다. |

성공적인 응답 hello 앱 프로 비전 끝점에서 받은 후 응용 프로그램에 요청한 hello 직접 응용 프로그램 권한을 왔습니다. 이제 원하는 hello 리소스에 대 한 토큰을 요청할 수 있습니다.

## 토큰 가져오기
응용 프로그램에 대 한 hello 필요한 권한을 획득 한 후에 Api에 대 한 액세스 토큰을 획득 하기를 진행 합니다. tooget hello 클라이언트 자격 증명 부여를 사용 하 여 토큰을 보내는 POST 요청 toohello `/token` v2.0 끝점:

### 첫 번째 사례: 공유 암호를 사용한 액세스 토큰 요청

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| 매개 변수 | 조건 | 설명 |
| --- | --- | --- |
| client_id |필수 |hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| scope |필수 |hello에 대 한 hello 값이 전달 `scope` 이 요청에서 매개 변수 hello로 부착 원하는 hello 리소스 hello 리소스 식별자 (응용 프로그램 ID URI) 이어야 합니다 `.default` 접미사입니다. Hello Microsoft Graph 예제 hello 값은 `https://graph.microsoft.com/.default`합니다. 이 값을 모든 hello 직접 응용 프로그램 권한을 앱에 대 한 구성의 것 발급 해야 원하는 hello 리소스와 관련 된 것과 hello에 대 한 토큰 toouse hello v2.0 끝점에 알립니다. |
| client_secret |필수 |hello hello 응용 프로그램 등록 포털에서 응용 프로그램에 대해 생성 한 응용 프로그램 암호입니다. |
| grant_type |필수 |`client_credentials`이어야 합니다. |

### 두 번째 사례: 인증서를 사용한 액세스 토큰 요청

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| 매개 변수 | 조건 | 설명 |
| --- | --- | --- |
| client_id |필수 |hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| scope |필수 |hello에 대 한 hello 값이 전달 `scope` 이 요청에서 매개 변수 hello로 부착 원하는 hello 리소스 hello 리소스 식별자 (응용 프로그램 ID URI) 이어야 합니다 `.default` 접미사입니다. Hello Microsoft Graph 예제 hello 값은 `https://graph.microsoft.com/.default`합니다. 이 값을 모든 hello 직접 응용 프로그램 권한을 앱에 대 한 구성의 것 발급 해야 원하는 hello 리소스와 관련 된 것과 hello에 대 한 토큰 toouse hello v2.0 끝점에 알립니다. |
| client_assertion_type |필수 |hello 값 이어야 합니다.`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |필수 | 어설션을 (JSON 웹 토큰) toocreate 필요 하 고 hello로 로그인 하면 인증서 응용 프로그램에 대 한 자격 증명으로 등록 됩니다. 에 대 한 읽기 [인증서 자격 증명](active-directory-certificate-credentials.md) toolearn 어떻게 tooregister hello 어설션의 사용자 인증서와 hello 형식입니다.|
| grant_type |필수 |`client_credentials`이어야 합니다. |

Hello 매개 변수는 거의 hello hello 요청의 hello 경우 처럼 동일한 공유 암호 하 여 제외 하 고 hello client_secret 매개 변수는 두 매개 변수로 대체: client_assertion_type 및 client_assertion 합니다.

### 성공적인 응답
성공적인 응답은 다음과 같습니다.

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| 매개 변수 | 설명 |
| --- | --- |
| access_token |hello 요청 된 액세스 토큰입니다. hello 앱이 토큰 tooauthenticate toohello tooa 웹 API와 같은 리소스에 보안을 사용할 수 있습니다. |
| token_type |Hello 토큰 형식 값을 나타냅니다. Azure AD에서는 형식만 hello `bearer`합니다. |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |

### 오류 응답
오류 응답은 다음과 같습니다.

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |발생 하는 오류 및 tooreact tooerrors tooclassify 형식을 사용할 수 있습니다는 오류 코드 문자열입니다. |
| error_description |인증 오류 hello 근본 원인을 파악 하는 데 도움이 되는 특정 오류 메시지. |
| error_codes |진단에 도움이 될 수 있는 STS 특정 오류 코드의 목록입니다. |
| timestamp |hello hello 오류가 발생 한 시간입니다. |
| trace_id |진단에 도움이 될 수 있는 hello 요청에 대 한 고유 식별자입니다. |
| correlation_id |구성 요소에서 진단에 도움이 될 수 있는 hello 요청에 대 한 고유 식별자입니다. |

## 토큰 사용
토큰을 획득 했습니다 했으므로 hello 토큰 toomake 요청 toohello 리소스를 사용 합니다. Hello 토큰이 만료 되 면 hello 요청 toohello 반복 `/token` 끝점 tooacquire 새 액세스 토큰입니다.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## 코드 샘플
toosee 구현 hello 관리자 동의 끝점을 사용 하 여 클라이언트 자격 증명 부여를 hello 응용 프로그램의 예 참조 우리의 [v2.0 데몬 코드 샘플](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)합니다.
