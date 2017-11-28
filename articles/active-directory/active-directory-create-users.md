---
title: "aaaAdd 새 사용자 tooAzure Active Directory | Microsoft Docs"
description: "에 대해 설명 방법을 tooadd 새 사용자 또는 Azure Active Directory에서 사용자 정보를 변경 합니다."
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
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="28eb0-103">새 사용자 또는 Microsoft 계정 tooAzure Active Directory와 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="28eb0-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="28eb0-104">사용자가 toopopulate 디렉터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="28eb0-105">이 문서에서는 설명 방법을 tooadd 조직 내에서 새 사용자와 방법을 tooadd 사용자에 게 Microsoft 계정을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="28eb0-106">Azure Active Directory의 다른 디렉터리의 사용자 추가 또는 파트너 회사의 사용자 추가에 대한 자세한 내용은 [Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가](active-directory-create-users-external.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28eb0-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="28eb0-107">기본적으로 추가 된 사용자가 관리자 권한이 필요는 없지만 언제 든 지 역할 toothem를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28eb0-108">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="28eb0-109">Tooadd hello Azure AD 관리 센터에서 사용자 참조에 대 한 [추가 Active Directory에 새 사용자 tooAzure](active-directory-users-create-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="28eb0-110">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="28eb0-110">Add a user</span></span>
1. <span data-ttu-id="28eb0-111">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="28eb0-112">선택 **Active Directory**, 조직 디렉터리의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="28eb0-113">선택 hello **사용자** 탭을 선택한 다음 hello 명령 모음에서 선택 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="28eb0-114">Hello에 **이 사용자에 대해 알리기** 페이지의 **유형의 사용자**을 하나 선택:</span><span class="sxs-lookup"><span data-stu-id="28eb0-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="28eb0-115">**조직의 새 사용자** – 디렉터리에 새 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="28eb0-116">**기존 Microsoft 계정 사용자** – 기존 Microsoft 소비자 계정 tooyour 디렉터리 (예: Outlook 계정)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="28eb0-117">**사용자 유형**에 따라 사용자 이름(새 사용자) 또는 전자 메일 주소(Microsoft 계정이 있는 사용자)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="28eb0-118">Hello 사용자에 **프로필** 페이지에서 첫 번째 및 마지막 이름, 사용자에 게 친숙 한 이름 및 hello에서 사용자 역할을 제공 합니다. **역할** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="28eb0-119">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28eb0-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="28eb0-120">지정 여부 너무**다단계 인증 사용** hello 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="28eb0-121">Hello에 **임시 암호 가져오기** 페이지에서 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28eb0-122">조직에서 둘 이상의 도메인을 사용 하는 경우 사용자 계정을 추가할 때 문제를 다음 hello 알아야:</span><span class="sxs-lookup"><span data-stu-id="28eb0-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="28eb0-123">tooadd 사용자 계정과 도메인 간에 동일한 사용자 계정 이름 (UPN) hello **첫 번째** 추가, 예를 들어 geoffgrisso@contoso.onmicrosoft.com, **이어서** geoffgrisso@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="28eb0-124">geoffgrisso@contoso.onmicrosoft.com을 추가하기 전에 geoffgrisso@contoso.com을 추가하지 **마세요**. 이 순서는 중요, 하며 번거로운 tooundo 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="28eb0-125">사용자 정보 변경</span><span class="sxs-lookup"><span data-stu-id="28eb0-125">Change user information</span></span>
<span data-ttu-id="28eb0-126">Hello 개체 ID 제외 하 고 모든 사용자 특성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="28eb0-127">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-127">Open your directory.</span></span>
2. <span data-ttu-id="28eb0-128">선택 hello **사용자** 탭 및의 표시 이름을 선택한 후 hello hello toochange 하려는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="28eb0-129">변경을 완료하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="28eb0-130">변경 하는 hello 사용자는 온-프레미스 Active Directory 서비스와 동기화 되 면이 절차를 사용 하 여 hello 사용자 정보를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="28eb0-131">toochange hello 사용자 하려면 온-프레미스 Active Directory 관리 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="28eb0-132">게스트 사용자 관리 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="28eb0-132">Guest user management and limitations</span></span>
<span data-ttu-id="28eb0-133">게스트 계정은 초대한 tooyour 디렉터리 tooaccess SharePoint 문서, 응용 프로그램, 또는 다른 Azure 리소스로 이었던 다른 디렉터리의 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="28eb0-134">디렉터리에 게스트 계정에는 기본 UserType 특성 설정 너무 "Guest."</span><span class="sxs-lookup"><span data-stu-id="28eb0-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="28eb0-135">일반 사용자 (특히, 디렉터리의 구성원) 특성이 hello UserType "멤버"입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="28eb0-136">게스트는 hello 디렉터리에 제한 된 권한 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="28eb0-137">이러한 권한은 hello 디렉터리에 다른 사용자에 대 한 게스트 toodiscover 정보에 대 한 hello 기능을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="28eb0-138">그러나 게스트 사용자에 게 hello 사용자 및 그룹에서 작업 하는 hello 리소스와 관련 된 상호 작용 여전히 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="28eb0-139">게스트 사용자는 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-139">Guest users can:</span></span>

* <span data-ttu-id="28eb0-140">다른 사용자와 그룹을 할당 하는 Azure 구독 toowhich와 관련 된 참조</span><span class="sxs-lookup"><span data-stu-id="28eb0-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="28eb0-141">소속 그룹 toowhich의 hello 멤버를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="28eb0-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="28eb0-142">Hello 사용자의 hello 전체 전자 메일 주소를 알고 있으면 hello 디렉터리에 다른 사용자가을 조회합니다</span><span class="sxs-lookup"><span data-stu-id="28eb0-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="28eb0-143">제한 된 집합의 특성을-제한 toodisplay 이름, 전자 메일 주소, 사용자 계정 이름 (UPN) 및 미리 보기 사진 찾아볼 hello 사용자의를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="28eb0-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="28eb0-144">Hello 디렉터리의 확인 된 도메인 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="28eb0-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="28eb0-145">권한을 부여 하는 동의 tooapplications hello 멤버 디렉터리에 있는 동일한 액세스</span><span class="sxs-lookup"><span data-stu-id="28eb0-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="28eb0-146">게스트 사용자 액세스 정책 설정</span><span class="sxs-lookup"><span data-stu-id="28eb0-146">Set guest user access policies</span></span>
<span data-ttu-id="28eb0-147">hello **구성** 디렉터리의 탭에는 게스트 사용자에 대 한 옵션 toocontrol 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="28eb0-148">이러한 옵션은 디렉터리 전역 관리자에 의해 Azure 클래식 포털에서만 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="28eb0-149">현재는 PowerShell 또는 API 메서드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="28eb0-150">tooopen hello **구성** hello에 탭 Azure 클래식 포털에서 선택 **Active Directory**, hello 디렉터리의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Azure Active Directory의 구성 탭][1]

<span data-ttu-id="28eb0-152">다음 게스트 사용자에 대 한 hello 옵션 toocontrol 액세스를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb0-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![게스트 사용자에 대한 액세스 제어 옵션][2]

## <a name="whats-next"></a><span data-ttu-id="28eb0-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28eb0-154">What's next</span></span>
* [<span data-ttu-id="28eb0-155">Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="28eb0-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="28eb0-156">Azure AD 관리</span><span class="sxs-lookup"><span data-stu-id="28eb0-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="28eb0-157">Azure AD에서 암호 관리</span><span class="sxs-lookup"><span data-stu-id="28eb0-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="28eb0-158">Azure AD에서 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="28eb0-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
