---
title: "Azure Active Directory의 그룹 기반 라이선스란? | Microsoft Docs"
description: "Azure Active Directory 그룹 기반 라이선스, 작동 방법 및 모범 사례에 대한 설명"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/29/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 52dd48ce4e4acaf48f31edc51bbb657f8cd249cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="group-based-licensing-basics-in-azure-active-directory"></a><span data-ttu-id="1b8b7-105">Azure Active Directory에서 그룹 기반 라이선스 기본</span><span class="sxs-lookup"><span data-stu-id="1b8b7-105">Group-based licensing basics in Azure Active Directory</span></span>

<span data-ttu-id="1b8b7-106">Office 365, Enterprise Mobility + Security, Dynamics CRM 및 기타 유사한 제품과 같은 Microsoft 유료 클라우드 서비스를 사용하려면 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-106">Using Microsoft paid cloud services, such as Office 365, Enterprise Mobility + Security, Dynamics CRM, and other similar products, requires licenses.</span></span> <span data-ttu-id="1b8b7-107">이러한 라이선스는 해당 서비스에 액세스해야 하는 각 사용자에게 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-107">These licenses are assigned to each user who needs access to these services.</span></span> <span data-ttu-id="1b8b7-108">라이선스를 관리하기 위해 관리자는 관리 포털(Office 또는 Azure) 및 PowerShell cmdlet 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-108">To manage licenses, administrators use one of the management portals (Office or Azure) and PowerShell cmdlets.</span></span> <span data-ttu-id="1b8b7-109">Azure AD(Azure Active Directory)는 모든 Microsoft 클라우드 서비스에 대한 ID 관리를 지원하는 기본 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-109">Azure Active Directory (Azure AD) is the underlying infrastructure that supports identity management for all Microsoft cloud services.</span></span> <span data-ttu-id="1b8b7-110">Azure AD는 사용자에 대한 라이선스 할당 상태에 대한 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-110">Azure AD stores information about license assignment states for users.</span></span>

<span data-ttu-id="1b8b7-111">지금까지 개별 사용자 수준에서만 라이선스를 할당할 수 있었기 때문에 대규모 관리가 어려워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-111">Until now, licenses could only be assigned at the individual user level, which can make large-scale management difficult.</span></span> <span data-ttu-id="1b8b7-112">예를 들어 조직이나 부서에 가입하거나 탈퇴하는 사용자와 같이 조직의 변경 내용에 따라 사용자 라이선스를 추가하거나 제거하려면 관리자는 종종 복잡한 PowerShell 스크립트를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-112">For example, to add or remove user licenses based on organizational changes, such as users joining or leaving the organization or a department, an administrator often must write a complex PowerShell script.</span></span> <span data-ttu-id="1b8b7-113">이 스크립트는 클라우드 서비스를 개별적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-113">This script makes individual calls to the cloud service.</span></span>

<span data-ttu-id="1b8b7-114">이러한 문제를 해결하기 위해 이제는 Azure AD에 그룹 기반 라이선스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-114">To address those challenges, Azure AD now includes group-based licensing.</span></span> <span data-ttu-id="1b8b7-115">그룹에 제품 라이선스를 하나 이상 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-115">You can assign one or more product licenses to a group.</span></span> <span data-ttu-id="1b8b7-116">Azure AD는 그룹의 모든 멤버에게 라이선스가 할당되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-116">Azure AD ensures that the licenses are assigned to all members of the group.</span></span> <span data-ttu-id="1b8b7-117">그룹에 참가하는 새 멤버에게는 적절한 라이선스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-117">Any new members who join the group are assigned the appropriate licenses.</span></span> <span data-ttu-id="1b8b7-118">멤버가 그룹을 떠날 때 해당 라이선스가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-118">When they leave the group, those licenses are removed.</span></span> <span data-ttu-id="1b8b7-119">이렇게 하면 사용자 기준으로 조직 및 부서 구조에 변경 내용을 반영하기 위해 PowerShell을 통해 라이선스 관리를 자동화할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-119">This eliminates the need for automating license management via PowerShell to reflect changes in the organization and departmental structure on a per-user basis.</span></span>

## <a name="features"></a><span data-ttu-id="1b8b7-120">기능</span><span class="sxs-lookup"><span data-stu-id="1b8b7-120">Features</span></span>

<span data-ttu-id="1b8b7-121">다음은 그룹 기반 라이선스 기능의 주요 특징입니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-121">Here are the main features of group-based licensing:</span></span>

- <span data-ttu-id="1b8b7-122">Azure AD의 보안 그룹에 라이선스를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-122">Licenses can be assigned to any security group in Azure AD.</span></span> <span data-ttu-id="1b8b7-123">Azure AD Connect를 사용하여 보안 그룹을 온-프레미스에서 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-123">Security groups can be synced on-premises, by using Azure AD Connect.</span></span> <span data-ttu-id="1b8b7-124">또한 Azure AD(클라우드 전용 그룹이라고도 함)에서 보안 그룹을 직접 만들거나 Azure AD 동적 그룹 기능을 통해 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-124">You can also create security groups directly in Azure AD (also called cloud-only groups), or automatically via the Azure AD dynamic group feature.</span></span>

