---
title: "Azure AD Connect: 통과 인증 문제 해결 | Microsoft 문서"
description: "이 문서에서는 설명 방법을 tootroubleshoot Azure Active Directory (Azure AD) 통과 인증 합니다."
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
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="c963a-104">Azure Active Directory 통과 인증 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c963a-104">Troubleshoot Azure Active Directory Pass-through Authentication</span></span>

<span data-ttu-id="c963a-105">이 문서에서는 Azure AD 통과 인증과 관련된 일반적인 문제에 대한 문제 해결 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-105">This article helps you find troubleshooting information about common issues regarding Azure AD Pass-through Authentication.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c963a-106">통과 인증으로 사용자 로그인 문제에 직면 하, 경우 hello 기능을 사용 하지 않도록 설정 하거나 클라우드 전용 전역 관리자 계정 toofall 다시 필요 없이 통과 인증 에이전트를 제거 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-106">If you are facing user sign-in issues with Pass-through Authentication, don't disable hello feature or uninstall Pass-through Authentication Agents without having a cloud-only Global Administrator account toofall back on.</span></span> <span data-ttu-id="c963a-107">[클라우드 전용 전역 관리자 계정 추가](../active-directory-users-create-azure-portal.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-107">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="c963a-108">이 단계를 수행하는 것이 중요하며 테넌트가 잠기지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-108">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>

## <a name="general-issues"></a><span data-ttu-id="c963a-109">일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-109">General issues</span></span>

### <a name="check-status-of-hello-feature-and-authentication-agents"></a><span data-ttu-id="c963a-110">Hello 기능 및 인증 에이전트의 상태 확인</span><span class="sxs-lookup"><span data-stu-id="c963a-110">Check status of hello feature and Authentication Agents</span></span>

