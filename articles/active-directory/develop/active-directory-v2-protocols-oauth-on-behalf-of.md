---
title: "AD aaaAzure v2.0 oauth 2.0에 대신-흐름 | Microsoft Docs"
description: "이 문서에서는 어떻게 oauth 2.0에 대신-흐름 hello toouse HTTP 메시지 tooimplement tooservice 인증 사용 하 여 서비스를 설명 합니다."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 6063869d07c2544000094db8deea7dce19f14f67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 및 OAuth 2.0 On-Behalf-Of 흐름
OAuth 2.0 On-Behalf-Of 흐름 hello hello 사용 사례는 응용 프로그램 서비스/web API를 호출 하는 위치는 차례로 toocall 다른 서비스/web API를 사용 됩니다. hello 개념은 toopropagate hello 위임 된 사용자 id 및 hello 요청 체인을 통해 사용 권한입니다. Hello 중간 계층 서비스 인증 toomake 요청 toohello 다운스트림 서비스에 대 한 hello 사용자를 대신 하 여 Azure Active Directory (Azure AD)에서 액세스 토큰 toosecure가 필요합니다.

> [!NOTE]
> hello v2.0 끝점은 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다. 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

## 프로토콜 다이어그램
Hello를 사용 하 여 응용 프로그램에서 해당 hello 사용자가 인증 되었음을 가정 [OAuth 2.0 인증 코드 부여 흐름](active-directory-v2-protocols-oauth-code.md)합니다. 이 시점에서 hello 응용 프로그램에 hello 사용자 클레임 및 동의 tooaccess hello 중간 계층 웹 API (API A)와 액세스 토큰이 (토큰 A). 이제 API A toomake 인증 된 요청 toohello 다운스트림 웹 API (API B) 필요합니다.

수행 하는 hello 단계 hello에-를 대신 하 여-의 흐름을 구성 하 고 사용 하 여 hello hello 다이어그램을 다음 설명 합니다.

