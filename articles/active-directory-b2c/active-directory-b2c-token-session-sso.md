---
title: "Azure Active Directory B2C: 토큰, 세션 및 Single Sign-On 구성 | Microsoft Docs"
description: "Azure Active Directory B2C에서 토큰, 세션 및 Single Sign-On 구성"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: 토큰, 세션 및 Single Sign-On 구성
이 기능은 다음의 [정책별](active-directory-b2c-reference-policies.md)세분화된 제어를 제공합니다.

1. Azure AD(Azure Active Directory) B2C에서 내보낸 보안 토큰의 수명.
2. Azure AD B2C에서 관리하는 웹 응용 프로그램 세션의 수명.
3. Azure AD B2C에서 내보내는 hello 보안 토큰에 있는 중요 한 클레임의 형식입니다.
4. B2C 테넌트에 있는 여러 앱 및 정책의 SSO(Single Sign-On) 동작.

다음과 같이 B2C 테넌트에서 이 기능을 사용할 수 있습니다.

1. 다음 단계를 너무[toohello B2C 기능 블레이드를 탐색](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure 포털에 있습니다.
2. **로그인 정책**을 클릭합니다. *참고: **로그인 정책**뿐만 아니라 모든 정책 유형에서 이 기능을 사용할 수 있습니다*.
3. 클릭하여 정책을 엽니다. 예를 들어 **B2C_1_SiIn**을 클릭합니다.
4. 클릭 **편집** hello hello 블레이드 위쪽에 있습니다.
5. **토큰, 세션 및 Single Sign-On 구성**을 클릭합니다.
6. 원하는 변경 사항을 적용합니다. 이후 섹션에서 사용할 수 있는 속성에 대해 알아봅니다.
7. **확인**을 클릭합니다.
8. 클릭 **저장** hello hello 블레이드 맨 합니다.

## <a name="token-lifetimes-configuration"></a>토큰 수명 구성
Azure AD B2C 지원 hello [OAuth 2.0 권한 부여 프로토콜](active-directory-b2c-reference-protocols.md) 사용을 위한 보안 액세스 tooprotected 리소스입니다. tooimplement 다양 한이 지원, Azure AD B2C 내보냅니다 [보안 토큰](active-directory-b2c-reference-tokens.md)합니다. 다음은 Azure AD B2C에서 내보낸 보안 토큰의 수명을 toomanage를 사용할 수 있는 하는 hello 속성입니다.

* **ID 및 액세스 토큰 수명 (분)**: hello 수명의 hello OAuth 2.0 전달자 토큰 사용 되는 toogain 액세스 tooa 보호 된 리소스입니다. Azure AD B2C는 이때 ID 토큰을 발급합니다. 에 대 한 지원을 추가 하는 경우이 값은 tooaccess 토큰에도 적용 됩니다.
  * 기본값: 60분.
  * 최소(포함) = 5분.
  * 최대(포함) = 1440분.
* **토큰 수명 새로 고침 (일)**: 새 액세스 또는 ID 토큰 새로 고침 토큰 사용된 tooacquire 되기까지의 일 수 있습니다는 최대 기간을 hello (및 필요에 따라 새로운 새로 고침 토큰, hello 응용 프로그램에 권한이 부여 된 경우 `offline_access` 범위).
  * 기본값 = 14일.
  * 최소(포함) = 1일.
  * 최대(포함) = 90일.
* **슬라이딩 창 수명 토큰 새로 고침 (일)**:이 시간 기간이 경과 된 hello 사용자가 강제 toore 후-hello 응용 프로그램에 의해 획득 hello 가장 최근 새로 고침 토큰의 hello 유효 기간에 관계 없이 인증 합니다. Hello 스위치 너무 설정 된 경우에 제공할 수**Bounded**합니다. 보다 큰 toobe 또는 같은 toohello 필요로 **새로 고침 토큰 수명 (일)** 값입니다. Hello 스위치가 너무 설정 되어 있으면**Unbounded**, 특정 값을 제공할 수 없습니다.
  * 기본값 = 90일.
  * 최소(포함) = 1일.
  * 최대(포함) = 365일.

다음은 이러한 속성을 사용하여 활성화할 수 있는 몇 가지 사용 사례입니다.

* 자신이 hello 응용 프로그램에 지속적으로 활성화 됩니다으로 무제한으로 모바일 응용 프로그램에 로그인 한 사용자 toostay를 허용 합니다. Hello 설정 하 여 이렇게 하려면 **새로 고침 토큰 슬라이딩 창 수명 (일)** 너무 전환**Unbounded** 로그인 정책에서 합니다.
* Hello 적절 한 액세스 토큰 수명을 설정 하 여 업계의 보안 및 규정 준수 요구 사항을 충족 합니다.

    > [!NOTE]
    > 이러한 설정을 암호 재설정 정책에는 사용할 수 없습니다.
    > 
    > 

## <a name="token-compatibility-settings"></a>토큰 호환성 설정
Azure AD B2C에서 내보낸 보안 토큰의 서식 변경 tooimportant 클레임을 만들었습니다. 이 표준 프로토콜 지원 tooimprove 수행 및 타사 id 라이브러리와 상호 운용성에 대 한 합니다. 그러나 tooavoid 주요 기존 앱 속성 tooallow tooopt-고객에 게 필요에 따라 다음 hello 만든:

* **(Iss) 발급자 클레임**: hello 토큰을 발급 하는 hello Azure AD B2C 테 넌 트를 식별 합니다.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Hello 기본값입니다.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`:이 값에 hello B2C 테 넌 트와 hello 토큰 요청에 사용 되는 hello 정책에 대 한 Id를 포함 합니다. 경우 프로그램 응용 프로그램 또는 라이브러리에 필요한 Azure AD B2C toobe hello 준수 [OpenID Connect 검색 1.0 사양](http://openid.net/specs/openid-connect-discovery-1_0.html),이 값을 사용 합니다.
* **제목 (sub) 클레임**: hello 엔터티, 즉, hello 사용자, 토큰은 hello에 대 한 정보를 어설션하는이 이름을 식별 합니다.
  * **ObjectID**: hello 기본값입니다. Hello 디렉터리의 hello 사용자의 개체 ID hello hello로 채워져 `sub` hello 토큰에서 클레임입니다.
  * **지원 되지 않습니다**: 이전 버전과 호환성을 위해서만 제공 됩니다이 고 너무 전환 하는 것이 좋습니다**ObjectID** 수 있다면으로 합니다.
* **정책 ID를 나타내는 클레임**: hello 토큰 요청에 사용 되는 정책 ID는 hello에 채워집니다 hello 클레임 유형을 식별 합니다.
  * **tfp**: hello 기본값입니다.
  * **acr**: 이전 버전과 호환성을 위해서만 제공 됩니다이 고 너무 전환 하는 것이 좋습니다`tfp` 수 있다면으로 합니다.

## <a name="session-behavior"></a>세션 동작
Azure AD B2C 지원 hello [OpenID Connect 인증 프로토콜](active-directory-b2c-reference-oidc.md) tooweb 로그인 보안 응용 프로그램을 사용 하도록 설정 합니다. 다음은 hello 속성 toomanage 웹 응용 프로그램 세션을 사용할 수 있습니다.

* **웹 응용 프로그램 세션 수명 (분)**: hello 수명의 인증 성공 시 hello 사용자의 브라우저에 저장 된 Azure AD B2C 세션 쿠키입니다.
  * 기본값: 1440분.
  * 최소(포함) = 15분.
  * 최대(포함) = 1440분.
* **웹 앱에 대 한 세션 제한 시간**:이 스위치가 너무 설정 되어 있으면**절대**, hello 사용자가 강제 toore-hello로 지정 된 기간 후 인증 **웹 응용 프로그램 세션 수명 (분)** 간격이 경과 합니다. 이 스위치가 너무 설정 되어 있으면**롤링** (기본 설정 hello) hello 사용자가 웹 응용 프로그램에서 계속 활성화 상태로 hello 사용자 로그인 유지 합니다.

다음은 이러한 속성을 사용하여 활성화할 수 있는 몇 가지 사용 사례입니다.

* Hello 적절 한 웹 응용 프로그램 세션을 설정 하 여 업계의 보안 및 규정 준수 요구 사항을 충족 수명입니다.
* 사용자가 웹 응용 프로그램의 높은 수준의 보안 일부와 상호 작용하는 동안 설정 기간 후 강제로 다시 인증합니다. 

    > [!NOTE]
    > 이러한 설정을 암호 재설정 정책에는 사용할 수 없습니다.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>SSO(Single Sign-On) 구성
B2C 테 넌 트의 여러 응용 프로그램 및 정책을 경우 간에 사용자 상호 작용을 관리할 hello를 사용 하 여 **Single sign on 구성** 속성입니다. 설정에 따라 hello hello 속성 tooone를 설정할 수 있습니다.

* **테 넌 트**: hello 기본 설정입니다. 이 설정을 사용 하면 여러 응용 프로그램 및 정책을 B2C 테 넌 트에 tooshare hello 동일한 사용자 세션. 예를 들어 사용자가 응용 프로그램, Contoso Shopping에 로그인하면 액세스의 관점에서 볼 때 다른 앱인 Contoso Pharmacy에도 원활하게 로그인할 수 있습니다.
* **응용 프로그램**: 이렇게 하면 다른 응용 프로그램에 관계 없이 응용 프로그램에만 사용자 세션 toomaintain 합니다. 예를 들어 hello 사용자 toosign tooContoso 약 학에서에서 원하는 (hello로 동일한 자격 증명)가 Contoso 쇼핑 hello에 다른 응용 프로그램에 이미 서명이 된 경우에 동일한 B2C 테 넌 트입니다. 
* **정책**: 이렇게 하면 toomaintain 독립적으로 사용 하는 hello 응용 프로그램 정책에만 사용자 세션. 예를 들어 hello 사용자가 이미 로그인를 다중 단계 인증 (MFA) 단계를 완료 하는 경우 자신이 부여할 수 있습니다 여러 응용 프로그램의 액세스 toohigher 보안 부분 hello 연결 세션 toohello 정책 만료 되지 않습니다.
* **비활성화 된**: hello 전체 사용자 작업을 통해 사용자 toorun hello hello 정책 실행할 때마다 강제로 합니다. 예를 들어 이렇게 하면 여러 사용자가 toosign (에 공유 데스크톱 시나리오) 응용 프로그램을 tooyour hello 전체 시간 동안 단일 사용자를 로그인 상태인 동안에 있습니다.

    > [!NOTE]
    > 이러한 설정을 암호 재설정 정책에는 사용할 수 없습니다.
    > 
    > 

