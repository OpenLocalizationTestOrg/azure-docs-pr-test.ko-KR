---
title: "hello Azure 포털에서에서 액세스 제어 aaaRole 기반 | Microsoft Docs"
description: "시작 액세스 관리에서 hello Azure 포털의에서 역할 기반 액세스 제어 합니다. 역할 할당 tooassign 권한 tooyour 리소스를 사용 합니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>역할 기반 액세스 제어 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여
> [!div class="op_single_selector"]
> * [사용자 또는 그룹에 따른 액세스 관리](role-based-access-control-manage-assignments.md)
> * [리소스에 따른 액세스 관리](role-based-access-control-configure.md)

Azure RBAC(역할 기반 액세스 제어)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다. RBAC를 사용 하 여 권한을 부여할 수 있습니다만 hello 제한 된 액세스 사용자를에 tooperform 업무를 필요 합니다. 이 문서를 사용 하면 hello Azure 포털에에서 RBAC 실행 되 고 시작 합니다. RBAC를 사용하여 액세스를 관리하는 방법에 대한 자세한 정보를 원하는 경우 [역할 기반 액세스 제어란](role-based-access-control-what-is.md)을 참조하세요.

각 구독 내에서 too2000 역할 할당을 부여할 수 있습니다. 

## <a name="view-access"></a>액세스 보기
Hello에서 액세스 tooa 리소스, 리소스 그룹 또는 해당 기본 블레이드에서 구독을가지고 있는 사람을 확인할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 예를 들어이 리소스 그룹의 액세스 tooone 가진 toosee 주시기 바랍니다.

1. 선택 **리소스 그룹** hello hello 왼쪽 탐색 모음에서.  
    ![리소스 그룹 - 아이콘](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Hello에서 hello 리소스 그룹의 이름을 선택 hello **리소스 그룹** 블레이드입니다.
3. 선택 **액세스 제어 (IAM)** hello 왼쪽된 메뉴에서 합니다.  
4. 모든 사용자, 그룹 및 응용 프로그램 액세스 toohello 리소스 그룹에 부여 된 액세스 제어 블레이드 hello를 나열 합니다.  
   
    ![사용자 블레이드 - 상속된 및 할당된 액세스 스크린샷](./media/role-based-access-control-configure/view-access.png)

일부 역할은 너무 범위가 지정 된 것을 알**이 리소스** 이지만 나머지는 **Inherited** 다른 범위에서 합니다. 액세스는 toohello 리소스 그룹에 특별히 할당 또는 할당 toohello 부모 구독에서 상속 합니다.

> [!NOTE]
> 클래식 구독 관리자와 공동 관리자는 hello 새 RBAC 모델에서의 hello 구독 소유자 간주 됩니다.

## <a name="add-access"></a>액세스 추가
Hello 리소스, 리소스 그룹 또는 hello 역할 할당의 hello 범위는 구독 내에서 액세스 권한을 부여할 수 있습니다.

1. 선택 **추가** hello 액세스 제어 블레이드에서 합니다.  
2. 선택 hello 역할 tooassign hello에서 원하는 **역할 선택** 블레이드입니다.
3. 에 대 한 toogrant 액세스 하려는 디렉터리의 hello 사용자, 그룹 또는 응용 프로그램을 선택 합니다. 표시 이름, 전자 메일 주소 및 개체 식별자에 hello 디렉터리를 검색할 수 있습니다.  
   
    ![사용자 추가 블레이드 - 검색 스크린샷](./media/role-based-access-control-configure/grant-access2.png)
4. 선택 **확인** toocreate hello 할당 합니다. hello **추가 사용자** 팝업 hello 진행 상태를 추적 합니다.  
    ![사용자 진행률 표시줄 추가 - 스크린샷](./media/role-based-access-control-configure/addinguser_popup.png)

역할 할당을 성공적으로 추가한 후에 나타나는 hello **사용자** 블레이드입니다.

## <a name="remove-access"></a>액세스 제거
1. Tooremove hello 할당의 hello 이름 위에 커서를 올려서 합니다. 확인란 다음 toohello 이름 나타납니다.
2. 확인란 tooselect hello를 사용 하 여 하나 이상의 역할 할당 합니다.
2. **제거**를 선택합니다.  
3. 선택 **예** tooconfirm hello 제거 합니다.

상속된 할당을 제거할 수 있습니다. Tooremove 상속 된 할당 해야 할 경우 toodo hello 역할 할당 생성 된 위치 범위 hello에 필요 합니다. Hello에 **범위** 열, 다음 너무**Inherited** 이동 하는 리소스 toohello이이 역할 할당 된 링크가 있습니다. 여기에 나열 된 toohello 리소스 이동 tooremove hello 역할 할당 합니다.

![사용자 블레이드 - 상속된 액세스는 제거 단추를 사용할 수 없도록 설정함 스크린샷](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>다른 도구 toomanage 액세스
역할을 할당 하 고 Azure 포털 hello 이외의 다른 도구에서 Azure RBAC 명령 사용 하 여 액세스를 관리할 수 있습니다.  Hello 링크 toolearn hello 필수 구성 요소에 대 한 자세한 따르고 hello Azure RBAC 명령을 사용 하 여 시작 합니다.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Azure 명령줄 인터페이스](role-based-access-control-manage-access-azure-cli.md)
* [REST API](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>다음 단계
* [액세스 변경 기록 보고서 만들기](role-based-access-control-access-change-history-report.md)
* Hello 참조 [RBAC 기본 제공 역할](role-based-access-built-in-roles.md)
* [Azure RBAC에서 사용자 지정 역할](role-based-access-control-custom-roles.md)

