---
title: "Azure Active Directory B2C: 인증 프로토콜 | Microsoft Docs"
description: "사용 하 여 직접 toobuild 앱 Azure Active Directory B2C에서 지 원하는 프로토콜 hello 하는 방법"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C: 인증 프로토콜
Azure AD B2C(Azure Active Directory B2C)는 두 개의 업계 표준 프로토콜인 OpenID Connect 및 OAuth 2.0을 지원하여 앱에 대한 Identity-as-a-Service를 제공합니다. hello 서비스는 표준 호환 되지만 이러한 프로토콜의 모든 두 구현이 약간의 차이가 있을 수 있습니다. 

이 가이드의 hello 정보는 오픈 소스 라이브러리를 사용 하는 대신 직접 전송 하 고 HTTP 요청을 처리 하 여 코드를 작성 하는 경우에 유용 합니다. 각 특정 프로토콜의 hello 세부 정보에 착수 하기 전에이 페이지를 참조 하는 것이 좋습니다. 이미 Azure AD B2C에 잘 알고 있다면 넘어가면 너무 바로 하지만[프로토콜 참조 가이드 hello](#protocols)합니다.

<!-- TODO: Need link toolibraries above -->

## hello 기본 사항
Azure AD B2C를 사용 하는 모든 앱 toobe hello에 B2C 디렉터리에 등록 해야 [Azure 포털](https://portal.azure.com)합니다. 수집 하 고 몇 가지 값 tooyour 응용 프로그램을 할당 하는 hello 응용 프로그램 등록 프로세스:

* 앱을 고유하게 식별하는 **응용 프로그램 ID**
* A **리디렉션 URI** 또는 **식별자 패키지** 사용된 toodirect 응답 백 tooyour 앱 일 수 있는 합니다.
* 다른 몇 가지 시나리오 관련 값. 자세한 내용은 [어떻게 tooregister 응용 프로그램](active-directory-b2c-app-registration.md)합니다.

앱을 등록 하면 통신할 Azure Active Directory (Azure AD) toohello 끝점 요청을 전송 하 여:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

거의 모든 OAuth 및 OpenID Connect 흐름에서 4 자 hello 교환에 포함 됩니다.

![OAuth 2.0 역할](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* hello **권한 부여 서버** hello Azure AD 끝점입니다. 어느 것에 관련된 toouser 정보 및 액세스 안전 하 게 처리 됩니다. 또한 흐름의 hello 파티 간의 hello 트러스트 관계를 처리합니다. 이기 hello 사용자의 신원을 확인 하 고, 부여 및 액세스 tooresources 취소 토큰을 발급 해야 합니다. Hello id 공급자 라고도 합니다.

* hello **리소스 소유자** hello 최종 사용자는 일반적으로 합니다. Hello 데이터를 소유 하는 hello 파티 인데 %hello 전원 tooallow 제 3 자 tooaccess 해당 데이터 또는 리소스.

* hello **OAuth 클라이언트** 앱 됩니다. 응용 프로그램 ID로 식별됩니다. 이 일반적으로 최종 사용자 상호 작용 하는 hello 파티 합니다. 또한 hello 권한 부여 서버에서 토큰을 요청합니다. hello 클라이언트 권한 tooaccess hello 리소스 hello 리소스 소유자 부여 해야 합니다.

* hello **리소스 서버** hello 리소스 또는 데이터가 상주 합니다. 트러스트 hello 권한 부여 서버 toosecurely 인증 하 고 hello OAuth 클라이언트에 권한을 부여 합니다. 또한 tooa 리소스에 액세스 하는 토큰 tooensure 마스터인 전달자 액세스를 사용 합니다.

## 정책
지금, Azure AD B2C 정책은 hello hello 서비스의 가장 중요 한 기능입니다. Azure AD B2C 정책 도입 하 여 hello 표준 OAuth 2.0 및 OpenID Connect 프로토콜을 확장 합니다. Azure AD B2C tooperform 단순 인증 및 권한 부여 보다 훨씬 더 수 있습니다. 

정책은 등록, 로그인, 프로필 편집 등의 소비자 ID 경험을 완벽하게 설명합니다. 정책은 관리 UI에서 정의될 수 있습니다. HTTP 인증 요청에서 특별한 쿼리 매개 변수를 사용하여 실행될 수 있습니다. 

정책은 않습니다 OAuth 2.0 및 OpenID Connect의 표준 기능 hello 시간 toounderstand를 취해야 하 합니다. 자세한 내용은 참조 hello [Azure AD B2C 정책 참조 가이드](active-directory-b2c-reference-policies.md)합니다.

## 토큰
OAuth 2.0 및 OpenID Connect의 Azure AD B2C hello 구현은 JSON 웹 토큰 (Jwt)로 표현 되는 전달자 토큰을 포함 하 여 전달자 토큰을 광범위 하 게 사용 합니다. 전달자 토큰은 보호 된 리소스를 부여 "전달자" 액세스 tooa hello 하는 경량 보안 토큰입니다.

hello 전달자 hello 토큰을 제공할 수 있는 당사자입니다. Azure AD에서 전달자 토큰을 받으려면 먼저 당사자를 인증해야 합니다. 하지만 hello 필요한 단계는 전송 및 저장에서 toosecure hello 토큰을 따르지 않은 경우 차단 하 고 수 있습니다는 의도 하지 않은 당사자에서 사용 하는.

일부 보안 토큰에는 권한이 없는 당사자가 토큰을 사용하지 못하게 하는 메커니즘이 기본 제공되지만 전달자 토큰에는 이 메커니즘이 없습니다. 전송 계층 보안(HTTPS) 등의 보안 채널로 전송해야 합니다. 

전달자 토큰에 보안 채널 외부 전송 경우 악의적인 사용자 중간자 개입 공격 tooacquire hello 토큰을 사용할 수 있으며 toogain 무단 액세스 tooa 보호 된 리소스를 사용 합니다. hello 전달자 토큰을 저장 하거나 나중에 캐시 하는 경우 동일한 보안 원칙이 적용 됩니다. 항상 앱이 안전한 방식으로 전달자 토큰을 전송하고 저장하도록 합니다.

전달자 토큰의 보안 고려 사항에 대한 자세한 내용은 [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750)를 참조하세요.

사용할 수 있는 hello 여러 유형의 Azure AD B2C에 사용 되는 토큰에 대 한 자세한 내용은 [Azure AD 토큰 참조를 hello](active-directory-b2c-reference-tokens.md)합니다.

## 프로토콜
준비가 끝나면 tooreview 몇 가지 예제 요청, hello 자습서를 다음 중 하나로 시작할 수 있습니다. 각 해당 tooa 특정 인증 시나리오. 흘러가 적합 한지 결정 해야 할 경우 체크 아웃 [유형의 앱을 Azure AD B2C를 사용 하 여 빌드할 수 hello](active-directory-b2c-apps.md)합니다.

* [OAuth 2.0을 사용하여 모바일 및 네이티브 응용 프로그램 빌드](active-directory-b2c-reference-oauth-code.md)
* [OpenID Connect를 사용하여 웹앱 빌드](active-directory-b2c-reference-oidc.md)
* [Hello OAuth 2.0 암시적 흐름을 사용 하 여 단일 페이지 앱 빌드](active-directory-b2c-reference-spa.md)

