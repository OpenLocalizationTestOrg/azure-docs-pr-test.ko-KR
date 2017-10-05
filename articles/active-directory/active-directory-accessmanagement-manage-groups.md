---
title: "Azure Active Directory에서 그룹 관리 | Microsoft Docs"
description: "Azure Active Directory를 사용하여 Azure 사용자를 관리하기 위해 그룹을 만들고 관리하는 방법."
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
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="bde52-103">Azure Active Directory에서 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="bde52-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bde52-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="bde52-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="bde52-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="bde52-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="bde52-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bde52-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="bde52-107">Azure AD(Azure Active Directory) 사용자 관리의 주요 기능 중 하나는 사용자 그룹을 만드는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="bde52-108">그룹을 사용하여 한 번에 많은 사용자에게 라이선스 또는 사용 권한을 할당하는 등 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="bde52-109">그룹을 사용하여 액세스 권한을 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="bde52-110">디렉터리의 개체와 같은 리소스</span><span class="sxs-lookup"><span data-stu-id="bde52-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="bde52-111">SaaS 응용 프로그램, Azure 서비스, SharePoint 사이트 또는 온-프레미스 리소스와 같은 디렉터리 외부에 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="bde52-112">또한 리소스 소유자는 다른 사람이 소유한 Azure AD 그룹에 리소스에 대한 액세스를 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="bde52-113">이 할당은 해당 그룹의 멤버에게 리소스에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="bde52-114">그런 다음 그룹의 소유자는 그룹의 멤버 자격을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="bde52-115">실질적으로 리소스 소유자는 그룹의 소유자에게 권한을 위임하여 해당 리소스에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bde52-116">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="bde52-117">Azure AD 관리 센터에서 그룹을 관리하는 방법은 [Azure Active Directory에서 그룹 만들기 및 멤버 추가](active-directory-groups-create-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bde52-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="bde52-118">그룹을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="bde52-118">How do I create a group?</span></span>
<span data-ttu-id="bde52-119">조직에서 구독하는 서비스에 따라 다음 중 하나를 사용하여 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="bde52-120">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="bde52-120">the Azure classic portal</span></span>
* <span data-ttu-id="bde52-121">Office 365 계정 포털</span><span class="sxs-lookup"><span data-stu-id="bde52-121">the Office 365 account portal</span></span>
* <span data-ttu-id="bde52-122">Windows Intune 계정 포털</span><span class="sxs-lookup"><span data-stu-id="bde52-122">the Windows Intune account portal</span></span>

<span data-ttu-id="bde52-123">Azure 클래식 포털에서 수행하는 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="bde52-124">비 Azure 포털을 사용하여 Azure AD를 관리하는 방법에 대한 자세한 내용은 [Azure AD 디렉터리 관리](active-directory-administer.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bde52-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="bde52-125">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="bde52-126">**그룹** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="bde52-127">**그룹 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="bde52-128">**그룹 추가** 창에서 그룹의 이름 및 설명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="bde52-129">보안 그룹에서 개별 사용자를 추가하거나 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="bde52-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="bde52-130">**그룹에 개별 사용자를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="bde52-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="bde52-131">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="bde52-132">**그룹** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="bde52-133">구성원을 추가할 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="bde52-134">표시되지 않은 경우 선택된 그룹의 **멤버** 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="bde52-135">**멤버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="bde52-136">**멤버 추가** 페이지에서 이 그룹의 멤버로 추가할 사용자 또는 그룹의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="bde52-137">이 이름이 **선택한** 창에 추가되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="bde52-138">**그룹에서 개별 사용자를 제거하려면**</span><span class="sxs-lookup"><span data-stu-id="bde52-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="bde52-139">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="bde52-140">**그룹** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="bde52-141">멤버를 제거할 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="bde52-142">**멤버** 탭을 선택하고 이 그룹에서 제거할 멤버의 이름을 선택한 다음 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="bde52-143">프롬프트에서 이 멤버를 그룹에서 제거한다고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="bde52-144">그룹의 멤버 자격을 동적으로 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="bde52-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="bde52-145">Azure AD에서는 간단한 규칙을 매우 쉽게 설정하여 그룹의 멤버가 될 사용자를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="bde52-146">간단한 규칙에서 단일 비교를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="bde52-147">예를 들어 그룹을 SaaS 응용 프로그램에 할당하면 규칙을 설정하여 "판매 담당자"의 직위를 가진 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="bde52-148">이 규칙은 디렉터리에서 해당 직위를 가진 모든 사용자에게 SaaS 응용 프로그램에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="bde52-149">사용자의 특성이 변경될 때 사용자의 특성 변경 내용이 그룹 추가 또는 제거를 트리거할지를 확인하기 위해 시스템은 디렉터리에서 모든 동적 그룹 규칙을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="bde52-150">사용자가 그룹에 대한 규칙을 만족하면 해당 그룹에 대한 구성원으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="bde52-151">구성원인 그룹의 규칙을 더 이상 만족하지 않는 경우 해당 그룹의 구성원에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="bde52-152">보안 그룹 또는 Office 365 그룹에서 동적 멤버 자격에 대한 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="bde52-153">중첩 그룹 구성원은 현재 응용 프로그램에 대한 그룹 기반 할당에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="bde52-154">그룹의 동적 멤버 자격에는 할당될 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="bde52-155">그룹의 규칙을 관리하는 관리자</span><span class="sxs-lookup"><span data-stu-id="bde52-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="bde52-156">그룹의 모든 멤버</span><span class="sxs-lookup"><span data-stu-id="bde52-156">All members of the group</span></span>
>
>

<span data-ttu-id="bde52-157">**그룹에 동적 멤버 자격을 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="bde52-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="bde52-158">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="bde52-159">**그룹** 탭을 선택하고 편집할 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="bde52-160">**구성** 탭을 선택한 다음 **동적 멤버 자격 사용**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="bde52-161">그룹에 간단한 단일 규칙을 설정하여 이 그룹에 대한 동적 멤버 자격 작동 방식을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="bde52-162">**사용자 추가 위치** 옵션이 선택되어 있는지 확인하고 목록에서 사용자 속성(예: department, jobTitle 등)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="bde52-163">그런 다음, 조건(같지 않음, 같음, 다음으로 시작 안 함, 다음으로 시작, 포함 안 함, 포함, 일치하지 않음, 일치)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="bde52-164">선택한 사용자 속성에 대한 비교 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="bde52-165">동적 그룹 멤버 자격에 대한 *고급* 규칙(여러 비교를 포함할 수 있는 규칙)을 만드는 방법에 대해 자세히 알아보려면 [특성을 사용하여 고급 규칙 만들기](active-directory-accessmanagement-groups-with-advanced-rules.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bde52-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="bde52-166">추가 정보</span><span class="sxs-lookup"><span data-stu-id="bde52-166">Additional information</span></span>
<span data-ttu-id="bde52-167">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bde52-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="bde52-168">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="bde52-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="bde52-169">그룹 설정을 구성하는 Azure Active Directory cmdlet</span><span class="sxs-lookup"><span data-stu-id="bde52-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="bde52-170">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="bde52-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="bde52-171">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="bde52-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="bde52-172">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="bde52-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
