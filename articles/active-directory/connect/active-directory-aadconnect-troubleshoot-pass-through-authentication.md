---
title: "Azure AD Connect: 통과 인증 문제 해결 | Microsoft 문서"
description: "이 문서에서는 Azure AD(Azure Active Directory) 통과 인증 문제를 해결하는 방법에 대해 설명합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증 문제 해결, Active Directory 설치, Azure AD에 필요한 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 72bd39bcf720cf5704274fcdfa0f2b8fc44a77bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="f8792-104">Azure Active Directory 통과 인증 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f8792-104">Troubleshoot Azure Active Directory Pass-through Authentication</span></span>

<span data-ttu-id="f8792-105">이 문서에서는 Azure AD 통과 인증과 관련된 일반적인 문제에 대한 문제 해결 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-105">This article helps you find troubleshooting information about common issues regarding Azure AD Pass-through Authentication.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f8792-106">통과 인증에서 사용자 로그인 문제가 발생하는 경우 클라우드 전용 전역 관리자 계정을 다시 사용하지 않고 해당 기능을 사용하지 않도록 설정하거나 통과 인증 에이전트를 제거하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f8792-106">If you are facing user sign-in issues with Pass-through Authentication, don't disable the feature or uninstall Pass-through Authentication Agents without having a cloud-only Global Administrator account to fall back on.</span></span> <span data-ttu-id="f8792-107">[클라우드 전용 전역 관리자 계정 추가](../active-directory-users-create-azure-portal.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-107">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="f8792-108">이 단계를 수행하는 것이 중요하며 테넌트가 잠기지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-108">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>

## <a name="general-issues"></a><span data-ttu-id="f8792-109">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-109">General issues</span></span>

### <a name="check-status-of-the-feature-and-authentication-agents"></a><span data-ttu-id="f8792-110">기능 및 인증 에이전트의 상태 확인</span><span class="sxs-lookup"><span data-stu-id="f8792-110">Check status of the feature and Authentication Agents</span></span>

<span data-ttu-id="f8792-111">테넌트에서 통과 인증 기능이 여전히 **사용**으로 설정되고 인증 에이전트의 상태가 **비활성**이 아닌 **활성**으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-111">Ensure that the Pass-through Authentication feature is still **Enabled** on your tenant and the status of Authentication Agents shows **Active**, and not **Inactive**.</span></span> <span data-ttu-id="f8792-112">[Azure Active Directory 관리 센터](https://aad.portal.azure.com/)의 **Azure AD Connect** 블레이드로 이동하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-112">You can check status by going to the **Azure AD Connect** blade on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 관리 센터 - Azure AD Connect 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 관리 센터 - 통과 인증 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a><span data-ttu-id="f8792-115">사용자 관련 로그인 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="f8792-115">User-facing sign-in error messages</span></span>

<span data-ttu-id="f8792-116">사용자가 통과 인증을 통해 로그인할 수 없는 경우 Azure AD 로그인 화면에서 다음과 같은 사용자 관련 오류 메시지 중 하나가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-116">If the user is unable to sign into using Pass-through Authentication, they may see one of the following user-facing errors on the Azure AD sign-in screen:</span></span> 

