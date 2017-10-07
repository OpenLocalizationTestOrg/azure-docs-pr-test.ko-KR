---
title: "Azure Active Directory에서 라이선스를 사용한 aaaGet 시작 | Microsoft Docs"
description: "Azure Active Directory 라이선스 작동 방식 tooget를 어떻게 시작 모범 사례"
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
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a><span data-ttu-id="1e81d-104">Azure Active Directory에서 사용자 본인 및 사용자의 사용자 라이선스</span><span class="sxs-lookup"><span data-stu-id="1e81d-104">License yourself and your users in Azure Active Directory</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e81d-105">Azure Portal 지침</span><span class="sxs-lookup"><span data-stu-id="1e81d-105">Azure portal instructions</span></span>](active-directory-licensing-get-started-azure-portal.md)
> * [<span data-ttu-id="1e81d-106">Azure 클래식 포털 정보</span><span class="sxs-lookup"><span data-stu-id="1e81d-106">Get Azure classic portal info</span></span>](active-directory-licensing-what-is.md)
>
>

<span data-ttu-id="1e81d-107">Azure AD(Azure Active Directory)는 Microsoft의 IDaaS(Identity as a Service) 솔루션 및 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-107">Azure Active Directory (Azure AD) is an identity as a service (IDaaS) solution and platform from Microsoft.</span></span> <span data-ttu-id="1e81d-108">Azure AD는 다양한 서비스 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-108">Azure AD is offered in different service editions:</span></span>

* <span data-ttu-id="1e81d-109">Azure Active Directory Free - Office 365, Dynamics, Microsoft Intune 또는 Azure와 같은 Microsoft 서비스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-109">Azure Active Directory Free, which is available with any Microsoft service such as Office 365, Dynamics, Microsoft Intune, or Azure.</span></span> <span data-ttu-id="1e81d-110">Azure AD는 이 모드에서 사용량 요금을 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-110">Azure AD does not generate any consumption charges in this mode.</span></span>

* <span data-ttu-id="1e81d-111">Azure AD 유료 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-111">Azure AD paid editions, such as:</span></span>
  - <span data-ttu-id="1e81d-112">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="1e81d-112">Enterprise Mobility + Security</span></span> 
  - <span data-ttu-id="1e81d-113">Azure AD Premium(P1 및 P2)</span><span class="sxs-lookup"><span data-stu-id="1e81d-113">Azure AD Premium (P1 and P2)</span></span>
  - <span data-ttu-id="1e81d-114">Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="1e81d-114">Azure AD Basic</span></span>
  - <span data-ttu-id="1e81d-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="1e81d-115">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="1e81d-116">많은 Microsoft 온라인 서비스와 마찬가지로 대부분의 Azure AD 유료 버전은 Office 365, Microsoft Intune 및 Azure AD에서 사용자별 권한 부여를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-116">Like many of Microsoft online services, most Azure AD paid versions are delivered through per-user entitlements as they are in Office 365, Microsoft Intune, and Azure AD.</span></span> <span data-ttu-id="1e81d-117">이러한 경우 하나 이상의 구독 hello 서비스 구매 표시 되 고 각 구독 테 넌 트의 몇 가지 prepurchased 라이선스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-117">In these cases, hello service purchase is represented by one or more subscriptions, and each subscription includes some prepurchased licenses in your tenant.</span></span> <span data-ttu-id="1e81d-118">사용자 단위 자격은 다음을 통해 취득합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-118">Per-user entitlements are achieved by:</span></span>

* <span data-ttu-id="1e81d-119">라이선스 할당.</span><span class="sxs-lookup"><span data-stu-id="1e81d-119">Assigning a license.</span></span> 
* <span data-ttu-id="1e81d-120">Hello 사용자와 hello 제품 간의 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-120">Creating a link between hello user and hello product.</span></span>
* <span data-ttu-id="1e81d-121">Hello 사용자에 대 한 hello 서비스 구성 요소를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-121">Enabling hello service components for hello user.</span></span>
* <span data-ttu-id="1e81d-122">라이선스 선불 hello 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-122">Consuming one of hello prepaid licenses.</span></span>

