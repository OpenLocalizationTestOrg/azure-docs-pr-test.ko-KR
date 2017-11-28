---
title: "AD 서비스 tooService Auth aaaAzure oauth 2.0을 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 toouse HTTP 메시지 tooimplement tooservice 인증 hello oauth 2.0 클라이언트 자격 증명 부여 흐름을 사용 하 여 서비스 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# 클라이언트 자격 증명 (예: 공유 암호 또는 인증서)를 사용 하 여 서비스 tooservice 호출
hello OAuth 2.0 클라이언트 자격 증명 부여 흐름을 통해 웹 서비스 (*기밀 클라이언트*) toouse tooauthenticate 다른를 호출할 때 사용자를 가장 하는 대신 고유한 자격 증명 웹 서비스입니다. 이 시나리오에서는 hello 클라이언트가 있는 경우 일반적으로 중간 계층 웹 서비스, 데몬 서비스 또는 웹 사이트 더 높은 수준의 보증을 위해 Azure AD 서비스 toouse (대신 공유 암호) 자격 증명으로 인증서를 호출 하는 hello를 수도 있습니다.

## 클라이언트 자격 증명 부여 흐름 다이어그램
hello 다음 다이어그램에서는 설명 hello 클라이언트 자격 증명 흐름 works Azure Active Directory (Azure AD)에 부여 하는 방법입니다.

![OAuth 2.0 클라이언트 자격 증명 부여 흐름](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. toohello Azure AD 토큰 발급 끝점을 인증 하 고 액세스 토큰을 요청 하는 hello 클라이언트 응용 프로그램입니다.
2. hello Azure AD 토큰 발급 끝점 문제 hello 액세스 토큰입니다.
3. hello 액세스 토큰은 사용 되는 tooauthenticate toohello 리소스를 보호 합니다.
4. 리소스를 보호 하는 hello 데이터로 toohello 웹 응용 프로그램에 반환 됩니다.

## Hello 서비스를 Azure AD에 등록
서비스를 호출 하는 hello와 hello 수신 서비스를 Azure Active Directory (Azure AD)에 등록 합니다. 자세한 지침은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)을 참조하세요.

## 액세스 토큰 요청
toorequest 액세스 토큰에는 HTTP POST toohello 테 넌 트 별 Azure AD 끝점을 사용 합니다.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## 서비스 간 액세스 토큰 요청
Hello 클라이언트 응용 프로그램의 toobe 공유 암호 또는 인증서에 의해 보안 선택 여부에 따라 두 가지 경우가 있습니다.

