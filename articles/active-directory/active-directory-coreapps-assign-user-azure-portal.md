---
title: "Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 aaaAssign | Microsoft Docs"
description: "어떻게 엔터프라이즈 앱 tooassign Azure Active Directory에서 사용자 또는 그룹 tooit tooselect"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당
인지 쉽게 tooassign 사용자는 Azure Active Directory (Azure AD)의 그룹 tooyour 엔터프라이즈 응용 프로그램입니다. Hello 디렉터리에 대 한 전역 관리자 여야 하며 hello 적절 한 사용 권한을 toomanage hello 엔터프라이즈 앱 있어야 합니다.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>사용자 액세스 tooan 엔터프라이즈 응용 프로그램을 할당 하려면 어떻게 해야 합니까?
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**hello 텍스트 상자에 Azure Active Directory를 입력 한 다음 선택, **Enter**합니다.
3. Hello에 **Azure Active Directory- *디렉터리 이름***  블레이드 (관리 하는 hello 디렉터리에 대 한 즉, Azure AD hello 블레이드) 선택 **엔터프라이즈 응용 프로그램**합니다.

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. Hello에 **엔터프라이즈 응용 프로그램** 블레이드를 **모든 응용 프로그램**합니다. 관리할 수는 hello 앱 목록이 표시 됩니다.
5. Hello에 **엔터프라이즈 응용 프로그램-모든 응용 프로그램** 블레이드에서 응용 프로그램을 선택 합니다.
6. Hello에 ***appname*** 블레이드 (hello hello 제목에 선택 된 응용 프로그램의 hello 이름으로, 즉 hello 블레이드) 선택 **사용자 및 그룹**합니다.

    ![모든 응용 프로그램 명령 hello 선택](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. Hello에 ***appname*** **-사용자 및 그룹 할당** 블레이드, 선택 hello **추가** 명령입니다.
8. Hello에 **할당 추가** 블레이드를 **사용자 및 그룹**합니다.

    ![사용자 또는 그룹 toohello 응용 프로그램 할당](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. Hello에 **사용자 및 그룹** 블레이드, 선택 하나 이상의 사용자 또는 그룹 hello에서 나열 하 고 다음 hello 선택 **선택** hello hello 블레이드 맨 아래에 단추입니다.
10. Hello에 **할당 추가** 블레이드를 **역할**합니다. 그런 다음 hello **역할 선택** 블레이드에서 선택한 역할 tooapply toohello 사용자 또는 그룹을 선택한 다음 선택 hello **확인** hello hello 블레이드 맨 아래에 단추입니다.
11. Hello에 **할당 추가** 블레이드, 선택 hello **할당** hello hello 블레이드 맨 아래에 단추입니다. hello 할당 사용자 또는 그룹에는이 엔터프라이즈 응용 프로그램에 대 한 hello 선택한 역할에 의해 정의 하는 hello 사용 권한을 갖습니다.

## <a name="next-steps"></a>다음 단계
* [내 그룹 모두 보기](active-directory-groups-view-azure-portal.md)
* [엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거](active-directory-coreapps-remove-assignment-azure-portal.md)
* [엔터프라이즈 앱에 대한 사용자 로그인 비활성화](active-directory-coreapps-disable-app-azure-portal.md)
* [Hello 이름 변경 또는 엔터프라이즈 응용 프로그램에서의 로고](active-directory-coreapps-change-app-logo-user-azure-portal.md)
