---
title: "aaaAdd 소유자 및 사용자가 Azure DevTest Labs | Microsoft Docs"
description: "Hello Azure 포털 또는 PowerShell을 사용 하 여 Azure DevTest Labs에 소유자와 사용자 추가"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a>Azure DevTest Labs에 소유자 및 사용자 추가
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

Azure DevTest Labs의 액세스는 [Azure RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-what-is.md)를 통해 제어됩니다. RBAC를 사용 하 여 있습니다 수 구분할 업무에 팀 내에서 *역할* 하면 부여 hello 양의 데이터만 액세스가 필요한 toousers tooperform 작업 합니다. 이러한 세 가지 RBAC 역할은 *소유자*, *DevTest Labs 사용자* 및 *참가자*입니다. 이 문서에 알아봅니다 hello 세 가지 주요 RBAC 역할의 각 작업을 수행할 수 있습니다. 어떻게 tooadd 사용자 tooa 랩-를 통해 둘 다 hello 배웁니다 여기서에서 포털 및 PowerShell 스크립트 및에서 tooadd 사용자 구독 수준 hello 하는 방법을 통해 합니다.

## <a name="actions-that-can-be-performed-in-each-role"></a>각 역할에서 수행할 수 있는 작업
사용자를 할당할 수 있는 세 가지 주요 역할이 있습니다.

* 소유자
* DevTest Lab 사용자
* 참여자

hello 다음 테이블에서는 이러한 각 역할의 사용자가 수행할 수 있는 hello 작업 수행 합니다.

| **이 역할의 사용자가 수행할 수 있는 작업** | **DevTest Lab 사용자** | **소유자** | **참여자** |
| --- | --- | --- | --- |
| **랩 작업** | | | |
| 사용자가 tooa 랩 추가 |아니요 |예 |아니요 |
| 비용 설정 업데이트 |아니요 |예 |예 |
| **VM 기본 작업** | | | |
| 사용자 지정 이미지 추가 및 제거 |아니요 |예 |예 |
| 수식 추가, 업데이트 및 삭제 |예 |예 |예 |
| Azure Marketplace 이미지를 허용 목록에 추가 |아니요 |예 |예 |
| **VM 작업** | | | |
| VM 만들기 |예 |예 |예 |
| VM 시작, 중지 및 삭제 |Hello 사용자가 만든 Vm에만 |예 |예 |
| VM 정책 업데이트 |아니요 |예 |예 |
| VM에 데이터 디스크 추가/VM에서 데이터 디스크 제거 |Hello 사용자가 만든 Vm에만 |예 |예 |
| **아티팩트 작업** | | | |
| 아티팩트 리포지토리 추가 및 제거 |아니요 |예 |예 |
| 아티팩트 적용 |예 |예 |예 |

