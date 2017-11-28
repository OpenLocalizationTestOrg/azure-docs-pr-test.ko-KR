---
title: "Azure AD v 2.0에서 지 원하는 hello 권한 부여 프로토콜에 대 한 aaaLearn | Microsoft Docs"
description: "Hello Azure AD v2.0 끝점에서 지 원하는 가이드 tooprotocols 합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# v2.0 프로토콜 - OAuth 2.0 및 OpenID Connect
hello v2.0 끝점 identity로-서비스 업계 표준 프로토콜을 OAuth 2.0 및 OpenID Connect 사용에 대 한 Azure AD에서 사용할 수 있습니다.  Hello 서비스 표준 호환 상태인 동안 미세한 차이로 이러한 프로토콜의 모든 두 구현이 있을 수 있습니다.  여기에 hello 정보를 직접 보내서 toowrite 코드 선택 & 우리의 오픈 소스 라이브러리 중 하나를 사용 하지 않고 소스 라이브러리를 열고 HTTP 요청 또는 세 번째 서비스로 사용 하 여 당사자를 처리 하는 경우 도움이 됩니다.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>
>

## hello 기본 사항
거의 모든 OAuth 및 OpenID Connect 흐름에는 4 자 hello 교환에 관련 된

![OAuth 2.0 역할](../../media/active-directory-v2-flows/protocols_roles.png)

* hello **권한 부여 서버** hello v2.0 끝점입니다.  이 hello 사용자의 id를 확인, 부여 및 액세스 tooresources 해지 및 토큰을 발급 하는 일을 담당 합니다.  Hello id 공급자는 라고도-안전 하 게 처리 아무 것도 hello 사용자의 정보, 해당 액세스 및는 흐름에서 파티 간의 트러스트 관계 hello와 toodo 합니다.
* hello **리소스 소유자** hello 최종 사용자는 일반적으로 합니다.  Hello 파티 hello 데이터를 소유 하 고 hello 전원 tooallow에는 타사 tooaccess 해당 데이터 또는 리소스 이며
* hello **OAuth 클라이언트** 응용 프로그램은 응용 프로그램 id로 식별 되는  이 일반적으로 hello 파티 hello 최종 사용자 상호 작용 하 고 hello 권한 부여 서버에서 토큰을 요청 합니다.  hello 부여 받아야 합니다 권한 tooaccess hello 리소스 hello 리소스 소유자가 있습니다.
* hello **리소스 서버** hello 리소스 또는 데이터가 상주 합니다.  Hello toosecurely 인증 하 고 hello OAuth 클라이언트에 권한을 부여 하는 권한 부여 서버를 신뢰 하 고 tooa 리소스에 액세스 하는 access_tokens tooensure 마스터인 전달자를 사용 하 여 합니다.

## 앱 등록
Hello v2.0 끝점을 사용 하는 모든 응용 프로그램에 등록 된 toobe 필요 합니다 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 전에 OAuth 또는 OpenID Connect를 사용 하 여 상호 작용할 수 있습니다.  hello 응용 프로그램 등록 프로세스는 수집 및 몇 가지 값 tooyour 앱 할당:

* 앱을 고유하게 식별하는 **응용 프로그램 ID**
* A **리디렉션 URI** 또는 **패키지 식별자** 사용된 toodirect 응답 백 tooyour 앱 일 수 있는
* 다른 몇 가지 시나리오 관련 값.

자세한 내용은 자세한 방법을 너무[앱을 등록](active-directory-v2-app-registration.md)합니다.

## 끝점
등록 되 면 hello 앱 toohello v2.0 끝점 요청을 전송 하 여 Azure AD와 통신 합니다.

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

여기서 hello `{tenant}` 네 개의 서로 다른 값 중 하나를 수행 합니다.

