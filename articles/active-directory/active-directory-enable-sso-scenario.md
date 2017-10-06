---
title: "Azure Active Directory와 응용 프로그램 aaaManaging | Microsoft Docs"
description: "이 문서 hello Azure Active Directory 온-프레미스, 클라우드 및 SaaS 응용 프로그램 통합의 혜택."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Azure Active Directory로 응용 프로그램 관리
Hello 실제 워크플로 또는 콘텐츠 외 기업에는 모든 응용 프로그램에 대 한 두 가지 기본 요구 사항이 있습니다.

1. tooincrease 생산성, 응용 프로그램 쉽게 toodiscover 및 액세스 해야 합니다.
2. 제어 및 감독은 사용자 수 및 실제로 액세스 하는 각 응용 프로그램에 hello 조직에 필요한 tooenable 보안 및 거 버 넌 스

가장 잘 액세스가 가능 identity toocontrol를 사용 하 여 클라우드 응용 프로그램의 hello world "*toodo 어떤 허용 하는 누구 입니까*"입니다.

용어 계산에서

* *가* 라고 *identity* -hello 사용자 및 그룹 관리
* *어떤* 라고 *액세스 관리* – hello 액세스 tooprotected 리소스 관리

두 구성 요소를 함께 라고 *Id 및 액세스 관리 (IAM)*, hello로 정의 된 [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) 으로 "*hello hello 오른쪽 수 있도록 하는 보안 규칙 hello에 개인 tooaccess hello 오른쪽 리소스 이유가 hello에 대 한 시간을 마우스 오른쪽 단추로*"입니다.

알겠습니다 hello 문제는 무엇이 있습니까? IAM이 한 곳에서 통합 솔루션으로 *관리되지 않는* 경우 다음과 같습니다.

* Identity 관리자가 만들고 모든 응용 프로그램에서 사용자 계정을 업데이트 하거나 별도로 tooindividually 중복 및 시간이 오래 걸리는 작업입니다.
* 사용자는 여러 자격 증명 tooaccess hello 필요한 응용 프로그램으로 toowork toomemorize를가지고 있습니다. 결과적으로, 사용자 암호 아래로 toowrite 경향이 또는 기타 데이터 보안 위험을 소개 하는 다른 암호 관리 솔루션을 사용 합니다.
* 중복 시간이 오래 걸리는 작업에는 사용자의 hello 양을 줄일 수 있으며 관리자 비즈니스의 결론을 증가 하는 비즈니스 활동에 작동 합니다.

따라서 무엇이 일반적으로 조직이 통합된 IAM 솔루션을 채택하지 못하게 합니까?

* 대부분의 기술 솔루션 배포 하 고 자신의 응용 프로그램에 대 한 각 조직에서 조정할 toobe 해야 하는 소프트웨어 플랫폼을 기반으로 합니다.
* 종종 클라우드 응용 프로그램은 IT 조직이 기존 IAM 솔루션을 통합할 수 있는 것 보다 빠른 속도로 적용됩니다.
* 보안 및 모니터링 도구 추가 사용자 지정 및 통합 tooachieve 포괄적인 E2E 시나리오 필요 합니다.

## <a name="azure-active-directory-integrated-with-applications"></a>응용 프로그램과 통합된 Azure Active Directory
Azure Active Directory는 Microsoft의 포괄적인 IDaaS(Identity as a Service) 솔루션입니다.

