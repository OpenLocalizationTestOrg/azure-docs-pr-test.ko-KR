---
title: "Azure Active Directory에서 라이선스 시작 | Microsoft Docs"
description: "Azure Active Directory 라이선스 작동 원리, 모범 사례를 시작하는 방법"
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
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 6fa7cbbc452861870136482aa320d268e78fe3d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a><span data-ttu-id="91ca9-104">Azure Active Directory에서 사용자 본인 및 사용자의 사용자 라이선스</span><span class="sxs-lookup"><span data-stu-id="91ca9-104">License yourself and your users in Azure Active Directory</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="91ca9-105">Azure Portal 지침</span><span class="sxs-lookup"><span data-stu-id="91ca9-105">Azure portal instructions</span></span>](active-directory-licensing-get-started-azure-portal.md)
> * [<span data-ttu-id="91ca9-106">Azure 클래식 포털 정보</span><span class="sxs-lookup"><span data-stu-id="91ca9-106">Get Azure classic portal info</span></span>](active-directory-licensing-what-is.md)
>
>

<span data-ttu-id="91ca9-107">Azure AD(Azure Active Directory)는 Microsoft의 IDaaS(Identity as a Service) 솔루션 및 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-107">Azure Active Directory (Azure AD) is an identity as a service (IDaaS) solution and platform from Microsoft.</span></span> <span data-ttu-id="91ca9-108">Azure AD는 다양한 서비스 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-108">Azure AD is offered in different service editions:</span></span>

* <span data-ttu-id="91ca9-109">Azure Active Directory Free - Office 365, Dynamics, Microsoft Intune 또는 Azure와 같은 Microsoft 서비스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-109">Azure Active Directory Free, which is available with any Microsoft service such as Office 365, Dynamics, Microsoft Intune, or Azure.</span></span> <span data-ttu-id="91ca9-110">Azure AD는 이 모드에서 사용량 요금을 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-110">Azure AD does not generate any consumption charges in this mode.</span></span>

* <span data-ttu-id="91ca9-111">Azure AD 유료 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-111">Azure AD paid editions, such as:</span></span>
  - <span data-ttu-id="91ca9-112">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="91ca9-112">Enterprise Mobility + Security</span></span> 
  - <span data-ttu-id="91ca9-113">Azure AD Premium(P1 및 P2)</span><span class="sxs-lookup"><span data-stu-id="91ca9-113">Azure AD Premium (P1 and P2)</span></span>
  - <span data-ttu-id="91ca9-114">Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="91ca9-114">Azure AD Basic</span></span>
  - <span data-ttu-id="91ca9-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="91ca9-115">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="91ca9-116">많은 Microsoft 온라인 서비스와 마찬가지로 대부분의 Azure AD 유료 버전은 Office 365, Microsoft Intune 및 Azure AD에서 사용자별 권한 부여를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-116">Like many of Microsoft online services, most Azure AD paid versions are delivered through per-user entitlements as they are in Office 365, Microsoft Intune, and Azure AD.</span></span> <span data-ttu-id="91ca9-117">이런 경우 서비스 구매는 하나 이상의 구독으로 표시되며 각 구독에는 테넌트의 일부 사전 구매 라이선스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-117">In these cases, the service purchase is represented by one or more subscriptions, and each subscription includes some prepurchased licenses in your tenant.</span></span> <span data-ttu-id="91ca9-118">사용자 단위 자격은 다음을 통해 취득합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-118">Per-user entitlements are achieved by:</span></span>

* <span data-ttu-id="91ca9-119">라이선스 할당.</span><span class="sxs-lookup"><span data-stu-id="91ca9-119">Assigning a license.</span></span> 
* <span data-ttu-id="91ca9-120">사용자와 제품 간 링크 만들기.</span><span class="sxs-lookup"><span data-stu-id="91ca9-120">Creating a link between the user and the product.</span></span>
* <span data-ttu-id="91ca9-121">사용자에 대한 서비스 구성 요소 사용.</span><span class="sxs-lookup"><span data-stu-id="91ca9-121">Enabling the service components for the user.</span></span>
* <span data-ttu-id="91ca9-122">선불 라이선스 중 하나 사용.</span><span class="sxs-lookup"><span data-stu-id="91ca9-122">Consuming one of the prepaid licenses.</span></span>

