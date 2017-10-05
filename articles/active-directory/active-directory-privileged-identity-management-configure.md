---
title: "Azure AD Privileged Identity Management 구성 | Microsoft Docs"
description: "Azure AD Privileged Identity Management가 무엇이고 클라우드 보안을 개선하기 위한 PIM 사용 방법을 설명하는 항목입니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: eb7059368cb80be7dd625f9dc6ad2aab1bad709a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a><span data-ttu-id="0273f-103">Azure AD Privileged Identity Management란?</span><span class="sxs-lookup"><span data-stu-id="0273f-103">What is Azure AD Privileged Identity Management?</span></span>
<span data-ttu-id="0273f-104">Azure Active Directory(AD) Privileged Identity Management를 사용하여 조직 내에서 액세스를 관리, 제어 및 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="0273f-105">Azure AD의 리소스 및 Office 365 또는 Microsoft Intune과 같은 다른 Microsoft 온라인 서비스에 대한 액세스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-105">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

> [!NOTE]
> <span data-ttu-id="0273f-106">Privileged Identity Management는 Premium P2 버전의 Azure Active Directory로 관리자에게 사용을 허가할 때 전체 조직에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-106">Privileged Identity Management is available to your entire organization when you license your Administrators with the Premium P2 edition of Azure Active Directory.</span></span> <span data-ttu-id="0273f-107">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0273f-107">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

<span data-ttu-id="0273f-108">조직에서는 악의적인 사용자가 해당 액세스 권한을 갖게 될 가능성을 줄일 수 있기 때문에 보안 정보 또는 리소스에 액세스하는 사용자 수를 최소화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-108">Organizations want to minimize the number of people who have access to secure information or resources, because that reduces the chance of a malicious user getting that access.</span></span> <span data-ttu-id="0273f-109">하지만, 사용자는 여전히 Azure, Office 365 또는 SaaS 앱에서 권한 있는 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-109">However, users still need to carry out privileged operations in Azure, Office 365, or SaaS apps.</span></span> <span data-ttu-id="0273f-110">조직은 사용자에게 Azure AD에서 권한 있는 액세스를 제공하며 사용자가 자신의 관리자 권한을 가지고 무엇을 하는지 모니터링하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-110">Organizations give users privileged access in Azure AD without monitoring what those users are doing with their admin privileges.</span></span> <span data-ttu-id="0273f-111">Azure AD Privileged Identity Management는 이 위험을 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-111">Azure AD Privileged Identity Management helps to resolve this risk.</span></span>  

<span data-ttu-id="0273f-112">Azure AD Privileged Identity Management를 통해 다음을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-112">Azure AD Privileged Identity Management helps you:</span></span>  

