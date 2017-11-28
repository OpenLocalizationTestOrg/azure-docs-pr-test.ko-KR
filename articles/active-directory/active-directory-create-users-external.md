---
title: "다른 디렉터리 또는 Azure Active Directory에서 파트너 회사의 사용자가 aaaAdd | Microsoft Docs"
description: "에 대해 설명 방법을 tooadd 사용자가 외부 및 게스트 사용자를 포함 한 Azure Active Directory에서 사용자 정보를 변경 합니다."
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
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a><span data-ttu-id="2ebc8-103">Azure Active Directory의 다른 디렉터리 또는 파트너 회사의 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="2ebc8-103">Add users from other directories or partner companies in Azure Active Directory</span></span>

<span data-ttu-id="2ebc8-104">이 문서에서는 설명 어떻게 tooadd 사용자가 Azure Active Directory에 있는 다른 디렉터리에서 또는 파트너 회사에서 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-104">This article explains how tooadd users from other directories in Azure Active Directory or add users from partner companies.</span></span> <span data-ttu-id="2ebc8-105">조직 내에서 새 사용자를 추가 하 고 Microsoft 계정을 가진 사용자를 추가 하는 방법에 대 한 정보를 참조 하십시오. [추가 Active Directory에 새 사용자 tooAzure](active-directory-create-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-105">For information about adding new users in your organization, and adding users who have Microsoft accounts, see [Add new users tooAzure Active Directory](active-directory-create-users.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2ebc8-106">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="2ebc8-107">Admin 님 안녕하세요 Azure AD에서에서 tooadd B2B 공동 작업 게스트 사용자의 가운데에 대 한 참조 [Azure AD B2B 공동 작업 이란?](active-directory-b2b-what-is-azure-ad-b2b.md)</span><span class="sxs-lookup"><span data-stu-id="2ebc8-107">For how tooadd B2B collaboration guest users in hello Azure AD admin center, see [What is Azure AD B2B collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)</span></span>

<span data-ttu-id="2ebc8-108">기본적으로 추가 된 사용자가 관리자 권한이 필요는 없지만 언제 든 지 역할 toothem를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-108">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="add-a-user"></a><span data-ttu-id="2ebc8-109">사용자 추가</span><span class="sxs-lookup"><span data-stu-id="2ebc8-109">Add a user</span></span>
1. <span data-ttu-id="2ebc8-110">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-110">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="2ebc8-111">**Active Directory**를 선택한 다음 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-111">Select **Active Directory**, and then open your directory.</span></span>
3. <span data-ttu-id="2ebc8-112">선택 hello **사용자** 탭을 선택한 다음 hello 명령 모음에서 선택 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-112">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="2ebc8-113">Hello에 **이 사용자에 대해 알리기** 페이지의 **유형의 사용자**을 하나 선택:</span><span class="sxs-lookup"><span data-stu-id="2ebc8-113">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="2ebc8-114">**다른 Azure AD 디렉터리의 사용자** – 다른 Azure AD 디렉터리에서 소싱 된 사용자 계정 tooyour 디렉터리에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-114">**User in another Azure AD directory** – adds a user account tooyour directory that's sourced from another Azure AD directory.</span></span> <span data-ttu-id="2ebc8-115">또한 사용자는 해당 디렉터리의 멤버인 경우에만 또 다른 디렉터리의 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-115">You can select a user in another directory only if you're also a member of that directory.</span></span>
   * <span data-ttu-id="2ebc8-116">**파트너 회사의 사용자** -tooinvite 고 파트너 회사 사용자 tooyour 디렉터리 권한을 부여 (참조 [Azure Active Directory B2B 공동 작업](active-directory-b2b-what-is-azure-ad-b2b.md)).</span><span class="sxs-lookup"><span data-stu-id="2ebc8-116">**Users in partner companies** - tooinvite and authorize partner company users tooyour directory (See [Azure Active Directory B2B collaboration](active-directory-b2b-what-is-azure-ad-b2b.md)).</span></span> <span data-ttu-id="2ebc8-117">너무 해야[전자 메일 주소를 지정 하는 CSV 파일 업로드](active-directory-b2b-references-csv-file-format.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-117">You'll need too[upload a CSV file specifying email addresses](active-directory-b2b-references-csv-file-format.md).</span></span>
5. <span data-ttu-id="2ebc8-118">Hello 사용자에 **프로필** 페이지에서 첫 번째 및 마지막 이름, 사용자에 게 친숙 한 이름 및 hello에서 사용자 역할을 제공 합니다. **역할** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="2ebc8-119">사용자 및 관리자 역할에 대한 자세한 내용은 [Azure AD에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="2ebc8-120">지정 여부 너무**다단계 인증 사용** hello 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
6. <span data-ttu-id="2ebc8-121">Hello에 **임시 암호 가져오기** 페이지에서 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ebc8-122">조직에서 둘 이상의 도메인을 사용 하는 경우 사용자 계정을 추가할 때 문제를 다음 hello 알아야:</span><span class="sxs-lookup"><span data-stu-id="2ebc8-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="2ebc8-123">tooadd 사용자 계정과 도메인 간에 동일한 사용자 계정 이름 (UPN) hello **첫 번째** 추가, 예를 들어 geoffgrisso@contoso.onmicrosoft.com, **이어서** geoffgrisso@contoso.com합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="2ebc8-124">geoffgrisso@contoso.onmicrosoft.com을 추가하기 전에 geoffgrisso@contoso.com을 추가하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span>
>

<span data-ttu-id="2ebc8-125">온-프레미스 Active Directory 서비스와 id 동기화 되는 사용자에 대 한 정보를 변경 하면 hello Azure 클래식 포털에서에서 hello 사용자 정보를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-125">If you change information for a user whose identity is synchronized with your on-premises Active Directory service, you can't change hello user information in hello Azure classic portal.</span></span> <span data-ttu-id="2ebc8-126">toochange hello 사용자 정보를 온-프레미스 Active Directory 관리 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-126">toochange hello user information, use your on-premises Active Directory management tools.</span></span>

## <a name="add-external-users"></a><span data-ttu-id="2ebc8-127">외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="2ebc8-127">Add external users</span></span>
<span data-ttu-id="2ebc8-128">추가할 수 있습니다도 사용자가 사용자가 속한 다른 Azure AD 디렉터리 toowhich 또는 파트너 회사에서 CSV 파일을 업로드 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-128">You can also add users from another Azure AD directory toowhich you belong, or from partner companies by uploading a CSV file.</span></span> <span data-ttu-id="2ebc8-129">tooadd 외부 사용자에 대 한 **사용자 유형**, 지정 **다른 Microsoft Azure AD 디렉터리의 사용자** 또는 **파트너 회사의 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-129">tooadd an external user, for **Type of User**, specify **User in another Microsoft Azure AD directory** or **Users in partner companies**.</span></span>

<span data-ttu-id="2ebc8-130">두 형식의 사용자는 모두 다른 디렉터리가 원본이며 **외부 사용자**로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-130">Users of either type are sourced from another directory and are added as **external users**.</span></span> <span data-ttu-id="2ebc8-131">외부 사용자는 모든 요구 사항 tooadd 새 계정 및 자격 증명 없이 디렉터리에 다른 사용자와 공동 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-131">External users can collaborate with other users in a directory without any requirement tooadd new accounts and credentials.</span></span> <span data-ttu-id="2ebc8-132">외부 사용자가 로그인 할 때 추가 된 다른 디렉터리 toowhich 인증은 해당 홈 디렉터리도 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-132">External users authenticate with their home directory when they sign in, and that authentication works for any other directories toowhich they have been added.</span></span>

## <a name="external-user-management-and-limitations"></a><span data-ttu-id="2ebc8-133">외부 사용자 관리 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="2ebc8-133">External user management and limitations</span></span>
<span data-ttu-id="2ebc8-134">다른 디렉터리 tooyour 디렉터리에서 사용자를 추가 하면 해당 사용자는 디렉터리의 외부 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-134">When you add a user from another directory tooyour directory, that user is an external user in your directory.</span></span> <span data-ttu-id="2ebc8-135">hello 표시 이름 및 사용자 이름 홈 디렉터리에서 복사 하 고 hello 디렉터리에 외부 사용자에 대해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-135">hello display name and user name are copied from their home directory and used for hello external user in your directory.</span></span> <span data-ttu-id="2ebc8-136">이제부터 hello 외부 사용자 계정의 속성은 완전히 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-136">From then on, properties of hello external user account are entirely independent.</span></span> <span data-ttu-id="2ebc8-137">속성이 변경 되 면 toohello 사용자가 홈 디렉터리에서 해당 변경 내용이 전파 되지 toohello 외부 사용자 계정을 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-137">If property changes are made toohello user in their home directory, those changes aren't propagated toohello external user account in your directory.</span></span>

<span data-ttu-id="2ebc8-138">hello 두 개의 계정 사이의 유일한 연결은 hello 해당 hello 사용자가 항상 홈 디렉터리에 대해 또는 Microsoft 계정으로 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-138">hello only linkage between hello two accounts is that hello user always authenticates against their home directory or with their Microsoft account.</span></span> <span data-ttu-id="2ebc8-139">바로 이러한 이유로 옵션 tooreset hello 암호를 표시 하지 않거나 외부 사용자에 대해 multi-factor authentication을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-139">That's why you don't see an option tooreset hello password or enable multi-factor authentication for an external user.</span></span> <span data-ttu-id="2ebc8-140">현재 hello 홈 디렉터리 또는 Microsoft 계정의 hello 인증 정책을 하나 hello 사용자가 로그인 할 때 평가 되는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-140">Currently, hello authentication policy of hello home directory or Microsoft account is hello only one that's evaluated when hello user signs in.</span></span>

> [!NOTE]
> <span data-ttu-id="2ebc8-141">여전히 hello tooyour 디렉터리에 액세스를 차단 하는 hello 디렉터리에 외부 사용자를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-141">You can still disable hello external user in hello directory, which blocks access tooyour directory.</span></span>
>
>

<span data-ttu-id="2ebc8-142">에서 홈 디렉터리에서 사용자가 삭제 되거나 Microsoft 계정을 취소 하는 경우 hello 외부 사용자는 디렉터리에 여전히 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-142">If a user is deleted in their home directory or they cancel their Microsoft account, hello external user still exists in your directory.</span></span> <span data-ttu-id="2ebc8-143">그러나 디렉터리의 hello 사용자 홈 디렉터리 또는 Microsoft 계정으로 인증할 수 없는 리소스 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-143">However, hello user in your directory can't access resources because they can't authenticate with a home directory or Microsoft account.</span></span>

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a><span data-ttu-id="2ebc8-144">현재 Azure AD 외부 사용자의 액세스를 지원하는 서비스</span><span class="sxs-lookup"><span data-stu-id="2ebc8-144">Services that currently support access by Azure AD external users</span></span>
* <span data-ttu-id="2ebc8-145">**Azure 클래식 포털**:는 외부 사용자가 여러 디렉터리 toomanage 각 해당 디렉터리의 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-145">**Azure classic portal**: allows an external user who's an administrator of multiple directories toomanage each of those directories.</span></span>
* <span data-ttu-id="2ebc8-146">**SharePoint Online**: 외부 공유를 사용 하는 경우 외부 사용자 tooaccess 권한이 SharePoint Online 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-146">**SharePoint Online**: if external sharing is enabled, allows an external user tooaccess SharePoint Online authorized resources.</span></span>
* <span data-ttu-id="2ebc8-147">**Dynamics CRM**: hello 사용자에 PowerShell을 통해 사용이 허가 하는 경우에 외부 사용자 tooaccess Dynamics CRM의 리소스 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-147">**Dynamics CRM**: if hello user is licensed via PowerShell, allows an external user tooaccess authorized resources in Dynamics CRM.</span></span>
* <span data-ttu-id="2ebc8-148">**Dynamics AX**: hello 사용자에 PowerShell을 통해 사용이 허가 하는 경우에 외부 사용자 tooaccess Dynamics AX의 리소스 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-148">**Dynamics AX**: if hello user is licensed via PowerShell, allows an external user tooaccess authorized resources in Dynamics AX.</span></span> <span data-ttu-id="2ebc8-149">제한 사항에 대 한 hello [외부 사용자가 Azure AD](#known-limitations-of-azure-ad-external-users) tooexternal 사용자가 Dynamics AX에도 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-149">hello limitations for [Azure AD external users](#known-limitations-of-azure-ad-external-users) apply tooexternal users in Dynamics AX as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ebc8-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ebc8-150">Next steps</span></span>
* [<span data-ttu-id="2ebc8-151">새 사용자 tooAzure Active Directory를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ebc8-151">Add new users tooAzure Active Directory</span></span>](active-directory-create-users.md)
* [<span data-ttu-id="2ebc8-152">Azure AD 관리</span><span class="sxs-lookup"><span data-stu-id="2ebc8-152">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="2ebc8-153">Azure AD에서 암호 관리</span><span class="sxs-lookup"><span data-stu-id="2ebc8-153">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="2ebc8-154">Azure AD에서 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="2ebc8-154">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)
