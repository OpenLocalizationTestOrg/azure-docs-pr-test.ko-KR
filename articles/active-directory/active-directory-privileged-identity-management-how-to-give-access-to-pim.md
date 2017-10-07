---
title: "aaaHow toogive 액세스 tooPrivileged Id 관리-Azure | Microsoft Docs"
description: "PIM을 관리할 수 있도록 Azure Active Directory Privileged Identity Management 확장와 tooadd 역할 toousers hello 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>액세스 toomanage Azure AD Privileged Identity Management를 제공합니다.
조직에 대 한 Azure AD Privileged Identity Management (PIM)를 사용 하면 자동으로 hello 전역 관리자 역할 할당을 가져오고 tooPIM에 액세스 합니다. 하지만, 기본적으로 다른 전역 관리자를 포함하여 아무도 쓰기 액세스 권한을 갖지 못합니다. 다른 전역 관리자, 보안 관리자 및 보안 판독기 읽기 전용 액세스 tooAzure AD PIM 있어야 합니다. toogive 액세스 tooPIM hello 첫 번째 사용자가 할당할 수 다른 toohello **권한 있는 역할 관리자** 역할입니다. 이 할당은 PIM 자체 내에서 수행해야 하고 PowerShell 또는 다른 포털을 통해 변경할 수 없습니다.

> [!NOTE]
> Azure AD PIM 관리에 Azure MFA가 필요합니다. Azure MFA에 대해 Microsoft 계정을 등록할 수 없기 때문에 Microsoft 계정으로 로그인하는 사용자는 Azure AD PIM에 액세스할 수 없습니다.
> 
> 

한 명의 사용자가 잠긴 경우 또는 해당 계정이 삭제된 경우 최소한 두 명의 사용자가 항상 권한 있는 역할 관리자 역할에 있어야 합니다.

## <a name="give-another-user-access-toomanage-pim"></a>다른 사용자 액세스 toomanage PIM를 제공 합니다.
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 및 선택 hello **Azure AD Privileged Identity Management** hello 대시보드에서 응용 프로그램입니다.
2. **권한 있는 역할 관리** > **권한 있는 역할 관리자** > **추가**를 선택합니다.
   
    ![권한 있는 역할 관리자 추가 - 스크린샷][1]
3. Hello 추가 관리 되는 사용자 블레이드 1 단계는 이미 완료입니다. 선택 단계 2, **사용자 선택** 검색 원하는 tooadd hello 사용자에 대 한 합니다.
   
    ![사용자 선택 - 스크린 샷][2]
4. Hello 검색 결과에서 hello 사용자를 선택 하 고 클릭 **수행**합니다.
5. 클릭 **확인** toosave 선택 합니다. hello 선택한 사용자는 권한 있는 역할 관리자 hello 목록에 표시 됩니다.
   
   * 새 역할 toosomeone에 할당 될 때마다은 자동으로 설정 됩니다 적격 tooactivate hello 역할을 합니다. Toomake 하려는 경우 hello 역할에 영구적으로 hello 목록에서 hello 사용자를 클릭 합니다. 선택 **권한 확인** hello 사용자 정보 메뉴에 있습니다.
6. 너무 hello 사용자에 게 링크 보내기[Azure AD Privileged Identity Management 시작](active-directory-privileged-identity-management-getting-started.md)합니다.

## <a name="remove-another-users-access-rights-for-managing-pim"></a>PIM 관리에 대한 다른 사용자의 액세스 권한 제거
Hello, 관리자 역할 권한 있는 역할에서에서 사용자를 제거 하기 전에 항상 수 있으며 이러한 할당 tooit 두 명의 사용자가 선택 되어 있는지 확인 합니다.

1. Hello PIM 대시보드에 hello 역할 클릭 **권한 있는 역할 관리자**합니다.  해당 역할에 있는 현재 사용자의 hello 목록이 표시 됩니다.
2. Hello hello 사용자 목록에는 사용자를 클릭 합니다.
3. **제거**를 클릭합니다.  확인 메시지가 나타납니다.
4. 클릭 **예** hello 역할에서 tooremove hello 사용자입니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
