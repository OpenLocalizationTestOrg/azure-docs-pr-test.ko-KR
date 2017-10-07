---
title: "aaaWhat은 Azure Active Directory 란?"
description: "사용 하 여 Azure Active Directory tooextend hello에 기존 온-프레미스 id 클라우드 또는 Azure AD를 개발 응용 프로그램을 통합 합니다."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.assetid: 498820c4-9ebe-42be-bda2-ecf38cc514ca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.custom: it-pro
ms.openlocfilehash: b470d7d8f0e733fe9363bd46ed2c2d143d5b3982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-active-directory"></a>Azure Active Directory란?
Azure AD(Azure Active Directory)는 Microsoft의 다중 테넌트 클라우드 기반 디렉터리 및 ID 관리 서비스입니다. Azure AD는 핵심 디렉터리 서비스, 고급 ID 통제 및 응용 프로그램 액세스 관리 기능을 모두 제공합니다. Azure AD는 또한 개발자가 있는 풍부한 표준 기반 플랫폼 toodeliver 액세스 제어 tootheir 응용 프로그램을 중앙 집중식된 정책 및 규칙에 따라 제공 합니다. 

IT 관리자에 대 한 Azure AD는 솔루션을 제공 경제적이 고 쉬운 toouse toogive 직원 및 비즈니스 파트너 single sign on (SSO) 액세스 너무[클라우드 SaaS 응용 프로그램에서는 수천](active-directory-saas-tutorial-list.md) office 365, Salesforce.com, DropBox, 같은 및 Concur 합니다.

응용 프로그램 개발자를 위한 Azure AD에서는 수백만 개 조직에서 신속 하 고는 세계 클래스 id 관리 솔루션으로 간단한 toointegrate 함으로써 응용 프로그램 사용에 hello world.

Azure AD에는 다단계 인증, 장치 등록, 셀프 서비스 암호 관리, 셀프서비스 그룹 관리, 권한 있는 계정 관리, 역할 기반 액세스 제어, 응용 프로그램 사용 모니터링, 광범위한 감사 및 보안 모니터링 및 경고를 포함하는 완전한 ID 관리 기능이 포함되어 있습니다. 이러한 기능을 통해 클라우드 기반 응용 프로그램을 보호하고, IT 프로세스를 간소화하고, 비용을 절감하고, 회사의 규정 준수 목표를 충족할 수 있도록 합니다.

와 마찬가지로 또한 [4 번의 클릭](./connect/active-directory-aadconnect-get-started-express.md), 기존 Windows Server Active Directory와 Azure AD를 통합할 수 있습니다, 조직 hello 기능 tooleverage 제공 기존 온-프레미스 id 투자 toomanage 액세스 toocloud는 SaaS 응용 프로그램을 기반으로 합니다.

Office 365, Azure 또는 Dynamics CRM Online 고객인 경우 이미 Azure AD를 사용하고 있다는 것을 알지 못할 수도 있습니다. 모든 Office 365, Azure 및 Dynamics CRM 테넌트는 실제로 이미 Azure AD 테넌트입니다. 사용 하기를 원할 때마다 다른 클라우드 응용 프로그램이 Azure AD의 테 넌 트 toomanage 액세스 toothousands 해당와 통합 되어!

![Azure AD Connect 스택](./media/active-directory-whatis/Azure_Active_Directory.png)

## <a name="how-reliable-is-azure-ad"></a>Azure AD가 안정적입니까?
Azure AD의 hello 다중 테 넌 트, 지리적으로 분산, 높은 가용성 디자인 의미 가장 중요 한 비즈니스 요구에를 사용할 수 있습니다. 28 데이터를 활용 하는 hello world 센터 with 자동된 장애 조치를 실행 해야 합니다. hello 편안 하 게 Azure AD는 안정성이 높아야 하는 데이터 센터의 작동이 중지 하는 경우에 디렉터리 데이터의 복사본 두 개 이상 동시에 더으로 분산 되어 있는 데이터를 알고 있으면 에 중점을 즉시 액세스할 수 있습니다.

자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.

## <a name="choose-an-edition"></a>버전 선택
모든 Microsoft Online 비즈니스 서비스는 로그온 및 기타 ID가 필요로 할 때 Azure Active Directory(Azure AD)를 사용합니다. Tooany (예: Office 365 또는 Microsoft Azure)는 Microsoft Online 비즈니스 서비스를 구독 하면 Azure AD와 액세스 tooall hello 무료 기능을 얻을 수 있습니다. Hello Azure Active Directory Free edition에서는 있습니다 수 사용자 및 그룹 관리, 온-프레미스 디렉터리와의 동기화, Azure, Office 365와 Salesforce, Workday, Concur, DocuSign와 같은 인기 있는 SaaS 응용 프로그램에서 single sign on 가져오기 Google Apps, Box, ServiceNow, Dropbox, 및 더 합니다. 