<span data-ttu-id="c963a-111">해당 hello 통과 인증 기능은 아직 확인 **Enabled** 인증 에이전트의 테 넌 트 및 hello 상태를 보여 줍니다. **활성**, 아닌 **비활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-111">Ensure that hello Pass-through Authentication feature is still **Enabled** on your tenant and hello status of Authentication Agents shows **Active**, and not **Inactive**.</span></span> <span data-ttu-id="c963a-112">Toohello 이동 하 여 상태를 확인할 수 있습니다 **Azure AD Connect** hello에 블레이드 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-112">You can check status by going toohello **Azure AD Connect** blade on hello [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 관리 센터 - Azure AD Connect 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 관리 센터 - 통과 인증 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a><span data-ttu-id="c963a-115">사용자 관련 로그인 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="c963a-115">User-facing sign-in error messages</span></span>

<span data-ttu-id="c963a-116">Hello 사용자가 없습니다 toosign 통과 인증을 사용 하 여, hello hello Azure AD 로그인 화면에 다음 사용자 용 오류 중 하나가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-116">If hello user is unable toosign into using Pass-through Authentication, they may see one of hello following user-facing errors on hello Azure AD sign-in screen:</span></span> 

|<span data-ttu-id="c963a-117">오류</span><span class="sxs-lookup"><span data-stu-id="c963a-117">Error</span></span>|<span data-ttu-id="c963a-118">설명</span><span class="sxs-lookup"><span data-stu-id="c963a-118">Description</span></span>|<span data-ttu-id="c963a-119">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c963a-119">Resolution</span></span>
| --- | --- | ---
|<span data-ttu-id="c963a-120">AADSTS80001</span><span class="sxs-lookup"><span data-stu-id="c963a-120">AADSTS80001</span></span>|<span data-ttu-id="c963a-121">없습니다 tooconnect tooActive 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c963a-121">Unable tooconnect tooActive Directory</span></span>|<span data-ttu-id="c963a-122">에이전트 서버는 해당 암호가 필요 toobe 유효성을 검사 하는 hello 사용자로 hello 동일한 AD 포리스트의 구성원 수 tooconnect tooActive 디렉터리 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-122">Ensure that agent servers are members of hello same AD forest as hello users whose passwords need toobe validated and they are able tooconnect tooActive Directory.</span></span>  
|<span data-ttu-id="c963a-123">AADSTS8002</span><span class="sxs-lookup"><span data-stu-id="c963a-123">AADSTS8002</span></span>|<span data-ttu-id="c963a-124">시간 초과가 발생 연결 tooActive 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c963a-124">A timeout occurred connecting tooActive Directory</span></span>|<span data-ttu-id="c963a-125">Tooensure Active Directory를 사용할 수 및 toorequests hello 에이전트 로부터 응답을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-125">Check tooensure that Active Directory is available and is responding toorequests from hello agents.</span></span>
|<span data-ttu-id="c963a-126">AADSTS80004</span><span class="sxs-lookup"><span data-stu-id="c963a-126">AADSTS80004</span></span>|<span data-ttu-id="c963a-127">toohello 에이전트 전달 hello 사용자 이름이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-127">hello username passed toohello agent was not valid</span></span>|<span data-ttu-id="c963a-128">Hello 사용자가 올바른 사용자 hello 사용 하 여 toosign 시도 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-128">Ensure hello user is attempting toosign in with hello right username.</span></span>
|<span data-ttu-id="c963a-129">AADSTS80005</span><span class="sxs-lookup"><span data-stu-id="c963a-129">AADSTS80005</span></span>|<span data-ttu-id="c963a-130">유효성 검사 중 예측할 수 없는 WebException 발생</span><span class="sxs-lookup"><span data-stu-id="c963a-130">Validation encountered unpredictable WebException</span></span>|<span data-ttu-id="c963a-131">일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-131">A transient error.</span></span> <span data-ttu-id="c963a-132">Hello 요청을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-132">Retry hello request.</span></span> <span data-ttu-id="c963a-133">Toofail 계속 하는 경우 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-133">If it continues toofail, contact Microsoft support.</span></span>
|<span data-ttu-id="c963a-134">AADSTS80007</span><span class="sxs-lookup"><span data-stu-id="c963a-134">AADSTS80007</span></span>|<span data-ttu-id="c963a-135">Active Directory와 통신 중 오류 발생</span><span class="sxs-lookup"><span data-stu-id="c963a-135">An error occurred communicating with Active Directory</span></span>|<span data-ttu-id="c963a-136">자세한 내용은 hello 에이전트 로그를 확인 하 고 Active Directory가 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-136">Check hello agent logs for more information and verify that Active Directory is operating as expected.</span></span>

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a><span data-ttu-id="c963a-137">Hello Azure Active Directory 관리 센터에 로그인 실패 이유</span><span class="sxs-lookup"><span data-stu-id="c963a-137">Sign-in failure reasons on hello Azure Active Directory admin center</span></span>

<span data-ttu-id="c963a-138">Hello 확인 하 여 사용자 로그인 관련 문제를 해결 [로그인 활동 보고서](../active-directory-reporting-activity-sign-ins.md) hello에 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-138">Start troubleshooting user sign-in issues by looking at hello [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on hello [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 관리 센터 - 로그인 보고서](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

<span data-ttu-id="c963a-140">너무 이동**Azure Active Directory** -> **로그인** hello에 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/) 특정 사용자의 로그인 활동을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-140">Navigate too**Azure Active Directory** -> **Sign-ins** on hello [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="c963a-141">Hello에 대 한 확인 **로그인 오류 코드** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-141">Look for hello **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="c963a-142">해당 필드 tooa 실패 이유 및 다음 표에 hello를 사용 하는 확인의 hello 값을 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-142">Map hello value of that field tooa failure reason and resolution using hello following table:</span></span>