* <span data-ttu-id="0273f-113">Azure AD 관리자인 사용자를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-113">See which users are Azure AD administrators</span></span>
* <span data-ttu-id="0273f-114">Office 365 및 Intune 등의 Microsoft Online Services에 대해 주문형으로 “Just-In-Time”에 관리 권한을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-114">Enable on-demand, "just in time" administrative access to Microsoft Online Services like Office 365 and Intune</span></span>
* <span data-ttu-id="0273f-115">관리자 액세스 기록 및 관리자 할당 변경에 대한 보고서 가져오기</span><span class="sxs-lookup"><span data-stu-id="0273f-115">Get reports about administrator access history and changes in administrator assignments</span></span>
* <span data-ttu-id="0273f-116">권한 있는 역할의 액세스에 대한 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-116">Get alerts about access to a privileged role</span></span>
* <span data-ttu-id="0273f-117">활성화하기 위해 승인 필요(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="0273f-117">Require approval to activate (Preview)</span></span>

<span data-ttu-id="0273f-118">Azure AD Privileged Identity Management는 다음을 포함하여 기본 제공된 Azure AD 조직 역할을 관리할 수 있습니다(여기에 제한되지 않음).</span><span class="sxs-lookup"><span data-stu-id="0273f-118">Azure AD Privileged Identity Management can manage the built-in Azure AD organizational roles, including (but not limited to):</span></span>  

* <span data-ttu-id="0273f-119">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="0273f-119">Global Administrator</span></span>
* <span data-ttu-id="0273f-120">대금 청구 관리자</span><span class="sxs-lookup"><span data-stu-id="0273f-120">Billing Administrator</span></span>
* <span data-ttu-id="0273f-121">서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="0273f-121">Service Administrator</span></span>  
* <span data-ttu-id="0273f-122">사용자 관리자</span><span class="sxs-lookup"><span data-stu-id="0273f-122">User Administrator</span></span>
* <span data-ttu-id="0273f-123">암호 관리자</span><span class="sxs-lookup"><span data-stu-id="0273f-123">Password Administrator</span></span>

## <a name="just-in-time-administrator-access"></a><span data-ttu-id="0273f-124">시간에 맞추는 관리자 액세스</span><span class="sxs-lookup"><span data-stu-id="0273f-124">Just in time administrator access</span></span>
<span data-ttu-id="0273f-125">지금까지 Azure 클래식 포털 또는 Windows PowerShell을 통해 사용자를 관리자 역할에 할당할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-125">Historically, you could assign a user to an admin role through the Azure classic portal or Windows PowerShell.</span></span> <span data-ttu-id="0273f-126">그 결과, 해당 사용자는 **영구 관리자**가 되어 할당된 역할에 항상 활성 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-126">As a result, that user becomes a **permanent admin**, always active in the assigned role.</span></span> <span data-ttu-id="0273f-127">Azure AD Privileged Identity Management는 **적격인 관리자**개념을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-127">Azure AD Privileged Identity Management introduces the concept of an **eligible admin**.</span></span> <span data-ttu-id="0273f-128">적격인 관리자는 매일은 아니지만 때때로 권한 있는 액세스가 필요한 사용자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-128">Eligible admins should be users that need privileged access now and then, but not every day.</span></span> <span data-ttu-id="0273f-129">역할은 사용자가 액세스가 필요할 때까지 비활성으로 있다가, 활성화 프로세스를 완료하고 미리 정해진 시간 동안 활성 관리자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-129">The role is inactive until the user needs access, then they complete an activation process and become an active admin for a predetermined amount of time.</span></span>

## <a name="enable-privileged-identity-management-for-your-directory"></a><span data-ttu-id="0273f-130">디렉터리에서 Privileged Identity Management 사용</span><span class="sxs-lookup"><span data-stu-id="0273f-130">Enable Privileged Identity Management for your directory</span></span>
<span data-ttu-id="0273f-131">[Azure 포털](https://portal.azure.com/)에서 Azure AD Privileged Identity Management 사용을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-131">You can start using Azure AD Privileged Identity Management in the [Azure portal](https://portal.azure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="0273f-132">디렉터리에 대해 Azure AD Privileged Identity Management를 사용하려면 Microsoft 계정(예: @outlook.com)이 아닌 조직 계정(예: @yourdomain.com)의 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-132">You must be a global administrator with an organizational account (for example, @yourdomain.com), not a Microsoft account (for example, @outlook.com), to enable Azure AD Privileged Identity Management for a directory.</span></span>

1. <span data-ttu-id="0273f-133">해당 디렉터리의 전역 관리자로 [Azure 포털](https://portal.azure.com/) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-133">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="0273f-134">조직에 둘 이상의 디렉터리가 있는 경우 Azure 포털의 오른쪽 위에서 사용자 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-134">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="0273f-135">Azure AD Privileged Identity Management를 사용할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-135">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>
3. <span data-ttu-id="0273f-136">**더 많은 서비스**를 선택하고 [필터] 텍스트 상자를 사용하여 **Azure AD Privileged Identity Management**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-136">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="0273f-137">**대시보드에 고정** 옵션을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-137">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="0273f-138">Privileged Identity Management 응용 프로그램이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-138">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="0273f-139">디렉터리에서 Azure AD Privileged Identity Management를 처음 사용하는 사용자이면 [보안 마법사](active-directory-privileged-identity-management-security-wizard.md) 가 초기 할당 환경을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-139">If you're the first person to use Azure AD Privileged Identity Management in your directory, then the [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through the initial assignment experience.</span></span> <span data-ttu-id="0273f-140">이 작업 이후 자동으로 디렉터리의 첫 번째 **보안 관리자** 및 **권한 있는 역할 관리자**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-140">After that you automatically become the first **Security administrator** and **Privileged role administrator** of the directory.</span></span>

<span data-ttu-id="0273f-141">권한 있는 역할 관리자만 다른 관리자의 액세스 권한을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-141">Only a privileged role administrator can manage access for other administrators.</span></span> <span data-ttu-id="0273f-142">[PIM 관리 기능을 다른 사용자에게 제공](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-142">You can [give other users the ability to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="privileged-identity-management-admin-dashboard"></a><span data-ttu-id="0273f-143">Privileged Identity Management 관리 대시보드</span><span class="sxs-lookup"><span data-stu-id="0273f-143">Privileged Identity Management admin dashboard</span></span>
<span data-ttu-id="0273f-144">Azure AD 권한 있는 ID 관리자는 다음과 같은 중요한 정보를 전달하는 관리 대시보드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-144">Azure AD Privileged Identity Manager provides an admin dashboard that gives you important information such as:</span></span>

* <span data-ttu-id="0273f-145">보안을 향상시킬 기회를 알려주는 경고</span><span class="sxs-lookup"><span data-stu-id="0273f-145">Alerts that point out opportunities to improve security</span></span>
* <span data-ttu-id="0273f-146">각 권한 있는 역할에 할당된 사용자 수</span><span class="sxs-lookup"><span data-stu-id="0273f-146">The number of users who are assigned to each privileged role</span></span>  
* <span data-ttu-id="0273f-147">적격 및 영구 관리자 수</span><span class="sxs-lookup"><span data-stu-id="0273f-147">The number of eligible and permanent admins</span></span>
* <span data-ttu-id="0273f-148">디렉터리의 권한 있는 역할 활성화 그래프</span><span class="sxs-lookup"><span data-stu-id="0273f-148">A graph of privileged role activations in your directory</span></span>

![PIM 대시보드 - 스크린샷][2]

## <a name="privileged-role-management"></a><span data-ttu-id="0273f-150">권한 있는 역할 관리</span><span class="sxs-lookup"><span data-stu-id="0273f-150">Privileged role management</span></span>
<span data-ttu-id="0273f-151">Azure AD Privileged Identity Management로 각 역할에 영구 또는 적격 관리자를 추가하거나 제거하여 관리자를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-151">With Azure AD Privileged Identity Management, you can manage the administrators by adding or removing permanent or eligible administrators to each role.</span></span>

![PIM 추가/제거 관리자 - 스크린샷][3]

## <a name="configure-the-role-activation-settings"></a><span data-ttu-id="0273f-153">역할 활성화 설정 구성</span><span class="sxs-lookup"><span data-stu-id="0273f-153">Configure the role activation settings</span></span>
<span data-ttu-id="0273f-154">[역할 설정](active-directory-privileged-identity-management-how-to-change-default-settings.md) 을 사용하여 다음을 포함한 적격 역할 활성화 속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-154">Using the [role settings](active-directory-privileged-identity-management-how-to-change-default-settings.md) you can configure the eligible role activation properties including:</span></span>

* <span data-ttu-id="0273f-155">역할 활성화 기간</span><span class="sxs-lookup"><span data-stu-id="0273f-155">The duration of the role activation period</span></span>
* <span data-ttu-id="0273f-156">역할 활성화 알림</span><span class="sxs-lookup"><span data-stu-id="0273f-156">The role activation notification</span></span>
* <span data-ttu-id="0273f-157">역할 활성화 프로세스 중 사용자가 제공해야 하는 정보</span><span class="sxs-lookup"><span data-stu-id="0273f-157">The information a user needs to provide during the role activation process</span></span>
* <span data-ttu-id="0273f-158">서비스 티켓 또는 인시던트 번호</span><span class="sxs-lookup"><span data-stu-id="0273f-158">Service ticket or incident number</span></span>
* [<span data-ttu-id="0273f-159">승인 워크플로 요구 사항 - 미리 보기</span><span class="sxs-lookup"><span data-stu-id="0273f-159">Approval workflow requirements - Preview</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM 설정 - 관리자 활성화 - 스크린샷][4]

<span data-ttu-id="0273f-161">이미지에서 **Multi-Factor Authentication** 에 대한 단추가 비활성입니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-161">Note that in the image, the buttons for **Multi-Factor Authentication** are disabled.</span></span> <span data-ttu-id="0273f-162">높은 권한이 필요한 특정 역할에 대해 우리는 강화된 보호를 위해 MFA가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-162">For certain, highly privileged roles, we require MFA for heightened protection.</span></span>

## <a name="role-activation"></a><span data-ttu-id="0273f-163">역할 활성화</span><span class="sxs-lookup"><span data-stu-id="0273f-163">Role activation</span></span>
<span data-ttu-id="0273f-164">[역할을 활성화](active-directory-privileged-identity-management-how-to-activate-role.md)하기 위해 적격 관리자는 역할에 대해 시간 제한이 있는 "활성화"를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-164">To [activate a role](active-directory-privileged-identity-management-how-to-activate-role.md), an eligible admin requests a time-bound "activation" for the role.</span></span> <span data-ttu-id="0273f-165">Azure AD Privileged Identity Management에서 **내 역할 활성화** 옵션을 사용하여 활성화를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-165">The activation can be requested using the **Activate my role** option in Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="0273f-166">역할을 활성화하려는 관리자는 Azure 포털에서 Azure AD Privileged Identity Management를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-166">An admin who wants to activate a role needs to initialize Azure AD Privileged Identity Management in the Azure portal.</span></span>

<span data-ttu-id="0273f-167">역할 활성화는 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-167">Role activation is customizable.</span></span> <span data-ttu-id="0273f-168">PIM 설정에서 활성화 길이 및 역할을 활성화하기 위해 관리자가 제공해야 하는 정보를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-168">In the PIM settings, you can determine the length of the activation and what information the admin needs to provide to activate the role.</span></span>

![PIM 관리자 요청 역할 활성화 - 스크린샷][5]

## <a name="review-role-activity"></a><span data-ttu-id="0273f-170">역할 작업 검토</span><span class="sxs-lookup"><span data-stu-id="0273f-170">Review role activity</span></span>
<span data-ttu-id="0273f-171">직원 및 관리자가 권한 있는 역할을 사용하는 방법을 추적하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-171">There are two ways to track how your employees and admins are using privileged roles.</span></span> <span data-ttu-id="0273f-172">첫 번째 옵션은 [디렉터리 역할 감사 기록](active-directory-privileged-identity-management-how-to-use-audit-log.md)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-172">The first option is using [Directory Roles audit history](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span></span> <span data-ttu-id="0273f-173">감사 기록 로그는 권한 있는 역할 할당 및 역할 활성화 기록의 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-173">The audit history logs track changes in privileged role assignments and role activation history.</span></span>

![PIM 활성화 기록 - 스크린샷][6]

<span data-ttu-id="0273f-175">두 번째 옵션은 정기적인 [액세스 검토](active-directory-privileged-identity-management-how-to-start-security-review.md)를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-175">The second option is to set up regular [access reviews](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="0273f-176">이러한 액세스 검토는 할당된 검토자(예: 팀 관리자) 또는 자체적으로 검토할 수 있는 직원에 의해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-176">These access reviews can be performed by and assigned reviewer (like a team manager) or the employees can review themselves.</span></span> <span data-ttu-id="0273f-177">사용자의 액세스 필요 여부를 모니터링하는 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-177">This is the best way to monitor who still requires access, and who no longer does.</span></span>

## <a name="azure-ad-pim-at-subscription-expiration"></a><span data-ttu-id="0273f-178">구독 만료 시 Azure AD PIM</span><span class="sxs-lookup"><span data-stu-id="0273f-178">Azure AD PIM at subscription expiration</span></span>
<span data-ttu-id="0273f-179">일반적 가용성에 도달하기 전에 Azure AD PIM은 미리 보기에 있었으며, 테넌트에서 Azure AD PIM을 미리 볼 수 있는 라이선스 검사가 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-179">Prior to reaching general availability Azure AD PIM was in preview and there were no license checks for a tenant to preview Azure AD PIM.</span></span>  <span data-ttu-id="0273f-180">Azure AD PIM이 일반 공급 상태가 되면 PIM을 계속 사용할 수 있게 테넌트 관리자에게 평가판 또는 유료 라이선스를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-180">Now that Azure AD PIM has reached general availability, trial or paid licenses must be assigned to the administrators of the tenant to continue using PIM.</span></span>  <span data-ttu-id="0273f-181">조직에서 Azure AD Premium P2를 구입하지 않았거나 평가 기간이 만료된 경우에는 테넌트에서 Azure AD PIM 기능 거의 대부분을 더 이상 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-181">If your organization does not purchase Azure AD Premium P2 or your trial expires, mostly all of the Azure AD PIM features will no longer be available in your tenant.</span></span>  <span data-ttu-id="0273f-182">[Azure AD PIM 구독 요구 사항](./privileged-identity-management/subscription-requirements.md)에서 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0273f-182">You can read more in the [Azure AD PIM subscription requirements](./privileged-identity-management/subscription-requirements.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0273f-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0273f-183">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