tooenhance Azure Active Directory를 Azure Active Directory Basic, 프리미엄 P1 및 P2 Premium edition hello 사용 하 여 유료 기능을 추가할 수 있습니다. Azure Active Directory 유료 버전은 기존 무료 디렉터리 위에 구축되어 모바일 작업자를 위한 셀프 서비스를 확장하는 엔터프라이즈 클래스 기능, 향상 된 모니터링, 보안 보고, Multi-Factor Authentication(MFA) 및 보안 액세스를 제공합니다.

> [!NOTE]
> 이러한 버전의 옵션 가격 hello에 대 한 참조 [Azure Active Directory 가격](https://azure.microsoft.com/pricing/details/active-directory/)합니다. Azure Active Directory Premium P1, Premium P2 및 Azure Active Directory Basic은 중국에서 현재 지원되지 않습니다. 자세한 내용은 hello Azure Active Directory 포럼에 문의 하십시오.
>

* **Azure Active Directory Basic** - 클라우드를 주로 필요로 하는 작업자를 위해 설계된 이 버전은 클라우드 중심 응용 프로그램 액세스 및 셀프 서비스 ID 관리 솔루션을 제공합니다. Azure Active directory Basic edition hello 사용 하면 생산성 향상 가져오고 그룹 기반의 액세스 관리, 클라우드 응용 프로그램 및 Azure Active Directory 응용 프로그램 프록시 (toopublish에 셀프 서비스 암호 재설정과 같은 기능을 줄이면 비용 99.9% 가동률의 엔터프라이즈 수준 SLA에서 지 원하는 모든 온-프레미스 웹 응용 프로그램 Azure Active Directory를 사용 하 여).
* **Azure Active Directory 프리미엄 P1** -tooempower 조직 더 많이 사용 되는 설계 id 및 액세스 관리, Azure Active Directory Premium 버전 기능을 갖춘 엔터프라이즈 수준 id 관리 기능을 추가 하 고 활성화 하이브리드 사용자 tooseamlessly 온-프레미스에 액세스 및 클라우드 기능입니다. 이 버전에서는 정보 근로자 및 하이브리드 환경에서 identity 관리자에 대 한 응용 프로그램 액세스, 셀프 서비스 id 및 액세스 관리 (IAM), id 보호 및 보안 hello 클라우드에서 간에 필요한 모든 항목입니다. 동적 그룹 및 셀프 서비스 그룹 관리와 같은 고급 관리 및 위임 리소스를 지원합니다. 온-프레미스 사용자를 위한 셀프 서비스 암호 재설정과 같은 솔루션을 사용하여 Microsoft ID 관리자(온-프레미스 ID 및 액세스 관리 제품군)를 포함하며 클라우드 쓰기 저장 기능을 제공합니다.
* **Azure Active Directory 프리미엄 P2** -모든 사용자와 관리자에 대 한 고급 보호에 두고 설계, 새 제공이 기능이 포함 된 모든 hello Azure AD Premium P1으로 새 Id 보호 권위 있는 Id에 관리 합니다. Azure Active Directory Id 보호 신호 tooprovide 위험 기반 조건부 액세스 tooyour 응용 프로그램 및 중요 한 회사 데이터의 10 억을 활용합니다. 에서는 관리 하 고 Azure Active Directory Privileged Identity management는 권한 있는 계정을 검색할 수 없도록 보호 하려는 경우 도움말도 제한 관리자 및 해당 액세스 tooresources 및 모니터링 필요할 때 적시에 대 한 액세스를 제공 합니다.  

> [!NOTE]
> 다양한 Azure Active Directory 기능은 "종량제" 버전을 통해 사용할 수 있습니다.
>
> * Active Directory B2C는 hello id 및 액세스 관리 솔루션으로 소비자 용 응용 프로그램에 대 한 합니다. 자세한 내용은 [Azure Active Directory B2C](https://azure.microsoft.com/documentation/services/active-directory-b2c/)
> * Azure Multi-Factor Authentication는 사용자 또는 인증 공급자 단위를 통해 사용될 수 있습니다. 자세한 내용은 [Azure Multi-Factor Authentication 정의](../multi-factor-authentication/multi-factor-authentication.md)
>

## <a name="how-can-i-get-started"></a>어떻게 시작하나요?

**IT 관리자인 경우:**

* [사용해 보세요!](https://azure.microsoft.com/trial/get-started-active-directory/) - 지금 무료 30일 평가판에 등록하면 이 링크를 사용하여 5분 내에 첫 번째 클라우드 솔루션을 배포할 수 있습니다.

* Azure AD 테넌트를 시작하고 빠르게 실행하는 팁과 요령은 [Azure AD 시작](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium)을 참조하세요.

**개발자인 경우:**
 
* 체크 아웃 우리의 [Developers Guide](active-directory-developers-guide.md) tooAzure Active Directory

* [평가판 시작](https://azure.microsoft.com/trial/get-started-active-directory/) – 지금 무료 30일 평가판에 등록하고 Azure AD와 앱을 통합하기 시작합니다.

## <a name="next-steps"></a>다음 단계
[Id 및 액세스 관리를 Azure의 hello 기본 사항에 대 한 자세한 정보](https://docs.microsoft.com/azure/active-directory/identity-fundamentals)
