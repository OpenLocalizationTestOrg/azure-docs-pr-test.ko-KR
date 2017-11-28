---
title: "oauth 2.0에 대신-초안 사양을 사용 하 여 aaaAzure AD 서비스 tooservice auth | Microsoft Docs"
description: "이 문서에서는 어떻게 oauth 2.0에 대신-흐름 hello toouse HTTP 메시지 tooimplement tooservice 인증 사용 하 여 서비스를 설명 합니다."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# 서비스 tooservice hello에 대신-흐름에서 위임 된 사용자 id를 사용 하 여 호출
OAuth 2.0 On-Behalf-Of 흐름 hello hello 사용 사례는 응용 프로그램 서비스/web API를 호출 하는 위치는 차례로 toocall 다른 서비스/web API를 사용 됩니다. hello 개념은 toopropagate hello 위임 된 사용자 id 및 hello 요청 체인을 통해 사용 권한입니다. Hello 중간 계층 서비스 인증 toomake 요청 toohello 다운스트림 서비스에 대 한 hello 사용자를 대신 하 여 Azure Active Directory (Azure AD)에서 액세스 토큰 toosecure가 필요합니다.

## On-Behalf-Of 흐름 다이어그램
Hello를 사용 하 여 응용 프로그램에서 해당 hello 사용자가 인증 되었음을 가정 [OAuth 2.0 인증 코드 부여 흐름](active-directory-protocols-oauth-code.md)합니다. 이 시점에서 hello 응용 프로그램에 hello 사용자 클레임 및 동의 tooaccess hello 중간 계층 웹 API (API A)와 액세스 토큰이 (토큰 A). 이제 API A toomake 인증 된 요청 toohello 다운스트림 웹 API (API B) 필요합니다.

수행 하는 hello 단계 hello에-를 대신 하 여-의 흐름을 구성 하 고 사용 하 여 hello hello 다이어그램을 다음 설명 합니다.

