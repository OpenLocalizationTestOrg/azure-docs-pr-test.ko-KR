---
title: "Azure AD에 대 한 aaaDevelop 앱 | Microsoft Docs"
description: "Hello IT 전문가 용으로 작성 된,이 문서에서는 Active Directory와 Azure 응용 프로그램 통합에 대 한 지침을 제공 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Azure Active Directory용 기간 업무 앱 개발
이 가이드에서는 Azure AD (Active Directory).hello 용 기간 업무 (LoB) 응용 프로그램 개발의 개요를 의도 한 대상 그룹은 Active Directory/Office 365 전역 관리자를 제공 합니다.

## <a name="overview"></a>개요
Azure AD와 통합된 응용 프로그램을 구축하면 조직의 사용자에게 Office 365를 사용하여 Single Sign-On을 제공합니다. Hello 응용 프로그램에서 Azure AD 사용 hello 응용 프로그램에 대 한 인증 정책을 hello 제어할 때 발생 합니다. 조건부 액세스 및 multi-factor authentication (MFA)를 사용 하 여 tooprotect 앱 확인 하는 방법에 대 한 자세한 toolearn [구성 액세스 규칙](active-directory-conditional-access-azuread-connected-apps.md)합니다.

응용 프로그램 toouse Azure Active Directory에 등록 합니다. 개발자가 Azure AD tooauthenticate 사용자를 사용 하 고 전자 메일, 일정 및 문서와 같은 리소스에 액세스 toouser 요청 수를 의미 hello 응용 프로그램을 등록 합니다.

디렉터리(게스트 아님)의 멤버는 응용 프로그램을 등록할 수 있습니다.( *응용 프로그램 개체 만들기*라고 함)

응용 프로그램 등록 하는 사용자 toodo hello 후행을 수 있습니다.

* Azure AD가 인식하는 응용 프로그램에 ID 가져오기
* 구입 하거나 응용 프로그램 hello 하는 자세한 암호/키 자체 tooauthenticate tooAD를 사용할 수 있습니다.
* 브랜드 hello hello 사용자 정의 이름, 로고 등으로 Azure 포털에서에서 응용 프로그램입니다.
* Azure AD 권한 부여 기능 tootheir 앱 적용 포함 하 여:

  * 역할 기반 액세스 제어(RBAC)
  * OAuth 권한 부여 서버와 azure Active Directory (보안 hello 응용 프로그램에 의해 노출 되는 API)
* 포함 하 여 예상 대로 필요한 사용 권한이 필요한 응용 프로그램 toofunction hello에 대 한 선언 합니다.

      - 앱 사용 권한(전역 관리자만 해당) 예: 다른 Azure AD 응용 프로그램 또는 역할 멤버 자격 상대 tooan Azure 리소스, 리소스 그룹의에서 역할 멤버 자격 또는 구독
      - 위임된 권한(모든 사용자). 예: Azure AD, 로그인 및 프로필 읽기

> [!NOTE]
> 기본적으로 모든 멤버는 응용 프로그램을 등록할 수 있습니다. 응용 프로그램 toospecific 멤버를 등록 하기 위한 toorestrict 사용 권한을 확인 하려면 어떻게 해야 toolearn [응용 프로그램 tooAzure AD에 추가 하는 방법을](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)합니다.
>
>

여기은 어떤 사용자 전역 관리자에 게 필요 toodo toohelp 개발자 확인 합니다 응용 프로그램 프로덕션에 대 한 준비:

* 액세스 규칙 구성(액세스 정책/MFA)
* Hello 앱 toorequire 사용자 할당을 구성 하 고 사용자를 할당 합니다.
* Hello 기본 사용자 승인 환경에 표시 안 함

## <a name="configure-access-rules"></a>액세스 규칙 구성
응용 프로그램별 액세스 규칙 tooyour SaaS 앱을 구성 합니다. 예를 들어 MFA를 요구할 수도 있고 신뢰할 수 있는 네트워크 액세스 toousers 허용할 수 있습니다. 이 대 한 세부 정보 hello hello 문서에서 사용할 수 있는 [구성 액세스 규칙](active-directory-conditional-access-azuread-connected-apps.md)합니다.

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Hello 앱 toorequire 사용자 할당을 구성 하 고 사용자를 할당 합니다.
기본적으로 사용자는 할당되지 않아도 응용 프로그램에 액세스할 수 있습니다. 그러나 hello 응용 프로그램 역할을 노출 하는 경우 또는 사용자의 액세스 패널에 응용 프로그램 tooappear hello를 하려는 경우 사용자 할당을 해야 합니다.

[사용자 할당 요구](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Azure AD Premium 또는 Enterprise Mobility Suite(EMS) 구독자인 경우 그룹을 사용하는 것이 좋습니다. Toohello 응용 프로그램 그룹을 지정 toodelegate 진행 중인 액세스 관리 toohello 그룹의 소유자를 hello 있습니다. Hello 그룹을 만들거나 hello 담당자 그룹 관리 기능을 사용 하 여 조직 toocreate hello 그룹에 게 요청 수 있습니다.

[Tooan 응용 프로그램 사용자를 할당합니다.](active-directory-applications-guiding-developers-assigning-users.md)  
[Tooan 응용 프로그램 그룹 지정](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>사용자 동의 무시
기본적으로 각 사용자의 동의 환경 toosign를 거칩니다. 사용자에 게 toogrant 권한을 tooan 응용 프로그램 요청 hello 승인 환경을 그러한 결정에 익숙하지 않은 사용자에 게 혼란을 줄 수 있습니다.

신뢰할 수 있는 응용 프로그램의 경우 조직을 대신 하 여 승인 toohello 응용 프로그램에 의해 hello 사용자 경험을 간소화할 수 있습니다.

사용자 승인 및 동의 hello에 대 한 자세한 내용은 Azure의 경험 하십시오 참조 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)합니다.

## <a name="related-articles"></a>관련 문서
* [보안 된 원격 액세스 tooon 온-프레미스 응용 프로그램을 Azure AD 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-get-started.md)
* [Azure Conditional Access Preview for SaaS Apps](active-directory-conditional-access-azuread-connected-apps.md)
* [Azure AD와 tooapps 액세스 관리](active-directory-managing-access-to-apps.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
