---
title: Active Directory FAQ aaaAzure | Microsoft Docs
description: "Azure Active Directory FAQ tooaccess Azure 및 Azure Active Directory, 암호 관리 및 응용 프로그램 액세스 하는 방법에 대 한 질문에 답변 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Azure Active Directory FAQ
Azure Active Directory(Azure AD)는 ID, 액세스 관리 및 보안의 모든 측면에 걸쳐있는 포괄적인 IDaaS(Identity as a Service) 솔루션입니다.

자세한 내용은 [Azure Active Directory란?](active-directory-whatis.md)을 참조하세요.


## <a name="access-azure-and-azure-active-directory"></a>Azure 및 Azure Active Directory 액세스
**Q: 왜 받기 "구독이 없어 찾을 수" hello Azure 클래식 포털에서에서 Azure AD tooaccess 하려고 하면**

**A:** tooaccess hello Azure 클래식 포털, 각 사용자는 Azure 구독 함께 권한이 필요 합니다. Office 365 또는 Azure AD 유료 구독을 사용 하는 경우 너무 이동[http://aka.ms/accessAAD](http://aka.ms/accessAAD) 일회성 정품 인증 단계에 대 한 합니다. 그렇지 않은 경우 무료 tooactivate 할 [Azure 계정](https://azure.microsoft.com/pricing/free-trial/) 또는 유료 구독 합니다.

자세한 내용은 다음을 참조하세요.

* [Azure 구독과 Azure Active Directory의 연관 관계](active-directory-how-subscriptions-associated-directory.md)
* [Hello Azure에서 Office 365 구독의 디렉터리 관리](active-directory-manage-o365-subscription.md)

- - -
**Q: 사이 관계가 hello Azure AD를 Office 365 및 Azure?**

**A:** Azure AD 사용자 공통 id 및 액세스 기능을 가진 tooall 웹 서비스를 제공 합니다. 이러한 모든 서비스에 대 한 로그인 및 액세스 관리 설정 이미 Azure AD toohelp를 사용 하 여 Office 365, Microsoft Azure, Intune, 또는 다른 사용자, 있습니다를 사용 하 여 합니다.

Toouse 웹 서비스를 설정 하는 모든 사용자는 Azure AD 인스턴스를 하나 이상에서 사용자 계정으로 정의 됩니다. 클라우드 응용 프로그램 액세스와 같은 무료 Azure AD 기능에 이러한 계정을 설정할 수 있습니다.

Enterprise Mobility + Security와 같은 Azure AD 유료 서비스는 포괄적인 엔터프라이즈 규모 관리 및 보안 솔루션을 통해 Office 365 및 Microsoft Azure와 같은 기타 웹 서비스를 보완합니다.
- - -
**Toohello Azure 포털에에서 로그인 하지만 Azure 클래식 포털을 hello 하지 수 q 있습니까?**

**A:** hello Azure 포털 유효한 구독을 않아도 hello 클래식 포털에 유효한 구독이 필요 합니다.  구독이 없는 경우 toohello 클래식 포털에 로그인 할 수 없습니다.
- - -
**Q: 구독 관리자와 디렉터리 관리자 간의 hello 차이?**

**A:** 기본적으로 할당 된 Azure에 등록할 때 hello 구독 관리자 역할입니다. Microsoft 계정 또는 회사 구독 관리자를 사용 하거나 학교 계정은 Azure 구독 hello hello 디렉터리에서에 연결 됩니다.  이 역할은 hello Azure 포털에서에서 권한 있는 toomanage 서비스.

다른 사용자에 toosign 고 하 여 서비스에 액세스할 경우 동일한 구독 hello를 사용 하 여, 공동 관리자로 추가할 수 있습니다. 이 역할 hello에 대 한 액세스 권한이 hello 서비스 관리자와 동일 하지만 구독 tooAzure 디렉터리의 hello 연결을 변경할 수 없습니다.  구독 관리자에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooadd 또는 변경 Azure 관리자 역할](../billing-add-change-azure-subscription-administrator.md) 및 [Azure 구독과 Azure Active Directory와 연결 된](active-directory-how-subscriptions-associated-directory.md)합니다.


