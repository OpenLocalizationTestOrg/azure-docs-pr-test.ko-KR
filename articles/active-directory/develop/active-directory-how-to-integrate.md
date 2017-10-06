---
title: "Azure Active Directory와 aaaHow tooIntegrate | Microsoft Docs"
description: "가이드 toobenefits 및 Azure Active Directory와의 통합에 대 한 리소스입니다."
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Azure Active Directory와의 통합
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory는 클라우드 응용 프로그램에 대해 엔터프라이즈급 ID 관리를 조직에 제공합니다.  Azure AD 통합 된 간소화 된 로그인 환경을 사용자에 게 제공 하 고 tooIT 정책을 준수 하는 응용 프로그램을 지원 합니다.

## <a name="how-toointegrate"></a>어떻게 tooIntegrate
여러 가지 방법으로 Azure AD와 응용 프로그램 toointegrate 프로그램에 대 한 합니다.  응용 프로그램에 맞게 이 시나리오를 활용하세요.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>TooYour 응용 프로그램에서에서 방식으로 tooSign으로 Azure AD를 지원 합니다.
**로그인 충돌을 줄이고 지원 비용을 절감합니다.** Azure AD toosign를 tooyour 응용 프로그램에서 사용 하 여 사용자가 한 더 많은 이름 및 암호 tooremember가 없을 있습니다.  개발자는 적은 하나의 암호 toostore 있어야 하 고 보호 합니다.  Toohandle 잊은 암호를 다시 설정 하지 않은 것 만으로는 크게 절약할 수 있습니다.  Azure AD의 hello 세계에서 가장 인기 있는 클라우드 응용 프로그램을 Office 365 및 Microsoft Azure를 포함 하 여 일부에 대 한 로그인을에서는 제공 합니다.  억으로 수백만의 조직 사용자가 되며 사용자가 이미 AD tooAzure 로그인 합니다.  [Azure AD 로그인 지원 추가](active-directory-authentication-scenarios.md)에 대해 자세히 알아보세요.

**응용 프로그램 등록을 단순화합니다.**  응용 프로그램을 등록하는 동안 등록 양식을 사전에 입력하거나 완전히 제거할 수 있도록 Azure AD가 사용자에 대한 필수 정보를 보낼 수 있습니다.  소셜 미디어 및 모바일 응용 프로그램에 친숙 한 동의 환경 비슷한 toothose 통해 자신의 Azure AD 계정을 사용 하 여 응용 프로그램에 대 한 사용자가 등록할 수 있습니다.  모든 사용자는 등록 하 고 IT 담당자의 도움 없이 Azure AD와 통합 된 tooan 응용 프로그램에 로그인 수입니다.  [Azure AD 계정 로그인을 위해 응용 프로그램 등록](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)에 대해 자세히 알아보세요.

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>사용자, 사용자 프로 비전 관리 및 액세스 제어 tooYour 응용 프로그램에 대 한 찾아보기
**Hello 디렉터리의 사용자가 찾아보십시오.**  다른 사용자를 초대할 때 조직의 다른 사용자에 대 한 hello Graph API toohelp 사용자 검색 및 찾아보기 사용 또는 전자 메일 주소로 tootype 대신 액세스를 부여 합니다.  사용자는 hello 조직 계층의 hello 세부 정보 보기를 포함 하는 주소를 친숙 한 책 스타일 인터페이스를 사용 하 여 찾을 수 있습니다.  Hello에 대 한 자세한 [Graph API](active-directory-graph-api.md)합니다.

**Active Directory 그룹 및 고객이 이미 관리하는 메일 그룹을 다시 사용합니다.**  Azure AD는 hello 그룹 고객이 이미 전자 메일 배포를 위해 사용 하 여 및 액세스 관리를 포함 합니다.  Hello Graph API를 사용 하 여 다시 고객 toocreate 요구 하는 대신 이러한 그룹을 사용 하 고 별도의 응용 프로그램에 그룹 집합을 관리 합니다.  그룹 정보 또한 보낼 수 있습니다 tooyour 응용 프로그램 토큰에 서명 합니다.  Hello에 대 한 자세한 [Graph API](active-directory-graph-api.md)합니다.

