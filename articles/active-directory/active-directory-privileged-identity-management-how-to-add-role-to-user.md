---
title: "aaaHow tooadd 사용자 역할을 제거 하거나 | Microsoft Docs"
description: "Tooadd 역할 tooprivileged id를 Azure Active Directory Privileged Identity Management 응용 프로그램을 hello 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: 어떻게 tooadd 또는 사용자 역할 제거
와 Azure AD (Active Directory), 전역 관리자 (또는 회사 관리자)를 업데이트할 수 있는 사용자가 **영구적으로** tooroles Azure AD에 할당 합니다. 이 작업은 `Add-MsolRoleMember` 및 `Remove-MsolRoleMember` 등 PowerShell cmdlet을 사용하여 완료됩니다. 에 설명 된 대로 hello Azure 클래식 포털을 사용할 수 있습니다 또는 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)합니다.

권한 있는 역할 관리자 toomake 영구 역할 할당도 사용 하는 hello Azure AD Privileged Identity Management 응용 프로그램. 또한 권한이 있는 역할 관리자는 사용자의 관리자 역할을 **적격**으로 만들 수 있습니다. 소요 되 고 작업이 완료 되 면이 해당 사용 권한을 만료 되는 다음 적격 관리자 hello 역할을 활성화할 수 있습니다.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>PIM으로 hello Azure 포털에서에서 역할 관리
조직에서 Azure AD를 Office 365, 및 기타 Microsoft 서비스 및 응용 프로그램에서 사용자에 toodifferent 관리 역할 할당 수입니다.  사용 가능한 역할 hello에 대 한 자세한 내용은에서 확인할 수 있습니다 [Azure AD PIM의 역할](active-directory-privileged-identity-management-roles.md)합니다.

hello PIM 대시보드 tooadd / Privileged Identity Management를 사용 하 여 역할의 사용자 제거를 여십시오. Hello 두 번 클릭 한 다음 **관리자 역할의 사용자가** 단추 또는 hello 역할 테이블에서 특정 역할 (예: 전역 관리자)를 선택 합니다.

> [!NOTE]
> PIM hello Azure 포털에서에서를 아직 활성화 하지 않은, 이동 너무[Azure AD PIM 시작](active-directory-privileged-identity-management-getting-started.md) 대 한 자세한 내용은 합니다.

Toogive PIM hello 사용자 toohave는에서 더 자세히 설명 해야 하는 hello 역할 자체를 다른 사용자 액세스 tooPIM를 원하는 경우 [toogive tooPIM를 액세스 하는 방법을](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)합니다.

## <a name="add-a-user-tooa-role"></a>사용자 tooa 역할 추가
1. Hello에 [Azure 포털](https://portal.azure.com/)선택, hello **Azure AD Privileged Identity Management** hello 대시보드에서 타일을 합니다.
2. **권한 있는 역할 관리**를 선택합니다.
3. Hello에 **역할 요약** 테이블, toomanage 선택 hello 역할입니다.
4. Hello 역할 블레이드 선택 **추가**합니다.
5. 클릭 **사용자 선택** hello 사용자 hello에 대 한 검색 **사용자 선택** 블레이드입니다.  
6. Hello 검색 결과 목록에서 hello 사용자를 선택 하 고 클릭 **수행**합니다.
7. 클릭 **확인** toosave 선택 합니다. 선택한 hello 사용자 hello 역할에 대해 적합으로 hello 목록에 표시 됩니다.

> [!NOTE]
> 새 사용자 역할에는 기본적으로 hello 역할 수 만입니다. Toomake hello 역할을 영구적으로 적용 하려는 경우 hello 목록에서 hello 사용자를 클릭 합니다. hello 사용자의 정보는 새 블레이드가에 표시 됩니다. 선택 **만들기 권한** hello 사용자 정보 메뉴에 있습니다.  
> 사용자에 대 한 Azure Multi-factor Authentication (MFA)를 등록할 수 없습니다 또는 Microsoft 계정을 사용 하는 경우 (일반적으로 @outlook.com), toomake 해야 자신의 모든 역할에 영구적으로 합니다. 적격 관리자는 활성화 하는 동안 tooregister MFA에 대 한 요청 됩니다.

이제을 hello 사용자 역할에 대 한 적격, 알 수 있도록 것의 toohello 지침에 따라 활성화할 수 있습니다 [어떻게 tooactivate는 역할을 하거나 비활성화](active-directory-privileged-identity-management-how-to-activate-role.md)합니다.

## <a name="remove-a-user-from-a-role"></a>역할에서 사용자 제거
적격 역할 할당에서 사용자를 제거할 수 있지만 영구 전역 관리자인 사용자가 최소 한 명은 항상 있어야 합니다.

이러한 단계 tooremove 특정 사용자 역할에서 수행 합니다.

1. Hello Azure AD PIM 대시보드 역할을 선택 하 여 또는 hello를 클릭 하 여 hello 역할 목록에서 toohello 역할 이동 **관리자 역할의 사용자가** 단추입니다.
2. Hello hello 사용자 목록에는 사용자를 클릭 합니다.
3. **제거**를 클릭합니다. 메시지 tooconfirm를 요청 합니다.
4. 클릭 **예** hello 사용자 로부터 tooremove hello 역할입니다.

어떤 사용자가 자신의 역할 할당을 여전히 필요 확실 하지 않은 경우 할 수 있습니다 [hello 역할에 대 한 액세스 검토는 시작](active-directory-privileged-identity-management-how-to-start-security-review.md)합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

