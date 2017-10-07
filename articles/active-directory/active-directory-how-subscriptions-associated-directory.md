---
title: "aaaHow Azure 구독은 Azure Active Directory와 연결 | Microsoft Docs"
description: "TooMicrosoft Azure에에서 로그인 하 고 관련 Azure 구독과 Azure Active Directory 간에 hello 관계와 같은 문제입니다."
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
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a><span data-ttu-id="5f482-103">Azure 구독과 Azure Active Directory의 연관 관계</span><span class="sxs-lookup"><span data-stu-id="5f482-103">How Azure subscriptions are associated with Azure Active Directory</span></span>
<span data-ttu-id="5f482-104">이 문서에서는 Azure 구독과 Azure Active Directory (Azure AD) 간의 hello 관계에 대 한 정보 및 방법 tooadd 기존 구독 tooyour Azure AD 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-104">This article covers information about hello relationship between an Azure subscription and Azure Active Directory (Azure AD), and how tooadd an existing subscription tooyour Azure AD directory.</span></span>

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a><span data-ttu-id="5f482-105">Azure 구독 관계 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="5f482-105">Your Azure subscription's relationship tooAzure AD</span></span>
<span data-ttu-id="5f482-106">Azure 구독에 hello directory tooauthenticate 사용자, 서비스 및 장치를 트러스트 하는 Azure AD와의 신뢰 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-106">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts hello directory tooauthenticate users, services, and devices.</span></span> <span data-ttu-id="5f482-107">여러 구독 hello 신뢰할 수 있는 동일한 디렉터리 하지만 각 구독 하나의 디렉터리만 트러스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-107">Multiple subscriptions can trust hello same directory, but each subscription trusts only one directory.</span></span> 

<span data-ttu-id="5f482-108">구독 디렉터리 개가 있는 hello 트러스트 관계 (웹 사이트, 데이터베이스 및 등)는 Azure의 다른 리소스와 있는 hello 관계와 달리입니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-108">hello trust relationship that a subscription has with a directory is unlike hello relationship that it has with other resources in Azure (websites, databases, and so on).</span></span> <span data-ttu-id="5f482-109">구독이 만료 되는 경우 액세스 toohello hello 구독과 연결 된 다른 리소스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-109">If a subscription expires, access toohello other resources associated with hello subscription also stops.</span></span> <span data-ttu-id="5f482-110">하지만 Azure에서 Azure AD 디렉터리 남아 있으며 해당 디렉터리와는 다른 구독을 연결 하 고 새 구독 hello를 사용 하 여 hello 디렉터리를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-110">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage hello directory using hello new subscription.</span></span>

