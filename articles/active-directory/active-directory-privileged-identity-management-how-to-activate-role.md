---
title: "aaaHow tooactivate는 역할을 하거나 비활성화 | Microsoft Docs"
description: "Tooactivate 역할에 대 한 hello Azure Privileged Identity Management 응용 프로그램 id를 특권 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>어떻게 tooactivate 또는 역할에 Azure AD Privileged Identity Management 비활성화 하려면
Azure AD (Active Directory) Privileged Identity Management 기업 Azure AD에서 권한 있는 액세스 tooresources 및 Microsoft Intune 또는 Office 365와 같은 다른 Microsoft online services를 관리 하는 방법을 간소화 합니다.  

하면 내용이 있으면 관리 역할에 대 한 적격, 즉, tooperform 권한 있는 작업을 할 때 해당 역할을 활성화할 수 있습니다. 예를 들어 경우에 따라 Office 365 기능을 관리하는 경우 조직의 권한 있는 역할 관리자는 해당 역할이 다른 서비스에도 또한 영향을 주므로 사용자를 영구적인 전역 관리자로 만들지 못할 수 있습니다. 대신 Exchange Online 관리자와 같은 Azure AD 역할에 대한 자격을 줍니다. 해당 권한이 필요 합니다. 미리 결정 된 기간에 대 한 관리 제어 가질 수 하는 경우 해당 역할 tooactivate을 요청할 수 있습니다.

이 문서는 Azure AD Privileged Identity Management (PIM)에서 자신의 역할 tooactivate 해야 하는 관리자입니다. 안내 합니다 hello 단계 tooactivate 역할 hello 사용 권한이 필요 하 고 완료 되 면 hello 역할을 비활성화 합니다. 또한 권한 있는 역할 관리자 승인 tooactivate 역할 (미리 보기)를 요구할 수 있습니다. [PIM 승인 워크플로](./privileged-identity-management/azure-ad-pim-approval-workflow.md)에 대한 자세한 내용은 여기를 참조하세요.

## <a name="add-hello-privileged-identity-management-application"></a>Hello Privileged Identity Management 응용 프로그램 추가
Hello Azure AD Privileged Identity Management 응용 프로그램을 사용 하 여 hello에 [Azure 포털](https://portal.azure.com/) toorequest 다른 포털 또는 PowerShell에서 toooperate 거 하는 경우에 역할 활성화 합니다. Hello Azure AD Privileged Identity Management 응용 프로그램을 다른 Azure 포털에 없는 경우에 따라 이러한 단계 tooget 시작 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 작동 중인 hello Azure 포털의 상단 오른쪽 모서리 hello 및 수는 선택 hello 디렉터리에 사용자 이름을 선택 합니다.
3. 선택 **더 많은 서비스** 에 대 한 필터 텍스트 상자에 붙여넣습니다 toosearch hello를 사용 하 여 **Azure AD Privileged Identity Management**합니다.
4. 확인 **Pin toodashboard** 클릭 하 고 **만들기**합니다. hello Privileged Identity Management 응용 프로그램을 엽니다.

## <a name="activate-a-role"></a>역할 활성화
Hello를 선택 하 여 정품 인증을 요청할 수 tootake 역할에 필요한 경우 **내 역할** hello Azure AD Privileged Identity Management 응용 프로그램에서 탐색 옵션의 왼쪽 탐색 열입니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 및 선택 hello Azure AD Privileged Identity Management 타일입니다.
2. **My Roles**(내 역할)를 선택합니다. Hello hello 페이지 위쪽에 그룹화 하는 hello에 할당 된 해당 역할의 목록이 나타납니다.
3. 역할 tooactivate를 선택 합니다.
4. **활성화**를 선택합니다. hello **역할 활성화 요청** 블레이드 나타납니다.
5. 일부 역할 hello 역할을 활성화 하기 전에 Multi-factor Authentication (MFA) 필요 합니다. 세션당 한 번씩 tooauthenticate를 하기만 하면 됩니다.
   
    ![역할 활성화 전에 MFA 사용하여 확인합니다 - 스크린샷][2]
6. Hello 텍스트 필드에 hello 정품 인증 요청에 대 한 hello 이유를 입력 합니다.  일부 역할을 사용 하는 데 문제가 티켓 번호 toosupply를 해야합니다.
7. **확인**을 선택합니다.  Hello 역할 승인이 필요 하지 않습니다, 이제 활성화 및 hello 역할 활성 역할 (바로 아래 hello 목록 적격 역할 할당)의 hello 목록에 나타납니다. 경우 hello [역할 승인이 필요한](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, hello의 오른쪽 위에 알리는 hello 승인이 보류 중인 브라우저에 알림 메시지 표시 간단 하 게 됩니다.

    ![보류 중인 요청 알림 - 스크린샷][3]

## <a name="deactivate-a-role"></a>역할 비활성화
역할이 활성화된 후 시간 제한(적격 기간)에 도달하면 자동으로 비활성화됩니다.

관리 작업을 조기에 완료 hello Azure AD Privileged Identity Management 응용 프로그램에서 수동으로 역할을 비활성화할 수 있습니다.  선택 **내 역할**를 삭제 하 고 나면 hello 역할 선택 하 여 hello에서 사용 하 여 **활성 역할 할당** 그룹화 및 선택 **비활성화**합니다.  

## <a name="cancel-a-pending-request"></a>보류 중인 요청 취소
Hello 이벤트에 필요 하지 않으면 승인이 필요한 역할의 활성화, 언제 든 지 보류 중인 요청을 취소할 수 있습니다. 단순히 select hello **내 역할** hello Azure AD Privileged Identity Management 응용 프로그램에서 탐색 옵션의 왼쪽 탐색 열입니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 및 선택 hello Azure AD Privileged Identity Management 타일입니다.
2. **My Roles**(내 역할)를 선택합니다. Hello hello 페이지 위쪽에 그룹화 하는 hello에 할당 된 해당 역할의 목록이 나타납니다.
3. 원하는 역할을 선택합니다.
4. 선택 hello **थ ा प 활성화가** hello 역할 활성화 세부 정보 블레이드에서 배너 합니다.
5. 선택 **취소** hello의 hello 위쪽 **थ ा प** 블레이드입니다.

   ![보류 중인 요청 취소 스크린샷][4]

## <a name="next-steps"></a>다음 단계
Azure AD Privileged Identity Management에 대해 더 관심이 hello 다음 링크 한 자세한 정보.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