Azure AD에는 다양 한 관리자 역할 toomanage hello 디렉터리 및 id 관련 기능입니다.  이러한 관리자 액세스 toovarious 기능 hello Azure 포털에에서 있는 되거나 Azure 클래식 포털 hello 됩니다. admin 님 안녕하세요 역할 수 있는 작업을 만들기 또는 사용자가 편집을 tooothers 관리 역할 할당, 사용자 암호 다시 설정, 사용자 라이선스를 관리 하거나 도메인 관리 등을 결정 합니다.  Azure AD 디렉터리 관리자 및 그 역할에 대한 자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.

또한, Enterprise Mobility + Security와 같은 Azure AD 유료 서비스는 포괄적인 엔터프라이즈 규모 관리 및 보안 솔루션을 통해 Office 365 및 Microsoft Azure와 같은 기타 웹 서비스를 보완합니다.

- - -
**Q: 보고서에서 내 Azure AD 사용자 라이선스가 만료되는 시기를 표시하나요?**

**A:** 아니요.  현재는 제공되지 않습니다.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>하이브리드 Azure AD 시작


**Q: 협력자로 추가된 경우 테넌트를 어떻게 나가나요?**

**A:** hello "테 넌 트 전환기" hello 상단 오른쪽 tooswitch에서 테 넌 트 간의 공동 작업자로 tooanother 조직 테 넌 트를 추가할 때 사용할 수 있습니다.  현재 조직에 초대 방법은 tooleave hello 않으며 Microsoft이이 기능을 제공 하는 작업입니다.  Hello 조직 tooremove 초대를 요청할 수 있을 때까지이 기능을 테 넌 트에서 있습니다.
- - -
**Q: 내 온-프레미스 디렉터리 tooAzure AD는 어떻게 연결할 수 있습니까?**

**A:** Azure AD Connect를 사용 하 여 온-프레미스 디렉터리 tooAzure AD를 연결할 수 있습니다.

자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.

- - -
**Q: 온-프레미스 디렉터리와 클라우드 응용 프로그램 간에 SSO를 설정하려면 어떻게 해야 하나요?**

**A:** single sign-on를 (SSO) 온-프레미스 디렉터리와 Azure AD 간의 tooset 하기만 하면 됩니다. Azure AD를 통해 클라우드 응용 프로그램에 액세스 하면으로 hello 서비스 toocorrectly 자신의 온-프레미스 자격 증명을 사용 하 여 인증 사용자를 자동으로 구동 합니다.

온-프레미스에서 SSO 구현은 AD FS(Active Directory Federation Services)와 같은 페더레이션 솔루션 또는 암호 해시 동기화 구성으로 쉽게 달성할 수 있습니다. Hello Azure AD Connect 구성 마법사를 사용 하 여 두 옵션을 쉽게 배포할 수 있습니다.

자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.

- - -
**Q: Azure AD에서 내 조직의 사용자에 대한 셀프 서비스 포털을 제공하나요?**

