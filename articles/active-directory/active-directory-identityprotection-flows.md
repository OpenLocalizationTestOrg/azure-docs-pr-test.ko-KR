---
title: "Azure AD Identity Protection 사용한 aaaSign에서 경험 | Microsoft Docs"
description: "Id 보호 된 완화 있거나 사용자 또는 정책에 의해 multi-factor authentication 인증이 필요한 경우 재구성 hello 사용자 경험에 대 한 개요를 제공 합니다."
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
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="01102-104">Azure AD ID 보호를 사용하는 로그인 환경</span><span class="sxs-lookup"><span data-stu-id="01102-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="01102-105">Azure Active Directory ID 보호를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="01102-106">multi-factor authentication 사용자가 tooregister 필요</span><span class="sxs-lookup"><span data-stu-id="01102-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="01102-107">위험한 로그인 및 손상된 사용자 처리</span><span class="sxs-lookup"><span data-stu-id="01102-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="01102-108">hello 시스템 toothese 문제의 hello 응답 방금 직접 로그인 사용자 이름과 암호를 제공 하 여 수 없기 때문에 가능한 더 이상 사용자의 로그인 환경에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="01102-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="01102-109">추가 단계는 필요한 tooget 안전 하 게 비즈니스 사용자에 스풀링됩니다.</span><span class="sxs-lookup"><span data-stu-id="01102-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="01102-110">이 항목에서는 발생할 수 있는 모든 경우의 사용자 로그인 환경에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="01102-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="01102-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="01102-112">Multi-Factor Authentication 등록</span><span class="sxs-lookup"><span data-stu-id="01102-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="01102-113">**위험한 로그인**</span><span class="sxs-lookup"><span data-stu-id="01102-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="01102-114">위험한 로그인 복구</span><span class="sxs-lookup"><span data-stu-id="01102-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="01102-115">위험한 로그인 차단됨</span><span class="sxs-lookup"><span data-stu-id="01102-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="01102-116">위험한 로그인 시 Multi-Factor Authentication 등록</span><span class="sxs-lookup"><span data-stu-id="01102-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="01102-117">**위험한 사용자**</span><span class="sxs-lookup"><span data-stu-id="01102-117">**User at risk**</span></span>

* <span data-ttu-id="01102-118">손상된 계정 복구</span><span class="sxs-lookup"><span data-stu-id="01102-118">Compromised account recovery</span></span>
* <span data-ttu-id="01102-119">손상된 계정 차단됨</span><span class="sxs-lookup"><span data-stu-id="01102-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="01102-120">Multi-Factor Authentication 등록</span><span class="sxs-lookup"><span data-stu-id="01102-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="01102-121">모두에 대 한 최상의 사용자 환경을 hello, 손상 된 계정 복구 흐름 hello 및 위험한 로그인 흐름 hello 때 hello 사용자 자체 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="01102-122">사용자가 multi-factor authentication 등록을 하는 경우 보안 문제를 사용 하는 toopass 일 수 있는 자신의 계정과 연결 된 전화 번호를이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="01102-123">도움말 센터 또는 관리자 관여 하지 않습니다는 필요한 toorecover 계정 손상 되지 않도록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="01102-124">따라서 것이 좋습니다 tooget 사용자가 multi-factor authentication에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="01102-125">관리자는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-125">Administrators can:</span></span>

