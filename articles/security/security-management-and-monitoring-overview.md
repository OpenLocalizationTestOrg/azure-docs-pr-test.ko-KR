---
title: "aaaAzure 보안 관리 및 모니터링 개요 | Microsoft Docs"
description: " Azure 보안 메커니즘 tooaid hello 관리 및 Azure 클라우드 서비스 및 가상 컴퓨터의 모니터링을 제공 합니다.  이 문서에서는 이러한 핵심 보안 기능 및 서비스에 대한 개요를 제공합니다. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Azure 보안 관리 및 모니터링 개요
Azure 보안 메커니즘 tooaid hello 관리 및 Azure 클라우드 서비스 및 가상 컴퓨터의 모니터링을 제공 합니다. 이 문서에서는 이러한 핵심 보안 기능 및 서비스에 대한 개요를 제공합니다. 링크의 각 세부 정보를 자세히 확인할 수 있도록 제공 하는 tooarticles를 제공 됩니다.

Microsoft 클라우드 서비스의 보안을 hello은 파트너 관계 및 사용자와 Microsoft 간에 공유 해야 합니다. 연대 (잠긴된 배지 항목 문, 울타리 및 가드와 같은 보안 보호 기능 사용)에서 Microsoft는 Microsoft Azure hello와의 데이터 센터의 물리적 보안에 대 한 책임을 의미 합니다. 또한 Azure는 강력한 클라우드에서 수준의 보안 hello 보안, 개인 정보 및 까다로운 고객의 규정 준수 요구를 충족 하는 hello 소프트웨어 계층을 제공 합니다.

사용자 데이터 및 identities, 보호, 온-프레미스 리소스의 보안을 hello 및 사용자가 제어 하는 클라우드 구성의 보안을 hello에 대 한 hello 책임을 소유 합니다. Microsoft 제공 보안 컨트롤 및 기능 toohelp 사용 하면 데이터 및 응용 프로그램을 보호할 합니다. 보안에 대 한 책임 게임의 hello 유형의 클라우드 서비스를 기반으로 합니다.

다음 차트 hello Microsoft와 hello 고객에 대 한 책임의 hello 균형을 요약 합니다.

![공동 책임][1]

보안 관리에 대해 더 자세히 알아보려면 [Azure의 보안 관리](azure-security-management.md)를 참조하세요.

이 문서에서 다루는 hello 코어 기능 toobe 다음과 같습니다.

* 역할 기반 액세스 제어
* 맬웨어 방지
* Multi-Factor Authentication
* Express 경로
* 가상 네트워크 게이트웨이
* Privileged Identity Management
* ID 보호
* 보안 센터

## <a name="role-based-access-control"></a>역할 기반 액세스 제어
RBAC(역할 기반 액세스 제어)를 통해 Azure 리소스에 대한 세밀한 액세스 관리가 가능합니다. RBAC를 사용 하 여 부여할 수 있습니다 사람 hello 양의 데이터만 필요 하다는 tooperform 업무 액세스.  RBAC는 사용자 hello 조직 나갈 때 잃게 hello 클라우드에서 액세스 tooresources 있는지 확인할 수을 유용할 수 있습니다.

자세한 정보:

* [RBAC의 Active Directory 팀 블로그](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>맬웨어 방지
Azure를 통해 Microsoft, Symantec, Trend Micro McAfee 등의 주요 보안 공급 업체의 맬웨어 방지 소프트웨어를 사용할 수 있습니다 및 Kaspersky toohelp 가상 컴퓨터를 악의적인 파일, 애드웨어, 및 기타 위협 으로부터 보호 합니다.

Microsoft 맬웨어 방지 기능 tooinstall PaaS 역할 및 가상 컴퓨터 모두에 대 한 맬웨어 방지 에이전트 hello를 제공 합니다. System Center Endpoint Protection에 따라,이 기능은 실행가 검증 된 온-프레미스 보안 기술 toohello 클라우드 됩니다.

추세의에 대 한 완벽 한 통합 제공 [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ 및 [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ hello Azure 플랫폼의에서 제품입니다. DeepSecurity는 바이러스 백신 솔루션이며 SecureCloud는 암호화 솔루션입니다. DeepSecurity는 확장 모델을 사용하여 VM 내부에 배포됩니다. Hello 포털 UI 및 PowerShell을 사용 하 여, 생성 되는 새 Vm 또는 이미 배포 된 기존 Vm 내부 DeepSecurity toouse를 선택할 수 있습니다.

SEP(Symantec End Point Protection)도 Azure에서 지원됩니다. 포털 통합을 통해 고객은 VM 내에서 9 월 toouse를 추가할지 여부를 지정할 수 있습니다. 9 월 hello Azure 포털을 통해 새 VM에 설치할 수 있습니다 또는 PowerShell을 사용 하 여 기존 VM에 설치할 수 있습니다.

자세한 정보:

* [Azure 가상 컴퓨터에 맬웨어 방지 솔루션 배포](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Azure Cloud Services 및 Virtual Machines용 Microsoft 맬웨어 방지 프로그램](azure-security-antimalware.md)
* [어떻게 tooinstall 및 서비스로 Windows VM에서 Trend Micro Deep Security 구성](../virtual-machines/windows/classic/install-trend.md)
* [어떻게 tooinstall Windows VM에서 Symantec Endpoint Protection을 구성 하 고](../virtual-machines/windows/classic/install-symantec.md)
* [Azure 가상 컴퓨터에 대한 새로운 맬웨어 방지 옵션 - McAfee Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure multi-factor authentication (MFA)은 확인 방법을 두 개 이상 hello 사용 해야 하 고 보안 toouser 로그인 및 트랜잭션에 중요 한 두 번째 계층을 추가 하는 인증 방법입니다. MFA 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다. 전화 통화, 문자 메시지 또는 모바일 앱 알림 또는 확인 코드 및 타사 OATH 토큰과 같은 다양한 확인 옵션을 통해 강력한 인증을 전달합니다.

자세한 정보:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure Multi-Factor Authentication 작동 방법](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>Express 경로
Microsoft Azure ExpressRoute를 사용 하면 연결 공급자를 통해 지원 되는 전용된 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장할 수 있습니다. ExpressRoute를 사용 Microsoft Azure, Office 365, CRM Online과 같은 연결 tooMicrosoft 클라우드 서비스를 설정할 수 있습니다. 공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다. ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 이렇게 하면 express 경로 연결 toooffer 안정성, 빨라진 속도, 낮은 대기 시간, 및 일반 연결 보다 보안성이 높으며 더 많은 hello 인터넷을 통해.

자세한 정보:

* [Express 경로 기술 개요](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>가상 네트워크 게이트웨이
또한 Azure 가상 네트워크 게이트웨이 호출 하는 VPN 게이트웨이 사용 되 toosend 네트워크 트래픽을 가상 네트워크와 온-프레미스 위치입니다. 또한 Azure (VNet 대 VNet) 내에서 여러 가상 네트워크 간에 사용 되는 toosend 트래픽을 구분 됩니다.  VPN 게이트웨이는 Azure와 인프라 사이의 안전한 프레미스 간 연결을 제공합니다.

자세한 정보:

* [VPN 게이트웨이 정보](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Azure 네트워크 보안 개요](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
경우에 따라 사용자는 Azure 리소스 또는 다른 SaaS 응용 프로그램에서 권한 있는 작업 toocarry가 필요합니다. 종종 즉, 조직 toogive Azure Active Directory (Azure AD)에 해당 영구 권한 액세스 합니다. 조직은 사용자가 권한 있는 액세스 권한으로 수행하는 작업을 충분히 모니터링할 수 없으므로 클라우드에 호스트된 리소스의 보안 위험이 증가합니다.
또한 권한 있는 액세스가 있는 사용자 계정이 손상되면 이로 인해 전반적인 클라우드 보안에 영향을 줄 수 있습니다. Azure AD Privileged Identity Management tooresolve이이 위험 권한 hello 노출 시간 단축 및 사용에 대 한 가시성을 증가 하 여 수 있습니다.  

Privileged Identity Management 역할 또는 "just in time" 관리자 접근 toocomplete는 정품 인증 프로세스에 대 한 역할 할당 필요로 하는 사용자에 대 한 임시 admin hello 개념을 소개 합니다. hello 정품 인증 프로세스 변경 내용을 hello 8 시간 등 지정 된 시간 동안 비활성 tooactive에서 Azure AD에서 hello 사용자 tooa 역할의 할당 합니다.

자세한 정보:

* [Azure AD 권한 있는 ID 관리](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Azure AD Privileged Identity Management 시작](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>ID 보호
의심 스러운 로그인 활동의 통합된 보기를 제공 하는 azure AD (Active Directory) Id 보호 하 고 잠재적인 취약점 toohelp 비즈니스를 보호 합니다. ID 보호는 무차별 암호 대입 공격(brute-force attack), 자격 증명 유출, 낯선 위치 및 감염된 장치에서 로그인 같은 신호를 기반으로 한 의심스러운 로그인 활동을 검색하며,

Id 보호 알림 및 권장된 업데이트 관리를 제공 하 여 실시간으로 toomitigate 위험은 데 도움이 됩니다. 사용자 위험 심각도 계산 하 고 이후 위협 요소 로부터 위험 기반 정책 tooautomatically 도움말 보호 방법을 응용 프로그램 액세스를 구성할 수 있습니다.

자세한 정보:

* [Azure Active Directory ID 보호](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD 및 ID 표시: ID 보호 미리 보기](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>보안 센터
Azure 보안 센터를 사용 하면 방지 하 고 검색 toothreats, 응답 하 고에 대 한 가시성 및에 대 한 제어, Azure 리소스의 보안을 hello 증가 제공 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

보안 센터를 사용 하 여 최적화 하 고 모니터링 하 여 Azure 리소스의 보안을 hello 수 있습니다.

* Tooyour에 따라 Azure 구독 리소스에 대 한 toodefine 정책을 사용 하면 회사의 보안 되어야 하며 응용 프로그램 종류 또는 hello 데이터 각 구독에서의 민감도 hello 합니다.
* Azure 가상 컴퓨터, 네트워킹 및 응용 프로그램의 hello 상태를 모니터링 합니다.
* 보안 경고를 통합된 파트너 tooquickly 필요한 hello 정보와 함께 솔루션, 조사 및 권장 방법 경고를 포함 하 여 우선 순위가 지정 된 목록을 제공 하는 방식의 공격 tooremediate 합니다.

자세한 정보:

* [소개 tooAzure 보안 센터](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
