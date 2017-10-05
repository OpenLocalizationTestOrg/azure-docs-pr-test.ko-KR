---
title: "Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가 | Microsoft Docs"
description: "외부 및 게스트 사용자를 포함하여 Azure Active Directory에서 사용자를 추가하거나 사용자 정보를 변경하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 399230584d01986dd0f793a6ff8245ef2b4f8fb1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a><span data-ttu-id="a195e-103">Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="a195e-103">Add users from other directories or partner companies in Azure Active Directory</span></span>

<span data-ttu-id="a195e-104">이 문서에서는 Azure Active Directory에 있는 다른 디렉터리의 사용자를 추가하거나 파트너 회사의 사용자를 추가하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-104">This article explains how to add users from other directories in Azure Active Directory or add users from partner companies.</span></span> <span data-ttu-id="a195e-105">조직 내에서 새 사용자 추가 및 Microsoft 계정이 있는 사용자 추가에 대한 자세한 내용은 [Azure Active Directory에 새 사용자 추가](active-directory-create-users.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a195e-105">For information about adding new users in your organization, and adding users who have Microsoft accounts, see [Add new users to Azure Active Directory](active-directory-create-users.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a195e-106">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="a195e-107">Azure AD 관리 센터에서 B2B 공동 작업 게스트 사용자를 추가하는 방법은 [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a195e-107">For how to add B2B collaboration guest users in the Azure AD admin center, see [What is Azure AD B2B collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)</span></span>

<span data-ttu-id="a195e-108">기본적으로 추가된 사용자에게는 관리자 권한이 없지만 언제든 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-108">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="add-a-user"></a><span data-ttu-id="a195e-109">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="a195e-109">Add a user</span></span>
1. <span data-ttu-id="a195e-110">디렉터리에 대한 전역 관리자인 계정으로 [Azure 클래식 포털](https://manage.windowsazure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-110">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="a195e-111">**Active Directory**를 선택한 다음 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-111">Select **Active Directory**, and then open your directory.</span></span>
3. <span data-ttu-id="a195e-112">**사용자** 탭을 선택한 다음 명령 모음에서 **사용자 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-112">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="a195e-113">**이 사용자에 대해 알리기** 페이지의 **사용자 형식**에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-113">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="a195e-114">**다른 Azure AD 디렉터리의 사용자** – 다른 Azure AD 디렉터리가 원본인 사용자 계정을 사용자 디렉터리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-114">**User in another Azure AD directory** – adds a user account to your directory that's sourced from another Azure AD directory.</span></span> <span data-ttu-id="a195e-115">또한 사용자는 해당 디렉터리의 멤버인 경우에만 또 다른 디렉터리의 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-115">You can select a user in another directory only if you're also a member of that directory.</span></span>
   * <span data-ttu-id="a195e-116">**파트너 회사의 사용자** - 파트너 회사 사용자를 디렉터리에 초대하고 권한 부여( [Azure Active Directory B2B 공동 작업 참조](active-directory-b2b-what-is-azure-ad-b2b.md)).</span><span class="sxs-lookup"><span data-stu-id="a195e-116">**Users in partner companies** - to invite and authorize partner company users to your directory (See [Azure Active Directory B2B collaboration](active-directory-b2b-what-is-azure-ad-b2b.md)).</span></span> <span data-ttu-id="a195e-117">[전자 메일 주소를 지정하는 CSV 파일을 업로드](active-directory-b2b-references-csv-file-format.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-117">You'll need to [upload a CSV file specifying email addresses](active-directory-b2b-references-csv-file-format.md).</span></span>
5. <span data-ttu-id="a195e-118">사용자 **프로필** 페이지에 **역할** 목록의 이름과 성, 별명 및 사용자 역할을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="a195e-119">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a195e-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="a195e-120">사용자에 대해 **Multi-Factor Authentication 사용** 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
6. <span data-ttu-id="a195e-121">**임시 암호 가져오기** 페이지에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a195e-122">조직에서 둘 이상의 도메인을 사용하는 경우 사용자 계정을 추가할 때 다음과 같은 문제를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="a195e-123">도메인 간에 동일한 UPN(사용자 계정 이름)을 가진 사용자 계정을 추가하려면 예를 들어 **먼저** geoffgrisso@contoso.onmicrosoft.com을 추가한 **다음** geoffgrisso@contoso.com을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="a195e-124">geoffgrisso@contoso.onmicrosoft.com을 추가하기 전에 geoffgrisso@contoso.com을 추가하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="a195e-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span>
>

<span data-ttu-id="a195e-125">ID가 온-프레미스 Active Directory 서비스와 동기화된 사용자에 대한 정보를 변경하는 경우 Azure 클래식 포털에서 사용자 정보를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-125">If you change information for a user whose identity is synchronized with your on-premises Active Directory service, you can't change the user information in the Azure classic portal.</span></span> <span data-ttu-id="a195e-126">사용자 정보를 변경하려면 온-프레미스 Active Directory 관리 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-126">To change the user information, use your on-premises Active Directory management tools.</span></span>

## <a name="add-external-users"></a><span data-ttu-id="a195e-127">외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="a195e-127">Add external users</span></span>
<span data-ttu-id="a195e-128">또한 사용자가 속해 있는 Azure AD 디렉터리 또는 파트너 회사에서 CSV 파일을 업로드하여 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-128">You can also add users from another Azure AD directory to which you belong, or from partner companies by uploading a CSV file.</span></span> <span data-ttu-id="a195e-129">외부 사용자를 추가하려면 **사용자 형식**으로 **다른 Microsoft Azure AD 디렉터리의 사용자** 또는 **파트너 회사의 사용자**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-129">To add an external user, for **Type of User**, specify **User in another Microsoft Azure AD directory** or **Users in partner companies**.</span></span>

<span data-ttu-id="a195e-130">두 형식의 사용자는 모두 다른 디렉터리가 원본이며 **외부 사용자**로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-130">Users of either type are sourced from another directory and are added as **external users**.</span></span> <span data-ttu-id="a195e-131">외부 사용자가 새 계정 및 자격 증명을 추가하지 않아도 디렉터리에 있는 다른 사용자와 공동 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-131">External users can collaborate with other users in a directory without any requirement to add new accounts and credentials.</span></span> <span data-ttu-id="a195e-132">외부 사용자는 로그인 시 홈 디렉터리로 인증하며 해당 인증은 해당 사용자가 추가된 다른 모든 디렉터리에서 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-132">External users authenticate with their home directory when they sign in, and that authentication works for any other directories to which they have been added.</span></span>

## <a name="external-user-management-and-limitations"></a><span data-ttu-id="a195e-133">외부 사용자 관리 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="a195e-133">External user management and limitations</span></span>
<span data-ttu-id="a195e-134">다른 디렉터리의 사용자를 내 디렉터리에 추가하면 해당 사용자는 내 디렉터리에서 외부 사용자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-134">When you add a user from another directory to your directory, that user is an external user in your directory.</span></span> <span data-ttu-id="a195e-135">표시 이름 및 사용자 이름을 해당 홈 디렉터리에서 복사하고 내 디렉터리에서 외부 사용자로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-135">The display name and user name are copied from their home directory and used for the external user in your directory.</span></span> <span data-ttu-id="a195e-136">이후로 외부 사용자 계정의 속성을 완전히 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-136">From then on, properties of the external user account are entirely independent.</span></span> <span data-ttu-id="a195e-137">해당 홈 디렉터리의 사용자에 대한 속성이 변경된 경우 해당 변경 내용은 내 디렉터리에 있는 외부 사용자 계정에 전파되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-137">If property changes are made to the user in their home directory, those changes aren't propagated to the external user account in your directory.</span></span>

<span data-ttu-id="a195e-138">두 계정 사이의 유일한 연계는 사용자가 항상 홈 디렉터리에 대해 인증을 받거나 자신의 Microsoft 계정으로 인증을 받는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-138">The only linkage between the two accounts is that the user always authenticates against their home directory or with their Microsoft account.</span></span> <span data-ttu-id="a195e-139">이러한 이유로 암호를 다시 설정하거나 외부 사용자에 대해 Multi-Factor Authentication을 활성화하는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-139">That's why you don't see an option to reset the password or enable multi-factor authentication for an external user.</span></span> <span data-ttu-id="a195e-140">현재는 사용자가 로그인 할 때 홈 디렉터리 또는 Microsoft 계정의 인증 정책만 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-140">Currently, the authentication policy of the home directory or Microsoft account is the only one that's evaluated when the user signs in.</span></span>

> [!NOTE]
> <span data-ttu-id="a195e-141">디렉터리에서 외부 사용자가 여전히 비활성화될 수 있으며 이로 인해 디렉터리에 대한 액세스가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-141">You can still disable the external user in the directory, which blocks access to your directory.</span></span>
>
>

<span data-ttu-id="a195e-142">홈 디렉터리에서 사용자가 삭제되거나 사용자가 자신의 Microsoft 계정을 취소하더라도 해당 외부 사용자는 여전히 내 디렉터리에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-142">If a user is deleted in their home directory or they cancel their Microsoft account, the external user still exists in your directory.</span></span> <span data-ttu-id="a195e-143">그러나 내 디렉터리의 사용자는 홈 디렉터리 또는 Microsoft 계정으로 인증할 수 없기 때문에 리소스에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-143">However, the user in your directory can't access resources because they can't authenticate with a home directory or Microsoft account.</span></span>

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a><span data-ttu-id="a195e-144">현재 Azure AD 외부 사용자의 액세스를 지원하는 서비스</span><span class="sxs-lookup"><span data-stu-id="a195e-144">Services that currently support access by Azure AD external users</span></span>
* <span data-ttu-id="a195e-145">**Azure 클래식 포털**: 여러 디렉터리의 관리자인 외부 사용자가 해당하는 각 디렉터리를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-145">**Azure classic portal**: allows an external user who's an administrator of multiple directories to manage each of those directories.</span></span>
* <span data-ttu-id="a195e-146">**SharePoint Online**: 외부 공유가 활성화될 경우 SharePoint Online에서 권한을 부여한 리소스에 외부 사용자가 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-146">**SharePoint Online**: if external sharing is enabled, allows an external user to access SharePoint Online authorized resources.</span></span>
* <span data-ttu-id="a195e-147">**Dynamics CRM**: PowerShell을 통해 라이선스를 부여할 경우 사용이 허가된 리소스에 외부 사용자가 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-147">**Dynamics CRM**: if the user is licensed via PowerShell, allows an external user to access authorized resources in Dynamics CRM.</span></span>
* <span data-ttu-id="a195e-148">**Dynamics AX**: PowerShell을 통해 라이선스를 부여할 경우 외부 사용자가 Dynamics AX의 권한이 부여된 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-148">**Dynamics AX**: if the user is licensed via PowerShell, allows an external user to access authorized resources in Dynamics AX.</span></span> <span data-ttu-id="a195e-149">[Azure AD 외부 사용자](#known-limitations-of-azure-ad-external-users) 에 대한 제한은 Dynamics AX의 외부 사용자에게도 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a195e-149">The limitations for [Azure AD external users](#known-limitations-of-azure-ad-external-users) apply to external users in Dynamics AX as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a195e-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a195e-150">Next steps</span></span>
* [<span data-ttu-id="a195e-151">Azure Active Directory에 새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="a195e-151">Add new users to Azure Active Directory</span></span>](active-directory-create-users.md)
* [<span data-ttu-id="a195e-152">Azure AD 관리</span><span class="sxs-lookup"><span data-stu-id="a195e-152">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="a195e-153">Azure AD에서 암호 관리</span><span class="sxs-lookup"><span data-stu-id="a195e-153">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="a195e-154">Azure AD에서 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="a195e-154">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)