| 값 | 설명 |
| --- | --- |
| `common` |Hello 응용 프로그램으로 사용자가 개인 Microsoft 계정 및 Azure Active Directory toosign에서 작업/학교 계정을 둘 다를 수 있습니다. |
| `organizations` |Hello 응용 프로그램으로 Azure Active Directory toosign에서 작업/학교 계정이 있는 사용자를을 수 있습니다. |
| `consumers` |Hello 응용 프로그램으로 개인 Microsoft 계정 (MSA) toosign 있는 사용자를을 수 있습니다. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 또는 `contoso.onmicrosoft.com` |Hello 응용 프로그램에 특정 Azure Active Directory 테 넌 트 toosign에서 작업/학교 계정이 있는 사용자만을 허용 합니다.  도메인 이름이 hello hello Azure AD 테 넌 트 또는 hello 테 넌 트의 guid 식별자를 사용할 수 있습니다. |

방법에 대 한 자세한 내용은 이러한 끝점과 toointeract 아래 특정 응용 프로그램 종류를 선택 합니다.

## 토큰
OAuth 2.0 및 OpenID Connect hello v2.0 구현 Jwt로 대표 되는 전달자 토큰을 포함 하 여 전달자 토큰을 광범위 하 게 사용 하 게 합니다. 전달자 토큰은 보호 된 리소스를 부여 "전달자" 액세스 tooa hello 하는 경량 보안 토큰입니다. 이 전반에 "bearer" hello hello 토큰을 제공할 수 있는 당사자입니다. 파티 먼저 Azure AD tooreceive hello bearer 토큰으로 인증 hello 필요한 단계는 전송 및 저장에서 toosecure hello 토큰을 따르지 않은 경우, 있지만 차단 하 고 의도 하지 않은 당사자에서 사용 하는 수 있습니다. 일부 보안 토큰에는 권한 없는 당사자가 사용하는 것을 방지하는 기본 제공 메커니즘이 있지만, 전달자 토큰에는 이러한 메커니즘이 없으므로 전송 계층 보안(HTTPS)과 같은 보안 채널에서 전달자 토큰을 전송해야 합니다. 전달자 토큰 지우기 hello에 전송 되기 매뉴얼에 hello 중간 공격 악의적인 당사자 tooacquire hello 토큰에서 사용할 수 있습니다 하 고 사용 하 여 무단된 액세스 tooa 보호 된 리소스에 대 한 합니다. hello 저장 하거나 나중에 사용 하기 위해 전달자 토큰을 캐시 하는 경우 동일한 보안 원칙이 적용 됩니다. 항상 앱이 안전한 방식으로 전달자 토큰을 전송하고 저장하도록 합니다. 전달자 토큰의 보안 고려 사항을 자세히 알아보려면 [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750)를 참조하세요.

다양 한 유형의 hello v2.0 끝점에 사용 되는 토큰에 대 한 자세한 내용은 영어로 [v2.0 끝점 토큰 참조를 hello](active-directory-v2-tokens.md)합니다.

## 프로토콜
준비 toosee hello 아래 자습서 중 하나 시작, 몇 가지 예를 요청 하는 경우.  각 하나 해당 tooa 특정 인증 시나리오.  도움말 있습니다에 대 한 hello 오른쪽 흐름을 결정 해야 할 경우 체크 아웃 [유형의 hello v2.0를 빌드할 수 앱 hello](active-directory-v2-flows.md)합니다.

* [OAuth 2.0를 사용하여 모바일 및 네이티브 응용 프로그램 빌드](active-directory-v2-protocols-oauth-code.md)
* [Open ID Connect를 사용하는 웹앱 빌드](active-directory-v2-protocols-oidc.md)
* [OAuth 2.0 암시적 흐름 hello로 단일 페이지 앱 빌드](active-directory-v2-protocols-implicit.md)
* [OAuth 2.0 클라이언트 자격 증명 흐름 hello로 빌드 디먼 또는 서버 쪽 프로세스](active-directory-v2-protocols-oauth-client-creds.md)
* [OAuth 2.0 대신 흐름 hello로 Web API에서 토큰을 가져오기](active-directory-v2-protocols-oauth-on-behalf-of.md)
