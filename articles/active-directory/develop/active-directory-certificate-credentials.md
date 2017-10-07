---
title: "Azure AD에서 자격 증명 aaaCertificate | Microsoft Docs"
description: "이 문서에서는 hello 등록 및 응용 프로그램 인증 인증서 자격 증명 사용"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a>응용 프로그램 인증을 위한 인증서 자격 증명

Azure Active Directory에서는 응용 프로그램 toouse는 자신의 자격 증명 인증에 대 한 예를 들어의 hello OAuth 2.0 클라이언트 자격 증명 부여 흐름 및 hello에 대신-흐름 있습니다.
사용할 수 있는 자격 증명의 한 가지 형태는 JSON 웹 Token(JWT) 어설션 hello 응용 프로그램을 소유 하는 인증서로 서명 합니다.

## <a name="format-of-hello-assertion"></a>Hello 어설션 형식
toocompute hello 어설션 싶을 toouse hello 중 많은 [JSON 웹 토큰](https://jwt.io/) 라이브러리 hello 언어를 선택 합니다. hello 토큰 얻어진 hello 정보가입니다.

#### <a name="header"></a>헤더

| 매개 변수 |  설명 |
| --- | --- | --- |
| `alg` | **RS256**이어야 함 |
| `typ` | **JWT**여야 함 |
| `x5t` | Hello X.509 인증서 s h A-1 지문 이어야 합니다. |

#### <a name="claims-payload"></a>클레임(페이로드)

| 매개 변수 |  설명 |
| --- | --- | --- |
| `aud` | 대상: **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**이어야 함 |
| `exp` | 만료 날짜: hello 토큰이 만료 되는 hello 날짜입니다. hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰 유효 만료 될 때까지 UTC입니다.|
| `iss` | 발급자: hello client_id (hello client 서비스의 응용 프로그램 Id) 여야 합니다. |
| `jti` | GUID: hello JWT ID |
| `nbf` | 날짜부터: hello 날짜는 hello 하기 전에 토큰을 사용할 수 없습니다. hello 시간 1970 년 1 월 1 일에서 hello 시간 (초)로 표시 됩니다 (1970-01-01T0:0:0Z) hello 시간 hello 토큰이 발급 된 될 때까지 UTC입니다. |
| `sub` | 제목:에 대 한 `iss`, hello client_id (hello client 서비스의 응용 프로그램 Id) 여야 합니다. |

#### <a name="signature"></a>서명
hello에 설명 된 대로 hello 인증서 적용 hello 서명을 계산 [JSON 웹 토큰 RFC7519 사양](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>디코딩된 JWT 어설션 예제
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a>인코딩된 JWT 어설션 예제
다음 문자열 hello는 인코딩된 어설션의 예시입니다. 자세히 살펴보면 세 개의 섹션이 점(.)으로 구분된 것을 알 수 있습니다.
hello 첫 번째 섹션 hello 헤더로, 두 번째 hello 페이로드 hello 인코딩하고 hello 마지막는 hello 처음 두 섹션의 내용을 사용 hello hello 인증서로 계산 하는 hello 서명 합니다.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Azure AD에 인증서 등록
tooassociate hello 인증서 자격 증명은 Azure AD에서 hello 클라이언트 응용 프로그램, tooedit hello 응용 프로그램 매니페스트가 필요합니다.
Toocompute를 인증서의 보류는 데 필요 합니다.
- `$base64Thumbprint`해시 hello 인증서의 base64 인코딩을 hello가 있는
- `$base64Value`hello 인증서 원시 데이터의 base64 인코딩입니다 hello가 있는

또한 tooprovide hello 응용 프로그램 매니페스트에서 GUID tooidentify hello 키 해야 (`$keyId`)

Hello 응용 프로그램 매니페스트를 열고 hello 바꿉니다 hello hello 클라이언트 응용 프로그램에 대 한 Azure 응용 프로그램 등록에에서 *keyCredentials* 스키마를 따르는 hello를 사용 하 여 새 인증서 정보를 사용 하 여 속성:
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

Hello 편집 toohello 응용 프로그램 매니페스트를 저장 하 고 AD tooAzure를 업로드 합니다. hello keyCredentials 속성 다중 값 이므로 다양 한 키 관리에 대 한 여러 인증서를 업로드할 수 있습니다.