- <span data-ttu-id="1b8b7-125">그룹에 제품 라이선스를 할당하면 관리자는 제품에서 서비스 계획을 하나 이상 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-125">When a product license is assigned to a group, the administrator can disable one or more service plans in the product.</span></span> <span data-ttu-id="1b8b7-126">일반적으로 조직에서 제품에 포함된 서비스를 아직 사용할 준비가 되지 않은 경우에 이 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-126">Typically, this is done when the organization is not yet ready to start using a service included in a product.</span></span> <span data-ttu-id="1b8b7-127">예를 들어 관리자는 Office 365를 부서에 할당할 수 있지만 Yammer 서비스를 일시적으로 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-127">For example, the administrator might assign Office 365 to a department, but temporarily disable the Yammer service.</span></span>

- <span data-ttu-id="1b8b7-128">사용자 수준 라이선스를 필요로 하는 모든 Microsoft Clouds Services는 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-128">All Microsoft cloud services that require user-level licensing are supported.</span></span> <span data-ttu-id="1b8b7-129">여기에는 모든 Office 365 제품, Enterprise Mobility + Security 및 Dynamics CRM이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-129">This includes all Office 365 products, Enterprise Mobility + Security, and Dynamics CRM.</span></span>

- <span data-ttu-id="1b8b7-130">그룹 기반 라이선스는 현재 [Azure Portal](https://portal.azure.com)을 통해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-130">Group-based licensing is currently available only through [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1b8b7-131">Office 365 포털과 같이 주로 사용자 및 그룹 관리를 위해 다른 관리 포털을 사용하는 경우에 이 작업을 계속 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-131">If you primarily use other management portals for user and group management, such as the Office 365 portal, you can continue to do so.</span></span> <span data-ttu-id="1b8b7-132">그러나 그룹 수준에서 라이선스를 관리하려면 Azure Portal을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-132">But you should use the Azure portal to manage licenses at group level.</span></span>

- <span data-ttu-id="1b8b7-133">Azure AD는 그룹 멤버 자격 변경으로 인해 발생하는 라이선스 수정을 자동으로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-133">Azure AD automatically manages license modifications that result from group membership changes.</span></span> <span data-ttu-id="1b8b7-134">일반적으로 라이선스 수정은 멤버 자격 변경 후 수분 내에 효과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-134">Typically, license modifications are effective within minutes of a membership change.</span></span>

- <span data-ttu-id="1b8b7-135">사용자는 지정된 라이선스 정책을 사용하는 여러 그룹의 멤버가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-135">A user can be a member of multiple groups with license policies specified.</span></span> <span data-ttu-id="1b8b7-136">또한 사용자는 그룹 외부에서 직접 할당된 일부 라이선스를 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-136">A user can also have some licenses that were directly assigned, outside of any groups.</span></span> <span data-ttu-id="1b8b7-137">결과 사용자 상태는 모든 할당된 제품 및 서비스 라이선스의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-137">The resulting user state is a combination of all assigned product and service licenses.</span></span>

- <span data-ttu-id="1b8b7-138">어떤 경우에는 사용자에게 라이선스를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-138">In some cases, licenses cannot be assigned to a user.</span></span> <span data-ttu-id="1b8b7-139">예를 들어 테넌트에서 사용할 수 있는 라이선스가 충분하지 않거나 충돌하는 서비스를 동시에 할당했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-139">For example, there might not be enough available licenses in the tenant, or conflicting services might have been assigned at the same time.</span></span> <span data-ttu-id="1b8b7-140">관리자는 Azure AD가 그룹 라이선스를 완전하게 처리할 수 없는 사용자에 대한 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-140">Administrators have access to information about users for whom Azure AD could not fully process group licenses.</span></span> <span data-ttu-id="1b8b7-141">그런 다음 해당 정보에 따라 수정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-141">They can then take corrective action based on that information.</span></span>

- <span data-ttu-id="1b8b7-142">공개 미리 보기 동안 그룹 기반 라이선스 관리를 사용하려면 Azure AD Basic 또는 Premium Edition에 대한 유료 또는 평가판 구독이 테넌트에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-142">During public preview, a paid or trial subscription for Azure AD Basic or Premium editions is required in the tenant to use group-based license management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b8b7-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b8b7-143">Next steps</span></span>

<span data-ttu-id="1b8b7-144">그룹 기반 라이선스를 통한 라이선스 관리에 대한 기타 시나리오에 대해 자세히 알아보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b8b7-144">To learn more about other scenarios for license management through group-based licensing, see:</span></span>

* [<span data-ttu-id="1b8b7-145">Azure Active Directory에서 라이선스 시작</span><span class="sxs-lookup"><span data-stu-id="1b8b7-145">Get started with licenses in Azure Active Directory</span></span>](active-directory-licensing-get-started-azure-portal.md)
* [<span data-ttu-id="1b8b7-146">Azure Active Directory에서 그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="1b8b7-146">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="1b8b7-147">Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="1b8b7-147">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="1b8b7-148">Azure Active Directory에서 개별 라이선스 사용자를 그룹 기반 라이선스로 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="1b8b7-148">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="1b8b7-149">Azure Active Directory 그룹 기반 라이선스 추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="1b8b7-149">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
