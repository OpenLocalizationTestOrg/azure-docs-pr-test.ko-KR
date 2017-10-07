---
title: "aaaAzure 보안 기능이 id 관리에 도움이 되도록 | Microsoft Docs"
description: " 이 문서는 id 관리를 지 원하는 hello 핵심 Azure 보안 기능의 개요를 제공 합니다. Microsoft id 및 액세스 관리 솔루션 도움말 IT 액세스 tooapplications와 리소스를 보호 및 hello 클라우드로 hello 회사 데이터 센터에서 다단계 인증 및 조건부 같은 유효성 검사의 수준을 사용 하도록 설정 액세스 정책입니다. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Azure ID 관리 보안 개요
Microsoft id 및 액세스 관리 솔루션 도움말 IT 액세스 tooapplications와 리소스를 보호 및 hello 클라우드로 hello 회사 데이터 센터에서 다단계 인증 및 조건부 같은 유효성 검사의 수준을 사용 하도록 설정 액세스 정책입니다. 고급 보안 보고, 감사 및 경고를 통해 의심스러운 작업을 모니터링하여 잠재적인 보안 문제를 완화시킵니다. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) 클라우드 (SaaS) 응용 프로그램 및 온-프레미스를 실행 하는 액세스 tooweb 앱 single sign on toothousands를 제공 합니다.

보안 이점의 Azure AD (Active Directory)를 hello 기능이 포함합니다.

* 하이브리드 엔터프라이즈에서 사용자, 그룹 및 장치의 동기화를 유지하도록 각 사용자에 대한 단일 ID 만들기 및 관리
* 수천 개의 미리 통합 된 SaaS 응용 프로그램을 포함 하 여 tooyour 응용 프로그램 single sign-on 액세스를 제공 합니다.
* 온-프레미스 및 클라우드 응용 프로그램에 대한 규칙 기반 Multi-Factor Authentication을 적용하여 응용 프로그램 액세스 보안 활성화
* 보안 된 원격 액세스 tooon-프레미스 프로 비전 웹 Azure AD 응용 프로그램 프록시를 통해 응용 프로그램

hello이 문서의 목적은 tooprovide id 관리를 지 원하는 hello 핵심 Azure 보안 기능의 개요입니다. 자세히 확인할 수 있도록 각 기능에 대 한 세부 정보를 제공 하는 링크 tooarticles도 제공 합니다.  

hello 다음 핵심 Azure Id 관리 기능을 중점적으로 hello 문서:

* SSO(Single sign-on)
* 역방향 프록시
* Multi-Factor Authentication
* 보안 모니터링, 경고 및 기계 학습 기반 보고서
* 소비자 ID 및 액세스 관리
* 장치 등록
* Privileged Identity Management
* ID 보호
* 하이브리드 ID 관리

## <a name="single-sign-on"></a>SSO(Single sign-on)
Single sign on (SSO)를 의미 수 tooaccess 모든 hello 응용 프로그램 및 리소스를 한 번만 단일 사용자 계정을 사용 하 여 로그인 toodo 비즈니스 해야 합니다. 로그인 한 후 모든 hello 필요한 응용 프로그램을 tooauthenticate 필요는 없지만 액세스할 수 있습니다 (예를 들어 암호 입력)를 두 번입니다.

대부분의 조직에서는 최종 사용자 생산성을 위해 Office 365, Box, Salesforce와 같은 SaaS(Software as a Service) 응용 프로그램에 의존합니다. 지금까지 IT 직원 필요한 tooindividually 만들고 각 SaaS 응용 프로그램에서 사용자 계정을 업데이트 하 고 사용자가 각 SaaS 응용 프로그램에 대 한 암호를 tooremember 했습니다.

Azure AD가 확장 hello 클라우드로 온-프레미스 Active Directory 환경 toouse 사용자가 사용 하도록 설정의 기본 조직 계정 toonot만 로그인 tootheir 도메인에 가입 된 장치 및 회사 리소스에 하는데 웹 및 SaaS 응용 프로그램 모두 hello도 작업에 필요합니다.

뿐만 아니라 사용자가 필요는 없으며 toomanage 사용자 이름 및 암호의 여러 집합, 자동으로 프로 비전 하거나 프로 비전이 해제에 따라 조직 그룹 및 해당 상태는 응용 프로그램 액세스 될 수 있습니다. Azure AD 보안을 소개 하 고 toocentrally 있습니다 사용할 수 있는 액세스 거 버 넌 스 컨트롤 전체 SaaS 응용 프로그램 사용자의 액세스를 관리 합니다.

자세한 정보:

* [Single Sign-On 개요](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Azure Active Directory Single Sign-On과 SaaS 앱 통합](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>역방향 프록시
Azure AD 응용 프로그램 프록시를 사용 하면 온-프레미스 응용 프로그램을와 같은 게시 [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) 사이트 [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), 및 [IIS](http://www.iis.net/)-기반 개인 네트워크 내부 앱의 경우 네트워크 외부의 toousers 보안 액세스를 제공 합니다. 원격 액세스를 제공 하는 응용 프로그램 프록시 및 sign-on (SSO)의 다양 한 종류에 대 한 온-프레미스 Azure AD에서는 지원 되는 SaaS 응용 프로그램의 hello 수천으로 웹 응용 프로그램입니다. 직원 tooyour 앱에서 로그인 할 수 자신의 장치로 홈 하 고이 클라우드 기반 프록시를 통해 인증 합니다.

자세한 정보:

* [Azure AD 응용 프로그램 프록시 사용](../active-directory/active-directory-application-proxy-enable.md)
* [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](../active-directory/active-directory-application-proxy-publish.md)
* [응용 프로그램 프록시를 사용하는 Single-Sign-On](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [조건부 액세스로 작업하기](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure multi-factor authentication (MFA)은 확인 방법을 두 개 이상 hello 사용 해야 하 고 보안 toouser 로그인 및 트랜잭션에 중요 한 두 번째 계층을 추가 하는 인증 방법입니다. MFA 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다. 전화 통화, 문자 메시지 또는 모바일 앱 알림 또는 확인 코드 및 타사 OAuth 토큰과 같은 다양한 확인 옵션을 통해 강력한 인증을 전달합니다.

자세한 정보:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure Multi-Factor Authentication 작동 방법](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>보안 모니터링, 경고 및 기계 학습 기반 보고서
일치하지 않는 액세스 패턴을 식별하는 보안 모니터링 및 경고 및 기계 학습 기반 보고서로 비즈니스를 보호할 수 있습니다. Azure Active Directory의 액세스 및 조직 디렉터리의 hello 무결성 및 보안에 대 한 사용 현황 보고서 toogain 가시성을 사용할 수 있습니다. 이 정보를 사용 하면 디렉터리 관리자 수 보다 잘 결정 있는 가능한 보안 위험이 발생할 수 있습니다 적절 하 게 될 수 toomitigate 이러한 위험.

Hello Azure 클래식 포털에서에서 보고서는 다음 방법으로 hello로 분류 됩니다.

* 비정상 보고서-이벤트가 있음을 toobe 비정상적인 로그인을 포함 합니다. 목표는 toomake 이러한 활동을 인식 하 고 toobe 수 toomake 의심 스러운 이벤트 인지에 대 한 결정을 사용 합니다.
* 통합 응용 프로그램 보고서 – 클라우드 응용 프로그램이 조직에서 사용되는 방식을 파악할 수 있게 해 줍니다. Azure Active Directory는 수천 개의 클라우드 응용 프로그램과 통합을 제공합니다.
* 오류 보고서 – 계정 tooexternal 응용 프로그램을 프로 비전 할 때 발생할 수 있는 오류를 나타냅니다.
* 사용자별 보고서 – 특정 사용자에 대한 장치/로그인 활동 데이터를 표시합니다.
* 활동 로그-지난 24 시간 동안 hello 내의 모든 감사 된 이벤트의 레코드가 포함, 마지막 7 일 또는 30 일 이내 그룹 활동 변경 사항 및 암호 재설정 및 등록 활동입니다.

자세한 정보:

* [액세스 및 사용 보고서 보기](../active-directory/active-directory-view-access-usage-reports.md)
* [Azure Active Directory Reporting 시작하기](../active-directory/active-directory-reporting-getting-started.md)
* [Azure Active Directory Reporting 가이드](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>소비자 ID 및 액세스 관리
Azure Active Directory B2C toohundreds 수백만 id의 크기를 조정 하는 소비자 용 응용 프로그램에 대 한 전역, 항상 사용 가능한 id 관리 서비스입니다. 이 서비스는 모바일 및 웹 플랫폼에 통합될 수 있습니다. 소비자 로그온 할 수 tooall 사용자 지정할 수 있는 환경을 통해 응용 프로그램의 기존 소셜 계정을 사용 하 여 하거나 만들어 새 자격 증명.

지난 hello,에서는 응용 프로그램에를 toosign 및 소비자 로그인 하려는 단계는 응용 프로그램 개발자는 고유한 코드를 작성 했습니다. 있고 온-프레미스 데이터베이스 또는 시스템 toostore 사용자 이름 및 암호 사용 않은 것입니다. Azure Active Directory B2C 조직 hello 도움말 응용 프로그램 안전 하 고 표준 기반 플랫폼 및 다양 한 확장 가능한 정책으로는 더 나은 방법은 toointegrate 소비자 id 관리를 제공합니다.

Azure Active Directory B2C를 사용하면 소비자는 기존 소셜 계정(Facebook, Google, Amazon, LinkedIn)을 사용하거나 새 자격 증명(전자 메일 주소 및 암호 또는 사용자 이름 및 암호)을 만들어서 응용 프로그램을 등록할 수 있습니다.

자세한 정보:

* [Azure Active Directory B2C란?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C 미리 보기: 응용 프로그램에 소비자 등록 및 로그인](../active-directory-b2c/active-directory-b2c-overview.md)
* [Azure Active Directory B2C 미리 보기: 응용 프로그램 유형](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>장치 등록
Azure AD Device Registration은 hello foundation에 대 한 장치 기반 [조건부 액세스](../active-directory/active-directory-conditional-access-device-registration-overview.md) 시나리오입니다. 장치를 등록할 때 Azure Active Directory 장치 등록은 hello 사용자가 로그인 할 때 사용 되는 tooauthenticate hello 장치 id가 있는 hello 장치를 제공 합니다. 인증 된 hello 장치와 hello 장치의 hello 특성 수 hello 클라우드 및 온-프레미스에서 호스트 되는 응용 프로그램에 대 한 조건부 액세스 정책을 사용 하는 tooenforce 합니다.

Intune 같은 모바일 장치 관리 (MDM) 솔루션을 함께 사용 하면 Azure Active Directory의 장치 특성이 hello hello 장치에 대 한 추가 정보로 업데이트 됩니다. 이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다.

자세한 정보:

* [Azure Active Directory 장치 등록 시작](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Windows 도메인에 가입된 장치의 Azure Active Directory 자동 장치 등록](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Windows 도메인 가입 장치에 대한 Azure Active Directory 자동 등록 설정](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Azure AD (Active Directory) Privileged Identity Management를 사용 하 여 관리, 제어 및 권한 있는 id 및 Azure AD에서 액세스 tooresources로 Office 365 또는 Microsoft Intune과 같은 다른 Microsoft 온라인 서비스를 모니터링할 수 있습니다.

경우에 따라 사용자는 Azure 또는 Office 365 리소스 또는 다른 SaaS 앱에 권한 있는 작업 toocarry가 필요합니다. 종종 즉, 조직 toogive Azure AD에 해당 영구 권한 액세스 합니다. 조직은 사용자가 관리자 권한으로 수행하는 작업을 충분히 모니터링할 수 없으므로 클라우드에 호스트된 리소스의 보안 위험이 증가합니다. 또한 권한 있는 액세스가 있는 사용자 계정이 손상되면 이로 인해 전반적인 클라우드 보안에 영향을 줄 수 있습니다. Azure AD Privileged Identity Management tooresolve이이 위험을 수 있습니다.

Azure AD Privileged Identity Management를 통해 다음을 할 수 있습니다.

* Azure AD 관리자인 사용자를 확인할 수 있습니다.
* 요청 시 "just in time" Office 365 및 Intune 관리 액세스 tooMicrosoft 온라인 서비스와 같은 사용 하도록 설정
* 관리자 액세스 기록 및 관리자 할당 변경에 대한 보고서 가져오기
* 액세스 tooa 권한 있는 역할에 대 한 경고를 받으려면

자세한 정보:

* [Azure AD 권한 있는 ID 관리](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Azure AD Privileged Identity Management의 역할](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: 어떻게 tooadd 또는 사용자 역할 제거](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>ID 보호
Azure AD ID 보호는 조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공하는 보안 서비스입니다. ID 보호는 기존 Azure Active Directory의 비정상 감지 기능(Azure AD의 비정상적인 작업 보고서를 통해 사용 가능)을 활용하고 실시간으로 잘못된 부분을 검색할 수 있는 새로운 위험 이벤트 유형을 소개합니다.

자세한 정보:

* [Azure Active Directory ID 보호](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD 및 ID 표시: ID 보호 미리 보기](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>하이브리드 ID 관리
Microsoft의 접근 방식 tooidentity 범위 온-프레미스와 클라우드에 hello 위치에 관계 없이 tooall 리소스, 인증 및 권한 부여에 대 한 단일 사용자 id를 만드는 합니다.

자세한 정보:

* [하이브리드 ID 백서](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Active Directory 팀 블로그](https://blogs.technet.microsoft.com/ad/)