|<span data-ttu-id="c963a-143">로그인 오류 코드</span><span class="sxs-lookup"><span data-stu-id="c963a-143">Sign-in error code</span></span>|<span data-ttu-id="c963a-144">로그인 실패 이유</span><span class="sxs-lookup"><span data-stu-id="c963a-144">Sign-in failure reason</span></span>|<span data-ttu-id="c963a-145">해결 방법</span><span class="sxs-lookup"><span data-stu-id="c963a-145">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="c963a-146">50144</span><span class="sxs-lookup"><span data-stu-id="c963a-146">50144</span></span> | <span data-ttu-id="c963a-147">사용자의 Active Directory 암호가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-147">User's Active Directory password has expired.</span></span> | <span data-ttu-id="c963a-148">온-프레미스 Active Directory에서 hello 사용자의 암호를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-148">Reset hello user's password in your on-premises Active Directory.</span></span>
| <span data-ttu-id="c963a-149">80001</span><span class="sxs-lookup"><span data-stu-id="c963a-149">80001</span></span> | <span data-ttu-id="c963a-150">사용할 수 있는 인증 에이전트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-150">No Authentication Agent available.</span></span> | <span data-ttu-id="c963a-151">인증 에이전트를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-151">Install and register an Authentication Agent.</span></span>
| <span data-ttu-id="c963a-152">80002</span><span class="sxs-lookup"><span data-stu-id="c963a-152">80002</span></span> | <span data-ttu-id="c963a-153">인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-153">Authentication Agent's password validation request timed out.</span></span> | <span data-ttu-id="c963a-154">Active Directory hello 인증 에이전트에서에서 연결할 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-154">Check if your Active Directory is reachable from hello Authentication Agent.</span></span>
| <span data-ttu-id="c963a-155">80003</span><span class="sxs-lookup"><span data-stu-id="c963a-155">80003</span></span> | <span data-ttu-id="c963a-156">인증 에이전트에서 받은 응답이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-156">Invalid response received by Authentication Agent.</span></span> | <span data-ttu-id="c963a-157">여러 사용자 간에 일관 되 게 재현할 수 있는 hello 문제가 발생 하면 Active Directory 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-157">If hello problem is consistently reproducible across multiple users, check your Active Directory configuration.</span></span>
| <span data-ttu-id="c963a-158">80004</span><span class="sxs-lookup"><span data-stu-id="c963a-158">80004</span></span> | <span data-ttu-id="c963a-159">로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-159">Incorrect User Principal Name (UPN) used in sign-in request.</span></span> | <span data-ttu-id="c963a-160">올바른 사용자 이름 hello 사용 하 여 hello 사용자 toosign를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-160">Ask hello user toosign in with hello correct username.</span></span>
| <span data-ttu-id="c963a-161">80005</span><span class="sxs-lookup"><span data-stu-id="c963a-161">80005</span></span> | <span data-ttu-id="c963a-162">인증 에이전트: 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-162">Authentication Agent: Error occurred.</span></span> | <span data-ttu-id="c963a-163">일시적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-163">Transient error.</span></span> <span data-ttu-id="c963a-164">나중에 다시 시도하십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-164">Try again later.</span></span>
| <span data-ttu-id="c963a-165">80007</span><span class="sxs-lookup"><span data-stu-id="c963a-165">80007</span></span> | <span data-ttu-id="c963a-166">인증 에이전트 수 없습니다 tooconnect tooActive 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-166">Authentication Agent unable tooconnect tooActive Directory.</span></span> | <span data-ttu-id="c963a-167">Active Directory hello 인증 에이전트에서에서 연결할 수 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-167">Check if your Active Directory is reachable from hello Authentication Agent.</span></span>
| <span data-ttu-id="c963a-168">80010</span><span class="sxs-lookup"><span data-stu-id="c963a-168">80010</span></span> | <span data-ttu-id="c963a-169">인증 에이전트 수 없습니다 toodecrypt 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-169">Authentication Agent unable toodecrypt password.</span></span> | <span data-ttu-id="c963a-170">Hello 문제는 일관 되 게 재현할 수 있는 경우 설치 하 고 새 인증 에이전트에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-170">If hello problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="c963a-171">및 현재 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-171">And uninstall hello current one.</span></span> 
| <span data-ttu-id="c963a-172">80011</span><span class="sxs-lookup"><span data-stu-id="c963a-172">80011</span></span> | <span data-ttu-id="c963a-173">인증 에이전트 수 없습니다 tooretrieve 암호 해독 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-173">Authentication Agent unable tooretrieve decryption key.</span></span> | <span data-ttu-id="c963a-174">Hello 문제는 일관 되 게 재현할 수 있는 경우 설치 하 고 새 인증 에이전트에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-174">If hello problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="c963a-175">및 현재 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-175">And uninstall hello current one.</span></span>

## <a name="authentication-agent-installation-issues"></a><span data-ttu-id="c963a-176">인증 에이전트 설치 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-176">Authentication Agent installation issues</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="c963a-177">예기치 않은 오류가 발생함</span><span class="sxs-lookup"><span data-stu-id="c963a-177">An unexpected error occurred</span></span>

