---
title: "Azure Active Directory 포털의 로그인 활동 보고서 오류 코드 | Microsoft Docs"
description: "로그인 활동 보고서 오류 코드에 대한 참조입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 2a1b7b87df2cd8fa2e98f217480b46f5f6334297
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="sign-in-activity-report-error-codes-in-the-azure-active-directory-portal"></a><span data-ttu-id="3781f-103">Azure Active Directory 포털의 로그인 활동 보고서 오류 코드</span><span class="sxs-lookup"><span data-stu-id="3781f-103">Sign-in activity report error codes in the Azure Active Directory portal</span></span>

<span data-ttu-id="3781f-104">사용자 로그인 보고서에서 제공되는 정보를 사용하면 다음과 같은 질문에 대한 대답을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-104">With the information provided by the user sign-ins report, you find answers to questions such as:</span></span>

- <span data-ttu-id="3781f-105">Azure Active Directory를 사용하여 로그인한 사람은?</span><span class="sxs-lookup"><span data-stu-id="3781f-105">Who has signed-in using Azure Active Directory?</span></span>
- <span data-ttu-id="3781f-106">서명된 앱은?</span><span class="sxs-lookup"><span data-stu-id="3781f-106">Which apps were signed into?</span></span>
- <span data-ttu-id="3781f-107">실패한 로그인은? 그리고 실패한 경우 이유는?</span><span class="sxs-lookup"><span data-stu-id="3781f-107">Which sign-ins were failures and if so why?</span></span>

<span data-ttu-id="3781f-108">이 항목에서는 오류 코드와 관련 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-108">This topic lists the error codes and the related descriptions.</span></span> 

## <a name="how-can-i-display-failed-sign-ins"></a><span data-ttu-id="3781f-109">실패한 로그인을 표시하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="3781f-109">How can I display failed sign-ins?</span></span> 