![OAuth2.0 On-Behalf-Of 흐름](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. hello 클라이언트 응용 프로그램은 요청 tooAPI hello 토큰 1. 함께 A
2. API A toohello Azure AD 토큰 발급 끝점을 인증 하 고 토큰 tooaccess 2. API 요청
3. hello Azure AD 토큰 발급 끝점 토큰 a API A의 자격 증명의 유효성을 검사 하 고 문제 API B (토큰 B)에 대 한 액세스 토큰을 hello 합니다.
4. hello 토큰 B hello 요청 tooAPI B. hello 인증 헤더에 설정 된
5. 2. API에서 리소스를 보호 하는 hello의 데이터가 반환 됩니다.

> [!NOTE]
> 이 시나리오에서는 hello 중간 계층 서비스에는 없는 사용자 상호 작용 tooobtain hello 사용자의 동의 tooaccess hello 다운스트림 API 있습니다. 따라서 다운스트림 API에서 제공 되는 옵션 toogrant 액세스 toohello hello 인증 하는 동안 hello 동의 단계의 일부로 선행 합니다.
>

## 서비스 tooservice 액세스 토큰 요청
toorequest 액세스 토큰, 매개 변수 뒤 hello로 HTTP POST toohello 테 넌 트 별 Azure AD v2.0 끝점을 확인 합니다.

```
https://login.microsoftonline.com/<tenant>/oauth2/v2.0/token
```

Hello 클라이언트 응용 프로그램의 toobe 공유 암호 또는 인증서에 의해 보안 선택 여부에 따라 두 가지 경우가 있습니다.

### 첫 번째 사례: 공유 암호를 사용한 액세스 토큰 요청
공유 암호를 사용할 경우 서비스 간 액세스 토큰 요청 매개 변수 뒤 hello를 포함 되어 있습니다.

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| grant_type |필수 | hello 유형의 hello 토큰 요청 합니다. JWT를 사용 하 여 요청에 대 한 hello 길어야 **urn: ietf:params:oauth:grant-형식: jwt-전달자**합니다. |
| client_id |필수 | hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| client_secret |필수 | hello 응용 프로그램 등록 포털에서에서 응용 프로그램에 대해 생성 하는 hello 응용 프로그램 암호입니다. |
| 어설션 |필수 | hello 요청에 사용 되는 hello 토큰의 hello 값입니다. |
| scope |필수 | 공백으로 hello 토큰 요청에 대 한 범위 목록입니다. 자세한 내용은 [범위](active-directory-v2-scopes.md)를 참조하세요.|
| requested_token_use |필수 | Hello 요청 처리 방법을 지정 합니다. 대신 하 여-흐름 hello hello 값 이어야 합니다 **on_behalf_of**합니다. |

#### 예제
다음 HTTP POST hello와 액세스 토큰을 요청 `user.read` hello https://graph.microsoft.com 웹 API에 대 한 범위입니다.

```
//line breaks for legibility only

POST /oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn:ietf:params:oauth:grant-type:jwt-bearer
&client_id=2846f71b-a7a4-4987-bab3-760035b2f389
&client_secret=BYyVnAt56JpLwUcyo47XODd
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiIyODQ2ZjcxYi1hN2E0LTQ5ODctYmFiMy03NjAwMzViMmYzODkiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vNzJmOTg4YmYtODZmMS00MWFmLTkxYWItMmQ3Y2QwMTFkYjQ3L3YyLjAiLCJpYXQiOjE0OTM5MjA5MTYsIm5iZiI6MTQ5MzkyMDkxNiwiZXhwIjoxNDkzOTI0ODE2LCJhaW8iOiJBU1FBMi84REFBQUFnZm8vNk9CR0NaaFV2NjJ6MFFYSEZKR0VVYUIwRUlIV3NhcGducndMMnVrPSIsIm5hbWUiOiJOYXZ5YSBDYW51bWFsbGEiLCJvaWQiOiJkNWU5NzljNy0zZDJkLTQyYWYtOGYzMC03MjdkZDRjMmQzODMiLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJuYWNhbnVtYUBtaWNyb3NvZnQuY29tIiwic3ViIjoiZ1Q5a1FMN2hXRUpUUGg1OWJlX1l5dVZNRDFOTEdiREJFWFRhbEQzU3FZYyIsInRpZCI6IjcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0NyIsInV0aSI6IjN5U3F4UHJweUVPd0ZsTWFFMU1PQUEiLCJ2ZXIiOiIyLjAifQ.TPPJSvpNCSCyUeIiKQoLMixN1-M-Y5U0QxtxVkpepjyoWNG0i49YFAJC6ADdCs5nJXr6f-ozIRuaiPzy29yRUOdSz_8KqG42luCyC1c951HyeDgqUJSz91Ku150D9kP5B9-2R-jgCerD_VVuxXUdkuPFEl3VEADC_1qkGBiIg0AyLLbz7DTMp5DvmbC09DhrQQiouHQGFSk2TPmksqHm3-b3RgeNM1rJmpLThis2ZWBEIPx662pjxL6NJDmV08cPVIcGX4KkFo54Z3rfwiYg4YssiUc4w-w3NJUBQhnzfTl4_Mtq2d7cVlul9uDzras091vFy32tWkrpa970UvdVfQ
&scope=https://graph.microsoft.com/user.read
&requested_token_use=on_behalf_of
```

### 두 번째 사례: 인증서를 사용한 액세스 토큰 요청
인증서와 서비스 간 액세스 토큰 요청 매개 변수 뒤 hello를 포함 되어 있습니다.

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| grant_type |필수 | hello 유형의 hello 토큰 요청 합니다. JWT를 사용 하 여 요청에 대 한 hello 길어야 **urn: ietf:params:oauth:grant-형식: jwt-전달자**합니다. |
| client_id |필수 | hello 응용 프로그램 ID는 hello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) tooyour 응용 프로그램을 할당 합니다. |
| client_assertion_type |필수 |hello 값 이어야 합니다.`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |필수 | 어설션을 (JSON 웹 토큰) toocreate 필요 하 고 hello로 로그인 하면 인증서 응용 프로그램에 대 한 자격 증명으로 등록 됩니다.  에 대 한 읽기 [인증서 자격 증명](active-directory-certificate-credentials.md) toolearn 어떻게 tooregister hello 어설션의 사용자 인증서와 hello 형식입니다.|
| 어설션 |필수 | hello 요청에 사용 되는 hello 토큰의 hello 값입니다. |
| requested_token_use |필수 | Hello 요청 처리 방법을 지정 합니다. 대신 하 여-흐름 hello hello 값 이어야 합니다 **on_behalf_of**합니다. |
| scope |필수 | 공백으로 hello 토큰 요청에 대 한 범위 목록입니다. 자세한 내용은 [범위](active-directory-v2-scopes.md)를 참조하세요.|

Hello 매개 변수는 거의 hello hello 요청의 hello 경우 처럼 동일한 공유 암호 하 여 제외 하 고 hello client_secret 매개 변수는 두 매개 변수로 대체: client_assertion_type 및 client_assertion 합니다.

#### 예제
다음 HTTP POST hello와 액세스 토큰을 요청 `user.read` 인증서를 사용 하 여 hello https://graph.microsoft.com 웹 API에 대 한 범위입니다.

```
// line breaks for legibility only

