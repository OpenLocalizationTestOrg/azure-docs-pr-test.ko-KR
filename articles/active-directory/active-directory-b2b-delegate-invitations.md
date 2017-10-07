---
title: "Azure Active Directory B2B 공동 작업에 대 한 aaaDelegate 초대장 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 사용자 속성은 구성 가능합니다."
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Azure Active Directory B2B 공동 작업에 대한 초대 위임

Azure Active Directory (Azure AD) 기업 B2B 공동 작업와 없는 toobe 전역 관리자 toosend 초대 합니다. 대신, 정책을 사용 하 고 초대 toousers toosend 초대 허용 해당 역할을 위임할 수 있습니다. 중요 한 새로운 방식으로 toodelegate 게스트 사용자 초대 hello 게스트 초대자 역할을 통해 이루어집니다.

## <a name="guest-inviter-role"></a>게스트 초대자 역할
Hello 사용자 tooGuest 초대자 역할 toosend 초대 할당할 수 있습니다. Hello 전역 관리자 역할 toosend 초대 toobe 소속이 필요는 없습니다. 기본적으로 일반 사용자 전역 관리자에 대 한 일반 사용자가 초대장을 해제 하지 않는 한 hello 초대 API를 호출할 수도 있습니다. 사용자는 hello Azure 포털 또는 PowerShell을 사용 하 여 hello API를 호출할 수도 있습니다.

다음은 예제를 보여 주는 방법을 toouse PowerShell tooadd 사용자 toohello 게스트 초대자 역할:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>초대할 수 있는 사용자 제어

![제어 방법을 tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Azure AD B2B 공동 작업와 테 넌 트 관리자는 다음 초대 정책 hello를 설정할 수 있습니다.

- 초대 해제
- 관리자 및 hello 게스트 초대자 역할의 사용자를 초대할 수 있습니다.
- Admins, hello 게스트 초대자 역할 및 멤버 초대할 수 있습니다.
- 게스트를 포함한 모든 사용자가 초대를 수행할 수 있습니다.

기본적으로 테 넌 트 설정 된 너무 #4입니다. (게스트를 포함한 모든 사용자가 B2B 사용자를 초대할 수 있습니다.)

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B 공동 작업 사용자 속성](active-directory-b2b-user-properties.md)
* [B2B 공동 작업 사용자 tooa 역할 추가](active-directory-b2b-add-guest-to-role.md)
* [동적 그룹 및 B2B 공동 작업](active-directory-b2b-dynamic-groups.md)
* [B2B 공동 작업 코드 및 PowerShell 샘플](active-directory-b2b-code-samples.md)
* [B2B 공동 작업을 위한 SaaS 앱 구성](active-directory-b2b-configure-saas-apps.md)
* [B2B 공동 작업 사용자 토큰](active-directory-b2b-user-token.md)
* [B2B 공동 작업 사용자 클레임 매핑](active-directory-b2b-claims-mapping.md)
* [Office 365 외부 공유](active-directory-b2b-o365-external-user.md)
* [B2B 공동 작업 현재 제한](active-directory-b2b-current-limitations.md)
