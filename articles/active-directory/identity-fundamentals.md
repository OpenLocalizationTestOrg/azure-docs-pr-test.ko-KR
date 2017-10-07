---
title: "Azure id 관리 aaaFundamentals | Microsoft Docs"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Azure ID 관리의 기초
Hello 회사 네트워크, 클라우드의 hello 및 장치에서 외부 점점 더 많은 회사 디지털 리소스 실시간 뛰어난 클라우드 기반 id 및 액세스 관리 솔루션은 반드시 필요를 되 고 있습니다. 클라우드 기반 id는 이제 hello 가장 좋은 방법은 toomaintain 컨트롤 및 사용자가 회사 응용 프로그램과 데이터 액세스 방법 및 시기에 대 한 가시성을 합니다.

Microsoft가 되었습니다 및 보안 설정에 대 한 클라우드 기반 id 10 년 이상 이제와 [Azure AD (Active Directory)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), 이러한 동일한 보호 시스템은 사용 가능한 tooyou 합니다. 엔터프라이즈 관리자는 Azure AD를 통해 이전보다 더 우수한 보안 및 관리 기능으로 사용자 및 관리자의 책임을 쉽게 확인할 수 있습니다.

Azure AD Premium는 클라우드 기반 id 및 액세스 관리 솔루션으로 고급 보호 기능이 있는 모든 앱, 식별 정보 보호에 대 한 하나의 보안 id 수 있도록 (hello 여 보기 좋게 꾸밀 [Microsoft intelligence 보안 그래프](https://www.microsoft.com/en-us/security/intelligence)), Privileged Identity Management 및 합니다. 단지 다른 모니터링 또는 보고 도구, Azure AD Premium 사용자의 id를 실시간으로 보호 하 고 사용 하도록 설정 하면 toocreate 위험 기반 적응형에 대 한 액세스 정책을 tooprotect 조직의 데이터 수입니다.

다음 짧은 비디오에서 Azure AD ID 관리 및 보호에 대한 간략한 개요를 살펴보세요.
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft 뿐 아니라 모든 위치에서 이동 하는 id를 제공 하지만 또한, 보호 및 관리 도구 tooautomate 집합이 IT 조직 내에서. 클라우드 컴퓨팅 여전히 toomanage 요구 및 기술 지원팀 호출 tooreset 사용자 암호와 같은 IT 작업을 제어 hello 등장, 후에 사용자 관리 및 응용 프로그램 요청을 그룹화 합니다. 작업을 더욱 하므로 복잡해 집니다, 직원 이제 자신의 개인 장치 toowork를 가져와 쉽게 사용할 수 있는 SaaS 응용 프로그램을 사용 합니다. 따라서 회사 데이터 센터 및 공용 클라우드 플랫폼 간에 자사 응용 프로그램에 대한 제어를 유지하는 것이 중요한 과제입니다.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Azure AD 및 Office 365를 사용하여 온-프레미스 Active Directory 연결
온-프레미스 Active Directory에 대규모 투자를 보낸 조직에 Azure AD와 온-프레미스 디렉터리를 통합 하 여 이러한 투자 toohello 클라우드를 확장할 수 [하이브리드 id 관리](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)합니다. 이렇게 하면 사용자가 위치에 관계 없이 리소스에 액세스하기 위한 공통의 ID를 제공하여 더욱 생산성을 높일 수 있습니다. 사용자 및 조직의 single sign-on (SSO) tooaccess 사용 하 여 온-프레미스 리소스 그런 다음 수 및 클라우드 Office 365와 같은 서비스.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) 는 hello 유일한 도구 tooget hello 통합을 수행 해야 합니다. Azure AD Connect 제공 기능 toosupport id 동기화 필요 하 고 이전 버전의 디렉터리 동기화 및 Azure AD Sync 같은 identity 통합 도구를 대체 합니다. Azure AD Connect를 사용하면 다음을 통해 온-프레미스와 Azure AD 간의 ID 관리 및 동기화가 가능합니다.

- 동기화 - 이 구성 요소는 사용자, 그룹 및 기타 개체 생성을 담당합니다. 온-프레미스 사용자 및 그룹에 대 한 id 정보에는 hello 클라우드 일치 하는 확인할 책임이 이기도 합니다. 사용자가 Azure AD에서 자신의 암호를 업데이트할 때 암호 쓰기 저장 사용된 tookeep 온-프레미스 디렉터리 동기화를 수도 있습니다.
- AD FS에서 페더레이션에 사용 되는 온-프레미스를 사용 하는 하이브리드 환경 tooconfigure 일 수 있는 Azure AD Connect에서 제공 하는 선택적 기능 AD FS 인프라입니다. 페더레이션 single sign-on, 스마트 카드 또는 제 3 자 MFA 및 AD 로그인 정책 적용 등 조직 tooaddress 복잡 한 배포를 사용할 수 있습니다.
- 상태 모니터링- [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) 강력한 모니터링을 제공 하 고이 작업을 중앙 위치에서 Azure 포털 tooview hello 제공할 수 있습니다.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>셀프 서비스 및 Single Sign-On 환경으로 생산성 향상 및 헬프데스크 비용 절감

직원은 단일 사용자 이름 및 암호 tooremember 및 모든 장치에서 일관 된 환경을 포함 하는 경우 생산성을 높일 있습니다. 시간을 절약할 수도 수행할 수 있는 시기 등의 셀프 서비스 작업 [잊어버린된 암호를 재설정](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) 하거나 hello 기술 지원팀의 도움이 될 때까지 기다리지 않고 tooan 응용 프로그램 액세스를 요청 합니다.

Azure AD [온-프레미스 Active Directory 확장](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) hello 클라우드로 사용 하면 사용자가 toouse가 도메인에 가입 된 장치, 회사 리소스 및 모두 hello 웹 및 SaaS 응용 프로그램에 대 한 기본 자신의 조직 계정을 있습니다 toouse tooget가 작업을 수행 해야 합니다. 또한 여러 집합이 사용자 이름 및 암호, 사용자의 응용 프로그램 액세스도 자동으로 프로 비전 (하거나 수 프로 비전 해제) tooremember 필요 toonot 직원으로 조직 그룹 멤버 자격 및 해당 상태에 따라 합니다. 갤러리 앱 또는 개발 하 고 hello를 통해 게시 하는 온-프레미스 앱에 대 한 액세스를 제어할 수 있는 [Azure AD 응용 프로그램 프록시](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)합니다.

## <a name="manage-and-control-access-toocorporate-resources"></a>관리 및 toocorporate 리소스에 액세스를 제어 합니다.
Microsoft id 및 액세스 관리 솔루션 도움말 IT 액세스 tooapplications와 리소스를 보호 및 hello 클라우드로 hello 회사 데이터 센터에서와 같은 추가 수준의 유효성 검사를 사용 하도록 설정 [다단계인증](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) 및 [조건부 액세스 정책을](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)합니다. 고급 보안 보고, 감사 및 경고를 통해 의심스러운 작업을 모니터링하여 잠재적인 보안 문제를 완화시킵니다.

Azure AD Premium에서 조건부 액세스 정책을 사용 하면, 엔터프라이즈 관리자 hello, hello 모든 Azure AD에 연결 된 응용 프로그램 (SaaS 앱, hello 클라우드 또는 온-프레미스 웹 응용 프로그램에서 실행 되는 사용자 지정 앱)에 대 한 기능 toocreate 정책 기반의 액세스 규칙. Azure AD는 실시간으로 이러한 정책은 평가 하 고 적용 하는 사용자가 tooaccess 때마다 응용 프로그램. Azure id 보호 정책을 사용 하면 조치를 취하고 tooautomatically 의심 스러운 활동이 발견 되 면, 합니다. 이러한 작업에 multi-factor authentication 적용 위험 수준이 높은 액세스 toousers 차단 포함할 수 있으며, 손상 된 경우 다음과 같이 자격 증명 재설정 하는 중 사용자 암호입니다.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), Azure Active Directory 프리미엄 P2 hello에 포함 된 제품을 사용 하면 toodiscover, 제한, 하 고 관리 계정 및 해당 액세스 tooresources Azure Active Directory 및 기타 모니터링 Microsoft 온라인 서비스입니다. 필요한 시간을 정확 하 게 기간 hello에 대 한 요청에 대 한 관리 액세스를 관리 하는 데에 데 도움이 됩니다.

