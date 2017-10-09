---
title: "aaaAssign 사용자 Azure Active Directory에서 tooadministrator 역할 | Microsoft Docs"
description: "에 대해 설명 방법을 toochange Azure Active Directory에서 사용자 관리 정보"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="49aa6-103">Azure Active Directory에서 tooadministrator 역할에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="49aa6-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="49aa6-104">이 문서에서는 설명 방법을 tooassign 관리 역할 tooa 사용자를 사용 하 여 Azure Active Directory (Azure AD)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="49aa6-105">조직의 새 사용자를 추가 하는 방법에 대 한 정보를 참조 하십시오. [추가 Active Directory에 새 사용자 tooAzure](active-directory-users-create-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="49aa6-106">기본적으로 추가 된 사용자가 관리자 권한이 필요는 없지만 언제 든 지 역할 toothem를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="49aa6-107">역할 tooa 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="49aa6-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="49aa6-108">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="49aa6-109">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="49aa6-111">Hello에 **사용자 및 그룹** 블레이드를 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![여는 모든 사용자 블레이드 hello](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="49aa6-113">Hello에 **사용자 및 그룹-모든 사용자에 게** 블레이드에서 hello 목록에서 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="49aa6-114">Hello 선택한 사용자에 대 한 hello 블레이드에서 선택 **디렉터리 역할**, 다음 역할을 할당 hello 사용자 tooa hello에서 **디렉터리 역할** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="49aa6-115">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49aa6-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![사용자 tooa 역할 할당](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="49aa6-117">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49aa6-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49aa6-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49aa6-118">Next steps</span></span>
* [<span data-ttu-id="49aa6-119">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="49aa6-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="49aa6-120">Hello 새 Azure 포털에서 사용자의 암호를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49aa6-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="49aa6-121">사용자의 작업 정보 변경</span><span class="sxs-lookup"><span data-stu-id="49aa6-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="49aa6-122">사용자 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="49aa6-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="49aa6-123">Azure AD에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="49aa6-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
