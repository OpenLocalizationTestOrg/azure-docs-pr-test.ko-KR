---
title: "aaaAzure 보안 기술적 역량 | Microsoft Docs"
description: "다양 한 종류의 계산 인스턴스를 포함 하는 클라우드 기반 컴퓨팅 서비스 및 응용 프로그램 또는 엔터프라이즈의 hello 요구 자동으로 toomeet 위쪽 및 아래쪽으로 확장 될 수 있는 서비스에 알아봅니다."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Azure 보안 기술 기능

tooassist 현재 및 향후 Azure 고객 이해 하 고 hello 활용 다양 한 보안 관련 기능에 사용할 수 있으며 주변 hello Azure 플랫폼, Microsoft는 일련의 백서, 보안 개요, 모범 사례를 개발 하 고 검사 목록입니다. hello 항목 폭과 깊이 기준으로 다양 하 고 정기적으로 업데이트 됩니다. 이 문서는 hello 추상 섹션 아래에 요약 된 것 처럼 해당 시리즈의 일부는입니다. 이 Azure 보안 시리즈에 대한 자세한 내용은 (URL)에서 찾을 수 있습니다.

## <a name="azure-platform"></a>Azure 플랫폼

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/)는 데이터 서비스 및 고급 분석, 개발자 도구 및 서비스가 통합되고 Microsoft의 공용 클라우드 데이터 센터 내에 호스트된 인프라 및 응용 프로그램 서비스로 구성된 클라우드 플랫폼입니다. 고객이는 Azure를 사용 하 여 여러 다른 용량 및 기본 계산, 네트워킹 및 저장소, toomobile 및 웹 응용 프로그램 서비스, 사물 인터넷 같은 toofull 클라우드 시나리오에서에서의 시나리오에 대 한 오픈 소스 기술 사용할과 가능으로 하이브리드 배포 클라우드 또는 고객의 데이터 센터 내에서 호스팅됩니다. 빌딩 블록 toohelp 회사 비용을 절감 혁신 신속 하 게 하 고 시스템을 적극적으로 관리할 azure 클라우드 기술을 제공 합니다. 를, 작성 하거나 IT 자산 tooa 클라우드 공급자를 마이그레이션할 때 응용 프로그램 및 서비스 hello 및 클라우드 기반 자산의 toomanage hello 보안을 제공 하는 hello 컨트롤을 사용 하 여 데이터 해당 조직의 능력 tooprotect에 의존 하 고 있습니다.

Microsoft Azure hello 유일한 클라우드 컴퓨팅 공급자 응용 프로그램을 안전 하 고 일관 된 플랫폼 및 인프라-as a service 다른 클라우드 기술이 통합된 하는 데이터와 함께 프로젝트 복잡성 수준이 내에서 팀 toowork에 대 한 제공 하는 서비스 및 Microsoft 및 타사 플랫폼에 걸쳐 있는 경우 항상 intelligence 데이터에서 발견 하는 분석 열 프레임 워크 및 온-프레미스도 내에서 Azure 클라우드 서비스를 배포 클라우드를 통합 하기 위한 선택 항목을 제공 하는 도구 온-프레미스 데이터 센터입니다. Microsoft 신뢰할 수 있는 클라우드 hello의 일환으로, 고객은 업계 최고의 보안, 안정성, 규정 준수, 개인 정보 및 사용자, 파트너 및 프로세스 toosupport 조직의 hello 클라우드에서 hello vast 네트워크에 대 한 Azure에 의존 합니다.

Microsoft Azure를 사용하면 다음과 같은 작업을 수행할 수 있습니다.

- Hello 클라우드 된 혁신을 가속화할 수 있습니다.

- 통찰력으로 비즈니스 의사 결정 및 앱을 강화합니다.

- 어디서든 자유롭게 빌드하고 배포합니다.

- 비즈니스를 보호합니다.

## <a name="scope"></a>범위

