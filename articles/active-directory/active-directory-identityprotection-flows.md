---
title: "Azure AD ID 보호를 사용하는 로그인 환경 | Microsoft Docs"
description: "ID 보호가 완화되었거나 사용자를 재구성한 경우 또는 정책에서 다단계 인증을 요구하는 경우의 사용자 환경에 대한 개요를 제공합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="b69da-104">Azure AD ID 보호를 사용하는 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="b69da-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="b69da-105">Azure Active Directory ID 보호를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="b69da-106">사용자에게 다단계 인증 등록 요구</span><span class="sxs-lookup"><span data-stu-id="b69da-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="b69da-107">위험한 로그인 및 손상된 사용자 처리</span><span class="sxs-lookup"><span data-stu-id="b69da-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="b69da-108">더 이상 사용자 이름과 암호를 제공하여 직접 로그인할 수 없기 때문에 이러한 문제에 대한 시스템의 응답은 사용자의 로그인 환경에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="b69da-109">사용자를 업무 환경으로 안전하게 복귀시키려면 추가 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="b69da-110">이 항목에서는 발생할 수 있는 모든 경우의 사용자 로그인 환경에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="b69da-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="b69da-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="b69da-112">Multi-Factor Authentication 등록</span><span class="sxs-lookup"><span data-stu-id="b69da-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="b69da-113">**위험한 로그인**</span><span class="sxs-lookup"><span data-stu-id="b69da-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="b69da-114">위험한 로그인 복구</span><span class="sxs-lookup"><span data-stu-id="b69da-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="b69da-115">위험한 로그인 차단됨</span><span class="sxs-lookup"><span data-stu-id="b69da-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="b69da-116">위험한 로그인 시 Multi-Factor Authentication 등록</span><span class="sxs-lookup"><span data-stu-id="b69da-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="b69da-117">**위험한 사용자**</span><span class="sxs-lookup"><span data-stu-id="b69da-117">**User at risk**</span></span>

* <span data-ttu-id="b69da-118">손상된 계정 복구</span><span class="sxs-lookup"><span data-stu-id="b69da-118">Compromised account recovery</span></span>
* <span data-ttu-id="b69da-119">손상된 계정 차단됨</span><span class="sxs-lookup"><span data-stu-id="b69da-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="b69da-120">Multi-Factor Authentication 등록</span><span class="sxs-lookup"><span data-stu-id="b69da-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="b69da-121">손상된 계정 복구 흐름 및 위험한 로그인 흐름 모두에 대한 최상의 사용자 환경은 사용자가 자체 복구할 수 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="b69da-122">사용자가 다단계 인증에 등록된 경우 보안 과제를 전달하는 데 사용될 수 있는 해당 계정으로 연결된 전화 번호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="b69da-123">계정 손상을 복구하는 데 기술 지원팀 또는 관리자의 관여는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="b69da-124">따라서 사용자를 Multi-Factor Authentication에 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="b69da-125">관리자는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-125">Administrators can:</span></span>

