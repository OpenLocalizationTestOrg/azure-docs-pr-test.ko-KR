---
title: "Azure Active Directory에서 그룹에 대 한 aaaManage hello 멤버 | Microsoft Docs"
description: "어떻게 tooadd 또는 Azure Active Directory 그룹에서 사용자 및 장치 제거"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Azure Active Directory 테넌트의 사용자에 대한 그룹 멤버 자격 관리
이 문서에서는 toomanage Azure Active Directory (Azure AD)의 그룹에 대 한 멤버를 hello 하는 방법을 설명 합니다.

## <a name="how-do-i-find-hello-members-and-manage-them"></a>어떻게 hello 멤버를 찾을 하 고 관리 하 시겠습니까?
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.

   ![사용자 관리 열기](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. Hello에 **사용자 및 그룹** 블레이드를 **모든 그룹**합니다.

   ![Hello 그룹 블레이드 열기](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. Hello에 **사용자 및 그룹-모든 그룹** 블레이드에서 그룹을 선택 합니다.
5. Hello에 **그룹- *groupname* ** 블레이드를 **멤버**합니다.

   ![Hello 멤버 블레이드 열기](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. hello, tooadd 멤버 toohello 그룹 **그룹-멤버** 블레이드를 **구성원 추가**합니다.

   ![멤버 추가 명령](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. Hello에 **멤버** 블레이드, 하나를 선택 하거나 더 많은 사용자 또는 장치 tooadd toohello 그룹 및 선택 hello **선택** 단추 hello 블레이드 tooadd hello 맨 아래에 해당 toohello 그룹입니다. hello **사용자** 상자 필터 hello 일치 항목 tooany 부분은 사용자 또는 장치 이름 기준으로 표시 합니다. 와일드카드 문자는 해당 상자에서 허용되지 않습니다.
8. hello에 hello 그룹에서 멤버 tooremove **그룹-멤버** 블레이드, 구성원을 선택 합니다.
9. Hello에 ***membername*** 블레이드, 선택 hello **제거** 명령을 실행 하 고 hello 프롬프트에서 선택한 내용을 확인 합니다.

   ![멤버 제거 명령](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. 작업을 마치면 hello 그룹에 대 한 구성원 변경 선택 **저장**합니다.

## <a name="additional-information"></a>추가 정보
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [기존 그룹 보기](active-directory-groups-view-azure-portal.md)
* [새 그룹을 만들고 멤버 추가](active-directory-groups-create-azure-portal.md)
* [그룹의 설정 관리](active-directory-groups-settings-azure-portal.md)
* [그룹의 멤버 자격 관리](active-directory-groups-membership-azure-portal.md)
* [그룹의 사용자에 대한 동적 규칙 관리](active-directory-groups-dynamic-membership-azure-portal.md)