<span data-ttu-id="c963a-178">[에이전트 로그를 수집](#collecting-pass-through-authentication-agent-logs) hello 서버 및 해당 문제에 대해 Microsoft 지원에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-178">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from hello server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-registration-issues"></a><span data-ttu-id="c963a-179">인증 에이전트 등록 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-179">Authentication Agent registration issues</span></span>

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a><span data-ttu-id="c963a-180">Tooblocked 포트 인해 hello 인증 에이전트를 등록 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-180">Registration of hello Authentication Agent failed due tooblocked ports</span></span>

<span data-ttu-id="c963a-181">어떤 hello에 인증 에이전트 설치가 완료 된 후 해당 hello 서버 Url 및 포트에 나열 된 서비스와 통신할 수 확인 [여기](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-181">Ensure that hello server on which hello Authentication Agent has been installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a><span data-ttu-id="c963a-182">권한 부여 오류 tootoken 또는 계정 인해 hello 인증 에이전트를 등록 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-182">Registration of hello Authentication Agent failed due tootoken or account authorization errors</span></span>

<span data-ttu-id="c963a-183">모든 Azure AD Connect 또는 독립 실행형 인증 에이전트 설치 및 등록 작업에는 클라우드 전용 전역 관리자 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-183">Ensure that you use a cloud-only Global Administrator account for all Azure AD Connect or standalone Authentication Agent installation and registration operations.</span></span> <span data-ttu-id="c963a-184">MFA 활성화 전역 관리자 계정, 알려진된 문제는 해결 방법으로 MFA 일시적으로 (만 toocomplete hello 작업)를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-184">There is a known issue with MFA-enabled Global Administrator accounts; turn off MFA temporarily (only toocomplete hello operations) as a workaround.</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="c963a-185">예기치 않은 오류가 발생함</span><span class="sxs-lookup"><span data-stu-id="c963a-185">An unexpected error occurred</span></span>

<span data-ttu-id="c963a-186">[에이전트 로그를 수집](#collecting-pass-through-authentication-agent-logs) hello 서버 및 해당 문제에 대해 Microsoft 지원에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c963a-186">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from hello server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-uninstallation-issues"></a><span data-ttu-id="c963a-187">인증 에이전트 제거 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-187">Authentication Agent uninstallation issues</span></span>

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a><span data-ttu-id="c963a-188">Azure AD Connect 제거 시 나타나는 경고 메시지</span><span class="sxs-lookup"><span data-stu-id="c963a-188">Warning message when uninstalling Azure AD Connect</span></span>

<span data-ttu-id="c963a-189">통과 인증을 테 넌 트에 사용할 수 있고 toouninstall Azure AD Connect를 시도 하는 경우 아래와 같은 경고 메시지가 hello 표시: "사용자 됩니다 수에서 toosign tooAzure AD 다른 통과 인증 에이전트 없는 경우 다른 서버에 설치 합니다. "</span><span class="sxs-lookup"><span data-stu-id="c963a-189">If you have Pass-through Authentication enabled on your tenant and you try toouninstall Azure AD Connect, it shows you hello following warning message: "Users will not be able toosign-in tooAzure AD unless you have other Pass-through Authentication agents installed on other servers."</span></span>

<span data-ttu-id="c963a-190">설치 프로그램 인지 확인 [높은 사용 가능한](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) Azure AD Connect tooavoid 주요 사용자 로그인을 제거 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="c963a-190">Ensure that your setup is [high available](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) before you uninstall Azure AD Connect tooavoid breaking user sign-in.</span></span>

## <a name="issues-with-enabling-hello-feature"></a><span data-ttu-id="c963a-191">Hello 기능을 사용 하면 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-191">Issues with enabling hello feature</span></span>

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a><span data-ttu-id="c963a-192">인증 에이전트가 없습니다 없었기 때문에 hello 기능을 사용 하도록 설정 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-192">Enabling hello feature failed because there were no Authentication Agents available</span></span>

<span data-ttu-id="c963a-193">Toohave 필요한 하나 이상의 활성 인증 에이전트 tooenable 통과 인증 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-193">You need toohave at least one active Authentication Agent tooenable Pass-through Authentication on your tenant.</span></span> <span data-ttu-id="c963a-194">Azure AD Connect 또는 독립 실행형 인증 에이전트를 설치하여 인증 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-194">You can install an Authentication Agent by either installing Azure AD Connect or a standalone Authentication Agent.</span></span>

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a><span data-ttu-id="c963a-195">Tooblocked 포트 hello 기능을 사용 하면 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-195">Enabling hello feature failed due tooblocked ports</span></span>

<span data-ttu-id="c963a-196">Azure AD Connect가 설치 된 해당 hello 서버 Url 및 포트에 나열 된 서비스와 통신할 수 확인 [여기](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-196">Ensure that hello server on which Azure AD Connect is installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a><span data-ttu-id="c963a-197">Tootoken 또는 계정 권한 부여 오류 hello 기능을 사용 하면 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-197">Enabling hello feature failed due tootoken or account authorization errors</span></span>

<span data-ttu-id="c963a-198">Hello 기능을 사용 하면 클라우드 전용 전역 관리자 계정을 사용 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-198">Ensure that you use a cloud-only Global Administrator account when enabling hello feature.</span></span> <span data-ttu-id="c963a-199">Multi-factor authentication (MFA) 알려진 문제가-전역 관리자 계정, 사용 하도록 설정 해결 방법으로 MFA 일시적으로 (만 toocomplete hello 작업)를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-199">There is a known issue with multi-factor authentication (MFA)-enabled Global Administrator accounts; turn off MFA temporarily (only toocomplete hello operation) as a workaround.</span></span>

## <a name="exchange-activesync-configuration-issues"></a><span data-ttu-id="c963a-200">Exchange ActiveSync 구성 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-200">Exchange ActiveSync configuration issues</span></span>

<span data-ttu-id="c963a-201">통과 인증에 대 한 Exchange ActiveSync 지원을 구성 하는 경우 이들은 hello 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-201">These are hello common issues when you configure Exchange ActiveSync support for Pass-through Authentication.</span></span>

### <a name="exchange-powershell-issue"></a><span data-ttu-id="c963a-202">Exchange PowerShell 문제</span><span class="sxs-lookup"><span data-stu-id="c963a-202">Exchange PowerShell issue</span></span>

<span data-ttu-id="c963a-203">Hello 표시 되 면 "**'PerTenantSwitchToESTSEnabled' 매개 변수 이름과 일치 하는 매개 변수를 찾을 수 없습니다\.**"</span><span class="sxs-lookup"><span data-stu-id="c963a-203">If you see hello "**A parameter cannot be found that matches parameter name 'PerTenantSwitchToESTSEnabled'\.**"</span></span> <span data-ttu-id="c963a-204">hello를 실행 하는 동안 오류가 발생 했습니다. `Set-OrganizationConfig` Exchange PowerShell 명령를 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-204">error when you run hello `Set-OrganizationConfig` Exchange PowerShell command, contact Microsoft Support.</span></span>

### <a name="exchange-activesync-not-working"></a><span data-ttu-id="c963a-205">Exchange ActiveSync가 작동하지 않음</span><span class="sxs-lookup"><span data-stu-id="c963a-205">Exchange ActiveSync not working</span></span>

<span data-ttu-id="c963a-206">hello 구성에서는 일부 시간 tootake 효과 가져와서-hello 시간 동안 사용자 환경에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-206">hello configuration takes some time tootake effect - hello time period depends on your environment.</span></span> <span data-ttu-id="c963a-207">오랜 시간 동안 hello 상황이 지속 되 면 Microsoft 지원에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-207">If hello situation persists for a long time, contact Microsoft Support.</span></span>

## <a name="collecting-pass-through-authentication-agent-logs"></a><span data-ttu-id="c963a-208">통과 인증 에이전트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="c963a-208">Collecting Pass-through Authentication Agent logs</span></span>

<span data-ttu-id="c963a-209">수 있는의 hello 형식에 따라 통과 인증 에이전트 로그에 대 한 서로 다른 위치에서 toolook이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-209">Depending on hello type of issue you may have, you need toolook in different places for Pass-through Authentication Agent logs.</span></span>

### <a name="authentication-agent-event-logs"></a><span data-ttu-id="c963a-210">인증 에이전트 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="c963a-210">Authentication Agent event logs</span></span>

<span data-ttu-id="c963a-211">오류 관련 toohello 인증 에이전트를 hello hello 서버에서 응용 프로그램 이벤트 뷰어를 열고 확인에서 **응용 프로그램 및 서비스 Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-211">For errors related toohello Authentication Agent, open up hello Event Viewer application on hello server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.</span></span>

<span data-ttu-id="c963a-212">자세한 분석을 위해 hello "세션" 로그를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-212">For detailed analytics, enable hello "Session" log.</span></span> <span data-ttu-id="c963a-213">정상적인 작업 중에 사용할 수는이 로그와 hello 인증 에이전트를 실행 하지 마십시오 문제 해결에 대해서만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-213">Don't run hello Authentication Agent with this log enabled during normal operations; use only for troubleshooting.</span></span> <span data-ttu-id="c963a-214">hello 로그 다시 비활성화 된 후에 hello 로그 내용을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-214">hello log contents are only visible after hello log is disabled again.</span></span>

### <a name="detailed-trace-logs"></a><span data-ttu-id="c963a-215">자세한 추적 로그</span><span class="sxs-lookup"><span data-stu-id="c963a-215">Detailed trace logs</span></span>

<span data-ttu-id="c963a-216">추적 로그에 대 한 tootroubleshoot 사용자 로그인 실패, 확인 **%programdata%\Microsoft\Azure AD 연결 인증 Agent\Trace\\**합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-216">tootroubleshoot user sign-in failures, look for trace logs at **%programdata%\Microsoft\Azure AD Connect Authentication Agent\Trace\\**.</span></span> <span data-ttu-id="c963a-217">이러한 로그는 특정 사용자 로그인에 실패 한 이유 hello 통과 인증 기능을 사용 하 여 하는 이유를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-217">These logs include reasons why a specific user sign-in failed using hello Pass-through Authentication feature.</span></span> <span data-ttu-id="c963a-218">이러한 오류는 또한 hello 앞에 표시 된 매핑된 toohello 로그인 실패 이유 [테이블](#sign-in-failure-reasons-on-the-Azure-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-218">These errors are also mapped toohello sign-in failure reasons shown in hello preceding [table](#sign-in-failure-reasons-on-the-Azure-portal).</span></span> <span data-ttu-id="c963a-219">다음은 로그 항목의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-219">Following is an example log entry:</span></span>

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

<span data-ttu-id="c963a-220">다음 명령을 실행 중인 hello hello 명령 프롬프트를 열어 hello 오류 (이 예에서는 앞에 오는 hello 경우 ' 1328')의 설명이 포함 된 세부 정보를 가져올 수 있습니다 (참고: 대신 '1328' hello 실제 오류 번호에서 로그를 볼 수 있는):</span><span class="sxs-lookup"><span data-stu-id="c963a-220">You can get descriptive details of hello error ('1328' in hello preceding example) by opening up hello command prompt and running hello following command (Note: Replace '1328' with hello actual error number that you see in your logs):</span></span>

`Net helpmsg 1328`

![통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a><span data-ttu-id="c963a-222">도메인 컨트롤러 로그</span><span class="sxs-lookup"><span data-stu-id="c963a-222">Domain Controller logs</span></span>

<span data-ttu-id="c963a-223">감사 로깅이 설정 된 경우 도메인 컨트롤러의 hello 보안 로그에서 추가 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-223">If audit logging is enabled, additional information can be found in hello security logs of your Domain Controllers.</span></span> <span data-ttu-id="c963a-224">간단한 방법을 tooquery 로그인 전송 된 요청을 통과 인증 에이전트에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-224">A simple way tooquery sign-in requests sent by Pass-through Authentication Agents is as follows:</span></span>

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a><span data-ttu-id="c963a-225">성능 모니터 카운터</span><span class="sxs-lookup"><span data-stu-id="c963a-225">Performance Monitor counters</span></span>

<span data-ttu-id="c963a-226">또 다른 방법은 toomonitor 인증 에이전트는 각 서버 hello 인증 에이전트를 설치한 tootrack 특정 성능 모니터 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-226">Another way toomonitor Authentication Agents is tootrack specific Performance Monitor counters on each server where hello Authentication Agent is installed.</span></span> <span data-ttu-id="c963a-227">다음 전역 카운터를 사용 하 여 hello (**# 설명 인증**, **#PTA 실패 한 인증** 및 **#PTA 성공한 인증**) 및 오류 카운터 (**# 설명 인증 오류**):</span><span class="sxs-lookup"><span data-stu-id="c963a-227">Use hello following Global counters (**# PTA authentications**, **#PTA failed authentications** and **#PTA successful authentications**) and Error counters (**# PTA authentication errors**):</span></span>

![통과 인증 성능 모니터 카운터](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
><span data-ttu-id="c963a-229">통과 인증은 여러 인증 에이전트를 사용하여 고가용성을 제공하지만 부하 분산 기능은 제공하지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="c963a-229">Pass-through Authentication provides high availability using multiple Authentication Agents, and _not_ load balancing.</span></span> <span data-ttu-id="c963a-230">구성에 따라 모든 인증 에이전트는 요청과 _동일한_ 수를 수신하지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="c963a-230">Depending on your configuration, _not_ all your Authentication Agents receive roughly _equal_ number of requests.</span></span> <span data-ttu-id="c963a-231">특정 인증 에이전트는 트래픽을 전혀 수신하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c963a-231">It is possible that a specific Authentication Agent receives no traffic at all.</span></span>