|<span data-ttu-id="f8792-117">오류</span><span class="sxs-lookup"><span data-stu-id="f8792-117">Error</span></span>|<span data-ttu-id="f8792-118">설명</span><span class="sxs-lookup"><span data-stu-id="f8792-118">Description</span></span>|<span data-ttu-id="f8792-119">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f8792-119">Resolution</span></span>
| --- | --- | ---
|<span data-ttu-id="f8792-120">AADSTS80001</span><span class="sxs-lookup"><span data-stu-id="f8792-120">AADSTS80001</span></span>|<span data-ttu-id="f8792-121">Active Directory에 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="f8792-121">Unable to connect to Active Directory</span></span>|<span data-ttu-id="f8792-122">에이전트 서버가 자신의 암호에 대한 유효성이 검사되어야 하는 사용자와 동일한 AD 포리스트의 멤버이고 Active Directory에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-122">Ensure that agent servers are members of the same AD forest as the users whose passwords need to be validated and they are able to connect to Active Directory.</span></span>  
|<span data-ttu-id="f8792-123">AADSTS8002</span><span class="sxs-lookup"><span data-stu-id="f8792-123">AADSTS8002</span></span>|<span data-ttu-id="f8792-124">Active Directory에 연결하는 동안 시간 초과 발생</span><span class="sxs-lookup"><span data-stu-id="f8792-124">A timeout occurred connecting to Active Directory</span></span>|<span data-ttu-id="f8792-125">Active Directory를 사용할 수 있고 에이전트의 요청에 응답하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-125">Check to ensure that Active Directory is available and is responding to requests from the agents.</span></span>
|<span data-ttu-id="f8792-126">AADSTS80004</span><span class="sxs-lookup"><span data-stu-id="f8792-126">AADSTS80004</span></span>|<span data-ttu-id="f8792-127">에이전트에 전달된 사용자 이름이 유효하지 않음</span><span class="sxs-lookup"><span data-stu-id="f8792-127">The username passed to the agent was not valid</span></span>|<span data-ttu-id="f8792-128">사용자가 올바른 사용자 이름을 사용하여 로그인을 시도하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-128">Ensure the user is attempting to sign in with the right username.</span></span>
|<span data-ttu-id="f8792-129">AADSTS80005</span><span class="sxs-lookup"><span data-stu-id="f8792-129">AADSTS80005</span></span>|<span data-ttu-id="f8792-130">유효성 검사 중 예측할 수 없는 WebException 발생</span><span class="sxs-lookup"><span data-stu-id="f8792-130">Validation encountered unpredictable WebException</span></span>|<span data-ttu-id="f8792-131">일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-131">A transient error.</span></span> <span data-ttu-id="f8792-132">요청을 다시 시도하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8792-132">Retry the request.</span></span> <span data-ttu-id="f8792-133">계속 실패할 경우 Microsoft 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f8792-133">If it continues to fail, contact Microsoft support.</span></span>
|<span data-ttu-id="f8792-134">AADSTS80007</span><span class="sxs-lookup"><span data-stu-id="f8792-134">AADSTS80007</span></span>|<span data-ttu-id="f8792-135">Active Directory와 통신 중 오류 발생</span><span class="sxs-lookup"><span data-stu-id="f8792-135">An error occurred communicating with Active Directory</span></span>|<span data-ttu-id="f8792-136">에이전트 로그에서 자세한 정보를 확인하고 Active Directory가 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-136">Check the agent logs for more information and verify that Active Directory is operating as expected.</span></span>

### <a name="sign-in-failure-reasons-on-the-azure-active-directory-admin-center"></a><span data-ttu-id="f8792-137">Azure Active Directory 관리 센터에서 로그인이 실패한 이유</span><span class="sxs-lookup"><span data-stu-id="f8792-137">Sign-in failure reasons on the Azure Active Directory admin center</span></span>

