---
title: "Azure Active Directory에서 관리자 역할에 사용자 할당 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 관리 정보를 변경하는 방법을 설명합니다."
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
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="57fe1-103">Azure Active Directory에서 관리자 역할에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="57fe1-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="57fe1-104">이 문서는 Azure AD(Azure Active Directory)에서 사용자에게 관리 역할을 할당하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="57fe1-105">조직 내에서 새 사용자 추가에 대한 자세한 내용은 [Azure Active Directory에 새 사용자 추가](active-directory-users-create-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57fe1-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="57fe1-106">기본적으로 추가된 사용자에게는 관리자 권한이 없지만 언제든 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="57fe1-107">사용자에게 역할 할당</span><span class="sxs-lookup"><span data-stu-id="57fe1-107">Assign a role to a user</span></span>
1. <span data-ttu-id="57fe1-108">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="57fe1-109">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="57fe1-111">**사용자 및 그룹** 블레이드에서 **모든 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![모든 사용자 블레이드 열기](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="57fe1-113">**사용자 및 그룹 - 모든 사용자** 블레이드의 목록에서 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="57fe1-114">선택한 사용자에 대한 블레이드에서 **디렉터리 역할**을 선택한 다음 **디렉터리 역할** 목록의 역할에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="57fe1-115">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57fe1-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![역할에 사용자 할당](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="57fe1-117">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57fe1-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57fe1-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57fe1-118">Next steps</span></span>
* [<span data-ttu-id="57fe1-119">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="57fe1-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="57fe1-120">새 Azure 포털에서 사용자의 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="57fe1-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="57fe1-121">사용자의 작업 정보 변경</span><span class="sxs-lookup"><span data-stu-id="57fe1-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="57fe1-122">사용자 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="57fe1-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="57fe1-123">Azure AD에서 사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="57fe1-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
