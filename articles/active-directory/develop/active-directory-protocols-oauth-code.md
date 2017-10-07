---
title: "Azure AD의 OAuth 2.0 인증 코드 흐름 aaaUnderstand hello | Microsoft Docs"
description: "이 문서에서는 toouse HTTP 메시지 tooauthorize tooweb 응용 프로그램 및 Azure Active Directory 및 OAuth 2.0을 사용 하 여 테 넌 트의 웹 Api에 액세스 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# OAuth 2.0 및 Azure Active Directory를 사용 하 여 tooweb 응용 프로그램 액세스 권한 부여
Azure Active Directory (Azure AD) tooauthorize 액세스 tooweb 응용 프로그램을 Azure AD 테 넌 트의 웹 Api OAuth 2.0 tooenable를 사용 합니다. 이 가이드는 독립적, 언어 및 설명 방법을 toosend 우리의 오픈 소스 라이브러리를 사용 하지 않고 HTTP 메시지를 수신 하 고 있습니다.

OAuth 2.0 인증 코드 흐름 hello에 설명 되어 [섹션 4.1 hello OAuth 2.0 사양의](https://tools.ietf.org/html/rfc6749#section-4.1)합니다. 사용 되는 tooperform 인증 및 권한 부여 웹 응용 프로그램을 비롯 한 대부분의 응용 프로그램 종류에서 이며 기본적으로 설치 된 앱입니다.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## OAuth 2.0 권한 부여 흐름
상위 수준 응용 프로그램에 대 한 hello 전체 권한 부여 흐름은 약간 다음과 같습니다.

![OAuth 인증 코드 흐름](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## 인증 코드 요청
hello 클라이언트 hello 사용자 toohello 전달로 시작 하는 hello 권한 부여 코드 흐름 `/authorize` 끝점입니다. 이 요청에서 hello 클라이언트 hello 사용자 로부터 tooacquire 필요한 hello 권한을 나타냅니다. Hello에 Azure 클래식 포털에서 응용 프로그램의 페이지에서 hello OAuth 2.0 끝점을 가져올 수 있습니다 **끝점 보기** hello 맨 아래 서랍에서 단추입니다.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  값은 테 넌 트 식별자, 예를 들어 hello 허용 `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 또는 `contoso.onmicrosoft.com` 또는 `common` 테 넌 트 독립적 토큰에 대 한 |
| client_id |필수 |hello 응용 프로그램 Id 할당된 tooyour 때 응용 프로그램 Azure AD에 등록 합니다. Hello Azure 포털에서에서이 찾을 수 있습니다. 클릭 **Active Directory**hello 디렉터리 hello 응용 프로그램을 선택 및을 차례로 클릭 **구성** |
| response_type |필수 |포함 해야 `code` hello 권한 부여 코드 흐름에 대 한 합니다. |
| redirect_uri |권장 |인증 응답 전송 끌어다 응용 프로그램에서 받은 수 있는 응용 프로그램의 hello redirect_uri입니다.  또한 url로 인코딩되어 있어야 점을 제외 하 고 hello 포털에 등록 된 hello redirect_uris 중 하나에 정확히 일치 해야 합니다.  네이티브 및 모바일 앱의 hello 기본값을 사용 해야 `urn:ietf:wg:oauth:2.0:oob`합니다. |
| response_mode |권장 |사용 되는 toosend hello 결과 토큰 백 tooyour 앱 되어야 하는 hello 방법을 지정 합니다.  `query` 또는 `form_post`일 수 있습니다. |
| state |권장 |또한 hello 토큰 응답에 반환 되는 hello 요청에 포함 하는 값입니다. 일반적으로 [교차 사이트 요청 위조 공격을 방지](http://tools.ietf.org/html/rfc6749#section-10.12)하기 위해 임의로 생성된 고유 값이 사용됩니다.  hello 상태 hello 페이지 보기에 있는 것과 같은 hello 인증 요청이 발생 하기 전에 hello 앱에서 hello 사용자의 상태에 대 한 정보를 사용 하는 tooencode 이기도 합니다. |
| resource |선택 사항 |hello hello 웹 API (보안된 리소스)의 앱 ID URI입니다. toofind hello hello Azure 포털에서에서 hello web API의 앱 ID URI 클릭 **Active Directory**hello 디렉터리를 클릭, hello 응용 프로그램을 클릭 한 다음 클릭 **구성**합니다. |
| prompt |선택 사항 |필요한 사용자 상호 작용 hello 형식을 나타냅니다.<p> 유효한 값은 다음과 같습니다. <p> *로그인*: hello 사용자 프롬프트 tooreauthenticate 여야 합니다. <p> *동의*: 사용자 동의 부여 된 이지만 toobe 업데이트 합니다. hello 사용자 프롬프트 tooconsent 여야 합니다. <p> *admin_consent*: 관리자가 조직에서 모든 사용자를 대신 하 여 증명된 tooconsent 여야 합니다 |
| login_hint |선택 사항 |자신의 사용자 이름을 미리 알고 있는 경우 hello 사용자에 대 한 hello 로그인 페이지의 사용된 toopre 채우기 hello 사용자 이름/전자 메일 주소 필드 수 있습니다.  종종 앱이 매개이 변수를 사용 하 여 hello username 이전 로그인에서 추출 된 이미 있으면 다시 인증 하는 동안 hello를 사용 하 여 `preferred_username` 클레임입니다. |
| domain_hint |선택 사항 |Hello 테 넌 트 또는 사용자 hello 도메인에 대 한 힌트에서 toosign 사용할지를 제공 합니다. hello domain_hint hello 값은 hello 테 넌 트에 대 한 등록 된 도메인입니다. Hello 테 넌 트 페더레이션된 tooan 온-프레미스 디렉터리 이면 AAD toohello 지정한 테 넌 트 페더레이션 서버를 리디렉션합니다. |

> [!NOTE]
> Hello 사용자 조직의 일부 이면 hello 조직의 관리자 수 동의 또는 거부 hello 사용자 대신 하거나 hello 사용자 tooconsent 허용 합니다. hello 사용자 관리자에 게 허용 하는 경우에 hello 옵션 tooconsent을 제공 됩니다.
>
>

이 시점에서 hello를 묻는 메시지가 tooenter hello에 표시 된 자격 증명 및 동의 toohello 권한을 `scope` 쿼리 매개 변수입니다. Azure AD hello에 응답 tooyour 앱 보냅니다 hello 사용자를 인증 하 고 동의 허용 하면 `redirect_uri` 요청에 대 한 주소입니다.

### 성공적인 응답
성공적인 응답은 다음과 같습니다.

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| 매개 변수 | 설명 |
| --- | --- |
| admin_consent |관리자가 동의 요청 프롬프트 tooa 동의한 경우 hello 값은 True입니다. |
| 코드 |hello 응용 프로그램을 요청 하는 hello 권한 부여 코드입니다. hello 응용 hello 대상 리소스에 대 한 hello 권한 부여 코드 toorequest 액세스 토큰을 사용할 수 있습니다. |
| session_state |Hello 현재 사용자 세션을 식별 하는 고유 값입니다. 이 값은 GUID이지만 검사 없이 전달되는 불투명 값으로 처리되어야 합니다. |
| state |State 매개 변수는 hello 응답에 동일한 값이 표시 되어야 하는 hello hello 요청에 포함 됩니다. Hello 응용 프로그램 tooverify hello 응답을 사용 하기 전에 hello 요청 및 응답의 hello 상태 값이 동일한 지에 대 한 것이 좋습니다. 이렇게 하면 toodetect [교차 사이트 요청 위조 (CSRF) 공격](https://tools.ietf.org/html/rfc6749#section-10.12) hello 클라이언트에 대 한 합니다. |

### 오류 응답
오류 응답도 전송 될 수 있습니다 toohello `redirect_uri` hello 응용 프로그램 적절 하 게 처리할 수 있도록 합니다.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| 매개 변수 | 설명 |
| --- | --- |
| error |Hello의 5.2 항에에서 정의 된 오류 코드 값 [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749)합니다. hello 다음 표에서 Azure AD에서 반환 하는 hello 오류 코드를 설명 합니다. |
| error_description |Hello 오류의 자세한 설명입니다. 이 메시지는 아니며 toobe 최종 사용자 지원 합니다. |
| state |hello 상태 값은 hello 요청에서 전송 되 고 hello 응답 tooprevent 교차 사이트 요청 위조 (CSRF) 공격에 반환 하는 임의로 생성 된 다시 사용할 수 없는 값입니다. |

#### 권한 부여 끝점 오류에 대한 오류 코드
hello 다음 표에서 hello hello에 반환 될 수 있는 다양 한 오류 코드 `error` hello 오류 응답의 매개 변수입니다.

| 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- |
| invalid_request |프로토콜 오류(예: 필수 매개 변수 누락). |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 테스트 중에 발견되는 개발 오류입니다. |
| unauthorized_client |hello 클라이언트 응용 프로그램 없으면 toorequest 인증 코드를 허용 합니다. |이 문제는 일반적으로 hello 클라이언트 응용 프로그램이 Azure AD에 등록 되어 있지 않거나 toohello 사용자의 Azure AD 테 넌 트에 추가 되지 않습니다 때 발생 합니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| access_denied |리소스 소유자가 동의 거부 |hello 클라이언트 응용 프로그램 hello 사용자가 동의 하지 않는 한 진행할 수 hello 사용자에 게 알릴 수 있습니다. |
| unsupported_response_type |hello 권한 부여 서버 hello 요청에 hello 응답 유형을 지원 하지 않습니다. |수정 하 고 hello 요청을 다시 제출 하십시오. 일반적으로 초기 테스트 중에 발견되는 개발 오류입니다. |
| server_error |hello 서버 오류가 발생 했습니다. |Hello 요청을 다시 시도 합니다. 이러한 오류는 일시적인 상태 때문에 발생할 수 있습니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 해당 응답은 tooa 일시적 오류로 인해 지연 합니다. |
| temporarily_unavailable |hello 서버 사용량이 많음 toohandle hello 요청 일시적으로입니다. |Hello 요청을 다시 시도 합니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 tooa 일시적 상태로 인해 응답이 지연 된다고는 됩니다. |
| invalid_resource |hello 대상 리소스가 존재 하지 않는, Azure AD를 찾을 수 없거나 올바르게 구성 되지 않아 유효 하지 않습니다. |이 hello 리소스 있을 경우 구성 되지 않았습니다 hello 테 넌 트에 나타냅니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |

## Hello 권한 부여 코드 toorequest 액세스 토큰을 사용 하 여
POST 요청 toohello 전송 하 여 액세스 토큰 toohello 필요한 리소스에 대 한 hello 코드를 교환할 수 있습니다는 인증 코드를 얻었습니다 하 고 hello 사용자 권한이 부여 된 `/token` 끝점:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| tenant |필수 |hello `{tenant}` hello 요청의 hello 경로 값 hello 응용 프로그램에 로그인 할 수 있는 사용된 toocontrol 하나일 수 있습니다.  값은 테 넌 트 식별자, 예를 들어 hello 허용 `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 또는 `contoso.onmicrosoft.com` 또는 `common` 테 넌 트 독립적 토큰에 대 한 |
| client_id |필수 |hello 응용 프로그램 Id 할당된 tooyour 때 응용 프로그램 Azure AD에 등록 합니다. Hello Azure 클래식 포털에서에서이 찾을 수 있습니다. 클릭 **Active Directory**hello 디렉터리 hello 응용 프로그램을 선택 및을 차례로 클릭 **구성** |
| grant_type |필수 |해야 `authorization_code` hello 권한 부여 코드 흐름에 대 한 합니다. |
| 코드 |필수 |hello `authorization_code` hello 이전 섹션에서 복사한 |
| redirect_uri |필수 |동일한 hello `redirect_uri` 사용된 tooacquire hello 했던 값 `authorization_code`합니다. |
| client_secret |웹앱에 필요 |앱에 대 한 hello 응용 프로그램 등록 포털에서 만든 hello 응용 프로그램 암호입니다.  장치에 client_secret을 안정적으로 저장할 수 없으므로 네이티브 앱에서는 사용하면 안 됩니다.  웹 앱 및 웹 hello 기능 toostore hello를 포함 하는 Api에 대 한 필요한 `client_secret` hello 서버 쪽에서 안전 하 게 합니다. |
| resource |그렇지 않으면 선택적 인증 코드 요청에 지정 된 경우 필수 |hello hello 웹 API (보안된 리소스)의 앱 ID URI입니다. |

hello Azure 관리 포털에서에서 앱 ID URI toofind hello 클릭 **Active Directory**, hello 디렉터리를 클릭, hello 응용 프로그램을 클릭 한 다음 클릭 **구성**합니다.

### 성공적인 응답
Azure AD는 성공적인 응답에 액세스 토큰을 반환합니다. hello 클라이언트 응용 프로그램에서 toominimize 네트워크 호출 및 관련된 지연 시간 hello 클라이언트 응용 프로그램 hello OAuth 2.0 응답에에서 지정 된 hello 토큰 수명에 대 한 액세스 토큰을 캐시 해야 합니다. toodetermine hello 토큰 수명 중 하나가 hello를 사용 하 여 `expires_in` 또는 `expires_on` 매개 변수 값입니다.

웹 API 리소스를 반환 하는 경우는 `invalid_token` 오류 코드 있다는 의미일 수 있습니다 hello 리소스가 해당 hello 토큰이 만료 된을 확인 합니다. Hello 클라이언트 및 리소스 시계 시간이 서로 다른 (라고 "시간 불일치") 인 경우 hello 리소스 hello 토큰 toobe 만료 hello 토큰 hello 클라이언트 캐시에서 지워지기 전에 고려할 수 있습니다. 이 경우 계산 된 수명이 여전히 내에 없을 경우에 hello 캐시에서 토큰 hello 선택을 취소 합니다.

성공적인 응답은 다음과 같습니다.

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| 매개 변수 | 설명 |
| --- | --- |
| access_token |hello 요청 된 액세스 토큰입니다. hello 앱이 토큰 tooauthenticate toohello web API와 같은 리소스에 보안을 사용할 수 있습니다. |
| token_type |Hello 토큰 형식 값을 나타냅니다. hello는만 Azure AD에서는 전달자를 입력 합니다. 전달자 토큰에 대한 자세한 내용은 [OAuth 2.0 권한 부여 프레임워크: 전달자 토큰 사용(RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |
| expires_on |hello 액세스 토큰이 만료 되 면 hello 시간입니다. hello 날짜는 hello 시간 (초)에서 1970-01-hello 만료 시간까지 01T0:0:0Z UTC입니다. 이 값은 캐시 된 토큰의 사용 되는 toodetermine hello 수명입니다. |
| resource |hello hello 웹 API (보안된 리소스)의 앱 ID URI입니다. |
| scope |가장 권한 부여 toohello 클라이언트 응용 프로그램. hello 기본 권한은 `user_impersonation`합니다. 리소스를 보호 하는 hello hello 소유자는 Azure AD에 추가 값을 등록할 수 있습니다. |
| refresh_token |OAuth 2.0 새로 고침 토큰입니다. hello 앱 hello 현재 액세스 토큰이 만료 된 후이 토큰 tooacquire 추가 액세스 토큰을 사용할 수 있습니다.  새로 고침 토큰 수명이 긴 되며 오랜 시간에 사용 되는 tooretain 액세스 tooresources를 사용할 수 있습니다. |
| id_token |서명되지 않은 JWT(JSON 웹 토큰)입니다. hello 앱 수 base64Url hello 사용자 로그인에 대 한이 토큰 toorequest 정보의 hello 세그먼트를 디코드합니다. hello 앱 hello 값을 캐시를 업데이트 하 고를 표시할 수 있지만 것에 의존 하지 않아야 하 보안 경계 또는 권한 부여 합니다. |

### JWT 토큰 클레임
hello hello 값의 JWT 토큰 hello `id_token` 매개 변수는 hello 다음 클레임으로 디코딩될 수 있습니다.

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

JSON 웹 토큰에 대 한 자세한 내용은 참조 hello [JWT IETF 초안 사양을](http://go.microsoft.com/fwlink/?LinkId=392344)합니다. 클레임과 토큰 형식을 hello에 대 한 자세한 내용은 [지원 되는 토큰 및 클레임 유형](active-directory-token-and-claims.md)

hello `id_token` 클레임 유형에 따라 hello 매개 변수를 포함 합니다.

| 클레임 유형 | 설명 |
| --- | --- |
| aud |Hello 토큰의 대상 그룹입니다. Hello audience는 hello hello 토큰 tooa 클라이언트 응용 프로그램을 실행할 때는 `client_id` hello 클라이언트의 합니다. |
| exp |만료 시간입니다. hello 토큰이 만료 되 면 hello 시간입니다. Hello 유효한 토큰 toobe, hello 현재 날짜/시간 이어야 합니다 보다 작거나 같은 toohello `exp` 값입니다. hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰이 발급 된 될 때까지 UTC입니다. |
| family_name |사용자의 성입니다. hello 응용 프로그램이이 값을 표시할 수 있습니다. |
| given_name |사용자의 이름입니다. hello 응용 프로그램이이 값을 표시할 수 있습니다. |
| iat |발급 시간입니다. hello JWT가 발급 하는 hello 시간입니다. hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰이 발급 된 될 때까지 UTC입니다. |
| iss |Hello 토큰 발급자를 식별합니다. |
| nbf |이전 시간이 아닙니다. hello 시간 hello 토큰이 유효 해지는 경우입니다. Hello 유효한 토큰 toobe에 대 한 hello 현재 날짜/시간 보다 크거나 같은 toohello Nbf 값 이어야 합니다. hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰이 발급 된 될 때까지 UTC입니다. |
| oid |Azure AD에 hello 사용자 개체의 개체 식별자 (ID)입니다. |
| sub |토큰 주체 식별자입니다. 이것은 영구적이 고 변경할 수 없는 식별자 토큰 hello hello 사용자에 설명 합니다. 캐싱 논리에 이 값을 사용합니다. |
| tid |ID (식별자) 발급 hello 토큰 hello Azure AD 테 넌 트의 테 넌 트. |
| unique_name |에 대 한 고유 식별자는 표시 된 toohello 사용자 수 있습니다. 일반적으로 사용자 계정 이름(UPN)입니다. |
| upn |Hello 사용자의 사용자 계정 이름입니다. |
| ver |버전. 일반적으로 1.0 hello JWT 토큰의 hello 버전입니다. |

### 오류 응답
hello 토큰 발급 끝점 오류 hello 클라이언트 호출 토큰 발급 끝점을 직접 hello 때문에 HTTP 오류 코드는 합니다. 또한 toohello HTTP 상태 코드 hello Azure AD 토큰 발급 끝점도 반환 hello 오류를 설명 하는 개체에 포함 된 JSON 문서입니다.

샘플 오류 응답은 다음과 같습니다.

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
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

#### HTTP 상태 코드
hello 다음 표 hello 토큰 발급 끝점이 반환 하는 hello HTTP 상태 코드입니다. 경우에 따라 hello 오류 코드는 충분 한 toodescribe hello 응답 하지만 JSON 약관과 tooparse hello 필요 하는 오류가 있는 경우 문서화 하 고 해당 오류 코드를 검사 합니다.

| HTTP 코드 | 설명 |
| --- | --- |
| 400 |기본 HTTP 코드입니다. 대부분의 경우에 사용 하 고는 일반적으로 인해 tooa 형식이 잘못 된 요청입니다. 수정 하 고 hello 요청을 다시 제출 하십시오. |
| 401 |인증에 실패했습니다. 예를 들어 hello 요청 hello client_secret 매개를 변수가 없습니다. |
| 403 |권한 부여에 실패했습니다. 예를 들어 hello 사용자 권한 tooaccess hello 리소스는 없습니다. |
| 500 |Hello 서비스에서 내부 오류가 발생 했습니다. Hello 요청을 다시 시도 합니다. |

#### 토큰 끝점 오류에 대한 오류 코드
| 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- |
| invalid_request |프로토콜 오류(예: 필수 매개 변수 누락). |수정 하 고 hello 요청을 다시 제출 하십시오. |
| invalid_grant |hello 권한 부여 코드가 잘못 되었거나 만료 되었습니다. |새 요청 toohello 시도 `/authorize` 끝점 |
| unauthorized_client |hello 인증 된 클라이언트에 권한이 없습니다 toouse이 권한이 부여 허용 형식입니다. |이 문제는 일반적으로 hello 클라이언트 응용 프로그램이 Azure AD에 등록 되어 있지 않거나 toohello 사용자의 Azure AD 테 넌 트에 추가 되지 않습니다 때 발생 합니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| invalid_client |클라이언트 인증에 실패했습니다. |hello 클라이언트 자격 증명이 올바르지 않습니다. toofix, 응용 프로그램 관리자에 게 hello 자격 증명을 업데이트합니다. |
| unsupported_grant_type |hello 권한 부여 서버 hello 권한 부여 허용 유형을 지원 하지 않습니다. |변경 hello 형식 hello 요청에 권한을 부여 합니다. 이 유형의 오류는 개발 중에만 발생하며 초기 테스트 중에 검색됩니다. |
| invalid_resource |hello 대상 리소스가 존재 하지 않는, Azure AD를 찾을 수 없거나 올바르게 구성 되지 않아 유효 하지 않습니다. |이 hello 리소스 있을 경우 구성 되지 않았습니다 hello 테 넌 트에 나타냅니다. hello 응용 프로그램 hello 응용 프로그램을 설치 하 고 AD tooAzure 추가 대 한 명령으로 hello 사용자를 요구할 수 있습니다. |
| interaction_required |hello 요청 사용자 상호 작용이 필요합니다. 예를 들어 추가 인증 단계가 필요합니다. | 비 대화형 요청을 대신 하 여 다시 시도 hello에 대 한 대화형 요청 동일한 리소스입니다. |
| temporarily_unavailable |hello 서버 사용량이 많음 toohandle hello 요청 일시적으로입니다. |Hello 요청을 다시 시도 합니다. 클라이언트 응용 프로그램 hello toohello 사용자를 확인할 수 있습니다 tooa 일시적 상태로 인해 응답이 지연 된다고는 됩니다. |

## Hello 액세스 토큰 tooaccess hello 리소스를 사용 하 여
성공적으로 인식 한 했으므로 `access_token`, hello에 포함 하 여 hello 토큰 요청 tooWeb Api에서에서 사용할 수 있습니다 `Authorization` 헤더입니다. hello [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) 사양에서 HTTP 요청 tooaccess toouse 전달자 토큰에서 리소스를 보호 하는 방법을 설명 합니다.

### 샘플 요청
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### 오류 응답
RFC 6750 문제 HTTP 상태 코드를 구현하는 보안된 리소스입니다. 에 포함 된 hello 요청 인증 자격 증명을 포함 하지 않는 이거나 hello 토큰, hello 응답 없는 경우는 `WWW-Authenticate` 헤더입니다. 요청이 실패할 경우 리소스 서버 hello hello HTTP 상태 코드 및 오류 코드를 사용 하 여 응답 합니다.

hello 다음은 클라이언트 요청 hello hello 전달자 토큰을 포함 되지 않은 경우 실패 한 응답의 예입니다.

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### 오류 매개 변수
| 매개 변수 | 설명 |
| --- | --- |
| authorization_uri |hello hello 권한 부여 서버의 URI (실제 끝점). 이 값은 조회 key tooget 검색 끝점에서 서버 hello에 대 한 자세한 내용은으로 사용 됩니다. <p><p> 클라이언트 hello 해당 hello 유효성을 검사 해야 권한 부여 서버를 신뢰할 수 있습니다. Hello 리소스는 Azure AD에 의해 보호 되 면 hello URL https://login.microsoftonline.com로 시작 하는 충분 한 tooverify 또는 Azure AD가 지 원하는 다른 호스트 됩니다. 테넌트별 리소스는 언제나 테넌트별 권한 부여 URI를 반환해야 합니다. |
| error |Hello의 5.2 항에에서 정의 된 오류 코드 값 [OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749)합니다. |
| error_description |Hello 오류의 자세한 설명입니다. 이 메시지는 아니며 toobe 최종 사용자 지원 합니다. |
| resource_id |반환 hello hello 리소스의 고유 식별자입니다. hello 클라이언트 응용 프로그램의 hello hello 값으로이 식별자를 사용할 수 `resource` hello 리소스에 대 한 토큰을 요청할 때 매개 변수입니다. <p><p> 이 대 한 중요 클라이언트 응용 프로그램 tooverify이이 값을 hello, 그렇지 않으면 악성 서비스 수 수 tooinduce는 **권한 상승** 공격 <p><p> 권장 전략 hello tooverify는 공격을 방지 하는 hello `resource_id` 일치 hello hello 웹 API URL의 기본 액세스 하 고 있습니다. Https://service.contoso.com/data, 액세스 하는 경우 예를 들어 hello `resource_id` htttps://service.contoso.com/ 될 수 있습니다. hello 클라이언트 응용 프로그램을 거부 해야 합니다는 `resource_id` 신뢰할 수 있는 다른 방법은 tooverify hello id이 없는 경우 기본 URL hello로 시작 하지 않는 합니다. |

#### 전달자 체계 오류 코드
RFC 6750 사양은 hello hello 다음 hello에 대 한 응답 hello Www-authenticate 헤더와 전달자 체계를 사용 하는 리소스에 대 한 오류를 정의 합니다.

| HTTP 상태 코드 | 오류 코드 | 설명 | 클라이언트 작업 |
| --- | --- | --- | --- |
| 400 |invalid_request |hello 요청이 올바르지 않습니다. 예를 들어, 매개 변수 누락 수 또는 동일한 매개 변수를 두 번 hello를 사용 하 여 합니다. |Hello 오류를 수정 하 고 hello 요청을 다시 시도 하십시오. 이 유형의 오류는 개발 중에만 발생하며 초기 테스트에서 검색됩니다. |
| 401 |invalid_token |hello 액세스 토큰이 누락 되었거나, 잘못 되었거나 해지 되었습니다. hello hello error_description 매개 변수 값 추가 세부 정보를 제공합니다. |Hello 권한 부여 서버에서 새 토큰을 요청 합니다. Hello 새 토큰을 사용 해도 오류가 발생 했습니다. 오류 메시지 toohello 사용자 보내기 임의의 지연 시간 후 다시 시도 하십시오. |
| 403 |insufficient_scope |hello 액세스 토큰에는 hello 가장 권한이 필요한 tooaccess hello 리소스를 포함 되지 않습니다. |새 권한 부여 요청 toohello 권한 부여 끝점을 보냅니다. Hello 응답 hello scope 매개 변수에 들어 있는 경우 hello 요청 toohello 리소스의 hello 범위 값을 사용 합니다. |
| 403 |insufficient_access |hello 토큰의 주체 hello 필요한 tooaccess hello 리소스 된 hello 권한을 않아도 됩니다. |Prompt hello 사용자 toouse 다른 계정 또는 toorequest 권한 toohello 리소스를 지정합니다. |

## Hello 액세스 토큰 새로 고침
액세스 토큰 수명이 짧은 이며 리소스에 액세스 하는 toocontinue를 만료 된 후 새로 고쳐져 야 합니다. Hello를 새로 고칠 수 있습니다 `access_token` 다른을 제출 하 여 `POST` toohello 요청 `/token` 끝점 하지만 hello 제공이 이번 `refresh_token` hello 대신 `code`합니다.

새로 고침 토큰에는 지정된 수명이 없습니다. 일반적으로 새로 고침 토큰의 수명은 hello가 비교적 깁니다. 그러나 경우에 따라 새로 고침 토큰 만료, 해지 된 또는 hello 원하는 동작에 대 한 충분 한 권한이 없을 합니다. 응용 프로그램에 필요한 tooexpect 및 핸들 오류 hello 토큰 발급 끝점에서 올바르게 반환 합니다.

새로 고침 토큰 오류가 포함 된 응답을 받으면 hello 현재 새로 고침 토큰을 취소 하 고 새 권한 부여 코드를 요청 하거나 액세스 토큰 합니다. 특히, 새로 고침을 사용 하 여 토큰 때 hello 인증 코드 부여 흐름에에서 hello로 응답을 수신 하는 경우 `interaction_required` 또는 `invalid_grant` hello 새로 고침 토큰을 취소 하 고 새 권한 부여 코드를 요청 하는 오류 코드입니다.

샘플 요청 toohello **테 넌 트 별** 끝점 (hello를 사용할 수도 있습니다 **일반적인** 끝점) tooget 새로 고침 토큰을 사용 하 여 새 액세스 토큰은 다음과 같습니다:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### 성공적인 응답
성공적인 토큰 응답은 다음과 같습니다.

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| 매개 변수 | 설명 |
| --- | --- |
| token_type |hello 토큰 형식입니다. hello만 지원 점은 **전달자**합니다. |
| expires_in |hello 남은 hello 토큰의 수명 (초)입니다. 일반적인 값은 3600(한 시간)입니다. |
| expires_on |hello 날짜 및 시간에는 hello 토큰에 만료 됩니다. hello 날짜는 hello 시간 (초)에서 1970-01-hello 만료 시간까지 01T0:0:0Z UTC입니다. |
| resource |Hello 식별 리소스 보안 해당 hello 액세스 토큰 일 수 있습니다 tooaccess 사용된 합니다. |
| scope |가장 권한 부여 toohello 네이티브 클라이언트 응용 프로그램. hello 기본 권한은 **user_impersonation**합니다. hello 대상 리소스의 hello 소유자는 Azure AD에서 대체 값을 등록할 수 있습니다. |
| access_token |hello 새 액세스 토큰을 요청 합니다. |
| refresh_token |이 응답에 hello 하나 만료 될 때 사용 되는 toorequest 새 액세스 토큰 일 수 있는 새 OAuth 2.0 refresh_token입니다. |

### 오류 응답
샘플 오류 응답은 다음과 같습니다.

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
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

Hello 오류 코드 및 hello 권장 되는 클라이언트 작업의 설명을 참조 하십시오. [토큰 끝점 오류에 대 한 오류 코드](#error-codes-for-token-endpoint-errors)합니다.