![OAuth2.0 On-Behalf-Of 흐름](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. hello 클라이언트 응용 프로그램은 요청 tooAPI hello 토큰 1. 함께 A
2. API A toohello Azure AD 토큰 발급 끝점을 인증 하 고 토큰 tooaccess 2. API 요청
3. hello Azure AD 토큰 발급 끝점 토큰 a API A의 자격 증명의 유효성을 검사 하 고 문제 API B (토큰 B)에 대 한 액세스 토큰을 hello 합니다.
4. hello 토큰 B hello 요청 tooAPI B. hello 인증 헤더에 설정 된
5. 2. API에서 리소스를 보호 하는 hello의 데이터가 반환 됩니다.

## Hello 응용 프로그램 및 서비스를 Azure AD에 등록
Hello 클라이언트 응용 프로그램과 hello 중간 계층 서비스를 Azure AD에 등록 합니다.
### Hello 중간 계층 서비스 등록
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정에 및 hello에서 클릭 **디렉터리** 목록에서 원하는 위치 tooregister 응용 프로그램 hello Active Directory 테 넌 트를 선택 합니다.
3. 클릭 **더 서비스** 왼쪽 nav hello와 선택 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **새 응용 프로그램 등록**을 선택합니다.
5. Hello 응용 프로그램에 대 한 친숙 한 이름을 입력 하 고 hello 응용 프로그램 종류를 선택 합니다. 집합 hello 로그온 URL 또는 리디렉션 URL toohello 기준 URL hello 응용 프로그램 유형을 기반으로 합니다. 클릭 **만들기** toocreate hello 응용 프로그램입니다.
6. 상태 hello Azure 포털에서에서 응용 프로그램을 선택 하 고 클릭 **설정을**합니다. Hello 설정 메뉴에서 선택 **키** 키를 추가 하 고-1 년 또는 2 년의 키 기간을 선택 합니다. 이 페이지를 저장, hello 키 값을 표시할 복사 하 고 안전한 장소에 hello 값 저장--구현에서이 키 이후 tooconfigure hello 응용 프로그램 설정 해야 합니다 키 값이 됩니다 다시 표시 하거나 검색할 수으로 다른 방법 레코드 보십시오 것으로 hello Azure 포털에서에서 표시 됩니다.

### Hello 클라이언트 응용 프로그램 등록
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 위쪽 막대에서 계정에 및 hello에서 클릭 **디렉터리** 목록에서 원하는 위치 tooregister 응용 프로그램 hello Active Directory 테 넌 트를 선택 합니다.
3. 클릭 **더 서비스** 왼쪽 nav hello와 선택 **Azure Active Directory**합니다.
4. **앱 등록**을 클릭하고 **새 응용 프로그램 등록**을 선택합니다.
5. Hello 응용 프로그램에 대 한 친숙 한 이름을 입력 하 고 hello 응용 프로그램 종류를 선택 합니다. 집합 hello 로그온 URL 또는 리디렉션 URL toohello 기준 URL hello 응용 프로그램 유형을 기반으로 합니다. 클릭 **만들기** toocreate hello 응용 프로그램입니다.
6. Hello 설정 메뉴에서 응용 프로그램에 대 한 사용 권한을 구성, hello 선택 **필요한 권한** 섹션에서 클릭 **추가**, 다음 **API 선택**, 및 형식 hello hello 텍스트 상자에 hello 중간 계층 서비스의 이름입니다. 그런 다음 **권한 선택**을 클릭하고 '*서비스 이름* 액세스'를 선택합니다.

### 알려진 클라이언트 응용 프로그램 구성
이 시나리오에서는 hello 중간 계층 서비스에는 없는 사용자 상호 작용 tooobtain hello 사용자의 동의 tooaccess hello 다운스트림 API 있습니다. 따라서 다운스트림 API를 제공 해야 하는 옵션 toogrant 액세스 toohello hello 인증 하는 동안 hello 동의 단계의 일부로 선행 합니다.
tooachieve hello 등록 hello 동의 단일 대화 상자에 hello 클라이언트와 중간 계층에 필요한 병합 된 hello 중간 계층 서비스의 Azure AD에서 tooexplicitly 바인딩 hello 클라이언트 앱 등록 아래 hello 단계가를 수행 합니다.
1. Toohello 중간 계층 서비스 등록을 찾아서 클릭 **매니페스트** tooopen hello 매니페스트 편집기입니다.
2. Hello 매니페스트에서 찾을 hello `knownClientApplications` 배열 속성, 및 요소로 hello hello 클라이언트 응용 프로그램의 클라이언트 ID를 추가 합니다.
3. Hello 저장 단추를 클릭 하 여 hello 매니페스트를 저장 합니다.

## 서비스 tooservice 액세스 토큰 요청
toorequest 액세스 토큰, 매개 변수 뒤 hello로 HTTP POST toohello 테 넌 트 별 Azure AD 끝점을 확인 합니다.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Hello 클라이언트 응용 프로그램의 toobe 공유 암호 또는 인증서에 의해 보안 선택 여부에 따라 두 가지 경우가 있습니다.

### 첫 번째 사례: 공유 암호를 사용한 액세스 토큰 요청
공유 암호를 사용할 경우 서비스 간 액세스 토큰 요청 매개 변수 뒤 hello를 포함 되어 있습니다.

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| grant_type |필수 | hello 유형의 hello 토큰 요청 합니다. JWT를 사용 하 여 요청에 대 한 hello 길어야 **urn: ietf:params:oauth:grant-형식: jwt-전달자**합니다. |
| 어설션 |필수 | hello 요청에 사용 되는 hello 토큰의 hello 값입니다. |
| client_id |필수 | hello 응용 프로그램 ID가 할당 toohello 호출 서비스를 Azure AD에 등록 하는 동안. hello Azure 관리 포털에서에서 앱 ID toofind hello 클릭 **Active Directory**hello 디렉터리를 클릭 하 고 hello 응용 프로그램 이름을 클릭 합니다. |
| client_secret |필수 | Azure AD에서 서비스를 호출 하는 hello에 대 한 hello 키 등록 되었습니다. 이 값을 hello 등록 시 언급 해야 합니다. |
| resource |필수 | hello hello 수신 서비스 (보안된 리소스)의 앱 ID URI입니다. hello Azure 관리 포털에서에서 앱 ID URI toofind hello 클릭 **Active Directory**hello 디렉터리, hello 응용 프로그램 이름을 클릭를 클릭 하 고 **모든 설정을** 클릭 하 고 **속성** . |
| requested_token_use |필수 | Hello 요청 처리 방법을 지정 합니다. 대신 하 여-흐름 hello hello 값 이어야 합니다 **on_behalf_of**합니다. |
| scope |필수 | 공백으로 hello 토큰 요청에 대 한 범위 목록입니다. OpenID Connect에 대 한 범위 hello **openid** 지정 해야 합니다.|

#### 예제
hello 다음 HTTP POST 요청 hello https://graph.windows.net 웹 API에 대 한 액세스 토큰입니다. hello `client_id` hello 액세스 토큰을 요청 하는 hello 서비스를 식별 합니다.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### 두 번째 사례: 인증서를 사용한 액세스 토큰 요청
인증서와 서비스 간 액세스 토큰 요청 매개 변수 뒤 hello를 포함 되어 있습니다.

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| grant_type |필수 | hello 유형의 hello 토큰 요청 합니다. JWT를 사용 하 여 요청에 대 한 hello 길어야 **urn: ietf:params:oauth:grant-형식: jwt-전달자**합니다. |
| 어설션 |필수 | hello 요청에 사용 되는 hello 토큰의 hello 값입니다. |
| client_id |필수 | hello 응용 프로그램 ID가 할당 toohello 호출 서비스를 Azure AD에 등록 하는 동안. hello Azure 관리 포털에서에서 앱 ID toofind hello 클릭 **Active Directory**hello 디렉터리를 클릭 하 고 hello 응용 프로그램 이름을 클릭 합니다. |
| client_assertion_type |필수 |hello 값 이어야 합니다.`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |필수 | 어설션을 (JSON 웹 토큰) toocreate 필요 하 고 hello로 로그인 하면 인증서 응용 프로그램에 대 한 자격 증명으로 등록 됩니다.  에 대 한 읽기 [인증서 자격 증명](active-directory-certificate-credentials.md) toolearn 어떻게 tooregister hello 어설션의 사용자 인증서와 hello 형식입니다.|
| resource |필수 | hello hello 수신 서비스 (보안된 리소스)의 앱 ID URI입니다. hello Azure 관리 포털에서에서 앱 ID URI toofind hello 클릭 **Active Directory**hello 디렉터리, hello 응용 프로그램 이름을 클릭를 클릭 하 고 **모든 설정을** 클릭 하 고 **속성** . |
| requested_token_use |필수 | Hello 요청 처리 방법을 지정 합니다. 대신 하 여-흐름 hello hello 값 이어야 합니다 **on_behalf_of**합니다. |
| scope |필수 | 공백으로 hello 토큰 요청에 대 한 범위 목록입니다. OpenID Connect에 대 한 범위 hello **openid** 지정 해야 합니다.|

Hello 매개 변수는 거의 hello hello 요청의 hello 경우 처럼 동일한 공유 암호 하 여 제외 하 고 hello client_secret 매개 변수는 두 매개 변수로 대체: client_assertion_type 및 client_assertion 합니다.

#### 예제
다음 HTTP POST hello 인증서를 사용 하 여 hello https://graph.windows.net 웹 API에 대 한 액세스 토큰을 요청 합니다. hello `client_id` hello 액세스 토큰을 요청 하는 hello 서비스를 식별 합니다.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## 서비스 tooservice 액세스 토큰 응답
성공 응답은 다음 매개 변수는 hello로 JSON OAuth 2.0 응답입니다.

| 매개 변수 | 설명 |
| --- | --- |
| token_type |Hello 토큰 형식 값을 나타냅니다. Azure AD에서는 형식만 hello **전달자**합니다. 전달자 토큰에 대 한 자세한 내용은 참조 hello [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt)합니다. |
| scope |hello 토큰에 부여 된 액세스 hello 범위입니다. |
| expires_in |시간 hello 액세스 토큰의 hello 길이 (초)에서 유효합니다. |
| expires_on |hello 액세스 토큰이 만료 되 면 hello 시간입니다. hello 날짜는 hello 시간 (초)에서 1970-01-hello 만료 시간까지 01T0:0:0Z UTC입니다. 이 값은 캐시 된 토큰의 사용 되는 toodetermine hello 수명입니다. |
| resource |hello hello 수신 서비스 (보안된 리소스)의 앱 ID URI입니다. |
| access_token |hello 요청 된 액세스 토큰입니다. 서비스를 호출 하는 hello이 토큰 tooauthenticate toohello 수신 서비스를 사용할 수 있습니다. |
| id_token |hello 요청 된 id 토큰입니다. 서비스를 호출 하는 hello이 tooverify hello 사용자의이 id를 사용 하 고 hello 사용자와 세션을 시작할 수 있습니다. |
| refresh_token |hello hello 요청 된 액세스 토큰에 대 한 새로 고침 토큰입니다. 서비스를 호출 하는 hello hello 현재 액세스 토큰이 만료 되 면이 토큰 toorequest 다른 액세스 토큰을 사용할 수입니다. |

### 성공 응답 예제
hello 다음 예제에서는 hello https://graph.windows.net 웹 API에 대 한 액세스 토큰에 대 한 성공 응답 tooa 요청

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### 오류 응답 예제
오류 응답 경우에서 반환 되 Azure AD 토큰 끝점 hello 다운스트림 API에 대 한 액세스 토큰 tooacquire 하려고 할 때 hello 다운스트림 API에 multi-factor authentication에 설정할 수와 같은 조건부 액세스 정책. hello 중간 계층 서비스는 hello 클라이언트 응용 프로그램 hello 사용자 상호 작용 toosatisfy hello 조건부 액세스 정책에 제공할 수 있도록이 오류 toohello 클라이언트 응용 프로그램을 드러나게 됩니다.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## 리소스를 보호 하는 hello 액세스 토큰 tooaccess hello를 사용 하 여
Hello에 hello 토큰을 설정 하 여 hello 중간 계층 서비스 수를 사용 하 여 hello 인증 토큰 획득 한 위에 toomake 요청 toohello 다운스트림 웹 API를 `Authorization` 헤더입니다.

### 예제
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## 다음 단계
Hello OAuth 2.0 프로토콜 및 클라이언트 자격 증명을 사용 하 여 다른 방식으로 tooperform 서비스 tooservice 인증에 대해 자세히 알아보기
* [Azure AD의 OAuth 2.0 클라이언트 자격 증명 부여를 사용 하 여 서비스 tooservice 인증](active-directory-protocols-oauth-service-to-service.md)
* [Azure AD의 OAuth 2.0](active-directory-protocols-oauth-code.md)
