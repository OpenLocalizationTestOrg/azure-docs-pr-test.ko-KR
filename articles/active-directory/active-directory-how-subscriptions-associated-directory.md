---
title: "Azure 구독과 Azure Active Directory의 연관 관계 | Microsoft Docs"
description: "Microsoft Azure 로그인 및 Azure 구독과 Azure Active Directory 간의 관계와 같은 관련 문제입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 283c9903501a1e497e4dde81146d21edb869e9e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a><span data-ttu-id="e9b12-103">Azure 구독과 Azure Active Directory의 연관 관계</span><span class="sxs-lookup"><span data-stu-id="e9b12-103">How Azure subscriptions are associated with Azure Active Directory</span></span>
<span data-ttu-id="e9b12-104">이 문서에서는 Azure 구독과 Azure Active Directory(Azure AD) 간의 관계와 같은 정보 및 Azure AD 디렉터리에 기존 구독을 추가하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-104">This article covers information about the relationship between an Azure subscription and Azure Active Directory (Azure AD), and how to add an existing subscription to your Azure AD directory.</span></span>

## <a name="your-azure-subscriptions-relationship-to-azure-ad"></a><span data-ttu-id="e9b12-105">Azure AD에 대한 Azure 구독의 관계</span><span class="sxs-lookup"><span data-stu-id="e9b12-105">Your Azure subscription's relationship to Azure AD</span></span>
<span data-ttu-id="e9b12-106">Azure 구독은 Azure AD와 트러스트 관계가 있습니다. 즉, 사용자, 서비스 및 장치를 인증하는 디렉터리를 신뢰합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-106">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts the directory to authenticate users, services, and devices.</span></span> <span data-ttu-id="e9b12-107">여러 구독에서 동일한 디렉터리를 신뢰할 수 있지만 각 구독은 하나의 디렉터리만 신뢰합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-107">Multiple subscriptions can trust the same directory, but each subscription trusts only one directory.</span></span> 

<span data-ttu-id="e9b12-108">구독이 디렉터리와 갖는 트러스트 관계는 구독이 Azure의 다른 리소스(웹 사이트, 데이터베이스 등)와 갖는 관계와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-108">The trust relationship that a subscription has with a directory is unlike the relationship that it has with other resources in Azure (websites, databases, and so on).</span></span> <span data-ttu-id="e9b12-109">구독이 만료되면 구독과 연결된 다른 리소스에 대한 액세스도 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-109">If a subscription expires, access to the other resources associated with the subscription also stops.</span></span> <span data-ttu-id="e9b12-110">하지만 Azure AD 디렉터리는 Azure에 남아 있으며 해당 디렉터리와 다른 구독을 연결하고 새 구독을 사용하여 디렉터리를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-110">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage the directory using the new subscription.</span></span>

