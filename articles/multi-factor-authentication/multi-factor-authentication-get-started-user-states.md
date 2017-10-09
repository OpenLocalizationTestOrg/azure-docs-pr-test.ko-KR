---
title: "aaaMicrosoft Azure Multi-factor Authentication 사용자 상태"
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
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a><span data-ttu-id="fa3f8-103">어떻게 사용자 또는 그룹에 대 한 toorequire 2 단계 인증</span><span class="sxs-lookup"><span data-stu-id="fa3f8-103">How toorequire two-step verification for a user or group</span></span>

<span data-ttu-id="fa3f8-104">2단계 인증을 요구하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-104">There are two approaches for requiring two-step verification.</span></span> <span data-ttu-id="fa3f8-105">첫 번째 옵션 hello tooenable 각 개별 사용자가 Azure Multi-factor Authentication (MFA)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-105">hello first option is tooenable each individual user for Azure Multi-Factor Authentication (MFA).</span></span> <span data-ttu-id="fa3f8-106">사용자가 개별적으로 설정 된 몇 가지 예외가 있지만, 장치 기능이 설정 된 신뢰할 수 있는 IP 주소에서 로그인 할 때 또는 hello 기억 하는 경우 처럼 2 단계 인증 항상 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-106">When users are enabled individually, they always perform two-step verification (with some exceptions, like when they sign in from trusted IP addresses or if hello remembered devices feature is turned on).</span></span> <span data-ttu-id="fa3f8-107">hello 두 번째 옵션은 tooset 특정 조건에서 2 단계 인증을 요구 하는 조건부 액세스 정책 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-107">hello second option is tooset up a conditional access policy that requires two-step verification under certain conditions.</span></span>

>[!TIP] 
><span data-ttu-id="fa3f8-108">둘 다 이러한 메서드 toorequire 2 단계 인증 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-108">Choose one of these methods toorequire two-step verification, not both.</span></span> <span data-ttu-id="fa3f8-109">사용자가 Azure MFA를 사용하도록 설정하면 모든 조건부 액세스 정책이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-109">Enabling a user for Azure MFA overrides any conditional access policies.</span></span>

## <a name="which-option-is-right-for-you"></a><span data-ttu-id="fa3f8-110">어떤 옵션이 적합한가요?</span><span class="sxs-lookup"><span data-stu-id="fa3f8-110">Which option is right for you</span></span>

<span data-ttu-id="fa3f8-111">**사용자 상태를 변경 하 여 Azure MFA를 활성화** hello 일반적인 방법에 대 한 2 단계 인증을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-111">**Enabling Azure MFA by changing user states** is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="fa3f8-112">Hello 클라우드에서 모두 Azure MFA 및 Azure MFA 서버 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-112">It works for both Azure MFA in hello cloud and Azure MFA Server.</span></span> <span data-ttu-id="fa3f8-113">사용 하도록 설정 하면 모든 hello 사용자가 hello에 로그인 할 때마다 tooperform 2 단계 인증을 사용 하 되 같은 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-113">All hello users that you enable have hello same experience, which is tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="fa3f8-114">사용자가 사용하도록 설정되면 해당 사용자에게 영향을 줄 수 있는 모든 조건부 액세스 정책이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-114">Enabling a user overrides any conditional access policies that may affect that user.</span></span> 

