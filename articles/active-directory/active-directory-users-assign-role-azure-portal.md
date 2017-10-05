---
title: "Azure Active Directory에서 관리자 역할에 사용자 할당 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 관리 정보를 변경하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a>Azure Active Directory에서 관리자 역할에 사용자 할당
이 문서는 Azure AD(Azure Active Directory)에서 사용자에게 관리 역할을 할당하는 방법을 설명합니다. 조직 내에서 새 사용자 추가에 대한 자세한 내용은 [Azure Active Directory에 새 사용자 추가](active-directory-users-create-azure-portal.md)를 참조하세요. 기본적으로 추가된 사용자에게는 관리자 권한이 없지만 언제든 역할을 할당할 수 있습니다.

## <a name="assign-a-role-to-a-user"></a>사용자에게 역할 할당
1. 디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.
2. **더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.

   ![사용자 관리 열기](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. **사용자 및 그룹** 블레이드에서 **모든 사용자**를 선택합니다.

   ![모든 사용자 블레이드 열기](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. **사용자 및 그룹 - 모든 사용자** 블레이드의 목록에서 사용자를 선택합니다.
5. 선택한 사용자에 대한 블레이드에서 **디렉터리 역할**을 선택한 다음 **디렉터리 역할** 목록의 역할에 사용자를 할당합니다. 사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.

      ![역할에 사용자 할당](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. **저장**을 선택합니다.

## <a name="next-steps"></a>다음 단계
* [사용자 추가](active-directory-users-create-azure-portal.md)
* [새 Azure 포털에서 사용자의 암호 재설정](active-directory-users-reset-password-azure-portal.md)
* [사용자의 작업 정보 변경](active-directory-users-work-info-azure-portal.md)
* [사용자 프로필 관리](active-directory-users-profile-azure-portal.md)
* [Azure AD에서 사용자 삭제](active-directory-users-delete-user-azure-portal.md)
