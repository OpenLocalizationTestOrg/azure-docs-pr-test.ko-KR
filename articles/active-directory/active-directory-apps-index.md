---
title: "Azure Active Directory에 응용 프로그램 관리에 대 한 인덱스 aaaArticle | Microsoft Azure"
description: "어떻게 toorenew 인증서는 페더레이션 인증서에 사용 되는 hello 만료 날짜 toocustomize 곧 만료 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스
이 페이지에서는 Azure Active Directory (Azure AD)에 다양 한 응용 프로그램 관련 기능을 hello에 대 한 작성 하는 모든 문서에 대 한 포괄적인 목록을 제공 합니다.

찾고 있는 정보에 따라 어떤 문서 tooread에 대 한 지침 뿐만 아니라는 간략 한 소개 tooeach 주요 기능 영역에서 있습니다.

## <a name="overview-articles"></a>개요 문서
아래 hello 문서 좋은지 시작 사용자에 게 Azure AD 응용 프로그램 관리 기능에 간략하게 설명 하기를 원할 점으로 합니다.

| 문서 가이드 |  |
|:---:| --- |
| Azure AD를 해결 하는 소개 toohello 응용 프로그램 관리 문제 |[Azure Active Directory(AD)와 응용 프로그램 관리](active-directory-enable-sso-scenario.md) |
| Hello에 대 한 개요 tooenabling single sign on, 누가 정의 관련 된 Azure AD의 다양 한 기능 tooapps, 사용자가 앱을 시작 하는 방법 및 액세스 |[Azure Active Directory에서 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md) |
| Azure AD에 앱을 통합할 때 관련 된 hello 다른 단계를 살펴보면 |[Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications-getting-started.md)<br /><br />[Single Sign On tooSaaS 앱을 사용 하도록 설정](active-directory-sso-integrate-saas-apps.md)<br /><br />[액세스 tooApps 관리](active-directory-managing-access-to-apps.md) |
| 앱이 Azure AD에서 나타나는 방법에 대한 기술 정보 |[응용 프로그램을 AD tooAzure 추가 방법과 이유](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>문제 해결 문서
이 섹션에서는 toorelevant 문제 해결 가이드 빠른 액세스를 제공 합니다. 각 기능 영역에 대 한 자세한 내용은이 페이지의 hello 나머지 부분에 있습니다.

| 기능 영역 |  |
|:---:| --- |
| 페더레이션된 Single Sign-On |[SAML 기반 Single Sign-On 문제 해결](active-directory-saml-debugging.md) |
| 암호 기반 Single Sign-On |[Internet Explorer에 대 한 hello 액세스 패널 확장 문제 해결](active-directory-saas-ie-troubleshooting.md) |
| 응용 프로그램 프록시 |[앱 프록시 문제 해결 가이드](active-directory-application-proxy-troubleshoot.md) |
| 온-프레미스 AD 및 Azure AD 간의 Single Sign-On |[암호 동기화 문제 해결](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[비밀번호 쓰기 저장 문제 해결](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| 동적 그룹 멤버 자격 |[동적 그룹 멤버 자격 문제 해결](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>SSO(Single Sign-On)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>페더레이션된 Single Sign-On: 하나의 ID를 사용하여 많은 앱에 로그인
Single sign on 사용자 tooaccess 다양 한 응용 프로그램 및 서비스 자격 증명의 집합을 하나만 사용 하 여 허용 합니다. 페더레이션은 Single Sign-On을 사용할 수 있는 하나의 메서드입니다. 페더레이션된 응용 프로그램에 toosign를 시도할 경우 리디렉션된 tootheir 조직의 공식 로그인 페이지는 Azure Active Directory 힙이고 인증 성공 시 리디렉션된 백 toohello 앱에서 렌더링 받게 됩니다.

| 문서 가이드 |  |
|:---:| --- |
| 소개 toofederation 및 다른 종류의 로그온 |[Azure AD로 Single Sign-On](active-directory-appssoaccess-whatis.md) |
| Single Sign-On 구성 단계로 단순하게 Azure AD와 사전 통합된 수천 개의 SaaS 앱 |[Hello Azure AD 응용 프로그램 갤러리 시작](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[페더레이션을 지원하는 사전 통합된 앱의 전체 목록](http://aka.ms/aadfederatedapps)<br /><br />[어떻게 tooAdd 앱 toohello Azure AD 앱 갤러리](active-directory-app-gallery-listing.md) |
| 어떻게 tooconfigure single sign-on 앱에 대 한 같은 대 한 150 개 이상의 응용 프로그램 자습서 [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md), 등의 많은 |[방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md) |
| Toomanually 설정 하 고 single sign on 구성을 사용자 지정 하는 방법 |[어떻게 tooConfigure tooApps 페더레이션된 Single Sign-on에 없는 hello Azure Active Directory 응용 프로그램 갤러리](active-directory-saas-custom-apps.md)<br /><br />[tooCustomize 클레임 발급 방식 hello Pre-Integrated 앱에 대 한 SAML 토큰](active-directory-saml-claims-customization.md) |
| 문제 해결 hello SAML 프로토콜을 사용 하는 페더레이션된 응용 프로그램에 대 한 가이드 |[SAML 기반 Single Sign-On 문제 해결](active-directory-saml-debugging.md) |
| 어떻게 tooconfigure 앱의 인증서의 만료 날짜와 방법을 toorenew 인증서 |[Azure Active Directory에서 페더레이션된 Single Sign-On에 대한 인증서 관리](active-directory-sso-certs.md) |

페더레이션된 single sign-on 사용자 당 tooten 앱을 위해 Azure AD의 모든 버전에서 사용할 수는 합니다. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 은 응용 프로그램을 무제한 지원합니다. 조직에 있는 경우 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 또는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)를 수 있습니다 [tooassign 액세스 toofederated 응용 프로그램을 그룹화 하는 사용 하 여](#managing-access-to-applications)합니다.

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>암호 기반 Single Sign-On: 페더레이션되지 않은 앱에 대한 계정 공유 및 SSO
tooenable single sign on tooapplications 페더레이션 tooSaaS 앱 암호를 안전 하 게 저장 하 고 자동으로 사용자가 해당 앱에 서명할 수 있는 Azure AD는 암호 관리 기능을 지원 하지 않는 합니다. 새로 만든 계정에 자격 증명을 쉽게 배포하고 팀 계정을 여러 사람과 공유할 수 있습니다. 사용자가 tooknow hello 자격 증명 toohello 계정에 대 한 액세스를 제공 하는 반드시 필요 합니다.

| 문서 가이드 |  |
|:---:| --- |
| 소개 toohow 암호 기반 SSO 작동 및 간략 한 기술 개요 |[Azure AD를 사용한 암호 기반 Single Sign-On](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Hello 시나리오 관련된 tooaccount 공유의 요약 및 Azure AD를 통해 이러한 문제를 해결할 하는 방법 |[Azure AD와 계정 공유](active-directory-sharing-accounts.md) |
| 일정 한 간격으로 특정 앱에 대 한 hello 암호를 자동으로 변경 |[자동화된 암호 롤오버(미리 보기)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| 배포 및 hello Internet Explorer 버전의 Azure AD 암호 관리 확장 hello에 대 한 가이드 문제 해결 |[그룹 정책을 사용 하 여 Internet Explorer에 대 한 tooDeploy 액세스 패널 확장이 hello 하는 방법](active-directory-saas-ie-group-policy.md)<br /><br />[Internet Explorer에 대 한 hello 액세스 패널 확장 문제 해결](active-directory-saas-ie-troubleshooting.md) |

암호 기반 single sign on 사용자 당 tooten 앱을 위해 Azure AD의 모든 버전에서 사용할 수는 있습니다. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 은 응용 프로그램을 무제한 지원합니다. 조직에 있는 경우 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 또는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)를 수 있습니다 [사용 하 여 그룹화 tooassign 액세스 tooapplications](#managing-access-to-applications)합니다. 자동화된 암호 롤오버는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 기능입니다.

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>응용 프로그램 프록시: Single sign on 및 원격 액세스 tooon 온-프레미스 응용 프로그램
Toobe 사용자 및 장치 hello 네트워크 외부에서 액세스 해야 하는 개인 네트워크에서 응용 프로그램의 경우 Azure AD 응용 프로그램 프록시 tooenable 보안 원격 액세스 toothose 앱을 사용할 수 있습니다.

| 문서 가이드 |  |
|:---:| --- |
| Azure AD 응용 프로그램 프록시 및 작동 방식 개요 |[Tooon 온-프레미스 응용 프로그램 보안 된 원격 액세스를 제공합니다.](active-directory-application-proxy-get-started.md) |
| 방법에 대 한 자습서 응용 프로그램 프록시 tooconfigure 방법과 toopublish 첫 응용 프로그램 |[어떻게 tooSet Azure AD 응용 프로그램 프록시를](active-directory-application-proxy-enable.md)<br /><br />[TooSilently 설치 응용 프로그램 프록시 커넥터를 hello 하는 방법](active-directory-application-proxy-silent-installation.md)<br /><br />[어떻게 tooPublish 응용 프로그램 프록시를 사용 하 여 응용 프로그램](active-directory-application-proxy-publish.md)<br /><br />[어떻게 tooUse 사용자의 도메인 이름 지정](active-directory-application-proxy-custom-domains.md) |
| 응용 프로그램 프록시를 사용 하 여 게시 방법 tooenable single 앱에 대 한 로그온 및 조건부 액세스 |[앱 프록시를 사용하는 Single-Sign-On](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[조건부 액세스 및 응용 프로그램 프록시](active-directory-application-proxy-conditional-access.md) |
| 방법에 대 한 지침 hello 다음 시나리오에 대 한 응용 프로그램 프록시 toouse |[어떻게 tooSupport 네이티브 클라이언트 응용 프로그램](active-directory-application-proxy-native-client.md)<br /><br />[어떻게 tooSupport 클레임 인식 응용 프로그램](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[별도 네트워크 위치에 tooSupport 응용 프로그램을 게시 하는 방법](active-directory-application-proxy-connectors.md) |
| 응용 프로그램 프록시에 대한 문제 해결 가이드 |[앱 프록시 문제 해결 가이드](active-directory-application-proxy-troubleshoot.md) |

응용 프로그램 프록시는 사용자 당 tooten 앱을 위해 Azure AD의 모든 버전에서 사용할 수 있습니다. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 은 응용 프로그램을 무제한 지원합니다. 조직에 있는 경우 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 또는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)를 수 있습니다 [사용 하 여 그룹화 tooassign 액세스 tooapplications](#managing-access-to-applications)합니다.

에 관심이 있을 수 [Azure AD 도메인 서비스](../active-directory-domain-services/active-directory-ds-overview.md), 있습니다 toomigrate 프로그램 온-프레미스 응용 프로그램 tooAzure 여전히 hello identity를 만족 하는 동안 해당 응용 프로그램의 필요성을 해결 합니다.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Azure AD와 온-프레미스 AD 간에 Single Sign-On 사용
조직이 온-프레미스 hello 클라우드에서 Azure Active Directory와 함께 Windows Server Active Directory를 관리 하는 경우 다음 설정할 수 있습니다 tooenable single sign on이 두 시스템 간의 합니다. Single sign on을 설정 하기 위한 여러 옵션을 제공 하는 azure AD Connect (함께이 두 시스템을 통합 하는 hello 도구): ad FS 또는 기타 페더레이션 공급자와의 페더레이션을 설정할 또는 암호 동기화를 사용 합니다.

| 문서 가이드 |  |
|:---:| --- |
| 하이브리드 환경 관리에 대 한 정보를 비롯 하 여 Azure AD Connect에 제공 하는 hello single sign on 옵션에 대 한 개요 |[Azure AD Connect의 사용자 로그온 옵션](active-directory-aadconnect-user-signin.md) |
| 온-프레미스 Active Directory 및 Azure Active Directory로 환경을 관리하기 위한 일반적인 지침  |[Azure AD 하이브리드 ID 설계 고려 사항](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md) |
| 암호 동기화 tooenable SSO를 사용 하 여에 대 한 지침 |[Azure AD Connect와 암호 동기화 구현](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[암호 동기화 문제 해결](https://support.microsoft.com/en-us/kb/2855271) |
| 암호 쓰기 저장 tooenable SSO를 사용 하 여에 대 한 지침 |[Azure AD에서 암호 관리 시작](active-directory-passwords-getting-started.md)<br /><br />[비밀번호 쓰기 저장 문제 해결](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| 제 3 자 identity 공급자 tooenable SSO를 사용 하 여에 대 한 지침 |[Single Sign On tooEnable 호환 타사 Id 공급자를 사용할 수 있습니다 수의 목록](https://aka.ms/ssoproviders) |
| Windows 10 사용자가 single sign-on의 Azure AD Join을 통해 hello 혜택을 이용할 수는 방법 |[Azure Active Directory Join을 통해 장치를 10 tooWindows 클라우드 기능 확장](active-directory-azureadjoin-overview.md) |

Azure AD Connect는 [모든 버전의 Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)에 사용할 수 있습니다. Azure AD 셀프 서비스 암호 재설정은 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 및 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)에 사용할 수 있습니다. 암호 쓰기 저장 tooon 온-프레미스 AD는는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 기능입니다.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>조건부 액세스: 위험도 높은 앱에 대한 추가 보안 요구 사항 적용
Single sign on tooyour 앱 및 리소스를 설정 하면 다음 보안을 강화할 수 중요 한 응용 프로그램 로그인 toothat는 모든 앱에 특정 보안 요구 사항을 적용 하 여 합니다. 예를 들어, 모든 액세스 tooa 특정 앱에 항상 이러한 앱 기능을 하는 아주 지원 되는 여부에 관계 없이 multi-factor authentication을 요구 하는 Azure AD toodemand를 사용할 수 있습니다. 조건부 액세스의 또 다른 일반적인 예 toorequire 있는 사용자 수 연결된 toohello 조직의 신뢰할 수 있는 네트워크 순서 tooaccess에 특히 중요 한 응용 프로그램입니다.

| 문서 가이드 |  |
|:---:| --- |
| Azure AD에서 제공 되는 소개 toohello 조건부 액세스 기능을 office 365 및 Intune |[조건부 액세스를 사용한 위험 관리](active-directory-conditional-access.md) |
| 다음 유형의 리소스 hello에 대 한 tooenable 조건부 액세스 하는 방법 |[SaaS 앱에 대한 조건부 액세스](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Office 365 서비스에 대한 조건부 액세스](active-directory-conditional-access-device-policies.md)<br /><br />[온-프레미스 응용 프로그램에 대한 조건부 액세스](active-directory-conditional-access.md)<br /><br />[Azure AD 앱 프록시를 통해 게시된 온-프레미스 응용 프로그램에 대한 조건부 액세스](active-directory-application-proxy-conditional-access.md) |

| 방법에서 Azure Active Directory를 사용 하 여 tooregister 장치 정렬 tooenable 장치 기반 조건부 액세스 정책 | [Azure Active Directory 장치 등록의 개요](active-directory-conditional-access-device-registration-overview.md)<br /><br />[어떻게 tooEnable 도메인 가입 된 Windows 장치에 대해 자동 장치 등록](active-directory-conditional-access-automatic-device-registration.md)<br />- [Windows 8.1 장치에 대한 단계](active-directory-conditional-access-automatic-device-registration-setup.md)<br />- [Windows 7 장치에 대한 단계](active-directory-conditional-access-automatic-device-registration-setup.md) |

| 어떻게 toouse hello 2 단계 인증에 대 한 Microsoft Authenticator 앱 | [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

조건부 액세스는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 기능입니다.

## <a name="apps--azure-ad"></a>앱 및 Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>클라우드 앱 검색: 조직에서 사용된 SaaS 앱 찾기
Cloud App Discovery hello 조직 전반에 걸쳐 있는 SaaS 앱을 사용 하는 IT 부서는 데 도움이 됩니다. 앱 사용을 측정할 수 못하고 인기도 한다는 없도록 가장 hello 효과 얻을 수 있는 앱을 결정할 수 있도록 IT 제어 및 Azure AD와 통합 되 고 있습니다.

| 문서 가이드 |  |
|:---:| --- |
| 작동 방법의 일반적인 개요 |[클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md) |
| 이 작동 하는 방법, 개인 정보에 대 한 답변 tooquestions에 자세히 알아보려면 |[보안 및 개인정보 취급 방침 고려 사항](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| 질문과 대답 |[클라우드 앱 검색에 대한 FAQ](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Cloud App Discovery를 배포하기 위한 자습서 |[그룹 정책 배포 가이드](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[System Center 배포 가이드](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[사용자 지정 포트로 프록시 서버에 설치](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| hello 변경 toohello Cloud App Discovery 에이전트 업데이트에 대 한 로그 |[변경 로그](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 기능입니다.

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>SaaS 앱에서 사용자 계정 자동으로 프로비전 및 프로비전 해제
Hello 만들고 유지 관리, Dropbox, Salesforce, ServiceNow, 등과 같은 SaaS 응용 프로그램의 사용자 id의 제거를 자동화 합니다. 일치와 Azure AD 사이 있는 기존 id 동기화 및 SaaS 앱 및 사용자가 hello 조직을 떠날 때 계정을 자동으로 비활성화 하 여 액세스를 제어 합니다.

| 문서 가이드 |  |
|:---:| --- |
| 작동 방법에 대해 알아보고 toocommon 질문 답변을 찾을 |[사용자 프로 비전 및 프로 비전 해제 tooSaaS 응용 프로그램 자동화](active-directory-saas-app-provisioning.md) |
| Azure AD와 SaaS 앱 간에 매핑되는 정보 방식 구성 |[특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)<br><br>[특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Tooenable는 hello SCIM 프로토콜을 지 원하는 tooany 앱 프로 비전을 자동화 하는 방법을 |[자동 사용자 프로 비전 tooany SCIM-Enabled 응용 프로그램 설정](active-directory-scim-provisioning.md) |
| 방법에 대 한 tooreport 및 사용자 프로 비전 문제 해결 |[자동 사용자 프로비전 보고](active-directory-saas-provisioning-reporting.md)<br><br>[프로비전 알림](active-directory-saas-account-provisioning-notifications.md)<br><br>[사용자 프로비전 문제 해결](active-directory-application-provisioning-content-map.md) |
| 해당 특성 값에 따라 프로 비전 된 tooan 응용 있는 사람 제한 |[범위 지정 필터](active-directory-saas-scoping-filters.md) |

자동된 사용자 프로 비전 하는 것은 사용자 당 tooten 앱을 위해 Azure AD의 모든 버전에서 사용할 수 있습니다. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 은 응용 프로그램을 무제한 지원합니다. 조직에 있는 경우 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 또는 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)를 수 있습니다 [그룹 toomanage 있는 사용자 프로 비전을 사용 하 여](#managing-access-to-applications)합니다.

### <a name="building-applications-that-integrate-with-azure-ad"></a>Azure AD와 통합되는 응용 프로그램 작성
응용 프로그램 개발자는 Azure Active Directory를 사용 하는 고객 인 경우 hello 다음 자습서는 데 도움이 됩니다 또는 조직이 개발 하거나 기간 업무 (LoB) 응용 프로그램 유지 관리 하는 경우 Azure AD와 응용 프로그램을 통합 합니다.

| 문서 가이드 |  |
|:---:| --- |
| Azure AD와 앱 통합에 대한 IT 전문가 및 응용 프로그램 개발자를 위한 지침 |[Azure AD에 대 한 응용 프로그램 개발에 대 한 hello IT 전문가 가이드](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Azure Active Directory에 대 한 hello 개발자 가이드](active-directory-developers-guide.md) |
| Tooapplication 공급 업체 추가 하려면 어떻게 해야 자신의 앱 toohello Azure AD 앱 갤러리 |[Hello Azure Active Directory 응용 프로그램 갤러리에서에서 응용 프로그램 나열](active-directory-app-gallery-listing.md) |
| Toomanage는 toodeveloped 응용 프로그램에 Azure Active Directory를 사용 하 여 액세스 하는 방법 |[어떻게 tooEnable 개발 된 응용 프로그램에 대 한 사용자 할당](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[사용자가 tooyour 응용 프로그램 할당](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[할당 그룹 tooyour 응용 프로그램](active-directory-applications-guiding-developers-assigning-groups.md) |

소비자 용 응용 프로그램을 개발 하는 경우 사용 하 여에 관심이 있을 수 [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) 를 toodevelop 고유한 identity 시스템 toomanage 않아도 사용자가 있습니다. [자세히 알아봅니다](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>액세스 tooApplications 관리
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>그룹 및 toowhich 앱 액세스를 가진 toomanage 셀프 서비스를 사용 하 여
toohelp 관리 toowhich 리소스에 액세스할 수 있어야 하, Azure Active Directory에 한 있습니다 tooset 할당 및 권한 그룹을 사용 하 여 배율을 합니다. IT tooenable 필요할 때 사용자가 권한을 요청할 단순히 수 있도록 셀프 서비스 기능 선택할 수 있습니다.

| 문서 가이드 |  |
|:---:| --- |
| Azure AD 액세스 관리 기능의 개요 |[소개 tooManaging 액세스 tooApps](active-directory-managing-access-to-apps.md)<br /><br />[Azure AD에서 액세스 관리가 작동하는 방식](active-directory-manage-groups.md)<br /><br />[어떻게 tooUse 그룹 tooManage 액세스 tooSaaS 응용 프로그램](active-directory-accessmanagement-group-saasapps.md) |
| 앱 및 그룹의 셀프 서비스 관리 사용 |[셀프 서비스 응용 프로그램 관리](active-directory-self-service-application-access.md)<br /><br />[셀프 서비스 그룹 관리](active-directory-accessmanagement-self-service-group-management.md) |
| Azure AD에서 그룹을 설정하기 위한 지침 |[어떻게 tooCreate 보안 그룹](active-directory-accessmanagement-manage-groups.md)<br /><br />[어떻게 tooDesignate 그룹 소유자](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[어떻게 tooUse hello "모든 사용자" 그룹](active-directory-accessmanagement-dedicated-groups.md) |
| 사용 하 여 동적 그룹 tooautomatically 특성 기반 멤버 관리 규칙을 사용 하 여 그룹 멤버 자격을 채웁니다. |[동적 그룹 구성원: 고급 규칙](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[동적 그룹 멤버 자격 문제 해결](active-directory-accessmanagement-troubleshooting.md) |

그룹 기반 응용 프로그램 액세스 관리는 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 및 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)에 사용할 수 있습니다. 셀프 서비스 그룹 관리, 셀프 서비스 응용 프로그램 관리 및 동적 그룹은 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 기능입니다.

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>B2B 공동 작업: 파트너 액세스 tooapplications 사용 하도록 설정
비즈니스는 다른 회사와 협력 했습니다, 경우 toomanage 파트너 액세스 tooyour 회사 응용 프로그램 해야 할 수 있습니다. Azure Active Directory B2B 공동 작업 간편 하 고 안전한 tooshare 파트너와 응용 프로그램을 제공합니다.

| 문서 가이드 |  |
|:---:| --- |
| 다른 Azure AD의 개요는 파트너, 고객 등 외부 사용자를 관리할 수 있는 기능을 갖추고 있습니다. |[Azure AD에서 외부 ID 관리 기능 비교](active-directory-b2b-compare-external-identities.md) |
| 소개 tooB2B 공동 작업 및 tooget 시작 하는 방법 |[Azure AD와 간단하고 안전한 클라우드 통합](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Azure Active Directory B2B 공동 작업](active-directory-b2b-collaboration-overview.md) |
| Azure AD B2B 공동 작업에 자세히 알아보려면 방법과 toouse 것 |[B2B 공동 작업: 작동 방식](active-directory-b2b-how-it-works.md)<br /><br />[Azure AD B2B 공동 작업의 현재 제한 사항](active-directory-b2b-current-limitations.md)<br /><br />[Azure AD B2B 공동 작업 사용에 대한 자세한 연습](active-directory-b2b-detailed-walkthrough.md) |
| Azure AD B2B 공동 작업의 작동 방법에 대한 기술 세부 정보가 포함된 참조 문서 |[파트너 사용자를 추가하기 위한 CSV 파일 형식](active-directory-b2b-references-csv-file-format.md)<br /><br />[Azure AD B2B 공동 작업의 영향을 받는 사용자 특성](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[파트너 사용자에 대한 사용자 토큰 형식](active-directory-b2b-references-external-user-token-format.md) |

B2B 공동 작업은 현재 [모든 Azure Active Directory 버전](https://azure.microsoft.com/pricing/details/active-directory/)에 사용할 수 있습니다.

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>액세스 패널: 앱 및 셀프 서비스 기능에 액세스하기 위한 포털
Azure AD 액세스 패널 hello 여기서 최종 사용자가 시작할 수의 앱 및 액세스 hello 셀프 서비스 기능 toomanage 수 있게 하는 해당 응용 프로그램 및 그룹 멤버 자격입니다. 또한 toohello 액세스 패널을 SSO 지원 응용 프로그램에 액세스 하기 위한 다른 옵션은 아래 hello 목록에 포함 됩니다.

| 문서 가이드 |  |
|:---:| --- |
| Single sign-on 앱 toousers를 배포 하는 데 사용할 수 있는 다른 옵션 hello 비교 |[Azure AD 통합 응용 프로그램 tooUsers 배포](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Hello 액세스 패널 및 해당 모바일 해당 MyApps 개요 |[소개 tooAccess 패널과 MyApps](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Tooaccess Azure AD 앱에서 Office 365 웹 사이트를 hello 하는 방법 |[Hello Office 365 앱 시작 관리자를 사용 하 여](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Tooaccess Azure AD 앱에서 모바일 앱을 Intune Managed Browser hello 하는 방법 |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Azure AD tooaccess 앱 딥 링크 tooinitiate를 사용 하 여 단일 로그온 방법 |[직접 링크 로그온 tooYour 앱 가져오기](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

액세스 패널은 [모든 버전의 Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)에 사용할 수 있습니다.

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>: 보고서에서 쉽게 응용 프로그램은 액세스 변경을 감사 하 고 로그인 속도가 tooapps 모니터링
Azure Active Directory toohelp 경고와 여러 가지 보고서를 제공 하면 조직의 액세스 tooapplications를 모니터링 합니다. 비정상적인 로그인 tooyour 앱에 대 한 경고를 받을 수와 시기와 사용자의 액세스 tooan 응용 프로그램이 변경 된 이유를 추적할 수 있습니다.

| 문서 가이드 |  |
|:---:| --- |
| Hello Azure Active Directory에 보고 기능에 대 한 개요 |[Azure AD Reporting 시작](active-directory-reporting-getting-started.md) |
| 로그인 및 사용자의 응용 프로그램 사용 현황 toomonitor hello 하는 방법 |[액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md) |
| 변경 내용 추적 toowho 내용을 특정 응용 프로그램에 액세스할 수 있습니다. |[Azure Active Directory 감사 보고서 이벤트](active-directory-reporting-audit-events.md) |
| 이러한 보고서 tooyour 기본 도구를 사용 하 여 내보내기 hello 데이터 hello Reporting API |[Azure AD Reporting API hello 시작](active-directory-reporting-api-getting-started.md) |

Azure Active Directory의 다른 버전에 포함 되어 있는 보고서가 toosee [여기를 클릭](active-directory-view-access-usage-reports.md)합니다.

## <a name="see-also"></a>참고 항목
[Azure Active Directory란?](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Azure Active Directory 도메인 서비스](https://azure.microsoft.com/services/active-directory-ds/)

[Azure Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)