이 백서의 hello 초점 보안 기능 및 즉 Microsoft Azure의 핵심 구성 요소를 지 원하는 기능 관여 [Microsoft Azure 저장소](https://docs.microsoft.com/azure/storage/storage-introduction), [Microsoft Azure SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/), [Microsoft Azure 가상 컴퓨터 모델](https://docs.microsoft.com/azure/virtual-machines/  ), 및 hello 도구와 다를 관리 하는 인프라입니다. 이 백서에 집중 Microsoft Azure 기술적 역량 사용 가능한 tooyou 고객 toofulfil으로 자신의 역할 hello 보안 및 개인 정보 데이터를 보호 합니다.

이 공유 책임 모델 이해의 hello 중요성 toohello 클라우드를 이동 하는 고객을 위해 반드시 필요 합니다. 클라우드 공급자 보안 및 규정 준수 활동에 대 한 상당한 이점을 제공 하지만 이러한 장점 자신의 사용자, 응용 프로그램 및 서비스 제공을 보호에서 hello 고객 absolve 하지 않습니다.

IaaS 솔루션에 대 한 hello 고객은 또는 보안 설정 및 hello 운영 체제, 네트워크 구성, 응용 프로그램, id, 클라이언트 및 데이터 관리에 대 한 공유 책임입니다.  IaaS 배포에서 PaaS 솔루션 빌드, hello 고객을 통해 계속 또는 보안 설정 및 응용 프로그램, id, 클라이언트 및 데이터 관리에 대 한 공유 책임입니다. SaaS 솔루션의 경우, Nonetheless hello 고객 책임 toobe를 계속합니다. 데이터가 올바르게 분류 되는 해당 사용자 및 장치 끝점 책임 toomanage를 공유 하 확인 해야 합니다.

이 문서는 hello의 자세한 정보를 제공을 제공 하지 않는 관련 Azure 웹 사이트, Azure Active Directory, HDInsight, 미디어 서비스 hello 핵심 구성 요소 위에 표시 계층에 있는 다른 서비스와 같은 Microsoft Azure 플랫폼 구성 요소입니다. 최소 수준의 일반 정보가 제공되지만, 사용자가 Microsoft에서 제공하고 이 백서에 제공된 링크에 포함되어 있는 기타 참조에 설명된 Azure 기본 개념에 익숙하다고 가정합니다.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>사용 가능한 보안 기술적 역량 toofulfil 사용자 (고객) 책임 큰 그림

Microsoft Azure hello 보안, 개인 정보 보호 및 규정 준수 요구를 충족 하는 고객 수 있는 서비스를 제공 합니다. 다음 그림을 사용 하면 업계 표준에 따라 다양 한 Azure 사용할 수 있는 서비스 사용자가 toobuild 안전 하 고 규격 응용 프로그램 인프라에 대 한 설명 hello 합니다.

![사용 가능한 보안 기술 기능 - 전반적 이해](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>ID 및 사용자 액세스 관리 및 제어(보호)

Azure를 사용 하면 toomanage 사용자 id 및 자격 증명 및 액세스 제어를 사용 하 여 회사 및 개인 정보를 보호할 수 있습니다.

### <a name="azure-active-directory"></a>Azure Active Directory

Microsoft id 및 액세스 관리 솔루션 도움말 IT 액세스 tooapplications와 리소스를 보호 및 hello 클라우드로 hello 회사 데이터 센터에서 다단계 인증 및 조건부 같은 유효성 검사의 수준을 사용 하도록 설정 액세스 정책입니다. 고급 보안 보고, 감사 및 경고를 통해 의심스러운 작업을 모니터링하여 잠재적인 보안 문제를 완화시킵니다. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) 클라우드 (SaaS) 응용 프로그램 및 온-프레미스를 실행 하는 액세스 tooweb 앱 single sign on toothousands를 제공 합니다.

보안 이점의 Azure AD (Active Directory)를 hello 기능이 포함합니다.

- 하이브리드 엔터프라이즈에서 사용자, 그룹 및 장치의 동기화를 유지하도록 각 사용자에 대한 단일 ID 만들기 및 관리

- 수천 개의 미리 통합 된 SaaS 응용 프로그램을 포함 하 여 tooyour 응용 프로그램 single sign-on 액세스를 제공 합니다.

- 온-프레미스 및 클라우드 응용 프로그램 모두에 대해 규칙 기반 Multi-Factor Authentication을 적용하여 응용 프로그램 액세스 보안을 사용하도록 설정

- 프로 비전 보안 된 원격 액세스 tooon 온-프레미스 Azure AD 응용 프로그램 프록시를 통해 응용 프로그램 웹입니다.

[Azure Active Directory 포털](http://aad.portal.azure.com/)은 Azure Portal의 일부로 사용할 수 있습니다. 이 대시보드에서 ָ ¹ ר hello 상태에 대 한 개요를 얻을 수 있으며 쉽게 hello 디렉터리, 사용자 또는 응용 프로그램 액세스 관리에 대해 살펴보겠습니다.

![Azure Active Directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

다음은 핵심적인 Azure ID 관리 기능입니다.

- SSO(Single sign-on)

- Multi-Factor Authentication

- 보안 모니터링, 경고 및 기계 학습 기반 보고서

- 소비자 ID 및 액세스 관리

- 장치 등록

- Privileged Identity Management

- ID 보호

#### <a name="single-sign-on"></a>SSO(Single sign-on)

[Single sign-on (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) 의미 수 tooaccess 모든 hello 응용 프로그램 및 한 번만 단일 사용자 계정을 사용 하 여 로그인 toodo 비즈니스를 필요한 리소스입니다. 로그인 한 후 필요한 tooauthenticate 되 없이 필요한 모든 hello 응용 프로그램에 액세스할 수 있습니다 (예를 들어 암호 입력)를 두 번입니다.

대부분의 조직에서는 최종 사용자 생산성을 위해 Office 365, Box, Salesforce와 같은 SaaS(Software as a Service) 응용 프로그램에 의존합니다. 지금까지 IT 직원 필요한 tooindividually 만들고 각 SaaS 응용 프로그램에서 사용자 계정을 업데이트 하 고 사용자가 각 SaaS 응용 프로그램에 대 한 암호를 tooremember 했습니다.

[Azure AD는 온-프레미스 Active Directory hello 클라우드로 확장](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), tootheir 도메인에 가입 된 장치 및 회사 리소스에만 로그인 toonot 계정 하지만 웹 및 SaaS 응용 프로그램 모두 hello도 기본 조직 사용자가 toouse를 사용 하도록 설정 작업에 필요합니다.

뿐만 아니라 사용자가 필요는 없으며 toomanage 사용자 이름 및 암호의 여러 집합, 자동으로 프로 비전 하거나 프로 비전이 해제에 따라 조직 그룹 및 해당 상태는 응용 프로그램 액세스 될 수 있습니다. [Azure AD 보안 및 액세스 통제 컨트롤이 도입](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) 수 있는 toocentrally 전체 SaaS 응용 프로그램 사용자의 액세스를 관리 합니다.

#### <a name="multi-factor-authentication"></a>Multi-Factor Authentication

[Azure multi-factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) 는 확인 방법을 두 개 이상 hello 사용 해야 하 고 보안 toouser 로그인 및 트랜잭션에 중요 한 두 번째 계층을 추가 하는 인증 방법입니다. [MFA는 보호 기능이](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 toodata 및 응용 프로그램에 액세스 합니다. 전화 통화, 문자 메시지 또는 모바일 앱 알림 또는 확인 코드 및 타사 OAuth 토큰과 같은 다양한 확인 옵션을 통해 강력한 인증을 전달합니다.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>보안 모니터링, 경고 및 기계 학습 기반 보고서

일치하지 않는 액세스 패턴을 식별하는 보안 모니터링 및 경고 및 기계 학습 기반 보고서로 비즈니스를 보호할 수 있습니다. Azure Active Directory의 액세스 및 조직 디렉터리의 hello 무결성 및 보안에 대 한 사용 현황 보고서 toogain 가시성을 사용할 수 있습니다. 이 정보를 사용 하면 디렉터리 관리자 수 보다 잘 결정 있는 가능한 보안 위험이 발생할 수 있습니다 적절 하 게 될 수 toomitigate 이러한 위험.

Hello Azure 클래식 포털에서에서 또는 통해 [Azure Active directory 포털](http://aad.portal.azure.com/), [보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) hello 같은 방법으로 다음으로 분류 됩니다.

- 비정상 보고서-이벤트가 있음을 toobe 비정상적인 로그인을 포함 합니다. 목표는 toomake 이러한 활동을 인식 하 고 의심 스러운 이벤트 인지에 대 한 toobe 수 toodecide 있습니다를 사용 하도록 설정 합니다.

- 통합 응용 프로그램 보고서 – 클라우드 응용 프로그램이 조직에서 사용되는 방식을 파악할 수 있게 해 줍니다. Azure Active Directory는 수천 개의 클라우드 응용 프로그램과 통합을 제공합니다.

- 오류 보고서 – 계정 tooexternal 응용 프로그램을 프로 비전 할 때 발생할 수 있는 오류를 나타냅니다.

- 사용자별 보고서 – 특정 사용자에 대한 장치/로그인 활동 데이터를 표시합니다.

- 활동 로그-지난 24 시간 동안 hello 내의 모든 감사 된 이벤트의 레코드가 포함, 마지막 7 일 또는 30 일 이내 그룹 활동 변경 사항 및 암호 재설정 및 등록 활동입니다.

#### <a name="consumer-identity-and-access-management"></a>소비자 ID 및 액세스 관리

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) 는 toohundreds 수백만 id의 크기를 조정 하는 소비자 용 응용 프로그램에 대 한 전역, 항상 사용 가능한 id 관리 서비스입니다. 이 서비스는 모바일 및 웹 플랫폼에 통합될 수 있습니다. 소비자 로그온 할 수 tooall 사용자 지정할 수 있는 환경을 통해 응용 프로그램의 기존 소셜 계정을 사용 하 여 하거나 만들어 새 자격 증명.

Hello 너무 원하는 응용 프로그램 개발자가 과거에[등록 하 고 소비자 로그인](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) 응용 프로그램에는 작성 한 고유 코드입니다. 있고 온-프레미스 데이터베이스 또는 시스템 toostore 사용자 이름 및 암호 사용 않은 것입니다. Azure Active Directory B2C 조직 hello 도움말 응용 프로그램 안전 하 고 표준 기반 플랫폼 및 다양 한 확장 가능한 정책으로는 더 나은 방법은 toointegrate 소비자 id 관리를 제공합니다.

Azure Active Directory B2C를 사용하면 소비자는 기존 소셜 계정(Facebook, Google, Amazon, LinkedIn)을 사용하거나 새 자격 증명(전자 메일 주소 및 암호 또는 사용자 이름 및 암호)을 만들어서 응용 프로그램을 등록할 수 있습니다.

장치 등록

[Azure AD Device Registration](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) hello 토대 장치 기반 [조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) 시나리오입니다. 장치를 등록할 때 Azure Active Directory 장치 등록은 hello 사용자가 로그인 할 때 사용 되는 tooauthenticate hello 장치 id가 있는 hello 장치를 제공 합니다. 인증 된 hello 장치와 hello 장치의 hello 특성 수 hello 클라우드 및 온-프레미스에서 호스트 되는 응용 프로그램에 대 한 조건부 액세스 정책을 사용 하는 tooenforce 합니다.

함께 사용 하면 한 [모바일 장치 관리 (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) Intune, Azure Active Directory의 장치 특성이 hello 같은 솔루션 hello 장치에 대 한 추가 정보로 업데이트 됩니다. 이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다.

#### <a name="privileged-identity-management"></a>Privileged Identity Management

[Azure AD (Active Directory) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) 관리, 제어, 권한 있는 id 및 모니터링 tooresources Azure AD에서 Microsoft Intune 또는 Office 365와 같은 다른 Microsoft 온라인 서비스 액세스할 수 있습니다.

경우에 따라 사용자는 Azure 또는 Office 365 리소스 또는 다른 SaaS 앱에 권한 있는 작업 toocarry가 필요합니다. 종종 즉, 조직 toogive Azure AD에 해당 영구 권한 액세스 합니다. 조직은 사용자가 관리자 권한으로 수행하는 작업을 충분히 모니터링할 수 없으므로 클라우드에 호스트된 리소스의 보안 위험이 증가합니다. 또한 권한 있는 액세스가 있는 사용자 계정이 손상되면 이로 인해 전반적인 클라우드 보안에 영향을 줄 수 있습니다. Azure AD Privileged Identity Management tooresolve이이 위험을 수 있습니다.

Azure AD Privileged Identity Management를 통해 다음을 할 수 있습니다.

- Azure AD 관리자인 사용자를 확인할 수 있습니다.

- 요청 시 "just in time" Office 365 및 Intune 관리 액세스 tooMicrosoft 온라인 서비스와 같은 사용 하도록 설정

- 관리자 액세스 기록 및 관리자 할당 변경에 대한 보고서 가져오기

- 액세스 tooa 권한 있는 역할에 대 한 경고를 받으려면

#### <a name="identity-protection"></a>ID 보호

[Azure AD ID 보호](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)는 조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공하는 보안 서비스입니다. ID 보호는 기존 Azure Active Directory의 비정상 감지 기능(Azure AD의 비정상적인 작업 보고서를 통해 사용 가능)을 활용하고 실시간으로 잘못된 부분을 검색할 수 있는 새로운 위험 이벤트 유형을 소개합니다.

## <a name="secured-resource-access-in-azure"></a>Azure의 보안 리소스 액세스

Azure의 액세스 제어는 결제 관점에서 시작합니다. hello를 방문 하 여 액세스 하는 Azure 계정의 소유자 hello [Azure 계정 센터](https://account.windowsazure.com/subscriptions)는 hello AA (계정 관리자)입니다. 구독은 결제를 위한 컨테이너 이지만 보안 경계로도 작동 합니다: 각 구독에는 서비스 관리자 (SA) 추가, 제거 및 hello를 사용 하 여 해당 구독의 Azure 리소스를 수정할 수 있는 [Azure클래식포털](https://manage.windowsazure.com/). 새 구독의 기본 SA hello hello AA 이지만 AA hello hello Azure 계정 센터에서에서 hello SA를 변경할 수 있습니다.

![Azure의 보안 리소스 액세스](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

또한 구독은 디렉터리와 연결되어 있습니다. hello 디렉터리 사용자 집합을 정의합니다. Hello 회사 또는 학교 hello 디렉터리를 만든 사용자가 될 수 있습니다. 또는 외부 사용자 (즉, Microsoft 계정) 될 수 있습니다. 구독을 서비스 관리자 (SA) 또는 CA (공동 관리자);에 지정 된 해당 디렉터리 사용자의 하위 집합에서 액세스할 수 있습니다. hello 예외만, 레거시의 이유로 Microsoft 계정 (이전의 Windows Live ID) 할당할 수 있는 SA 또는 CA로 hello 디렉터리에 없는 합니다.

보안 지향적인 회사 직원에 게 필요한 hello 정확 하 게 사용 권한이 부여에 초점을 맞추어야 합니다. 너무 많은 권한을 계정 tooattackers를 노출할 수 있습니다. 권한이 너무 적으면 직원이 업무를 효율적으로 수행할 수 없습니다. [Azure RBAC(역할 기반 액세스 제어)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)는 Azure에 대한 세밀한 액세스 관리를 제공하여 이 문제를 해결하도록 도와줍니다.

![보안 리소스 액세스 ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

RBAC를 사용 하 여 팀 내에서 업무를 구분할 수 있으며 필요 하다는 tooperform 업무 hello 양의 데이터만 toousers 액세스 권한을 부여 수도 있습니다. Azure 구독 또는 리소스에서 모든 사람에게 무제한 권한을 제공하는 대신 특정 작업만 허용할 수 있습니다. 예를 들어 구독에서 가상 컴퓨터를 관리 하는 사용 하 여 RBAC toolet 직원이 한 명, 다른를 관리할 수 있는 반면 SQL 데이터베이스 hello 내에서 동일한 구독 합니다.

![Azure의 보안 리소스 액세스(RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Azure 데이터 보안 및 암호화(보호)

데이터 발생할 수 있는 및 해당 상태에 대해 사용할 수 있는 컨트롤의 hello 가능한 상태에 대 한 회계는 hello 클라우드에서 hello 키 toodata 보호 중 하나입니다. Azure 데이터 보안 및 암호화에 대 한 모범 사례에 대 한 hello 권장 사항은 데이터의 상태가 다음 hello 주위 수 있습니다.

- 저장: 모든 정보 저장 개체, 컨테이너 및 물리적 미디어(자기 또는 광 디스크)에 정적으로 존재하는 유형이 여기에 포함됩니다.

- 전송 중인: 때 데이터 사이 전송 될 구성 요소, 위치 또는 프로그램을와 같은 hello 네트워크를 통해 (온-프레미스 toocloud 반대의 ExpressRoute와 같은 하이브리드 연결을 포함 하 여)에서 서비스 버스를 통해 또는 입력/출력 하는 동안 프로세스 생각 됩니다의 것으로 동작 합니다.

### <a name="encryption--rest"></a>휴지 상태의 암호화

tooachieve 휴지 암호화 각 hello 다음 중:

Hello 권장 hello 테이블 tooencrypt 데이터 다음에 자세히 설명 하는 암호화 모델 중 하나 이상을 지원 합니다.

| 암호화 모델 |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| 서버 암호화 | 서버 암호화 | 서버 암호화 | 클라이언트 암호화
| 서비스 관리 키를 사용하는 서버 쪽 암호화 | Azure Key Vault의 고객 관리 키를 사용하는 서버 쪽 암호화 | 온-프레미스 고객 관리 키를 사용하는 서버 쪽 암호화 |
| • Azure 리소스 공급자 hello 암호화 및 해독 작업 수행 <br> • Microsoft hello 키를 관리합니다. <br>• 전체 클라우드 기능 | • Azure 리소스 공급자 hello 암호화 및 해독 작업 수행<br>•    고객이 Azure Key Vault를 통해 키 제어<br>• 전체 클라우드 기능 | • Azure 리소스 공급자 hello 암호화 및 해독 작업 수행 <br>• 고객 키 온-프레미스를 제어합니다. <br> •  전체 클라우드 기능| • Azure 서비스에서 해독된 데이터를 볼 수 없음 <br>•  고객이 온-프레미스(또는 다른 보안 저장소)에서 키 유지. 키는은 사용할 수 있는 tooAzure 서비스 하지 않습니다. <br>• 클라우드 기능 제한|

### <a name="enabling-encryption-at-rest"></a>휴지 상태의 암호화 사용

**데이터를 저장하는 모든 위치 식별**

휴지 암호화의 hello 목표 tooencrypt 모든 데이터가 됩니다. 이렇게 하면 hello 가능성을 누락 된 중요 한 데이터 또는 모든 지속 된 위치에 없습니다. 응용 프로그램에서 저장 된 모든 데이터를 열거 합니다. 

> [!Note] 
> 뿐 아니라 "application data" 또는 "PII' 하지만 tooapplication 포함 하 여 관련 된 모든 데이터는 메타 데이터 (구독 매핑, 계약 정보, PII) 계정.

어떤 저장 하는 것이 좋습니다 toostore 데이터를 사용 하는 합니다. 예:

- 외부 저장소(예: SQL Azure, 문서 DB, HDInsight, Data Lake 등)

- 임시 저장소(테넌트 데이터를 포함하는 모든 로컬 캐시)

- 메모리 내 캐시 (에 배치 될 수 hello 페이지 파일입니다.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Rest 지원 Azure의 hello 기존 암호화를 활용 합니다.

각 저장소 사용에 대 한 암호화 Rest 지원에 존재 하는 hello를 활용 합니다.

- Azure Storage: [휴지 상태의 데이터에 대한 Azure Storage 서비스 암호화](https://docs.microsoft.com/azure/storage/storage-service-encryption)를 참조하세요.

- SQL Azure: [TDE(투명한 데이터 암호화), SQL Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)를 참조하세요.

- VM 및 로컬 디스크 저장소([Azure Disk Encryption](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

지원되는 경우 VM 및 로컬 디스크 저장소에 대해 Azure Disk Encryption 사용:

IaaS

IaaS Vm (Windows 또는 Linux)를 사용 하 여 서비스를 사용 해야 [Azure 디스크 암호화](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) tooencrypt 볼륨 고객 데이터가 들어 있는입니다.

PaaS v2

실행 되는 서비스에서 PaaS v2 서비스 패브릭을 사용 하 여 수 사용 하 여 Azure 디스크 암호화 tooencrypt 가상 컴퓨터 크기 집합 [VMSS]의 PaaS v2 Vm입니다.

PaaS v1

Azure Disk Encryption은 현재 PaaS v1에서 지원되지 않습니다. 따라서 응용 프로그램 수준을 사용 해야 암호화 tooencrypt 미사용 데이터를 유지 합니다.  여기에는 응용 프로그램 데이터, 임시 파일, 로그 및 크래시 덤프가 포함되지만 이에 국한되지 않습니다.

대부분의 서비스는 저장소 리소스 공급자의 tooleverage hello 암호화를 시도해 야 합니다. 일부 서비스 toodo 명시적 암호화, 키 자료는 유지 하는 예를 들어 (인증서, 루트 / 마스터 키) 주요 자격 증명 모음에 저장 되어야 합니다.

고객이 관리 하는 키를 가진 서비스 쪽 암호화를 지 원하는 경우 필요 toobe 방식으로 hello 고객 tooget hello 키 toous 합니다. hello 지원 및 Azure 키 자격 증명 모음 (AKV)와 통합 하 여 하는 방식으로 toodo를 권장 합니다. 이 경우 고객은 Azure Key Vault에서 해당 키를 추가하고 관리할 수 있습니다. 고객에 배울 수 어떻게 toouse AKV 통해 [키 자격 증명 모음 시작](http://go.microsoft.com/fwlink/?linkid=521402)합니다.

Azure 키 자격 증명 toointegrate, 암호 해독을 위해 필요할 때 AKV에서 코드 toorequest 키를 추가 합니다.

- 참조 [Azure 키 자격 증명 모음 – 단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) 방법에 대 한 정보 toointegrate AKV 사용 합니다.

고객 관리 키를 지원 해야 tooprovide UX 고객 toospecify hello에 대 한 어떤 자격 증명 모음 키 (또는 키 자격 증명 모음 URI) toouse.

휴지 암호화 포함 hello 호스트, 인프라 및 테 넌 트 데이터 암호화, 암호화 hello 데이터가 모두 손실 됩니다 hello 키 기한 toosystem 오류 또는 악의적인 활동의 hello 손실 의미할 수 있습니다. 나머지 솔루션에서 암호화에는 복원 력 있는 toosystem 실패 및 악의적인 활동 스토리 포괄적인 재해 복구는 따라서 합니다.

미사용 데이터 암호화를 구현 하는 서비스는 일반적으로 여전히 취약 toohello 암호화 키 또는 hello 호스트 드라이브 (예를 들어 hello 페이지의 파일에서 hello 호스트 OS.)에 암호화 되지 않은 상태로 유지 되는 데이터 따라서 서비스 들이 서비스에 대 한 hello 호스트 볼륨이 암호화 되어 있어야 합니다. toofacilitate 계산 팀이 활성화를 사용 하는 호스트 암호화의 hello 배포 [Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP 및 확장 toohello DCM 서비스와 에이전트가 tooencrypt hello 호스트 볼륨입니다.

대부분의 서비스는 표준 Azure VM에서 구현됩니다. 이러한 서비스는 Compute에서 사용되도록 설정될 경우 [호스트 암호화](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)를 자동으로 가져옵니다. Compute 관리 클러스터에서 실행되는 서비스의 경우 Windows Server 2016이 출시되면 호스트 암호화가 자동으로 사용되도록 설정됩니다.

### <a name="encryption-in-transit"></a>전송 중인 암호화

전송 중인 데이터 보호는 데이터 보호 전략에서 절대 빠질 수 없는 핵심입니다. 데이터는 여러 위치에서 앞뒤로 이동 hello 일반적인 권장 사항은 이므로 다른 위치에서 SSL/TLS 프로토콜 tooexchange 데이터 항상 사용 합니다. 일부 경우에 온-프레미스와 클라우드 간의 tooisolate hello 전체 통신 채널을 사용할 수 있습니다 가상 사설망 (VPN)을 사용 하 여 인프라입니다.

온-프레미스 인프라와 Azure 사이를 이동하는 데이터의 경우 HTTPS 또는 VPN처럼 적절한 안전 장치를 고려해야 합니다.

여러 워크스테이션 온-프레미스 tooAzure에서 toosecure 액세스 해야 하는 조직에서 사용 하 여 [Azure 사이트 간 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create)합니다.

한 워크스테이션에서 toosecure 액세스 해야 하는 조직에서는 온-프레미스 tooAzure를 사용 하 여 64 \ [지점 및 사이트 간 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create)합니다.

대용량 데이터 집합은 [Express 경로](https://azure.microsoft.com/services/expressroute/) 같은 전용 고속 WAN 링크를 통해 이동할 수 있습니다. 또한 사용 하 여 hello 응용 프로그램 수준에서 hello 데이터를 암호화할 수 toouse express 경로 선택 하면 [SSL/TLS](https://support.microsoft.com/kb/257591) 또는 추가적인된 보호를 위해 다른 프로토콜입니다.

Hello Azure 포털을 통해 Azure 저장소와 상호 작용 하는, 하는 경우 HTTPS를 통해 모든 트랜잭션이 발생 합니다. [저장소 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx) HTTPS를 통해 수도 있습니다를 사용 하는 toointeract [Azure 저장소](https://azure.microsoft.com/services/storage/) 및 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/)합니다.

Tooprotect 데이터 전송 중에 실패 하는 조직에 보다 민감한는 [중간자 개입 공격](https://technet.microsoft.com/library/gg195821.aspx), [도청](https://technet.microsoft.com/library/gg195641.aspx), 세션 하이재킹 하 고 있습니다. 이러한 공격은 tooconfidential 데이터에 액세스 하지 못하도록 hello 첫 번째 단계 수 있습니다.

Hello 문서를 참조 하 여 Azure VPN 옵션에 대 한 자세히 알아볼 수 있습니다 [계획 및 디자인 VPN 게이트웨이에 대 한](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)합니다.

### <a name="enforce-file-level-data-encryption"></a>파일 수준 데이터 암호화 적용

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) 사용 하 여 암호화, id 및 권한 부여 정책 toohelp 보안 여 파일과 전자 메일을 설정 합니다. Azure RMS는 조직 내부와 조직 외부에서 휴대폰, 태블릿 및 PC와 같은 여러 장치를 보호합니다. 이 기능은 Azure RMS는 조직의 경계를 벗어나 더라도 hello 데이터를 계속 보호 수준을 추가 하기 때문에 가능 합니다.

Azure RMS tooprotect 파일을 사용 하는 업계 표준 암호화의 완벽 하 게 지원 [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html)합니다. 복사한 toostorage의 hello 제어 하지 않는 경우에 hello 파일 hello 보호가 유지 됩니다. hello 보증 있는 Azure RMS를 활용 하 여 데이터를 보호 하는 경우 클라우드 저장소 서비스 등 IT 합니다. hello 동일 하 게 실행 전자 메일을 통해 공유 하는 파일에 대 한 hello 파일을 첨부 tooan 전자 메일 메시지 보호와, 지침이 포함 된 방법을 tooopen hello 보호 된 첨부 파일입니다.
Azure RMS 채택을 계획할 때 다음을 hello 좋습니다.

- Hello 설치 [RMS 공유 앱](https://technet.microsoft.com/library/dn339006.aspx)합니다. 이 앱은 사용자가 간편하게 파일을 직접 보호할 수 있도록 Office 추가 기능을 설치하여 Office와 통합됩니다.

- 응용 프로그램 및 서비스 toosupport Azure RMS 구성

- 비즈니스 요구 사항을 반영하는 [사용자 지정 템플릿](https://technet.microsoft.com/library/dn642472.aspx) 만들기. 예: 모든 극비 관련 전자 메일에 적용해야 하는 극비 데이터 템플릿.

약한에 있는 조직이 [데이터 분류](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 파일 보호 보다 민감한 toodata 유출을 수 있습니다. 적절 한 파일 보호 없이 조직 않습니다 수 tooobtain 비즈니스 통찰력, 남용 모니터링 하며 방지의 악의적인 액세스 toofiles 합니다.

> [!Note]
> Hello 문서를 참조 하 여 Azure RMS에 대해 자세히 알아볼 수 있습니다 [Azure 권한 관리 시작](https://technet.microsoft.com/library/jj585016.aspx)합니다.

## <a name="secure-your-application-protect"></a>응용 프로그램 보안(보호)
Azure hello 인프라 및 응용 프로그램에서 실행 되는 플랫폼에 보안 설정에 대 한 책임이 책임 toosecure는 자체 응용 프로그램입니다. Toodevelop, 필요한 즉, 배포 하 고 안전 하 게에서 응용 프로그램 코드와 콘텐츠를 관리 합니다. 이렇게 하지 않으면 응용 프로그램 코드 또는 콘텐츠에 취약 한 toothreats 될 있을 수 있습니다.

### <a name="web-application-firewall-waf"></a>WAF(웹 응용 프로그램 방화벽)
[WAF(웹 응용 프로그램 방화벽)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)는 일반적인 악용 및 취약점으로부터 웹 응용 프로그램에 대해 중앙 집중화된 보호를 제공하는 [Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)의 기능입니다.

웹 응용 프로그램 방화벽 hello에서 규칙을 기반 [OWASP 코어 규칙 집합](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 또는 2.2.9 퀵 합니다. 웹 응용 프로그램의 널리 알려진 취약점을 악용하는 악의적인 공격이 점점 많아지고 있습니다. 이러한 익스플로잇 간에 공통적으로 적용은 SQL 삽입 공격, tooname 몇 가지 공격 교차 사이트 스크립팅 합니다. 응용 프로그램 코드에서 이러한 공격 방지 하기가 어려울 수 있습니다 및 엄격한 유지 관리, 패치 및 hello 응용 프로그램 토폴로지의 여러 계층에서 모니터링 해야 할 수 있습니다. 중앙 집중식된 웹 응용 프로그램 방화벽은 보안 관리를 훨씬 더 간단 하 게 하면 하 고 더 나은 보증 위협 또는 침입 tooapplication 관리자를 제공 합니다. WAF 솔루션와 각각의 개별 웹 응용 프로그램 보안을 중앙 위치에서 알려진된 취약점의 패치를 적용 하 여 tooa 보안 위협이 더 빠르게 반응 수 있습니다. 기존 응용 프로그램 게이트웨이 변환 된 tooa 웹 응용 프로그램 방화벽을 사용 응용 프로그램 게이트웨이 쉽게 될 수 있습니다.

Hello 일반적인 웹 취약점 으로부터 보호 하는 웹 응용 프로그램 방화벽 중 일부에 다음이 포함 됩니다.

- SQL 삽입 공격 보호

- 교차 사이트 스크립팅 공격 보호

- 명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호

- HTTP 프로토콜 위반 보호

- 누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호

- 보트, 크롤러 및 스캐너 방지

- 일반적인 응용 프로그램 구성 오류(즉 Apache, IIS 등) 검색

> [!Note]
> 해당 보호 및 더 자세한 규칙 목록이 참조 hello 다음 [규칙 집합 핵심](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

또한 azure는 몇 가지 사용 하기 쉬운 기능 toohelp 제공 응용 프로그램에 대 한 인바운드 및 아웃 바운드 트래픽의 보안을 유지 합니다. Azure 고객 외부에서 제공 하 여 해당 응용 프로그램 코드의 보안을 유지 하면 제공 기능 tooscan 취약점에 대 한 웹 응용 프로그램.

- [다양한 인증 및 권한 부여 방법을 사용하여 웹앱 보안](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [앱에 대한 Azure Active Directory 인증 설정](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Transport Layer Security (TLS/SSL)-HTTPS를 사용 하 여 트래픽 tooyour 응용 프로그램 보안](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [HTTPS 연결을 통해 들어오는 모든 트래픽 강제 지정](http://microsoftazurewebsitescheatsheet.info/)

  - [엄격한 전송 보안(HSTS)을 사용하도록 설정](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [클라이언트의 IP 주소로 tooyour 앱 액세스를 제한 합니다.](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [클라이언트의 동작-요청 빈도 및 동시성을 통해 tooyour 응용 프로그램 액세스를 제한 합니다.](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Tinfoil Security 검사를 사용하여 취약성에 대한 웹앱 코드 검사](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [TLS 상호 인증 toorequire 클라이언트 인증서 tooconnect tooyour 웹 앱 구성](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Tooexternal 리소스를 연결 하는 응용 프로그램 toosecurely에서 사용 하 여 클라이언트 인증서를 구성 합니다.](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [응용 프로그램 페이지에서 표준 서버 헤더 tooavoid 도구를 제거 합니다.](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [지점 및 사이트 간 VPN을 사용하여 개인 네트워크의 리소스로 안전하게 앱 연결](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [하이브리드 연결을 사용하여 개인 네트워크의 리소스로 안전하게 앱 연결](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure 앱 서비스 사용 하 여 hello Azure 클라우드 서비스 및 가상 컴퓨터에 사용 되는 동일한 맬웨어 방지 솔루션입니다. 이 대해 자세히 toolearn 참조 tooour [맬웨어 방지 설명서](https://docs.microsoft.com/azure/security/azure-security-antimalware)합니다.

## <a name="secure-your-network-protect"></a>네트워크 보안(보호)
Microsoft Azure 응용 프로그램 및 서비스 연결 요구 사항 강력한 네트워킹 인프라 toosupport를 포함합니다. Azure 호스팅 리소스 및 hello 인터넷에서에서 tooand 및 Azure 있으며 온-프레미스 간에 Azure에 배치 된 리소스 간에 네트워크 연결 됩니다.

hello [Azure 네트워크 인프라](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) 사용 하도록 설정 하면 toosecurely 연결와 다른 Azure 리소스 tooeach [가상 네트워크 (Vnet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)합니다. VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다. VNet는 hello Azure 클라우드 전용 네트워크 tooyour 구독의 논리적 격리입니다. Vnet tooyour 온-프레미스 네트워크를 연결할 수 있습니다.

![네트워크 보안(보호)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

기본 네트워크 수준 액세스 제어 (IP 주소와 hello TCP 또는 UDP 프로토콜에 따라), 필요한 경우 사용할 수 있습니다 [네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)합니다. 보안 그룹 NSG (네트워크)은 기본 상태 저장 패킷 필터링 방화벽 toocontrol 액세스할 수에 따라 수 있으며 한 [5-튜플](https://www.techopedia.com/definition/28190/5-tuple)합니다.

Azure 네트워킹은 Azure 가상 네트워크에서 네트워크 트래픽에 대 한 hello 기능 toocustomize hello 라우팅 동작을 지원 합니다. Azure에서 [사용자 정의 경로](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)를 구성하면 이 작업을 수행할 수 있습니다.

[강제 터널링](https://www.petri.com/azure-forced-tunneling) tooensure 없는 서비스를 사용할 수 있는 메커니즘에 사용할 수 tooinitiate 연결 toodevices hello 인터넷 합니다.

Azure 지원 WAN 링크 연결 tooyour 온-프레미스 네트워크와 Azure 가상 네트워크와 전용 [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)합니다. hello를 통해 전달 되지 않는 전용된 연결을 사용 하 여 사이트와 Azure 간의 hello 링크 공용 인터넷 합니다. Azure 응용 프로그램에서 여러 데이터 센터를 실행 하는 경우 사용할 수 있습니다 [Azure 트래픽 관리자](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute 사용자의 요청을 hello 응용 프로그램의 인스턴스를 통해 자동으로 조정 합니다. 또한 트래픽 tooservices hello 인터넷에서에서 액세스할 수 있는 경우 Azure에서 실행 중이지 라우팅할 수 있습니다.

## <a name="virtual-machine-security-protect"></a>가상 컴퓨터 보안(보호)

[Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/)를 사용하면 다양한 컴퓨팅 솔루션을 민첩하게 배포할 수 있습니다. Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP 및 Azure BizTalk Services 지원을 통해 거의 모든 운영 체제에 모든 작업과 언어를 배포할 수 있습니다.

Azure를 사용할 수 있습니다 [맬웨어 방지 프로그램 소프트웨어](https://docs.microsoft.com/azure/security/azure-security-antimalware) Microsoft, Symantec, Trend Micro 및 Kaspersky tooprotect과 같은 보안 공급 업체에서 악의적인 파일, 애드웨어, 및 기타 위협을에서 가상 컴퓨터.

Azure Cloud Services 및 Virtual Machines를 위한 Microsoft 맬웨어 방지 프로그램은 바이러스, 스파이웨어 및 기타 악성 소프트웨어를 식별 및 제거하는 데 도움이 되는 실시간 보호 기능입니다. Microsoft 맬웨어 방지 자체 악성 또는 동의 없이 설치 된 소프트웨어 시도 tooinstall 알 수 없거나 Azure 시스템에서 실행 하는 경우 구성 가능한 알림을 제공 합니다.

[Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)은 자본 투자 없이 최소의 비용으로 응용 프로그램 데이터를 보호하는 확장성이 뛰어난 솔루션입니다. 응용 프로그램 오류로 인해 데이터가 손상되고 사용자 오류로 인해 응용 프로그램에 버그가 발생할 수 있습니다. Azure 백업은 Windows 및 Linux를 실행하는 가상 컴퓨터의 보호에 도움이 됩니다.

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)를 사용하면 기본 위치가 중단되는 경우 보조 위치에서 사용할 수 있도록 워크로드 및 앱의 복제, 장애 조치 및 복구를 오케스트레이션할 수 있습니다.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>규정 준수 확인: Cloud Services 실사 검사 목록(보호)

Microsoft 개발 [클라우드 서비스 Due 성실 검사 목록 hello](https://aka.ms/cloudchecklist.download) 번 실행 한 toohelp 조직 성실 이동 toohello 클라우드를 고려할 합니다. 모든 형식과 크기의 조직에 대 한 구조를 제공-개인 기업과 조직 공공 부문의 모든 수준 및 비영리에서 정부를 포함 하 여-tooidentify 고유한 성능, 서비스, 데이터 관리 및 거 버 넌 스 목표 및 요구 사항입니다. 따라서 최종적으로 클라우드 서비스 계약에 대 한 hello 기반을 형성 되는 다른 클라우드 서비스 공급자의 toocompare hello 제공이 있습니다.

hello 검사 목록은 새 국제 표준 클라우드 서비스 계약에 대 한 ISO/IEC 19086 절 여 절을 정렬 하는 프레임 워크를 제공 합니다. 이 표준은 통합된 조직 toohelp 클라우드 채택에 대 한 결정을 내릴 및 클라우드 서비스 제공을 비교 하기 위한 공통 기반을 만들기 위한 고려 사항 집합을 제공 합니다.

hello 검사 목록에 클라우드 서비스 공급자를 선택 하기 위한 일관 되 고 반복 가능한 접근 방식 및 구조화 된 지침을 제공 하는 철저 하 게 심사 된 이동 toohello 클라우드를 승격 합니다.

클라우드 채택은 더 이상 단순히 기술 의사 결정이 아닙니다. 검사 목록 요구 사항 조직의 모든 측면에서 터치, 때문에 서비스가 제공 tooconvene 모든 키 내부-결정권자-hello CIO 및 CISO 뿐만 아니라 법적으로 위험 관리, 조달 및 규정 준수 전문가입니다. 이는 hello 의사 결정 프로세스와 소리 추론, 예기치 않은 장애물 tooadoption hello 가능성을 줄이는에 명확 하 게 의사 결정 hello 효율성을 높입니다.

또한 hello 검사 목록:

- 의사 결정자 hello 클라우드 채택 프로세스의 hello 시작 부분에 대 한 키 토론 주제를 노출합니다.

- 개인 정보, pii (개인), 개인 식별이 가능한 정보 및 데이터 보안에 대 한 규정 및 hello 조직의 목표에 대 한 철저 한 비즈니스 토론을 지원합니다.

- 조직에서 클라우드 프로젝트에 영향을 줄 수 있는 잠재적인 문제를 식별하는 데 도움을 줍니다.

- Hello로 질문의 일관성 집합을 제공 동일한 용어, 정의 메트릭 및 다른 클라우드 서비스 공급자의 제공 비교 toosimplify hello 프로세스 각 공급자에 대 한 결과물입니다.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Azure 인프라 및 응용 프로그램 보안 유효성 검사(검색)

[Azure Operational 보안](https://docs.microsoft.com/azure/security/azure-operational-security) toohello 서비스, 컨트롤 및 기능 사용 가능한 toousers 데이터, 응용 프로그램 및 Microsoft Azure에서 기타 자산을 보호 하기 위한 참조 합니다.

![보안 유효성 검사(검색)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Azure Operational 보안 hello Microsoft SDL Security Development Lifecycle (), 보안 응답 센터 Microsoft hello 포함 하는 고유한 tooMicrosoft 있는 다양 한 기능을 통해 얻은 hello 정보를 통합 하는 프레임 워크에 만들어집니다. 프로그램 및 hello 사이버 안보 위협 상황의 심층 인식 합니다.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft OMS(Operations Management Suite)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 는 hello hello 하이브리드 클라우드 용 IT 관리 솔루션입니다. 단독으로 사용 하거나 기존 System Center 배포 OMS를 사용 하면 tooextend hello 최대 유연성과 인프라의 클라우드 기반 관리에 대 한 제어 합니다.

![Microsoft OMS(Operations Management Suite)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

OMS를 사용하면 경쟁력 있는 솔루션보다 저렴한 비용으로 온-프레미스, Azure, AWS, Windows Server, Linux, VMware 및 OpenStack을 포함한 모든 클라우드의 모든 인스턴스를 관리할 수 있습니다. OMS를 새로운 접근 방식을 toomanaging에서는 클라우드 우선 world hello에 대 한 기본 제공 hello 가장 빠르고 가장 비용 효과적인 방법 toomeet 새로운 비즈니스 과제 하 고 응용 프로그램 및 클라우드 환경을 새 워크 로드를 수용 하는 기업입니다.

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)는 관리형 리소스의 데이터를 중앙 리포지토리로 수집하여 OMS에 대한 모니터링 서비스를 제공합니다. 이 데이터는 이벤트, 성능 데이터 또는 hello API 통해 제공 되는 사용자 지정 데이터에 포함 될 수 있습니다. 수집 되 면 hello 데이터는 경고, 분석 및 내보내기에 사용할 수 있습니다.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

이 방법을 사용 하면 다양 한 소스에서에서 tooconsolidate 데이터를 결합할 수 있으므로 데이터는 기존 Azure 서비스를 온-프레미스 환경. 모든 작업을 사용할 수 있는 tooall 종류의 데이터를 해당 데이터에 대해 수행한 hello 동작의 결과로 명확 하 게 hello 데이터의 hello 컬렉션을 구분 합니다.

### <a name="azure-security-center"></a>Azure Security Center

[Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro) 사용 방지를 감지 하 고 및 toothreats 파악할을 사용 하 여 응답을 제어할 수 hello Azure 리소스의 보안 합니다. 이는 Azure 구독에 대해 통합된 보안 모니터링 및 정책 관리를 제공하고 다른 방법으로 발견되지 않을 수 있는 위협을 감지하는 데 도움이 되며 보안 솔루션의 광범위한 환경에서 작동합니다.

보안 센터에 Azure 리소스 tooidentify 잠재적인 보안 취약점의 hello 보안 상태를 분석합니다. 권장 사항 목록 hello 필요한 컨트롤을 구성 과정을 안내 합니다.

예를 들면 다음과 같습니다.

- 맬웨어 방지 프로 비전 toohelp 식별 하 고 악성 소프트웨어를 제거 합니다.

- 네트워크 보안 그룹 및 규칙 toocontrol 트래픽 tooVMs 구성

- 웹 응용 프로그램 방화벽 toohelp 웹 응용 프로그램을 대상으로 하는 공격을 방어할의 프로 비전

- 누락된 시스템 업데이트 배포

- 초기 권장 hello와 일치 하지 않는 운영 체제 구성을 주소 지정

보안 센터 자동으로 수집, 분석 및 Azure 리소스, hello 네트워크 및 맬웨어 방지 프로그램 및 방화벽와 같은 파트너 솔루션에서 로그 데이터를 통합 합니다. 위협이 감지되었을 때 보안 경고가 생성됩니다. 감지되는 사항의 예:

- 알려진 악성 IP 주소와 통신하는 손상된 VM

- Windows 오류 보고를 사용하여 감지된 고급 맬웨어 프로그램

- VM에 대한 무작위 공격

- 통합 맬웨어 방지 프로그램 및 방화벽에서의 보안 경고

### <a name="azure-monitor"></a>Azure Monitor

[Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) 특정 유형의 리소스에 대 한 포인터 tooinformation을 제공 합니다. 시각화, 쿼리, 라우팅, 경고, 자동 크기 조정 및 자동화 hello Azure 인프라 (활동 로그)에서 데이터 및 각 개별 Azure 리소스 (진단 로그의 경우)에 제공합니다.

클라우드 응용 프로그램은 이동하는 부분이 많아 복잡합니다. 모니터링 없이 계속 응용 프로그램 데이터 tooensure 정상 상태에서 실행 되 고 제공 합니다. 또한 있습니다 toostave 잠재적 문제를 해제 하거나 문제를 해결 하십시오. 지난 수 있습니다.

![Azure 모니터](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) 또한 응용 프로그램에 대 한 모니터링 데이터 toogain 깊은 통찰력을 사용할 수 있습니다. 이 정보는 tooimprove 응용 프로그램 성능이 나 유지 관리의 편의성 하는 데 도움이 하거나 수동 개입 해야 하는 작업을 자동화할 수 있습니다.

네트워크 보안 감사는 네트워크 취약성을 검색하고 IT 보안 및 규제 관리 모델을 준수하는 것이 중요합니다. 보안 그룹 보기를 사용 하면 수 hello 구성 된 네트워크 보안 그룹 및 보안 규칙 검색으로 hello 효과적인 보안 규칙. 적용 되는 규칙 hello 목록을 사용 하 여 열려 있는 hello 포트 및 ss 네트워크 취약점을 확인할 수 있습니다.

### <a name="network-watcher"></a>Network Watcher

[네트워크 감시자](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) toomonitor 수 있는 지역 서비스 이며에서 및에서 Azure 네트워크 수준에서 상태를 진단 합니다. 네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다. 이 서비스에는 패킷 캡처, 다음 홉, IP 흐름 확인, 보안 그룹 보기, NSG 흐름 로그가 포함되어 있습니다. 수준 모니터링 시나리오는 전체적인 tooend 뷰 대비 tooindividual 네트워크 리소스 모니터링의 네트워크 리소스를 제공합니다.

### <a name="storage-analytics"></a>저장소 분석

[Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) 요청 tooa 저장소 서비스에 대 한 집계 된 트랜잭션 통계 및 용량 데이터가 포함 된 메트릭을 저장할 수 있습니다. Hello 저장소 서비스 수준에서 뿐만 아니라 두 hello API 작업 수준에서 트랜잭션을 보고 하 고 용량은 hello 저장소 서비스 수준에서 보고 됩니다. 메트릭 데이터는 사용 되는 tooanalyze 저장소 서비스 사용 될, hello 저장소 서비스 및 서비스를 사용 하는 응용 프로그램의 tooimprove hello 성능에 대해 수행 된 요청 문제를 진단할 수 있습니다.

### <a name="application-insights"></a>Application insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview)는 여러 플랫폼의 웹 개발자를 위한 확장성 있는 APM(Application Performance Management) 서비스입니다. Toomonitor를 사용 하 여 라이브 웹 응용 프로그램입니다. 성능 이상을 자동으로 감지합니다. 사용자가 앱을 사용 하 여 수행할 toounderstand 및 문제를 진단 하는 강력한 분석 도구 toohelp을 포함 됩니다. 기능은 toohelp 성능과 유용성 지속적으로 향상 됩니다. 앱에 대 한 작동.NET, Node.js 및 J2EE 포함 하는 플랫폼은 다양 한 온-프레미스 호스팅 또는 hello 클라우드에 있습니다. 것 devOps 프로세스와 통합 되어 있으며 연결 포인트 tooa 다양 한 개발 도구입니다.

다음 사항을 모니터링합니다.

- **요청 속도, 응답 시간 및 실패율** - 하루 중 어느 시간에 어떤 페이지를 가장 많이 방문하는지, 사용자가 어디에 있는지 확인합니다. 어떤 페이지가 가장 성능이 우수한지 확인합니다. 요청이 더 있는데 응답 시간과 실패율이 높아지면 아마도 리소스 문제가 있는 것입니다.

- **종속성 비율, 응답 시간 및 실패율** - 외부 서비스 때문에 속도가 느려지는지 확인합니다.

- **예외** -hello 집계 통계를 분석 하거나 특정 인스턴스를 선택 하 고 hello 스택 추적 및 관련된 요청으로 드릴 합니다. 서버 및 브라우저 예외가 전부 보고됩니다.

- **페이지 보기 및 로드 성능** - 사용자의 브라우저에서 보고합니다.

- **웹 페이지의 AJAX 호출** - 속도, 응답 시간 및 실패율

- **사용자 및 세션 수**

- Windows 또는 Linux 서버 컴퓨터의 **성능 카운터** - CPU, 메모리, 네트워크 사용량 등.

- Docker 또는 Azure의 **호스트 진단**.

- 앱의 **진단 추적 로그** - 추적 이벤트를 요청과 상호 연결하는 데 사용됩니다.

- **사용자 지정 이벤트 및 메트릭을** hello 클라이언트 또는 서버 코드, 예: 판매 된 항목 tootrack 비즈니스 이벤트 또는 긴 게임에 직접 작성 있습니다.
일반적으로 많은 구성 요소가 – 미정 가상 컴퓨터, 저장소 계정 및 가상 네트워크 또는 웹 응용 프로그램, 데이터베이스, 데이터베이스 서버 및 타사 서비스의 응용 프로그램에 대 한 hello 인프라 구성 됩니다. 이러한 구성 요소를 별도 엔터티로 표시하지 않으면, 대신 관련된 단일 엔터티의 상호 종속적으로 부분으로 표시됩니다. Toodeploy, 관리, 한 그룹으로 보고 모니터링 합니다. [Azure 리소스 관리자](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) toowork hello 리소스 그룹으로 솔루션에 있습니다.

배포 지정, 업데이트 또는 단일, 통합 작업에서 솔루션에 대 한 모든 hello 리소스를 삭제 합니다. 배포용 템플릿을 사용하고 이 템플릿을 테스트, 스테이징 및 프로덕션과 같은 여러 환경에서 사용할 수 있습니다. 리소스 관리자는 감사 보안을 제공 하 고 리소스 배포 된 후 관리 기능 toohelp 태그를 지정 합니다.

**리소스 관리자를 사용 하 여 hello 이점**

리소스 관리자는 다음과 같은 여러 이점이 있습니다.

- 배포, 관리 하 고 이러한 리소스를 개별적으로 처리 하지 않고 그룹에서 솔루션에 대 한 모든 hello 리소스를 모니터링할 수 있습니다.

- 반복 해 서 hello 개발 수명 주기 전체에서 솔루션을 배포할 수 있으며 것을 확신할 리소스 일관 된 상태로 배포 됩니다.

- 스크립트가 아닌 선언적 템플릿을 통해 인프라를 관리할 수 있습니다.

- Hello 올바른 순서로 배포 되므로 리소스 간의 종속성을 hello를 정의할 수 있습니다.

- 역할 기반 액세스 제어 (RBAC) hello 관리 플랫폼에 고유 하 게 통합 되어 있으므로 리소스 그룹에 대 한 액세스 제어 tooall 서비스를 적용할 수 있습니다.

- 태그를 적용할 수 tooresources toologically 구독에서 모든 hello 리소스를 구성 합니다.

- 리소스 그룹에 대 한 비용을 확인 하 여 조직의 요금 청구를 명확 하 게 같은 태그를 hello 공유 합니다.

> [!Note]
> 리소스 관리자는 새로운 방식으로 toodeploy 제공 하 고 솔루션을 관리 합니다. 사용 하는 경우 이전 버전의 배포 모델을 hello 및 toolearn hello 변경에 대 한 원하는, 참조 [이해 리소스 관리자 배포 및 클래식 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model)합니다.

## <a name="next-steps"></a>다음 단계

다음과 같은 심층적인 일부 보안 항목을 참조하여 보안에 대한 자세한 내용을 확인할 수 있습니다.

- [감사 및 로깅](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [사이버 범죄](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [설계 및 운영 보안](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [암호화](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [ID 및 액세스 관리](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [네트워크 보안](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [위협 관리](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
