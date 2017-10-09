---
title: "aaaShare Azure RBAC를 사용 하 여 포털 대시보드 | Microsoft Docs"
description: "이 문서에서 대시보드는 tooshare 역할 기반 액세스 제어를 사용 하 여 Azure 포털을 hello 하는 방법을 설명 합니다."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>역할 기반 액세스 제어를 사용하여 Azure 대시보드 공유
대시보드를 구성한 후에는 이를 게시하고 조직 내의 다른 사용자와 공유할 수 있습니다. 다른 사용자가 허용 tooview Azure를 사용 하 여 대시보드 [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다. 사용자 또는 그룹 사용자 tooa 역할을 할당 하 고 해당 역할을 해당 사용자가 확인 하거나 hello 게시 된 대시보드를 수정할 수 있는지 여부를 정의 합니다. 

모든 게시된 대시보드는 Azure 리소스로 구현됩니다. 따라서 구독 내에서 관리 가능한 항목으로 존재하며 리소스 그룹에 포함됩니다.  액세스 제어 관점에서 대시보드는 가상 컴퓨터 또는 저장소 계정과 같은 다른 리소스와 차이가 없습니다.

> [!TIP]
> Hello 대시보드에서 각 타일에 표시 하는 hello 리소스에 따라 자신의 액세스 제어 요구 사항을 적용 합니다.  따라서 각 타일에 hello 데이터 보호를 유지 하는 동안 광범위 하 게 공유 하는 대시보드를 디자인할 수 있습니다.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>대시보드에 대한 액세스 제어 이해
와 역할 기반 액세스 제어 (RBAC), 세 가지 서로 다른 수준의 범위에서 사용자가 tooroles를 할당할 수 있습니다.

* subscription
* 리소스 그룹
* resource

hello 사용 권한은 할당 하면 toohello 리소스를 구독에서 상속 됩니다. hello 게시 된 대시보드는 리소스입니다. 따라서 hello 게시 된 대시보드 대해서도 작동 하는 hello 구독에 대 한 할당 된 사용자 tooroles 이미 있을 수도 있습니다. 

다음은 예제입니다.  Azure 구독이 있어야 하 고 팀의 다양 한 멤버의 hello 역할 할당 된 가정해 **소유자**, **참가자**, 또는 **판독기** hello 구독에 대 한 합니다. 소유자 또는 참가자 인 사용자는 수 toolist, 보기, 만들기, 수정 또는 hello 구독 내에서 대시보드를 삭제 합니다.  판독기 인 사용자 수 toolist 및 view 대시보드는 있지만 수정 또는 삭제할 수 없습니다.  판독기 액세스 권한이 있는 사용자는 수 toomake 로컬 편집 내용을 tooa 게시 된 대시보드 (와 같은 문제를 해결 하는 경우), 않는 toopublish 수 없습니다. 이러한 변경 내용을 다시 toohello 서버입니다.  갖게 됩니다 hello 옵션 toomake hello 대시보드의 전용 복사본을 자신에 대 한

그러나 몇 가지 대시보드 또는 tooan 개별 대시보드를 포함 하는 권한을 toohello 리소스 그룹을 할당할 수 있습니다. 예를 들어는 사용자 그룹의 제한 되어야 합니다. 사용 권한을 hello 구독 하지만 큰 액세스 tooa 특정 대시보드에서 결정할 수 있습니다. 해당 대시보드에 대 한 해당 사용자가 tooa 역할을 할당 합니다. 

## <a name="publish-dashboard"></a>대시보드 게시
구독에 사용자의 그룹으로 tooshare를 원하는 대시보드 구성을 완료 한 경우를 생각해 보십시오. 다음 hello 단계 라는 저장소 관리자, 사용자 지정 된 그룹을 표시 하지만 원하는 대로 지정할 그룹 이름을 지정할 수 있습니다. Active Directory 그룹을 만들고 사용자 toothat 그룹을 추가 하는 방법에 대 한 정보를 참조 하십시오. [Azure Active Directory에서 그룹 관리](../active-directory/active-directory-accessmanagement-manage-groups.md)합니다.

1. Hello 대시보드에서 선택 **공유**합니다.
   
     ![공유 선택](./media/azure-portal-dashboard-share-access/select-share.png)
2. 액세스를 할당 하기 전에 hello 대시보드를 게시 해야 합니다. 기본적으로 hello 대시보드 이라는 게시 tooa 리소스 그룹 됩니다 **대시보드**합니다. **게시**를 선택합니다.
   
     ![게시](./media/azure-portal-dashboard-share-access/publish.png)

대시보드가 이제 게시되었습니다. Hello 구독에서 상속 되며, hello 사용 권한이 적절 한 경우, 불필요 toodo 하나라도 합니다. 조직의 다른 사용자가 수 tooaccess 되며 hello 대시보드 구독 수준에 따라 수정 합니다. 그러나이 자습서에서는 보겠습니다 할당 해당 대시보드에 대 한 사용자가 tooa 역할의 그룹.

## <a name="assign-access-tooa-dashboard"></a>액세스 tooa 대시보드 할당
1. Hello 대시보드를 게시 한 후 선택 **사용자 관리**합니다.
   
     ![사용자 관리](./media/azure-portal-dashboard-share-access/manage-users.png)
2. 이 대시보드에 대한 역할을 이미 할당한 기존 사용자의 목록이 표시됩니다. 기존 사용자 목록의 아래 hello 이미지 보다 달라 집니다. 대부분의 경우 hello 할당 hello 구독에서 상속 됩니다. tooadd 새 사용자 또는 그룹 선택 **추가**합니다.
   
     ![사용자 추가](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Toogrant 원하는 hello 사용 권한을 나타내는 hello 역할을 선택 합니다. 이 예에서는 **참가자**를 선택합니다.
   
     ![역할 선택](./media/azure-portal-dashboard-share-access/select-role.png)
4. Hello 사용자 또는 그룹 원하는 tooassign toohello 역할을 선택 합니다. Hello 사용자 또는 그룹 hello 목록에서 원하는 표시 되지 않으면 hello 검색 상자를 사용 합니다. 사용 가능한 그룹 목록 Active Directory에서 만든 hello 그룹에 따라 달라 집니다.
   
     ![사용자 선택](./media/azure-portal-dashboard-share-access/select-user.png) 
5. 사용자 또는 그룹을 추가했으면 **확인**을 선택합니다. 
6. hello 새 할당 toohello 사용자 목록에 추가 됩니다. 해당 **액세스**는 **상속됨**이 아닌 **할당**으로 나열됩니다.
   
     ![할당된 역할](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>다음 단계
* 역할의 목록은 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.
* 리소스를 관리 하는 방법에 대 한 toolearn 참조 [포털을 통해 관리 하는 Azure 리소스](resource-group-portal.md)합니다.

