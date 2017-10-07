---
title: "Azure Active Directory의 사용자에 대 한 그룹 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure Active Directory에서 그룹 구성원 toohello 그룹 추가"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Azure Active Directory에서 그룹 만들기 및 멤버 추가
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Azure 클래식 포털](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

이 문서에서는 설명 어떻게 toocreate Azure Active Directory에 새 그룹을 채웁니다. 할당 하는 등 라이선스 또는 권한을 사용자 또는 장치 tooa 수가 한 번에 그룹 tooperform 관리 작업을 사용 합니다.

## <a name="how-do-i-create-a-group"></a>그룹을 만드는 방법
1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.

   ![사용자 관리 열기](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. Hello에 **사용자 및 그룹** 블레이드를 **모든 그룹**합니다.

   ![Hello 그룹 블레이드 열기](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. Hello에 **사용자 및 그룹-모든 그룹** 블레이드, 선택 hello **추가** 명령입니다.

   ![Hello 추가 명령을 선택 하면](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. Hello에 **그룹** 블레이드에서 이름과 hello 그룹에 대 한 설명을 추가 합니다.
6. tooselect 멤버 tooadd toohello 그룹에서 **Assigned** hello에 **멤버 자격 유형** 상자를 선택한 후 **멤버**합니다. 어떻게 toomanage hello 그룹의 구성원이 동적으로 하는 방법에 대 한 자세한 내용은 참조 [toocreate 특성을 사용 하 여 고급 규칙 그룹 멤버 자격에 대 한](active-directory-groups-dynamic-membership-azure-portal.md)합니다.

   ![멤버 tooadd 선택](./media/active-directory-groups-create-azure-portal/select-members.png)
7. Hello에 **멤버** 블레이드, 하나를 선택 하거나 더 많은 사용자 또는 장치 tooadd toohello 그룹 및 선택 hello **선택** 단추 hello 블레이드 tooadd hello 맨 아래에 해당 toohello 그룹입니다. hello **사용자** 상자 필터 hello 일치 항목 tooany 부분은 사용자 또는 장치 이름 기준으로 표시 합니다. 와일드카드 문자는 해당 상자에서 허용되지 않습니다.
8. 멤버 toohello 그룹 추가 마치면 선택 **만들기** hello에 **그룹** 블레이드입니다.    

   ![그룹 확인 만들기](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>다음 단계
이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.

* [기존 그룹 보기](active-directory-groups-view-azure-portal.md)
* [그룹의 설정 관리](active-directory-groups-settings-azure-portal.md)
* [그룹의 멤버 관리](active-directory-groups-members-azure-portal.md)
* [그룹의 멤버 자격 관리](active-directory-groups-membership-azure-portal.md)
* [그룹의 사용자에 대한 동적 규칙 관리](active-directory-groups-dynamic-membership-azure-portal.md)
