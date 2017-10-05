---
title: "Azure Active Directory에 새 사용자 추가 | Microsoft Docs"
description: "Azure Active Directory에서 새 사용자를 추가하거나 사용자 정보를 변경하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="e5118-103">Azure Active Directory에 새 사용자 또는 Microsoft 계정이 있는 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="e5118-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="e5118-104">사용자를 추가하여 디렉터리를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-104">Add users to populate your directory.</span></span> <span data-ttu-id="e5118-105">이 문서에서는 조직 내에서 새 사용자를 추가하는 방법 및 Microsoft 계정이 있는 사용자를 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="e5118-106">Azure Active Directory의 다른 디렉터리의 사용자 추가 또는 파트너 회사의 사용자 추가에 대한 자세한 내용은 [Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가](active-directory-create-users-external.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5118-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="e5118-107">기본적으로 추가된 사용자에게는 관리자 권한이 없지만 언제든 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5118-108">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="e5118-109">Azure AD 관리 센터에서 사용자를 추가하는 방법은 [Azure Active Directory에 새 사용자 추가](active-directory-users-create-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5118-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="e5118-110">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="e5118-110">Add a user</span></span>
1. <span data-ttu-id="e5118-111">디렉터리에 대한 전역 관리자인 계정으로 [Azure 클래식 포털](https://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e5118-112">**Active Directory**를 선택한 다음 조직 디렉터리의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="e5118-113">**사용자** 탭을 선택한 다음 명령 모음에서 **사용자 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="e5118-114">**이 사용자에 대해 알리기** 페이지의 **사용자 형식**에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="e5118-115">**조직의 새 사용자** – 디렉터리에 새 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="e5118-116">**기존 Microsoft 계정이 있는 사용자** – 디렉터리에 기존 사용자 Microsoft 고객 계정(예: Outlook 계정)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="e5118-117">**사용자 유형**에 따라 사용자 이름(새 사용자) 또는 전자 메일 주소(Microsoft 계정이 있는 사용자)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="e5118-118">사용자 **프로필** 페이지에 **역할** 목록의 이름과 성, 별명 및 사용자 역할을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="e5118-119">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5118-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="e5118-120">사용자에 대해 **Multi-Factor Authentication 사용** 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="e5118-121">**임시 암호 가져오기** 페이지에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5118-122">조직에서 둘 이상의 도메인을 사용하는 경우 사용자 계정을 추가할 때 다음과 같은 문제를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="e5118-123">도메인 간에 동일한 UPN(사용자 계정 이름)을 가진 사용자 계정을 추가하려면 예를 들어 **먼저** geoffgrisso@contoso.onmicrosoft.com을 추가한 **다음** geoffgrisso@contoso.com을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="e5118-124">geoffgrisso@contoso.onmicrosoft.com을 추가하기 전에 geoffgrisso@contoso.com을 추가하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="e5118-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="e5118-125">이 작업은 중요하며 실행을 취소하기가 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="e5118-126">사용자 정보 변경</span><span class="sxs-lookup"><span data-stu-id="e5118-126">Change user information</span></span>
<span data-ttu-id="e5118-127">개체 ID를 제외하고 모든 사용자 특성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="e5118-128">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-128">Open your directory.</span></span>
2. <span data-ttu-id="e5118-129">**사용자** 탭을 선택하고 변경하려는 사용자의 표시 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="e5118-130">변경을 완료하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="e5118-131">변경하려는 사용자가 온-프레미스 Active Directory 서비스와 동기화된 경우 이 절차를 사용하여 사용자 정보를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="e5118-132">사용자를 변경하려면 온-프레미스 Active Directory 관리 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="e5118-133">게스트 사용자 관리 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="e5118-133">Guest user management and limitations</span></span>
<span data-ttu-id="e5118-134">게스트 계정은 SharePoint 문서, 응용 프로그램 또는 기타 Azure 리소스에 액세스할 수 있도록 내 디렉터리에 초대된 다른 디렉터리의 사용자를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="e5118-135">디렉터리의 게스트 계정은 기본 UserType 특성이 "게스트"로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="e5118-136">일반 사용자(즉, 내 디렉터리의 멤버)는 UserType 특성이 "멤버"입니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="e5118-137">게스트는 디렉터리에서 제한된 권한 집합을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="e5118-138">이러한 권한은 디렉터리의 다른 사용자에 대한 정보를 검색하는 게스트의 기능을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="e5118-139">그러나 게스트 사용자가 작업하는 리소스와 관련된 사용자 및 그룹과 계속 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="e5118-140">게스트 사용자는 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-140">Guest users can:</span></span>

* <span data-ttu-id="e5118-141">할당된 Azure 구독과 관련된 다른 사용자 및 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="e5118-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="e5118-142">속한 그룹의 멤버 보기</span><span class="sxs-lookup"><span data-stu-id="e5118-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="e5118-143">사용자의 전체 메일 주소를 알고 있는 경우 디렉터리의 다른 사용자 조회</span><span class="sxs-lookup"><span data-stu-id="e5118-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="e5118-144">조회하는 사용자의 제한된 특성 보기 - 표시 이름, 메일 주소, UPN(사용자 계정 이름) 및 축소한 사진으로 제한됨</span><span class="sxs-lookup"><span data-stu-id="e5118-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="e5118-145">디렉터리의 확인된 도메인 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="e5118-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="e5118-146">디렉터리의 멤버와 동일한 액세스 권한을 부여하며 응용 프로그램에 동의</span><span class="sxs-lookup"><span data-stu-id="e5118-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="e5118-147">게스트 사용자 액세스 정책 설정</span><span class="sxs-lookup"><span data-stu-id="e5118-147">Set guest user access policies</span></span>
<span data-ttu-id="e5118-148">디렉터리의 **구성** 탭에는 게스트 사용자의 액세스를 제어하는 옵션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="e5118-149">이러한 옵션은 디렉터리 전역 관리자에 의해 Azure 클래식 포털에서만 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="e5118-150">현재는 PowerShell 또는 API 메서드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="e5118-151">Azure 클래식 포털에서 **구성** 탭을 열려면 **Active Directory**를 선택한 다음 디렉터리의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Azure Active Directory의 구성 탭][1]

<span data-ttu-id="e5118-153">그러면 게스트 사용자의 액세스를 제어하는 옵션을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5118-153">Then you can edit the options to control access for guest users.</span></span>

![게스트 사용자에 대한 액세스 제어 옵션][2]

## <a name="whats-next"></a><span data-ttu-id="e5118-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5118-155">What's next</span></span>
* [<span data-ttu-id="e5118-156">Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="e5118-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="e5118-157">Azure AD 관리</span><span class="sxs-lookup"><span data-stu-id="e5118-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="e5118-158">Azure AD에서 암호 관리</span><span class="sxs-lookup"><span data-stu-id="e5118-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="e5118-159">Azure AD에서 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="e5118-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
