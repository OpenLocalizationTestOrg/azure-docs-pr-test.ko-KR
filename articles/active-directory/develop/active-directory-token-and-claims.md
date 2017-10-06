---
title: "hello 다른 토큰 및 클레임 유형 Azure AD에서 지 원하는 대해서 aaaLearn | Microsoft Docs"
description: "이해 및 평가 hello SAML 2.0 및에서 Azure Active Directory (AAD)를 발급 하는 JSON 웹 토큰 (JWT) 토큰의 클레임을 hello에 대 한 가이드"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Azure AD 토큰 참조
Azure Active Directory (Azure AD) 여러 유형의 각 인증 흐름의 hello 처리의 보안 토큰을 내보냅니다. 이 문서에서는 hello 형식, 보안 특성 및 각 유형의 토큰의 내용을 설명 합니다.

## <a name="types-of-tokens"></a>토큰 형식
Azure AD에서는 hello 지원 [OAuth 2.0 권한 부여 프로토콜](active-directory-protocols-oauth-code.md)를 사용 하는 access_tokens와 refresh_tokens 합니다.  또한 인증 및 로그인을 통해 지원 [OpenID Connect](active-directory-protocols-openid-connect-code.md), 세 번째 유형의 토큰을 hello id_token 도입 합니다.  이러한 토큰은 각각 "전달자 토큰"으로 표시됩니다.

전달자 토큰은 보호 된 리소스를 부여 "전달자" 액세스 tooa hello 하는 경량 보안 토큰입니다. 이 전반에 "bearer" hello hello 토큰을 제공할 수 있는 당사자입니다. Azure ad는 인증에 필요 하지만 tooreceive 전달자 토큰을 요청, 단계를 수행 해야 toosecure hello 토큰, tooprevent 인터 셉 션 의도 하지 않은 당사자가 있습니다. 전달자 토큰을 사용 하 여 기본 제공 메커니즘 tooprevent 권한이 없는 당사자 없으므로 전송 계층 보안 (HTTPS)와 같은 보안 채널에서 전송 해야 합니다. 전달자 토큰 지우기 hello에 전송 되기 매뉴얼에 hello 중간 공격의 사용된 tooacquire hello 토큰 수 있으며이 무단된 액세스 tooa 보호 된 리소스를 얻을 수 있습니다. hello 저장 하거나 나중에 사용 하기 위해 전달자 토큰을 캐시 하는 경우 동일한 보안 원칙이 적용 됩니다. 항상 앱이 안전한 방식으로 전달자 토큰을 전송하고 저장하도록 합니다. 전달자 토큰의 보안 고려 사항을 자세히 알아보려면 [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750)를 참조하세요.

