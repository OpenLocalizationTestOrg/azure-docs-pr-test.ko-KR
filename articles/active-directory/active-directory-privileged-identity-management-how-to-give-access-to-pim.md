---
title: "Privileged Identity Management에 대한 액세스 권한을 제공하는 방법 - Azure | Microsoft Docs"
description: "PIM을 관리할 수 있도록 Azure Active Directory Privileged Identity Management 확장을 사용하여 사용자에 역할을 추가하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="f1bc6-103">Azure AD Privileged Identity Management를 관리하기 위해 액세스 권한 제공</span><span class="sxs-lookup"><span data-stu-id="f1bc6-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="f1bc6-104">조직에 대한 Azure AD Privileged Identity Management (PIM)을 사용하는 전역 관리자는 자동적으로 역할 할당 및 PIM에 대한 액세스를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="f1bc6-105">하지만, 기본적으로 다른 전역 관리자를 포함하여 아무도 쓰기 액세스 권한을 갖지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="f1bc6-106">다른 전역 관리자, 보안 관리자 및 보안 판독기에는 Azure AD PIM에 대한 읽기 전용 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="f1bc6-107">PIM에 대한 액세스를 제공하기 위해 첫 번째 사용자가 다른 사용자를 **권한 있는 역할 관리자** 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="f1bc6-108">이 할당은 PIM 자체 내에서 수행해야 하고 PowerShell 또는 다른 포털을 통해 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="f1bc6-109">Azure AD PIM 관리에 Azure MFA가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="f1bc6-110">Azure MFA에 대해 Microsoft 계정을 등록할 수 없기 때문에 Microsoft 계정으로 로그인하는 사용자는 Azure AD PIM에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="f1bc6-111">한 명의 사용자가 잠긴 경우 또는 해당 계정이 삭제된 경우 최소한 두 명의 사용자가 항상 권한 있는 역할 관리자 역할에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="f1bc6-112">PIM을 관리하기 위해 다른 사용자에게 액세스 권한 제공</span><span class="sxs-lookup"><span data-stu-id="f1bc6-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="f1bc6-113">[Azure 포털](https://portal.azure.com/) 에 로그인하고 대시보드에서 **Azure AD Privileged Identity Management** 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="f1bc6-114">**권한 있는 역할 관리** > **권한 있는 역할 관리자** > **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![권한 있는 역할 관리자 추가 - 스크린샷][1]
3. <span data-ttu-id="f1bc6-116">관리되는 사용자 추가 블레이드에서 1 단계는 이미 완료된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="f1bc6-117">2 단계를 선택하여, **사용자를 선택** 하고 추가할 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![사용자 선택 - 스크린 샷][2]
4. <span data-ttu-id="f1bc6-119">검색 결과에서 사용자를 선택하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="f1bc6-120">**확인** 을 클릭하여 선택 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="f1bc6-121">선택한 사용자가 권한 있는 역할 관리자 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="f1bc6-122">다른 사람에게 새 역할을 할당할 때마다 자동으로 해당 역할을 활성화할 자격이 있는 것으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="f1bc6-123">영구적으로 역할에 지정하려면 목록에서 사용자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="f1bc6-124">사용자 정보 메뉴에서 **make perm** (영구 지정)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="f1bc6-125">사용자에게 [Azure AD Privileged Identity Management 시작](active-directory-privileged-identity-management-getting-started.md)링크를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="f1bc6-126">PIM 관리에 대한 다른 사용자의 액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="f1bc6-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="f1bc6-127">권한 있는 역할 관리자 역할에서 사용자를 제거하기 전에 항상 두 명의 사용자가 이 역할에 할당되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="f1bc6-128">PIM 대시보드에서 역할 **권한 있는 역할 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="f1bc6-129">현재 해당 역할 상태인 사용자 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="f1bc6-130">사용자 목록에서 사용자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="f1bc6-131">**제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-131">Click on **Remove**.</span></span>  <span data-ttu-id="f1bc6-132">확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="f1bc6-133">역할로부터 사용자를 제거하려면 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1bc6-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="f1bc6-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1bc6-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