**A:** 예, Azure AD에서는 hello [Azure AD 액세스 패널](http://myapps.microsoft.com) 셀프 서비스 사용자 및 응용 프로그램 액세스에 대 한 합니다. Office 365 고객 인 경우에서 찾을 수 있습니다 다양 한 hello 동일한 기능을 hello Office 365 포털입니다.

자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

- - -
**Q: Azure AD를 사용하면 내 온-프레미스 인프라를 관리하는 데 도움이 되나요?**

**A:** 예. Azure AD Premium edition hello Azure AD Connect Health를 제공합니다. Azure AD Connect Health를 사용 하 여 모니터링 하 고 온-프레미스 id 인프라 및 hello 동기화 서비스 파악할 수 있습니다.  

자세한 내용은 참조 [프로그램 hello 클라우드에서 온-프레미스 id 인프라 및 동기화 서비스 모니터링](active-directory-aadconnect-health.md)합니다.  

- - -
## <a name="password-management"></a>암호 관리
**Q: Azure AD 비밀번호 쓰기 저장을 암호 동기화 없이 사용할 수 있나요? (이 시나리오에서는 상태인 것 가능한 toouse Azure AD 셀프 서비스 암호 재설정 (SSPR) hello 클라우드에서 암호 쓰기 저장 및 저장소가 아니라 암호)**

**A:** 않아도 toosynchronize 프로그램 Active Directory 암호 tooAzure AD tooenable 쓰기 저장 합니다. 연결된 된 환경에서 Azure AD single sign on (SSO)에 의존 hello 온-프레미스 디렉터리 tooauthenticate hello 사용자 합니다. 이 시나리오에는 Azure AD에서 추적 하는 hello 온-프레미스 암호 toobe가 필요 하지 않습니다.

- - -
**Q: 어떻게 것 시간이 tooActive Directory 온-프레미스 다시 기록 암호 toobe?**

**A:** 비밀번호 쓰기 저장은 실시간으로 작동됩니다.

자세한 내용은 [암호 관리 시작](active-directory-passwords-getting-started.md)을 참조하세요.

- - -
**Q: 관리자가 관리하는 암호로 비밀번호 쓰기 저장을 사용할 수 있나요?**

**A:** 예, 암호 쓰기 저장 사용 하도록 설정 하는 경우 관리자가 수행 하는 hello 암호 작업은 다시 기록 tooyour 온-프레미스 환경입니다.  

Toopassword 관련 질문에 대 한 자세한 답변 참조 [암호 관리에 대 한 질문과 대답](active-directory-passwords-faq.md)합니다.
- - -
**Q: 내 암호 toochange 하는 동안 내 기존 Office 365/Azure AD 암호를 기억할 수 없을 경우 어떻게 해야 합니까?**

**A:** 이러한 상황에는 두 가지 옵션이 있습니다.  SSPR(셀프 서비스 암호 재설정)을 사용할 수 있으면 사용합니다.  SSPR 작동 여부는 구성 방식에 달려 있습니다.  자세한 내용은 참조 [어떻게 하더라도 hello 암호 다시 설정 포털 작업](active-directory-passwords-best-practices.md)합니다.

Office 365 사용자에 대 한 관리자 암호를 재설정할 수 hello에 설명 된 hello 단계를 사용 하 여 [사용자 암호 다시 설정](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US)합니다.

Azure AD 계정에 대 한 관리자 hello 다음 중 하나를 사용 하 여 암호를 재설정할 수 있습니다.

- [Hello Azure 포털에서에서 계정을 다시 설정](active-directory-users-reset-password-azure-portal.md)
- [Hello 클래식 포털에서 계정을 다시 설정](active-directory-create-users-reset-password.md)
- [PowerShell 사용](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>보안
**Q: 시도가 일정 횟수 실패하면 계정이 잠기나요 아니면 좀 더 복잡한 전략이 사용되나요?**</br>
보다 복잡 한 전략 toolock 계정을 사용합니다.  이 hello 요청 및 입력 하는 hello 암호의 hello IP 기반으로 합니다. 도 hello hello 잠금 기간 hello 가능성 공격 인지에 따라 증가 합니다.  

**Q: 특정 (일반적인) 암호 hello로 거부할 '이 암호가 되었습니다 toomany 사용한 번' 메시지, toopasswords hello 현재 active directory에 사용 되는 참조 않는?**</br>
이 모든 변형의 "Password" 및 "123456"와 같은 전역적으로 공통적인 toopasswords를 나타냅니다.

**Q: 수상한 소스(봇넷, tor 끝점)의 로그인 요청은 B2C 테넌트에서 차단되나요? 아니면 Basic 또는 Premium Edition 테넌트가 필요한가요?**</br>
요청을 필터링하고 봇넷으로부터 보호하며, 모든 B2C 테넌트에 적용되는 게이트웨이가 있습니다.

## <a name="application-access"></a>응용 프로그램 액세스
**Q: Azure AD 및 해당 기능과 미리 통합된 응용 프로그램의 목록을 어디에서 찾을 수 있나요?**

**A:** Azure AD에는 Microsoft, 응용 프로그램 서비스 공급자 및 파트너의 사전 통합된 응용 프로그램이 2,600개 넘게 있습니다. 사전 통합된 모든 응용 프로그램에서 SSO(Single Sign-On)를 지원합니다. SSO를 사용 하면 조직 자격 증명 tooaccess 앱을 사용할 수 있습니다. 일부 hello 응용 프로그램의 자동 프로 비전 및 프로 비전 해제에 지원 합니다.

Hello 미리 통합 된 응용 프로그램의 전체 목록은 참조 hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/)합니다.

- - -
**Q: 어떻게 하면 hello 필요한 응용 프로그램에에서 없는 Azure AD 마켓플레이스 hello?**

**A:** Azure AD Premium에서는 원하는 응용 프로그램을 추가하고 구성할 수 있습니다. 응용 프로그램의 기능 및 기본 설정에 따라 SSO 및 자동화된 프로비전을 구성할 수 있습니다.  

자세한 내용은 다음을 참조하세요.

* [Single sign on tooapplications hello Azure Active Directory 응용 프로그램 갤러리에 없는 구성](active-directory-saas-custom-apps.md)
* [SCIM tooenable 자동으로 프로 tooapplications Azure Active Directory에서에서 사용자 및 그룹을 사용 하 여](active-directory-scim-provisioning.md)

- - -
**Q: 사용자가 로그인 않는 tooapplications Azure AD를 사용 하 여?**

**A:** Azure AD 사용자가 tooview에 대 한 여러 가지 방법을 제공 하 고 같은 응용 프로그램에 액세스 합니다.

* hello Azure AD 액세스 패널
* hello Office 365 응용 프로그램 실행 프로그램
* 직접 로그인 toofederated 앱
* 암호 기반 딥 링크 toofederated, 또는 기존 앱

자세한 내용은 참조 [배포 Azure AD 통합 응용 프로그램 toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)합니다.

- - -
**Q: 여러 가지 방법 hello Azure AD 인증 및 single sign on tooapplications 수 무엇입니까?**

**A:** Azure AD는 SAML 2.0, OpenID Connect, OAuth 2.0, WS-Federation 등 인증 및 권한 부여를 위해 여러 표준화된 프로토콜을 지원합니다. 또한 Azure AD는 양식 기반 인증만 지원하는 앱에 대해 암호 보관 및 자동화된 로그인 기능도 지원합니다.  

자세한 내용은 다음을 참조하세요.

* [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)
* [Active Directory 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Azure Active Directory에서 Single Sign-On이 작동하는 방식](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**Q: 온-프레미스를 실행하는 응용 프로그램을 추가할 수 있나요?**

**A:** Azure AD 응용 프로그램 프록시 쉽고 안전한 액세스 제공 선택한 tooon 온-프레미스 웹 응용 프로그램입니다. Hello에 이러한 응용 프로그램에 액세스할 수 있습니다 동일한 방식으로 Azure AD에서 saas () 앱으로 소프트웨어를 액세스 합니다. 네트워크 인프라는 VPN 또는 toochange 필요 하지 않습니다.  

자세한 내용은 참조 [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](active-directory-application-proxy-get-started.md)합니다.

- - -
**Q: 특정 응용 프로그램에 액세스하는 사용자의 Multi-Factor Authentication을 어떻게 요청하나요?**

**A:** Azure AD 조건부 액세스에서는 각 응용 프로그램에 대한 고유한 액세스 정책을 할당할 수 있습니다. 정책에서 항상, 다단계 인증을 요구할 수 있습니다 또는 사용자가 로컬 네트워크에 연결 된 toohello 없는 합니다.  

자세한 내용은 참조 [tooAzure Active Directory 연결 tooOffice 365 및 기타 응용 프로그램 액세스 보안](active-directory-conditional-access.md)합니다.

- - -
**Q: SaaS 앱을 위한 자동 사용자 프로비전이 무엇인가요?**

**A:** Azure AD 사용 하 여 tooautomate hello 생성, 유지 관리 및 여러 인기 있는 클라우드 SaaS 응용 프로그램의 사용자 id 제거 합니다.

자세한 내용은 참조 [사용자 프로 비전 및 Azure Active Directory와 tooSaaS 응용 프로그램을 프로 비전 해제 자동화](active-directory-saas-app-provisioning.md)합니다.

- - -
**Q: Azure AD에서 보안 LDAP 연결을 설정할 수 있나요?**

**A:** 아니요. Azure AD는 hello LDAP 프로토콜을 지원 하지 않습니다.
