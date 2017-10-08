---
title: "aaaAzure id 및 액세스 보안 모범 사례 | Microsoft Docs"
description: "이 문서에서는 기본 제공 Azure 기능을 사용한 ID 관리 및 액세스 제어에 대한 몇 가지 모범 사례를 제공합니다."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Azure Identity Management 및 액세스 제어 보안 모범 사례
보안을 hello 기존 네트워크 중심 관점에서 해당 역할을 넘겨 받아 id toobe hello 새 경계 계층 많은 것이 좋습니다. 보안 주의 기울이고 투자에 대 한 기본 피벗 hello이이 진화 hello 팩트 네트워크 경계가 점점 더 porous 되 고 해당 경계 방어 의이전toohello급증이사용자를한번했을때높일수없습니다에서가져올[BYOD](http://aka.ms/byodcg) 장치와 클라우드 응용 프로그램입니다.

이 문서에서는 Azure ID 관리 및 액세스 제어 보안 모범 사례 컬렉션에 대해 설명합니다. 이들 모범 사례에 대 한 경험에서 파생 된 [Azure AD](../active-directory/active-directory-whatis.md) 와 고객의 hello 경험 같은 자신입니다.

각 모범 사례에 대해 다음 사항을 설명하겠습니다.

* 어떤 hello 것이 좋습니다.
* 이유는 tooenable 최선의 방법을
* Tooenable hello에 대 한 모범 사례를 실패 한 경우 hello 결과 버릴
* 가능한 대안 toohello 모범 사례
* Tooenable hello에 대 한 최상의 정보를 어떻게 알 수 있습니다.

이 Azure id 관리 및 액세스가이 문서가 작성 된 hello 시간에 존재 하 최선의 방법 문서 합의 의견 및 Azure 플랫폼 기능 및 기능 집합 기반 보안을 제어 합니다. 의견 및 기술 시간이 지남에 따라 변경 하 고이 문서 됩니다. 이러한 변경 내용을 정기적으로 tooreflect에서 업데이트 합니다.

이 문서에서 설명하는 Azure Identity Management 및 액세스 제어 보안 모범 사례는 다음과 같습니다.

* ID 관리를 중앙 집중화
* SSO(Single Sign-On) 사용
* 암호 관리 배포
* 사용자에 대한 MFA(Multi-Factor Authentication) 적용
* RBAC(역할 기반 액세스 제어) 사용
* 리소스 관리자를 사용하여 리소스를 만드는 위치 제어
* SaaS 앱 용 개발자 tooleverage id 기능을 안내 합니다.
* 의심스러운 활동을 적극적으로 모니터링

## <a name="centralize-your-identity-management"></a>ID 관리를 중앙 집중화
사용자의 id를 보호 한 중요 한 단계는 tooensure 한다는이 계정이 생성 된 위치에 대 한 단일 한 위치에서 계정을 관리할 수 있습니다. Hello 대부분의 hello 기업 IT 조직에는 기본 계정 디렉터리 온-프레미스 갖습니다는 hello 증가에 하이브리드 클라우드 배포 및 것이 중요 이해 어떻게 toointegrate 온-프레미스 및 클라우드 디렉터리를 제공 하는 동안 한 원활한 환경 toohello 최종 사용자입니다.

tooaccomplish이 [하이브리드 id](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) 두 가지 옵션이 권장 시나리오:

* Azure AD Connect를 사용하여 온-프레미스 디렉터리를 클라우드 디렉터리와 동기화
* AD FS[(Active Directory Federation Services)](https://msdn.microsoft.com/library/bb897402.aspx)를 사용하여 온-프레미스 ID를 클라우드 디렉터리와 페더레이션

클라우드 id가 사용 하 여 자신의 온-프레미스 id에 직면할 toointegrate 실패 하는 조직은 증가 관리 오버 헤드 계정, 관리 실수 및 보안 위반의 hello 가능성을 향상 시킵니다.

Azure AD 동기화에 대 한 자세한 내용은 hello 문서를 참조 하세요 [Azure Active Directory와 온-프레미스 id 통합](../active-directory/active-directory-aadconnect.md)합니다.

## <a name="enable-single-sign-on-sso"></a>SSO(Single Sign-On) 사용
이 뿐만 아니라에 대 한 관리는 문제가 있는 경우 여러 디렉터리 toomanage, IT 뿐만 아니라 최종 사용자에 게 암호를 여러 개 tooremember 대 한 합니다. 사용 하 여 [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) 사용자가 사용 하 여 hello 동일 toosign에 자격 증명을 설정 하 고 필요한 상관 없이이 리소스는 온-프레미스 또는 클라우드에서 hello hello 리소스에 액세스의 hello 기능을 제공 합니다.

SSO tooenable 사용자 tooaccess를 사용 하 여 자신의 [SaaS 응용 프로그램](../active-directory/active-directory-appssoaccess-whatis.md) Azure AD에서 자신의 조직 계정을 기반 합니다. 이 방법은 Microsoft SaaS 앱뿐만 아니라 [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) 및 [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md) 등 다른 앱에도 적용할 수 있습니다. 응용 프로그램으로 구성 된 toouse Azure AD 수는 [SAML 기반 id](../active-directory/fundamentals-identity.md) 공급자입니다. 보안 제어로 Azure AD는 있도록 toosign hello 응용 프로그램에 권한이 부여 된 Azure AD를 사용 하 여 액세스 하지 않는 한 토큰을 발급 하지 않습니다. 직접적으로 또는 멤버인 그룹을 통해 액세스를 부여할 수 있습니다.

> [!NOTE]
> hello 의사 결정 toouse SSO에 온-프레미스 디렉터리를 클라우드 디렉터리를 통합 어떻게 영향을 줍니다. 디렉터리 동기화 제공 하기 때문에 toouse 페더레이션 SSO를 사용 하도록 하려는 경우 필요한 [동일한 로그온 환경](../active-directory/active-directory-aadconnect.md)합니다.
>
>

가 사용자 및 응용 프로그램에 대 한 SSO를 실행 하지 않는 조직은 노출 된 tooscenarios 더 같습니다. 사용자 직접 사용자 암호 다시 사용 하거나 취약 한 암호를 사용 하 여 hello 가능성을 향상 시키는 여러 암호를 갖게 됩니다.

Hello 문서를 참조 하 여 Azure AD SSO에 대 한 자세히 알아볼 수 있습니다 [AD FS 관리 및 Azure AD Connect와 사용자 정의](../active-directory/active-directory-aadconnect-federation-management.md)합니다.

## <a name="deploy-password-management"></a>암호 관리 배포
여러 테 넌 트가 위치나 tooenable 사용자를 너무 하려는 시나리오에서[자신의 암호를 재설정](../active-directory/active-directory-passwords-update-your-own-password.md), 적절 한 보안 정책을 tooprevent 남용을 사용 하는 것이 중요 합니다. Azure의 hello 셀프 서비스 암호 재설정 기능을 활용할 수 있으며 hello 보안 옵션 toomeet 비즈니스 요구 사항을 사용자 지정할 수 있습니다.

이러한 사용자의 피드백을 특히 중요 tooobtain 이며 이러한 단계 tooperform 시도 경험에서 배울 합니다. 이러한 경험 based, 더 큰 그룹에 대 한 hello 배포 하는 동안 발생할 수 있는 계획 toomitigate 잠재적인 문제를 자세히 설명 합니다. Hello를 사용 하는 것이 좋습니다 [암호 재설정 등록 활동 보고서](../active-directory/active-directory-passwords-get-insights.md) 등록 중인 toomonitor hello 사용자입니다.

Tooavoid 암호 하려는 조직은 지원 요청을 변경 하지만 사용 않는 tooreset 사용자가 자신의 암호를 더 취약 tooa 높은 호출 볼륨 toohello 서비스 데스크 toopassword 문제 때문입니다. 여러 테 넌 트 조직에는이 유형의 기능을 구현 하 고 사용자가 tooperform 암호 hello 보안 정책에 설정 된 보안 경계 내에서 재설정을 사용 합니다.

Hello 문서를 읽는 하 여 암호 재설정에 대해 알아보십시오 [암호 관리 배포 및 학습 사용자 toouse 것](../active-directory/active-directory-passwords-best-practices.md)합니다.

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>사용자에 대한 MFA(Multi-Factor Authentication) 적용
와 같은 toobe 업계 표준 규격인 펌웨어 필요한 조직을 위해 [PCI DSS 버전 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), multi-factor authentication은 반드시 필요 합니다는 사용자를 인증에 대 한 기능을 포함 합니다. 그치지 않고 업계 표준 규격인 펌웨어, MFA tooauthenticate 사용자가 강제 적용 유용할 수 있습니다 조직 toomitigate 자격 증명 도난 공격 유형 같은 [-Pass-the-hash (부서가 제작한 PtH)](http://aka.ms/PtHPaper)합니다.

사용자를 위해 Azure MFA를 사용 하 여 두 번째 계층을 보안 toouser 로그인 및 트랜잭션에 추가 됩니다. 이 경우 트랜잭션이 파일 서버 또는 SharePoint Online에 있는 문서에 액세스할 수 있습니다. Azure MFA는 손상 된 자격 증명 액세스 tooorganization 데이터를 포함 하는 IT tooreduce hello 가능성도 도움이 됩니다.

예: 사용자를 위해 Azure MFA를 적용 하 고 확인으로 toouse 전화 통화 또는 문자 메시지를 구성 합니다. Hello 공격자가 없습니다 hello 사용자의 자격 증명의 보안이 침해 될 되므로 수 tooaccess 리소스 액세스 toouser 전화 사용할 수 없습니다. Id 보호의 추가 계층을 추가 하지 않는 조직에서는 toodata 손상을 야기할 수 있는 자격 증명 도난 공격에 보다 민감한 있습니다.

한 가지 대안은 tookeep hello 전체 인증 제어 하려는 조직에 온-프레미스 않았습니다 toouse [Azure Multi-factor Authentication 서버](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), MFA 온-프레미스 라고도 합니다. 이 메서드를 사용 하 여 hello MFA 서버 온-프레미스를 유지 하면서 수 tooenforce multi-factor authentication을 수 있습니다.

Azure MFA에 대 한 자세한 내용은 hello 문서를 참조 하세요 [hello 클라우드에서 Azure Multi-factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)합니다.

## <a name="use-role-based-access-control-rbac"></a>RBAC(역할 기반 액세스 제어) 사용
Hello에 따라 액세스를 제한 [tooknow 필요](https://en.wikipedia.org/wiki/Need_to_know) 및 [최소 권한](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 보안 주체는 데이터 액세스를 위한 보안 정책 tooenforce는 조직을 위한 것입니다. Azure 역할 기반 액세스 제어 (RBAC) 사용 하는 tooassign 권한 toousers, 그룹 및 특정 범위의 응용 프로그램 수 있습니다. 역할 할당의 hello 범위는 구독, 리소스 그룹 또는 단일 리소스 될 수 있습니다.

활용할 수 있는 [RBAC에 기본 제공](../active-directory/role-based-access-built-in-roles.md) Azure tooassign 권한 toousers의 역할입니다. 사용 하는 것이 좋습니다 *저장소 계정 참가자* toomanage 저장소 계정이 필요로 하는 클라우드 운영자에 대 한 및 *클래식 저장소 계정을 참가자* 역할 toomanage 클래식 저장소 계정을 합니다. 필요한 toomanage Vm 및 저장소 계정을 클라우드 연산자에 대 한 너무 추가한 것이 좋습니다*가상 컴퓨터 참가자* 역할입니다.

RBAC 같은 기능을 활용 하 여 데이터 액세스 제어를 실행 하지 않는 조직에서는 필요한 tootheir 사용자 보다 많은 권한을 부여 될 수 있습니다. Toodata 손상 될 수 있습니다 하 여 사용자 액세스 허용 toocertain 유형의 유형의 hello 먼저에서 하면 안 되는 데이터 (예: 높은 비즈니스 영향).

Hello 문서를 참조 하 여 Azure RBAC에 대해 자세히 알아보십시오 [신속히 알아봅니다 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>리소스 관리자를 사용하여 리소스를 만드는 위치 제어
사용 하면 클라우드 운영자 tooperform 작업 toomanage 필요한 규칙은 수준에서를 방지 하는 동안 조직의 리소스 하는 것이 매우 중요 합니다. Toocontrol hello 위치 리소스가 생성 하려는 조직에 이러한 위치를 하드 코딩 해야 합니다.

tooachieve이 조직에는 hello 동작 또는 구체적으로 거부 되는 리소스를 설명 하는 정의가 있는 보안 정책을 만들 수 있습니다. Hello 구독, 리소스 그룹 또는 개별 리소스와 같은 필요한 hello 범위에서 해당 정책 정의 할당합니다.

> [!NOTE]
> 동일 RBAC로 hello 하지는이, RBAC tooauthenticate hello 사용자 권한 toocreate 이러한 리소스에 실제로 활용 합니다.
>
>

활용 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) toocreate 사용자 지정 정책을 수도 있는 hello 조직 려 tooallow 작업만 경우 hello 적절 한 비용 센터 시나리오에 대 한 연결 된; hello 요청을 거부 합니다 그렇지 않은 경우.

리소스의 인스턴스가 만들어지는 방법을 제어 하지는 조직에서는 필요한 것 보다 더 많은 리소스를 만들어 hello 서비스를 남용할 수 보다 민감한 toousers를 있습니다. 중요 한 단계 toosecure 다중 테 넌 트 시나리오는 강화 hello 리소스 만들기 프로세스입니다.

Hello 문서를 참조 하 여 정책을 Azure 리소스 관리자를 만드는 방법에 대해 자세히 알아볼 수 있습니다 [toomanage 리소스 사용 정책 및 액세스 제어](../azure-resource-manager/resource-manager-policy.md)합니다.

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>SaaS 앱 용 개발자 tooleverage id 기능을 안내 합니다.
사용자 ID는 사용자가 온-프레미스 또는 클라우드 디렉터리와 통합할 수 있는 [SaaS 앱](https://azure.microsoft.com/marketplace/active-directory/all/)에 액세스하는 많은 시나리오에 활용됩니다. 무엇 보다도는 권장 개발자가 안전한 방법론 toodevelop 이러한 앱을와 같은 [Microsoft SDL Security Development Lifecycle ()](https://www.microsoft.com/sdl/default.aspx)합니다. Azure AD는 Identity-as-a-service를 제공하며 [OAuth 2.0](http://oauth.net/2/) 및 [OpenID Connect](http://openid.net/connect/) 등의 업계 표준 프로토콜뿐만 아니라 신속하게 여러 플랫폼용 오픈 소스 라이브러리를 지원하여 개발자의 인증 작업을 간소화합니다.

있는지 tooregister 인증 tooAzure AD 아웃소싱하는 응용 프로그램을 확인, 필수 프로시저입니다. 이 뒤에 있는 hello 이유 Azure AD는 로그온 (SSO)를 처리 하거나 교환 토큰 때 hello 응용 프로그램과 toocoordinate hello 통신 필요 때문입니다. Azure AD에서 발급 하는 hello 토큰의 hello 수명이 만료 될 경우 hello 사용자의 세션이 만료 합니다. 언제나 응용 프로그램이 이 시간을 사용해야 하는지 또는 이 시간을 줄일 수 있는지 여부를 평가합니다. 줄여서 hello 수명 생성을 강제로 아웃 사용자 toosign 일정 한 비활성 기간에 따라 보안 조치로 작동할 수 있습니다.

조직 id 제어 tooaccess 앱을 실행 하지 않는 수행 하지에 및 가이드의 개발자 toosecurely 자신의 id 관리 시스템을 앱에 통합 하는 방법을 보다 민감한 toocredential 도난 유형의 공격을와 같은 수 있습니다 [약한 열린 웹 응용 프로그램 보안 프로젝트 (OWASP) 상위 10 개의에 설명 된 인증 및 세션 관리](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)합니다.

SaaS 앱의 인증 시나리오에 대한 자세한 내용은 [Azure AD에 대한 인증 시나리오](../active-directory/active-directory-authentication-scenarios.md)를 참조하세요.

## <a name="actively-monitor-for-suspicious-activities"></a>의심스러운 활동을 적극적으로 모니터링
너무에 따라[Verizon 2016 데이터 위반 보고서](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), 자격 증명 손상 되 고 hello 상승과 사이버 범죄자가 hello 이윤이 가장 높은 비즈니스 중 하나입니다. 이러한 이유로 중요 한 toohave 신속 하 게 의심 스러운 동작 활동이 있는지 검색 하 고 추가 조사에 대 한 경고를 트리거할 수 있는 위치에는 활성 id 모니터 시스템의이 것입니다. Azure AD에는 조직에서 자신의 ID를 모니터링할 수 있도록 하는 두 가지 주요 기능: Azure AD Premium [비정상 보고서](../active-directory/active-directory-view-access-usage-reports.md) 및 Azure AD [ID 보호](../active-directory/active-directory-identityprotection.md) 기능이 있습니다.

있는지 toouse hello 비정상 보고서 tooidentify 시도 toosign에 확인 [추적 되지 않고](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [무작위](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) 여러 위치에서에서 시도 toosign는 특정 계정에 대 한 공격에 로그인 [장치 감염](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) 및 의심 스러운 IP 주소입니다. 이는 보고서임을 염두에 두십시오. 즉, IT 관리자 toorun에 대 한 이러한 보고서 hello 매일 또는 배치 (일반적으로: 사고 대응 시나리오)에서 요청 시 프로세스 및 절차에 있어야 합니다.

반면, Azure AD id 보호 활성 모니터링 시스템 이며 자체 대시보드에서 hello 현재 위험 플래그를 지정 합니다. 뿐만 아니라 전자 메일을 통해 일일 요약 알림을 받습니다. Hello 위험 수준을 tooyour 비즈니스 요구 사항에 따라 조정 하는 것이 좋습니다. 위험 이벤트에 대 한 hello 위험 수준을 hello 위험 이벤트의 hello 심각도 (높음, 중간 또는 낮음) 나타냅니다. hello 위험 수준 Id 보호 사용자 tooreduce hello 위험 tootheir 조직을 취해야 하는 hello 작업 우선 순위를 지정할 수 있습니다.

자신의 ID 시스템을 적극적으로 모니터링하지 않는 조직은 사용자 자격 증명이 손상될 위험에 직면합니다. 의심 스러운 활동을 수행 하는 지식 없이도 이러한 자격 증명을 사용 하 여 배치, 조직 됩니다 수 toomitigate이 이와 같은 위협을 합니다.
Azure ID 보호에 대한 자세한 내용은 [Azure Active Directory ID 보호](../active-directory/active-directory-identityprotection.md)를 참조하세요.
