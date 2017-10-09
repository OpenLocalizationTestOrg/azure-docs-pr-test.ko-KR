---
title: "hello Azure Active Directory 포털에서 aaaSign 기능 작업 보고서 오류 코드 | Microsoft Docs"
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
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a><span data-ttu-id="c23e5-103">Hello Azure Active Directory 포털의 로그인 활동 보고서 오류 코드</span><span class="sxs-lookup"><span data-stu-id="c23e5-103">Sign-in activity report error codes in hello Azure Active Directory portal</span></span>

<span data-ttu-id="c23e5-104">Hello 사용자 로그인 보고서에서 제공 하는 hello 정보를 통해 답변 tooquestions와 같은 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-104">With hello information provided by hello user sign-ins report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="c23e5-105">Azure Active Directory를 사용하여 로그인한 사람은?</span><span class="sxs-lookup"><span data-stu-id="c23e5-105">Who has signed-in using Azure Active Directory?</span></span>
- <span data-ttu-id="c23e5-106">서명된 앱은?</span><span class="sxs-lookup"><span data-stu-id="c23e5-106">Which apps were signed into?</span></span>
- <span data-ttu-id="c23e5-107">실패한 로그인은? 그리고 실패한 경우 이유는?</span><span class="sxs-lookup"><span data-stu-id="c23e5-107">Which sign-ins were failures and if so why?</span></span>

<span data-ttu-id="c23e5-108">이 항목 목록 hello 오류 코드 및 관련된 설명을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-108">This topic lists hello error codes and hello related descriptions.</span></span> 

## <a name="how-can-i-display-failed-sign-ins"></a><span data-ttu-id="c23e5-109">실패한 로그인을 표시하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c23e5-109">How can I display failed sign-ins?</span></span> 

