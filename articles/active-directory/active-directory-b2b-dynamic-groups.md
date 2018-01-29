---
title: "동적 그룹 및 Azure Active Directory B2B 공동 작업 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 기능에서 Azure AD 동적 그룹을 사용하는 방법을 보여줍니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: mtillman
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 12/14/2017
ms.author: twooley
ms.reviewer: sasubram
ms.openlocfilehash: d60b7f70332d6183a67003c1dceb96241fc6bae4
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>동적 그룹 및 Azure Active Directory B2B 공동 작업

## <a name="what-are-dynamic-groups"></a>동적 그룹이란?
Azure AD(Azure Active Directory)에 대한 보안 그룹 구성원의 동적 구성은 [Azure Portal](https://portal.azure.com)에서 사용할 수 있습니다. 관리자는 사용자 특성(예: userType, department 또는 country)에 따라 Azure AD에서 만든 그룹을 채우는 규칙을 설정할 수 있습니다. 특성에 따라 구성원을 보안 그룹에 자동으로 추가하거나 보안 그룹에서 제거할 수 있습니다. 이러한 그룹은 SharePoint 사이트, 문서 등의 응용 프로그램 또는 클라우드 리소스에 대한 액세스 권한을 제공하고 구성원에게 라이선스를 할당할 수 있습니다. [Azure Active Directory의 전용 그룹](active-directory-accessmanagement-dedicated-groups.md)에서 동적 그룹에 대해 자세히 알아보세요.

동적 그룹을 만들고 사용하려면 적절한 [Azure AD Premium P1 또는 P2 라이선스](https://azure.microsoft.com/pricing/details/active-directory/)가 필요합니다. 자세한 내용은 [Azure Active Directory에서 동적 그룹 멤버 자격에 대한 특성 기반 규칙 만들기](active-directory-groups-dynamic-membership-azure-portal.md) 문서를 참조하세요.

## <a name="what-are-the-built-in-dynamic-groups"></a>기본 제공 동적 그룹이란?
**모든 사용자** 동적 그룹을 사용하면 테넌트 관리자는 클릭 한 번으로 테넌트의 모든 사용자가 포함된 그룹을 만들 수 있습니다. 기본적으로 **모든 사용자** 그룹은 구성원 및 게스트를 비롯하여 디렉터리의 모든 사용자를 포함합니다.
새 Azure Active Directory 관리 포털 내의 그룹 설정 보기에서 **모든 사용자**를 사용하도록 설정할 수 있습니다.

![예로 설정된 모든 사용자 그룹 사용 표시](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

## <a name="hardening-the-all-users-dynamic-group"></a>모든 사용자 동적 그룹 강화
기본적으로 **모든 사용자** 그룹에는 B2B 공동 작업(게스트) 사용자도 포함됩니다. 게스트 사용자를 제거하는 규칙을 사용하여 **모든 사용자** 그룹을 추가로 보호할 수 있습니다. 다음 그림은 게스트를 제외하도록 수정된 **모든 사용자** 그룹을 보여 줍니다.

![사용자 형식이 게스트와 같지 않은 규칙 표시](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

정책(예: Azure AD 조건부 액세스 정책)을 적용할 수 있도록 게스트 사용자만 포함된 새 동적 그룹을 만드는 것이 유용할 수도 있습니다.
이러한 그룹은 다음과 같이 표시됩니다.

![사용자 형식이 게스트와 같은 규칙 표시](media/active-directory-b2b-dynamic-groups/only-guest-users.png)

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [역할에 B2B 공동 작업 사용자 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업을 위한 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
