---
title: "Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 사용자 또는 그룹 할당 aaaRemove | Microsoft Docs"
description: "Tooremove hello Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 사용자 또는 그룹의 할당에 액세스 하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Azure Active Directory에서 엔터프라이즈 앱의 사용자 또는 그룹 할당 제거
쉽게 tooremove 사용자 또는 그룹 액세스 tooone Azure Active Directory (Azure AD)에 엔터프라이즈 응용 프로그램의 할당 되지 않습니다. Hello 디렉터리에 대 한 전역 관리자 여야 하며 hello 적절 한 사용 권한을 toomanage hello 엔터프라이즈 앱 있어야 합니다.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>사용자 또는 그룹 할당을 제거하려면 어떻게 해야 합니까?
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **Azure Active Directory** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.
3. Hello에 **Azure Active Directory- *디렉터리 이름***  블레이드 (관리 하는 hello 디렉터리에 대 한 즉, Azure AD hello 블레이드) 선택 **엔터프라이즈 응용 프로그램**합니다.

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. Hello에 **엔터프라이즈 응용 프로그램** 블레이드를 **모든 응용 프로그램**합니다. 관리할 수는 hello 앱 목록이 표시 됩니다.
5. Hello에 **엔터프라이즈 응용 프로그램-모든 응용 프로그램** 블레이드에서 응용 프로그램을 선택 합니다.
6. Hello에 ***appname*** 블레이드 (hello hello 제목에 선택 된 응용 프로그램의 hello 이름으로, 즉 hello 블레이드) 선택 **사용자 및 그룹**합니다.

    ![사용자 또는 그룹 선택](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. Hello에 ***appname*** **-사용자 및 그룹 할당** 블레이드에서 이상의 사용자 또는 그룹 중 하나를 선택 하 고 다음 hello를 선택 **제거** 명령입니다. Hello 프롬프트에 대 한 의사 결정을 확인 합니다.

    ![Hello 제거 명령을 선택 하면](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>다음 단계
* [내 그룹 모두 보기](active-directory-groups-view-azure-portal.md)
* [사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](active-directory-coreapps-assign-user-azure-portal.md)
* [엔터프라이즈 앱에 대한 사용자 로그인 비활성화](active-directory-coreapps-disable-app-azure-portal.md)
* [Hello 이름 변경 또는 엔터프라이즈 응용 프로그램에서의 로고](active-directory-coreapps-change-app-logo-user-azure-portal.md)
