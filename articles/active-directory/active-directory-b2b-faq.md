---
title: "Active Directory B2B 공동 작업 Faq aaaAzure | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Azure Active Directory B2B 공동 작업 FAQ

질문과 대답 (Faq) Azure Active Directory (Azure AD) 기업 B2B 공동 작업에 대 한 이러한 값은 주기적으로 업데이트 tooinclude 새 항목입니다.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Azure AD B2B 공동 작업은 hello Azure 클래식 포털에서에서 사용할 수 있습니까?
아니요. Azure AD B2B 공동 작업 기능 hello에만 사용할 수 있는 [Azure 포털](https://portal.azure.com) 및 hello [액세스 패널](https://myapps.microsoft.com/)합니다. 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>B2B 공동 작업 게스트 사용자에게 더 직관적인 환경이 되도록 로그인 페이지를 사용자 지정할 수 있나요?
그렇습니다. [이 기능에 대한 블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/)을 참조하세요. 에 대 한 자세한 내용은 방법 toocustomize 조직의 로그인 페이지에서 참조 [회사에 toosign 및 액세스 패널 페이지에 브랜딩 추가](active-directory-add-company-branding.md)합니다.

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>B2B 공동 작업 사용자가 SharePoint Online 및 OneDrive에 액세스할 수 있습니까?
예. 그러나는 hello 사용자 선택기를 사용 하 여 SharePoint Online에서 기존 게스트 사용자에 대 한 hello 기능 toosearch **오프** 기본적으로 합니다. 기존 게스트 사용자에 게 옵션 toosearch hello에 tooturn 설정 **ShowPeoplePickerSuggestionsForGuestUsers** 너무**에**합니다. 이 설정을 hello 테 넌 트 수준에서 나 hello 사이트 모음 수준에서 설정할 수 있습니다. Hello 집합 SPOTenant 및 집합 SPOSite cmdlet을 사용 하 여이 설정을 변경할 수 있습니다. 이러한 cmdlet과 함께 멤버 hello 디렉터리에서 기존의 모든 게스트 사용자를 검색할 수 있습니다. Hello 테 넌 트 범위에 대 한 변경 내용에 이미 배포 되어 있는 SharePoint Online 사이트 영향을 주지 않습니다.

### <a name="is-hello-csv-upload-feature-still-supported"></a>여전히 지원 되는 기능을 업로드 하는 CSV hello?
예. Hello.csv 파일 업로드 기능을 사용 하는 방법에 대 한 자세한 내용은 참조 [이 PowerShell 샘플](active-directory-b2b-code-samples.md)합니다.

### <a name="how-can-i-customize-my-invitation-emails"></a>초대 전자 메일을 어떻게 사용자 지정할 수 있습니까?
Hello를 사용 하 여 hello 초대자 프로세스에 대 한 거의 모든 항목을 지정할 수 있습니다 [B2B 초대 Api](active-directory-b2b-api.md)합니다.

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>초대 된 외부 사용자 초대 하려는 후 hello 조직에 둘 수 있습니까?
초대 조직 관리자에 게 해당 디렉터리에서 B2B 공동 작업 게스트 사용자를 삭제할 수 있지만 hello 게스트 사용자 hello 단독으로 조직 디렉터리 초대를 벗어날 수 없습니다. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>게스트 사용자가 Multi-Factor Authentication 방법을 재설정할 수 있나요?
예. 게스트 사용자의 다단계 인증 메서드 hello 동일한 방식으로 일반 사용자가 수행 재설정할 수 있습니다.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>어떤 조직이 Multi-Factor Authentication 라이선스를 담당하나요?
hello 초대 조직 다단계 인증을 수행합니다. 조직 초대 hello hello 조직에 다단계 인증을 사용 하는 B2B가 사용자에 게 충분 한 라이선스가 있는지 확인 해야 합니다.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>파트너 조직이 이미 Multi-Factor Authentication을 설정한 경우에 어떻게 하나요? 해당 Multi-Factor Authentication을 신뢰하고 자체적인 Multi-Factor Authentication을 사용하지 않나요?
선택 하면 특정 파트너 tooexclude (hello 초대 조직의) multi-factor authentication에서 하므로이 기능은 이후 릴리스에서에 예정 되어 합니다.

### <a name="how-can-i-use-delayed-invitations"></a>지연된 초대는 어떻게 사용할 수 있나요?
조직 수도 tooadd B2B 공동 작업 사용자가 프로 비전 tooapplications 필요에 따라 있으며 다음 초대를 보냅니다. Hello B2B 공동 작업 초대 API toocustomize hello 온 보 딩 워크플로 사용할 수 있습니다.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>게스트 사용자를 제한된 관리자로 지정할 수 있나요?
그렇습니다. 자세한 내용은 참조 [추가 게스트 사용자 tooa 역할](active-directory-users-assign-role-azure-portal.md)합니다.

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Azure AD B2B 공동 작업 B2B 사용자 tooaccess hello Azure 포털 수 있습니까?
사용자가 제한 된 관리자 또는 전역 관리자의 hello 역할을 할당 하지 않으면 B2B 공동 작업 사용자가 Azure 포털 액세스 toohello를 필요로 합니다. 그러나 hello 제한 된 관리자 또는 전역 관리자 역할이 할당 된 B2B 공동 작업 사용자 hello 포털에 액세스할 수 있습니다. 또한 이러한 관리자 역할 중 하나의 할당 되지 않은 게스트 사용자가 hello 포털에 액세스 하는 경우 hello 사용자 될 수 있습니다 수 tooaccess의 특정 부분 hello 경험 합니다. hello 게스트 사용자 역할에 일부 권한이 hello 디렉터리에 있습니다.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>게스트 사용자에 게 Azure 포털 액세스 toohello를 차단할 수 있나요?
예! 이 정책을 구성 하는 경우 주의 tooavoid 실수로 차단 액세스 toomembers 및 관리자 수 있습니다.
tooblock 게스트 사용자의 액세스 toohello [Azure 포털](https://portal.azure.com), hello Windows Azure 클래식 배포 모델 API의에서 조건부 액세스 정책을 사용:
1. Hello 수정 **모든 사용자에 게** 그룹 구성원만 포함 되도록 합니다.
  ![수정 hello 그룹 스크린 샷](media/active-directory-b2b-faq/modify-all-users-group.png)
2. 게스트 사용자를 포함하는 동적 그룹을 만듭니다.
  ![그룹 스크린샷 만들기](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Hello 다음과 같이 비디오 hello 포털에 액세스 하지 못하도록 조건부 액세스 정책 tooblock 게스트 사용자를 설정 합니다.
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Azure AD B2B 공동 작업에서는 Multi-Factor Authentication 및 소비자 전자 메일 계정을 지원하나요?
예. Multi-Factor Authentication 및 소비자 전자 메일 계정은 둘 다 Azure AD B2B 공동 작업에 지원됩니다.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Toosupport 사용자 암호 재설정 Azure AD B2B 공동 작업을 계획 입니까?
예. Hello 파트너 조직에서 초대 B2B 사용자에 대 한 셀프 서비스 암호 재설정 (SSPR)에 대 한 중요 세부 정보는 다음과 같습니다.
 
* SSPR은 hello B2B 사용자의 hello identity 테 넌 트에만 발생합니다.
* Hello identity 테 넌 트 Microsoft 계정인 경우 Microsoft 계정 SSPR 메커니즘 hello 사용 됩니다.
* Hello identity 테 넌 트에는-just-in-time JIT ()은 "바이러스에 감염" 테 넌 트, 암호 재설정 전자 메일 전송 됩니다.
* 다른 테 넌 트에 대 한 hello 표준 SSPR 프로세스 B2B 사용자에 대 한 다음 됩니다. Hello 리소스의 hello 컨텍스트에서 B2B 사용자가 SSPR 멤버 처럼 테 넌 시 차단 됩니다. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>회사 또는 학교 전자 메일 주소를 사용하는 초대를 수락했으나 기존의 Azure AD 계정이 없는 JIT(Just-In-Time) 또는 "바이럴" 테넌트의 게스트 사용자는 암호 재설정을 사용할 수 있나요?
예. 허용 하는 사용자 tooreset 암호 hello JIT 테 넌 트의 암호 재설정 메일을 보낼 수 있습니다.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Microsoft Dynamics CRM에서 Azure AD B2B 공동 작업에 대한 온라인 지원을 제공합니까?
현재 Microsoft Dynamics CRM에서는 Azure AD B2B 공동 작업에 대한 온라인 지원을 제공하지 않습니다. 그러나 계획 toosupport이 향후 hello에입니다.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>새로 만든된 B2B 공동 작업 사용자에 대 한 초기 암호의 hello 수명을 이란?
Azure AD에는 문자, 암호 강도 및 계정 잠금 요구 사항이 적용 tooall Azure AD 클라우드 사용자 계정을 동일 하 게 고정된 된 집합입니다. 클라우드 사용자 계정은 다른 ID 공급자와 페더레이션되지 않은 계정입니다. 예를 들면 다음과 같습니다. 
* Microsoft 계정
* Facebook
* Active Directory Federation Services
* 다른 클라우드 테넌트(B2B 공동 작업용)

페더레이션된 계정에 대 한 암호 정책을 hello 온-프레미스 테 넌 트 및 hello 사용자의 Microsoft 계정 설정에 적용 되는 hello 정책에 따라 달라 집니다.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Toohave 다른 테 넌 트 사용자와 게스트 사용자에 대 한 응용 프로그램에서 발생 한 조직은 할 수 있습니다. 이에 대한 표준 지침이 있습니까? Hello identity provider 클레임 hello 올바른 모델 toouse의 hello 존재 인가요?
 게스트 사용자 모든 identity provider tooauthenticate를 사용할 수 있습니다. 자세한 내용은 [B2B 공동 작업 사용자의 속성](active-directory-b2b-user-properties.md)을 참조하세요. 사용 하 여 hello **UserType** 속성 toodetermine 사용자 경험 합니다. hello **UserType** 클레임 hello 토큰에 현재 포함 되지 않습니다. 응용 프로그램 hello 사용자 및 UserType tooget hello에 대 한 hello Graph API tooquery hello 디렉터리를 사용 해야 합니다.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>어디에 있습니까 B2B 공동 작업 커뮤니티 tooshare 솔루션 및 toosubmit 아이디어?
피드백 tooyour tooimprove B2B 공동 작업을 지속적으로 여러분 됩니다. 이때 회원님의 사용자 있습니다 tooshare 초대 시나리오, 모범 사례 및 Azure AD B2B 공동 작업에 대 한 원하는 합니다. Hello의 hello 토론을 조인할 [Microsoft 기술 커뮤니티](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b)합니다.
 
귀하의 아이디어와 기능에 대 한 투표 또한 있습니다 toosubmit 초대 [B2B 공동 작업 아이디어](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas)합니다.

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>요청을 자동으로 교환 됩니다, 사용자는 hello는 방금 "준비 toogo" 전송할? 또는 hello 사용자 항상가 toohello 상환 URL 통해 tooclick?
Hello 초대 hello 파트너 조직의 멤버는 또한 조직에서에서 사용자가 보낸 초대 상환 hello B2B 사용자가 필요 하지 않습니다.

Hello 파트너 조직 toojoin hello 초대 조직에서에서 한 명의 사용자를 초대 하는 것이 좋습니다. [Hello 리소스 조직에이 사용자 toohello 게스트 초대자 역할을 추가](active-directory-b2b-add-guest-to-role.md)합니다. 이 사용자 hello에 대 한 로그인을 사용 하 여 hello 파트너 조직 내의 다른 사용자를 초대할 수 UI, PowerShell 스크립트 또는 Api입니다. 그런 다음 B2B 공동 작업 사용자가 해당 조직에서 필요한 tooredeem 초대 되지 않습니다.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>B2B 공동 작업 하도록 초대 hello 파트너에서 사용 중일 때 페더레이션 tooadd 자신의 온-프레미스 인증에 주는 작동 방식
Hello 파트너에 게 페더레이션된 Azure AD 테 넌 트 경우 toohello 온-프레미스 인증 인프라, 온-프레미스 single sign on (SSO)는 자동으로 수행 됩니다. Hello 파트너 없는 경우 Azure AD 테 넌 트, Azure AD 계정의 새 사용자에 대해 생성 됩니다. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>B2C에서는 이러한 종류의 계정을 사용했는데 Azure AD B2B에서는 gmail.com 및 outlook.com 전자 메일 주소를 허용하지 않나요?
Hello 차이점 B2B 및 비즈니스-회사 (B2C) 공동 작업 identities는 측면에서 지원 됩니다 제거. 사용 되는 hello id B2B 또는 B2C 사용할지 이유가 toochoose 않습니다. 공동 작업 옵션을 선택하는 방법에 대한 정보는 [Azure Active Directory에서 B2B 공동 작업과 B2C 비교](active-directory-b2b-compare-b2c.md)를 참조하세요.

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>어떤 응용 프로그램 및 서비스에서 Azure B2B 게스트 사용자를 지원하나요?
모든 Azure AD 통합 응용 프로그램은 Azure B2B 게스트 사용자를 지원합니다. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>파트너가 Multi-Factor Authentication을 설치하지 않은 경우 B2B 게스트 사용자에 대해 Multi-Factor Authentication을 강제할 수 있나요?
예. 자세한 내용은 [B2B 공동 작업 사용자에 대한 조건부 액세스](active-directory-b2b-mfa-instructions.md)를 참조하세요.

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>SharePoint에서 외부 사용자에 대한 "허용" 또는 "거부" 목록을 정의할 수 있습니다. Azure에서 수행할 수 있나요?
예. Azure AD B2B 공동 작업은 허용 목록 및 거부 목록을 지원합니다. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>라이선스 무엇을 해야 Azure AD B2B toouse?
Azure AD B2B toouse 수요가 한 조직의 라이선스 기능에 대 한 정보를 참조 [라이선스 지침 Azure Active Directory B2B 공동 작업](active-directory-b2b-licensing.md)합니다.

### <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure AD 관리자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-admin-add-users.md)
* [정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-iw-add-users.md)
* [hello B2B 공동 작업 초대 메일의 hello 요소](active-directory-b2b-invitation-email.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure AD B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure AD B2B 공동 작업 API 및 사용자 지정](active-directory-b2b-api.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure AD에서 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