<span data-ttu-id="fa3f8-115">**조건부 액세스 정책을 사용하여 Azure MFA를 사용하도록 설정**하는 것은 2단계 인증을 요구하는 것보다 더 유연한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-115">**Enabling Azure MFA with a conditional access policy** is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="fa3f8-116">것에 대해서만 작동 hello 클라우드에서 Azure MFA 하지만 및 조건부 액세스는는 [유료 Azure Active Directory의 기능](https://www.microsoft.com/cloud-platform/azure-active-directory-features)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-116">It only work for Azure MFA in hello cloud, though, and conditional access is a [paid feature of Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span> <span data-ttu-id="fa3f8-117">Toogroups 뿐만 아니라 개별 사용자에 게 적용 되는 조건부 액세스 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-117">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="fa3f8-118">위험 수준이 높은 그룹에는 위험 수준이 낮은 그룹보다 더 많은 제한이 제공되거나 위험 수준이 높은 클라우드 앱에만 2단계 인증이 요구되고 위험 수준이 낮은 그룹에는 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-118">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> 

<span data-ttu-id="fa3f8-119">Hello 요구 사항 설정 후에 로그인 할 처음으로 Azure Multi-factor Authentication hello에 대 한 사용자가 tooregister 라는 두이 옵션 모두.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-119">Both of these options prompt users tooregister for Azure Multi-Factor Authentication hello first time that they sign in after hello requirements turn on.</span></span> <span data-ttu-id="fa3f8-120">두 옵션 모두 구성 가능한 hello로 확대할 [Azure Multi-factor Authentication 설정](multi-factor-authentication-whats-next.md)</span><span class="sxs-lookup"><span data-stu-id="fa3f8-120">Both options also work with hello configurable [Azure Multi-Factor Authentication settings](multi-factor-authentication-whats-next.md)</span></span>

## <a name="enable-azure-mfa-by-changing-user-status"></a><span data-ttu-id="fa3f8-121">사용자 상태를 변경하여 Azure MFA를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fa3f8-121">Enable Azure MFA by changing user status</span></span>

<span data-ttu-id="fa3f8-122">Azure Multi-factor Authentication에서 사용자 계정에는 다음 세 가지 상태는 hello를 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-122">User accounts in Azure Multi-Factor Authentication have hello following three distinct states:</span></span>

| <span data-ttu-id="fa3f8-123">가동 상태</span><span class="sxs-lookup"><span data-stu-id="fa3f8-123">Status</span></span> | <span data-ttu-id="fa3f8-124">설명</span><span class="sxs-lookup"><span data-stu-id="fa3f8-124">Description</span></span> | <span data-ttu-id="fa3f8-125">영향 받는 비브라우저 앱</span><span class="sxs-lookup"><span data-stu-id="fa3f8-125">Non-browser apps affected</span></span> |
|:---:|:---:|:---:|
| <span data-ttu-id="fa3f8-126">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="fa3f8-126">Disabled</span></span> |<span data-ttu-id="fa3f8-127">새 사용자에 대 한 기본 상태 hello Azure Multi-factor Authentication (MFA) 등록 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-127">hello default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span></span> |<span data-ttu-id="fa3f8-128">아니요</span><span class="sxs-lookup"><span data-stu-id="fa3f8-128">No</span></span> |
| <span data-ttu-id="fa3f8-129">사용</span><span class="sxs-lookup"><span data-stu-id="fa3f8-129">Enabled</span></span> |<span data-ttu-id="fa3f8-130">hello 사용자가 Azure MFA에 등록 되어 있지만 등록 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-130">hello user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="fa3f8-131">입력 정보 요청된 tooregister hello 다음 번에 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-131">They will be prompted tooregister hello next time they sign in.</span></span> |<span data-ttu-id="fa3f8-132">아니요.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-132">No.</span></span>  <span data-ttu-id="fa3f8-133">Toowork hello 등록 프로세스가 완료 될 때까지 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-133">They continue toowork until hello registration process is completed.</span></span> |
| <span data-ttu-id="fa3f8-134">적용</span><span class="sxs-lookup"><span data-stu-id="fa3f8-134">Enforced</span></span> |<span data-ttu-id="fa3f8-135">hello 사용자가 등록 되어 있고 Azure MFA에 대 한 hello 등록 프로세스를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-135">hello user has been enrolled and has completed hello registration process for Azure MFA.</span></span> |<span data-ttu-id="fa3f8-136">예.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-136">Yes.</span></span>  <span data-ttu-id="fa3f8-137">앱에 앱 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-137">Apps require app passwords.</span></span> |

<span data-ttu-id="fa3f8-138">사용자의 상태는 관리자가에 등록 되었는지 여부에 Azure MFA 및 hello 등록 프로세스를 완료 여부를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-138">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed hello registration process.</span></span>

<span data-ttu-id="fa3f8-139">모든 사용자는 *사용 안 함*으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-139">All users start out *disabled*.</span></span> <span data-ttu-id="fa3f8-140">Azure MFA에 사용자를 등록하면 상태는 *사용*으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-140">When you enroll users in Azure MFA, their state changes *enabled*.</span></span> <span data-ttu-id="fa3f8-141">사용 되는 사용자에 로그인 하 고 hello 등록 프로세스 완료를 상태로 변경 너무*적용*합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-141">When enabled users sign in and complete hello registration process, their state changes too*enforced*.</span></span>  

### <a name="view-hello-status-for-a-user"></a><span data-ttu-id="fa3f8-142">사용자에 대 한 hello 상태 보기</span><span class="sxs-lookup"><span data-stu-id="fa3f8-142">View hello status for a user</span></span>

<span data-ttu-id="fa3f8-143">사용 하 여 hello 다음 단계를 확인 하 고 사용자 상태를 관리할 수 있는 tooaccess hello 페이지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-143">Use hello following steps tooaccess hello page where you can view and manage user states:</span></span>

1. <span data-ttu-id="fa3f8-144">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-144">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="fa3f8-145">너무 이동**Azure Active Directory** > **사용자 및 그룹** > **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-145">Go too**Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="fa3f8-146">**Multi-Factor Authentication**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-146">Select **Multi-Factor Authentication**.</span></span>
   <span data-ttu-id="fa3f8-147">![Multi-Factor Authentication 선택](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span><span class="sxs-lookup"><span data-stu-id="fa3f8-147">![Select Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span></span>
4. <span data-ttu-id="fa3f8-148">Hello 사용자 상태를 표시 하는 새 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-148">A new page, which displays hello user states, opens.</span></span>
   <span data-ttu-id="fa3f8-149">![다단계 인증 사용자 상태 - 스크린샷](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="fa3f8-149">![multi-factor authentication user status - screenshot](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span></span>

### <a name="change-hello-status-for-a-user"></a><span data-ttu-id="fa3f8-150">사용자에 대 한 hello 상태 변경</span><span class="sxs-lookup"><span data-stu-id="fa3f8-150">Change hello status for a user</span></span>

1. <span data-ttu-id="fa3f8-151">Hello 앞 단계 tooget toohello multi-factor authentication 사용자가 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-151">Use hello preceding steps tooget toohello multi-factor authentication users page.</span></span>
2. <span data-ttu-id="fa3f8-152">Azure MFA에 대 한 tooenable 되도록 찾기 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-152">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="fa3f8-153">Toochange 할 수 있습니다 hello hello 위쪽에는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-153">You may need toochange hello view at hello top.</span></span> 
   <span data-ttu-id="fa3f8-154">![사용자 찾기 - 스크린샷](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="fa3f8-154">![Find user - screenshot](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
3. <span data-ttu-id="fa3f8-155">Hello 상자 다음 tootheir 이름을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-155">Check hello box next tootheir name.</span></span>
4. <span data-ttu-id="fa3f8-156">오른쪽의 빠른 단계에서 사용 되는 hello, 선택 **사용** 또는 **사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-156">On hello right, under quick steps, choose **Enable** or **Disable**.</span></span>
   <span data-ttu-id="fa3f8-157">![선택한 사용자 사용 - 스크린샷](./media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="fa3f8-157">![Enable selected user - screenshot](./media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>

   >[!TIP]
   ><span data-ttu-id="fa3f8-158">*활성화* 사용자를 자동으로 너무 전환할*적용* Azure MFA에 대해 등록할 때.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-158">*Enabled* users automatically switch too*enforced* when they register for Azure MFA.</span></span> <span data-ttu-id="fa3f8-159">Hello 사용자 상태 tooenforced를 수동으로 변경 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-159">You shouldn't manually change hello user state tooenforced.</span></span> 

5. <span data-ttu-id="fa3f8-160">Hello 팝업 창이 열리면 선택한 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-160">Confirm your selection in hello pop-up window that opens.</span></span> 

<span data-ttu-id="fa3f8-161">사용자를 사용으로 설정한 후 전자 메일을 통해 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-161">After you enable users, you should notify them via email.</span></span> <span data-ttu-id="fa3f8-162">증명이 요구 됩니다 tooregister hello 다음에 로그인 할 때 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-162">Tell them that they'll be asked tooregister hello next time they sign in.</span></span> <span data-ttu-id="fa3f8-163">또한 조직에서 최신 인증을 지원 하지 않는 비 브라우저 앱을 사용 하는 경우 toocreate 앱 암호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-163">Also, if your organization uses non-browser apps that don't support modern authentication, they'll need toocreate app passwords.</span></span> <span data-ttu-id="fa3f8-164">링크 tooour 포함할 수도 있습니다 [Azure MFA 최종 사용자 가이드](./end-user/multi-factor-authentication-end-user.md) toohelp을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-164">You can also include a link tooour [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) toohelp them get started.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="fa3f8-165">PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="fa3f8-165">Use PowerShell</span></span>
<span data-ttu-id="fa3f8-166">toochange hello 사용자 상태 사용 하 여 상태 [Azure AD PowerShell](/powershell/azure/overview), 변경 `$st.State`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-166">toochange hello user status state using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span></span> <span data-ttu-id="fa3f8-167">여기에는 세 가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-167">There are three possible states:</span></span>

* <span data-ttu-id="fa3f8-168">사용</span><span class="sxs-lookup"><span data-stu-id="fa3f8-168">Enabled</span></span>
* <span data-ttu-id="fa3f8-169">적용</span><span class="sxs-lookup"><span data-stu-id="fa3f8-169">Enforced</span></span>
* <span data-ttu-id="fa3f8-170">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="fa3f8-170">Disabled</span></span>  

<span data-ttu-id="fa3f8-171">사용자가 이동 하지 직접 toohello *Enforced* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-171">Don't move users directly toohello *Enforced* state.</span></span> <span data-ttu-id="fa3f8-172">비 브라우저 기반 앱 hello 사용자가 하지 등록 MFA 완료 하 고 가져올 수 없기 때문에 작동 중지 됩니다는 [앱 암호](multi-factor-authentication-whats-next.md#app-passwords)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-172">Non-browser-based apps will stop working because hello user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span></span> 

<span data-ttu-id="fa3f8-173">PowerShell을 사용 하는 것이 좋습니다 toobulk 사용자가 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-173">Using PowerShell is a good option when you need toobulk enabling users.</span></span> <span data-ttu-id="fa3f8-174">사용자 목록을 통해 반복하여 이 사용자들을 사용하도록 설정하는 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-174">Create a PowerShell script that loops through a list of users and enables them:</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="fa3f8-175">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-175">Here is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a><span data-ttu-id="fa3f8-176">조건부 액세스 정책으로 Azure MFA 사용</span><span class="sxs-lookup"><span data-stu-id="fa3f8-176">Enable Azure MFA with a conditional access policy</span></span>

<span data-ttu-id="fa3f8-177">조건부 액세스는 여러 가지 구성 옵션이 가능한 Azure Active Directory의 유료 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-177">Conditional access is a paid feature of Azure Active Directory, with many possible configuration options.</span></span> <span data-ttu-id="fa3f8-178">다음이 단계를 안내는 한 가지 방법은 toocreate 정책.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-178">These steps walk through one way toocreate a policy.</span></span> <span data-ttu-id="fa3f8-179">자세한 내용은 [Azure Active Directory 조건부 액세스](../active-directory/active-directory-conditional-access-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-179">For more information, read about [Conditional Access in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).</span></span>

1. <span data-ttu-id="fa3f8-180">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-180">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="fa3f8-181">너무 이동**Azure Active Directory** > **조건부 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-181">Go too**Azure Active Directory** > **Conditional access**.</span></span>
3. <span data-ttu-id="fa3f8-182">**새 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-182">Select **New policy**.</span></span>
4. <span data-ttu-id="fa3f8-183">**할당** 아래에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-183">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="fa3f8-184">사용 하 여 hello **Include** 및 **제외** 탭 toospecify 있는 사용자 및 그룹 hello 정책에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-184">Use hello **Include** and **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>
5. <span data-ttu-id="fa3f8-185">**할당** 아래에서 **클라우드 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-185">Under **Assignments**, select **Cloud apps**.</span></span> <span data-ttu-id="fa3f8-186">Tooinclude 선택 **모든 클라우드 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-186">Choose tooinclude **All cloud apps**.</span></span>
6. <span data-ttu-id="fa3f8-187">**액세스 제어** 아래에서 **허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-187">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="fa3f8-188">**다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-188">Choose **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="fa3f8-189">설정 **정책 사용** 너무**에** 선택한 후 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-189">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="fa3f8-190">hello hello 조건부 액세스 정책에서 다른 옵션 사용 하면 toospecify 2 단계 인증 해야 하는 경우에 정확 하 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-190">hello other options in hello conditional access policy allow you toospecify exactly when two-step verification should be required.</span></span> <span data-ttu-id="fa3f8-191">예를 들어 함을 나타내는 정책을 만들 수 있습니다: 계약자는 tooaccess 도메인에 가입 되지 않은 장치에서 신뢰할 수 없는 네트워크에서 조달 앱을 시도할 때 2 단계 인증을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-191">For example, you could make a policy that states: when contractors try tooaccess our procurement app from untrusted networks on devices that are not domain-joined, require two-step verification.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fa3f8-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fa3f8-192">Next steps</span></span>

- <span data-ttu-id="fa3f8-193">Hello에 대 한 팁 가져오기 [조건부 액세스에 대 한 유용한 정보](../active-directory/active-directory-conditional-access-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="fa3f8-193">Get tips on hello [Best practices for conditional access](../active-directory/active-directory-conditional-access-best-practices.md)</span></span>

- <span data-ttu-id="fa3f8-194">[사용자 및 장치](multi-factor-authentication-manage-users-and-devices.md)에 대한 Multi-Factor Authentication 설정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fa3f8-194">Manage Multi-Factor Authentication settings for [your users and their devices](multi-factor-authentication-manage-users-and-devices.md)</span></span>