[<span data-ttu-id="91ca9-123">이제 Azure AD premium을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-123">Try Azure AD Premium now.</span></span>](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

<span data-ttu-id="91ca9-124">Azure AD 서비스 기능에 대한 광범위한 개요는 [Azure AD란?](active-directory-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91ca9-124">For a broad overview of Azure AD service capabilities, see [What is Azure AD?](active-directory-whatis.md).</span></span> <span data-ttu-id="91ca9-125">자세한 내용은 [Azure Active Directory에 대한 SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91ca9-125">For more information, see our [Service Level Agreements page](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).</span></span>

> [!NOTE]
> <span data-ttu-id="91ca9-126">Azure 종량제 구독을 통해 Azure 리소스를 만들고 이 리소스를 결제 방법에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-126">Azure pay-as-you-go subscriptions enable creation of Azure resources and then map them to your payment method.</span></span> <span data-ttu-id="91ca9-127">구독과 연결된 라이선스 수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-127">There are no license counts associated with the subscription.</span></span> <span data-ttu-id="91ca9-128">구독에 매핑된 Azure 리소스에 적용할 사용자 권한을 부여하면 사용자는 구독과 연결되고 구독 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-128">When you grant a user permission to operate on Azure resources mapped to the subscription, they are associated with the subscription and can manage subscription resources.</span></span>

## <a name="how-does-azure-active-directory-licensing-work"></a><span data-ttu-id="91ca9-129">Azure Active Directory 라이선스는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="91ca9-129">How does Azure Active Directory licensing work?</span></span>

<span data-ttu-id="91ca9-130">라이선스 기반 Azure AD 서비스는 Azure AD 서비스 테넌트에서 구독을 활성화하면 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-130">License-based Azure AD services work by activating a subscription in your Azure AD service tenant.</span></span> <span data-ttu-id="91ca9-131">구독이 활성화된 후 서비스 기능은 Azure AD 관리자가 관리하고 사용이 허가된 사용자가 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-131">After the subscription is active, the service capabilities are managed by Azure AD administrators and used by licensed users.</span></span>

### <a name="manage-subscription-information"></a><span data-ttu-id="91ca9-132">구독 정보 관리</span><span class="sxs-lookup"><span data-stu-id="91ca9-132">Manage subscription information</span></span>

<span data-ttu-id="91ca9-133">Enterprise Mobility + Security, Azure AD Premium 또는 Azure AD Basic을 구매하면 디렉터리의 유효 기간 및 선불 라이선스를 포함하여 테넌트가 구독으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-133">When you purchase Enterprise Mobility + Security, Azure AD Premium, or Azure AD Basic, your tenant is updated with the subscription, including its validity period and prepaid licenses.</span></span> <span data-ttu-id="91ca9-134">할당되거나 사용 가능한 라이선스 수를 포함한 구독 정보는 Azure Portal을 통해 사용할 수 있습니다. **Azure Active Directory** 아래에서 특정 디렉터리에 대한 **라이선스** 타일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-134">Your subscription information, including the number of assigned or available licenses, is available through the Azure portal: Under **Azure Active Directory**, open the **Licenses** tile for the specific directory.</span></span> <span data-ttu-id="91ca9-135">**라이선스** 블레이드는 사용자 라이선스 할당을 관리하기에 가장 적합한 위치이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-135">The **Licenses** blade is also the best place to manage your license assignments.</span></span>

<span data-ttu-id="91ca9-136">각 구독은 Azure AD, Multi-Factor Authentication, Intune, Exchange Online 또는 SharePoint Online과 같은 하나 이상의 서비스 계획으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-136">Each subscription consists of one or more service plans, such as Azure AD, Multi-Factor Authentication, Intune, Exchange Online, or SharePoint Online.</span></span>  <span data-ttu-id="91ca9-137">Azure AD 라이선스 관리에는 서비스 계획 수준 관리가 필요하지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="91ca9-137">Azure AD license management does *not* require service-plan-level management.</span></span> <span data-ttu-id="91ca9-138">Office 365는 포함된 서비스에 대한 액세스를 관리하기 위해 이 고급 구성 모드에 의존하므로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-138">Office 365 differs because it relies on this advanced configuration mode to manage access to included services.</span></span> <span data-ttu-id="91ca9-139">Azure AD는 서비스 구성에 의존하여 기능을 활성화하고 개별 사용 권한을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-139">Azure AD relies on in-service configuration to enable features and manage individual permissions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91ca9-140">Azure AD Premium, Azure AD Basic 및 Enterprise Mobility + Security 구독은 프로비전된 해당 디렉터리/테넌트로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-140">Azure AD Premium, Azure AD Basic, and Enterprise Mobility + Security subscriptions are confined to their provisioned directory/tenant.</span></span> <span data-ttu-id="91ca9-141">구독은 디렉터리 간에 분할되거나 다른 디렉터리의 사용자에게 자격을 부여하는 데 사용될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-141">Subscriptions cannot be split between directories or used to entitle users in other directories.</span></span> <span data-ttu-id="91ca9-142">구독을 디렉터리 간에 이동하는 것은 가능하지만 지원 티켓을 제출하거나, 직접 구매의 경우 취소 후 다시 구매해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-142">Moving a subscription between directories is possible, but requires submitting a support ticket, or cancellation and repurchase for direct purchases.</span></span>
>
> <span data-ttu-id="91ca9-143">볼륨 라이선싱 구독을 통해 Azure AD 또는 Enterprise Mobility + Security를 구매하는 경우 규약에 다른 Microsoft Online Services(예: Office 365)가 포함되어 있으면 구독이 자동으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-143">When Azure AD or Enterprise Mobility + Security is purchased through a Volume Licensing subscription, and when the agreement includes other Microsoft Online services (for example, Office 365), activation happens automatically.</span></span> 

### <a name="assign-licenses"></a><span data-ttu-id="91ca9-144">라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="91ca9-144">Assign licenses</span></span>

<span data-ttu-id="91ca9-145">유료 기능을 구성하기 위해서는 구독을 얻기만 하면 되지만, Azure AD 유료 기능에 대한 라이선스를 사용자에게 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-145">Although obtaining a subscription is all you need to configure paid capabilities, you must still distribute licenses for Azure AD paid features to users.</span></span> <span data-ttu-id="91ca9-146">액세스 권한이 있어야 하거나 Azure AD 유료 기능을 통해 관리되는 모든 사용자에게 라이선스가 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-146">Any user who should have access to or who is managed through an Azure AD paid feature must be assigned a license.</span></span> <span data-ttu-id="91ca9-147">라이선스 할당은 Azure AD Premium, Basic 또는 Enterprise Mobility + Security 등의 구매한 서비스와 사용자 간의 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-147">License assignment is a mapping between a user and a purchased service, such as Azure AD Premium, Basic, or Enterprise Mobility + Security.</span></span>


<span data-ttu-id="91ca9-148">디렉터리의 어떤 사용자에게 라이선스가 있어야 하는지 관리하려면 다음 작업을 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-148">Managing which users in your directory should have a license can be accomplished by:</span></span> 

* <span data-ttu-id="91ca9-149">[Azure Portal](active-directory-licensing-whatis-azure-portal.md)에서 그룹에게 라이선스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-149">Assigning licenses to groups in the [Azure portal](active-directory-licensing-whatis-azure-portal.md).</span></span>
* <span data-ttu-id="91ca9-150">포털, PowerShell 또는 API를 통해 사용자에게 직접 라이선스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-150">Assigning licenses directly to users by way of the portal, PowerShell, or APIs.</span></span> 

<span data-ttu-id="91ca9-151">그룹에게 라이선스를 할당하면 모든 그룹 구성원에게 라이선스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-151">When you're assigning licenses to a group, all group members are assigned a license.</span></span> <span data-ttu-id="91ca9-152">사용자가 그룹에서 추가 또는 제거될 경우 해당 라이선스가 할당 또는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-152">If users are added or removed from the group, the appropriate license is assigned or removed.</span></span> <span data-ttu-id="91ca9-153">그룹 할당에는 사용자가 사용 가능한 모든 그룹 관리를 이용할 수 있으며 응용 프로그램에 대한 그룹 기반 할당과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-153">Group assignment can utilize any group management available to you, and it is consistent with group-based assignment to applications.</span></span>

<span data-ttu-id="91ca9-154">[그룹 기반 라이선스 할당](active-directory-licensing-whatis-azure-portal.md)을 사용하여 다음과 같은 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-154">You can use [group-based license assignment](active-directory-licensing-whatis-azure-portal.md) to set up rules such as the following:</span></span>
* <span data-ttu-id="91ca9-155">디렉터리의 모든 사용자가 자동으로 라이선스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-155">All users in your directory automatically get a license</span></span>
* <span data-ttu-id="91ca9-156">해당하는 직위를 가진 모든 사용자가 라이선스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-156">Everyone with the appropriate job title gets a license</span></span>
* <span data-ttu-id="91ca9-157">[셀프 서비스 그룹](active-directory-accessmanagement-self-service-group-management.md)을 사용하여 조직의 다른 관리자에게 의사 결정을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-157">You can delegate the decision to other managers in the organization (by using [self-service groups](active-directory-accessmanagement-self-service-group-management.md))</span></span>

<span data-ttu-id="91ca9-158">고급 시나리오 및 Office 365 라이선스 시나리오를 비롯한 그룹에 대한 라이선스 할당의 자세한 내용은 [Azure Active Directory에서 그룹 멤버 자격에 따라 사용자에게 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91ca9-158">For a detailed discussion of license assignment to groups, including advanced scenarios and Office 365 licensing scenarios, see [Assign licenses to users by group membership in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

## <a name="get-started-with-azure-ad-licensing"></a><span data-ttu-id="91ca9-159">Azure AD 라이선스 시작</span><span class="sxs-lookup"><span data-stu-id="91ca9-159">Get started with Azure AD licensing</span></span>

<span data-ttu-id="91ca9-160">Azure AD를 시작하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-160">Getting started with Azure AD is easy.</span></span> <span data-ttu-id="91ca9-161">언제든지 [Azure 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) 등록의 일부로 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-161">You can always create your directory as a part of signing up for an [Azure free trial](https://azure.microsoft.com/offers/ms-azr-0044p/).</span></span>

<span data-ttu-id="91ca9-162">다음 모범 사례를 통해 사용 중인 다른 Microsoft 서비스 및 서비스 목표에 테넌트가 적합한지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-162">The following best practices can help ensure that your tenant is aligned with other Microsoft services you might be consuming and with your goals for the service:</span></span>

- <span data-ttu-id="91ca9-163">Microsoft의 조직 서비스를 사용 중이면 이미 Azure AD 테넌트가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-163">If you are already using any of the organizational services from Microsoft, you already have an Azure AD tenant.</span></span> <span data-ttu-id="91ca9-164">프로비전 및 하이브리드 SSO(Single Sign-On)를 포함하여 핵심 ID 관리를 서비스 전체에서 사용할 수 있도록 다른 서비스에도 동일한 테넌트를 사용하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-164">It is useful to use the same tenant for other services so that core identity management, including provisioning and hybrid single sign-on (SSO), can be used across the services.</span></span> <span data-ttu-id="91ca9-165">Single Sign-On을 통해 사용자는 서비스 전체에서 다양한 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-165">With single sign-on, your users benefit from the rich capabilities across the services.</span></span> <span data-ttu-id="91ca9-166">따라서 직원을 위해 Azure AD 유료 서비스를 구매하기로 결정하는 경우 동일한 테넌트를 다시 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-166">Thus, if you decide to buy an Azure AD paid service for your workforce, we recommend that you use the same tenant again.</span></span>

- <span data-ttu-id="91ca9-167">다음을 계획 중인 경우 Azure Portal에 새 테넌트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-167">We recommend that you use a new tenant in the Azure portal if you are planning to:</span></span>
  - <span data-ttu-id="91ca9-168">다른 사용자 집합(예: 파트너 또는 고객)에 대해 Azure AD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-168">Use Azure AD for a different set of users (such as partners or customers).</span></span>
  - <span data-ttu-id="91ca9-169">프로덕션 서비스와 별개로 Azure AD 서비스를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-169">Evaluate Azure AD services in isolation from your production service.</span></span>
  - <span data-ttu-id="91ca9-170">서비스에 대한 샌드박스 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-170">Set up a sandbox environment for your services.</span></span>

  <span data-ttu-id="91ca9-171">새 디렉터리는 사용자 계정을 전역 관리자 권한이 있는 외부 사용자로 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-171">The new directory is created with your account as an external user with global administrator permissions.</span></span> <span data-ttu-id="91ca9-172">이 계정으로 Azure Portal에 로그인하면 이 테넌트가 표시되며 모든 관리 작업에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-172">When you sign in to the Azure portal with this account, you can see this tenant and access all administration tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="91ca9-173">Azure AD는 “게스트 사용자”를 지원하는데, 이 외부 사용자는 Microsoft 계정 또는 다른 테넌트의 Azure AD ID 중 하나를 통해 생성된 Azure AD 테넌트의 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-173">Azure AD supports “guest users,” which are user accounts in an Azure AD tenant that were created through either a Microsoft account or an Azure AD identity from another tenant.</span></span> <span data-ttu-id="91ca9-174">Office 365 관리 포털은 현재 이러한 사용자를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-174">The Office 365 administration portal does not currently support these users.</span></span> <span data-ttu-id="91ca9-175">Microsoft 계정을 가진 게스트 사용자가 Office 365 관리 포털에 전혀 액세스할 수 없으며 다른 Azure AD 테넌트의 게스트 사용자는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-175">Guest users with Microsoft accounts are not able to access the Office 365 administration portal at all, while guest users from other Azure AD tenants are ignored.</span></span> <span data-ttu-id="91ca9-176">후자의 경우, 사용자의 로컬 계정만 사용자가 원래 만들어진 Azure AD 또는 Office 365 테넌트에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-176">In the latter case, only the user’s local account, in the Azure AD or Office 365 tenant where the user was originally created, is accessible.</span></span>

### <a name="select-one-or-more-license-trials"></a><span data-ttu-id="91ca9-177">하나 이상의 라이선스 평가판 선택</span><span class="sxs-lookup"><span data-stu-id="91ca9-177">Select one or more license trials</span></span>

<span data-ttu-id="91ca9-178">**Azure Active Directory** &gt; **빠른 시작** 아래에서 Azure AD Premium 또는 Enterprise Mobility + Security 평가판 구독을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-178">You can activate an Azure AD Premium or Enterprise Mobility + Security trial subscription under **Azure Active Directory** &gt; **Quick start**.</span></span>

![라이선스 평가판 선택](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

<span data-ttu-id="91ca9-180">평가판 라이선스는 **라이선스** 블레이드에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-180">Trial licenses are available on the **Licenses** blade.</span></span>

### <a name="assign-licenses-to-users-and-groups"></a><span data-ttu-id="91ca9-181">사용자 및 그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="91ca9-181">Assign licenses to users and groups</span></span>

<span data-ttu-id="91ca9-182">구독이 활성화된 후 사용자가 자신에게 라이선스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-182">After the subscription is active, you should assign a license to yourself.</span></span> <span data-ttu-id="91ca9-183">그다음에 브라우저를 새로 고쳐야 모든 기능을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-183">Then refresh the browser to ensure that you are seeing all the features.</span></span> <span data-ttu-id="91ca9-184">다음 단계는 유료 Azure AD 기능에 액세스해야 할 사용자에게 라이선스를 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-184">The next step is to assign licenses to the users who need access to paid Azure AD features.</span></span> <span data-ttu-id="91ca9-185">[라이선스 할당](#assign-licenses)에서 설명된 대로 라이선스를 할당하는 한 가지 간편한 방법은 원하는 대상 그룹을 식별하여 라이선스를 할당하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-185">As described in [Assign licenses](#assign-licenses), one easy way to assign licenses is to identify the group representing the desired audience and assign the license to it.</span></span> <span data-ttu-id="91ca9-186">이 방법으로 수명 주기 동안 그룹에서 추가 또는 제거되는 사용자는 각각 라이선스를 할당받거나 라이선스에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-186">In this way, users who are added or removed from the group over its lifecycle are assigned or removed from the license, respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="91ca9-187">일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-187">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="91ca9-188">사용자에게 라이선스를 할당하려면 먼저 관리자가 해당 사용자에 대해 “**사용 위치**” 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-188">Before a license can be assigned to a user, the administrator must specify the **Usage location** property for the user.</span></span> <span data-ttu-id="91ca9-189">Azure Portal의 **사용자** &gt; **프로필** &gt; **설정**에서 이 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-189">You can set this property under **User** &gt; **Profile** &gt; **Settings** in the Azure portal.</span></span> <span data-ttu-id="91ca9-190">그룹 라이선스 할당을 사용할 때 사용 위치가 지정되지 않은 사용자는 디렉터리의 위치를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-190">When using group license assignment, any user whose usage location is not specified inherits the location of the directory.</span></span>

<span data-ttu-id="91ca9-191">라이선스를 할당하려면 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래에서 제품을 하나 이상 선택하고 명령 모음에서 **할당** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-191">To assign a license, under **Azure Active Directory** &gt; **Licenses** &gt; **All Products**, select one or more products, and then select **Assign** on the command bar.</span></span>

![할당할 라이선스 선택](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

<span data-ttu-id="91ca9-193">**사용자 및 그룹** 블레이드를 사용하여 여러 사용자나 그룹을 선택하거나 제품의 서비스 계획을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-193">You can use the **Users and groups** blade to choose multiple users or groups or to disable service plans in the product.</span></span> <span data-ttu-id="91ca9-194">맨 위에 있는 검색 상자를 사용하여 사용자 및 그룹 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-194">Use the search box on top to search for user and group names.</span></span>

![라이선스 할당을 위한 사용자 또는 그룹 선택](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

<span data-ttu-id="91ca9-196">라이선스를 그룹에 할당할 때는 모든 사용자가 라이선스를 상속하기 전에 그룹에 있는 사용자 수에 따라 다소 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-196">When you're assigning a license to a group, it can take some time before all users inherit the license, depending on the number of users in the group.</span></span> <span data-ttu-id="91ca9-197">**그룹** 블레이드의 **라이선스** 타일 아래에서 처리 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-197">You can check the processing status on the **Group** blade, under the **Licenses** tile.</span></span>

![라이선스 할당 상태](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

<span data-ttu-id="91ca9-199">Azure AD 라이선스 할당 중에 할당 오류가 발생할 수 있지만 Azure AD 및 Enterprise Mobility + Security 제품을 관리할 경우에는 상대적으로 드물게 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-199">Assignment errors can occur during Azure AD license assignment but are relatively rare when managing Azure AD and Enterprise Mobility + Security products.</span></span> <span data-ttu-id="91ca9-200">잠재적 할당 오류는 다음으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-200">Potential assignment errors are limited to:</span></span>
- <span data-ttu-id="91ca9-201">할당 충돌: 사용자에게 이전에 할당된 라이선스가 현재 라이선스와 호환되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="91ca9-201">Assignment conflict: When a user was previously assigned a license that is incompatible with the current license.</span></span> <span data-ttu-id="91ca9-202">이런 경우, 새 라이선스를 할당하려면 현재 라이선스를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-202">In this case, assigning the new license requires removing the current one.</span></span>
- <span data-ttu-id="91ca9-203">사용 가능한 라이선스 수 초과: 할당된 그룹의 사용자 수가 사용 가능한 라이선스 수를 초과한 경우 없는 라이선스로 인해 사용자의 할당 상태가 할당 실패로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-203">Exceeded available licenses: When the number of users in assigned groups exceeds the available licenses, a user's assignment status reflects a failure to assign due to missing licenses.</span></span>

#### <a name="azure-ad-b2b-collaboration-licensing"></a><span data-ttu-id="91ca9-204">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="91ca9-204">Azure AD B2B collaboration licensing</span></span>

<span data-ttu-id="91ca9-205">B2B 공동 작업을 통해 게스트 사용자를 Azure AD 테넌트로 초대해서 Azure AD 서비스 및 사용 가능하게 설정할 Azure 리소스에 대한 액세스 권한을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-205">B2B collaboration allows you to invite guest users into your Azure AD tenant to provide access to Azure AD services and any Azure resources you make available.</span></span>  

<span data-ttu-id="91ca9-206">B2B 사용자를 초대한 후 Azure AD에서 응용 프로그램에 할당하는 과정은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-206">There is no charge for inviting B2B users and assigning them to an application in Azure AD.</span></span> <span data-ttu-id="91ca9-207">게스트 사용자당 최대 10개 앱과 3개의 기본 보고서도 B2B 공동 작업 사용자에게 무료로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-207">Up to 10 apps per guest user and 3 basic reports are also free for B2B collaboration users.</span></span> <span data-ttu-id="91ca9-208">파트너의 Azure AD 테넌트에서 게스트 사용자에게 적절한 라이선스가 할당되어 있으면 여러분의 테넌트에서도 게스트 사용자에게 사용이 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-208">If your guest user has any appropriate licenses assigned in the partner's Azure AD tenant, they'll be licensed in yours as well.</span></span>

<span data-ttu-id="91ca9-209">필수는 아니지만 유료 Azure AD 기능에 대한 액세스 권한을 제공하려면 해당 B2B 게스트 사용자는 적절한 Azure AD 라이선스의 사용 허가를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-209">It's not required, but if you want to provide access to paid Azure AD features, those B2B guest users must be licensed with appropriate Azure AD licenses.</span></span> <span data-ttu-id="91ca9-210">Azure AD 유료 라이선스가 있는 초대하는 테넌트는 테넌트에 초대된 5명의 추가 게스트 사용자에게 B2B 공동 작업 사용자 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-210">An inviting tenant with an Azure AD paid license can assign B2B collaboration user rights to an additional five guest users invited to the tenant.</span></span> <span data-ttu-id="91ca9-211">시나리오와 정보는 [B2B 공동 작업 라이선스 지침](active-directory-b2b-licensing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91ca9-211">For scenarios and information, see [B2B collaboration licensing guidance](active-directory-b2b-licensing.md).</span></span>

### <a name="view-assigned-licenses"></a><span data-ttu-id="91ca9-212">할당된 라이선스 보기</span><span class="sxs-lookup"><span data-stu-id="91ca9-212">View assigned licenses</span></span>

<span data-ttu-id="91ca9-213">할당된 라이선스 및 사용 가능한 라이선스에 대한 요약 보기는 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-213">A summary view of assigned and available licenses is displayed under **Azure Active Directory** &gt; **Licenses** &gt; **All products**.</span></span>

![라이선스 요약 보기](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

<span data-ttu-id="91ca9-215">특정 제품을 선택할 때 사용 가능한 할당된 사용자 및 그룹의 자세한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-215">A detailed list of assigned users and groups is available when selecting a specific product.</span></span> <span data-ttu-id="91ca9-216">**허가된 사용자**에는 현재 라이선스를 사용 중인 모든 사용자와 함께 라이선스가 사용자에게 직접 할당되었는지, 그룹에서 상속되는지 여부가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-216">The **Licensed Users** list shows all users currently consuming a license and whether the license was assigned directly to the user or if it is inherited from a group.</span></span>

![라이선스 세부 정보 보기](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

<span data-ttu-id="91ca9-218">마찬가지로 **허가된 그룹**은 라이선스가 할당된 모든 그룹을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-218">Similarly, the **Licensed Groups** list shows all groups to which licenses have been assigned.</span></span> <span data-ttu-id="91ca9-219">사용자 또는 그룹을 선택하면 해당 개체에 할당된 모든 라이선스를 보여 주는 **라이선스** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-219">Select a user or group to open the **Licenses** blade, which shows all licenses assigned to that object.</span></span>

### <a name="remove-a-license"></a><span data-ttu-id="91ca9-220">라이선스 제거</span><span class="sxs-lookup"><span data-stu-id="91ca9-220">Remove a license</span></span>

<span data-ttu-id="91ca9-221">라이선스를 제거하려면 사용자 또는 그룹으로 이동하고 **라이선스** 타일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-221">To remove a license, go to the user or group, and open the **Licenses** tile.</span></span> <span data-ttu-id="91ca9-222">라이선스를 선택하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-222">Select the license, and click **Remove**.</span></span>

![라이선스 제거](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

<span data-ttu-id="91ca9-224">그룹에서 사용자에 상속된 라이선스는 직접 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-224">Licenses inherited by the user from a group cannot be removed directly.</span></span> <span data-ttu-id="91ca9-225">대신, 라이선스를 상속하는 그룹에서 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-225">Instead, remove the user from the group from which they are inheriting the license.</span></span>

### <a name="extend-trials"></a><span data-ttu-id="91ca9-226">평가판 연장</span><span class="sxs-lookup"><span data-stu-id="91ca9-226">Extend trials</span></span>

<span data-ttu-id="91ca9-227">고객에 대한 평가판 연장은 Office 365 포털을 통해 셀프 서비스 등록으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-227">Trial extensions for customers are available as self-service sign-up through the Office 365 portal.</span></span> <span data-ttu-id="91ca9-228">고객 관리자가 Office 포털(Office 포털에 대한 사용 권한에 따라 액세스 권한이 달라짐)로 이동하여 사용자의 Azure AD Premium 평가판을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-228">A customer admin can go to the Office portal (access depends on permissions for the Office portal) and select the Azure AD Premium trial.</span></span> <span data-ttu-id="91ca9-229">**평가판 확장** 링크를 클릭하면 확장 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-229">Clicking the **Extend trial** link starts the extension process.</span></span> <span data-ttu-id="91ca9-230">신용 카드가 필요하지만 요금이 부과되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-230">A credit card is required, but it is not charged.</span></span>

![Azure Portal에서 평가판 연장](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a><span data-ttu-id="91ca9-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91ca9-232">Next steps</span></span>

<span data-ttu-id="91ca9-233">그룹을 통해 라이선스를 관리하는 고급 시나리오에 대해 자세히 알아보려면 [그룹에 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md) 문서를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="91ca9-233">To learn more about advanced scenarios for license management through groups, read the article [Assigning licenses to a group](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

<span data-ttu-id="91ca9-234">다른 Azure AD 유료 기능을 구성 및 사용하는 방법에 대한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91ca9-234">Here's information about how to configure and use other Azure AD paid features:</span></span>

* [<span data-ttu-id="91ca9-235">셀프 서비스 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="91ca9-235">Self-service password reset</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="91ca9-236">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="91ca9-236">Self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="91ca9-237">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="91ca9-237">Azure AD Connect health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="91ca9-238">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="91ca9-238">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="91ca9-239">Azure AD Premium 라이선스 직접 구매</span><span class="sxs-lookup"><span data-stu-id="91ca9-239">Direct purchase of Azure AD Premium licenses</span></span>](http://aka.ms/buyaadp)
