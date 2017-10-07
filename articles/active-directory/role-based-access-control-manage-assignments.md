---
title: "Azure 리소스 액세스 할당 aaaView | Microsoft Docs"
description: "보기 및 모든 사용자 또는 그룹이 hello Azure 포털에 대 한 모든 hello 역할 기반 액세스 제어 할당 관리"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Hello Azure 포털에서에서 사용자 및 그룹에 대 한 보기 액세스 할당
> [!div class="op_single_selector"]
> * [사용자 또는 그룹에 따른 액세스 관리](role-based-access-control-manage-assignments.md)
> * [리소스에 따른 액세스 관리](role-based-access-control-configure.md)

Hello Azure Active Directory (Azure AD)의 역할 기반 액세스 제어 (RBAC)를 사용 하면 Azure 액세스 tooyour을 관리할 수 있습니다 리소스입니다. 

RBAC를 사용 하 여 할당할 액세스 세분화 된 이므로 두 가지 방법으로 hello 권한을 제한할 수 있습니다.

* **범위 지정:** RBAC 역할 할당은 범위가 지정 된 tooa 특정 구독, 리소스 그룹 또는 리소스입니다. 사용자 액세스 tooa 단일 리소스를 부여 hello의 다른 리소스에 액세스할 수 없습니다 동일한 구독 합니다.
* **역할:** 액세스 좁혀 hello hello 할당의 범위 내에서 역할을 할당 하 여 합니다. 역할은 소유자와 같이 높은 수준일 수도 있고 가상 컴퓨터 판독기와 같이 특정될 수도 있습니다.

만 역할 hello 구독, 리소스 그룹 또는 hello 할당에 대 한 hello 범위 리소스 내에서 할당할 수 있습니다. 하지만 지정 된 사용자나 그룹에 대 한 모든 hello 액세스 할당을 한 곳에서 볼 수 있습니다. 각 구독에 역할 할당 too2000 만들 수 있습니다. 

방법에 대 한 자세한 정보를 너무 가져오기[역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](role-based-access-control-configure.md)합니다.

## <a name="view-access-assignments"></a>액세스 권한 할당 보기
toolook 단일 사용자 또는 그룹에 대 한 액세스 할당 hello Azure Active Directory에서에서 시작 hello [Azure 포털](http://portal.azure.com)합니다.

1. **Azure Active Directory**를 선택합니다. 이 옵션을 탐색 목록에 표시 하는 경우 선택 **더 서비스** toofind 아래로 스크롤한 및 **Azure Active Directory**합니다.
2. **사용자 및 그룹** 및 **모든 사용자** 또는 **모든 그룹**을 차례로 선택합니다. 이 예제에서는 개별 사용자에게 집중합니다.
    ![Azure Active Directory에서 사용자 및 그룹 관리 - 스크린샷](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Hello 사용자 이름이 나 사용자 이름으로 검색 합니다.
4. 선택 **Azure 리소스** hello 사용자 블레이드의 합니다. 해당 사용자에 대 한 모든 hello 액세스 할당 표시 됩니다.

### <a name="read-permissions-tooview-assignments"></a>읽기 권한이 tooview 할당
만이 페이지 권한 tooread 있다고 hello 액세스 할당이 표시 됩니다. 예를 들어 읽기 액세스 toosubscription A 있고 toohello Azure 리소스 블레이드 toocheck 사용자의 지정을 이동 합니다. 구독 A에 대한 액세스 권한 할당을 확인할 수 있지만 구독 B에 대한 액세스 권한 할당이 있는지 표시되지 않습니다.

## <a name="delete-access-assignments"></a>액세스 권한 할당 삭제
이 블레이드에서 tooa 사용자 또는 그룹에 직접 할당 된 액세스 할당을 삭제할 수 있습니다. Hello 액세스 할당을 부모 그룹에서 상속 된 경우 toogo toohello 리소스 또는 구독 필요 하 고 관리 hello 할당 있습니다.

1. 사용자 또는 그룹에 대 한 모든 hello 액세스 할당의 hello 목록에서 원하는 toodelete hello 하나를 선택 합니다.
2. 선택 **제거** 차례로 **예** tooconfirm 합니다.
    ![액세스 권한 할당 제거 - 스크린샷](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>다음 단계

* 역할 기반 액세스 제어 너무 시작[역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](role-based-access-control-configure.md)
* Hello 참조 [RBAC 기본 제공 역할](role-based-access-built-in-roles.md)