* <span data-ttu-id="01102-126">추가 보안 확인에 대 한 자신의 계정을 tooset 사용자가 요구 하는 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="01102-127">toogive 사용자가 원하는 경우 건너뛴 too30 일 구성에 대 한 다단계 인증 등록 허용을 등록 하기 전에 유예 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="01102-128">**hello 다단계 인증 등록에는 세 가지 단계가 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="01102-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="01102-129">첫 번째 단계는 hello hello 사용자는 multi-factor authentication에 hello 요구 사항 tooset hello 계정에 대 한 알림을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="01102-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="01102-130">![수정](./media/active-directory-identityprotection-flows/140.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="01102-131">toolet hello 시스템이 필요를 tooset multi-factor authentication을 확인 하려는 toobe 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="01102-132">![수정](./media/active-directory-identityprotection-flows/141.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="01102-133">hello 시스템 챌린지 tooyou을 제출 하 고 toorespond 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="01102-134">![수정](./media/active-directory-identityprotection-flows/142.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="01102-135">위험한 로그인 복구</span><span class="sxs-lookup"><span data-stu-id="01102-135">Risky sign-in recovery</span></span>
<span data-ttu-id="01102-136">에 관리자가 로그인 위험에 대 한 정책을 구성한 경우에 toosign 하려고 할 때 hello 영향을 받는 사용자 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01102-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="01102-137">**hello 위험한 로그인 흐름에 두 개의 단계가 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="01102-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="01102-138">hello 사용자는 로그인을 새 위치, 장치 또는 앱에서 로그인 등에 대 한 검색 되었습니다 특이 한 활동이 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="01102-139">![수정](./media/active-directory-identityprotection-flows/120.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="01102-140">hello 사용자가 필요한 tooprove 신원을 보안 과제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="01102-141">Hello 사용자가 multi-factor authentication에 등록 하는 경우 tooround-여행 보안 코드 tootheir 전화 번호를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="01102-142">Just 이므로 위험한 로그인 및 손상 된 계정이 아닌 hello 사용자는이 흐름에서 toochange hello 암호 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="01102-143">![수정](./media/active-directory-identityprotection-flows/121.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="01102-144">위험한 로그인 차단됨</span><span class="sxs-lookup"><span data-stu-id="01102-144">Risky sign-in blocked</span></span>
<span data-ttu-id="01102-145">관리자가 tooset hello 위험 수준에 따라 로그인 시 로그인 위험 정책 tooblock 사용자 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="01102-146">tooget 차단 해제 됨, 최종 사용자에 게 문의 해야 관리자나 지원 센터 또는 친숙 한 위치 또는 장치에서 로그인을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="01102-147">다단계 인증을 해결하는 자체 복구는 이 경우에 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="01102-148">![수정](./media/active-directory-identityprotection-flows/200.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="01102-149">손상된 계정 복구</span><span class="sxs-lookup"><span data-stu-id="01102-149">Compromised account recovery</span></span>
<span data-ttu-id="01102-150">사용자에 게 특히 hello 사용자 위험 hello 정책에 지정 된 수준을 사용자 위험 보안 정책 구성 된 경우 (따라서 이라고 가정 손상)은에 로그인 하기 전에 hello 사용자 손상 복구 흐름을 통해 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="01102-151">**hello 사용자 손상 복구 흐름에는 세 가지 단계가 포함 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="01102-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="01102-152">hello 사용자는 자신의 계정 보안 위험에는 의심 스러운 활동 때문 또는 자격 증명을 유출 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="01102-153">![수정](./media/active-directory-identityprotection-flows/101.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="01102-154">hello 사용자가 필요한 tooprove 신원을 보안 과제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="01102-155">Hello 사용자가 multi-factor authentication에 등록 하는 경우에 손상 되지 않도록 자체 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="01102-156">이들은 tooround-여행 보안 코드 tootheir 전화 번호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="01102-157">![수정](./media/active-directory-identityprotection-flows/110.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="01102-158">마지막으로, 사용자를 hello 이후 액세스 tootheir 계정이 있을 수 있으며 다른 사용자가 암호 강제 toochange가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="01102-159">이러한 환경의 스크린 샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="01102-160">![수정](./media/active-directory-identityprotection-flows/111.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="01102-161">손상된 계정 차단됨</span><span class="sxs-lookup"><span data-stu-id="01102-161">Compromised account blocked</span></span>
<span data-ttu-id="01102-162">차단 해제 됨 사용자 위험 보안 정책에 의해 차단 된 사용자 tooget hello 사용자는 관리자나 기술 지원 서비스로 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="01102-163">다단계 인증을 해결하는 자체 복구는 이 경우에 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="01102-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="01102-164">![수정](./media/active-directory-identityprotection-flows/104.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="01102-165">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="01102-165">Reset password</span></span>
<span data-ttu-id="01102-166">손상된 사용자가 로그인할 수 없으면 관리자가 해당 사용자에게 임시 암호를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01102-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="01102-167">hello 사용자는 다음에 로그인 하는 동안 toochange 자신의 암호를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01102-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="01102-168">![수정](./media/active-directory-identityprotection-flows/160.png "수정")</span><span class="sxs-lookup"><span data-stu-id="01102-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="01102-169">참고 항목</span><span class="sxs-lookup"><span data-stu-id="01102-169">See also</span></span>
* [<span data-ttu-id="01102-170">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="01102-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