다양 한 Azure AD에서 발급 한 hello 토큰 JSON 웹 토큰 또는 Jwt로 구현 됩니다.  JWT는 두 요소 간에 정보를 전송하는 URL로부터 안전한 간단한 수단입니다.  Jwt에 포함 된 hello 정보 hello 전달자 및 hello 토큰의 주체에 대 한 한 정보 어설션 또는 "클레임"으로 알려져 있습니다.  Jwt의 hello 클레임은 JSON 개체 인코딩되고 전송을 위해 serialize 합니다.  Azure AD에서 발급 하는 hello Jwt는 서명 되었지만 암호화 되지, 이후 디버깅을 위해 JWT의 hello 내용의 쉽게 검사할 수 있습니다.  [jwt.calebb.net](http://jwt.calebb.net)등 이러한 작업에 사용할 수 있는 여러 도구가 있습니다. Jwt에 대 한 자세한 내용은 toohello를 참조할 수 있습니다 [JWT 사양의](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)합니다.

## <a name="idtokens"></a>Id_tokens
id_token은 [OpenID Connect](active-directory-protocols-openid-connect-code.md)를 사용하여 인증을 수행할 때 앱이 받는 로그인 보안 토큰의 한 형태입니다.  으로 표현 됩니다 [Jwt](#types-of-tokens), 응용 프로그램에 hello 사용자를 로그인에 사용할 수 있는 클레임을 포함 합니다.  계정 정보를 표시 하거나 응용 프로그램의 액세스 제어 결정에 사용 되는 일반적으로 나타나며로 id_token에 hello 클레임을 사용할 수 있습니다.

지금은 Id_token이 서명되었지만 암호화되지 않았습니다.  앱 프로그램 id_token를 받으면 다음 조건을 충족 해야 [hello 서명 유효성 검사](#validating-tokens) tooprove 토큰의 신뢰성을 hello 및 값이 유효한 토큰 tooprove hello에에서 몇 가지 클레임 유효성을 검사 합니다.  hello 응용 프로그램에서 유효성을 검사 하는 클레임 시나리오 요구 사항에 따라 다르지만 일부 [일반 클레임 유효성 검사](#validating-tokens) 앱 모든 시나리오에서 수행 해야 하는 합니다.

Hello 샘플 id_token: id_tokens 클레임에 다음 정보에 대 한 단원을 참조 하십시오.  Hello 클레임 id_tokens에서 특정 순서로 반환 되지 않습니다는 참고 사항  또한 언제든지 id_token에 새 클레임이 도입될 수 있으므로 새 클레임이 도입될 때 앱이 손상되지 않아야 합니다.  hello 다음 목록에 포함 되어 앱이이 작성 hello 시점에 안정적으로 해석할 수 있는 hello 클레임입니다.  하는 경우 필요에 따라 더 많은 세부 정보에서에서 확인할 수 있습니다 hello [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html)합니다.

#### <a name="sample-idtoken"></a>샘플 id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> 연습에 붙여 넣어 하 여 hello 샘플 id_token의 hello 클레임을 검사를 시도 [calebb.net](http://jwt.calebb.net)합니다.
> 
> 

#### <a name="claims-in-idtokens"></a>id_token의 클레임
> [!div class="mx-codeBreakAll"]
| JWT 클레임 | Name | 설명 |
| --- | --- | --- |
| `appid` |응용 프로그램 UI |Hello 토큰 tooaccess 리소스를 사용 하는 hello 응용 프로그램을 식별 합니다. hello 응용 프로그램은 자체적으로 또는 사용자를 대신 하 여 작동할 수 있습니다. hello 응용 프로그램 ID를 일반적으로 응용 프로그램 개체를 나타내지만 Azure AD에서 서비스 사용자 개체를 나타낼 수도 있습니다. <br><br> **JWT 값 예제**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |대상 |hello는 hello 토큰의 올바른 받는 것입니다. hello 토큰을 수신 하는 hello 응용 프로그램 hello 대상 그룹 값이 올바른지와 다른 대상 그룹을 위한 토큰을 거부 있는지 확인 해야 합니다. <br><br> **SAML 값 예제**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **JWT 값 예제**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |응용 프로그램 인증 컨텍스트 클래스 참조 |Hello 클라이언트 인증 된 방법을 나타냅니다. 공용 클라이언트 hello 값은 0입니다. 클라이언트 ID 및 클라이언트 암호를 사용 하는 경우 hello 값은 1입니다. <br><br> **JWT 값 예제**: <br> `"appidacr": "0"` |
| `acr` |인증 컨텍스트 클래스 참조 |Hello 응용 프로그램 인증 컨텍스트 클래스 참조 클레임에 대 한 것과 반대로 toohello 클라이언트로으로 hello 주체가 인증 된는 방법을 나타냅니다. 값이 "0" hello 최종 사용자 인증이 ISO/IEC 29115의 hello 요구 사항을 충족 하지 않는 것을 나타냅니다. <br><br> **JWT 값 예제**: <br> `"acr": "0"` |
| 인증 인스턴트 |레코드에는 날짜 및 인증 발생 했을 때 hello 합니다. <br><br> **SAML 값 예제**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |인증 방법 |Hello 토큰의 주체 hello 인증 된 방법을 식별 합니다. <br><br> **SAML 값 예제**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **JWT 값 예제**: `“amr”: ["pwd"]` |
| `given_name` |이름 |Hello Azure AD 사용자 개체에 설정 된 대로 먼저 또는 "지정 된" hello 사용자의 이름 hello를 제공합니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **JWT 값 예제**: <br> `"given_name": "Frank"` |
| `groups` |그룹 |Hello 주체의 그룹 멤버 자격을 나타내는 개체 Id를 제공 합니다. 이러한 값이 고유 (개체 ID 참조) 되어 권한 부여 tooaccess 리소스를 적용 하는 등의 액세스를 관리 하기 위한 안전 하 게 사용할 수 있습니다. hello 그룹 클레임에 포함 된 hello 그룹 hello 응용 프로그램 매니페스트의 "groupMembershipClaims" 속성 hello 통해 응용 프로그램 단위 별로 구성 됩니다. Null 값은 모든 그룹을 제외하고, "SecurityGroup" 값은 Active Directory 보안 그룹 멤버 자격만 포함하고, "All" 값은 보안 그룹과 Office 365 메일 그룹을 모두 포함합니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **JWT 값 예제**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |ID 공급자 |Hello 토큰의 hello 주체를 인증 하는 레코드 hello id 공급자입니다. 이 값은 동일한 toohello hello hello 사용자 계정을 hello 발급자는 다른 테 넌 트에 있지 않으면 발급자 클레임 값입니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **JWT 값 예제**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Hello는 hello 토큰 발급 된 시간을 저장 합니다. 것이 사용 되는 toomeasure 토큰 새로 고침입니다. <br><br> **SAML 값 예제**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **JWT 값 예제**: <br> `"iat": 1390234181` |
| `iss` |발급자 |Hello 보안 토큰 서비스 (STS)를 생성 하 고 hello 토큰을 반환 하는 식별 합니다. Azure AD에서 반환 하는 hello 토큰, hello 발급자는 sts.windows.net입니다. hello GUID hello 발급자 클레임 값에는 hello Azure AD 디렉터리의 hello 테 넌 트 ID입니다. hello 테 넌 트 ID는 hello 디렉터리의 사용 되는 신뢰할 수 있는 변경할 수 없는 식별자입니다. <br><br> **SAML 값 예제**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **JWT 값 예제**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |성 |Hello Azure AD 사용자 개체에 정의 된 hello 마지막 이름, 성 또는 hello 사용자의 성을 제공 합니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **JWT 값 예제**: <br> `"family_name": "Miller"` |
| `unique_name` |이름 |Hello 토큰의 hello 주체를 식별 하는 사람이 읽을 수 있는 값을 제공 합니다. 이 값은 정확 하지 toobe 테 넌 트 내에서 고유 않으며 설계 된 toobe 표시 용도로 사용 됩니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **JWT 값 예제**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |개체 ID |Azure AD 개체의 고유 식별자를 포함합니다. 이 값은 변경할 수 없으며 재할당 또는 재사용할 수 없습니다. 쿼리 tooAzure AD에서에서 hello 개체 ID tooidentify 개체를 사용 합니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **JWT 값 예제**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |역할 |액세스 제어를 받는 hello 하는 모든 응용 프로그램 역할 그룹 멤버 자격을 통해 직접 / 간접적으로 부여 된 및 역할 기반 사용된 tooenforce 수를 나타냅니다. Hello 통해 응용 프로그램 별로 응용 프로그램 역할을 정의 `appRoles` hello 응용 프로그램 매니페스트의 속성입니다. hello `value` 각 응용 프로그램 역할의 속성은 hello 역할 클레임에 표시 되는 hello 값입니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **JWT 값 예제**: <br> `“roles”: ["Admin", … ]` |
| `scp` |범위 |Hello 가장 권한이 부여 된 toohello 클라이언트 응용 프로그램을 나타냅니다. hello 기본 권한은 `user_impersonation`합니다. 리소스를 보호 하는 hello hello 소유자는 Azure AD에 추가 값을 등록할 수 있습니다. <br><br> **JWT 값 예제**: <br> `"scp": "user_impersonation"` |
| `sub` |제목 |Hello 보안 주체는 hello에 대 한 토큰 어설션 응용 프로그램의 hello 사용자 등의 정보를 식별 합니다. 이 값은 변경할 수 없습니다 및 할당할 수 없습니다 또는 계속 사용 하므로 것이 권한 부여 확인을 사용 하는 tooperform 안전 하 게 합니다. Hello 주체는 항상에 있기 때문에 hello hello Azure AD에서 발급 토큰, 범용 권한 부여 시스템에서이 값을 사용 하는 것이 좋습니다. <br> `SubjectConfirmation` 클레임이 아닙니다. Hello 토큰의 주체 hello 확인 하는 방법을 설명 합니다. `Bearer`hello 제목 hello 토큰 소유 여부를 통해 확인 나타냅니다. <br><br> **SAML 값 예제**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **JWT 값 예제**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |테넌트 ID |Hello 토큰을 발급 한 hello 디렉터리 테 넌 트를 식별 하는 변경할 수 없는, 비-다시 사용할 수 있는 식별자입니다. 다중 테 넌 트 응용 프로그램에서이 값 tooaccess 테 넌 트 별 디렉터리 리소스를 사용할 수 있습니다. 예를 들어 호출 toohello Graph API에서에서이 값 tooidentify hello 테 넌 트를 사용할 수 있습니다. <br><br> **SAML 값 예제**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **JWT 값 예제**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |토큰 수명 |Hello 유효한 시간 간격을 토큰을 정의 합니다. hello 토큰의 유효성을 검사 하는 hello 서비스는 hello hello 토큰 수명, 다른 hello 토큰을 거부 해야 내인지 현재 날짜를 확인 해야 합니다. hello 서비스 수에 대 한 hello 토큰 수명 범위 tooaccount toofive 분까지 시계 시간 ("시간 불일치")에서 모든 차이점에 대 한를 Azure AD 간의 및 hello 서비스입니다. <br><br> **SAML 값 예제**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **JWT 값 예제**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |사용자 계정 이름 |저장소 hello hello 사용자 계정이의 사용자 이름입니다.<br><br> **JWT 값 예제**: <br> `"upn": frankm@contoso.com` |
| `ver` |버전 |Hello 토큰의 hello 버전 번호를 저장합니다. <br><br> **JWT 값 예제**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>액세스 토큰
인증 성공 시 Azure AD 액세스 토큰을 사용 하는 tooaccess 보호 된 리소스 수를 반환 합니다. hello 액세스 토큰이 base 64 인코딩 JSON 웹 토큰 (JWT) 및 디코더를 통해 실행 하 여 해당 내용을 검사할 수 있습니다.

하는 경우 앱에만 *사용 하 여* 액세스 토큰 tooget 액세스 tooAPIs, 있습니다 수 (및 해야) 액세스 토큰으로 처리 완전히 불투명-는 앱에서 HTTP 요청 tooresources를 전달할 수 있는 정당한 문자열입니다.

액세스 토큰을 요청 하는 경우 Azure AD 응용 프로그램의 사용에 대 한 hello 액세스 토큰에 대 한 몇 가지 메타 데이터도 반환 합니다.  이 정보에는 hello 액세스 토큰 및을 유효한 hello 범위 hello 만료 시간이 포함 됩니다.  그러면 앱 tooperform tooparse 자체 hello 액세스 토큰을 열 필요 없이 액세스 토큰의 캐싱과 지능형 있습니다.

HTTP 요청에서 액세스 토큰을 필요로 하는 Azure AD로 보호 되는 API 앱을 사용 하는 경우 다음 수행 해야 유효성 검사 및 표시 하는 hello 토큰의 검사 합니다. 앱은 tooaccess 리소스를 사용 하기 전에 hello 액세스 토큰의 유효성 검사를 수행 해야 합니다. 유효성 검사에 대한 자세한 내용은 [토큰 유효성 검사](#validating-tokens)를 참조하세요.  
Toodo.net이 참조에 대 한 내용은 [Azure AD에서 전달자 토큰을 사용 하 여 Web API 보호](active-directory-devquickstarts-webapi-dotnet.md)합니다.

## <a name="refresh-tokens"></a>새로 고침 토큰

새로 고침 토큰은 응용 프로그램에서 사용할 수 있는 보안 토큰 tooacquire 새로운 액세스는 OAuth 2.0 흐름 토큰입니다.  사용자를 대신 하 여 응용 프로그램 tooachieve 장기 액세스 tooresources를 hello 사용자 상호 작용 없이 있습니다.

새로 고침 토큰은 다중 리소스입니다.  새로 고침 토큰 액세스 토큰 tooa 완전히 다른 리소스에 대 한 하나의 자원만 회수할 수에 대 한 토큰 요청 중에 받은 toosay입니다. toodo이, 집합 hello `resource` hello 요청 toohello에서 매개 변수 대상 리소스를 지정 합니다.

새로 고침 토큰은 완전히 불투명 tooyour 앱. 수명이 긴 하지만 앱 새로 고침 토큰은 특정 기간에 대 한 지속 됩니다 tooexpect 작성 합니다.  다양한 이유로 언제든지 새로 고침 토큰이 무효화될 수 있기 때문입니다.  새로 고침 토큰이 유효한 경우 응용 프로그램 tooknow 프로그램에 대 한 방법은 tooattempt tooredeem만 hello 토큰 요청 tooAzure AD 토큰 끝점 함으로써 것입니다.

새 액세스 토큰에 대 한 새로 고침 토큰을 교환할 때 hello 토큰 응답에 새 새로 고침 토큰을 받습니다.  Hello hello 요청에 사용 되는 대체 새로 발급 하는 hello 새로 고침 토큰을 저장 해야 합니다.  이렇게 하면 새로 고침 토큰이 최대한 오랫동안 유효한 상태로 유지됩니다.

## <a name="validating-tokens"></a>토큰 유효성 검사

순서 toovalidate id_token 또는 access_token 응용 프로그램 서명 및 hello 클레임을 모두 hello 토큰의 유효성을 검사 해야 합니다. 순서 toovalidate 액세스 토큰이 앱 hello 여러 hello 조건 및 토큰을 서명 하는 hello 확인 해야 합니다. 이러한 toobe hello OpenID 검색 문서에서 hello 값에 대해 유효성을 검사 해야 합니다. 예를 들어 hello 테 넌 트 독립적 버전의 hello 문서에 위치한 [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration)합니다. Azure AD 미들웨어 액세스 토큰의 유효성 검사에 대 한 기본 제공 기능을가지고 있으며 탐색할 수 있습니다이 [샘플](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind 하나 hello 언어를 선택 합니다. Tooexplicitly JWT 토큰을 확인 하는 방법에 대 한 자세한 내용은 hello를 참조 하십시오 [수동 JWT 유효성 검사 샘플](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation)합니다.  

라이브러리 및 tooeasily 토큰 유효성 검사 기능을 처리 하는 방법을 보여 주는 코드 예제가 제공 아래 정보는 hello 단순히 ´ ë ç toounderstand hello 프로세스 내부에 원하는 사용자에 게 합니다.  JWT 유효성 검사에 사용할 수 있는 여러 타사 오픈 소스 라이브러리도 있습니다. 거의 모든 플랫폼 및 언어에 대해 옵션이 하나 이상 있습니다. Azure AD 인증 라이브러리 및 코드 샘플에 대한 자세한 내용은 [Azure AD 인증 라이브러리](active-directory-authentication-libraries.md)를 참조하세요.

#### <a name="validating-hello-signature"></a>Hello 서명의 유효성을 검사

Hello로 구분 되는 세 개의 세그먼트를 포함 하는 JWT `.` 문자입니다.  hello 첫 번째 세그먼트 hello 라고 **헤더**, hello로 두 번째 hello **본문**, 및 hello로 세 번째 hello **서명**합니다.  앱에서 신뢰할 수 있도록 hello 서명 세그먼트 hello 토큰의 사용된 toovalidate hello 신뢰성을 수 있습니다.

Azure AD에서 발급된 토큰은 RSA 256 등의 업계 표준 비대칭 암호화 알고리즘을 사용하여 서명됩니다. hello JWT의 hello 헤더 hello 키에 대 한 정보를 포함 하 고 toosign hello 토큰을 사용 하는 암호화 방법.

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

hello `alg` hello 하는 동안 사용 되는 toosign hello 토큰 했던 hello 알고리즘 나타냅니다 `x5t` 클레임 hello 특정 공개 키를 사용 하는 toosign hello 토큰을 나타냅니다.

특정 시점에 Azure AD는 공개-개인 키 쌍의 특정 집합 중 하나를 사용하여 id_token에 서명할 수 있습니다. Azure AD 앱에 이러한 키를 자동으로 변경 toohandle 작성 해야 하므로 hello 가능한 키 집합을 정기적으로 회전 합니다.  Azure AD에서 사용 되는 업데이트 toohello 공개 키에 대 한 적절 한 주파수 toocheck 매 24 시간입니다.

Hello OpenID Connect 메타 데이터 문서에 있는 사용 하 여 필요한 toovalidate hello 서명 키 데이터를 서명 하는 hello를 얻을 수 있습니다.

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> 브라우저에서 이 URL을 사용해 보세요!
> 
> 

이 메타 데이터 문서는 몇 가지 유용한 hello OpenID Connect 인증을 수행 하는 데 필요한 다양 한 끝점의 hello 위치와 같은 정보를 포함 하는 JSON 개체입니다.  

또한 포함 한 `jwks_uri`, toosign 토큰에 사용 되는 공개 키의 hello 설정 hello 위치를 제공 하는 합니다.  hello에 있는 hello JSON 문서 `jwks_uri` 모든 해당 특정 시점에 사용 중인 hello 공개 키 정보를 포함 합니다.  앱 hello צ ְ ײ `kid` hello JWT 헤더 tooselect이이 문서에는 공개 키를 사용 하는 toosign 되었습니다에서 특정 토큰 클레임입니다.  Hello 올바른 공개 키와 hello 표시 된 알고리즘을 사용 하 여 서명 유효성 검사를 수행한 다음 수 있습니다.

서명 유효성 검사를 수행 합니다.이 문서의 외부 hello 범위-는 필요한 경우 이렇게 하는 데 사용할 수 있는 여러 오픈 소스 라이브러리입니다.

#### <a name="validating-hello-claims"></a>Hello 클레임 유효성 검사

앱 (사용자 로그인 시 id_token 또는 hello HTTP 요청에서 전달자 토큰으로 액세스 토큰) 토큰을 수신 하는 경우 hello 토큰에서 클레임 hello에 대 한 몇 가지 검사를 수행 해야 것입니다.  포함하지만 다음과 같이 제한되지 않습니다.

* hello **Audience** 클레임-토큰 hello tooverify가 의도 한 toobe tooyour 응용 프로그램을 제공 합니다.
* hello **날짜부터** 및 **만료 시간** 클레임-토큰 hello tooverify 만료 되지 않았습니다.
* hello **발급자** 클레임-Azure AD에서 토큰 hello tooverify tooyour 앱을 실제로 발급 되었습니다.
* hello **Nonce** -toomitigate 토큰 재생 공격입니다.
* 공유할 수 있습니다.

ID 토큰에 대 한 응용 프로그램을 수행 해야 하는 클레임 유효성 검사 목록은 전체 참조 toohello [OpenID Connect 사양](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)합니다. 이러한 클레임에 대 한 hello 예상 값의 세부 정보는 hello 앞에 포함 된 [id_token 섹션](#id-tokens) 섹션.

## <a name="sample-tokens"></a>샘플 토큰

이 섹션에서는 Azure AD가 반환하는 SAML 및 JWT 토큰 샘플을 보여 줍니다. 이러한 샘플 컨텍스트에서 hello 클레임을 볼 수 있습니다.

### <a name="saml-token"></a>SAML 토큰

다음은 일반적인 SAML 토큰 샘플입니다.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>JWT 토큰 - 사용자 가장
다음은 권한 부여 코드 부여 흐름에 사용되는 일반적인 JWT(JSON 웹 토큰) 샘플입니다.
또한 tooclaims hello 토큰의 버전 번호가 포함 됩니다. **ver** 및 **appidacr**, hello 인증 컨텍스트 클래스 참조 hello 클라이언트 인증 된 방법을 나타냅니다. 공용 클라이언트 hello 값은 0입니다. 클라이언트 ID 및 클라이언트 암호 사용 된 경우 hello 값은 1입니다.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>관련 콘텐츠
* Hello Azure AD 그래프를 참조 하십시오. [정책 작업](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) 및 hello [정책 엔터티에](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn hello Azure AD Graph API 통해 토큰 수명 정책을 관리 하는 방법에 대 한 자세한 합니다.
* 자세한 내용과 예제를 포함하여, PowerShell cmdlet를 통한 정책 관리 방법에 대한 샘플은 [Azure AD에서 구성 가능한 토큰 수명](../active-directory-configurable-token-lifetimes.md)을 참조하십시오. 