POST /oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=https://graph.microsoft.com/user.read
```

## 서비스 tooservice 액세스 토큰 응답
성공 응답은 다음 매개 변수는 hello로 JSON OAuth 2.0 응답입니다.

| 매개 변수 | 설명 |
| --- | --- |
| token_type |Hello 토큰 형식 값을 나타냅니다. Azure AD에서는 형식만 hello **전달자**합니다. 전달자 토큰에 대 한 자세한 내용은 참조 hello [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt)합니다. |
| scope |hello 토큰에 부여 된 액세스 hello 범위입니다. |
| expires_in |시간 hello 액세스 토큰의 hello 길이 (초)에서 유효합니다. |
| access_token |hello 요청 된 액세스 토큰입니다. 서비스를 호출 하는 hello이 토큰 tooauthenticate toohello 수신 서비스를 사용할 수 있습니다. |
| refresh_token |hello hello 요청 된 액세스 토큰에 대 한 새로 고침 토큰입니다. 서비스를 호출 하는 hello hello 현재 액세스 토큰이 만료 되 면이 토큰 toorequest 다른 액세스 토큰을 사용할 수입니다. |

### 성공 응답 예제
hello 다음 예제에서는 hello https://graph.microsoft.com 웹 API에 대 한 액세스 토큰에 대 한 성공 응답 tooa 요청

```
{
  "token_type": "Bearer",
  "scope": "https://graph.microsoft.com/user.read",
  "expires_in": 3269,
  "ext_expires_in": 0,
  "access_token": "eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQTZOVGFlN0NkV1c3UWZkQ0NDYy0tY0hGa18wZE50MVEtc2loVzRMd2RwQVZISGpnTVdQZ0tQeVJIaGlDbUN2NkdyMEpmYmRfY1RmMUFxU21TcFJkVXVydVJqX3Nqd0JoN211eHlBQSIsImFsZyI6IlJTMjU2IiwieDV0IjoiejAzOXpkc0Z1aXpwQmZCVksxVG4yNVFIWU8wIiwia2lkIjoiejAzOXpkc0Z1aXpwQmZCVksxVG4yNVFIWU8wIn0.eyJhdWQiOiJodHRwczovL2dyYXBoLm1pY3Jvc29mdC5jb20iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDcvIiwiaWF0IjoxNDkzOTMwMzA1LCJuYmYiOjE0OTM5MzAzMDUsImV4cCI6MTQ5MzkzMzg3NSwiYWNyIjoiMCIsImFpbyI6IkFTUUEyLzhEQUFBQU9KYnFFWlRNTnEyZFcxYXpKN1RZMDlYeDdOT29EMkJEUlRWMXJ3b2ZRc1k9IiwiYW1yIjpbInB3ZCJdLCJhcHBfZGlzcGxheW5hbWUiOiJUb2RvRG90bmV0T2JvIiwiYXBwaWQiOiIyODQ2ZjcxYi1hN2E0LTQ5ODctYmFiMy03NjAwMzViMmYzODkiLCJhcHBpZGFjciI6IjEiLCJmYW1pbHlfbmFtZSI6IkNhbnVtYWxsYSIsImdpdmVuX25hbWUiOiJOYXZ5YSIsImlwYWRkciI6IjE2Ny4yMjAuMC4xOTkiLCJuYW1lIjoiTmF2eWEgQ2FudW1hbGxhIiwib2lkIjoiZDVlOTc5YzctM2QyZC00MmFmLThmMzAtNzI3ZGQ0YzJkMzgzIiwib25wcmVtX3NpZCI6IlMtMS01LTIxLTIxMjc1MjExODQtMTYwNDAxMjkyMC0xODg3OTI3NTI3LTI2MTE4NDg0IiwicGxhdGYiOiIxNCIsInB1aWQiOiIxMDAzM0ZGRkEwNkQxN0M5Iiwic2NwIjoiVXNlci5SZWFkIiwic3ViIjoibWtMMHBiLXlpMXQ1ckRGd2JTZ1JvTWxrZE52b3UzSjNWNm84UFE3alVCRSIsInRpZCI6IjcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0NyIsInVuaXF1ZV9uYW1lIjoibmFjYW51bWFAbWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hY2FudW1hQG1pY3Jvc29mdC5jb20iLCJ1dGkiOiJWR1ItdmtEZlBFQ2M1dWFDaENRSkFBIiwidmVyIjoiMS4wIn0.cubh1L2VtruiiwF8ut1m9uNBmnUJeYx4x0G30F7CqSpzHj1Sv5DCgNZXyUz3pEiz77G8IfOF0_U5A_02k-xzwdYvtJUYGH3bFISzdqymiEGmdfCIRKl9KMeoo2llGv0ScCniIhr2U1yxTIkIpp092xcdaDt-2_2q_ql1Ha_HtjvTV1f9XR3t7_Id9bR5BqwVX5zPO7JMYDVhUZRx08eqZcC-F3wi0xd_5ND_mavMuxe2wrpF-EZviO3yg0QVRr59tE3AoWl8lSGpVc97vvRCnp4WVRk26jJhYXFPsdk4yWqOKZqzr3IFGyD08WizD_vPSrXcCPbZP3XWaoTUKZSNJg",
  "refresh_token": "OAQABAAAAAABnfiG-mA6NTae7CdWW7QfdAALzDWjw6qSn4GUDfxWzJDZ6lk9qRw4AnqPnvFqnzS3GiikHr5wBM1bV1YyjH3nUeIhKhqJWGwqJFRqs2sE_rqUfz7__3J92JDpi6gDdCZNNaXgreQsH89kLCVNYZeN6kGuFGZrjwxp1wS2JYc97E_3reXBxkHrA09K5aR-WsSKCEjf6WI23FhZMTLhk_ZKOe_nWvcvLj13FyvSrTMZV2cmzyCZDqEHtPVLJgSoASuQlD2NXrfmtcmgWfc3uJSrWLIDSn4FEmVDA63X6EikNp9cllH3Gp7Vzapjlnws1NQ1_Ff5QrmBHp_LKEIwfzVKnLLrQXN0EzP8f6AX6fdVTaeKzm7iw6nH0vkPRpUeLc3q_aNsPzqcTOnFfgng7t2CXUsMAGH5wclAyFCAwL_Cds7KnyDLL7kzOS5AVZ3Mqk2tsPlqopAiHijZaJumdTILDudwKYCFAMpUeUwEf9JmyFjl2eIWPmlbwU7cHKWNvuRCOYVqbsTTpJthwh4PvsL5ov5CawH_TaV8omG_tV6RkziHG9urk9yp2PH9gl7Cv9ATa3Vt3PJWUS8LszjRIAJmyw_EhgHBfYCvEZ8U9PYarvgqrtweLcnlO7BfnnXYEC18z_u5wemAzNBFUje2ttpGtRmRic4AzZ708tBHva2ePJWGX6pgQbiWF8esOrvWjfrrlfOvEn1h6YiBW291M022undMdXzum6t1Y1huwxHPHjCAA"
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
GET /v1.0/me HTTP/1.1
Host: graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJub25jZSI6IkFRQUJBQUFBQUFCbmZpRy1tQTZOVGFlN0NkV1c3UWZkSzdNN0RyNXlvUUdLNmFEc19vdDF3cEQyZjNqRkxiNlVrcm9PcXA2cXBJclAxZVV0QktzMHEza29HN3RzXzJpSkYtQjY1UV8zVGgzSnktUHZsMjkxaFNBQSIsImFsZyI6IlJTMjU2IiwieDV0IjoiejAzOXpkc0Z1aXpwQmZCVksxVG4yNVFIWU8wIiwia2lkIjoiejAzOXpkc0Z1aXpwQmZCVksxVG4yNVFIWU8wIn0.eyJhdWQiOiJodHRwczovL2dyYXBoLm1pY3Jvc29mdC5jb20iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDcvIiwiaWF0IjoxNDkzOTMwMDE2LCJuYmYiOjE0OTM5MzAwMTYsImV4cCI6MTQ5MzkzMzg3NSwiYWNyIjoiMCIsImFpbyI6IkFTUUEyLzhEQUFBQUlzQjN5ZUljNkZ1aEhkd1YxckoxS1dlbzJPckZOUUQwN2FENTVjUVRtems9IiwiYW1yIjpbInB3ZCJdLCJhcHBfZGlzcGxheW5hbWUiOiJUb2RvRG90bmV0T2JvIiwiYXBwaWQiOiIyODQ2ZjcxYi1hN2E0LTQ5ODctYmFiMy03NjAwMzViMmYzODkiLCJhcHBpZGFjciI6IjEiLCJmYW1pbHlfbmFtZSI6IkNhbnVtYWxsYSIsImdpdmVuX25hbWUiOiJOYXZ5YSIsImlwYWRkciI6IjE2Ny4yMjAuMC4xOTkiLCJuYW1lIjoiTmF2eWEgQ2FudW1hbGxhIiwib2lkIjoiZDVlOTc5YzctM2QyZC00MmFmLThmMzAtNzI3ZGQ0YzJkMzgzIiwib25wcmVtX3NpZCI6IlMtMS01LTIxLTIxMjc1MjExODQtMTYwNDAxMjkyMC0xODg3OTI3NTI3LTI2MTE4NDg0IiwicGxhdGYiOiIxNCIsInB1aWQiOiIxMDAzM0ZGRkEwNkQxN0M5Iiwic2NwIjoiVXNlci5SZWFkIiwic3ViIjoibWtMMHBiLXlpMXQ1ckRGd2JTZ1JvTWxrZE52b3UzSjNWNm84UFE3alVCRSIsInRpZCI6IjcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0NyIsInVuaXF1ZV9uYW1lIjoibmFjYW51bWFAbWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hY2FudW1hQG1pY3Jvc29mdC5jb20iLCJ1dGkiOiJzUVlVekYxdUVVS0NQS0dRTVFVRkFBIiwidmVyIjoiMS4wIn0.Hrn__RGi-HMAzYRyCqX3kBGb6OS7z7y49XPVPpwK_7rJ6nik9E4s6PNY4XkIamJYn7tphpmsHdfM9lQ1gqeeFvFGhweIACsNBWhJ9Nx4dvQnGRkqZ17KnF_wf_QLcyOrOWpUxdSD_oPKcPS-Qr5AFkjw0t7GOKLY-Xw3QLJhzeKmYuuOkmMDJDAl0eNDbH0HiCh3g189a176BfyaR0MgK8wrXI_6MTnFSVfBePqklQeLhcr50YTBfWg3Svgl6MuK_g1hOuaO-XpjUxpdv5dZ0SvI47fAuVDdpCE48igCX5VMj4KUVytDIf6T78aIXMkYHGgW3-xAmuSyYH_Fr0yVAQ
```

## 다음 단계
Hello OAuth 2.0 프로토콜 및 클라이언트 자격 증명을 사용 하 여 다른 방식으로 tooperform 서비스 tooservice 인증에 대해 자세히 알아보기
* [Azure AD v2.0에서 OAuth 2.0 클라이언트 자격 증명 부여](active-directory-v2-protocols-oauth-client-creds.md)
* [Azure AD v2.0의 OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
