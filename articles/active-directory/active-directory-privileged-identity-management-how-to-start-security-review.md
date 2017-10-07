---
title: "aaaHow toostart 액세스 검토 | Microsoft Docs"
description: "어떻게 toocreate 대 한 액세스를 검토 하 여 hello Azure Privileged Identity Management 응용 프로그램으로 권한 있는 id에 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>어떻게 toostart 액세스에서에서 검토 하 고 Azure AD Privileged Identity Management
사용자가 더 이상 필요 없는 권한 있는 액세스를 가진 경우 "오래된" 역할 할당이 됩니다. 순서 tooreduce hello는 관련 된 오래 된 역할은 위험, 권한 있는 역할 관리자가 사용자 지정 된 hello 역할을 정기적으로 검토 해야 합니다. 이 문서에서는 Azure AD Privileged Identity Management (PIM)에서 액세스 검토를 시작 하기 위한 hello 단계를 설명 합니다.

## <a name="start-an-access-review"></a>액세스 검토 시작
> [!NOTE]
> Hello Azure 포털에서에서 hello PIM 응용 프로그램 tooyour 대시보드를 추가 하지 않았다면, 참조의 hello 단계 [Azure Privileged Identity Management 시작 하기](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Hello PIM 응용 프로그램 기본 페이지에서 세 가지 방법으로 toostart 액세스 검토

* **액세스 검토** > **추가**
* **역할** > **검토** 단추
* Hello 역할 목록에서 선택 hello 특정 역할 toobe 검토 > **검토** 단추

Hello에 클릭할 때 **검토** 단추 hello **액세스 검토를 시작** 블레이드 나타납니다. 이 블레이드를 이름으로 하락 tooconfigure hello 검토 하는 및 제한 시간, 역할 tooreview 선택한는 hello 검토를 수행할지 결정 합니다.

![액세스 검토 시작 - 스크린 샷][1]

### <a name="configure-hello-review"></a>Hello 검토를 구성 합니다.
toocreate 대 한 액세스를 검토 하 고 시작 및 종료 날짜 집합 tooname를 해야 합니다.

![검토 구성 - 스크린 샷][2]

충분 한 시간 동안 사용자가 toocomplete 검토 hello의 hello 길이 확인 합니다. Hello 종료 날짜 이전에 완료 일찍 hello 검토를 중지할 항상 있습니다.

### <a name="choose-a-role-tooreview"></a>역할 tooreview 선택
각 검토는 오직 하나의 역할에 집중합니다. 특정 역할 블레이드에서 hello 액세스 검토를 시작 하지 않은 이제 toochoose 역할 필요 합니다.

1. 너무 이동**역할 구성원 자격 검토**
   
    ![역할 멤버 자격 검토 - 스크린샷][3]
2. Hello 목록에서 역할 하나를 선택 합니다.

### <a name="decide-who-will-perform-hello-review"></a>hello 검토를 수행할지 결정 합니다.
검토를 수행하는 데 세 가지 옵션이 있습니다. Hello 검토 toosomeone를 할당할 수 있습니다 다른 toocomplete 할 수 있는 것을 직접 또는 각 사용자가 자신의 액세스 검토 있을 수 있습니다.

1. 너무 이동**검토자를 선택 합니다.**
   
    ![검토자 선택 - 스크린 샷][4]
2. Hello 옵션 중 하나를 선택 합니다.
   
   * **검토자 선택**: 액세스가 필요한 사용자를 알 수 없는 경우 이 옵션을 사용합니다. 이 옵션을 hello 검토 tooa 리소스 소유자 또는 관리자 toocomplete 그룹을 할당할 수 있습니다.
   * **Me**: 방법을 toopreview 사용 하려는 경우 유용 tooreview 수 없는 사용자를 대신 하 여 원하는 또는 access 작업을 검토 합니다.
   * **멤버 자체 검토**:이 옵션 toohave hello 사용자가 검토 자신의 역할 할당을 사용 합니다.

### <a name="start-hello-review"></a>Hello 검토를 시작
마지막으로 hello 옵션 toorequire 액세스를 승인 하는 경우 사용자가 이유를 제공 해야 합니다. 원하는 경우 hello 검토에 대 한 설명을 추가 하 고 선택 **시작**합니다.

고객을 위해 대기 하는 액세스 검토가 있다는 것을 표시 합니다. 따라서 사용자가 있는지 확인 [어떻게 tooperform 액세스 검토](active-directory-privileged-identity-management-how-to-perform-security-review.md)합니다.

## <a name="manage-hello-access-review"></a>Hello 액세스 검토를 관리 합니다.
Hello 검토자가 검토 hello Azure AD PIM 대시보드에서에서 완료 된 것으로 hello 진행률을 추적할 수, access hello에서 섹션을 검토 합니다. 액세스 권한이 없습니다.까지 hello 디렉터리에 변경 됩니다 [hello 검토 완료](active-directory-privileged-identity-management-how-to-complete-review.md)합니다.

Hello 검토 기간이 끝나면 될 때까지 해당 검토 사용자 toocomplete를 알려줍니다 또는 중지 hello 검토 초기 hello 액세스 로부터 검토 섹션.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>PIM 목차
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
