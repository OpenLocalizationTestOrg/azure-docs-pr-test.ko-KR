---
title: "Azure AD를 사용 하 여 aaaSharing 계정을 | Microsoft Docs"
description: "Azure Active Directory 온-프레미스 응용 프로그램 및 소비자 클라우드 서비스에 대 한 조직 toosecurely 공유 계정을 사용 하는 방법을 설명 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Azure AD와 계정 공유
## <a name="overview"></a>개요
경우에 따라 조직에서는 여러 사용자에 대 한 toouse 단일 사용자 이름 및 암호 해야 합니다. 일반적으로 다음 두 경우가 여기에 해당합니다.

* 온-프레미스 앱이나 소비자 클라우드 서비스 등, 각 사용자에 대한 고유의 로그인과 암호가 필요한 응용 프로그램을 액세스할 때(예: 기업 소셜 미디어 계정)
* 다중 사용자 환경을 만들 때. 상승 된 권한을 갖는 단일, 로컬 계정에 있을 수 있습니다 및 사용 되는 toodo 핵심 설치, 관리 및 복구 작업 (예: hello 로컬 "전역 관리자" 계정 Salesforce에서 Office 365 또는 hello 루트 계정에 대 한) 될 수 있습니다.

일반적으로 이러한 계정은 hello 자격 증명 (사용자 이름/암호) toohello 오른쪽 개인 배포 하거나 여러 신뢰할 수 있는 에이전트에 액세스할 수 있는 공유 위치에 저장 하 여 공유할 수는 있습니다.

기존 공유 모델 hello에 몇 가지 단점이 있습니다.

* 응용 프로그램에서 액세스 toonew 사용 액세스 해야 하는 toodistribute 자격 증명 tooeveryone가 필요 합니다.
* 각 공유 응용 프로그램은 자체 고유한 사용자 tooremember 여러 가지 자격 증명을 요구 하는 공유 자격 증명 집합이 필요할 수 있습니다. 사용자가 tooremember 많은 자격 증명을가지고 hello 위험 toorisky 사례 적용은 증가 합니다. (예: 암호를 적어).
* 누구에 게 액세스 tooan 응용 프로그램을 알 수 없습니다.
* 응용 프로그램에 누가 *액세스했는지* 알 수 없습니다.
* 다시 배포 하 고 tooupdate hello 자격 증명이 있어야 tooremove 액세스 tooan 응용 프로그램이 필요할 때 tooeveryone toothat 응용 프로그램에 액세스 해야 하는 합니다.

## <a name="azure-active-directory-account-sharing"></a>Azure Active Directory 계정 공유
Azure AD는 새로운 접근 방식을 이러한 단점을 제거 하는 공유 toousing 계정을 제공 합니다.

Azure AD 관리자에 게 사용자가 액세스 패널 hello를 사용 하 고 hello 유형의 single sign on 해당 응용 프로그램에 가장 적합 한 선택 하 여 액세스할 수 있는 응용 프로그램을 구성 합니다. 이러한 형식 중 하나 *암호 기반 single sign-on*, 해당 앱에 대 한 hello 로그온 프로세스 중 "브로커"의 일종으로 작동 하는 Azure AD를 통해 수 있습니다.

사용자가 조직 계정으로 한번에 로그인합니다. 이 hello 동일한 계정을 정기적으로 사용 하는 tooaccess 데스크톱 또는 전자 메일입니다. 사용자는 자신에게 할당된 응용 프로그램만 확인하고 액세스할 수 있습니다. 공유 계정을 사용하면 이 응용 프로그램 목록이 수에 관계없이 공유 자격 증명을 포함할 수 있습니다. hello 최종 사용자는 tooremember 필요 하지 않습니다 또는 다양 한 계정을 사용 중일 수도 hello 적어 둡니다.

공유 계정을 사용하면 관리뿐 아니라 활용성도 높아지며 보안도 향상됩니다. 사용 권한 toouse hello 자격 증명이 있는 사용자 암호를 공유 하는 hello를 표시 되지 않는 하지만 대신 오케스트레이션된 인증 흐름의 일환으로 사용 권한을 toouse hello 암호를 가져옵니다. 또한 일부 암호 SSO 응용 프로그램을 사용할 경우 hello 옵션 toohave Azure AD 계정 보안 hello 증가 대규모의 복잡 한 암호를 사용 하 여 롤오버 (업데이트) hello 암호 주기적으로 합니다. 관리자에 게 쉽게 부여할 수 있습니다 또는 tooan 응용 프로그램 액세스를 해지 되 고 또한 액세스 toohello 계정 누가 및 지난 hello에 액세스 하를 알아야 합니다.

Azure AD는 모든 유형의 암호 Single Sign-on 응용 프로그램 전체에서EMS(Enterprise Mobility Suite), 프리미엄 또는 기본 라이선스 사용자의 공유 계정을 지원합니다. Hello 응용 프로그램 갤러리에서 미리 통합 된 응용 프로그램 중 하나에 대 한 계정을 공유할 수 있습니다 및 암호 인증 응용 프로그램 자체에 추가할 수 [SSO의 사용자 지정 앱](active-directory-sso-integrate-saas-apps.md)합니다.

계정에 공유를 사용하는 Azure AD 기능은 다음과 같습니다.

* [암호 SSO(Single sign-on)](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* 암호 SSO(Single sign-on) 에이전트
* [그룹 할당](active-directory-accessmanagement-self-service-group-management.md)
* 사용자 지정 암호 앱
* [앱 사용 대시보드/보고서](active-directory-passwords-get-insights.md)
* 최종 사용자 액세스 패널
* [앱 프록시](active-directory-application-proxy-get-started.md)
* [Active Directory 마켓플레이스](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>계정 공유
Azure AD toouse tooshare 계정을를 해야 합니다.

* 응용 프로그램 [앱 갤러리](https://azure.microsoft.com/marketplace/active-directory/)나 [사용자 지정 응용 프로그램](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx) 추가
* 암호 Single Sign-on (SSO)에 대 한 hello 응용 프로그램 구성
* 사용 하 여 [그룹 기반 할당](active-directory-accessmanagement-group-saasapps.md) 선택 hello 옵션 tooenter 공유 자격 증명 및
* 선택 사항: Facebook, Twitter, LinkedIn, 등 일부 응용 프로그램에서 사용할 수 있습니다에 대 한 hello 옵션 [Azure AD 자동 암호 롤오버](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

만들 수도 있습니다 공유 계정 보다 안전한 Multi-factor Authentication (MFA)와 (에 대 한 자세한 내용은 [Azure AD와 응용 프로그램 보안](../multi-factor-authentication/multi-factor-authentication-get-started.md)) 사용 하 여 액세스 toohello 응용 프로그램을 가진 hello 기능 toomanage 위임할 수 있습니다 및 [Azure AD 셀프 서비스](active-directory-accessmanagement-self-service-group-management.md) 그룹 관리 합니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [조건부 액세스를 사용한 앱 보호](active-directory-conditional-access.md)
* [셀프 서비스 그룹 관리/SSAA](active-directory-accessmanagement-self-service-group-management.md)

