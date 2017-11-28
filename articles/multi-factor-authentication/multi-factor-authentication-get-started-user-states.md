---
title: "Microsoft Azure Multi-Factor Authentication 사용자 상태"
description: "Azure MFA의 사용자 상태에 대해 알아보세요."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 1869b7a4ef42536a3cd909ba2983ae0fe97185a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-require-two-step-verification-for-a-user-or-group"></a><span data-ttu-id="f2ba6-103">사용자 또는 그룹에 대해 2단계 인증을 요구하는 방법</span><span class="sxs-lookup"><span data-stu-id="f2ba6-103">How to require two-step verification for a user or group</span></span>

<span data-ttu-id="f2ba6-104">2단계 인증을 요구하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-104">There are two approaches for requiring two-step verification.</span></span> <span data-ttu-id="f2ba6-105">첫 번째 옵션은 각 개별 사용자가 Azure MFA(Multi-Factor Authentication)를 사용하도록 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-105">The first option is to enable each individual user for Azure Multi-Factor Authentication (MFA).</span></span> <span data-ttu-id="f2ba6-106">사용자가 개별적으로 설정되면 신뢰할 수 있는 IP 주소에서 로그인하거나 기억된 장치 기능이 설정되어 경우와 같이 몇 가지 예외를 제외하고는 항상 2단계 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-106">When users are enabled individually, they always perform two-step verification (with some exceptions, like when they sign in from trusted IP addresses or if the remembered devices feature is turned on).</span></span> <span data-ttu-id="f2ba6-107">두 번째 옵션은 특정 조건에서 2단계 인증을 요구하는 조건부 액세스 정책을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-107">The second option is to set up a conditional access policy that requires two-step verification under certain conditions.</span></span>

>[!TIP] 
><span data-ttu-id="f2ba6-108">두 가지 방법 중 하나를 선택하여 2단계 인증을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-108">Choose one of these methods to require two-step verification, not both.</span></span> <span data-ttu-id="f2ba6-109">사용자가 Azure MFA를 사용하도록 설정하면 모든 조건부 액세스 정책이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-109">Enabling a user for Azure MFA overrides any conditional access policies.</span></span>

## <a name="which-option-is-right-for-you"></a><span data-ttu-id="f2ba6-110">어떤 옵션이 적합한가요?</span><span class="sxs-lookup"><span data-stu-id="f2ba6-110">Which option is right for you</span></span>

<span data-ttu-id="f2ba6-111">**사용자 상태를 변경하여 Azure MFA를 사용하도록 설정**하는 것이 2단계 인증을 요구하는 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-111">**Enabling Azure MFA by changing user states** is the traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="f2ba6-112">이 방법은 클라우드의 Azure MFA와 Azure MFA Server 모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-112">It works for both Azure MFA in the cloud and Azure MFA Server.</span></span> <span data-ttu-id="f2ba6-113">사용하도록 설정한 모든 사용자는 동일한 환경에서 로그인할 때마다 2단계 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-113">All the users that you enable have the same experience, which is to perform two-step verification every time they sign in.</span></span> <span data-ttu-id="f2ba6-114">사용자가 사용하도록 설정되면 해당 사용자에게 영향을 줄 수 있는 모든 조건부 액세스 정책이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-114">Enabling a user overrides any conditional access policies that may affect that user.</span></span> 