<span data-ttu-id="f8792-138">[Azure Active Directory 관리 센터](https://aad.portal.azure.com/)에서 [로그인 활동 보고서](../active-directory-reporting-activity-sign-ins.md)를 살펴보고 사용자 로그인 문제 해결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-138">Start troubleshooting user sign-in issues by looking at the [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 관리 센터 - 로그인 보고서](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

<span data-ttu-id="f8792-140">[Azure Active Directory 관리 센터](https://aad.portal.azure.com/)에서 **Azure Active Directory** -> **로그인**으로 차례로 이동하고 특정 사용자의 로그인 활동을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-140">Navigate to **Azure Active Directory** -> **Sign-ins** on the [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="f8792-141">**로그인 오류 코드** 필드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-141">Look for the **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="f8792-142">다음 표를 사용하여 해당 필드의 값을 실패 이유 및 해결에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-142">Map the value of that field to a failure reason and resolution using the following table:</span></span>

|<span data-ttu-id="f8792-143">로그인 오류 코드</span><span class="sxs-lookup"><span data-stu-id="f8792-143">Sign-in error code</span></span>|<span data-ttu-id="f8792-144">로그인 실패 이유</span><span class="sxs-lookup"><span data-stu-id="f8792-144">Sign-in failure reason</span></span>|<span data-ttu-id="f8792-145">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f8792-145">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="f8792-146">50144</span><span class="sxs-lookup"><span data-stu-id="f8792-146">50144</span></span> | <span data-ttu-id="f8792-147">사용자의 Active Directory 암호가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-147">User's Active Directory password has expired.</span></span> | <span data-ttu-id="f8792-148">온-프레미스 Active Directory에서 사용자의 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-148">Reset the user's password in your on-premises Active Directory.</span></span>
| <span data-ttu-id="f8792-149">80001</span><span class="sxs-lookup"><span data-stu-id="f8792-149">80001</span></span> | <span data-ttu-id="f8792-150">사용할 수 있는 인증 에이전트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-150">No Authentication Agent available.</span></span> | <span data-ttu-id="f8792-151">인증 에이전트를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-151">Install and register an Authentication Agent.</span></span>
| <span data-ttu-id="f8792-152">80002</span><span class="sxs-lookup"><span data-stu-id="f8792-152">80002</span></span> | <span data-ttu-id="f8792-153">인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-153">Authentication Agent's password validation request timed out.</span></span> | <span data-ttu-id="f8792-154">인증 에이전트에서 Active Directory에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-154">Check if your Active Directory is reachable from the Authentication Agent.</span></span>
| <span data-ttu-id="f8792-155">80003</span><span class="sxs-lookup"><span data-stu-id="f8792-155">80003</span></span> | <span data-ttu-id="f8792-156">인증 에이전트에서 받은 응답이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-156">Invalid response received by Authentication Agent.</span></span> | <span data-ttu-id="f8792-157">여러 사용자 간에 일관되게 재현될 수 있는 문제이면 Active Directory 구성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-157">If the problem is consistently reproducible across multiple users, check your Active Directory configuration.</span></span>
| <span data-ttu-id="f8792-158">80004</span><span class="sxs-lookup"><span data-stu-id="f8792-158">80004</span></span> | <span data-ttu-id="f8792-159">로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-159">Incorrect User Principal Name (UPN) used in sign-in request.</span></span> | <span data-ttu-id="f8792-160">사용자에게 올바른 사용자 이름으로 로그인하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-160">Ask the user to sign in with the correct username.</span></span>
| <span data-ttu-id="f8792-161">80005</span><span class="sxs-lookup"><span data-stu-id="f8792-161">80005</span></span> | <span data-ttu-id="f8792-162">인증 에이전트: 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-162">Authentication Agent: Error occurred.</span></span> | <span data-ttu-id="f8792-163">일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-163">Transient error.</span></span> <span data-ttu-id="f8792-164">나중에 다시 시도하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8792-164">Try again later.</span></span>
| <span data-ttu-id="f8792-165">80007</span><span class="sxs-lookup"><span data-stu-id="f8792-165">80007</span></span> | <span data-ttu-id="f8792-166">인증 에이전트에서 Active Directory에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-166">Authentication Agent unable to connect to Active Directory.</span></span> | <span data-ttu-id="f8792-167">인증 에이전트에서 Active Directory에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-167">Check if your Active Directory is reachable from the Authentication Agent.</span></span>
| <span data-ttu-id="f8792-168">80010</span><span class="sxs-lookup"><span data-stu-id="f8792-168">80010</span></span> | <span data-ttu-id="f8792-169">인증 에이전트에서 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-169">Authentication Agent unable to decrypt password.</span></span> | <span data-ttu-id="f8792-170">일관되게 재현될 수 있는 문제이면 새 인증 에이전트를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-170">If the problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="f8792-171">그리고 현재의 인증 에이전트는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-171">And uninstall the current one.</span></span> 
| <span data-ttu-id="f8792-172">80011</span><span class="sxs-lookup"><span data-stu-id="f8792-172">80011</span></span> | <span data-ttu-id="f8792-173">인증 에이전트에서 암호 해독 키를 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-173">Authentication Agent unable to retrieve decryption key.</span></span> | <span data-ttu-id="f8792-174">일관되게 재현될 수 있는 문제이면 새 인증 에이전트를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-174">If the problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="f8792-175">그리고 현재의 인증 에이전트는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-175">And uninstall the current one.</span></span>

## <a name="authentication-agent-installation-issues"></a><span data-ttu-id="f8792-176">인증 에이전트 설치 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-176">Authentication Agent installation issues</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="f8792-177">예기치 않은 오류가 발생함</span><span class="sxs-lookup"><span data-stu-id="f8792-177">An unexpected error occurred</span></span>

<span data-ttu-id="f8792-178">서버에서 [에이전트 로그를 수집](#collecting-pass-through-authentication-agent-logs)하고 문제와 관련하여 Microsoft 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f8792-178">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from the server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-registration-issues"></a><span data-ttu-id="f8792-179">인증 에이전트 등록 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-179">Authentication Agent registration issues</span></span>

### <a name="registration-of-the-authentication-agent-failed-due-to-blocked-ports"></a><span data-ttu-id="f8792-180">차단된 포트로 인해 인증 에이전트 등록에 실패함</span><span class="sxs-lookup"><span data-stu-id="f8792-180">Registration of the Authentication Agent failed due to blocked ports</span></span>

<span data-ttu-id="f8792-181">인증 에이전트가 설치된 서버가 [여기](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)에 나열된 서비스 URL 및 포트와 통신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-181">Ensure that the server on which the Authentication Agent has been installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="registration-of-the-authentication-agent-failed-due-to-token-or-account-authorization-errors"></a><span data-ttu-id="f8792-182">토큰 또는 계정 권한 부여 오류로 인해 인증 에이전트 등록에 실패함</span><span class="sxs-lookup"><span data-stu-id="f8792-182">Registration of the Authentication Agent failed due to token or account authorization errors</span></span>

<span data-ttu-id="f8792-183">모든 Azure AD Connect 또는 독립 실행형 인증 에이전트 설치 및 등록 작업에는 클라우드 전용 전역 관리자 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-183">Ensure that you use a cloud-only Global Administrator account for all Azure AD Connect or standalone Authentication Agent installation and registration operations.</span></span> <span data-ttu-id="f8792-184">MFA 사용 전역 관리자 계정에 알려진 문제점이 있습니다. 해결 방법으로 MFA를 일시적으로 해제하세요(작업 완료를 위해서만).</span><span class="sxs-lookup"><span data-stu-id="f8792-184">There is a known issue with MFA-enabled Global Administrator accounts; turn off MFA temporarily (only to complete the operations) as a workaround.</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="f8792-185">예기치 않은 오류가 발생함</span><span class="sxs-lookup"><span data-stu-id="f8792-185">An unexpected error occurred</span></span>

<span data-ttu-id="f8792-186">서버에서 [에이전트 로그를 수집](#collecting-pass-through-authentication-agent-logs)하고 문제와 관련하여 Microsoft 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f8792-186">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from the server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-uninstallation-issues"></a><span data-ttu-id="f8792-187">인증 에이전트 제거 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-187">Authentication Agent uninstallation issues</span></span>

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a><span data-ttu-id="f8792-188">Azure AD Connect 제거 시 나타나는 경고 메시지</span><span class="sxs-lookup"><span data-stu-id="f8792-188">Warning message when uninstalling Azure AD Connect</span></span>

<span data-ttu-id="f8792-189">테넌트에서 통과 인증을 사용하도록 설정했고 Azure AD Connect를 제거하려고 하면 "다른 통과 인증 에이전트가 다른 서버에 설치되어 있지 않으면 사용자가 Azure AD에 로그인할 수 없습니다."라는 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-189">If you have Pass-through Authentication enabled on your tenant and you try to uninstall Azure AD Connect, it shows you the following warning message: "Users will not be able to sign-in to Azure AD unless you have other Pass-through Authentication agents installed on other servers."</span></span>

<span data-ttu-id="f8792-190">사용자 로그인이 중단되지 않도록 방지하려면 Azure AD Connect를 제거하기 전에 설정이 [고가용성](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-190">Ensure that your setup is [high available](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) before you uninstall Azure AD Connect to avoid breaking user sign-in.</span></span>

## <a name="issues-with-enabling-the-feature"></a><span data-ttu-id="f8792-191">기능 사용 관련 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-191">Issues with enabling the feature</span></span>

### <a name="enabling-the-feature-failed-because-there-were-no-authentication-agents-available"></a><span data-ttu-id="f8792-192">사용 가능한 인증 에이전트가 없어 기능을 사용하도록 설정하지 못함</span><span class="sxs-lookup"><span data-stu-id="f8792-192">Enabling the feature failed because there were no Authentication Agents available</span></span>

<span data-ttu-id="f8792-193">테넌트에서 통과 인증을 사용하도록 설정하려면 하나 이상의 활성 인증 에이전트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-193">You need to have at least one active Authentication Agent to enable Pass-through Authentication on your tenant.</span></span> <span data-ttu-id="f8792-194">Azure AD Connect 또는 독립 실행형 인증 에이전트를 설치하여 인증 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-194">You can install an Authentication Agent by either installing Azure AD Connect or a standalone Authentication Agent.</span></span>

### <a name="enabling-the-feature-failed-due-to-blocked-ports"></a><span data-ttu-id="f8792-195">차단된 포트로 인해 기능을 사용하도록 설정하지 못함</span><span class="sxs-lookup"><span data-stu-id="f8792-195">Enabling the feature failed due to blocked ports</span></span>

<span data-ttu-id="f8792-196">Azure AD Connect가 설치된 서버가 [여기](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)에 나열된 서비스 URL 및 포트와 통신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-196">Ensure that the server on which Azure AD Connect is installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="enabling-the-feature-failed-due-to-token-or-account-authorization-errors"></a><span data-ttu-id="f8792-197">토큰 또는 계정 권한 부여 오류로 인해 기능을 사용하도록 설정하지 못함</span><span class="sxs-lookup"><span data-stu-id="f8792-197">Enabling the feature failed due to token or account authorization errors</span></span>

<span data-ttu-id="f8792-198">기능을 활성화할 때는 클라우드 전용 전역 관리자 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-198">Ensure that you use a cloud-only Global Administrator account when enabling the feature.</span></span> <span data-ttu-id="f8792-199">MFA(Multi-Factor Authentication) 사용 전역 관리자 계정에 알려진 문제점이 있습니다. 해결 방법으로 MFA를 일시적으로 해제하세요(작업 완료를 위해서만).</span><span class="sxs-lookup"><span data-stu-id="f8792-199">There is a known issue with multi-factor authentication (MFA)-enabled Global Administrator accounts; turn off MFA temporarily (only to complete the operation) as a workaround.</span></span>

## <a name="exchange-activesync-configuration-issues"></a><span data-ttu-id="f8792-200">Exchange ActiveSync 구성 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-200">Exchange ActiveSync configuration issues</span></span>

<span data-ttu-id="f8792-201">이들은 통과 인증에 대한 Exchange ActiveSync 지원을 구성할 때 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-201">These are the common issues when you configure Exchange ActiveSync support for Pass-through Authentication.</span></span>

### <a name="exchange-powershell-issue"></a><span data-ttu-id="f8792-202">Exchange PowerShell 문제</span><span class="sxs-lookup"><span data-stu-id="f8792-202">Exchange PowerShell issue</span></span>

<span data-ttu-id="f8792-203">표시는 "**'PerTenantSwitchToESTSEnabled' 매개 변수 이름과 일치 하는 매개 변수를 찾을 수 없습니다\.**"</span><span class="sxs-lookup"><span data-stu-id="f8792-203">If you see the "**A parameter cannot be found that matches parameter name 'PerTenantSwitchToESTSEnabled'\.**"</span></span> <span data-ttu-id="f8792-204">실행 하는 동안 오류가 발생 했습니다.는 `Set-OrganizationConfig` Exchange PowerShell 명령를 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-204">error when you run the `Set-OrganizationConfig` Exchange PowerShell command, contact Microsoft Support.</span></span>

### <a name="exchange-activesync-not-working"></a><span data-ttu-id="f8792-205">Exchange ActiveSync가 작동하지 않음</span><span class="sxs-lookup"><span data-stu-id="f8792-205">Exchange ActiveSync not working</span></span>

<span data-ttu-id="f8792-206">구성을 적용하는 데 다소 시간이 걸립니다. 시간은 사용자 환경에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-206">The configuration takes some time to take effect - the time period depends on your environment.</span></span> <span data-ttu-id="f8792-207">오랜 시간 동안 상황이 지속되면 Microsoft 지원에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-207">If the situation persists for a long time, contact Microsoft Support.</span></span>

## <a name="collecting-pass-through-authentication-agent-logs"></a><span data-ttu-id="f8792-208">통과 인증 에이전트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="f8792-208">Collecting Pass-through Authentication Agent logs</span></span>

<span data-ttu-id="f8792-209">발생하는 문제의 유형에 따라 다른 위치에서 통과 인증 에이전트 로그를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-209">Depending on the type of issue you may have, you need to look in different places for Pass-through Authentication Agent logs.</span></span>

### <a name="authentication-agent-event-logs"></a><span data-ttu-id="f8792-210">인증 에이전트 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="f8792-210">Authentication Agent event logs</span></span>

<span data-ttu-id="f8792-211">인증 에이전트 관련 오류의 경우 서버에서 이벤트 뷰어 응용 프로그램을 열고 **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-211">For errors related to the Authentication Agent, open up the Event Viewer application on the server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.</span></span>

<span data-ttu-id="f8792-212">자세한 분석을 위해 "세션" 로그를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-212">For detailed analytics, enable the "Session" log.</span></span> <span data-ttu-id="f8792-213">정상 작동 중에는 이 로그를 활성화한 상태에서 인증 에이전트를 실행하지 마세요. 문제 해결에만 이 로그를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="f8792-213">Don't run the Authentication Agent with this log enabled during normal operations; use only for troubleshooting.</span></span> <span data-ttu-id="f8792-214">로그 내용은 로그를 다시 비활성화한 후에만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-214">The log contents are only visible after the log is disabled again.</span></span>

### <a name="detailed-trace-logs"></a><span data-ttu-id="f8792-215">자세한 추적 로그</span><span class="sxs-lookup"><span data-stu-id="f8792-215">Detailed trace logs</span></span>

<span data-ttu-id="f8792-216">사용자 로그인 실패 문제를 해결하려면 **%programdata%\Microsoft\Azure AD Connect Authentication Agent\Trace\\**에서 추적 로그를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-216">To troubleshoot user sign-in failures, look for trace logs at **%programdata%\Microsoft\Azure AD Connect Authentication Agent\Trace\\**.</span></span> <span data-ttu-id="f8792-217">이러한 로그에는 통과 인증 기능을 통해 특정 사용자 로그인이 실패한 이유가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-217">These logs include reasons why a specific user sign-in failed using the Pass-through Authentication feature.</span></span> <span data-ttu-id="f8792-218">이러한 오류는 이전의 [표](#sign-in-failure-reasons-on-the-Azure-portal)에 나오는 로그인 실패 이유에도 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-218">These errors are also mapped to the sign-in failure reasons shown in the preceding [table](#sign-in-failure-reasons-on-the-Azure-portal).</span></span> <span data-ttu-id="f8792-219">다음은 로그 항목의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-219">Following is an example log entry:</span></span>

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

<span data-ttu-id="f8792-220">명령 프롬프트를 열고 다음 명령을 실행하면 오류(위 예제의 경우 '1328')에 대한 자세한 설명을 얻을 수 있습니다. 참고: '1328'을 로그에 표시되는 실제 오류 번호로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="f8792-220">You can get descriptive details of the error ('1328' in the preceding example) by opening up the command prompt and running the following command (Note: Replace '1328' with the actual error number that you see in your logs):</span></span>

`Net helpmsg 1328`

![통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a><span data-ttu-id="f8792-222">도메인 컨트롤러 로그</span><span class="sxs-lookup"><span data-stu-id="f8792-222">Domain Controller logs</span></span>

<span data-ttu-id="f8792-223">감사 로깅이 사용되는 경우에는 도메인 컨트롤러의 보안 로그에서도 추가 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-223">If audit logging is enabled, additional information can be found in the security logs of your Domain Controllers.</span></span> <span data-ttu-id="f8792-224">통과 인증 에이전트에서 보낸 로그인 요청을 쿼리하는 간단한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-224">A simple way to query sign-in requests sent by Pass-through Authentication Agents is as follows:</span></span>

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a><span data-ttu-id="f8792-225">성능 모니터 카운터</span><span class="sxs-lookup"><span data-stu-id="f8792-225">Performance Monitor counters</span></span>

<span data-ttu-id="f8792-226">인증 에이전트를 모니터링하는 다른 방법은 인증 에이전트가 설치된 각 서버에서 특정 성능 모니터 카운터를 추적하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-226">Another way to monitor Authentication Agents is to track specific Performance Monitor counters on each server where the Authentication Agent is installed.</span></span> <span data-ttu-id="f8792-227">다음 전역 카운터(**# PTA 인증**, **#PTA 실패 인증** 및 **#PTA 성공 인증**) 및 오류 카운터(**# PTA 인증 오류**)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-227">Use the following Global counters (**# PTA authentications**, **#PTA failed authentications** and **#PTA successful authentications**) and Error counters (**# PTA authentication errors**):</span></span>

![통과 인증 성능 모니터 카운터](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
><span data-ttu-id="f8792-229">통과 인증은 여러 인증 에이전트를 사용하여 고가용성을 제공하지만 부하 분산 기능은 제공하지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="f8792-229">Pass-through Authentication provides high availability using multiple Authentication Agents, and _not_ load balancing.</span></span> <span data-ttu-id="f8792-230">구성에 따라 모든 인증 에이전트는 요청과 _동일한_ 수를 수신하지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="f8792-230">Depending on your configuration, _not_ all your Authentication Agents receive roughly _equal_ number of requests.</span></span> <span data-ttu-id="f8792-231">특정 인증 에이전트는 트래픽을 전혀 수신하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8792-231">It is possible that a specific Authentication Agent receives no traffic at all.</span></span>
