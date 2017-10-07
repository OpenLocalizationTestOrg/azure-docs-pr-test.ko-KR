---
title: "Azure AD에서 권한 있는 액세스 aaaSecuring | Microsoft Docs"
description: "Hello를 설명 하는 항목에서는 Azure, Azure Active Directory와 Microsoft 온라인 서비스에서 권한 있는 액세스를 보호 하기 위한 취급 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Azure AD에서 권한 있는 액세스 보안
권한 있는 액세스 보안이 중요 한 첫 번째 단계 toohelp 최신 조직에서 비즈니스 자산을 보호 합니다. 권한 있는 계정은 IT 시스템을 운영하고 관리하는 계정입니다. 사이버 공격자가 이러한 계정 toogain 액세스 tooan 조직 데이터와 시스템 대상합니다. toosecure 특권 수준의 액세스, hello 계정 격리 해야 및 hello 위험은에서 시스템 tooa 악의적인 사용자가을 노출 합니다.

더 많은 사용자는 클라우드 서비스를 통해 tooget 권한 있는 액세스를 시작 했습니다. 여기에는 Office365의 전역 관리자, Azure 구독 관리자 및 SaaS 앱 또는 VM에서 관리 액세스 권한이 있는 사용자가 포함됩니다.

[권한 있는 액세스 보안](https://technet.microsoft.com/library/mt631194.aspx)에서 이 로드맵을 수행하는 것이 좋습니다.

Azure Active Directory, Office 365 또는 다른 Microsoft 서비스 및 응용 프로그램을 사용하는 고객의 경우 이러한 원칙은 Active Directory 또는 Azure Active Directory에서 사용자 계정을 관리하고 인증하는지 여부에 관계없이 적용됩니다. hello 다음 섹션에서는 대 한 자세한 내용은 Azure AD 기능 toosupport 권한 있는 액세스를 보호 합니다.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
관리자 인증 tooincrease hello 보안, 권한 부여 하기 전에 2 단계 인증을 해야 합니다. 2 단계 인증은 되었음을 확인 하는 방법을 보다 더 사용자 이름 및 암호를 hello 사용 해야 합니다. 보안 toouser 로그인 및 트랜잭션에 두 번째 계층을 제공합니다.

Azure Multi-factor Authentication (MFA)는 Microsoft의 2 단계 확인 솔루션는 데 도움이 되는 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 액세스 toodata 및 응용 프로그램 보호 합니다. 다음과 같이 다양하고 손쉬운 인증 옵션을 통해 강력한 인증을 제공합니다.

- 전화 통화
- 문자 메시지
- 모바일 앱 알림
- 모바일 앱 확인 코드
- 타사 OATH 토큰

Azure Multi-factor Authentication의 작동 방식에 대 한 개요 비디오를 따라 hello 참조:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

자세한 내용은 [Office 365용 MFA 및 Azure용 MFA](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)(영문)를 참조하세요.

## <a name="time-bound-privileges"></a>시간 제한 권한
일부 조직에서는 높은 권한이 있는 역할의 사용자가 너무 많은 것을 볼 수 있습니다. 사용자 추가 되었을 toosign는 서비스와 같은 특정 작업에 대 한 toohello 역할 있지만 해당 권한을 나중에 자주 사용 하지 않았습니다.

권한 toolower hello 노출 시간 제한 사용자 tooonly "just in time"의 권한 맡 사용에 대 한 가시성을 증가 하 고 JIT (), tooperform 작업 해야 할 때입니다. Azure Active Directory 및 Microsoft Online Services에서 [Azure AD PIM(Privileged Identity Management)](http://aka.ms/AzurePIM)을 사용할 수 있습니다.

![PIM 대시보드][2]

## <a name="attack-detection"></a>공격 탐지
[Azure Active Directory ID 보호](../active-directory-identityprotection.md)는 조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공합니다. 위험 이벤트에 따라, Identity Protection을 각 사용자에 대 한 사용자 위험 수준을 계산, tooconfigure 위험 기반 정책 tooautomatically 보호 hello 수 있게 해 주는 조직의 id입니다. Azure Active Directory 및 EMS에서 제공 하는 다른 조건부 액세스 제어와 함께 이러한 정책에 자동으로 hello 사용자를 차단 하거나 암호 재설정 및 다단계 인증 적용을 포함 하는 제안 수 있습니다.

![Azure AD ID 보호][3]

## <a name="conditional-access"></a>조건부 액세스
조건부 액세스 제어를 통해 Azure Active Directory tooan 응용 프로그램 액세스를 허용 하기 전에 사용자를 인증할 때 선택 하는 hello 특정 상태를 확인 합니다. 이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다.

![MFA를 사용하는 조건부 액세스 규칙 설정][4]

## <a name="related-articles"></a>관련된 문서
* [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md) 사용
* [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md) 사용
* [Azure AD ID 보호](../active-directory-identityprotection.md) 사용
* [조건부 액세스 제어](../active-directory-conditional-access.md) 사용

완벽 한 보안 로드맵 구축에 대 한 자세한 내용은 hello의 hello "고객의 책임 및 로드맵" 섹션을 참조 [Enterprise 설계자를 위해 Microsoft 클라우드 보안](http://aka.ms/securecustomer) 문서. 이 항목의 모든 Microsoft 서비스 tooassist 참여에 대 한 자세한 내용은 Microsoft 담당자에 게 문의 하거나 방문 우리의 [사이버 안보 솔루션 페이지](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)합니다.

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
