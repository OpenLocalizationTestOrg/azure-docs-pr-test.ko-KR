---
title: "Active Directory v2.0 aaaAzure 토큰 참조 | Microsoft Docs"
description: "Azure AD v2.0 끝점 hello에서 내보내는 hello 유형의 토큰 및 클레임"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Azure Active Directory v2.0 토큰 참조
hello Azure Active Directory (Azure AD) v 2.0 끝점 여러 유형을 내보내는 각 보안 토큰의 [인증 흐름](active-directory-v2-flows.md)합니다. 이 참조는 hello 형식, 보안 특성 및 각 유형의 토큰의 내용을 설명합니다.

> [!NOTE]
> hello v2.0 끝점에는 모든 Azure Active Directory 시나리오 및 기능을 지원 하지 않습니다. 에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는지를 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

## <a name="types-of-tokens"></a>토큰 형식
hello v2.0 끝점 지원 hello [OAuth 2.0 권한 부여 프로토콜](active-directory-v2-protocols.md)를 사용 하 여 액세스 토큰 및 새로 고침 토큰입니다. hello v2.0 끝점에는 또한 인증 및 로그인을 통해 지원 [OpenID Connect](active-directory-v2-protocols.md)합니다. OpenID Connect 토큰, hello ID 토큰의 세 번째 형식을 소개합니다. 이러한 토큰은 각각 *전달자* 토큰으로 표시됩니다.

전달자 토큰은 보호 된 리소스를 부여 전달자 액세스 tooa hello 하는 경량 보안 토큰입니다. hello 전달자 hello 토큰을 제공할 수 있는 당사자입니다. 파티 단계 전송 또는 저장 도중 toosecure hello 토큰을 따르지 않은 경우 Azure AD tooreceive hello 전달자 토큰을 인증 해야, 있지만 차단 하 고 의도 하지 않은 당사자에서 사용 하는 수 있습니다. 일부 보안 토큰 있지만, 전달자 토큰 do 사용 하 여 기본 제공 메커니즘 tooprevent 권한이 없는 파티가 있어야 합니다. 전달자 토큰은 전송 계층 보안(HTTPS) 등의 보안 채널에서 전송해야 합니다. 전달자 토큰은이 유형의 보안 없이 전송 되 면 악의적인 사용자 수 없습니다 "중간자 개입 공격" tooacquire hello 토큰을 사용 하 고 사용 하 여 무단된 액세스 tooa 보호 된 리소스에 대 한. hello 저장 하거나 나중에 사용 하기 위해 전달자 토큰을 캐시 하는 경우 동일한 보안 원칙이 적용 됩니다. 항상 앱이 전달자 토큰을 안전하게 전송하고 저장하도록 합니다. 전달자 토큰의 보안 고려 사항을 자세히 알아보려면 [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750)를 참조하세요.

대부분 hello v2.0 끝점에서 발급 한 hello 토큰의 JSON 웹 토큰 (Jwt)로 구현 됩니다. JWT는 두 당사자 간에 compact, URL 안전한 방식으로 tootransfer 정보입니다. JWT의 hello 정보 라고는 *클레임*합니다. Hello 전달자에 대 한 정보 어설션 및 hello 토큰의 주체 않습니다. JWT의 hello 클레임은 인코딩된 및 전송을 위해 serialize 되는 개체 JSON (JavaScript Notation) 개체입니다. 발행 한 hello Jwt hello v2.0 끝점은 서명이 수행 되지만 암호화 되지, 디버깅을 위해 JWT의 hello 내용의 쉽게 검사할 수 있습니다. Jwt에 대 한 자세한 내용은 참조 hello [JWT 사양의](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)합니다.