* 클라우드 서비스로 IAM 사용 
* 중앙 액세스 관리, SSO(Single Sign-On) 및 보고 제공 
* 통합 된 액세스 관리에 대 한 지원 [응용 프로그램](https://azure.microsoft.com/marketplace/active-directory/) hello 응용 프로그램 갤러리에서 비롯 한 Salesforce, Google Apps, Box, Concur, 및 더 합니다. 

Azure Active Directory와 모든 응용 프로그램에 게시 하면 파트너 및 고객 (비즈니스 또는 소비자) hello 들이 동일한 id 및 액세스 관리 기능.<br> 이 사용 하면 toosignificantly 운영 비용을 절감 합니다.

경우에 어떻게 tooimplement hello 응용 프로그램 갤러리에 아직 나열 되지 않은 응용 프로그램 필요 한가요? Hello 응용 프로그램 갤러리에서 응용 프로그램에 대 한 SSO를 구성 하는 것 보다 좀 더 빠릅니다 이지만, Azure AD hello 구성으로 하는 데 도움이 되는 마법사를 제공 합니다.

Azure AD의 hello 값이 "바로" 클라우드 응용 프로그램을 초과 합니다. 또한 보안된 원격 액세스를 제공하여 온-프레미스 응용 프로그램과 함께 사용할 수도 있습니다. 보안 된 원격 액세스 Vpn 또는 다른 기존의 원격 액세스 관리 구현에 대 한 hello hello 필요성을 없앨 수 있습니다.

모든 응용 프로그램에 대 한 중앙 액세스 관리 및 single sign-on (SSO)을 제공 하 여 Azure AD toohello 기본 데이터 보안 및 생산성 문제 hello 솔루션을 제공 합니다.

* 사용자는 여러 응용 프로그램 제공 더 많은 시간 tooincome 생성 또는 비즈니스 작업 활동을 수행 하는 하나의 로그온을 액세스할 수 있습니다.
* Identity 관리자 액세스 tooapplications 한 곳에서 관리할 수 있습니다.

회사 및 hello 사용자에 대 한 hello 혜택은 사용 합니다. 좀 더 자세히 살펴보고 id 관리자 및 hello 조직에 대 한 hello 이점 살펴보겠습니다.

## <a name="integrated-application-benefits"></a>통합된 응용 프로그램 혜택
hello SSO 프로세스에 두 개의 단계가 있습니다.

* 인증, hello hello 사용자의 id 유효성을 검사 하는 프로세스입니다.
* 권한 부여 결정 tooenable hello 또는 액세스 정책 사용 하 여 tooa 리소스 액세스를 차단 합니다.

사용할 경우 Azure AD toomanage 응용 프로그램 및 SSO 사용 하도록 설정:

* 인증은 hello 사용자의 온-프레미스 (예: AD) 또는 Azure AD 계정에서 수행 됩니다.
* 권한 부여 hello Azure AD 할당 및 보호 정책에 일관성 있는 최종 사용자 환경을 보장 하 고 tooadd 할당, 위치 및 그 내부 기능에 관계 없이 모든 응용 프로그램에 대 한 MFA 조건 있게를 실행 합니다.

중요 한 방식으로 hello 권한 부여 hello toounderstand는 hello 대상 응용 프로그램에 적용 하기 hello 응용 프로그램 Azure AD와 통합 된 방식에 따라 달라 집니다.

* **서비스 공급자에 의해 미리 통합된 응용 프로그램** Office 365나 Azure와 같이 이러한 응용 프로그램은 Azure AD에서 직접 작성하고 해당되는 포괄적인 ID 및 액세스 관리 기능을 사용합니다. 액세스 toothese 응용 프로그램 디렉터리 정보 및 토큰 발급 통해 설정 됩니다.
* **Microsoft 및 사용자 지정 응용 프로그램에서 통합된 응용 프로그램** 내부 응용 프로그램 디렉터리를 사용하고 Azure AD와 독립적으로 작동할 수 있는 독립적인 클라우드 응용 프로그램입니다. 액세스 toothese 응용 프로그램은 응용 프로그램 특정 자격 증명 매핑된 tooan 응용 프로그램 계정을 실행 하 여 활성화 됩니다. Hello 응용 프로그램 기능에 따라 페더레이션 토큰 또는 사용자 이름 및 암호 hello 응용 프로그램에서 이전에 프로 비전 된 계정에 대 한 hello 자격 증명 수 있습니다.
* **온-프레미스 응용 프로그램** 응용 프로그램은 주로 tooon 온-프레미스 응용 프로그램에서 액세스를 사용 하는 hello Azure AD 응용 프로그램 프록시를 통해 게시 합니다. 이러한 응용 프로그램은 Windows Server Active Directory와 같은 온-프레미스 디렉터리를 사용합니다. 액세스 toothese 응용 프로그램 요구 사항 로그온 온-프레미스 hello 적용 하면서 hello 프록시 toodeliver hello 응용 프로그램 콘텐츠 toohello 최종 사용자를 트리거하여 활성화 됩니다.

예를 들어 사용자 조직에 조인 하는 경우 필요한 계정을 toocreate hello 사용자에 대 한 작업용 hello 기본 로그온에 Azure AD에서 합니다. 이 사용자가 Salesforce와 같은 액세스 tooa 관리 되는 응용 프로그램을 필요한 경우도 toocreate 계정이 Salesforce에서이 사용자에 대 한 필요 하 고 toohello Azure 계정 toomake SSO 작업에 연결 합니다. Hello 사용자가 조직을 떠난, 좋습니다 toodelete hello Azure AD 계정 응용 프로그램과의 모든 테이블에 해당 계정의 hello hello 사용자에 게 hello 응용 프로그램의 IAM 저장소입니다.

## <a name="access-detection"></a>액세스 감지
오늘날의 기업에서 IT 부서에서는 사용 중인 모든 hello 클라우드 응용 프로그램의 인식 종종 하지 않습니다. Cloud App Discovery와 함께, Azure AD는 제공 솔루션 toodetect 이러한 응용 프로그램입니다.

## <a name="account-management"></a>계정 관리
일반적으로 hello에서 계정을 관리 다양 한 응용 프로그램은 수동으로 수행한 IT 또는 hello 조직의 개인을 지원 합니다. Azure AD는 모든 서비스 공급자 통합 응용 프로그램에 걸쳐 계정 관리를 완전히 자동화했으며 해당 응용 프로그램은 Microsoft가 지원하는 자동화된 사용자 프로비전 또는 SAML JIT에서 사전 통합되었습니다.

## <a name="automated-user-provisioning"></a>자동화된 사용자 프로비전
일부 응용 프로그램은 계정 만들기 및 제거(또는 비활성화)에 자동화 인터페이스를 제공합니다. 공급자가 이러한 인터페이스를 제공하는 경우 Azure AD에서 활용됩니다. 관리 작업을 자동으로 발생 하기 때문에 운영 비용을 감소 하 고 hello 무단된 액세스 가능성이 줄어들기 때문에 hello 환경의 보안을 향상 시킵니다.

## <a name="access-management"></a>액세스 관리
Azure AD를 사용 하 여 액세스 tooapplications를 사용 하 여 개별 또는 할당을 제어 하는 규칙을 관리할 수 있습니다. 액세스 관리 toohello 적임자 hello 조직 등과 hello 최상의 감독 및 기술 지원팀의 hello 부담을 줄이는 위임할 수 있습니다.

## <a name="on-premises-applications"></a>온-프레미스 응용 프로그램
응용 프로그램 프록시에 기본 제공 hello toopublish를 일관 둘 다에 온-프레미스 응용 프로그램 tooyour 사용자가 Azure AD 모니터링, 보고 및 보안 기능에서 최신 클라우드 응용 프로그램 및 hello 이점 사용 경험에 액세스할 수 있습니다. .

## <a name="reporting-and-monitoring"></a>보고 및 모니터링
Azure AD와 사전 통합 된 보고 및 모니터링 tooknow 누구에 게 액세스 tooapplications 있으며이 경우 실제로 사용을 사용할 수 있는 기능을 제공 합니다.

## <a name="related-capabilities"></a>관련 기능
Azure AD를 사용하여 세부적인 액세스 정책 및 사전 통합된 MFA로 응용 프로그램을 보호할 수 있습니다. Azure MFA에 대 한 자세한 참조 toolearn [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/)합니다.

## <a name="getting-started"></a>시작
Azure AD와 응용 프로그램 통합을 시작 하는 tooget hello 살펴보세요 [Azure Active Directory 통합을 시작 하는 응용 프로그램과 함께 시작 가이드](active-directory-integrating-applications-getting-started.md)합니다.

## <a name="see-also"></a>참고 항목
[Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