<span data-ttu-id="f2ba6-115">**조건부 액세스 정책을 사용하여 Azure MFA를 사용하도록 설정**하는 것은 2단계 인증을 요구하는 것보다 더 유연한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-115">**Enabling Azure MFA with a conditional access policy** is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="f2ba6-116">Azure MFA는 클라우드에서만 작동하며 조건부 액세스는 [Azure Active Directory의 유료 기능](https://www.microsoft.com/cloud-platform/azure-active-directory-features)입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-116">It only work for Azure MFA in the cloud, though, and conditional access is a [paid feature of Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span> <span data-ttu-id="f2ba6-117">개별 사용자뿐만 아니라 그룹에도 적용되는 조건부 액세스 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-117">You can create conditional access policies that apply to groups as well as individual users.</span></span> <span data-ttu-id="f2ba6-118">위험 수준이 높은 그룹에는 위험 수준이 낮은 그룹보다 더 많은 제한이 제공되거나 위험 수준이 높은 클라우드 앱에만 2단계 인증이 요구되고 위험 수준이 낮은 그룹에는 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-118">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> 

<span data-ttu-id="f2ba6-119">두 옵션은 모두 인증 요구가 설정된 후에 사용자가 처음 로그인하면 Azure Multi-Factor Authentication에 등록하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-119">Both of these options prompt users to register for Azure Multi-Factor Authentication the first time that they sign in after the requirements turn on.</span></span> <span data-ttu-id="f2ba6-120">또한 두 옵션은 모두 구성 가능한 [Azure Multi-Factor Authentication 설정](multi-factor-authentication-whats-next.md)에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-120">Both options also work with the configurable [Azure Multi-Factor Authentication settings](multi-factor-authentication-whats-next.md)</span></span>

## <a name="enable-azure-mfa-by-changing-user-status"></a><span data-ttu-id="f2ba6-121">사용자 상태를 변경하여 Azure MFA를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f2ba6-121">Enable Azure MFA by changing user status</span></span>

<span data-ttu-id="f2ba6-122">Azure Multi-Factor Authentication의 사용자 계정은 다음과 같은 3가지 상태를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-122">User accounts in Azure Multi-Factor Authentication have the following three distinct states:</span></span>

| <span data-ttu-id="f2ba6-123">가동 상태</span><span class="sxs-lookup"><span data-stu-id="f2ba6-123">Status</span></span> | <span data-ttu-id="f2ba6-124">설명</span><span class="sxs-lookup"><span data-stu-id="f2ba6-124">Description</span></span> | <span data-ttu-id="f2ba6-125">영향 받는 비브라우저 앱</span><span class="sxs-lookup"><span data-stu-id="f2ba6-125">Non-browser apps affected</span></span> |
|:---:|:---:|:---:|
| <span data-ttu-id="f2ba6-126">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="f2ba6-126">Disabled</span></span> |<span data-ttu-id="f2ba6-127">Azure MFA(Multi-Factor Authentication)에 등록되지 않은 새 사용자에 대한 기본 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-127">The default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span></span> |<span data-ttu-id="f2ba6-128">아니요</span><span class="sxs-lookup"><span data-stu-id="f2ba6-128">No</span></span> |
| <span data-ttu-id="f2ba6-129">사용</span><span class="sxs-lookup"><span data-stu-id="f2ba6-129">Enabled</span></span> |<span data-ttu-id="f2ba6-130">사용자가 Azure MFA에 등록되었지만 등록하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-130">The user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="f2ba6-131">이 경우 다음에 로그인할 때 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-131">They will be prompted to register the next time they sign in.</span></span> |<span data-ttu-id="f2ba6-132">아니요.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-132">No.</span></span>  <span data-ttu-id="f2ba6-133">등록 프로세스가 완료될 때까지 계속 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-133">They continue to work until the registration process is completed.</span></span> |
| <span data-ttu-id="f2ba6-134">적용</span><span class="sxs-lookup"><span data-stu-id="f2ba6-134">Enforced</span></span> |<span data-ttu-id="f2ba6-135">사용자가 등록되었으며 Azure MFA를 위한 등록 프로세스를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-135">The user has been enrolled and has completed the registration process for Azure MFA.</span></span> |<span data-ttu-id="f2ba6-136">예.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-136">Yes.</span></span>  <span data-ttu-id="f2ba6-137">앱에 앱 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-137">Apps require app passwords.</span></span> |

<span data-ttu-id="f2ba6-138">사용자의 상태는 관리자가 사용자를 Azure MFA에 등록했는지 그리고 사용자가 등록 프로세스를 완료했는지 여부를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-138">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed the registration process.</span></span>

<span data-ttu-id="f2ba6-139">모든 사용자는 *사용 안 함*으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-139">All users start out *disabled*.</span></span> <span data-ttu-id="f2ba6-140">Azure MFA에 사용자를 등록하면 상태는 *사용*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-140">When you enroll users in Azure MFA, their state changes *enabled*.</span></span> <span data-ttu-id="f2ba6-141">사용된 사용자가 로그인하고 등록 프로세스를 완료하면 상태는 변경 *적용*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-141">When enabled users sign in and complete the registration process, their state changes to *enforced*.</span></span>  

### <a name="view-the-status-for-a-user"></a><span data-ttu-id="f2ba6-142">사용자 상태 보기</span><span class="sxs-lookup"><span data-stu-id="f2ba6-142">View the status for a user</span></span>

<span data-ttu-id="f2ba6-143">다음 단계를 통해 사용자 상태를 보고 관리할 수 있는 페이지에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-143">Use the following steps to access the page where you can view and manage user states:</span></span>

1. <span data-ttu-id="f2ba6-144">관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-144">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="f2ba6-145">**Azure Active Directory** > **사용자 및 그룹** > **모든 사용자**로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-145">Go to **Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="f2ba6-146">**Multi-Factor Authentication**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-146">Select **Multi-Factor Authentication**.</span></span>
   <span data-ttu-id="f2ba6-147">![Multi-Factor Authentication 선택](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span><span class="sxs-lookup"><span data-stu-id="f2ba6-147">![Select Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span></span>
4. <span data-ttu-id="f2ba6-148">사용자 상태를 표시하는 새 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-148">A new page, which displays the user states, opens.</span></span>
   <span data-ttu-id="f2ba6-149">![다단계 인증 사용자 상태 - 스크린샷](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="f2ba6-149">![multi-factor authentication user status - screenshot](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span></span>

### <a name="change-the-status-for-a-user"></a><span data-ttu-id="f2ba6-150">사용자 상태 변경</span><span class="sxs-lookup"><span data-stu-id="f2ba6-150">Change the status for a user</span></span>

1. <span data-ttu-id="f2ba6-151">이전 단계를 통해 다단계 인증 사용자 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-151">Use the preceding steps to get to the multi-factor authentication users page.</span></span>
2. <span data-ttu-id="f2ba6-152">Azure MFA에 사용하려는 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-152">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="f2ba6-153">위쪽에서 보기를 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-153">You may need to change the view at the top.</span></span> 
   <span data-ttu-id="f2ba6-154">![사용자 찾기 - 스크린샷](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="f2ba6-154">![Find user - screenshot](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
3. <span data-ttu-id="f2ba6-155">이름 옆의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-155">Check the box next to their name.</span></span>
4. <span data-ttu-id="f2ba6-156">오른쪽의 빠른 단계에서 **사용** 또는 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-156">On the right, under quick steps, choose **Enable** or **Disable**.</span></span>
   <span data-ttu-id="f2ba6-157">![선택한 사용자 사용 - 스크린샷](./media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="f2ba6-157">![Enable selected user - screenshot](./media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>

   >[!TIP]
   ><span data-ttu-id="f2ba6-158">Azure MFA에 등록하면 *사용* 사용자는 *적용*으로 자동으로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-158">*Enabled* users automatically switch to *enforced* when they register for Azure MFA.</span></span> <span data-ttu-id="f2ba6-159">사용자 상태를 수동으로 '적용'으로 변경하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-159">You shouldn't manually change the user state to enforced.</span></span> 

5. <span data-ttu-id="f2ba6-160">열리는 팝업 창에서 선택한 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-160">Confirm your selection in the pop-up window that opens.</span></span> 

<span data-ttu-id="f2ba6-161">사용자를 사용으로 설정한 후 전자 메일을 통해 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-161">After you enable users, you should notify them via email.</span></span> <span data-ttu-id="f2ba6-162">다음에 로그인할 때 등록하도록 요구된다고 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-162">Tell them that they'll be asked to register the next time they sign in.</span></span> <span data-ttu-id="f2ba6-163">또한 조직에서 최신 인증을 지원하지 않는 비브라우저 앱을 사용하는 경우 앱 암호를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-163">Also, if your organization uses non-browser apps that don't support modern authentication, they'll need to create app passwords.</span></span> <span data-ttu-id="f2ba6-164">또한 사용자가 시작할 수 있도록 [Azure MFA 최종 사용자 가이드](./end-user/multi-factor-authentication-end-user.md)에 연결되는 링크를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-164">You can also include a link to our [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) to help them get started.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="f2ba6-165">PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="f2ba6-165">Use PowerShell</span></span>
<span data-ttu-id="f2ba6-166">[Azure AD PowerShell](/powershell/azure/overview)을 사용하여 사용자 상태를 변경하려면 `$st.State`를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-166">To change the user status state using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span></span> <span data-ttu-id="f2ba6-167">여기에는 세 가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-167">There are three possible states:</span></span>

* <span data-ttu-id="f2ba6-168">사용</span><span class="sxs-lookup"><span data-stu-id="f2ba6-168">Enabled</span></span>
* <span data-ttu-id="f2ba6-169">적용</span><span class="sxs-lookup"><span data-stu-id="f2ba6-169">Enforced</span></span>
* <span data-ttu-id="f2ba6-170">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="f2ba6-170">Disabled</span></span>  

<span data-ttu-id="f2ba6-171">사용자를 *적용* 상태로 직접 전환하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-171">Don't move users directly to the *Enforced* state.</span></span> <span data-ttu-id="f2ba6-172">사용자가 MFA 등록을 마치고 [앱 암호](multi-factor-authentication-whats-next.md#app-passwords)를 가져오지 못했기 때문에 비 브라우저 기반 앱은 작동을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-172">Non-browser-based apps will stop working because the user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span></span> 

<span data-ttu-id="f2ba6-173">PowerShell을 사용하는 방법은 사용자를 대량으로 사용하도록 설정해야 할 때 적합한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-173">Using PowerShell is a good option when you need to bulk enabling users.</span></span> <span data-ttu-id="f2ba6-174">사용자 목록을 통해 반복하여 이 사용자들을 사용하도록 설정하는 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-174">Create a PowerShell script that loops through a list of users and enables them:</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="f2ba6-175">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-175">Here is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a><span data-ttu-id="f2ba6-176">조건부 액세스 정책으로 Azure MFA 사용</span><span class="sxs-lookup"><span data-stu-id="f2ba6-176">Enable Azure MFA with a conditional access policy</span></span>

<span data-ttu-id="f2ba6-177">조건부 액세스는 여러 가지 구성 옵션이 가능한 Azure Active Directory의 유료 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-177">Conditional access is a paid feature of Azure Active Directory, with many possible configuration options.</span></span> <span data-ttu-id="f2ba6-178">이러한 단계는 정책을 만드는 한 가지 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-178">These steps walk through one way to create a policy.</span></span> <span data-ttu-id="f2ba6-179">자세한 내용은 [Azure Active Directory 조건부 액세스](../active-directory/active-directory-conditional-access-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-179">For more information, read about [Conditional Access in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).</span></span>

1. <span data-ttu-id="f2ba6-180">관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-180">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="f2ba6-181">**Azure Active Directory** > **조건부 액세스**로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-181">Go to **Azure Active Directory** > **Conditional access**.</span></span>
3. <span data-ttu-id="f2ba6-182">**새 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-182">Select **New policy**.</span></span>
4. <span data-ttu-id="f2ba6-183">**할당** 아래에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-183">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="f2ba6-184">**포함** 및 **제외** 탭을 사용하여 정책별로 관리될 사용자와 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-184">Use the **Include** and **Exclude** tabs to specify which users and groups will be managed by the policy.</span></span>
5. <span data-ttu-id="f2ba6-185">**할당** 아래에서 **클라우드 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-185">Under **Assignments**, select **Cloud apps**.</span></span> <span data-ttu-id="f2ba6-186">**모든 클라우드 앱**을 포함하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-186">Choose to include **All cloud apps**.</span></span>
6. <span data-ttu-id="f2ba6-187">**액세스 제어** 아래에서 **허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-187">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="f2ba6-188">**다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-188">Choose **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="f2ba6-189">**정책 사용**을 **설정**으로 선택한 다음 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-189">Turn **Enable policy** to **On** and then select **Save**.</span></span>

<span data-ttu-id="f2ba6-190">조건부 액세스 정책의 다른 옵션을 사용하면 2단계 인증이 요구되는 경우를 정확하게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-190">The other options in the conditional access policy allow you to specify exactly when two-step verification should be required.</span></span> <span data-ttu-id="f2ba6-191">예를 들어 계약자가 도메인에 가입되지 않은 장치의 신뢰할 수 없는 네트워크에서 조달 앱에 액세스하려고 할 때 2단계 인증을 요구하는 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-191">For example, you could make a policy that states: when contractors try to access our procurement app from untrusted networks on devices that are not domain-joined, require two-step verification.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f2ba6-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2ba6-192">Next steps</span></span>

- <span data-ttu-id="f2ba6-193">[조건부 액세스 모범 사례](../active-directory/active-directory-conditional-access-best-practices.md)에 대한 팁을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-193">Get tips on the [Best practices for conditional access](../active-directory/active-directory-conditional-access-best-practices.md)</span></span>

- <span data-ttu-id="f2ba6-194">[사용자 및 장치](multi-factor-authentication-manage-users-and-devices.md)에 대한 Multi-Factor Authentication 설정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f2ba6-194">Manage Multi-Factor Authentication settings for [your users and their devices](multi-factor-authentication-manage-users-and-devices.md)</span></span>