### <a name="id-tokens"></a>ID 토큰
ID 토큰은 [OpenID Connect](active-directory-v2-protocols.md)를 사용하여 인증을 수행할 때 앱이 받는 로그인 보안 토큰의 한 형태입니다. ID 토큰으로 표시 됩니다 [Jwt](#types-of-tokens), 하며 toosign hello 사용자 tooyour 응용 프로그램에서 사용할 수 있는 클레임을 포함 합니다. 다양 한 방법으로 ID 토큰에서 hello 클레임을 사용할 수 있습니다. 일반적으로 관리자는 응용 프로그램의 ID 토큰 toodisplay 계정 정보 또는 액세스 제어 결정에 toomake 사용합니다. hello v2.0 끝점 한 가지 유형의 일관 된 hello 유형의 로그인 하는 사용자에 관계 없이 클레임 집합이 있는 ID 토큰을 발급 합니다. hello 형식 및 ID 토큰의 콘텐츠는 hello 동일 하 고 회사 또는 학교 계정에 대 한 개인 Microsoft 계정 사용자에 대 한 합니다.

ID 토큰은 현재 서명되었지만 암호화되지 않았습니다. 앱 ID 토큰을 받으면 다음 조건을 충족 해야 [hello 서명 유효성 검사](#validating-tokens) tooprove 토큰의 신뢰성을 hello 및 값이 유효한 토큰 tooprove hello에에서 몇 가지 클레임 유효성을 검사 합니다. hello 응용 프로그램에서 유효성을 검사 하는 클레임 시나리오 요구 사항에 따라 다르지만 응용 프로그램 일부를 수행 해야 [일반 클레임 유효성 검사](#validating-tokens) 모든 시나리오에서.

저희가에서 ID 토큰의에서 클레임에 대 한 자세한 내용은 hello hello 섹션 다음 또한 tooa 샘플 ID 토큰입니다. ID 토큰의 클레임은 특정 순서로 반환되지 않습니다. 또한 언제든지 새 클레임을 ID 토큰에 도입할 수 있습니다. 새 클레임이 도입될 때 앱을 중단하지 않아야 합니다. hello 목록 다음에 앱을 현재 해석할 안정적 수 있는 hello 클레임 포함 됩니다. Hello에 자세한 내용을 볼 수 [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다.

#### <a name="sample-id-token"></a>샘플 ID 토큰
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> 연습을 tooinspect hello 샘플 ID 토큰으로 붙여 hello hello 샘플 ID 토큰에서 클레임 [calebb.net](http://calebb.net/)합니다.
>
>

#### <a name="claims-in-id-tokens"></a>ID 토큰의 클레임
| 이름 | 클레임 | 예제 값 | 설명 |
| --- | --- | --- | --- |
| audience |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Hello 토큰의 hello 의도 한 받는 사람을 식별합니다. ID 토큰에 hello 대상은 hello Microsoft 응용 프로그램 등록 포털에서에서 tooyour 응용 프로그램을 할당 한 응용 프로그램의 응용 프로그램 ID입니다. 앱이이 값의 유효성을 검사 하 고 hello 값과 일치 하지 않으면 hello 토큰을 거부 해야 합니다. |
| 발급자 |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Hello 보안 토큰 서비스 (STS) 생성 하 고 hello 토큰과 hello Azure AD 테 넌 트 사용자가 인증 된 어떤 hello 반환을 식별 합니다. 앱에는 토큰 hello tooensure hello v2.0 끝점에서 제공 하는 hello 발급자 클레임 유효성을 검사 해야 합니다. 또한 toohello 앱에 로그인 할 수 있는 테 넌 트의 hello 클레임 toorestrict hello 집합의 GUID 부분 hello도 사용 해야 합니다. hello 해당 hello 사용자를 나타내는 GUID가 소비자 사용자 계정이 Microsoft에서 `9188040d-6c67-4c5b-b112-36a304b66dad`합니다. |
| 발급 시간 |`iat` |`1452285331` |hello는 hello에 토큰이 발급 된 시간, epoch 시간으로 표현 합니다. |
| 만료 시간 |`exp` |`1452289231` |hello 시간부터 hello 토큰이 유효 하지 않은 epoch 시간에 표시 합니다. 앱이 클레임 tooverify hello의 유효성을 검사 토큰 수명 hello 사용 해야 합니다. |
| 이전이 아님 |`nbf` |`1452285331` |토큰이 유효 하 게 되는 hello에 hello 시간 epoch 시간으로 표현 합니다. 것이 일반적으로 hello 발급 시간으로 hello 동일 합니다. 앱이 클레임 tooverify hello의 유효성을 검사 토큰 수명 hello 사용 해야 합니다. |
| 버전 |`ver` |`2.0` |hello ID 토큰을 Azure AD에 의해 정의 된 대로의 hello 버전입니다. Hello v2.0 끝점 hello 값은 `2.0`합니다. |
| 테넌트 ID |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |사용자 hello hello Azure AD 테 넌 트를 나타내는 GUID입니다. 회사 및 학교 계정 hello GUID는 hello 변경할 수 없는 테 넌 트에 속한 사용자 hello hello 조직의 ID입니다. 개인 계정을 hello 값은 `9188040d-6c67-4c5b-b112-36a304b66dad`합니다. hello `profile` 범위는 필요한 순서 tooreceive이이 클레임입니다. |
| 코드 해시 |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hello 코드 해시는 OAuth 2.0 권한 부여 코드와 함께 hello ID 토큰이 발급 될 경우에 ID 토큰에 포함 됩니다. 인증 코드의 사용된 toovalidate hello 신뢰성 수 있습니다. 이 유효성 검사를 수행 하는 방법에 대 한 자세한 참조 hello [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다. |
| 액세스 토큰 해시 |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hello 액세스 토큰 해시는 OAuth 2.0 액세스 토큰으로 hello ID 토큰이 발급 될 경우에 ID 토큰에 포함 됩니다. 액세스 토큰의 사용된 toovalidate hello 신뢰성 수 있습니다. 이 유효성 검사를 수행 하는 방법에 대 한 자세한 참조 hello [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다. |
| nonce |`nonce` |`12345` |hello nonce는 토큰 재생 공격을 완화 하기 위한 전략입니다. 앱 hello를 사용 하 여 권한 부여 요청에서 nonce에 지정할 수 `nonce` 쿼리 매개 변수입니다. hello 요청에서 제공 하는 hello 값 hello ID 토큰에 내보낼 `nonce` 수정 되지 않은 클레임입니다. 응용 프로그램 특정 ID 토큰을 hello 응용 프로그램의 세션을 연결 하는 hello 요청에 지정 된 hello 값에 대 한 hello 값을 확인할 수 있습니다. 앱은 hello ID 토큰 유효성 검사 프로세스 중이 유효성 검사를 수행 해야 합니다. |
| name |`name` |`Babe Ruth` |hello 이름 클레임 hello 토큰의 hello 주체를 식별 하는 사람이 읽을 수 있는 값을 제공 합니다. hello 값 toobe 고유는 변경할 수 있고 그것이 설계 toobe 표시 용도로 사용 하는 것을 보장 되지 않습니다. hello `profile` 범위는 필요한 순서 tooreceive이이 클레임입니다. |
| email |`email` |`thegreatbambino@nyy.onmicrosoft.com` |있는 경우 hello 사용자 계정과 연결 된 기본 전자 메일 주소를 hello입니다. 해당 값은 변경 가능하며 시간이 지남에 따라 변경될 수 있습니다. hello `email` 범위는 필요한 순서 tooreceive이이 클레임입니다. |
| 기본 설정된 사용자 이름 |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |hello 주 사용자 이름 hello v2.0 끝점에 대 한 hello 사용자를 나타내는입니다. 메일 주소, 전화 번호 또는 지정된 형식이 없는 일반 사용자 이름일 수 있습니다. 해당 값은 변경 가능하며 시간이 지남에 따라 변경될 수 있습니다. hello `profile` 범위는 필요한 순서 tooreceive이이 클레임입니다. |
| subject |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | hello는 hello에 대 한 토큰 어설션 정보는 응용 프로그램의 hello 사용자 같은 보안 주체입니다. 이 값은 변경할 수 없으며 재할당 또는 재사용할 수 없습니다. 을 안전 하 게 hello 토큰은 사용 되는 tooaccess는 리소스 및 데이터베이스 테이블의 키로 사용할 수 있습니다 때와 같은 사용된 tooperform 권한 부여 확인 수 있습니다. Hello 주체는 항상 hello 토큰에 있기 때문에 해당 Azure AD에서 발행, 범용 권한 부여 시스템에서이 값을 사용 하는 것이 좋습니다. 그러나 hello 주체은 쌍으로 된 식별자-고유 tooa 특정 응용 프로그램 id입니다.  따라서 단일 사용자가 두 개의 서로 다른 클라이언트 Id를 사용 하 여 두 개의 서로 다른 앱에 로그인 할, 해당 앱 hello 주체 클레임에 대 한 서로 다른 두 값 받게 됩니다.  아키텍처 및 개인 정보 보호 요구 사항에 따라 적합할 수도 있고 적합하지 않을 수도 있습니다. |
| 개체 ID |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | hello Microsoft id 시스템,이 경우 사용자 계정에에서는 개체에 대 한 변경할 수 없는 식별자를 hello 합니다.  안전 하 고 데이터베이스 테이블에서 키로 사용 되는 tooperform 권한 부여 확인 일 수도 있습니다. 이 ID는 고유 하 게 hello 사용자 응용 프로그램 간에 식별-동일한 사용자에 게 hello에 로그인 하는 두 개의 서로 다른 응용 프로그램 같은 hello hello 값 `oid` 클레임입니다.  이 쿼리 hello Microsoft Graph와 같은 tooMicrosoft 온라인 서비스를 만들 때 사용할 수 있다는 것을 의미 합니다.  Microsoft Graph hello hello와이 ID를 반환 합니다 `id` 지정 된 사용자 계정에 대 한 속성.  때문에 hello `oid` 를 사용 하면 여러 앱 toocorrelate, hello `profile` 범위는 필요한 순서 tooreceive이이 클레임입니다. 사용자 한 명이 여러 테 넌 트에 있으면 hello 사용자는 각 테 넌 트에 다른 개체 ID 포함-서로 다른 계정으로 각 계정에 사용자가 hello hello 동일한 자격 증명 하는 경우에 간주 됩니다. |

### <a name="access-tokens"></a>액세스 토큰
현재 Microsoft 서비스에 의해서만 hello v2.0 끝점에서 발급 하는 액세스 토큰을 사용한 수 있습니다. 앱 필요는 없습니다 tooperform 모든 유효성 검사 또는 액세스 토큰에 대 한 검사 hello 현재 지원 시나리오에 대 한 합니다. 액세스 토큰을 완전 불투명으로 처리할 수 있습니다. 이들은 앱에서 HTTP 요청 tooMicrosoft를 통과할 수 정당한 문자열입니다.

Hello 미래 hello v2.0 근처에서 끝점 내의 다른 클라이언트에서 사용자가 앱 tooreceive 액세스 토큰에 대 한 hello 기능을 소개 합니다. 그 당시이 참조 항목의 hello 정보 앱 tooperform 액세스 토큰 유효성 검사 또는 기타 유사한 작업에 필요한 hello 정보로 업데이트 됩니다.

Hello v2.0 끝점에서 액세스 토큰을 요청할 때 hello v2.0 끝점에 대 한 앱 toouse hello 액세스 토큰에 대 한 메타 데이터도 반환 합니다. 이 정보에는 hello 액세스 토큰 및을 유효한 hello 범위 hello 만료 시간이 포함 됩니다. ऍ प ्이 메타 데이터 tooperform 지능형 토큰의 캐싱과 액세스 자체 tooparse 열려 hello 액세스 토큰이 필요 없이 합니다.

### <a name="refresh-tokens"></a>새로 고침 토큰
새로 고침 토큰은 보안 토큰을 앱 צ ְ ײ tooget 새 액세스는 OAuth 2.0 흐름 토큰입니다. 응용 프로그램 사용자를 대신 하 여 새로 고침 토큰 tooachieve 장기 액세스 tooresources를 사용 하 여 hello 사용자와 상호 작용 없이 수 있습니다.

새로 고침 토큰은 다중 리소스입니다. 액세스 토큰 tooa 완전히 다른 리소스에 대 한 하나의 리소스에 대 한 토큰 요청 중에 받은 새로 고침 토큰을 교환할 수 있습니다.

토큰 응답에서 새로 고침 tooreceive 응용 프로그램 요청 해야 하며 hello 부여할 `offline_acesss` 범위입니다. hello에 대 한 자세한 toolearn `offline_access` 범위 hello를 참조 하십시오 [동 및 범위](active-directory-v2-scopes.md) 문서.

새로 고침 토큰, 하며 항상, 완전히 불투명 tooyour 앱. 이러한 hello Azure AD v2.0 끝점에서 발급 한 및만 검사 하 고 수 hello v2.0 끝점에 의해 해석 합니다. 수명이 긴 하지만 앱 새로 고침 토큰은 특정 기간에 대 한 지속 됩니다 tooexpect 작성 합니다. 다양한 이유로 언제든지 새로 고침 토큰이 무효화될 수 있기 때문입니다. 새로 고침 토큰이 유효한 경우 응용 프로그램 tooknow 프로그램에 대 한 방법은 tooattempt tooredeem만 hello 토큰 요청 toohello v2.0 끝점 함으로써 것입니다.

새 액세스 토큰에 대 한 새로 고침 토큰을 교환할 때 (앱 허가 hello 경우 `offline_access` 범위)를 hello 토큰 응답에 새로운 새로 고침 토큰을 수신 합니다. 새로 발급 하는 hello 새로 고침 토큰, tooreplace hello 사용한 hello 요청에 저장 합니다. 이렇게 하면 새로 고침 토큰이 최대한 오랫동안 유효한 상태로 유지되도록 할 수 있습니다.

## <a name="validating-tokens"></a>토큰 유효성 검사
현재, 필요한 응용 프로그램에 토큰 유효성 검사만 hello tooperform의 유효성을 검사할 ID 토큰입니다. ID 토큰 toovalidate 앱 hello ID 토큰의 두 hello ID 토큰 서명 및 hello 클레임을 확인 해야 합니다.

<!-- TODO: Link -->
Microsoft은 라이브러리 및 tooeasily 토큰 유효성 검사를 처리 하는 방법을 보여 주는 코드 샘플을 제공 합니다. Hello 다음 섹션에서는 프로세스를 기본 hello에 설명 합니다. JWT 유효성 검사에 사용할 수 있는 여러 타사 오픈 소스 라이브러리도 있습니다. 거의 모든 플랫폼 및 언어에 대해 하나 이상의 옵션이 있습니다.

### <a name="validate-hello-signature"></a>Hello 서명 유효성 검사
Hello로 구분 되는 세 개의 세그먼트를 포함 하는 JWT `.` 문자입니다. 첫 번째 세그먼트 hello hello 라고 *헤더*, hello 두 번째 세그먼트는 hello *본문*, hello 세 번째 세그먼트는 hello 및 *서명*합니다. 앱에서 신뢰할 수 있도록 hello 서명 세그먼트 hello ID 토큰의 사용된 toovalidate hello 신뢰성을 수 있습니다.

ID 토큰은 RSA 256 등의 업계 표준 비대칭 암호화 알고리즘을 사용하여 서명됩니다. hello hello ID 토큰의 헤더에 대 한 정보가 hello 키 및 암호화 방법을 toosign hello 토큰을 사용 합니다. 예:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

hello `alg` 클레임 토큰이 사용 되는 toosign hello hello 알고리즘을 나타냅니다. hello `kid` hello 공개 키 토큰이 사용 되는 toosign hello를 나타냅니다.

언제 든 지 hello v2.0 끝점 공개-개인 키 쌍의 특정 집합 중 하나를 사용 하 여 ID 토큰에 서명할 수도 있습니다. hello v2.0 끝점 앱 작성 toohandle 해당 키를 자동으로 변경 해야 하므로 hello 가능한 개수를 키를 정기적으로 회전 시킵니다. Hello v2.0 끝점에서 사용 되는 업데이트 toohello 공개 키에 대 한 적절 한 주파수 toocheck 매 24 시간입니다.

Hello OpenID Connect 메타 데이터 문서에 있는 사용 하 여 toovalidate hello 서명 해야 하는 키 데이터에 서명 하는 hello를 얻을 수 있습니다.

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> 브라우저에서 URL hello 보세요!
>
>

이 메타 데이터 문서는 hello OpenID Connect 인증에 필요한 다양 한 끝점의 hello 위치와 같은 여러 가지 유용한 정보를가 하는 JSON 개체입니다.  hello 문서도 포함 되어는 *jwks_uri*, toosign 토큰에 사용 되는 공개 키의 hello 설정 hello 위치를 제공 하는 합니다. hello JSON 문서 hello jwks_uri에 있는 모든 hello 공개 키 정보를 현재 사용 중인에 있습니다. 앱 hello צ ְ ײ `kid` hello JWT 헤더 tooselect이이 문서에는 공개 키를 사용 하는 toosign 되었습니다에서 토큰 클레임입니다. Hello 올바른 공개 키와 hello 표시 된 알고리즘을 사용 하 여 서명 유효성 검사를 수행 합니다.

서명 유효성 검사를 수행 하는 것은이 문서의 외부 hello 범위입니다. 여러 오픈 소스 라이브러리를 사용할 수 있는 toohelp이 있습니다.

### <a name="validate-hello-claims"></a>Hello 클레임의 유효성 검사
앱 사용자 로그인 시 ID 토큰을 받으면 hello ID 토큰에서 hello 클레임에 대 한 몇 가지 검사를 수행 해야 것입니다. 포함하지만 다음과 같이 제한되지 않습니다.

* **대상 그룹** 클레임 ID 토큰 hello tooverify가 의도 한 toobe tooyour 앱 제공
* **날짜부터** 및 **만료 시간** 클레임 ID 토큰 hello tooverify가 만료 되지 않았습니다
* **발급자** 클레임, 토큰 hello tooverify에서 발급 한 tooyour 앱 hello v2.0 끝점
* **nonce** - 토큰 재생 공격 완화로 사용됩니다.

응용 프로그램에서 수행 해야 하는 클레임 유효성 검사의 전체 목록을 참조 hello [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)합니다.

이러한 클레임에 대 한 hello 예상 값의 세부 정보는 hello에 포함 된 [ID 토큰](# ID tokens) 섹션.

## <a name="token-lifetimes"></a>토큰 수명
다음 토큰 수명 정보 제공 용 hello를 제공 합니다. hello 정보는 개발 하 고 응용 프로그램을 디버깅 도움이 될 수 있습니다. 앱 되어서는 안 이러한 수명 tooremain 상수 중 tooexpect을 기록 합니다. 토큰 수명은 언제든지 변경될 수 있고 변경됩니다.

| 위임 | 수명 | 설명 |
| --- | --- | --- |
| ID 토큰(회사 또는 학교 계정) |1시간 |ID 토큰은 일반적으로 1시간 동안 유효합니다. 웹 앱은 자체 세션 (권장) hello 사용자와 선택할 수 있습니다 완전히 다른 세션 수명 동안 동일한 수명 toomaintain이 사용할 수 있습니다. 앱 tooget 새 ID 토큰을 필요한 경우 새 로그인 toomake 요청 권한 부여 끝점 toohello v2.0 필요 합니다. Hello 사용자 않을 수도 있습니다 hello 사용자 hello v2.0 끝점이 포함 된 유효한 브라우저 세션이 있으면 필요한 tooenter 자격 증명을 다시 수 있습니다. |
| ID 토큰(개인 계정) |24시간 |개인 계정에 대한 ID 토큰은 일반적으로 24시간 동안 유효합니다. 웹 앱은 자체 세션 (권장) hello 사용자와 선택할 수 있습니다 완전히 다른 세션 수명 동안 동일한 수명 toomaintain이 사용할 수 있습니다. 앱 tooget 새 ID 토큰을 필요한 경우 새 로그인 toomake 요청 권한 부여 끝점 toohello v2.0 필요 합니다. Hello 사용자 않을 수도 있습니다 hello 사용자 hello v2.0 끝점이 포함 된 유효한 브라우저 세션이 있으면 필요한 tooenter 자격 증명을 다시 수 있습니다. |
| 액세스 토큰(회사 또는 학교 계정) |1시간 |Hello 토큰 메타 데이터의 일부로 토큰 응답에 나와 있습니다. |
| 액세스 토큰(개인 계정) |1시간 |Hello 토큰 메타 데이터의 일부로 토큰 응답에 나와 있습니다. 개인 계정 대신 발급된 액세스 토큰은 다른 수명으로 구성할 수도 있지만 1시간이 일반적입니다. |
| 새로 고침 토큰(회사 또는 학교 계정) |Too14 일 수를 |단일 새로 고침 토큰이 최대 14일 동안 유효합니다. 그러나 앱 새로운 새로 고침 토큰으로 대체 될 때까지 또는 실패할 때까지 앱 tootry toouse 새로 고침 토큰을 계속 해야 하므로 hello 새로 고침 토큰 언제 든 지 여러 가지 이유로 잘못 될 수 있습니다. 또한 새로 고침 토큰 hello 사용자가 자격 증명을 입력 한 후 90 일 경과 된 경우에 잘못 됩니다. |
| 새로 고침 토큰(개인 계정) |Too1 연도를 |단일 새로 고침 토큰이 최대 1년 동안 유효합니다. 그러나 hello 새로 고침 토큰을 사용할 수 없게 언제 든 지 여러 가지 이유로, 될 때까지 새로 고침 토큰에 실패 하면 되므로 앱 tootry toouse 계속 해야 합니다. |
| 권한 부여 코드(회사 또는 학교 계정) |10분 |권한 부여 코드는 의도적으로 수명이 짧으므로 hello 토큰을 받을 때 액세스 토큰 및 새로 고침 토큰에 대 한 즉시 사용 해야 합니다. |
| 권한 부여 코드(개인 계정) |5분 |권한 부여 코드는 의도적으로 수명이 짧으므로 hello 토큰을 받을 때 액세스 토큰 및 새로 고침 토큰에 대 한 즉시 사용 해야 합니다. 개인 계정 대신 발급된 권한 부여 코드는 일회용으로 사용됩니다. |
