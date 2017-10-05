---
title: Azure Active Directory FAQ | Microsoft Docs
description: "Azure Active Directory FAQ는 Azure 및 Azure Active Directory에 액세스하는 방법, 암호 관리 및 응용 프로그램 액세스에 대한 질문에 답변합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 8d4460b3059558de2253c6f6a2d2fc8e7564d6d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="199be-103">Azure Active Directory FAQ</span><span class="sxs-lookup"><span data-stu-id="199be-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="199be-104">Azure Active Directory(Azure AD)는 ID, 액세스 관리 및 보안의 모든 측면에 걸쳐있는 포괄적인 IDaaS(Identity as a Service) 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="199be-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="199be-105">자세한 내용은 [Azure Active Directory란?](active-directory-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="199be-106">Azure 및 Azure Active Directory 액세스</span><span class="sxs-lookup"><span data-stu-id="199be-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="199be-107">**Q: Azure 클래식 포털에서 Azure AD에 액세스하려고 할 때 "구독을 찾을 수 없음"이 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="199be-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal?**</span></span>

<span data-ttu-id="199be-108">**A:** Azure 클래식 포털에 액세스하려면 각 사용자에게 Azure 구독을 통한 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="199be-109">유료 Office 365 또는 Azure AD 구독이 있는 경우 일회성 활성화 단계를 위해 [http://aka.ms/accessAAD](http://aka.ms/accessAAD)로 이동하십시오.</span><span class="sxs-lookup"><span data-stu-id="199be-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="199be-110">그렇지 않으면 무료 [Azure 계정](https://azure.microsoft.com/pricing/free-trial/) 또는 유료 구독을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="199be-111">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-111">For more information, see:</span></span>

* [<span data-ttu-id="199be-112">Azure 구독과 Azure Active Directory의 연관 관계</span><span class="sxs-lookup"><span data-stu-id="199be-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="199be-113">Azure에서 Office 365 구독의 디렉터리 관리</span><span class="sxs-lookup"><span data-stu-id="199be-113">Manage the directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="199be-114">**Q: Azure AD, Office 365와 Azure 간에는 어떤 관계가 있나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="199be-115">**A:** Azure AD는 모든 웹 서비스에 공통 ID 및 액세스 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="199be-116">Office 365, Microsoft Azure, Intune 또는 기타 제품을 사용하든지 이러한 모든 서비스에 대해 로그온 및 액세스 관리 설정을 지원하는 데 Azure AD를 이미 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="199be-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="199be-117">웹 서비스를 사용하도록 설정된 모든 사용자는 하나 이상의 Azure AD 인스턴스에 사용자 계정으로 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="199be-118">클라우드 응용 프로그램 액세스와 같은 무료 Azure AD 기능에 이러한 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="199be-119">Enterprise Mobility + Security와 같은 Azure AD 유료 서비스는 포괄적인 엔터프라이즈 규모 관리 및 보안 솔루션을 통해 Office 365 및 Microsoft Azure와 같은 기타 웹 서비스를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="199be-120">**Q: Azure Portal에는 로그인할 수 있는데 Azure 클래식 포털에는 로그인할 수 없는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="199be-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span></span>

<span data-ttu-id="199be-121">**A:** 클래식 포털에서는 유효한 구독이 필요한 반면 Azure Portal에는 유효한 구독이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span></span>  <span data-ttu-id="199be-122">구독이 없는 경우 클래식 포털에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-122">If you do not have a subscription, you can't sign in to the classic portal.</span></span>
- - -
<span data-ttu-id="199be-123">**Q:  구독 관리자와 디렉터리 관리자의 차이점은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="199be-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="199be-124">**A:** 기본적으로 Azure에 로그인할 때 구독 관리자 역할이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="199be-125">구독 관리자는 Azure 구독이 연결된 디렉터리에서 Microsoft 계정이나 회사 또는 학교 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="199be-126">이 역할은 Azure Portal에서 서비스를 관리할 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-126">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="199be-127">다른 사용자가 동일한 구독을 사용하여 로그인하고 서비스에 액세스해야 하는 경우 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="199be-128">이 역할은 서비스 관리자와 동일한 액세스 권한이 있지만 Azure 디렉터리에 대한 구독의 연결을 변경할 수는 없는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="199be-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span></span>  <span data-ttu-id="199be-129">구독 관리자에 대한 자세한 내용은 [Azure 관리자 역할을 추가 또는 변경하는 방법](../billing-add-change-azure-subscription-administrator.md) 및 [Azure 구독과 Azure Active Directory의 연관 관계](active-directory-how-subscriptions-associated-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="199be-130">Azure AD에는 디렉터리 및 ID 관련 기능을 관리하는 다른 관리 역할 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span></span>  <span data-ttu-id="199be-131">이러한 관리자는 Azure Portal 또는 Azure 클래식 포털의 다양한 기능에 대해 액세스 권한을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span></span> <span data-ttu-id="199be-132">관리자 역할은 사용자 만들기 또는 편집, 다른 사람에게 관리자 역할 할당, 사용자 암호 재설정, 사용자 라이선스 관리 또는 도메인 관리와 같이 관리자가 수행할 수 있는 업무를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="199be-133">Azure AD 디렉터리 관리자 및 그 역할에 대한 자세한 내용은 [Azure Active Directory에서 관리자 역할 할당](active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="199be-134">또한, Enterprise Mobility + Security와 같은 Azure AD 유료 서비스는 포괄적인 엔터프라이즈 규모 관리 및 보안 솔루션을 통해 Office 365 및 Microsoft Azure와 같은 기타 웹 서비스를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="199be-135">**Q: 보고서에서 내 Azure AD 사용자 라이선스가 만료되는 시기를 표시하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="199be-136">**A:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="199be-136">**A:** No.</span></span>  <span data-ttu-id="199be-137">현재는 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="199be-138">하이브리드 Azure AD 시작</span><span class="sxs-lookup"><span data-stu-id="199be-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="199be-139">**Q: 협력자로 추가된 경우 테넌트를 어떻게 나가나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="199be-140">**A:** 다른 조직의 테넌트에 협력자로 추가된 경우 오른쪽 위의 "테넌트 전환기"를 사용하여 테넌트 사이를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="199be-141">현재는 초대한 조직을 나갈 수 있는 방법이 없으며, 이 기능을 제공하기 위해 준비 중입니다.</span><span class="sxs-lookup"><span data-stu-id="199be-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="199be-142">이 기능이 제공될 때까지는 테넌트에서 사용자를 제거해 주도록 초대한 조직에게 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="199be-143">**Q: Azure AD에 온-프레미스 디렉터리를 연결하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-143">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="199be-144">**A:** Azure AD Connect를 사용하여 온-프레미스 디렉터리를 Azure AD에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="199be-145">자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="199be-146">**Q: 온-프레미스 디렉터리와 클라우드 응용 프로그램 간에 SSO를 설정하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="199be-147">**A:** 온-프레미스 디렉터리와 Azure AD 간에 SSO(Single Sign-On)만 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="199be-148">Azure AD를 통해 클라우드 응용 프로그램에 액세스할 수만 있다면 서비스는 온-프레미스 자격 증명으로 올바르게 인증하도록 사용자를 자동으로 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="199be-149">온-프레미스에서 SSO 구현은 AD FS(Active Directory Federation Services)와 같은 페더레이션 솔루션 또는 암호 해시 동기화 구성으로 쉽게 달성할 수 있습니다. 두 옵션 모두 Azure AD Connect 구성 마법사를 사용하여 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="199be-150">자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="199be-151">**Q: Azure AD에서 내 조직의 사용자에 대한 셀프 서비스 포털을 제공하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="199be-152">**A:** 예, Azure AD는 사용자 셀프 서비스 및 응용 프로그램 액세스를 위해 [Azure AD 액세스 패널](http://myapps.microsoft.com)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="199be-153">Office 365 고객인 경우 Office 365 포털에서 동일한 기능을 많이 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="199be-154">자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="199be-155">**Q: Azure AD를 사용하면 내 온-프레미스 인프라를 관리하는 데 도움이 되나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="199be-156">**A:** 예.</span><span class="sxs-lookup"><span data-stu-id="199be-156">**A:** Yes.</span></span> <span data-ttu-id="199be-157">Azure AD Premium Edition에는 Azure AD Connect Health가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="199be-158">Azure AD Connect Health를 사용하면 온-프레미스 ID 인프라 및 동기화 서비스를 모니터링하고 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="199be-159">자세한 내용은 [온-프레미스 ID 인프라 및 클라우드 동기화 서비스 모니터링](active-directory-aadconnect-health.md)을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="199be-160">암호 관리</span><span class="sxs-lookup"><span data-stu-id="199be-160">Password management</span></span>
<span data-ttu-id="199be-161">**Q: Azure AD 비밀번호 쓰기 저장을 암호 동기화 없이 사용할 수 있나요? (이 시나리오에서 클라우드에 암호를 저장하기 않고 암호 쓰기 저장을 사용하여 Azure AD SSPR(셀프 서비스 암호 재설정)을 사용할 수 있나요?)**</span><span class="sxs-lookup"><span data-stu-id="199be-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="199be-162">**A:** 쓰기 저장을 사용하기 위해 Azure AD에 Active Directory 암호를 동기화할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="199be-163">페더레이션된 환경에서 Azure AD SSO(Single Sign-On)는 온-프레미스 디렉터리에 의존하여 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="199be-164">이 시나리오는 Azure AD에서 추적되는 온-프레미스 암호를 필요로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="199be-165">**Q: Active Directory 온-프레미스에 암호를 쓰기 저장하는 데 시간이 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="199be-166">**A:** 비밀번호 쓰기 저장은 실시간으로 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="199be-167">자세한 내용은 [암호 관리 시작](active-directory-passwords-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="199be-168">**Q: 관리자가 관리하는 암호로 비밀번호 쓰기 저장을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="199be-169">**A:** 예, 비밀번호 쓰기 저장을 사용하도록 설정하는 경우 관리자가 수행하는 암호 작업이 온-프레미스 환경에 다시 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="199be-170">암호와 관련된 질문에 대한 자세한 답변은 [암호 관리 질문과 대답](active-directory-passwords-faq.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="199be-171">**Q: 암호 변경을 시도하는 동안 기존 Office 365/Azure AD 암호를 기억할 수 없는 경우 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="199be-172">**A:** 이러한 상황에는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="199be-173">SSPR(셀프 서비스 암호 재설정)을 사용할 수 있으면 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="199be-174">SSPR 작동 여부는 구성 방식에 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="199be-175">자세한 내용은 [암호 재설정 포털의 작동 원리](active-directory-passwords-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-175">For more information, see [How does the password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="199be-176">Office 365 사용자의 경우 [사용자 암호 다시 설정](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US)에 설명된 단계를 사용하여 관리자가 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="199be-177">Azure AD 계정의 경우 다음 중 하나를 사용하여 관리자가 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- [<span data-ttu-id="199be-178">Azure Portal에서 계정 재설정</span><span class="sxs-lookup"><span data-stu-id="199be-178">Reset accounts in the Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="199be-179">클래식 Portal에서 계정 재설정</span><span class="sxs-lookup"><span data-stu-id="199be-179">Reset accounts in the classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="199be-180">PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="199be-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="199be-181">보안</span><span class="sxs-lookup"><span data-stu-id="199be-181">Security</span></span>
<span data-ttu-id="199be-182">**Q: 시도가 일정 횟수 실패하면 계정이 잠기나요 아니면 좀 더 복잡한 전략이 사용되나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="199be-183">좀 더 복잡한 계정 잠금 전략이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="199be-183">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="199be-184">이 전략은 요청의 IP 주소와 입력된 암호를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-184">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="199be-185">또한 실패한 시도가 공격일 가능성에 따라 잠금 기간이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="199be-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="199be-186">**Q: ‘이 암호가 너무 많이 사용되었습니다’라는 메시지와 함께 특정(공통) 암호가 거부되었습니다. 현재 활성 디렉터리에서 사용되는 암호를 말하는 것입니까?**</span><span class="sxs-lookup"><span data-stu-id="199be-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span></br>
<span data-ttu-id="199be-187">"Password" 및 "123456"의 변형과 같이 전역에서 일반적인 암호를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="199be-188">**Q: 수상한 소스(봇넷, tor 끝점)의 로그인 요청은 B2C 테넌트에서 차단되나요? 아니면 Basic 또는 Premium Edition 테넌트가 필요한가요?**</span><span class="sxs-lookup"><span data-stu-id="199be-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="199be-189">요청을 필터링하고 봇넷으로부터 보호하며, 모든 B2C 테넌트에 적용되는 게이트웨이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="199be-190">응용 프로그램 액세스</span><span class="sxs-lookup"><span data-stu-id="199be-190">Application access</span></span>
<span data-ttu-id="199be-191">**Q: Azure AD 및 해당 기능과 미리 통합된 응용 프로그램의 목록을 어디에서 찾을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="199be-192">**A:** Azure AD에는 Microsoft, 응용 프로그램 서비스 공급자 및 파트너의 사전 통합된 응용 프로그램이 2,600개 넘게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="199be-193">사전 통합된 모든 응용 프로그램에서 SSO(Single Sign-On)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="199be-194">SSO를 사용하면 조직의 자격 증명을 사용하여 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-194">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="199be-195">일부 응용 프로그램은 자동화된 프로비전 및 프로비전 해제도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-195">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="199be-196">미리 통합된 응용 프로그램의 전체 목록은 [Active Directory 마켓플레이스](https://azure.microsoft.com/marketplace/active-directory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="199be-197">**Q: 필요한 응용 프로그램이 Azure AD 마켓플레이스에 없는 경우 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="199be-198">**A:** Azure AD Premium에서는 원하는 응용 프로그램을 추가하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="199be-199">응용 프로그램의 기능 및 기본 설정에 따라 SSO 및 자동화된 프로비전을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="199be-200">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-200">For more information, see:</span></span>

* [<span data-ttu-id="199be-201">Azure Active Directory 응용 프로그램 갤러리에 있지 않은 응용 프로그램에 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="199be-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="199be-202">SCIM를 사용하여 Azure Active Directory으로부터 응용 프로그램에 사용자 및 그룹의 자동 프로비전 사용</span><span class="sxs-lookup"><span data-stu-id="199be-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="199be-203">**Q: 사용자가 Azure AD를 사용하여 응용 프로그램에 로그인하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-203">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="199be-204">**A:** Azure AD는 다음과 같이 사용자가 자신의 응용 프로그램을 보고 액세스할 수 있는 여러 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="199be-205">Azure AD 액세스 패널</span><span class="sxs-lookup"><span data-stu-id="199be-205">The Azure AD access panel</span></span>
* <span data-ttu-id="199be-206">Office 365 응용 프로그램 실행 프로그램</span><span class="sxs-lookup"><span data-stu-id="199be-206">The Office 365 application launcher</span></span>
* <span data-ttu-id="199be-207">페더레이션된 앱에 직접 로그인</span><span class="sxs-lookup"><span data-stu-id="199be-207">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="199be-208">페더레이션된 앱, 암호로 보호된 앱 또는 기존 앱에 대한 딥 링크</span><span class="sxs-lookup"><span data-stu-id="199be-208">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="199be-209">자세한 내용은 [사용자에게 Azure AD 통합 응용 프로그램 배포](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="199be-210">**Q: Azure AD에서 응용 프로그램에 대한 인증 및 Single Sign-On을 설정하는 다른 방법은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="199be-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="199be-211">**A:** Azure AD는 SAML 2.0, OpenID Connect, OAuth 2.0, WS-Federation 등 인증 및 권한 부여를 위해 여러 표준화된 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="199be-212">또한 Azure AD는 양식 기반 인증만 지원하는 앱에 대해 암호 보관 및 자동화된 로그인 기능도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="199be-213">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-213">For more information, see:</span></span>

* [<span data-ttu-id="199be-214">Azure AD의 인증 시나리오</span><span class="sxs-lookup"><span data-stu-id="199be-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="199be-215">Active Directory 인증 프로토콜</span><span class="sxs-lookup"><span data-stu-id="199be-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="199be-216">Azure Active Directory에서 Single Sign-On이 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="199be-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="199be-217">**Q: 온-프레미스를 실행하는 응용 프로그램을 추가할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="199be-218">**A:** Azure AD 응용 프로그램 프록시는 선택한 온-프레미스 웹 응용 프로그램에 대해 손쉽고 안전한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="199be-219">Azure AD에서 SaaS(Software as a Service) 앱에 액세스하는 것과 동일한 방식으로 이러한 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="199be-220">네트워크 인프라 변경이나 VPN이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-220">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="199be-221">자세한 내용은 [온-프레미스 응용 프로그램에 보안 원격 액세스를 제공하는 방법](active-directory-application-proxy-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="199be-222">**Q: 특정 응용 프로그램에 액세스하는 사용자의 Multi-Factor Authentication을 어떻게 요청하나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="199be-223">**A:** Azure AD 조건부 액세스에서는 각 응용 프로그램에 대한 고유한 액세스 정책을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="199be-224">정책에서 언제든지 또는 사용자가 로컬 네트워크에 연결되지 않은 경우 Multi-Factor Authentication을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="199be-225">자세한 내용은 [Azure Active Directory에 연결된 Office 365 및 기타 앱에 대한 액세스 보호](active-directory-conditional-access.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="199be-226">**Q: SaaS 앱을 위한 자동 사용자 프로비전이 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="199be-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="199be-227">**A:** Azure AD를 사용하여 다수의 인기 있는 클라우드 SaaS 앱의 사용자 ID 만들기, 유지 관리 및 제거를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="199be-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="199be-228">자세한 내용은 [Azure Active Directory를 사용하여 SaaS 응용 프로그램의 사용자를 자동으로 프로비전 및 프로비전 해제](active-directory-saas-app-provisioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="199be-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="199be-229">**Q: Azure AD에서 보안 LDAP 연결을 설정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="199be-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="199be-230">**A:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="199be-230">**A:**  No.</span></span> <span data-ttu-id="199be-231">Azure AD에서는 LDAP 프로토콜을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="199be-231">Azure AD does not support the LDAP protocol.</span></span>
