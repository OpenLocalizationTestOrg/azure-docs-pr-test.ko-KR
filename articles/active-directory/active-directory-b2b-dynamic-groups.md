---
title: "aaaDynamic 그룹 및 Azure Active Directory B2B 공동 작업 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 기능을 Azure AD 동적 그룹에 사용할 수 있습니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>동적 그룹 및 Azure Active Directory B2B 공동 작업

## <a name="what-are-dynamic-groups"></a>동적 그룹이란?
Azure Active Directory (Azure AD)에 대 한 보안 그룹 구성원 자격의 동적 구성에서 사용할 수는 [Azure 포털 hello](https://portal.azure.com)합니다. 관리자는 Azure Active Directory에서 만든 toopopulate 그룹 사용자 특성 (예: userType, 부서 또는 국가)를 기반으로 규칙을 설정할 수 있습니다. 해당 특성을 기반으로 하는 보안 그룹에서 제거 tooor 멤버를 자동으로 추가할 수 있습니다. 이러한 그룹 액세스 tooapplications 또는 클라우드 리소스 (예: SharePoint 사이트, 문서) 제공할 수 있으며 tooassign toomembers 라이선스. [Azure Active Directory의 전용 그룹](active-directory-accessmanagement-dedicated-groups.md)에서 동적 그룹에 대해 자세히 알아보세요.

적절 한 hello [Azure AD Premium P1 또는 p 2 라이선스](https://azure.microsoft.com/pricing/details/active-directory/) 필요한 toocreate 및 사용 하 여 동적 그룹입니다. Hello 문서에서 자세한 내용을 [Azure Active Directory에 동적 그룹 멤버 자격에 대 한 특성 기반 규칙을 만드는](active-directory-groups-dynamic-membership-azure-portal.md)합니다.

## <a name="what-are-hello-built-in-dynamic-groups"></a>Hello 기본 제공 동적 그룹 이란?
hello **모든 사용자에 게** 동적 그룹을 사용 하면 테 넌 트 관리자 toocreate 단일 hello 테 넌 트의 모든 사용자가 포함 하는 그룹을 클릭 합니다. 기본적으로 hello **모든 사용자에 게** 그룹 멤버와 게스트를 포함 하 여 hello 디렉터리에 모든 사용자를 포함 합니다.
Hello 새 Azure Active Directory 관리 포털 내에서 tooenable hello를 선택할 수 있습니다 **모든 사용자에 게** 그룹에서 hello 그룹 설정을 확인 합니다.

![기본 제공 그룹](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>보안 강화 hello 모든 사용자가 동적 그룹
기본적으로 hello **모든 사용자에 게** 도 B2B 공동 작업 (게스트) 사용자 그룹에 포함 합니다. 추가로 보호할 수 있습니다 프로그램 **모든 사용자에 게** 규칙 tooremove 게스트 사용자를 사용 하 여 그룹화 합니다. hello 다음 그림과 hello **모든 사용자에 게** tooexclude guests 그룹을 수정 합니다.

![모든 사용자 그룹을 사용하도록 설정](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

찾을 수도 것 유용한 toocreate 게스트 사용자만을 포함 하는 새 동적 그룹 정책 (예: Azure AD 조건부 액세스 정책) toothem를 적용할 수 있도록 합니다.
이러한 그룹은 다음과 같이 표시됩니다.

![게스트 사용자 제외](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업을 위한 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