[<span data-ttu-id="1e81d-123">이제 Azure AD premium을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-123">Try Azure AD Premium now.</span></span>](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

<span data-ttu-id="1e81d-124">Azure AD 서비스 기능에 대한 광범위한 개요는 [Azure AD란?](active-directory-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e81d-124">For a broad overview of Azure AD service capabilities, see [What is Azure AD?](active-directory-whatis.md).</span></span> <span data-ttu-id="1e81d-125">자세한 내용은 [Azure Active Directory에 대한 SLA](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e81d-125">For more information, see our [Service Level Agreements page](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).</span></span>

> [!NOTE]
> <span data-ttu-id="1e81d-126">Azure 리소스를 만들 수 있도록 하 고 tooyour 지불 메서드 매핑할 azure 종 량 제 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-126">Azure pay-as-you-go subscriptions enable creation of Azure resources and then map them tooyour payment method.</span></span> <span data-ttu-id="1e81d-127">Hello 구독과 관련 된 없는 라이선스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-127">There are no license counts associated with hello subscription.</span></span> <span data-ttu-id="1e81d-128">Azure 리소스에 사용자 권한 toooperate 매핑된 toohello 구독에 부여 된 hello 구독에 연결 되며 구독 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-128">When you grant a user permission toooperate on Azure resources mapped toohello subscription, they are associated with hello subscription and can manage subscription resources.</span></span>

## <a name="how-does-azure-active-directory-licensing-work"></a><span data-ttu-id="1e81d-129">Azure Active Directory 라이선스는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="1e81d-129">How does Azure Active Directory licensing work?</span></span>

<span data-ttu-id="1e81d-130">라이선스 기반 Azure AD 서비스는 Azure AD 서비스 테넌트에서 구독을 활성화하면 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-130">License-based Azure AD services work by activating a subscription in your Azure AD service tenant.</span></span> <span data-ttu-id="1e81d-131">Hello 구독이 활성 상태 이면 hello 서비스 기능이 Azure AD 관리자가 관리 되 고 사용이 허가 된 사용자가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-131">After hello subscription is active, hello service capabilities are managed by Azure AD administrators and used by licensed users.</span></span>

### <a name="manage-subscription-information"></a><span data-ttu-id="1e81d-132">구독 정보 관리</span><span class="sxs-lookup"><span data-stu-id="1e81d-132">Manage subscription information</span></span>

<span data-ttu-id="1e81d-133">Enterprise Mobility + 보안, Azure AD Premium 또는 Azure AD Basic에서는 테 넌 트을 구입할 때 선불 라이선스로 hello 구독에서 유효 기간을 포함 하 여 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-133">When you purchase Enterprise Mobility + Security, Azure AD Premium, or Azure AD Basic, your tenant is updated with hello subscription, including its validity period and prepaid licenses.</span></span> <span data-ttu-id="1e81d-134">Hello 할당 또는 사용 가능한 라이선스 수를 포함 하 여 구독 정보는 hello Azure 포털을 통해 사용할 수 있는: 아래 **Azure Active Directory**개방형 hello **라이선스** hello에 대 한 바둑판식으로 배열 특정 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-134">Your subscription information, including hello number of assigned or available licenses, is available through hello Azure portal: Under **Azure Active Directory**, open hello **Licenses** tile for hello specific directory.</span></span> <span data-ttu-id="1e81d-135">hello **라이선스** 블레이드 최상의 위치 toomanage 라이선스 할당 hello도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-135">hello **Licenses** blade is also hello best place toomanage your license assignments.</span></span>

<span data-ttu-id="1e81d-136">각 구독은 Azure AD, Multi-Factor Authentication, Intune, Exchange Online 또는 SharePoint Online과 같은 하나 이상의 서비스 계획으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-136">Each subscription consists of one or more service plans, such as Azure AD, Multi-Factor Authentication, Intune, Exchange Online, or SharePoint Online.</span></span>  <span data-ttu-id="1e81d-137">Azure AD 라이선스 관리에는 서비스 계획 수준 관리가 필요하지 *않습니다*.</span><span class="sxs-lookup"><span data-stu-id="1e81d-137">Azure AD license management does *not* require service-plan-level management.</span></span> <span data-ttu-id="1e81d-138">Office 365는이 고급 구성 모드 toomanage 액세스 tooincluded 서비스에 사용 하기 때문에 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-138">Office 365 differs because it relies on this advanced configuration mode toomanage access tooincluded services.</span></span> <span data-ttu-id="1e81d-139">Azure AD는 in service 구성 tooenable 기능을 사용 하 고 개별 사용 권한을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-139">Azure AD relies on in-service configuration tooenable features and manage individual permissions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e81d-140">Azure AD Premium, Azure AD Basic 및 Enterprise Mobility + 보안 서비스는 사용자를 프로 비전 예외일된 tootheir 디렉터리/테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="1e81d-140">Azure AD Premium, Azure AD Basic, and Enterprise Mobility + Security subscriptions are confined tootheir provisioned directory/tenant.</span></span> <span data-ttu-id="1e81d-141">디렉터리나 다른 디렉터리에서 사용 되는 tooentitle 사용자 사이의 구독을 분할할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-141">Subscriptions cannot be split between directories or used tooentitle users in other directories.</span></span> <span data-ttu-id="1e81d-142">구독을 디렉터리 간에 이동하는 것은 가능하지만 지원 티켓을 제출하거나, 직접 구매의 경우 취소 후 다시 구매해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-142">Moving a subscription between directories is possible, but requires submitting a support ticket, or cancellation and repurchase for direct purchases.</span></span>
>
> <span data-ttu-id="1e81d-143">때 Azure AD 또는 볼륨 라이선스 구독을 통해 구매한 Enterprise Mobility + 보안 및 활성화가 자동으로 수행 hello 계약 다른 Microsoft Online 서비스 (예를 들어 Office 365)에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-143">When Azure AD or Enterprise Mobility + Security is purchased through a Volume Licensing subscription, and when hello agreement includes other Microsoft Online services (for example, Office 365), activation happens automatically.</span></span> 

### <a name="assign-licenses"></a><span data-ttu-id="1e81d-144">라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="1e81d-144">Assign licenses</span></span>

<span data-ttu-id="1e81d-145">경우에 구독을 가져오는 모든 필요한 기능을 유료 tooconfigure 기능 toousers 유료 Azure AD에 대 한 라이선스를 계속 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-145">Although obtaining a subscription is all you need tooconfigure paid capabilities, you must still distribute licenses for Azure AD paid features toousers.</span></span> <span data-ttu-id="1e81d-146">Azure AD 유료 기능을 통해 관리 되는 액세스 tooor 가져야 하는 모든 사용자 라이선스를 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-146">Any user who should have access tooor who is managed through an Azure AD paid feature must be assigned a license.</span></span> <span data-ttu-id="1e81d-147">라이선스 할당은 Azure AD Premium, Basic 또는 Enterprise Mobility + Security 등의 구매한 서비스와 사용자 간의 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-147">License assignment is a mapping between a user and a purchased service, such as Azure AD Premium, Basic, or Enterprise Mobility + Security.</span></span>


<span data-ttu-id="1e81d-148">디렉터리의 어떤 사용자에게 라이선스가 있어야 하는지 관리하려면 다음 작업을 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-148">Managing which users in your directory should have a license can be accomplished by:</span></span> 

* <span data-ttu-id="1e81d-149">Toogroups hello에 라이선스 할당 [Azure 포털](active-directory-licensing-whatis-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-149">Assigning licenses toogroups in hello [Azure portal](active-directory-licensing-whatis-azure-portal.md).</span></span>
* <span data-ttu-id="1e81d-150">Toousers hello 포털, PowerShell 또는 Api를 통해 직접 라이선스를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-150">Assigning licenses directly toousers by way of hello portal, PowerShell, or APIs.</span></span> 

<span data-ttu-id="1e81d-151">라이선스 tooa 그룹을 할당 하는 모든 그룹 구성원 라이선스가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-151">When you're assigning licenses tooa group, all group members are assigned a license.</span></span> <span data-ttu-id="1e81d-152">사용자가 더하거나 hello 그룹에서 제거 하는 경우에 hello 적절 한 라이선스 할당 하거나 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-152">If users are added or removed from hello group, hello appropriate license is assigned or removed.</span></span> <span data-ttu-id="1e81d-153">그룹 할당 된 그룹 관리 사용 가능한 tooyou 활용할 수 있습니다 및 그룹 기반 할당 tooapplications와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-153">Group assignment can utilize any group management available tooyou, and it is consistent with group-based assignment tooapplications.</span></span>

<span data-ttu-id="1e81d-154">사용할 수 있습니다 [그룹 기반의 라이선스 할당](active-directory-licensing-whatis-azure-portal.md) hello 다음과 같은 규칙을 tooset:</span><span class="sxs-lookup"><span data-stu-id="1e81d-154">You can use [group-based license assignment](active-directory-licensing-whatis-azure-portal.md) tooset up rules such as hello following:</span></span>
* <span data-ttu-id="1e81d-155">디렉터리의 모든 사용자가 자동으로 라이선스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-155">All users in your directory automatically get a license</span></span>
* <span data-ttu-id="1e81d-156">Hello 적절 한 직책을 가진 모든 사람에 게 라이선스</span><span class="sxs-lookup"><span data-stu-id="1e81d-156">Everyone with hello appropriate job title gets a license</span></span>
* <span data-ttu-id="1e81d-157">Hello 조직에서 hello 의사 결정 tooother 관리자를 위임할 수 있습니다 (사용 하 여 [셀프 서비스 그룹](active-directory-accessmanagement-self-service-group-management.md))</span><span class="sxs-lookup"><span data-stu-id="1e81d-157">You can delegate hello decision tooother managers in hello organization (by using [self-service groups](active-directory-accessmanagement-self-service-group-management.md))</span></span>

<span data-ttu-id="1e81d-158">라이선스 할당 toogroups, 대 한 자세한 내용은 포함 하 여 고급 시나리오 및 Office 365 라이선스 시나리오 참조 [toousers Azure Active Directory 그룹 멤버 자격을 통해 라이선스를 할당](active-directory-licensing-group-assignment-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-158">For a detailed discussion of license assignment toogroups, including advanced scenarios and Office 365 licensing scenarios, see [Assign licenses toousers by group membership in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

## <a name="get-started-with-azure-ad-licensing"></a><span data-ttu-id="1e81d-159">Azure AD 라이선스 시작</span><span class="sxs-lookup"><span data-stu-id="1e81d-159">Get started with Azure AD licensing</span></span>

<span data-ttu-id="1e81d-160">Azure AD를 시작하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-160">Getting started with Azure AD is easy.</span></span> <span data-ttu-id="1e81d-161">언제든지 [Azure 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) 등록의 일부로 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-161">You can always create your directory as a part of signing up for an [Azure free trial](https://azure.microsoft.com/offers/ms-azr-0044p/).</span></span>

<span data-ttu-id="1e81d-162">hello 다음 모범 사례 보장할 수 있습니다 hello 서비스에 대 한 목표와 있습니다를 사용 하는 다른 Microsoft 서비스와 테 넌 트 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-162">hello following best practices can help ensure that your tenant is aligned with other Microsoft services you might be consuming and with your goals for hello service:</span></span>

- <span data-ttu-id="1e81d-163">이미 사용 하는 Microsoft에서 조직 서비스 hello, 이미 있는 경우 Azure AD 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-163">If you are already using any of hello organizational services from Microsoft, you already have an Azure AD tenant.</span></span> <span data-ttu-id="1e81d-164">것이 유용한 toouse hello 동일한 테 넌 트 다른 서비스에 대 한 프로 비전을 포함 하 여 핵심 id 관리 및 하이브리드 single sign on (SSO) hello 서비스에서 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-164">It is useful toouse hello same tenant for other services so that core identity management, including provisioning and hybrid single sign-on (SSO), can be used across hello services.</span></span> <span data-ttu-id="1e81d-165">Single sign-on을 사용자에 게는 hello 서비스 전반에 걸쳐 hello 다양 한 기능에서 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-165">With single sign-on, your users benefit from hello rich capabilities across hello services.</span></span> <span data-ttu-id="1e81d-166">따라서 toobuy 직원에 대 한 Azure AD 유료 서비스를 결정 하는 경우 다시 테 넌 동일 hello를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-166">Thus, if you decide toobuy an Azure AD paid service for your workforce, we recommend that you use hello same tenant again.</span></span>

- <span data-ttu-id="1e81d-167">계획인 경우 hello Azure 포털에서에서 새 테 넌 트에 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-167">We recommend that you use a new tenant in hello Azure portal if you are planning to:</span></span>
  - <span data-ttu-id="1e81d-168">다른 사용자 집합(예: 파트너 또는 고객)에 대해 Azure AD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-168">Use Azure AD for a different set of users (such as partners or customers).</span></span>
  - <span data-ttu-id="1e81d-169">프로덕션 서비스와 별개로 Azure AD 서비스를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-169">Evaluate Azure AD services in isolation from your production service.</span></span>
  - <span data-ttu-id="1e81d-170">서비스에 대한 샌드박스 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-170">Set up a sandbox environment for your services.</span></span>

  <span data-ttu-id="1e81d-171">전역 관리자 권한이 있는 외부 사용자로 계정을 사용 하 여 hello 새 디렉터리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-171">hello new directory is created with your account as an external user with global administrator permissions.</span></span> <span data-ttu-id="1e81d-172">Toohello이이 계정 사용 하 여 Azure 포털에 로그인 할 때이 테 넌이 트를 보고 모든 관리 작업에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-172">When you sign in toohello Azure portal with this account, you can see this tenant and access all administration tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="1e81d-173">Azure AD는 “게스트 사용자”를 지원하는데, 이 외부 사용자는 Microsoft 계정 또는 다른 테넌트의 Azure AD ID 중 하나를 통해 생성된 Azure AD 테넌트의 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-173">Azure AD supports “guest users,” which are user accounts in an Azure AD tenant that were created through either a Microsoft account or an Azure AD identity from another tenant.</span></span> <span data-ttu-id="1e81d-174">hello Office 365 관리 포털은 이러한 사용자를 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-174">hello Office 365 administration portal does not currently support these users.</span></span> <span data-ttu-id="1e81d-175">Microsoft 계정 가진 사용자가 게스트 수 tooaccess hello Office 365 관리 포털, 동안 없는 다른 Azure AD 테 넌 트의 게스트 사용자는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-175">Guest users with Microsoft accounts are not able tooaccess hello Office 365 administration portal at all, while guest users from other Azure AD tenants are ignored.</span></span> <span data-ttu-id="1e81d-176">Hello 후자의 경우에만 hello Azure AD에서에서 사용자의 로컬 계정 hello 되었거나 여기서 hello 사용자가 원래 만들어진 Office 365 테 넌 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-176">In hello latter case, only hello user’s local account, in hello Azure AD or Office 365 tenant where hello user was originally created, is accessible.</span></span>

### <a name="select-one-or-more-license-trials"></a><span data-ttu-id="1e81d-177">하나 이상의 라이선스 평가판 선택</span><span class="sxs-lookup"><span data-stu-id="1e81d-177">Select one or more license trials</span></span>

<span data-ttu-id="1e81d-178">**Azure Active Directory** &gt; **빠른 시작** 아래에서 Azure AD Premium 또는 Enterprise Mobility + Security 평가판 구독을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-178">You can activate an Azure AD Premium or Enterprise Mobility + Security trial subscription under **Azure Active Directory** &gt; **Quick start**.</span></span>

![라이선스 평가판 선택](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

<span data-ttu-id="1e81d-180">Hello에 사용할 수 있는 평가판 라이선스 **라이선스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-180">Trial licenses are available on hello **Licenses** blade.</span></span>

### <a name="assign-licenses-toousers-and-groups"></a><span data-ttu-id="1e81d-181">라이선스 toousers 및 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="1e81d-181">Assign licenses toousers and groups</span></span>

<span data-ttu-id="1e81d-182">Hello 구독이 활성 상태 이면 후 라이선스 tooyourself를 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-182">After hello subscription is active, you should assign a license tooyourself.</span></span> <span data-ttu-id="1e81d-183">Hello 브라우저 tooensure를 hello 기능을 모두 표시를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-183">Then refresh hello browser tooensure that you are seeing all hello features.</span></span> <span data-ttu-id="1e81d-184">hello 다음 단계 toopaid Azure AD 기능에 액세스 해야 하는 tooassign 라이선스 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-184">hello next step is tooassign licenses toohello users who need access toopaid Azure AD features.</span></span> <span data-ttu-id="1e81d-185">에 설명 된 대로 [라이선스 할당](#assign-licenses), tooidentify hello hello 나타내는 필요 청중 그룹과 할당 hello 라이선스 tooit tooassign 라이선스는 한 가지 쉬운 방법은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-185">As described in [Assign licenses](#assign-licenses), one easy way tooassign licenses is tooidentify hello group representing hello desired audience and assign hello license tooit.</span></span> <span data-ttu-id="1e81d-186">이러한 방식으로 수명 주기 동안 hello 그룹에서 제거 되거나 추가 된 사용자를은 할당 되거나 각각 hello 라이선스에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-186">In this way, users who are added or removed from hello group over its lifecycle are assigned or removed from hello license, respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="1e81d-187">일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-187">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="1e81d-188">관리자에 게 hello를 지정 해야 tooa 사용자 라이선스를 할당할 수 있습니다, 전에 **사용 위치** hello 사용자에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="1e81d-188">Before a license can be assigned tooa user, hello administrator must specify hello **Usage location** property for hello user.</span></span> <span data-ttu-id="1e81d-189">이 속성을 설정할 수 있습니다 **사용자** &gt; **프로필** &gt; **설정을** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="1e81d-189">You can set this property under **User** &gt; **Profile** &gt; **Settings** in hello Azure portal.</span></span> <span data-ttu-id="1e81d-190">그룹 라이선스 할당을 사용할 경우 사용 위치가 지정 되지 않은 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-190">When using group license assignment, any user whose usage location is not specified inherits hello location of hello directory.</span></span>

<span data-ttu-id="1e81d-191">tooassign 라이선스 아래에서 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품**하나 이상의 제품을 선택한 다음 선택 **할당** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-191">tooassign a license, under **Azure Active Directory** &gt; **Licenses** &gt; **All Products**, select one or more products, and then select **Assign** on hello command bar.</span></span>

![라이선스 tooassign 선택](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

<span data-ttu-id="1e81d-193">Hello를 사용할 수 있습니다 **사용자 및 그룹** 블레이드 toochoose hello 제품의 여러 사용자 또는 그룹 또는 toodisable 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-193">You can use hello **Users and groups** blade toochoose multiple users or groups or toodisable service plans in hello product.</span></span> <span data-ttu-id="1e81d-194">사용자 및 그룹 이름에 대 한 상위 toosearch에 hello 검색 상자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-194">Use hello search box on top toosearch for user and group names.</span></span>

![라이선스 할당을 위한 사용자 또는 그룹 선택](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

<span data-ttu-id="1e81d-196">라이선스 tooa 그룹을 할당 하는 경우 모든 사용자가 상속 hello hello 그룹의 사용자 수에 따라 hello 라이선스 되기까지 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-196">When you're assigning a license tooa group, it can take some time before all users inherit hello license, depending on hello number of users in hello group.</span></span> <span data-ttu-id="1e81d-197">Hello에 hello 처리 상태를 확인할 수 **그룹** hello 아래 블레이드 **라이선스** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-197">You can check hello processing status on hello **Group** blade, under hello **Licenses** tile.</span></span>

![라이선스 할당 상태](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

<span data-ttu-id="1e81d-199">Azure AD 라이선스 할당 중에 할당 오류가 발생할 수 있지만 Azure AD 및 Enterprise Mobility + Security 제품을 관리할 경우에는 상대적으로 드물게 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-199">Assignment errors can occur during Azure AD license assignment but are relatively rare when managing Azure AD and Enterprise Mobility + Security products.</span></span> <span data-ttu-id="1e81d-200">잠재적 할당 오류는 다음으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-200">Potential assignment errors are limited to:</span></span>
- <span data-ttu-id="1e81d-201">할당 충돌: 사용자 hello 현재 라이선스와 호환 되지 않는 라이선스를 이전에 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-201">Assignment conflict: When a user was previously assigned a license that is incompatible with hello current license.</span></span> <span data-ttu-id="1e81d-202">이 경우 hello 새 라이선스를 할당 합니다. 현재 hello를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-202">In this case, assigning hello new license requires removing hello current one.</span></span>
- <span data-ttu-id="1e81d-203">사용 가능한 라이선스를 초과 했습니다: 사용자의 할당 상태가 반영 toomissing 라이선스 기한 오류 tooassign hello 할당 된 그룹에 사용자 수가 hello 사용 가능한 라이선스를 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-203">Exceeded available licenses: When hello number of users in assigned groups exceeds hello available licenses, a user's assignment status reflects a failure tooassign due toomissing licenses.</span></span>

#### <a name="azure-ad-b2b-collaboration-licensing"></a><span data-ttu-id="1e81d-204">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="1e81d-204">Azure AD B2B collaboration licensing</span></span>

<span data-ttu-id="1e81d-205">B2B 공동 작업 tooinvite 게스트 사용자에 게 Azure AD 테 넌 트 tooprovide 액세스 tooAzure AD 서비스에 및 있습니다 사용할 수 있도록 모든 Azure 리소스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-205">B2B collaboration allows you tooinvite guest users into your Azure AD tenant tooprovide access tooAzure AD services and any Azure resources you make available.</span></span>  

<span data-ttu-id="1e81d-206">무료 B2B 사용자 초대 및 Azure AD에서 응용 프로그램 tooan를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-206">There is no charge for inviting B2B users and assigning them tooan application in Azure AD.</span></span> <span data-ttu-id="1e81d-207">게스트 당 too10 앱을 사용자와 3 기본 보고서는 B2B 공동 작업 사용자에 게 무료로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-207">Up too10 apps per guest user and 3 basic reports are also free for B2B collaboration users.</span></span> <span data-ttu-id="1e81d-208">게스트 사용자 hello 파트너의 Azure AD 테 넌 트에 할당 된 적절 한 라이선스가 있으면은 합니다 라이선스를 취득 내용에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-208">If your guest user has any appropriate licenses assigned in hello partner's Azure AD tenant, they'll be licensed in yours as well.</span></span>

<span data-ttu-id="1e81d-209">필요 하지는 않지만 tooprovide 액세스 toopaid Azure AD 기능을 사용 하도록 하려는 경우 이러한 B2B 게스트 사용자에 게 사용 허가 받아야 적절 한 Azure AD 라이선스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-209">It's not required, but if you want tooprovide access toopaid Azure AD features, those B2B guest users must be licensed with appropriate Azure AD licenses.</span></span> <span data-ttu-id="1e81d-210">라이선스를 지불 하는 Azure AD와 테 넌 트 초대 B2B 공동 작업 사용자 권한 초대 tooan 추가 5 게스트 사용자에 게 할당할 수 toohello 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-210">An inviting tenant with an Azure AD paid license can assign B2B collaboration user rights tooan additional five guest users invited toohello tenant.</span></span> <span data-ttu-id="1e81d-211">시나리오와 정보는 [B2B 공동 작업 라이선스 지침](active-directory-b2b-licensing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e81d-211">For scenarios and information, see [B2B collaboration licensing guidance](active-directory-b2b-licensing.md).</span></span>

### <a name="view-assigned-licenses"></a><span data-ttu-id="1e81d-212">할당된 라이선스 보기</span><span class="sxs-lookup"><span data-stu-id="1e81d-212">View assigned licenses</span></span>

<span data-ttu-id="1e81d-213">할당된 라이선스 및 사용 가능한 라이선스에 대한 요약 보기는 **Azure Active Directory** &gt; **라이선스** &gt; **모든 제품** 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-213">A summary view of assigned and available licenses is displayed under **Azure Active Directory** &gt; **Licenses** &gt; **All products**.</span></span>

![라이선스 요약 보기](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

<span data-ttu-id="1e81d-215">특정 제품을 선택할 때 사용 가능한 할당된 사용자 및 그룹의 자세한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-215">A detailed list of assigned users and groups is available when selecting a specific product.</span></span> <span data-ttu-id="1e81d-216">hello **사용이 허가 된 사용자가** 목록 현재 사용 하는 라이선스 및 여부 hello 라이선스가 할당 된 직접 toohello 사용자 또는 그룹에서 상속 하는 모든 사용자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-216">hello **Licensed Users** list shows all users currently consuming a license and whether hello license was assigned directly toohello user or if it is inherited from a group.</span></span>

![라이선스 세부 정보 보기](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

<span data-ttu-id="1e81d-218">마찬가지로, hello **사용이 허가 된 그룹** 목록 toowhich 라이선스 할당 된 모든 그룹이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-218">Similarly, hello **Licensed Groups** list shows all groups toowhich licenses have been assigned.</span></span> <span data-ttu-id="1e81d-219">사용자 또는 그룹 tooopen hello 선택 **라이선스** 모든 라이선스를 보여 주는 블레이드 toothat 개체를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-219">Select a user or group tooopen hello **Licenses** blade, which shows all licenses assigned toothat object.</span></span>

### <a name="remove-a-license"></a><span data-ttu-id="1e81d-220">라이선스 제거</span><span class="sxs-lookup"><span data-stu-id="1e81d-220">Remove a license</span></span>

<span data-ttu-id="1e81d-221">에 게 라이선스를 tooremove toohello 사용자 또는 그룹을 이동한 hello **라이선스** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-221">tooremove a license, go toohello user or group, and open hello **Licenses** tile.</span></span> <span data-ttu-id="1e81d-222">Hello 라이선스를 선택 하 고 클릭 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-222">Select hello license, and click **Remove**.</span></span>

![라이선스 제거](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

<span data-ttu-id="1e81d-224">라이선스 그룹에서 hello 사용자가 상속 직접 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-224">Licenses inherited by hello user from a group cannot be removed directly.</span></span> <span data-ttu-id="1e81d-225">대신, hello 라이선스 상속 되는지은 hello 그룹에서 hello 사용자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-225">Instead, remove hello user from hello group from which they are inheriting hello license.</span></span>

### <a name="extend-trials"></a><span data-ttu-id="1e81d-226">평가판 연장</span><span class="sxs-lookup"><span data-stu-id="1e81d-226">Extend trials</span></span>

<span data-ttu-id="1e81d-227">고객에 대 한 평가판 확장을 사용할 수로 셀프 서비스 hello Office 365 포털을 통해 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-227">Trial extensions for customers are available as self-service sign-up through hello Office 365 portal.</span></span> <span data-ttu-id="1e81d-228">고객 관리자 toohello Office 포털을 이동할 수 있습니다 (액세스 hello Office 포털에 대 한 권한을에 따라 다름) hello Azure AD Premium 평가판을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-228">A customer admin can go toohello Office portal (access depends on permissions for hello Office portal) and select hello Azure AD Premium trial.</span></span> <span data-ttu-id="1e81d-229">클릭 하 여 hello **평가판 확장** 링크 hello 확장 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-229">Clicking hello **Extend trial** link starts hello extension process.</span></span> <span data-ttu-id="1e81d-230">신용 카드가 필요하지만 요금이 부과되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-230">A credit card is required, but it is not charged.</span></span>

![Hello Azure 포털에서에서 평가판을 확장 합니다.](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a><span data-ttu-id="1e81d-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e81d-232">Next steps</span></span>

<span data-ttu-id="1e81d-233">hello 문서를 읽기에 대해 더 알아봅니다 toolearn 고급 그룹을 통해 라이선스 관리에 대 한 시나리오 [할당 라이선스 tooa 그룹](active-directory-licensing-group-assignment-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e81d-233">toolearn more about advanced scenarios for license management through groups, read hello article [Assigning licenses tooa group](active-directory-licensing-group-assignment-azure-portal.md).</span></span>

<span data-ttu-id="1e81d-234">다음 방법에 대 한 정보를은 tooconfigure 다른 Azure AD 유료 기능을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1e81d-234">Here's information about how tooconfigure and use other Azure AD paid features:</span></span>

* [<span data-ttu-id="1e81d-235">셀프 서비스 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="1e81d-235">Self-service password reset</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="1e81d-236">셀프 서비스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="1e81d-236">Self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
* [<span data-ttu-id="1e81d-237">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="1e81d-237">Azure AD Connect health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="1e81d-238">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="1e81d-238">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="1e81d-239">Azure AD Premium 라이선스 직접 구매</span><span class="sxs-lookup"><span data-stu-id="1e81d-239">Direct purchase of Azure AD Premium licenses</span></span>](http://aka.ms/buyaadp)