<span data-ttu-id="3781f-110">모든 로그인 활동 데이터에 대한 첫 번째 진입점은 **Azure Active**의 **활동** 섹션에 있는 **[로그인](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**입니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-110">Your first entry point to all sign-in activities data is **[Sign-ins](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)** in the **Activity** section of **Azure Active**.</span></span>


<span data-ttu-id="3781f-111">![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/61.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="3781f-111">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Sign-in activity")</span></span>


<span data-ttu-id="3781f-112">로그인 보고서에서 **실패**를 **로그인 상태**로 선택하여 실패한 로그인을 모두 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-112">In your sign-ins report, you can display all failed sign-ins by selecting **Failure** as **Sign-in status**.</span></span>


<span data-ttu-id="3781f-113">![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/06.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="3781f-113">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Sign-in activity")</span></span>

<span data-ttu-id="3781f-114">표시된 목록에서 항목을 클릭하면 **활동 세부 정보: 로그인**  블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-114">Clicking an item in the displayed list, opens the **Activity Details: Sign-ins** blade.</span></span> <span data-ttu-id="3781f-115">이 보기에서는 **로그인 오류 코드** 및 **실패 이유**를 포함하여 Azure Active Directory에서 로그인에 대해 추적하는 모든 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-115">This view provides you with all the details that Azure Active Directory tracks about sign-ins, including the **sign-in error code** and a **failure reason**.</span></span>

<span data-ttu-id="3781f-116">![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/05.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="3781f-116">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Sign-in activity")</span></span>


<span data-ttu-id="3781f-117">Azure Portal을 사용하여 로그인 데이터에 액세스하는 대신 [보고 API](active-directory-reporting-api-getting-started-azure-portal.md)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-117">As an alternative to using the Azure portal to access the sign-ins data, you can also use the [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).</span></span>


<span data-ttu-id="3781f-118">다음 섹션에서는 가능한 모든 오류 및 관련 설명에 대한 전체 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-118">The following section provides you with a complete overview of all possible errors and the related descriptions.</span></span> 

## <a name="error-codes"></a><span data-ttu-id="3781f-119">오류 코드</span><span class="sxs-lookup"><span data-stu-id="3781f-119">Error codes</span></span>

| <span data-ttu-id="3781f-120">오류</span><span class="sxs-lookup"><span data-stu-id="3781f-120">Error</span></span>| <span data-ttu-id="3781f-121">설명</span><span class="sxs-lookup"><span data-stu-id="3781f-121">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3781f-122">50001</span><span class="sxs-lookup"><span data-stu-id="3781f-122">50001</span></span>| <span data-ttu-id="3781f-123">X라는 서비스 주체가 Y라는 테넌트에 없습니다. 테넌트의 관리자가 응용 프로그램을 설치하지 않은 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-123">The service principal named X was not found in the tenant named Y. This can happen if the application has not been installed by the administrator of the tenant.</span></span> <span data-ttu-id="3781f-124">또는 리소스 보안 주체가 디렉터리에 없거나 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-124">Or Resource principal was not found in the directory or is invalid</span></span>|
| <span data-ttu-id="3781f-125">50008</span><span class="sxs-lookup"><span data-stu-id="3781f-125">50008</span></span>| <span data-ttu-id="3781f-126">토큰에서 SAML 어설션이 누락되었거나 잘못 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-126">SAML assertion are missing or misconfigured in the token.</span></span>|
| <span data-ttu-id="3781f-127">50011</span><span class="sxs-lookup"><span data-stu-id="3781f-127">50011</span></span>| <span data-ttu-id="3781f-128">회신 주소가 누락되었거나 잘못 구성되었거나 응용 프로그램에 대해 구성된 회신 주소와 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-128">The reply address is missing, misconfigured or does not match reply addresses configured for the application.</span></span>|
| <span data-ttu-id="3781f-129">50053</span><span class="sxs-lookup"><span data-stu-id="3781f-129">50053</span></span>| <span data-ttu-id="3781f-130">잘못된 사용자 ID 또는 암호로 로그인을 너무 많이 시도하여 계정이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-130">Account is locked because user tried to sign in too many times with an incorrect user ID or password.</span></span>|
| <span data-ttu-id="3781f-131">50054</span><span class="sxs-lookup"><span data-stu-id="3781f-131">50054</span></span>| <span data-ttu-id="3781f-132">이전 암호가 인증에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-132">Old password is used for authentication.</span></span>|
| <span data-ttu-id="3781f-133">50055</span><span class="sxs-lookup"><span data-stu-id="3781f-133">50055</span></span>| <span data-ttu-id="3781f-134">잘못된 암호입니다. 만료된 암호를 입력했습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-134">Invalid password, entered expired password.</span></span>|
| <span data-ttu-id="3781f-135">50057</span><span class="sxs-lookup"><span data-stu-id="3781f-135">50057</span></span>| <span data-ttu-id="3781f-136">사용자 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-136">User account is disabled.</span></span>|
| <span data-ttu-id="3781f-137">50058</span><span class="sxs-lookup"><span data-stu-id="3781f-137">50058</span></span>| <span data-ttu-id="3781f-138">제공된 자격 증명에서 사용자의 ID에 대한 정보가 없거나, 테넌트에서 사용자를 찾을 수 없거나, 자동 로그인 요청을 보냈지만 사용자가 로그인되지 않았거나 서비스에서 사용자를 인증하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-138">No information about user's identity is found among provided credentials or User was not found in tenant or A silent sign-in request was sent but no user is signed in or Service was unable to authenticate the user.</span></span>|
| <span data-ttu-id="3781f-139">50074</span><span class="sxs-lookup"><span data-stu-id="3781f-139">50074</span></span>| <span data-ttu-id="3781f-140">강력한 인증(2단계)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-140">Strong Authentication (second factor) is required</span></span>|
| <span data-ttu-id="3781f-141">50079</span><span class="sxs-lookup"><span data-stu-id="3781f-141">50079</span></span>| <span data-ttu-id="3781f-142">사용자는 2단계 인증에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-142">User needs to enroll for second factor authentication</span></span>|
| <span data-ttu-id="3781f-143">50126</span><span class="sxs-lookup"><span data-stu-id="3781f-143">50126</span></span>| <span data-ttu-id="3781f-144">잘못된 사용자 이름 또는 암호이거나 잘못된 온-프레미스 사용자 이름 또는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-144">Invalid username or password or Invalid on-premise username or password.</span></span>|
| <span data-ttu-id="3781f-145">50131</span><span class="sxs-lookup"><span data-stu-id="3781f-145">50131</span></span>| <span data-ttu-id="3781f-146">다양한 조건부 액세스 오류에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-146">Used in various conditional access errors.</span></span> <span data-ttu-id="3781f-147">예: Windows 장치 상태가 잘못되었습니다. 의심스러운 활동, 액세스 정책 및 보안 정책 결정으로 인해 요청이 차단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-147">E.g Bad Windows device state, request blocked due to suspicious activity, access policy and security policy decisions.</span></span>|
| <span data-ttu-id="3781f-148">50133</span><span class="sxs-lookup"><span data-stu-id="3781f-148">50133</span></span>| <span data-ttu-id="3781f-149">만료 또는 최근 암호 변경으로 인해 세션이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-149">Session is invalid due to expiration or recent password change.</span></span>|
| <span data-ttu-id="3781f-150">50144</span><span class="sxs-lookup"><span data-stu-id="3781f-150">50144</span></span>| <span data-ttu-id="3781f-151">사용자의 Active Directory 암호가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-151">User's Active Directory password has expired.</span></span>|
| <span data-ttu-id="3781f-152">65001</span><span class="sxs-lookup"><span data-stu-id="3781f-152">65001</span></span>| <span data-ttu-id="3781f-153">Y 응용 프로그램에 대한 액세스 권한이 X 응용 프로그램에 없거나 권한이 취소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-153">Application X doesn't have permission to access application Y or the permission has been revoked.</span></span> <span data-ttu-id="3781f-154">또는 사용자 또는 관리자가 X ID로 응용 프로그램을 사용하는 데 동의하지 않았습니다. 이 사용자 및 리소스에 대한 대화형 권한 부여 요청을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="3781f-154">Or The user or administrator has not consented to use the application with ID X. Send an interactive authorization request for this user and resource.</span></span> <span data-ttu-id="3781f-155">또는 사용자 또는 관리자가 X ID로 응용 프로그램을 사용하는 데 동의하지 않았습니다. Z 리소스에 대한 Y 앱을 대신하여 테넌트 관리자에게 권한 부여 요청을 보내세요.</span><span class="sxs-lookup"><span data-stu-id="3781f-155">Or The user or administrator has not consented to use the application with ID X. Send an authorization request to your tenant admin to act on behalf of the App : Y for Resource : Z.</span></span>|
| <span data-ttu-id="3781f-156">65005</span><span class="sxs-lookup"><span data-stu-id="3781f-156">65005</span></span>| <span data-ttu-id="3781f-157">응용 프로그램 필수 리소스 액세스 목록에 리소스에서 검색 가능한 응용 프로그램이 없거나, 클라이언트 응용 프로그램에서 필수 리소스 액세스 목록에 지정되지 않은 리소스에 대한 액세스를 요청했거나, Graph 서비스에서 잘못된 요청 또는 찾을 수 없는 리소스를 반환했습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-157">The application required resource access list does not contain applications discoverable by the resource or The client application has requested access to resource which was not specified in its required resource access list or Graph service returned bad request or resource not found.</span></span>|
| <span data-ttu-id="3781f-158">70001</span><span class="sxs-lookup"><span data-stu-id="3781f-158">70001</span></span>| <span data-ttu-id="3781f-159">X라는 응용 프로그램이 Y라는 테넌트에 없습니다. 테넌트의 관리자가 응용 프로그램을 설치하지 않았거나 테넌트의 사용자가 동의하지 않은 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-159">The application named X was not found in the tenant named Y. This can happen if the application has not been installed by the administrator of the tenant or consented to by any user in the tenant.</span></span> <span data-ttu-id="3781f-160">잘못된 테넌트에 인증 요청을 보냈을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-160">You might have sent your authentication request to the wrong tenant.</span></span>|
| <span data-ttu-id="3781f-161">80001</span><span class="sxs-lookup"><span data-stu-id="3781f-161">80001</span></span>| <span data-ttu-id="3781f-162">사용할 수 있는 인증 에이전트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-162">No Authentication Agent available.</span></span>|
| <span data-ttu-id="3781f-163">80002</span><span class="sxs-lookup"><span data-stu-id="3781f-163">80002</span></span>| <span data-ttu-id="3781f-164">인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-164">Authentication Agent's password validation request timed out.</span></span>|
| <span data-ttu-id="3781f-165">80003</span><span class="sxs-lookup"><span data-stu-id="3781f-165">80003</span></span>| <span data-ttu-id="3781f-166">인증 에이전트에서 받은 응답이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-166">Invalid response received by Authentication Agent.</span></span>|
| <span data-ttu-id="3781f-167">80004</span><span class="sxs-lookup"><span data-stu-id="3781f-167">80004</span></span>| <span data-ttu-id="3781f-168">로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-168">Incorrect User Principal Name (UPN) used in sign-in request.</span></span>|
| <span data-ttu-id="3781f-169">80005</span><span class="sxs-lookup"><span data-stu-id="3781f-169">80005</span></span>| <span data-ttu-id="3781f-170">인증 에이전트: 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-170">Authentication Agent: Error occurred.</span></span>|
| <span data-ttu-id="3781f-171">80007</span><span class="sxs-lookup"><span data-stu-id="3781f-171">80007</span></span>| <span data-ttu-id="3781f-172">인증 에이전트에서 Active Directory에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-172">Authentication Agent unable to connect to Active Directory.</span></span>|
| <span data-ttu-id="3781f-173">80010</span><span class="sxs-lookup"><span data-stu-id="3781f-173">80010</span></span>| <span data-ttu-id="3781f-174">인증 에이전트에서 암호를 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-174">Authentication Agent unable to decrypt password.</span></span>|
| <span data-ttu-id="3781f-175">81001</span><span class="sxs-lookup"><span data-stu-id="3781f-175">81001</span></span>| <span data-ttu-id="3781f-176">사용자의 Kerberos 티켓이 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-176">User's Kerberos ticket is too large.</span></span>|
| <span data-ttu-id="3781f-177">81002</span><span class="sxs-lookup"><span data-stu-id="3781f-177">81002</span></span>| <span data-ttu-id="3781f-178">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-178">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="3781f-179">81003</span><span class="sxs-lookup"><span data-stu-id="3781f-179">81003</span></span>| <span data-ttu-id="3781f-180">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-180">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="3781f-181">81004</span><span class="sxs-lookup"><span data-stu-id="3781f-181">81004</span></span>| <span data-ttu-id="3781f-182">Kerberos 인증 시도가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-182">Kerberos authentication attempt failed.</span></span>|
| <span data-ttu-id="3781f-183">81008</span><span class="sxs-lookup"><span data-stu-id="3781f-183">81008</span></span>| <span data-ttu-id="3781f-184">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-184">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="3781f-185">81009</span><span class="sxs-lookup"><span data-stu-id="3781f-185">81009</span></span>| <span data-ttu-id="3781f-186">사용자의 Kerberos 티켓에 대한 유효성을 검사할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-186">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="3781f-187">81010</span><span class="sxs-lookup"><span data-stu-id="3781f-187">81010</span></span>| <span data-ttu-id="3781f-188">사용자의 Kerberos 티켓이 만료되었거나 잘못되었으므로 Seamless SSO가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-188">Seamless SSO failed because the user's Kerberos ticket has expired or is invalid.</span></span>|
| <span data-ttu-id="3781f-189">81011</span><span class="sxs-lookup"><span data-stu-id="3781f-189">81011</span></span>| <span data-ttu-id="3781f-190">사용자의 Kerberos 티켓 정보에 기반하여 사용자 개체를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-190">Unable to find user object based on information in the user's Kerberos ticket.</span></span>|
| <span data-ttu-id="3781f-191">81012</span><span class="sxs-lookup"><span data-stu-id="3781f-191">81012</span></span>| <span data-ttu-id="3781f-192">Azure AD에 로그인하려는 사용자가 장치에 로그인한 사용자와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-192">The user trying to sign in to Azure AD is different from the user signed into the device.</span></span>|
| <span data-ttu-id="3781f-193">81013</span><span class="sxs-lookup"><span data-stu-id="3781f-193">81013</span></span>| <span data-ttu-id="3781f-194">사용자의 Kerberos 티켓 정보에 기반하여 사용자 개체를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-194">Unable to find user object based on information in the user's Kerberos ticket.</span></span>|
| <span data-ttu-id="3781f-195">90014</span><span class="sxs-lookup"><span data-stu-id="3781f-195">90014</span></span>| <span data-ttu-id="3781f-196">예상된 필드가 자격 증명에 없는 다양한 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-196">Used in various cases when an expected field is not present in the credential.</span></span>|
| <span data-ttu-id="3781f-197">90093</span><span class="sxs-lookup"><span data-stu-id="3781f-197">90093</span></span>| <span data-ttu-id="3781f-198">요청에 대해 사용할 수 없는 오류 코드와 함께 반환된 그래프입니다.</span><span class="sxs-lookup"><span data-stu-id="3781f-198">Graph returned with forbidden error code for the request.</span></span>|



## <a name="next-steps"></a><span data-ttu-id="3781f-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3781f-199">Next steps</span></span>

<span data-ttu-id="3781f-200">자세한 내용은 [Azure Active Directory 포털의 로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3781f-200">For more details, see the [Sign-in activity reports in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins.md).</span></span>

