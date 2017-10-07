---
title: "aaaOffice 365 외부 공유 및 Azure Active Directory B2B 공동 작업 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에 대한 클레임 매핑 참조"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Office 365 외부 공유 및 Azure Active Directory B2B 공동 작업

Office 365 (OneDrive, SharePoint Online, 그룹 통합, 등) 및 Azure Active Directory (Azure AD) B2B 공동 작업은 기술적으로 공유 하 고 외부 hello 동일한 것입니다. 이미 hello Azure AD B2B 공동 작업 초대 Api를 사용 하 여 공유 하는 데을 Office 365 그룹에 게스트를 비롯 한 모든 외부 공유 (OneDrive/SharePoint Online) 제외 합니다.

OneDrive/SharePoint Online에는 별도 초대 관리자가 있습니다. OneDrive/SharePoint Online의 외부 공유 지원은 Azure AD에서 지원을 개발하기 전에 시작되었습니다. 시간이 지남에 따라 몇 가지 기능을 계산에 OneDrive/SharePoint Online 외부 공유 하 고 수백만 hello 제품을 사용 하는 사용자의 기본 제공 패턴을 공유 합니다. 그렇지만 OneDrive/SharePoint Online 외부 공유의 작동 방식과 Azure AD B2B 공동 작업의 작동 방식 간에 미묘한 차이가 있습니다.

- OneDrive/SharePoint Online 사용자 toohello 디렉터리 사용자가 초대를 회수 된 후 추가 합니다. 따라서 상환 하기 전에 hello 사용자 Azure AD 포털에 표시 되지 않으면 합니다. 다른 사이트, 그 동안 hello의 사용자 초대 합니다. 새 초대 생성 됩니다. 그러나 Azure AD B2B 공동 작업을 사용하면 초대와 동시에 사용자가 추가되므로 모든 위치에 사용자가 표시됩니다.

- hello 상환 경험 OneDrive/SharePoint Online에서 Azure AD B2B 공동 작업에서 환경을 hello 다르게 보입니다. 사용자 초대 교환, 후 hello 경험 동일 합니다.

- Azure AD B2B 공동 작업의 초대된 사용자는 OneDrive/SharePoint Online 공유 대화 상자에서 선택할 수 있습니다. OneDrive/SharePoint Online의 초대된 사용자는 초대를 상환한 후 Azure AD에도 표시됩니다.

- 외부 toomanage 외부 너무 설정 공유 hello OneDrive/SharePoint Online을 설정 OneDrive/SharePoint Online에서 Azure AD B2B 공동 작업와 공유**만 hello 디렉터리에 이미 외부 사용자와 공유할 수 있도록**합니다. 사용자가 공유 tooexternally 사이트 이동 수 및 hello 관리 하는 외부 공동 작업자에서 선택이 추가 합니다. admin 님 안녕하세요 hello hello B2B 공동 작업 초대 Api 통해 외부 공동 작업자를 추가할 수 있습니다.

![hello OneDrive/SharePoint Online 외부 공유 설정](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [B2B 공동 작업 초대 위임](active-directory-b2b-delegate-invitations.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업을 위한 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