* <span data-ttu-id="b69da-126">사용자가 해당 계정에 추가 보안 확인을 설정해야 하는 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="b69da-127">등록하기 전에 사용자에게 유예 기간을 제공하려는 경우 최대 30일 동안 Multi-Factor Authentication 등록을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="b69da-128">**다단계 인증 등록에 세 가지 단계가 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="b69da-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="b69da-129">첫 번째 단계에서 다단계 인증에 대한 계정을 설정하라는 요구 사항에 대한 알림이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="b69da-130">![수정](./media/active-directory-identityprotection-flows/140.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="b69da-131">다단계 인증을 설정하려면 연결하려는 방법을 시스템에 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="b69da-132">![수정](./media/active-directory-identityprotection-flows/141.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="b69da-133">시스템에서 챌린지를 제출하면 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="b69da-134">![수정](./media/active-directory-identityprotection-flows/142.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="b69da-135">위험한 로그인 복구</span><span class="sxs-lookup"><span data-stu-id="b69da-135">Risky sign-in recovery</span></span>
<span data-ttu-id="b69da-136">관리자가 로그인 위험에 대한 정책을 구성하는 경우 로그인하려고 할 때 영향을 받는 사용자에게 알려지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="b69da-137">**위험한 로그인 흐름에는 두 단계가 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="b69da-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="b69da-138">사용자는 새 위치, 장치 또는 앱에서 로그인과 같은 해당 로그인에 대해 비정상적인 점이 검색되었음을 통보받습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="b69da-139">![수정](./media/active-directory-identityprotection-flows/120.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="b69da-140">사용자가 보안 과제를 해결하여 해당 ID를 증명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="b69da-141">사용자가 Multi-Factor Authentication에 등록된 경우 전화 번호에 대한 보안 코드를 왕복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="b69da-142">손상된 계정이 아닌 위험한 로그인일 뿐이기 때문에 사용자는 이 흐름에서 암호를 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="b69da-143">![수정](./media/active-directory-identityprotection-flows/121.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="b69da-144">위험한 로그인 차단됨</span><span class="sxs-lookup"><span data-stu-id="b69da-144">Risky sign-in blocked</span></span>
<span data-ttu-id="b69da-145">관리자는 로그인 위험 정책을 설정하도록 선택하여 위험 수준에 따라 로그인 시 사용자를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="b69da-146">차단을 해제하려면 최종 사용자는 관리자나 기술 지원팀에 문의해야 하고 익숙한 위치 또는 장치에서 로그인을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="b69da-147">다단계 인증을 해결하는 자체 복구는 이 경우에 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="b69da-148">![수정](./media/active-directory-identityprotection-flows/200.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="b69da-149">손상된 계정 복구</span><span class="sxs-lookup"><span data-stu-id="b69da-149">Compromised account recovery</span></span>
<span data-ttu-id="b69da-150">사용자 위험 보안 정책이 구성된 경우 정책에 지정된 사용자 위험 수준을 만족하는 사용자(따라서 손상되었다고 가정됨)는 로그인할 수 있기 전에 사용자 손상 복구 흐름을 통해 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="b69da-151">**사용자 손상 복구 흐름에는 세 가지 단계가 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="b69da-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="b69da-152">사용자는 해당 계정 보안이 의심스러운 작업 또는 유출된 자격 증명으로 인해 위험에 노출되었다는 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="b69da-153">![수정](./media/active-directory-identityprotection-flows/101.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="b69da-154">사용자가 보안 과제를 해결하여 해당 ID를 증명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="b69da-155">Multi-Factor Authentication에 사용자를 등록하는 경우 손상되지 않도록 자체 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="b69da-156">해당 전화 번호에 보안 코드를 왕복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="b69da-157">![수정](./media/active-directory-identityprotection-flows/110.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="b69da-158">마지막으로, 다른 사람이 해당 계정에 액세스했을 수 있으므로 사용자는 해당 암호를 변경하도록 강제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="b69da-159">이러한 환경의 스크린 샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="b69da-160">![수정](./media/active-directory-identityprotection-flows/111.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="b69da-161">손상된 계정 차단됨</span><span class="sxs-lookup"><span data-stu-id="b69da-161">Compromised account blocked</span></span>
<span data-ttu-id="b69da-162">차단 해제된 사용자 위험 보안 정책에 의해 차단된 사용자를 가져오려면 사용자는 관리자 또는 기술 지원팀에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="b69da-163">다단계 인증을 해결하는 자체 복구는 이 경우에 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="b69da-164">![수정](./media/active-directory-identityprotection-flows/104.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="b69da-165">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="b69da-165">Reset password</span></span>
<span data-ttu-id="b69da-166">손상된 사용자가 로그인할 수 없으면 관리자가 해당 사용자에게 임시 암호를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="b69da-167">사용자는 다음 로그인 시 자신의 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b69da-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="b69da-168">![수정](./media/active-directory-identityprotection-flows/160.png "수정")</span><span class="sxs-lookup"><span data-stu-id="b69da-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="b69da-169">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b69da-169">See also</span></span>
* [<span data-ttu-id="b69da-170">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="b69da-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

