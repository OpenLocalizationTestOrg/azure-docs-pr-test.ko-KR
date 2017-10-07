---
title: "Azure Active Directory의 aaaManaging 그룹 | Microsoft Docs"
description: "어떻게 toocreate 그룹 toomanage Azure 관리 및 사용자가 Azure Active Directory를 사용 합니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="1d7c1-103">Azure Active Directory에서 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="1d7c1-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d7c1-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="1d7c1-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="1d7c1-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="1d7c1-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="1d7c1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d7c1-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="1d7c1-107">Azure Active Directory (Azure AD) 사용자 관리 hello 기능 중 하나는 사용자의 hello 기능 toocreate 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="1d7c1-108">할당 하는 등 라이선스 또는 권한을 tooa 사용자 수가 한 번에 한 그룹 tooperform 관리 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="1d7c1-109">또한 그룹 tooassign 액세스 권한을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="1d7c1-110">예: hello 디렉터리의 개체는 리소스</span><span class="sxs-lookup"><span data-stu-id="1d7c1-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="1d7c1-111">SaaS 응용 프로그램, Azure 서비스, SharePoint 사이트 또는 온-프레미스 리소스와 같은 리소스 외부 toohello 디렉터리</span><span class="sxs-lookup"><span data-stu-id="1d7c1-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="1d7c1-112">또한 리소스 소유자는 다른 사용자가 소유한 액세스 tooa 리소스 tooan Azure AD 그룹을 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="1d7c1-113">이 할당 해당 그룹 액세스 toohello 리소스의 hello 구성원에 게 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="1d7c1-114">그런 다음 hello 그룹의 hello 소유자 hello 그룹의 멤버 자격을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="1d7c1-115">효과적으로 hello 리소스 소유자 대리자 toohello의 소유자 hello 그룹 hello 권한 tooassign 사용자 tootheir 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d7c1-116">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="1d7c1-117">Hello Azure AD 관리 센터에서 toomanage 그룹 방법을 참조 [그룹을 만들고 Azure Active Directory에 멤버 추가](active-directory-groups-create-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="1d7c1-118">그룹을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1d7c1-118">How do I create a group?</span></span>
<span data-ttu-id="1d7c1-119">Hello 서비스 toowhich 조직에서 구독을 따라 hello 다음 중 하나를 사용 하 여 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="1d7c1-120">hello Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="1d7c1-120">hello Azure classic portal</span></span>
* <span data-ttu-id="1d7c1-121">hello Office 365 계정 포털</span><span class="sxs-lookup"><span data-stu-id="1d7c1-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="1d7c1-122">hello Windows Intune 계정 포털</span><span class="sxs-lookup"><span data-stu-id="1d7c1-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="1d7c1-123">설명 하 고 작업 hello Azure 클래식 포털에서에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="1d7c1-124">Azure AD 디렉터리 toomanage 비 Azure 포털을 사용 하는 방법에 대 한 자세한 내용은 참조 [Azure AD 디렉터리 관리](active-directory-administer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="1d7c1-125">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="1d7c1-126">선택 hello **그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="1d7c1-127">**그룹 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="1d7c1-128">Hello에 **그룹 추가** 창의 hello 이름을 지정 하 고 hello에 대 한 그룹 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="1d7c1-129">보안 그룹에서 개별 사용자를 추가하거나 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="1d7c1-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="1d7c1-130">**개별 사용자 tooa 그룹 tooadd**</span><span class="sxs-lookup"><span data-stu-id="1d7c1-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="1d7c1-131">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="1d7c1-132">선택 hello **그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="1d7c1-133">Hello 그룹 toowhich를 tooadd 구성원이 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="1d7c1-134">열기 hello **멤버** hello 탭 그룹을 선택 하는 경우 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="1d7c1-135">**멤버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="1d7c1-136">Hello에 **구성원 추가** 페이지, hello 사용자 또는이 그룹의 구성원으로 tooadd 원하는 그룹이 선택 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="1d7c1-137">이 이름은 toohello 추가 되는지 확인 **선택한** 창.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="1d7c1-138">**tooremove 개별 사용자의 그룹**</span><span class="sxs-lookup"><span data-stu-id="1d7c1-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="1d7c1-139">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="1d7c1-140">선택 hello **그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="1d7c1-141">Tooremove 멤버 원하는 hello 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="1d7c1-142">선택 hello **멤버** 탭,이 그룹에서 tooremove 원하고 클릭 hello 멤버의 선택 hello 이름 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="1d7c1-143">Hello 프롬프트 것인지 확인 하는 tooremove hello 그룹에서이 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="1d7c1-144">그룹의 구성원이 hello를 동적으로 관리할 수는 방법</span><span class="sxs-lookup"><span data-stu-id="1d7c1-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="1d7c1-145">Azure AD에서 사용자 toobe 그룹의 멤버인 hello 간단한 규칙 toodetermine를를 매우 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="1d7c1-146">간단한 규칙에서 단일 비교를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="1d7c1-147">예를 들어 그룹이 SaaS 응용 프로그램 tooa 할당 되 면 설정할 수 있습니다 "Sales Rep". 직함을 가진 규칙 tooadd 사용자를</span><span class="sxs-lookup"><span data-stu-id="1d7c1-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="1d7c1-148">이 규칙의 디렉터리에 해당 직책을 가진 toothis SaaS 응용 프로그램 tooall 사용자 액세스를 다음 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="1d7c1-149">사용자 변경의 특성을 hello 시스템 평가 되 면 hello 특성 변경 hello 사용자의 모든 그룹을 발생 시키는 경우 디렉터리 toosee의 모든 동적 그룹 규칙을 추가 하거나 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="1d7c1-150">그룹에 규칙을 충족 하는 사용자, 멤버 toothat 그룹으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="1d7c1-151">멤버인 그룹의 hello 규칙을 더 이상 만족 하는 경우는 멤버와 해당 그룹에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="1d7c1-152">보안 그룹 또는 Office 365 그룹에서 동적 멤버 자격에 대한 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="1d7c1-153">중첩 된 그룹 멤버 자격 그룹 기반 할당 tooapplications에 대 한 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="1d7c1-154">그룹에 대 한 동적 멤버 자격을 할당 하는 Azure AD Premium 라이선스 toobe 필요</span><span class="sxs-lookup"><span data-stu-id="1d7c1-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="1d7c1-155">hello 규칙 그룹에서 관리 하는 hello 관리자</span><span class="sxs-lookup"><span data-stu-id="1d7c1-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="1d7c1-156">Hello 그룹의 모든 멤버</span><span class="sxs-lookup"><span data-stu-id="1d7c1-156">All members of hello group</span></span>
>
>

<span data-ttu-id="1d7c1-157">**그룹에 대 한 동적 멤버 자격 tooenable**</span><span class="sxs-lookup"><span data-stu-id="1d7c1-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="1d7c1-158">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory**, 조직에 대 한 hello 디렉터리의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="1d7c1-159">선택 hello **그룹** 탭 및 tooedit hello open 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="1d7c1-160">선택 hello **구성** 탭을 클릭 한 다음 설정 **동적 멤버 자격 사용** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="1d7c1-161">그룹 toocontrol hello에 대 한 간단한 단일 규칙을 설정 합니다.이 그룹 기능에 대 한 동적 멤버 자격입니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="1d7c1-162">있는지 hello 확인 **사용자 추가 위치** 옵션을 선택 하 고 (예를 들어, 부서, 직책 등), hello 목록에서 사용자 속성을 선택 합니다</span><span class="sxs-lookup"><span data-stu-id="1d7c1-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="1d7c1-163">그런 다음, 조건(같지 않음, 같음, 다음으로 시작 안 함, 다음으로 시작, 포함 안 함, 포함, 일치하지 않음, 일치)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="1d7c1-164">Hello 선택한 사용자 속성에 대 한 비교 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="1d7c1-165">방법에 대 한 toolearn toocreate *고급* 규칙 (여러 비교를 포함할 수 있는 규칙) 동적 그룹 멤버 자격에 대 한 참조 [toocreate 특성을 사용 하 여 고급 규칙](active-directory-accessmanagement-groups-with-advanced-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="1d7c1-166">추가 정보</span><span class="sxs-lookup"><span data-stu-id="1d7c1-166">Additional information</span></span>
<span data-ttu-id="1d7c1-167">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d7c1-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="1d7c1-168">Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리</span><span class="sxs-lookup"><span data-stu-id="1d7c1-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="1d7c1-169">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="1d7c1-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="1d7c1-170">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="1d7c1-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="1d7c1-171">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="1d7c1-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="1d7c1-172">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="1d7c1-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