<span data-ttu-id="c23e5-110">첫 번째 항목 지점 tooall 로그인 활동 데이터는  **[로그인](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  hello에 **활동** 섹션 **Azure Active**합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-110">Your first entry point tooall sign-in activities data is **[Sign-ins](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)** in hello **Activity** section of **Azure Active**.</span></span>


<span data-ttu-id="c23e5-111">![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/61.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="c23e5-111">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Sign-in activity")</span></span>


<span data-ttu-id="c23e5-112">로그인 보고서에서 **실패**를 **로그인 상태**로 선택하여 실패한 로그인을 모두 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-112">In your sign-ins report, you can display all failed sign-ins by selecting **Failure** as **Sign-in status**.</span></span>


<span data-ttu-id="c23e5-113">![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/06.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="c23e5-113">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Sign-in activity")</span></span>

<span data-ttu-id="c23e5-114">Hello 열립니다 hello 표시 목록에서 항목을 클릭 하면 **활동 세부 정보: 로그인** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-114">Clicking an item in hello displayed list, opens hello **Activity Details: Sign-ins** blade.</span></span> <span data-ttu-id="c23e5-115">이 보기 기능에 대 한 로그인을 hello를 포함 하 여 Azure Active Directory를 추적 하는 모든 hello 정보를 제공 **로그인 오류 코드** 및 **실패 이유**합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-115">This view provides you with all hello details that Azure Active Directory tracks about sign-ins, including hello **sign-in error code** and a **failure reason**.</span></span>

<span data-ttu-id="c23e5-116">![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/05.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="c23e5-116">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Sign-in activity")</span></span>


<span data-ttu-id="c23e5-117">대체 toousing hello Azure 포털 tooaccess hello 로그인 데이터도 사용 하 여 hello [보고 API](active-directory-reporting-api-getting-started-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-117">As an alternative toousing hello Azure portal tooaccess hello sign-ins data, you can also use hello [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).</span></span>


<span data-ttu-id="c23e5-118">hello 다음 섹션에서는 제공 된 모든 가능한 오류와 hello의 전체 목록은 관련 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-118">hello following section provides you with a complete overview of all possible errors and hello related descriptions.</span></span> 

## <a name="error-codes"></a><span data-ttu-id="c23e5-119">오류 코드</span><span class="sxs-lookup"><span data-stu-id="c23e5-119">Error codes</span></span>

| <span data-ttu-id="c23e5-120">오류</span><span class="sxs-lookup"><span data-stu-id="c23e5-120">Error</span></span>| <span data-ttu-id="c23e5-121">설명</span><span class="sxs-lookup"><span data-stu-id="c23e5-121">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c23e5-122">50001</span><span class="sxs-lookup"><span data-stu-id="c23e5-122">50001</span></span>| <span data-ttu-id="c23e5-123">X 라는 hello 서비스 사용자 Y 라는 hello 테 넌 트에 없습니다. 이 hello 테 넌 트의 관리자에 게 여 hello 응용 프로그램을 설치 하지 않은 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-123">hello service principal named X was not found in hello tenant named Y. This can happen if hello application has not been installed by hello administrator of hello tenant.</span></span> <span data-ttu-id="c23e5-124">또는 리소스 사용자 hello 디렉터리에서 찾을 수 없습니다. 또는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-124">Or Resource principal was not found in hello directory or is invalid</span></span>|
| <span data-ttu-id="c23e5-125">50008</span><span class="sxs-lookup"><span data-stu-id="c23e5-125">50008</span></span>| <span data-ttu-id="c23e5-126">SAML 어설션이 없거나 hello 토큰에 잘못 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-126">SAML assertion are missing or misconfigured in hello token.</span></span>|
| <span data-ttu-id="c23e5-127">50011</span><span class="sxs-lookup"><span data-stu-id="c23e5-127">50011</span></span>| <span data-ttu-id="c23e5-128">hello 회신 주소 요소가 잘못 구성 되었거나 hello 응용 프로그램으로 구성 된 회신 주소와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-128">hello reply address is missing, misconfigured or does not match reply addresses configured for hello application.</span></span>|
| <span data-ttu-id="c23e5-129">50053</span><span class="sxs-lookup"><span data-stu-id="c23e5-129">50053</span></span>| <span data-ttu-id="c23e5-130">사용자에 너무 여러 번 잘못 된 사용자 ID 또는 암호와 toosign 려 때문에 계정이 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-130">Account is locked because user tried toosign in too many times with an incorrect user ID or password.</span></span>|
| <span data-ttu-id="c23e5-131">50054</span><span class="sxs-lookup"><span data-stu-id="c23e5-131">50054</span></span>| <span data-ttu-id="c23e5-132">이전 암호가 인증에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-132">Old password is used for authentication.</span></span>|
| <span data-ttu-id="c23e5-133">50055</span><span class="sxs-lookup"><span data-stu-id="c23e5-133">50055</span></span>| <span data-ttu-id="c23e5-134">잘못된 암호입니다. 만료된 암호를 입력했습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-134">Invalid password, entered expired password.</span></span>|
| <span data-ttu-id="c23e5-135">50057</span><span class="sxs-lookup"><span data-stu-id="c23e5-135">50057</span></span>| <span data-ttu-id="c23e5-136">사용자 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-136">User account is disabled.</span></span>|
| <span data-ttu-id="c23e5-137">50058</span><span class="sxs-lookup"><span data-stu-id="c23e5-137">50058</span></span>| <span data-ttu-id="c23e5-138">사용자의 id에 대 한 정보가 없습니다 자격 증명 또는 사용자 테 넌 트에 없습니다 또는 자동 로그인 요청을 보냈습니다 하지만 사용자가 로그인 이나 서비스에서 없습니다 tooauthenticate hello 사용자 제공 중에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-138">No information about user's identity is found among provided credentials or User was not found in tenant or A silent sign-in request was sent but no user is signed in or Service was unable tooauthenticate hello user.</span></span>|
| <span data-ttu-id="c23e5-139">50074</span><span class="sxs-lookup"><span data-stu-id="c23e5-139">50074</span></span>| <span data-ttu-id="c23e5-140">강력한 인증(2단계)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-140">Strong Authentication (second factor) is required</span></span>|
| <span data-ttu-id="c23e5-141">50079</span><span class="sxs-lookup"><span data-stu-id="c23e5-141">50079</span></span>| <span data-ttu-id="c23e5-142">사용자는 두 번째 단계 인증에 대 한 tooenroll 필요</span><span class="sxs-lookup"><span data-stu-id="c23e5-142">User needs tooenroll for second factor authentication</span></span>|
| <span data-ttu-id="c23e5-143">50126</span><span class="sxs-lookup"><span data-stu-id="c23e5-143">50126</span></span>| <span data-ttu-id="c23e5-144">잘못된 사용자 이름 또는 암호이거나 잘못된 온-프레미스 사용자 이름 또는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-144">Invalid username or password or Invalid on-premise username or password.</span></span>|
| <span data-ttu-id="c23e5-145">50131</span><span class="sxs-lookup"><span data-stu-id="c23e5-145">50131</span></span>| <span data-ttu-id="c23e5-146">다양한 조건부 액세스 오류에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-146">Used in various conditional access errors.</span></span> <span data-ttu-id="c23e5-147">예: 잘못 된 Windows 장치 상태 이면 요청이 차단 기한 toosuspicious 활동, 액세스 정책 및 보안 정책을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-147">E.g Bad Windows device state, request blocked due toosuspicious activity, access policy and security policy decisions.</span></span>|
| <span data-ttu-id="c23e5-148">50133</span><span class="sxs-lookup"><span data-stu-id="c23e5-148">50133</span></span>| <span data-ttu-id="c23e5-149">세션 기한 tooexpiration 또는 최근에 암호 변경을 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-149">Session is invalid due tooexpiration or recent password change.</span></span>|
| <span data-ttu-id="c23e5-150">50144</span><span class="sxs-lookup"><span data-stu-id="c23e5-150">50144</span></span>| <span data-ttu-id="c23e5-151">사용자의 Active Directory 암호가 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-151">User's Active Directory password has expired.</span></span>|
| <span data-ttu-id="c23e5-152">65001</span><span class="sxs-lookup"><span data-stu-id="c23e5-152">65001</span></span>| <span data-ttu-id="c23e5-153">응용 프로그램 X 권한 tooaccess 응용 Y 없는 또는 hello 사용 권한 해지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-153">Application X doesn't have permission tooaccess application Y or hello permission has been revoked.</span></span> <span data-ttu-id="c23e5-154">또는 hello 사용자 또는 관리자가 되지 동의 toouse hello 응용 프로그램 ID X. 송신이 사용자 및 리소스에 대 한 대화형 권한 부여 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-154">Or hello user or administrator has not consented toouse hello application with ID X. Send an interactive authorization request for this user and resource.</span></span> <span data-ttu-id="c23e5-155">Hello 사용자 또는 관리자가 toouse hello 응용 프로그램 ID X. 보내기 권한 부여 요청 tooyour 테 넌 트 관리자 tooact hello 응용 프로그램을 대신 하 여 동의 하지 또는: 리소스에 대 한 Y: Z.</span><span class="sxs-lookup"><span data-stu-id="c23e5-155">Or hello user or administrator has not consented toouse hello application with ID X. Send an authorization request tooyour tenant admin tooact on behalf of hello App : Y for Resource : Z.</span></span>|
| <span data-ttu-id="c23e5-156">65005</span><span class="sxs-lookup"><span data-stu-id="c23e5-156">65005</span></span>| <span data-ttu-id="c23e5-157">리소스 액세스 목록 hello 리소스에서 응용 프로그램을 검색할 수를 포함 하지 않거나 hello 클라이언트 응용 프로그램에서 해당 필수 리소스 액세스 목록 또는 잘못 된 반환 된 그래프 서비스에 지정 되지 않은 액세스 tooresource를 요청 하는 hello 응용 프로그램이 필요 요청 또는 리소스를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-157">hello application required resource access list does not contain applications discoverable by hello resource or hello client application has requested access tooresource which was not specified in its required resource access list or Graph service returned bad request or resource not found.</span></span>|
| <span data-ttu-id="c23e5-158">70001</span><span class="sxs-lookup"><span data-stu-id="c23e5-158">70001</span></span>| <span data-ttu-id="c23e5-159">X 라는 hello 응용 프로그램 Y 라는 hello 테 넌 트에 없습니다. 이 수 발생할 hello 응용 프로그램으로 설치 되지 않은 경우 hello hello 테 넌 트 또는 승인된 tooby 관리자 hello 테 넌 트의 모든 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-159">hello application named X was not found in hello tenant named Y. This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.</span></span> <span data-ttu-id="c23e5-160">인증 요청 toohello 잘못 된 테 넌 트를 보냈을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-160">You might have sent your authentication request toohello wrong tenant.</span></span>|
| <span data-ttu-id="c23e5-161">80001</span><span class="sxs-lookup"><span data-stu-id="c23e5-161">80001</span></span>| <span data-ttu-id="c23e5-162">사용할 수 있는 인증 에이전트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-162">No Authentication Agent available.</span></span>|
| <span data-ttu-id="c23e5-163">80002</span><span class="sxs-lookup"><span data-stu-id="c23e5-163">80002</span></span>| <span data-ttu-id="c23e5-164">인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-164">Authentication Agent's password validation request timed out.</span></span>|
| <span data-ttu-id="c23e5-165">80003</span><span class="sxs-lookup"><span data-stu-id="c23e5-165">80003</span></span>| <span data-ttu-id="c23e5-166">인증 에이전트에서 받은 응답이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-166">Invalid response received by Authentication Agent.</span></span>|
| <span data-ttu-id="c23e5-167">80004</span><span class="sxs-lookup"><span data-stu-id="c23e5-167">80004</span></span>| <span data-ttu-id="c23e5-168">로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-168">Incorrect User Principal Name (UPN) used in sign-in request.</span></span>|
| <span data-ttu-id="c23e5-169">80005</span><span class="sxs-lookup"><span data-stu-id="c23e5-169">80005</span></span>| <span data-ttu-id="c23e5-170">인증 에이전트: 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-170">Authentication Agent: Error occurred.</span></span>|
| <span data-ttu-id="c23e5-171">80007</span><span class="sxs-lookup"><span data-stu-id="c23e5-171">80007</span></span>| <span data-ttu-id="c23e5-172">인증 에이전트 수 없습니다 tooconnect tooActive 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-172">Authentication Agent unable tooconnect tooActive Directory.</span></span>|
| <span data-ttu-id="c23e5-173">80010</span><span class="sxs-lookup"><span data-stu-id="c23e5-173">80010</span></span>| <span data-ttu-id="c23e5-174">인증 에이전트 수 없습니다 toodecrypt 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-174">Authentication Agent unable toodecrypt password.</span></span>|
| <span data-ttu-id="c23e5-175">81001</span><span class="sxs-lookup"><span data-stu-id="c23e5-175">81001</span></span>| <span data-ttu-id="c23e5-176">사용자의 Kerberos 티켓이 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-176">User's Kerberos ticket is too large.</span></span>|
| <span data-ttu-id="c23e5-177">81002</span><span class="sxs-lookup"><span data-stu-id="c23e5-177">81002</span></span>| <span data-ttu-id="c23e5-178">없습니다 toovalidate 사용자의 Kerberos 티켓입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-178">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="c23e5-179">81003</span><span class="sxs-lookup"><span data-stu-id="c23e5-179">81003</span></span>| <span data-ttu-id="c23e5-180">없습니다 toovalidate 사용자의 Kerberos 티켓입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-180">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="c23e5-181">81004</span><span class="sxs-lookup"><span data-stu-id="c23e5-181">81004</span></span>| <span data-ttu-id="c23e5-182">Kerberos 인증 시도가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-182">Kerberos authentication attempt failed.</span></span>|
| <span data-ttu-id="c23e5-183">81008</span><span class="sxs-lookup"><span data-stu-id="c23e5-183">81008</span></span>| <span data-ttu-id="c23e5-184">없습니다 toovalidate 사용자의 Kerberos 티켓입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-184">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="c23e5-185">81009</span><span class="sxs-lookup"><span data-stu-id="c23e5-185">81009</span></span>| <span data-ttu-id="c23e5-186">없습니다 toovalidate 사용자의 Kerberos 티켓입니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-186">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="c23e5-187">81010</span><span class="sxs-lookup"><span data-stu-id="c23e5-187">81010</span></span>| <span data-ttu-id="c23e5-188">원활한 SSO 없으므로 hello 사용자의 Kerberos 티켓이 만료 되었거나 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-188">Seamless SSO failed because hello user's Kerberos ticket has expired or is invalid.</span></span>|
| <span data-ttu-id="c23e5-189">81011</span><span class="sxs-lookup"><span data-stu-id="c23e5-189">81011</span></span>| <span data-ttu-id="c23e5-190">없습니다 toofind 사용자 개체 hello 사용자의 Kerberos 티켓에 대 한 정보를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-190">Unable toofind user object based on information in hello user's Kerberos ticket.</span></span>|
| <span data-ttu-id="c23e5-191">81012</span><span class="sxs-lookup"><span data-stu-id="c23e5-191">81012</span></span>| <span data-ttu-id="c23e5-192">tooAzure AD에서에서 toosign hello 사용자는 hello 장치에 로그인 하는 hello 사용자와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-192">hello user trying toosign in tooAzure AD is different from hello user signed into hello device.</span></span>|
| <span data-ttu-id="c23e5-193">81013</span><span class="sxs-lookup"><span data-stu-id="c23e5-193">81013</span></span>| <span data-ttu-id="c23e5-194">없습니다 toofind 사용자 개체 hello 사용자의 Kerberos 티켓에 대 한 정보를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-194">Unable toofind user object based on information in hello user's Kerberos ticket.</span></span>|
| <span data-ttu-id="c23e5-195">90014</span><span class="sxs-lookup"><span data-stu-id="c23e5-195">90014</span></span>| <span data-ttu-id="c23e5-196">예상된 된 필드는 hello 자격 증명에 없을 경우 다양 한 경우에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-196">Used in various cases when an expected field is not present in hello credential.</span></span>|
| <span data-ttu-id="c23e5-197">90093</span><span class="sxs-lookup"><span data-stu-id="c23e5-197">90093</span></span>| <span data-ttu-id="c23e5-198">그래프는 hello 요청에 대 한 금지 된 오류 코드와 함께 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-198">Graph returned with forbidden error code for hello request.</span></span>|



## <a name="next-steps"></a><span data-ttu-id="c23e5-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c23e5-199">Next steps</span></span>

<span data-ttu-id="c23e5-200">자세한 내용은 참조 hello [hello Azure Active Directory 포털의 로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c23e5-200">For more details, see hello [Sign-in activity reports in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins.md).</span></span>

