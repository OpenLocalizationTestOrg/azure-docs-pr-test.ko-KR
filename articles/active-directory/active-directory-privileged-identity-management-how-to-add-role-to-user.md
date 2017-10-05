---
title: "사용자 역할을 추가하거나 제거하는 방법| Microsoft Azure"
description: "Azure Active Directory Privileged Identity Management 응용 프로그램을 사용하여 권한 있는 ID에 역할을 추가하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: 3ac07bb7b070f44595c099a454b3d0dbc66126c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a><span data-ttu-id="a6bb9-103">Azure AD Privileged Identity Management: 사용자 역할을 추가 또는 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="a6bb9-103">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>
<span data-ttu-id="a6bb9-104">Azure AD(Active Directory)와 전역 관리자(또는 회사 관리자)는 사용자가 Azure AD에서 **영구적으로** 역할에 할당되도록 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span></span> <span data-ttu-id="a6bb9-105">이 작업은 `Add-MsolRoleMember` 및 `Remove-MsolRoleMember` 등 PowerShell cmdlet을 사용하여 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="a6bb9-106">또는 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)에 설명된 대로 Azure 클래식 포털을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="a6bb9-107">Azure AD Privileged Identity Management 응용 프로그램을 통해 권한 있는 역할 관리자가 영구 역할 할당을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span></span> <span data-ttu-id="a6bb9-108">또한 권한이 있는 역할 관리자는 사용자의 관리자 역할을 **적격**으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="a6bb9-109">적격인 관리자는 필요할 때 역할을 활성화할 수 있으며 작업을 완료하고 나면 권한이 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-the-azure-portal"></a><span data-ttu-id="a6bb9-110">Azure 포털에서 PIM으로 역할 관리</span><span class="sxs-lookup"><span data-stu-id="a6bb9-110">Manage roles with PIM in the Azure portal</span></span>
<span data-ttu-id="a6bb9-111">조직에서 Azure AD, Office 365 및 기타 Microsoft 서비스 및 응용 프로그램의 다른 관리 역할에 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="a6bb9-112">사용 가능한 역할에 대한 자세한 내용은 [Azure AD PIM의 역할](active-directory-privileged-identity-management-roles.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="a6bb9-113">Privileged Identity Management를 사용하여 역할에 사용자를 추가하거나 제거하려면 PIM 대시보드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span></span> <span data-ttu-id="a6bb9-114">그런 다음 **관리자 역할의 사용자** 단추를 클릭하거나 역할 테이블에서 특정 역할(예: 전역 관리자)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="a6bb9-115">Azure 포털에서 아직 PIM을 사용하도록 설정하지 않은 경우 [Azure AD PIM 시작](active-directory-privileged-identity-management-getting-started.md) 에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="a6bb9-116">다른 사용자가 PIM에 액세스할 수 있도록 하려는 경우 PIM에 필요한 사용자 역할은 [PIM에 대한 액세스 권한을 제공하는 방법](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="a6bb9-117">역할에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="a6bb9-117">Add a user to a role</span></span>
1. <span data-ttu-id="a6bb9-118">[Azure 포털](https://portal.azure.com/)에서 대시보드의 **Azure AD Privileged Identity Management** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span></span>
2. <span data-ttu-id="a6bb9-119">**권한 있는 역할 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="a6bb9-120">**역할 요약** 테이블에서 관리하려는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-120">In the **Role summary** table, select the role you want to manage.</span></span>
4. <span data-ttu-id="a6bb9-121">역할 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-121">In the role blade, select **Add**.</span></span>
5. <span data-ttu-id="a6bb9-122">**사용자 선택**을 클릭하고 **사용자 선택** 블레이드에서 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-122">Click **Select users** and search for the user on the **Select users** blade.</span></span>  
6. <span data-ttu-id="a6bb9-123">검색 결과 목록에서 사용자를 선택하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-123">Select the user from the search results list, and click **Done**.</span></span>
7. <span data-ttu-id="a6bb9-124">**확인** 을 클릭하여 선택 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-124">Click **OK** to save your selection.</span></span> <span data-ttu-id="a6bb9-125">선택한 사용자가 그 역할에 대해 적합하다고 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-125">The user you have selected will appear in the list as eligible for the role.</span></span>

> [!NOTE]
> <span data-ttu-id="a6bb9-126">역할에 포함된 새 사용자는 기본적으로 그 역할에 대해서만 자격이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-126">New users in a role are only eligible for the role by default.</span></span> <span data-ttu-id="a6bb9-127">역할을 영구적으로 지정하려면 목록에서 사용자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-127">If you want to make the role permanent, click the user in the list.</span></span> <span data-ttu-id="a6bb9-128">사용자의 정보가 새 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-128">The user's information will appear in a new blade.</span></span> <span data-ttu-id="a6bb9-129">사용자 정보 메뉴에서 **make perm** (영구 지정)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-129">Select **Make perm** in the user information menu.</span></span>  
> <span data-ttu-id="a6bb9-130">사용자에 대 한 Azure Multi-factor Authentication (MFA)를 등록할 수 없습니다 또는 Microsoft 계정을 사용 하는 경우 (일반적으로 @outlook.com), 해당 역할에 영구적으로 적용 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span> <span data-ttu-id="a6bb9-131">활성화 과정에서 적격 관리자에게 MFA를 등록하도록 요청하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-131">Eligible admins are asked to register for MFA during activation.</span></span>

<span data-ttu-id="a6bb9-132">사용자가 역할을 부여받을 자격이 있으므로 [역할을 활성화 또는 비활성화하는 방법](active-directory-privileged-identity-management-how-to-activate-role.md)의 지침에 따라 역할을 활성화할 수 있음을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="a6bb9-133">역할에서 사용자 제거</span><span class="sxs-lookup"><span data-stu-id="a6bb9-133">Remove a user from a role</span></span>
<span data-ttu-id="a6bb9-134">적격 역할 할당에서 사용자를 제거할 수 있지만 영구 전역 관리자인 사용자가 최소 한 명은 항상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="a6bb9-135">특정 사용자를 역할에서 제거하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-135">Follow these steps to remove a specific user from a role:</span></span>

1. <span data-ttu-id="a6bb9-136">Azure AD PIM 대시보드에서 역할을 선택하거나 **관리자 역할의 사용자** 단추를 클릭하여 역할 목록의 역할로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="a6bb9-137">사용자 목록에서 사용자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-137">Click on the user in the user list.</span></span>
3. <span data-ttu-id="a6bb9-138">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-138">Click **Remove**.</span></span> <span data-ttu-id="a6bb9-139">메시지에서 확인을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-139">A message will ask you to confirm.</span></span>
4. <span data-ttu-id="a6bb9-140">사용자로부터 역할을 제거하려면 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-140">Click **Yes** to remove the role from the user.</span></span>

<span data-ttu-id="a6bb9-141">사용자에게 해당 역할 할당이 여전히 필요한지 확실하지 않은 경우에는 [역할에 대한 액세스 권한을 검토하기 시작](active-directory-privileged-identity-management-how-to-start-security-review.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6bb9-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6bb9-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6bb9-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