![구독과 다이어그램의 연관 관계](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

<span data-ttu-id="e9b12-112">모든 사용자는 자신을 인증하는 단일 홈 디렉터리를 가지고 있지만 다른 디렉터리의 게스트가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-112">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span></span> <span data-ttu-id="e9b12-113">Azure AD에서 사용자 계정이 멤버 또는 게스트인 디렉터리만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-113">In Azure AD, you can see the directories of which your user account is a member or guest.</span></span>

## <a name="azure-ad-and-cloud-service-subscriptions"></a><span data-ttu-id="e9b12-114">Azure AD 및 클라우드 서비스 구독</span><span class="sxs-lookup"><span data-stu-id="e9b12-114">Azure AD and cloud service subscriptions</span></span>
<span data-ttu-id="e9b12-115">Azure AD는 다음을 포함하여 대부분의 Microsoft 클라우드 서비스 뒤에 핵심 디렉터리 및 ID 관리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-115">Azure AD provides the core directory and identity management capabilities behind most of Microsoft’s cloud services, including:</span></span>

* <span data-ttu-id="e9b12-116">Azure</span><span class="sxs-lookup"><span data-stu-id="e9b12-116">Azure</span></span>
* <span data-ttu-id="e9b12-117">Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="e9b12-117">Microsoft Office 365</span></span>
* <span data-ttu-id="e9b12-118">Microsoft Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="e9b12-118">Microsoft Dynamics CRM Online</span></span>
* <span data-ttu-id="e9b12-119">Microsoft Intune</span><span class="sxs-lookup"><span data-stu-id="e9b12-119">Microsoft Intune</span></span>

<span data-ttu-id="e9b12-120">이러한 Microsoft 클라우드 서비스 중 하나에 등록하면 Azure AD 서비스를 체험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-120">You get the Azure AD service free when you sign up for any of these Microsoft cloud services.</span></span> <span data-ttu-id="e9b12-121">Azure AD 디렉터리에 Azure 구독을 더 추가하려는 경우 Microsoft 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-121">If you want to add an additional Azure subscription to an Azure AD directory, you must be signed in with a Microsoft account.</span></span> <span data-ttu-id="e9b12-122">회사 또는 학교 계정으로 Azure에 로그인한 경우 회사 또는 학교 계정을 Azure에서 직접 인증할 수 없기 때문에 기존 디렉터리에 Azure 구독을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-122">If you sign in to Azure with a work or school account, you can't add an Azure subscription to an existing directory because your work or school account can't be authenticated directly by Azure.</span></span> 

## <a name="to-add-an-existing-subscription-to-your-azure-ad-directory"></a><span data-ttu-id="e9b12-123">Azure AD 디렉터리에 기존 구독을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="e9b12-123">To add an existing subscription to your Azure AD directory</span></span>
<span data-ttu-id="e9b12-124">구독이 연결된 현재 디렉터리 및 추가하려는 디렉터리에 존재하는 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-124">You must sign in with an account that exists in both the current directory with which the subscription is associated and in the directory you want to add it to.</span></span> 

1. <span data-ttu-id="e9b12-125">소유권을 이전하려는 구독의 계정 관리자인 계정을 사용하여 [Azure 계정 센터](https://account.windowsazure.com/Home/Index)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-125">Sign in to the [Azure Account Center](https://account.windowsazure.com/Home/Index) with an account that is the Account Administrator of the subscription whose ownership you want to transfer.</span></span>
2. <span data-ttu-id="e9b12-126">구독 소유자로 선택한 사용자가가 대상 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-126">Ensure that the user who you want to be the subscription owner is in the targeted directory.</span></span>
3. <span data-ttu-id="e9b12-127">**구독 이전**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-127">Click **Transfer subscription**.</span></span>
4. <span data-ttu-id="e9b12-128">받는 사람을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-128">Specify the recipient.</span></span> <span data-ttu-id="e9b12-129">받는 사람은 수락 링크가 포함된 전자 메일을 자동으로 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-129">The recipient automatically gets an email with an acceptance link.</span></span>
5. <span data-ttu-id="e9b12-130">받는 사람은 링크를 클릭하고 지불 정보 입력 등의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-130">The recipient clicks the link and follows the instructions, including entering their payment information.</span></span> <span data-ttu-id="e9b12-131">받는 사람이 성공하면 구독이 이전됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-131">When the recipient succeeds, the subscription is transferred.</span></span> 
6. <span data-ttu-id="e9b12-132">구독의 기본 디렉터리는 해당 사용자가 있는 디렉터리로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-132">The default directory of the subscription is changed to the directory that the user is in.</span></span>


## <a name="suggestions-to-manage-both-a-subscription-and-a-directory"></a><span data-ttu-id="e9b12-133">구독 및 디렉터리를 모두 관리하기 위한 제안</span><span class="sxs-lookup"><span data-stu-id="e9b12-133">Suggestions to manage both a subscription and a directory</span></span>
<span data-ttu-id="e9b12-134">Azure 구독의 관리 역할은 Azure 구독에 연결된 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-134">The administrative roles for an Azure subscription manage resources tied to the Azure subscription.</span></span> <span data-ttu-id="e9b12-135">이 섹션에서는 Azure 구독 관리자와 Azure AD 디렉터리 관리자 간의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-135">This section explains the differences between Azure subscription admins and Azure AD directory admins.</span></span> <span data-ttu-id="e9b12-136">관리자 역할 및 구독을 관리하기 위해 해당 역할을사용하는 다른 제안은 [Azure Active Directory의 관리자 역할 할당](active-directory-assign-admin-roles.md)에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-136">Administrative roles and other suggestions for using them to manage your subscription are covered at [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="e9b12-137">등록할 때 기본적으로 서비스 관리자 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-137">By default, you are assigned the Service Administrator role when you sign up.</span></span> <span data-ttu-id="e9b12-138">다른 사용자가 동일한 구독을 사용하여 로그인하고 서비스에 액세스해야 하는 경우 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-138">If others need to sign in and access services using the same subscription, you can add them as co-administrators.</span></span> 

<span data-ttu-id="e9b12-139">Azure AD는 디렉터리 및 ID 관련 기능을 관리하는 다른 관리 역할 집합을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-139">Azure AD has a different set of administrative roles to manage the directory and identity-related features.</span></span> <span data-ttu-id="e9b12-140">예를 들어 디렉터리의 전역 관리자는 디렉터리에 사용자 및 그룹을 추가하거나 사용자에 대해 다단계 인증을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-140">For example, the global administrator of a directory can add users and groups to the directory, or require multifactor authentication for users.</span></span> <span data-ttu-id="e9b12-141">디렉터리를 만든 사용자는 전역 관리자 역할에 할당되어 다른 사용자에게 관리자 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-141">A user who creates a directory is assigned to the global administrator role and they can assign administrative roles to other users.</span></span> <span data-ttu-id="e9b12-142">또한 Azure AD 관리 역할은 Office 365 및 Microsoft Intune과 같은 다른 서비스에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-142">Azure AD administrative roles are also used by other services such as Office 365 and Microsoft Intune.</span></span> 

<span data-ttu-id="e9b12-143">Azure 구독 관리자와 Azure AD 디렉터리 관리자는 서로 다른 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-143">Azure subscription admins and Azure AD directory admins are two separate roles.</span></span> 
* <span data-ttu-id="e9b12-144">Azure 구독 관리자는 Azure에서 리소스를 관리하고 Azure Portal에서 Azure AD를 사용할 수 있습니다(Azure Portal 자체가 Azure 리소스이기 때문).</span><span class="sxs-lookup"><span data-stu-id="e9b12-144">Azure subscription admins can manage resources in Azure and can use Azure AD in the Azure portal (because the Azure portal itself is an Azure resource).</span></span> 
* <span data-ttu-id="e9b12-145">디렉터리 관리자는 Azure AD 디렉터리에서만 속성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-145">Directory admins can manage properties only in the Azure AD directory.</span></span>

<span data-ttu-id="e9b12-146">역할을 모두 담당할 수 있지만 그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-146">A person can be in both roles but it isn’t required.</span></span> <span data-ttu-id="e9b12-147">디렉터리 전역 관리자는 Azure 구독의 서비스 관리자 또는 공동 관리자로 할당될 수 없고 반대도 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-147">A directory global administrator might not be assigned as service administrator or co-administrator of an Azure subscription, or vice versa.</span></span> <span data-ttu-id="e9b12-148">구독 관리자가 아니어도 사용자는 Azure Portal에 로그인할 수 있지만 포털에서 해당 구독의 디렉터리를 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-148">Without being an administrator of the subscription, the user can sign in to the Azure portal, but can't manage the directories for that subscription in the portal.</span></span> <span data-ttu-id="e9b12-149">그러나 이 사용자는 Azure AD PowerShell 또는 Office 365 관리 센터와 같은 다른 도구를 사용하여 디렉터리를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9b12-149">However, this user can manage directories using other tools such as Azure AD PowerShell or the Office 365 Admin Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9b12-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9b12-150">Next steps</span></span>
* <span data-ttu-id="e9b12-151">Azure 구독의 관리자를 변경하는 방법을 자세히 알아보려면 [다른 계정에 Azure 구독의 소유권 이전](../billing/billing-subscription-transfer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9b12-151">To learn more about how to change administrators for an Azure subscription, see [Transfer ownership of an Azure subscription to another account](../billing/billing-subscription-transfer.md)</span></span>
* <span data-ttu-id="e9b12-152">Microsoft Azure에서 리소스 액세스를 제어하는 방법에 대해 자세히 알아보려면 [Azure의 리소스 액세스 이해](active-directory-understanding-resource-access.md)</span><span class="sxs-lookup"><span data-stu-id="e9b12-152">To learn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](active-directory-understanding-resource-access.md)</span></span>
* <span data-ttu-id="e9b12-153">Azure AD에서 역할을 할당하는 방법에 대한 자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e9b12-153">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