**Access tooyour 응용 프로그램을 지닌 Azure AD toocontrol를 사용 합니다.**  관리자와 Azure AD에서 응용 프로그램 소유자 액세스 tooapplications toospecific 사용자 및 그룹을 할당할 수 있습니다.  Hello Graph API를 사용 하 여이 목록 및 toocontrol 프로 비전 하 고 리소스의 프로 비전 해제 하는 사용 읽고 수 응용 프로그램 내에서 액세스 합니다.

**Azure AD를 사용하여 역할 기반 액세스를 제어합니다.**  사용자 및 그룹 tooroles Azure AD에서 응용 프로그램을 등록할 때를 정의 하는 관리자와 응용 프로그램 소유자가 할당할 수 있습니다.  역할 정보 tooyour 응용 프로그램 토큰에 서명할에 보내지고 hello Graph API를 사용 하 여 읽을 수도 있습니다.  [Azure AD를 사용하여 권한 부여](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx)에 대해 자세히 알아보세요.

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Get 액세스 tooUser 프로필, 일정, 전자 메일, 연락처, 파일 등
**Azure AD는 Office 365에 대 한 권한 부여 서버 hello 및 기타 Microsoft 비즈니스 서비스는 합니다.**  로그인 tooyour 응용 프로그램 또는 현재 사용자 계정 tooAzure AD 사용자 계정을 OAuth 2.0을 사용 하 여 연결 하는 지원에 대 한 Azure AD를 지 원하는 경우에 읽기 및 쓰기 액세스 tooa 사용자의 프로필, 일정, 전자 메일, 연락처, 파일 및 기타 정보를 요청할 수 있습니다.  있습니다 수 원활 하 게 이벤트 toouser 일정을 작성 하 고 읽기 또는 쓰기 파일 tootheir OneDrive.  에 대 한 자세한 내용은 [Office 365 Api hello 액세스](https://msdn.microsoft.com/office/office365/howto/platform-development-overview)합니다.

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Hello Azure에서에서 응용 프로그램 및 Office 365 시장 승격
**이미 Azure AD를 사용 하는 조직에 응용 프로그램 toohello 수백만 승격 합니다.**  이러한 마켓플레이스를 검색하고 찾아보는 사용자는 자격 있는 클라우드 서비스 고객이 되어 이미 하나 이상의 클라우드 서비스를 사용하고 있습니다.  응용 프로그램을 승격 하는 방법에 대 한 자세한 정보 [Azure 마켓플레이스 hello](https://azure.microsoft.com/marketplace/partner-program/)합니다.

**사용자가 응용 프로그램에 등록하면 사용자의 Azure AD 액세스 패널 및 Office 365 앱 시작 관리자에 표시됩니다.**  사용자가 수 수 tooquickly 및 나중에 쉽게 반환 tooyour 응용 프로그램 사용자 참여를 향상.  Hello에 대 한 자세한 [Azure AD 액세스 패널](../active-directory-saas-access-panel-introduction.md)합니다.

### <a name="secure-device-to-service-and-service-to-service-communication"></a>장치와 서비스 및 서비스와 서비스 간의 안전한 통신
**Azure AD를 사용 하 여 서비스 및 장치 id 관리를 위한 toowrite 필요 하 고 IT toomanage 액세스할 수 있도록 hello 코드를 줄입니다.**  서비스에서 OAuth를 사용 하 여 Azure AD 토큰을 가져오기 및 장치가 이러한 토큰 tooaccess 웹 Api를 사용 합니다.  Azure AD를 사용하면 복잡한 인증 코드를 작성할 필요가 없습니다.  Hello id hello 서비스 및 장치는 Azure AD에 저장 되므로 IT 키 및 해지 하는 대신 toodo이 별도로 응용 프로그램에서 한 곳에서 관리할 수 있습니다.

## <a name="benefits-of-integration"></a>통합의 이점
Azure AD와의 통합 이점 필요 하지 않은 있습니다 toowrite 추가 코드가 포함 되어 있습니다.

### <a name="integration-with-enterprise-identity-management"></a>엔터프라이즈 ID 관리와의 통합
**응용 프로그램이 IT 정책을 준수하도록 합니다.**  조직에서는 Azure AD와의 엔터프라이즈 id 관리 시스템을 통합 사용자가 조직을 떠나면은 자동으로 손실 IT 이므로 tootake 없이 액세스 tooyour 응용 프로그램이 별도 단계입니다.  IT 응용 프로그램에 액세스 하 고 액세스 하는 정책을 복잡 한 회사 정책으로는 필요 toowrite 코드 toocomply 감소-예에서는 다단계 인증에 필요한-를 확인할 수 있는 사람을 관리할 수 있습니다.  Azure AD에서는 관리자가 되도록 로그인 되어 tooyour 응용 프로그램의 자세한 감사 로그에 제공 IT 사용을 추적할 수 있습니다.

**Azure AD 응용 프로그램은 AD와 통합할 수 있도록 Active Directory toohello 클라우드를 확장 합니다.**  대부분의 조직 hello 전 세계 해당 보안 주체 로그인 및 id 관리 시스템으로 Active Directory를 사용 하 고 AD와 응용 프로그램 toowork가 필요 합니다.  Azure AD와 통합하면 응용 프로그램이 Active Directory와 통합됩니다.

### <a name="advanced-security-features"></a>고급 보안 기능
**다단계 인증.**  Azure AD는 네이티브 다단계 인증을 제공합니다.  IT 관리자가 없는 toocode이이 지원은 사용자가 직접 있도록 multi-factor authentication tooaccess 응용 프로그램에 필요할 수 있습니다.  [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)에 대해 자세히 알아보세요.

**비정상적인 로그인 감지.**  Azure AD는 컴퓨터를 사용 하는 동안 하루 십억 이상 로그인 처리 알고리즘 toodetect 의심 스러운 활동을 학습 하 고 IT 관리자는 발생 가능한 문제에 게 알립니다.  응용 프로그램을 Azure AD 로그인을 지원 하 여이 보호의 이점을 hello 가져옵니다. [Azure Active Directory 액세스 보고서 보기](../active-directory-view-access-usage-reports.md)에 대해 자세히 알아보세요.

**조건부 액세스.**  또한 toomulti 단계 인증을 관리자가 할 수 전에 사용자가 로그인 특정 조건을 충족 tooyour 응용 프로그램입니다.  지정 된 그룹 및 액세스에 사용 되 고 hello 장치의 hello 상태에 멤버 자격, 클라이언트 장치의 hello IP 주소 범위를 포함 하는 조건을 설정할 수 있는 합니다.  [Azure Active Directory 조건부 액세스](../active-directory-conditional-access.md)에 대해 자세히 알아보세요.

### <a name="easy-development"></a>손쉬운 배포
**산업 표준 프로토콜.**  Microsoft는 커밋된 toosupporting 산업 표준입니다.  Azure AD는 hello SAML 2.0, OpenID Connect 1.0, OAuth 2.0 및 Ws-federation 1.2 인증 프로토콜을 지원합니다.  hello Graph API는 OData 4.0과 호환 됩니다.  이미 응용 프로그램을 지 원하는 경우 hello SAML 2.0 또는 OpenID Connect 1.0 프로토콜 페더레이션된 로그인에 대 한 Azure AD에 대 한 지원을 추가 하기 위한 간단한 수 있습니다.  [Azure AD 지원 인증 프로토콜](active-directory-authentication-protocols.md)에 대해 자세히 알아보세요.

**오픈 소스 라이브러리.**  Microsoft는 인기 있는 언어 및 플랫폼 toospeed 개발을 위한 완전히 지원 되는 오픈 소스 라이브러리를 제공합니다.  hello 소스 코드 Apache 2.0 라이선스 및 무료 toofork 하 고 뒤로 toohello 프로젝트에 기여 합니다.  [Azure AD 인증 라이브러리](active-directory-authentication-libraries.md)에 대해 자세히 알아보세요.

### <a name="worldwide-presence-and-high-availability"></a>전 세계 제공 및 고가용성
**Azure AD는 hello 전 세계 데이터 센터에 배포 하 고 관리 되 고 hello 클록 주위 모니터링 합니다.**  Azure AD는 Microsoft Azure 및 Office 365에 대 한 hello id 관리 시스템 이며 hello 전 세계 28 데이터 센터에 배포 됩니다.  디렉터리 데이터 복제 toobe tooat 최소 3 데이터 센터를 보장 됩니다.  전역 부하 분산 장치는 사용자가 자신의 데이터를 포함 하는 Azure AD의 hello 가장 가까운 복사본에 액세스 하 고 자동으로 다시 라우팅 요청 tooother 데이터 센터 문제가 발견 되는 경우를 확인 합니다.

## <a name="next-steps"></a>다음 단계
[코드 작성 시작하기](active-directory-developers-guide.md#get-started).

[Azure AD를 사용한 사용자 로그인](active-directory-authentication-scenarios.md)