Privileged Identity Management 관리자가 다단계 인증, 임시 해당 권한 상승을 미리 구성 된 기간 동안 자신의 계정을 tooa 일반 반환 전에 요청할 수 있도록 주문형으로 관리자 권한을 적용할 수 있습니다. 사용자 상태입니다.

## <a name="benefits-of-azure-identity"></a>Azure ID의 이점

Azure ID 관리를 통해 다음을 수행할 수 있습니다.

-   엔터프라이즈 전체에서 각 사용자에 대한 단일 ID를 만들고 관리하여 사용자, 그룹 및 장치를 [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)와 동기화된 상태로 유지합니다.

-   수천 개의 미리 통합 된 SaaS 응용 프로그램을 포함 하 여 tooyour 응용 프로그램 single sign-on 액세스를 제공 하거나 tooon 온-프레미스 SaaS 응용 프로그램 hello를 사용 하 여 보안 된 원격 액세스를 제공할 [Azure AD 응용 프로그램 프록시](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)합니다.

-   온-프레미스 및 클라우드 응용 프로그램 모두에 대해 규칙 기반 [Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)을 적용하여 응용 프로그램 액세스 보안을 사용하도록 설정합니다.

-   사용 하 여 사용자 생산성 향상 [셀프 서비스 암호 재설정](https://docs.microsoft.com/azure/active-directory/active-directory-passwords), 그룹 및 hello를 사용 하 여 요청에 액세스 하는 응용 프로그램 및 [MyApps 포털](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help)합니다.

-   Hello 활용 [높은 가용성 및 안정성](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) 전 세계 엔터프라이즈급의 클라우드 기반 id 및 액세스 관리 솔루션입니다.

## <a name="next-steps"></a>다음 단계
[Azure ID 솔루션에 대한 자세한 정보](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)