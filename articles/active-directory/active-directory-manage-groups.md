---
title: "Azure Active Directory에서 그룹을 사용하여 리소스에 대한 액세스 관리 | Microsoft Docs"
description: "온-프레미스 및 클라우드 응용 프로그램 및 리소스에 대한 사용자 액세스 관리를 위해 Azure Active Directory의 그룹을 사용하는 방법입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cd8125eda7643f0b190d35cbb89edf8b7b4eca30
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-access-to-resources-with-azure-active-directory-groups"></a><span data-ttu-id="7ae0a-103">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="7ae0a-103">Manage access to resources with Azure Active Directory groups</span></span>
<span data-ttu-id="7ae0a-104">Azure Active Directory(Azure AD)는 Office 365와 같은 Microsoft 온라인 서비스 및 수많은 비 Microsoft SaaS 응용 프로그램을 포함하여 온-프레미스와 클라우드 응용 프로그램 및 리소스에 대한 액세스를 관리하는 강력한 기능을 제공하는 포괄적인 ID 및 액세스 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-104">Azure Active Directory (Azure AD) is a comprehensive identity and access management solution that provides a robust set of capabilities to manage access to on-premises and cloud applications and resources including Microsoft online services like Office 365 and a world of non-Microsoft SaaS applications.</span></span> <span data-ttu-id="7ae0a-105">이 문서에서는 개요를 제공하지만 지금 바로 Azure AD 그룹 사용을 시작하려는 경우 [Azure AD에서 보안 그룹 관리](active-directory-accessmanagement-manage-groups.md)의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-105">This article provides an overview, but if you want to start using Azure AD groups right now, follow the instructions in [Managing security groups in Azure AD](active-directory-accessmanagement-manage-groups.md).</span></span> <span data-ttu-id="7ae0a-106">PowerShell을 사용하여 Azure Active directory에서 그룹을 관리하는 방법을 보려면 자세한 내용은 [그룹 관리를 위한 Azure Active Directory cmdlet](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-106">If you want to see how you can use PowerShell to manage groups in Azure Active directory you can read more in [Azure Active Directory cmdlets for group management](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7ae0a-107">Azure Active Directory를 사용하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-107">To use Azure Active Directory, you need an Azure account.</span></span> <span data-ttu-id="7ae0a-108">계정이 없으면 [무료 Azure 계정을 등록](https://azure.microsoft.com/pricing/free-trial/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-108">If you don't have an account, you can [sign up for a free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
>
>

<span data-ttu-id="7ae0a-109">Azure AD 내에서 주요 기능 중 하나는 리소스에 대한 액세스를 관리하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-109">Within Azure AD, one of the major features is the ability to manage access to resources.</span></span> <span data-ttu-id="7ae0a-110">이러한 리소스는 디렉터리에서 역할을 통해 개체를 관리하는 권한이나 SaaS 응용 프로그램, Azure 서비스 및 SharePoint 사이트 또는 온-프레미스 리소스와 같이 디렉터리 외부에 있는 리소스의 경우처럼 디렉터리의 일부일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-110">These resources can be part of the directory, as in the case of permissions to manage objects through roles in the directory, or resources that are external to the directory, such as SaaS applications, Azure services, and SharePoint sites or on-premises resources.</span></span> <span data-ttu-id="7ae0a-111">다음 네 가지 방법으로 사용자에게 리소스에 대한 액세스 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-111">There are four ways a user can be assigned access rights to a resource:</span></span>

1. <span data-ttu-id="7ae0a-112">직접 할당</span><span class="sxs-lookup"><span data-stu-id="7ae0a-112">Direct assignment</span></span>

    <span data-ttu-id="7ae0a-113">해당 리소스의 소유자가 사용자에게 직접 리소스를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-113">Users can be assigned directly to a resource by the owner of that resource.</span></span>
2. <span data-ttu-id="7ae0a-114">그룹 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="7ae0a-114">Group membership</span></span>

    <span data-ttu-id="7ae0a-115">리소스 소유자가 그룹에 리소스를 지정할 수 있고, 이렇게 함으로써 해당 그룹의 멤버에게 리소스에 대한 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-115">A group can be assigned to a resource by the resource owner, and by doing so, granting the members of that group access to the resource.</span></span> <span data-ttu-id="7ae0a-116">그러면 그룹의 소유자가 그룹의 멤버 자격을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-116">Membership of the group can then be managed by the owner of the group.</span></span> <span data-ttu-id="7ae0a-117">실질적으로 리소스 소유자는 사용자를 해당 리소스에 할당할 권한을 그룹 소유자에게 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-117">Effectively, the resource owner delegates the permission to assign users to their resource to the owner of the group.</span></span>
3. <span data-ttu-id="7ae0a-118">규칙 기반</span><span class="sxs-lookup"><span data-stu-id="7ae0a-118">Rule-based</span></span>

    <span data-ttu-id="7ae0a-119">리소스 소유자는 규칙을 사용하여 어느 사용자에게 리소스에 대한 액세스 권한을 할당해야 하는지를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-119">The resource owner can use a rule to express which users should be assigned access to a resource.</span></span> <span data-ttu-id="7ae0a-120">규칙 결과는 해당 규칙에 사용된 특성 및 특정 사용자에 대한 값에 따라 다르며, 이렇게 함으로써 리소스 소유자는 자신의 리소스에 대한 액세스 관리 권한을 규칙에 사용된 특성에 대한 권한 있는 원본으로 효과적으로 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-120">The outcome of the rule depends on the attributes used in that rule and their values for specific users, and by doing so, the resource owner effectively delegates the right to manage access to their resource to the authoritative source for the attributes that are used in the rule.</span></span> <span data-ttu-id="7ae0a-121">리소스 소유자는 여전히 규칙 자체를 관리하고 해당 리소스에 대한 액세스를 제공하는 특성 및 값을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-121">The resource owner still manages the rule itself and determines which attributes and values provide access to their resource.</span></span>
4. <span data-ttu-id="7ae0a-122">외부 기관</span><span class="sxs-lookup"><span data-stu-id="7ae0a-122">External authority</span></span>

    <span data-ttu-id="7ae0a-123">리소스에 대한 액세스 권한은 외부 소스에서 파생됩니다. 예를 들면 온-프레미스 디렉터리와 같은 권한이 있는 원본이나 WorkDay와 같은 SaaS 앱에서 동기화되는 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-123">The access to a resource is derived from an external source; for example, a group that is synchronized from an authoritative source such as an on-premises directory or a SaaS app such as WorkDay.</span></span> <span data-ttu-id="7ae0a-124">리소스 소유자는 리소스에 대한 액세스 권한을 제공하는 그룹을 할당하고 외부 소스는 그룹의 구성원을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-124">The resource owner assigns the group to provide access to the resource, and the external source manages the members of the group.</span></span>

   ![액세스 관리 다이어그램의 개요](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a><span data-ttu-id="7ae0a-126">액세스 관리를 설명하는 비디오 보기</span><span class="sxs-lookup"><span data-stu-id="7ae0a-126">Watch a video that explains access management</span></span>
<span data-ttu-id="7ae0a-127">이에 대해 자세히 설명하는 짧은 비디오를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-127">You can watch a short video that explains more about this:</span></span>

<span data-ttu-id="7ae0a-128">**Azure AD: 그룹의 동적 멤버 자격 소개**</span><span class="sxs-lookup"><span data-stu-id="7ae0a-128">**Azure AD: Introduction to dynamic membership for groups**</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a><span data-ttu-id="7ae0a-129">Azure Active Directory에서 액세스 관리는 어떻게 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="7ae0a-129">How does access management in Azure Active Directory work?</span></span>
<span data-ttu-id="7ae0a-130">Azure AD의 액세스 관리 솔루션 센터에 보안 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-130">At the center of the Azure AD access management solution is the security group.</span></span> <span data-ttu-id="7ae0a-131">리소스에 대한 액세스 관리에 보안 그룹을 사용하는 것은 잘 알려진 전형적인 예로, 이를 통해 의도한 사용자 그룹에 리소스에 대한 액세스 권한을 제공하는 방법을 유연하고 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-131">Using a security group to manage access to resources is a well-known paradigm, which allows for a flexible and easily understood way to provide access to a resource for the intended group of users.</span></span> <span data-ttu-id="7ae0a-132">리소스 소유자(또는 디렉터리 관리자)는 특정한 액세스 권한을 제공할 그룹을 자신이 소유한 리소스에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-132">The resource owner (or the administrator of the directory) can assign a group to provide a certain access right to the resources they own.</span></span> <span data-ttu-id="7ae0a-133">그룹 구성원에게 액세스 권한이 제공되며, 리소스 소유자는 부서 관리자 또는 기술 지원팀 관리자와 같은 다른 사람에게 그룹 구성원 목록을 관리할 권한을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-133">The members of the group will be provided the access, and the resource owner can delegate the right to manage the members list of a group to someone else, such as a department manager or a helpdesk administrator.</span></span>

![Azure Active Directory 액세스 관리 다이어그램](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

<span data-ttu-id="7ae0a-135">그룹 소유자는 해당 그룹이 셀프 서비스 요청을 이용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-135">The owner of a group can also make that group available for self-service requests.</span></span> <span data-ttu-id="7ae0a-136">이 과정에서 최종 사용자가 그룹을 검색하고 찾을 수 있으며, 참여하도록 요청하여 그룹을 통해 관리되는 리소스에 액세스할 수 있는 권한을 효과적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-136">In doing so, an end user can search for and find the group and make a request to join, effectively seeking permission to access the resources that are managed through the group.</span></span> <span data-ttu-id="7ae0a-137">그룹의 소유자는 참가 요청을 자동으로 승인하거나 그룹 소유자의 승인을 요구하도록 그룹을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-137">The owner of the group can set up the group so that join requests are approved automatically or require approval by the owner of the group.</span></span> <span data-ttu-id="7ae0a-138">사용자가 그룹 가입을 요청하면 가입 요청이 그룹 소유자에게 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-138">When a user makes a request to join a group, the join request is forwarded to the owners of the group.</span></span> <span data-ttu-id="7ae0a-139">소유자 중 한 명이 요청을 승인하면 요청한 사용자에게 알리고 사용자가 그룹에 가입됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-139">If one of the owners approves the request, the requesting user is notified and the user is joined to the group.</span></span> <span data-ttu-id="7ae0a-140">소유자 중 한 명이 요청을 거부하면 요청한 사용자에게 알리지만 사용자가 그룹에 가입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-140">If one of the owners denies the request, the requesting user is notified but not joined to the group.</span></span>

## <a name="getting-started-with-access-management"></a><span data-ttu-id="7ae0a-141">액세스 관리 시작</span><span class="sxs-lookup"><span data-stu-id="7ae0a-141">Getting started with access management</span></span>
<span data-ttu-id="7ae0a-142">시작할 준비가 되셨습니까?</span><span class="sxs-lookup"><span data-stu-id="7ae0a-142">Ready to get started?</span></span> <span data-ttu-id="7ae0a-143">Azure AD 그룹으로 수행할 수 있는 기본 작업 중 일부를 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-143">You should try out some of the basic tasks you can do with Azure AD groups.</span></span> <span data-ttu-id="7ae0a-144">이러한 기능을 사용하여 조직의 다른 리소스에 다른 사용자 그룹에 대한 특별한 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-144">Use these capabilities to provide specialized access to different groups of people for different resources in your organization.</span></span> <span data-ttu-id="7ae0a-145">다음은 기본 첫 단계 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-145">A list of basic first steps are listed below.</span></span>

* [<span data-ttu-id="7ae0a-146">그룹에 대한 동적 구성원을 구성하는 간단한 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="7ae0a-146">Creating a simple rule to configure dynamic memberships for a group</span></span>](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [<span data-ttu-id="7ae0a-147">SaaS 응용 프로그램에 대한 액세스를 관리할 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="7ae0a-147">Using a group to manage access to SaaS applications</span></span>](active-directory-accessmanagement-group-saasapps.md)
* [<span data-ttu-id="7ae0a-148">최종 사용자 셀프서비스에 사용할 수 있는 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="7ae0a-148">Making a group available for end user self-service</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="7ae0a-149">Azure AD Connect를 사용하여 Azure에 온-프레미스 그룹 동기화</span><span class="sxs-lookup"><span data-stu-id="7ae0a-149">Syncing an on-premises group to Azure using Azure AD Connect</span></span>](active-directory-aadconnect.md)
* [<span data-ttu-id="7ae0a-150">그룹에 대한 소유자 관리</span><span class="sxs-lookup"><span data-stu-id="7ae0a-150">Managing owners for a group</span></span>](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a><span data-ttu-id="7ae0a-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ae0a-151">Next steps</span></span>
<span data-ttu-id="7ae0a-152">액세스 관리의 기본 사항을 이해했으므로, 다음은 Azure Active Directory에서 추가 응용 프로그램 및 리소스에 대한 액세스를 관리하는 데 사용할 수 있는 몇 가지 고급 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae0a-152">Now that you have understood the basics of access management, here are some additional advanced capabilities available in Azure Active Directory for managing access to your applications and resources.</span></span>

* [<span data-ttu-id="7ae0a-153">특성을 사용하여 고급 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="7ae0a-153">Using attributes to create advanced rules</span></span>](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [<span data-ttu-id="7ae0a-154">Azure AD의 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="7ae0a-154">Managing security groups in Azure AD</span></span>](active-directory-accessmanagement-manage-groups.md)
* [<span data-ttu-id="7ae0a-155">Azure AD에서 전용 그룹 설정</span><span class="sxs-lookup"><span data-stu-id="7ae0a-155">Setting up dedicated groups in Azure AD</span></span>](active-directory-accessmanagement-dedicated-groups.md)
* [<span data-ttu-id="7ae0a-156">그룹에 대한 그래프 API 참조</span><span class="sxs-lookup"><span data-stu-id="7ae0a-156">Graph API reference for groups</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [<span data-ttu-id="7ae0a-157">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="7ae0a-157">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