> [!NOTE]
> 사용자는 VM을 만들 해당 사용자가 자동으로 할당 toohello **소유자** VM을 만든 hello의 역할을 합니다.
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a>Hello 랩 수준에서 소유자 또는 사용자를 추가 합니다.
Hello Azure 포털을 통해 hello 랩 수준에서 소유자 및 사용자를 추가할 수 있습니다. 여기에는 유효한 [MSA(Microsoft 계정)](devtest-lab-faq.md#what-is-a-microsoft-account)를 가진 외부 사용자도 포함됩니다.
단계를 수행 하는 hello Azure DevTest Labs에는 소유자 또는 사용자 tooa 랩을 추가 hello 과정을 안내 합니다.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.
3. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.
4. Hello 랩 블레이드에서 선택 **구성**합니다. 
5. Hello에 **구성** 블레이드를 **사용자**합니다.
6. Hello에 **사용자** 블레이드를 **+ 추가**합니다.
   
    ![사용자 추가](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. Hello에 **역할 선택** 블레이드, 선택 hello 할당할된 역할을 합니다. 섹션 hello [각 역할에서 수행할 수 있는 작업](#actions-that-can-be-performed-in-each-role) 목록 hello hello 소유자, DevTest 사용자 및 참가자 역할의 사용자가 수행할 수 있는 다양 한 작업입니다.
8. Hello에 **사용자 추가** 블레이드에서 hello 전자 메일 주소 또는 지정한 hello 역할에 tooadd hello 사용자의 이름을 입력 합니다. Hello 사용자를 찾을 수 없는 경우 오류 메시지가 hello 문제를 설명 합니다. Hello 사용자의 경우, 해당 사용자가 선택 되어 나열 합니다. 
9. **선택**을 선택합니다.
10. 선택 **확인** tooclose hello **액세스 추가** 블레이드입니다.
11. Toohello 돌아가서 **사용자** 블레이드에서 hello 사용자가 추가 되었습니다.  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a>PowerShell을 사용 하는 외부 사용자 tooa 랩을 추가합니다
또한 hello Azure 포털에서에서 tooadding 사용자, PowerShell 스크립트를 사용 하는 외부 사용자 tooyour 랩을 추가할 수 있습니다. Hello에서 hello에서 hello 매개 변수 값을 수정 하면 다음 예제를 **값 toochange** 메모 합니다.
Hello를 검색할 수 있습니다 `subscriptionId`, `labResourceGroup`, 및 `labName` hello Azure 포털에서에서 hello 랩 블레이드의 값으로에서.

> [!NOTE]
> hello 샘플 스크립트는 hello 사용자 게스트 toohello Active Directory로 추가 되 고 hello 대/소문자 그렇지 않은 경우 실패 합니다를 지정 하는 것으로 가정 합니다. Active Directory tooa 랩 hello에 없는 사용자 tooadd hello 섹션에 설명 된 대로 hello Azure 포털 tooassign hello 사용자 tooa 역할을 사용 [hello 랩 수준에서 소유자 또는 사용자를 추가](#add-an-owner-or-user-at-the-lab-level)합니다.   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a>Hello 구독 수준에서 소유자 또는 사용자를 추가 합니다.
Azure에서 부모 범위 toochild 범위에서 azure 권한 전파 됩니다. 따라서 랩을 포함하는 Azure 구독 소유자는 자동으로 해당 랩의 소유자입니다. Hello Vm 및 기타 리소스 hello lab의 사용자 및 hello Azure DevTest Labs 서비스에서 만든 또한 소유한. 

Hello에 hello 랩 블레이드를 통해 tooa 랩 추가 소유자를 추가할 수 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다. 그러나 hello 소유자의 관리 범위는 hello 구독 소유자의 범위 보다 더 세부적인 추가 합니다. 예를 들어 hello 추가 소유자 hello DevTest Labs 서비스에 의해 hello 구독에서 만들어진 hello 리소스에 대 한 모든 권한을 toosome 필요가 없습니다. 

tooadd 소유자 tooan Azure 구독에는 다음이 단계를 따르십시오.

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.
2. 선택 **더 서비스**를 선택한 후 **구독** hello 목록에서 합니다.
3. Hello 원하는 구독을 선택 합니다.
4. **액세스** 아이콘을 선택합니다. 
   
    ![사용자 액세스](./media/devtest-lab-add-devtest-user/access-users.png)
5. Hello에 **사용자** 블레이드를 **추가**합니다.
   
    ![사용자 추가](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. Hello에 **역할 선택** 블레이드에서 선택 **소유자**합니다.
7. Hello에 **사용자 추가** 블레이드에서 hello 전자 메일 주소 또는 이름을 입력 hello 사용자의 소유자로 tooadd 원하는 합니다. Hello 사용자를 찾을 수 없는 경우 hello 문제를 설명 하는 오류 메시지를 가져옵니다. Hello 사용자의 경우, 해당 사용자 아래에 있는지 hello **사용자** 입력란.
8. Hello 있는 사용자 이름을 선택 합니다.
9. **선택**을 선택합니다.
10. 선택 **확인** tooclose hello **액세스 추가** 블레이드입니다.
11. Toohello 돌아가서 **사용자** 블레이드에서 hello 사용자가 소유자로 추가 되었습니다. 이 사용자는 이제이 구독에서 만든 모든 랩의 소유자가 되며 수 tooperform 소유자 작업 여야 합니다. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