### 첫 번째 사례: 공유 암호를 사용한 액세스 토큰 요청
공유 암호를 사용할 경우 서비스 간 액세스 토큰 요청 매개 변수 뒤 hello를 포함 되어 있습니다.

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| grant_type |필수 |요청 된 hello 지정 허용 형식입니다. 클라이언트 자격 증명 부여 흐름 hello 값 이어야 합니다 **client_credentials**합니다. |
| client_id |필수 |웹 서비스를 호출 하는 hello의 hello Azure AD 클라이언트 id를 지정 합니다. hello에서 응용 프로그램의 클라이언트 ID를 호출 하는 toofind hello [Azure 포털](https://portal.azure.com), 클릭 **Active Directory**, 디렉터리를 바꾸거나 hello 응용 프로그램을 클릭 합니다. hello client_id는 hello *응용 프로그램 ID* |
| client_secret |필수 |Azure AD에서 웹 서비스 또는 데몬 응용 프로그램을 호출 하는 hello에 대 한 등록 키를 입력 합니다. toocreate hello Azure 포털의에서 키 클릭 **Active Directory**, 디렉터리 전환, hello 응용 프로그램, **설정**, 클릭 **키**, 고 키를 추가 합니다.|
| resource |필수 |Hello hello 수신 웹 서비스의 앱 ID URI를 입력 합니다. hello Azure 포털에서에서 앱 ID URI toofind hello 클릭 **Active Directory**디렉터리 전환 되어 있고 hello 서비스 응용 프로그램을 클릭 한 다음 클릭, **설정** 및 **속성** |

#### 예제
hello 다음 HTTP POST 요청 hello https://service.contoso.com/ 웹 서비스에 대 한 액세스 토큰입니다. hello `client_id` hello 액세스 토큰을 요청 하는 hello 웹 서비스를 식별 합니다.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### 두 번째 사례: 인증서를 사용한 액세스 토큰 요청
인증서와 서비스 간 액세스 토큰 요청 매개 변수 뒤 hello를 포함 되어 있습니다.

| 매개 변수 |  | 설명 |
| --- | --- | --- |
| grant_type |필수 |지정 hello 요청 응답 유형입니다. 클라이언트 자격 증명 부여 흐름 hello 값 이어야 합니다 **client_credentials**합니다. |
| client_id |필수 |웹 서비스를 호출 하는 hello의 hello Azure AD 클라이언트 id를 지정 합니다. hello에서 응용 프로그램의 클라이언트 ID를 호출 하는 toofind hello [Azure 포털](https://portal.azure.com), 클릭 **Active Directory**, 디렉터리를 바꾸거나 hello 응용 프로그램을 클릭 합니다. hello client_id는 hello *응용 프로그램 ID* |
| client_assertion_type |필수 |hello 값 이어야 합니다.`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |필수 | 어설션을 (JSON 웹 토큰) toocreate 필요 하 고 hello로 로그인 하면 인증서 응용 프로그램에 대 한 자격 증명으로 등록 됩니다. 에 대 한 읽기 [인증서 자격 증명](active-directory-certificate-credentials.md) toolearn 어떻게 tooregister hello 어설션의 사용자 인증서와 hello 형식입니다.|
| resource | 필수 |Hello hello 수신 웹 서비스의 앱 ID URI를 입력 합니다. hello Azure 포털에서에서 앱 ID URI toofind hello 클릭 **Active Directory**, hello 디렉터리를 클릭, hello 응용 프로그램을 클릭 한 다음 클릭 **구성**합니다. |

Hello 매개 변수는 거의 hello hello 요청의 hello 경우 처럼 동일한 공유 암호 하 여 제외 하 고 hello client_secret 매개 변수는 두 매개 변수로 대체: client_assertion_type 및 client_assertion 합니다.

#### 예제
다음 HTTP POST hello 인증서로 hello https://service.contoso.com/ 웹 서비스에 대 한 액세스 토큰을 요청 합니다. hello `client_id` hello 액세스 토큰을 요청 하는 hello 웹 서비스를 식별 합니다.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### 서비스 간 액세스 토큰 응답

성공 응답 매개 변수 뒤 hello로 JSON OAuth 2.0 응답이 포함:

| 매개 변수 | 설명 |
| --- | --- |
| access_token |hello 요청 된 액세스 토큰입니다. 웹 서비스를 호출 하는 hello이 토큰 tooauthenticate toohello 수신 웹 서비스를 사용할 수 있습니다. |
| token_type |Hello 토큰 형식 값을 나타냅니다. Azure AD에서는 형식만 hello **전달자**합니다. 전달자 토큰에 대 한 자세한 내용은 참조 hello [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt)합니다. |
| expires_in |시간 hello 액세스 토큰 (초)에서 유효 합니다. |
| expires_on |hello 액세스 토큰이 만료 되 면 hello 시간입니다. hello 날짜는 hello 시간 (초)에서 1970-01-hello 만료 시간까지 01T0:0:0Z UTC입니다. 이 값은 캐시 된 토큰의 사용 되는 toodetermine hello 수명입니다. |
| not_before |액세스 토큰이 있는 hello에서 사용할 수 있게 하는 hello 시간입니다. hello 날짜는 hello 시간 (초)에서 1970-01-hello 토큰의 유효 시간까지 01T0:0:0Z UTC입니다.|
| resource |hello hello 수신 웹 서비스의 앱 ID URI입니다. |

#### 응답 예제
hello 다음 예제에서는 액세스 토큰 tooa 웹 서비스에 대 한 성공 응답 tooa 요청

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## 참고 항목
* [Azure AD의 OAuth 2.0](active-directory-protocols-oauth-code.md)
* [공유 암호를 사용 하 여 hello 서비스 tooservice 호출의 C# 샘플](https://github.com/Azure-Samples/active-directory-dotnet-daemon) 및 [인증서로 hello 서비스 tooservice 호출의 C# 샘플](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