![구독과 다이어그램의 연관 관계](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

<span data-ttu-id="5f482-112">모든 사용자는 자신을 인증하는 단일 홈 디렉터리를 가지고 있지만 다른 디렉터리의 게스트가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-112">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span></span> <span data-ttu-id="5f482-113">Azure ad에서는 사용자 계정에는 멤버 또는 게스트 hello 디렉터리를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-113">In Azure AD, you can see hello directories of which your user account is a member or guest.</span></span>

## <a name="azure-ad-and-cloud-service-subscriptions"></a><span data-ttu-id="5f482-114">Azure AD 및 클라우드 서비스 구독</span><span class="sxs-lookup"><span data-stu-id="5f482-114">Azure AD and cloud service subscriptions</span></span>
<span data-ttu-id="5f482-115">Azure AD hello 핵심 디렉터리 및 id 뒤에 있는 대부분의 Microsoft 클라우드 서비스를 포함 하 여 관리 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-115">Azure AD provides hello core directory and identity management capabilities behind most of Microsoft’s cloud services, including:</span></span>

* <span data-ttu-id="5f482-116">Azure</span><span class="sxs-lookup"><span data-stu-id="5f482-116">Azure</span></span>
* <span data-ttu-id="5f482-117">Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="5f482-117">Microsoft Office 365</span></span>
* <span data-ttu-id="5f482-118">Microsoft Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="5f482-118">Microsoft Dynamics CRM Online</span></span>
* <span data-ttu-id="5f482-119">Microsoft Intune</span><span class="sxs-lookup"><span data-stu-id="5f482-119">Microsoft Intune</span></span>

<span data-ttu-id="5f482-120">이 Microsoft 클라우드 서비스에 등록할 때 hello를 무료 Azure AD 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-120">You get hello Azure AD service free when you sign up for any of these Microsoft cloud services.</span></span> <span data-ttu-id="5f482-121">추가 Azure 구독 tooan Azure AD 디렉터리 tooadd 하려는 경우 Microsoft 계정으로 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-121">If you want tooadd an additional Azure subscription tooan Azure AD directory, you must be signed in with a Microsoft account.</span></span> <span data-ttu-id="5f482-122">또는 학교 계정을, tooAzure 저작물에 로그인 하는 경우에 회사 또는 학교 계정을 Azure에서 직접 인증할 수 없어서 Azure 구독 tooan 기존 디렉터리를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-122">If you sign in tooAzure with a work or school account, you can't add an Azure subscription tooan existing directory because your work or school account can't be authenticated directly by Azure.</span></span> 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a><span data-ttu-id="5f482-123">tooadd 기존 구독 tooyour Azure AD 디렉터리</span><span class="sxs-lookup"><span data-stu-id="5f482-123">tooadd an existing subscription tooyour Azure AD directory</span></span>
<span data-ttu-id="5f482-124">hello 구독이 연결 된 두 hello 현재 디렉터리에 있는 계정으로 로그인 해야 하 고 tooadd hello 디렉터리에서 원하는 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-124">You must sign in with an account that exists in both hello current directory with which hello subscription is associated and in hello directory you want tooadd it to.</span></span> 

1. <span data-ttu-id="5f482-125">Toohello 로그인 [Azure 계정 센터](https://account.windowsazure.com/Home/Index) 원하는 tootransfer는 hello hello 구독의 계정 관리자에 소유권 있는 계정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-125">Sign in toohello [Azure Account Center](https://account.windowsazure.com/Home/Index) with an account that is hello Account Administrator of hello subscription whose ownership you want tootransfer.</span></span>
2. <span data-ttu-id="5f482-126">해당 hello 게 사용자에 게 toobe hello 구독 소유자는 hello 대상 디렉터리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-126">Ensure that hello user who you want toobe hello subscription owner is in hello targeted directory.</span></span>
3. <span data-ttu-id="5f482-127">**구독 이전**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-127">Click **Transfer subscription**.</span></span>
4. <span data-ttu-id="5f482-128">Hello 받는 사람을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-128">Specify hello recipient.</span></span> <span data-ttu-id="5f482-129">hello 받는 사람 전자 메일을 동의 링크를 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-129">hello recipient automatically gets an email with an acceptance link.</span></span>
5. <span data-ttu-id="5f482-130">hello 받는 사람 hello 링크를 클릭 하 고 지불 정보를 입력 하는 등 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-130">hello recipient clicks hello link and follows hello instructions, including entering their payment information.</span></span> <span data-ttu-id="5f482-131">Hello 받는 사람에 성공 하면 hello 구독 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-131">When hello recipient succeeds, hello subscription is transferred.</span></span> 
6. <span data-ttu-id="5f482-132">hello 구독의 hello 기본 디렉터리 변경 toohello 디렉터리에는 해당 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-132">hello default directory of hello subscription is changed toohello directory that hello user is in.</span></span>


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a><span data-ttu-id="5f482-133">구독 및 디렉터리가 제안 toomanage</span><span class="sxs-lookup"><span data-stu-id="5f482-133">Suggestions toomanage both a subscription and a directory</span></span>
<span data-ttu-id="5f482-134">Azure 구독에 대 한 hello 관리 역할 연결 리소스 toohello Azure 구독을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-134">hello administrative roles for an Azure subscription manage resources tied toohello Azure subscription.</span></span> <span data-ttu-id="5f482-135">이 섹션에서는 Azure 구독 관리자와 Azure AD 디렉터리 관리자 간의 hello 차이점을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-135">This section explains hello differences between Azure subscription admins and Azure AD directory admins.</span></span> <span data-ttu-id="5f482-136">관리 역할 관리 및 구독에 대해서는 설명 toomanage 사용에 대 한 다른 제안 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-136">Administrative roles and other suggestions for using them toomanage your subscription are covered at [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="5f482-137">기본적으로 등록할 때는 hello 서비스 관리자 역할을 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-137">By default, you are assigned hello Service Administrator role when you sign up.</span></span> <span data-ttu-id="5f482-138">다른 사용자에 toosign 고 hello를 사용 하 여 서비스에 액세스할 경우 동일한 구독을 추가할 수 있습니다 공동 관리자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-138">If others need toosign in and access services using hello same subscription, you can add them as co-administrators.</span></span> 

<span data-ttu-id="5f482-139">Azure AD에는 다른 일련의 관리 역할 toomanage hello 디렉터리 및 id 관련 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-139">Azure AD has a different set of administrative roles toomanage hello directory and identity-related features.</span></span> <span data-ttu-id="5f482-140">예를 들어 디렉터리의 전역 관리자에 게 사용자 및 그룹 toohello 디렉터리를 추가 하거나 사용자에 대 한 다단계 인증을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-140">For example, hello global administrator of a directory can add users and groups toohello directory, or require multifactor authentication for users.</span></span> <span data-ttu-id="5f482-141">디렉터리를 만드는 사용자가 toohello 전역 관리자 역할이 할당 및 관리 역할 tooother 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-141">A user who creates a directory is assigned toohello global administrator role and they can assign administrative roles tooother users.</span></span> <span data-ttu-id="5f482-142">또한 Azure AD 관리 역할은 Office 365 및 Microsoft Intune과 같은 다른 서비스에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-142">Azure AD administrative roles are also used by other services such as Office 365 and Microsoft Intune.</span></span> 

<span data-ttu-id="5f482-143">Azure 구독 관리자와 Azure AD 디렉터리 관리자는 서로 다른 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-143">Azure subscription admins and Azure AD directory admins are two separate roles.</span></span> 
* <span data-ttu-id="5f482-144">Azure 구독 관리자는 Azure의에서 리소스를 관리 하 고 (Azure 포털 자체 hello Azure 리소스 이므로) hello Azure 포털에서에서 Azure AD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-144">Azure subscription admins can manage resources in Azure and can use Azure AD in hello Azure portal (because hello Azure portal itself is an Azure resource).</span></span> 
* <span data-ttu-id="5f482-145">디렉터리 관리자만 hello Azure AD 디렉터리에서에서 속성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-145">Directory admins can manage properties only in hello Azure AD directory.</span></span>

<span data-ttu-id="5f482-146">역할을 모두 담당할 수 있지만 그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-146">A person can be in both roles but it isn’t required.</span></span> <span data-ttu-id="5f482-147">디렉터리 전역 관리자는 Azure 구독의 서비스 관리자 또는 공동 관리자로 할당될 수 없고 반대도 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-147">A directory global administrator might not be assigned as service administrator or co-administrator of an Azure subscription, or vice versa.</span></span> <span data-ttu-id="5f482-148">Hello 구독 관리자가 아니어도 hello 사용자 toohello Azure 포털에에서 서명할 수 있지만 hello 포털에서 해당 구독에 대 한 hello 디렉터리를 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-148">Without being an administrator of hello subscription, hello user can sign in toohello Azure portal, but can't manage hello directories for that subscription in hello portal.</span></span> <span data-ttu-id="5f482-149">그러나이 사용자는 Azure AD PowerShell 또는 Office 365 관리 센터 hello와 같은 다른 도구를 사용 하 여 디렉터리를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f482-149">However, this user can manage directories using other tools such as Azure AD PowerShell or hello Office 365 Admin Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f482-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f482-150">Next steps</span></span>
* <span data-ttu-id="5f482-151">toochange 관리자는 Azure 구독에 대 한 참조 하는 방법에 대해 더 알아봅니다을 toolearn [의 Azure 구독 tooanother 계정 소유권 이전](../billing/billing-subscription-transfer.md)</span><span class="sxs-lookup"><span data-stu-id="5f482-151">toolearn more about how toochange administrators for an Azure subscription, see [Transfer ownership of an Azure subscription tooanother account](../billing/billing-subscription-transfer.md)</span></span>
* <span data-ttu-id="5f482-152">Microsoft Azure에서 리소스 액세스 제어 하는 방법에 대 한 자세한 toolearn 참조 [Azure에서 리소스 액세스 이해](active-directory-understanding-resource-access.md)</span><span class="sxs-lookup"><span data-stu-id="5f482-152">toolearn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](active-directory-understanding-resource-access.md)</span></span>
* <span data-ttu-id="5f482-153">방법에 대 한 자세한 내용은 Azure AD에서 tooassign 역할 참조 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5f482-153">For more information on how tooassign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
