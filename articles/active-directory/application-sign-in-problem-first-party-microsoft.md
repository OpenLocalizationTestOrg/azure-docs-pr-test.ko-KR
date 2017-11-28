---
title: "aaaProblems tooa Microsoft 응용 프로그램에에서 서명 | Microsoft Docs"
description: "Toofirst 파티 Microsoft Azure AD (예: Office 365)를 사용 하 여 응용 프로그램에 로그인 할 때 직면 하는 일반적인 문제 해결"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="603ff-103">Tooa Microsoft 응용 프로그램에에서 로그인 하는 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="603ff-104">타사 SaaS 응용 프로그램 또는 Single Sign-On을 위해 Azure AD와 통합하는 다른 응용 프로그램과는 약간 다른 방법으로 Microsoft 응용 프로그램(예: Office 365 Exchange, SharePoint, Yammer 등)을 할당하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="603ff-105">사용자 액세스 tooa Microsoft 게시 된 응용 프로그램을 얻을 수 있는 세 가지 주요 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="603ff-106">Hello Office 365 또는 다른 유료 도구 모음에서 응용 프로그램에 대 한 사용자 액세스를 통해 부여 됩니다 **라이선스 할당** 하거나 직접 tootheir 사용자 계정 또는 그룹 기반의 라이선스 할당 기능을 사용 하 여 그룹을 통해.</span><span class="sxs-lookup"><span data-stu-id="603ff-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="603ff-107">Microsoft 소프트웨어 또는 세 번째 파티 게시 자유롭게 누구나 toouse 응용 프로그램에 대 한 사용자가 부여할 수 있습니다를 통한 액세스 **사용자 동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="603ff-108">This0 있음을 나타내는 Azure AD의 직장 또는 학교 계정으로 toohello 응용 프로그램에 로그인 계정에 데이터 집합이 액세스 제한 toosome toohave 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="603ff-109">Microsoft 소프트웨어 또는 3rd 파티 게시 자유롭게 누구나 toouse 응용 프로그램에 대 한 사용자 수 또한 권한을 부여 통해 **관리자의 동의가**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="603ff-110">즉, 전역 관리자 계정 가진 toohello 응용 프로그램에 로그인 하 고 액세스 tooeveryone hello 조직에서 부여 있도록 hello 조직의 모든 사용자가 hello 응용 프로그램을 사용할 수 있습니다는 관리자가 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="603ff-111">tootroubleshoot hello로 시작 문제를 [응용 프로그램 액세스 tooconsider로 일반적인 문제 영역](#general-problem-areas-with-application-access-to-consider) hello 읽습니다 [연습: Microsoft 응용 프로그램 액세스 단계 tootroubleshoot](#walkthrough-steps-to-troubleshoot-microsoft-application-access) hello 세부 정보로 tooget 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="603ff-112">응용 프로그램 액세스 tooconsider로 일반적인 문제 영역</span><span class="sxs-lookup"><span data-stu-id="603ff-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="603ff-113">다음 목록은 hello toostart, 하지만 권장할 신속 하 게 진행 하는 hello 연습 tooget 읽기의 방법이 있는 경우 드릴 수 있는 일반적인 문제 영역: [연습: Microsoft 응용 프로그램 액세스단계tootroubleshoot](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="603ff-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="603ff-114">Hello 사용자 계정과 관련 된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="603ff-115">그룹과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="603ff-116">조건부 액세스 정책과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="603ff-117">응용 프로그램 동의와 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="603ff-118">단계 tootroubleshoot Microsoft 응용 프로그램 액세스</span><span class="sxs-lookup"><span data-stu-id="603ff-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="603ff-119">아래 몇 가지 일반적인 문제 동료 들을 때 실행가 사용자에 게 tooa Microsoft 응용 프로그램에 로그인 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="603ff-120">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-120">General issues toocheck first</span></span>

  * <span data-ttu-id="603ff-121">Hello 사용자가 로그인 하 여 toohello에 있는지 확인 **올바른 URL** 및 로컬 응용 프로그램 URL이 아니기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="603ff-122">Hello 사용자의 계정이 인지 확인 **잠겨 있지 않으면입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="603ff-123">있는지 hello 확인 **사용자의 계정이 존재** Azure Active Directory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="603ff-124">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="603ff-125">Hello 사용자의 계정이 인지 확인 **활성화** 에 로그인 합니다. [사용자의 계정 상태 확인](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="603ff-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="603ff-126">있는지 hello 사용자 확인 **암호를 만료 하거나 잊어버린 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="603ff-127">[사용자의 암호 재설정](#reset-a-users-password) 또는 [셀프 서비스 암호 재설정 사용](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="603ff-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="603ff-128">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="603ff-129">[사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status) 또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="603ff-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="603ff-130">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="603ff-131">[특정 조건부 액세스 정책 확인](#problems-with-conditional-access-policies) 또는 [특정 응용 프로그램의 조건부 액세스 정책 확인](#check-a-specific-applications-conditional-access-policy) 또는 [특정 조건부 액세스 정책 사용 안 함](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="603ff-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="603ff-132">다음 사항을 확인 한 사용자의 **인증 연락처 정보** toodate tooallow Multi-factor Authentication 또는 조건부 액세스 정책 toobe 적용 중일 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="603ff-133">[사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status) 또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="603ff-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="603ff-134">에 대 한 **Microsoft** **라이선스를 필요로 하는 응용 프로그램** (예: office 365), 다음은 몇 가지 특정 문제 toocheck 위의 일반적인 문제 hello 아닌 경우:</span><span class="sxs-lookup"><span data-stu-id="603ff-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="603ff-135">Hello 사용자 확인 되었거나는 **라이선스가 할당 합니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="603ff-136">[사용자의 할당된 라이선스 확인](#check-a-users-assigned-licenses) 또는 [그룹의 할당된 라이선스 확인](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="603ff-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="603ff-137">Hello 라이선스가 **tooa 할당** **정적 그룹**, 해당 hello 확인 **사용자가 멤버인** 해당 그룹의 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="603ff-138">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="603ff-139">Hello 라이선스가 **tooa 할당** **동적 그룹**, 해당 hello 확인 **동적 그룹 규칙을 올바르게 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="603ff-140">동적 그룹의 구성원 자격 조건 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="603ff-141">Hello 라이선스가 **tooa 할당** **동적 그룹**, 해당 hello 동적 그룹에 있는지 확인 **처리가 완료** 구성원 자격 및 해당 hello **사용자가을 멤버** (다소 시간이 걸릴 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="603ff-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="603ff-142">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="603ff-143">Hello 라이선스가 할당 되었는지 확인 하면 hello 라이선스가 있는지 확인 **만료 되지**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="603ff-144">Hello 라이선스가 있는지 확인 **hello 응용 프로그램에 대 한** 에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="603ff-145">에 대 한 **Microsoft** **라이선스를 필요로 하지 않는 응용 프로그램**, 일부 다른 작업 toocheck 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="603ff-146">Hello 응용 프로그램을 요청 하는 경우 **사용자 수준 권한** 해당 hello 사용자가 toohello 응용 프로그램에 로그인 하 고가 수행 되었는지 확인 (예를 들어 "이이 사용자의이 사서함")에 액세스 한 **사용자 동의 작업**  toolet hello 응용 프로그램의 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="603ff-147">Hello 응용 프로그램을 요청 하는 경우 **관리자 수준 사용 권한이** 전역 관리자가 수행 했는지 있는지 확인 (예를 들어 "모든 사용자의 사서함")에 액세스 한 **에서 관리자 권한으로 승인 작업 모든 사용자를 대신 하 여** hello 조직에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="603ff-148">Hello 사용자 계정과 관련 된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-148">Problems with hello user’s account</span></span>

<span data-ttu-id="603ff-149">기한 tooa 문제 toohello 응용 프로그램에 할당 된 사용자와 응용 프로그램 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="603ff-150">다음 몇 가지 방법으로 사용자 및 해당 계정 설정과 관련된 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="603ff-151">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="603ff-152">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="603ff-153">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="603ff-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="603ff-154">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="603ff-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="603ff-155">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="603ff-156">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="603ff-157">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="603ff-158">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="603ff-159">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="603ff-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="603ff-160">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="603ff-161">아래의 hello 단계를 수행 하는 사용자의 계정이 표시 되 면 toocheck:</span><span class="sxs-lookup"><span data-stu-id="603ff-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-162">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-163">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-164">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-165">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-166">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-166">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-167">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-168">Hello 속성의 hello 사용자 개체 toobe 고 없는 데이터가 누락 된 표시 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="603ff-169">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-169">Check a user’s account status</span></span>

<span data-ttu-id="603ff-170">toocheck 사용자의 계정 상태, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-171">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-172">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-173">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-174">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-175">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-175">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-176">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-177">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-177">click **Profile**.</span></span>

8.  <span data-ttu-id="603ff-178">**설정** 되도록 **블록 로그인** 너무 설정 되어**아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="603ff-179">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="603ff-179">Reset a user’s password</span></span>

<span data-ttu-id="603ff-180">tooreset 사용자의 암호를 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="603ff-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-181">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-182">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-183">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-184">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-185">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-185">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-186">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-187">hello 클릭 **암호 재설정** hello hello 사용자 블레이드 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="603ff-188">hello 클릭 **암호 재설정** hello에서 단추 **암호 재설정** 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="603ff-189">복사 hello **임시 암호** 또는 **새 암호를 입력** hello 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="603ff-190">이 새 암호 toohello 사용자 통신, 필요한 toochange tooAzure Active Directory에에서 로그인 하는 동안 다음 번이이 암호를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="603ff-191">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="603ff-191">Enable self-service password reset</span></span>

<span data-ttu-id="603ff-192">tooenable 셀프 서비스 암호 재설정에 아래의 hello 배포 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="603ff-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="603ff-193">Azure Active Directory 암호 tooreset 사용자가 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="603ff-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="603ff-194">사용자가 tooreset를 사용 하거나 Active Directory 온-프레미스 암호 변경</span><span class="sxs-lookup"><span data-stu-id="603ff-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="603ff-195">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="603ff-196">toocheck 사용자의 다단계 인증 상태, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="603ff-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-197">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-198">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-199">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-200">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-201">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-201">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-202">hello 클릭 **Multi-factor Authentication** hello hello 블레이드 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="603ff-203">한 번 hello **Multi-factor Authentication 관리 포털** 부하를 hello에 있는 확인 하십시오 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="603ff-204">검색, 필터링 또는 정렬 하 여 hello 사용자 목록에서 hello 사용자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="603ff-205">사용자의 hello 목록에서 선택 hello 사용자 및 **사용**, **사용 하지 않도록 설정**, 또는 **적용** 원하는 대로 다단계 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="603ff-206">**참고**: 사용자가 있는 경우에 **Enforced** 상태 이면 너무 설정할 수 있습니다**비활성화 된** 일시적으로 toolet 다시 자신의 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="603ff-207">인 다시 변경할 수 있습니다 다음 상태로 너무**Enabled** toorequire 다시 해당 toore 레지스터 그들의 연락처 정보 중 다음 번에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="603ff-208">Hello의 hello 단계를 수행 수 또는 [사용자의 인증 연락처 정보를 확인](#check-a-users-authentication-contact-info) tooverify 하거나 하에이 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="603ff-209">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="603ff-210">아래의 hello 단계를 수행 하는 사용자의 인증 연락처 정보 multi-factor authentication, 조건부 액세스, Id 보호 및 암호 재설정에 사용 되는 toocheck:</span><span class="sxs-lookup"><span data-stu-id="603ff-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-211">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-212">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-213">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-214">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-215">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-215">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-216">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-217">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-217">click **Profile**.</span></span>

8.  <span data-ttu-id="603ff-218">너무 아래로 스크롤하여**인증 연락처 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="603ff-219">**검토** 필요에 따라 hello 데이터 hello 사용자 및 업데이트에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="603ff-220">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-220">Check a user’s group memberships</span></span>

<span data-ttu-id="603ff-221">toocheck 사용자의 그룹 구성원 자격, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-222">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-223">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-224">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-225">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-226">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-226">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-227">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-228">클릭 **그룹** toosee hello 사용자 그룹의 멤버인 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="603ff-229">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="603ff-230">toocheck 사용자의 라이선스를 다음 단계에 따라 hello 할당:</span><span class="sxs-lookup"><span data-stu-id="603ff-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-231">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-232">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-233">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-234">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-235">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-235">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-236">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-237">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="603ff-238">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="603ff-238">Assign a user a license</span></span> 

<span data-ttu-id="603ff-239">아래의 hello 단계를 수행 하는 라이선스 tooa 사용자 tooassign:</span><span class="sxs-lookup"><span data-stu-id="603ff-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-240">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-241">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-242">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-243">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-244">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-244">click **All users**.</span></span>

6.  <span data-ttu-id="603ff-245">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-246">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="603ff-247">Hello 클릭 **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="603ff-248">선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="603ff-249">**선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="603ff-250">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="603ff-251">Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 사용자 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="603ff-252">그룹과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-252">Problems with groups</span></span>

<span data-ttu-id="603ff-253">Tooa 문제 toohello 응용 프로그램에 할당 된 그룹으로 인해 응용 프로그램 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="603ff-254">다음 몇 가지 방법으로 그룹 및 구성원 자격과 관련된 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="603ff-255">그룹의 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="603ff-256">동적 그룹의 구성원 자격 조건 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="603ff-257">그룹의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="603ff-258">그룹의 라이선스 다시 처리</span><span class="sxs-lookup"><span data-stu-id="603ff-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="603ff-259">그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="603ff-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="603ff-260">그룹의 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-260">Check a group’s membership</span></span>

<span data-ttu-id="603ff-261">toocheck 그룹의 구성원, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="603ff-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-262">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-263">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-264">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-265">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-266">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-266">click **All groups**.</span></span>

6.  <span data-ttu-id="603ff-267">**검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-268">클릭 **멤버** 사용자 tooreview hello 목록 toothis 그룹을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="603ff-269">동적 그룹의 구성원 자격 조건 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="603ff-270">toocheck 아래의 hello 단계를 수행 하는 동적 그룹 멤버 자격 기준:</span><span class="sxs-lookup"><span data-stu-id="603ff-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-271">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-272">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-273">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-274">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-275">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-275">click **All groups**.</span></span>

6.  <span data-ttu-id="603ff-276">**검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-277">**동적 구성원 자격 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="603ff-278">검토 hello **간단한** 또는 **고급** 이 그룹에 대해 정의 된 규칙 및 해당 toobe이이 그룹의 구성원 hello 사용자를 이러한 조건을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="603ff-279">그룹의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="603ff-280">toocheck 그룹의 할당 된 라이선스를 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="603ff-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-281">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-282">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-283">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-284">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-285">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-285">click **All groups**.</span></span>

6.  <span data-ttu-id="603ff-286">**검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-287">클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="603ff-288">그룹의 라이선스 다시 처리</span><span class="sxs-lookup"><span data-stu-id="603ff-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="603ff-289">tooreprocess 그룹의 할당 된 라이선스를 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="603ff-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-290">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-291">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-292">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-293">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-294">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-294">click **All groups**.</span></span>

6.  <span data-ttu-id="603ff-295">**검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-296">클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="603ff-297">hello 클릭 **다시 처리** 라이선스가 할당 toothis 그룹의 구성원 hello 단추 tooensure 최신 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="603ff-298">Hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="603ff-299">toodo이 더 빨리 고려 임시로 라이선스 toohello 사용자를 직접 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="603ff-300">[사용자에게 라이선스를 할당합니다](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="603ff-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="603ff-301">그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="603ff-301">Assign a group a license</span></span>

<span data-ttu-id="603ff-302">아래의 hello 단계를 수행 하는 라이선스 tooa 그룹을 tooassign:</span><span class="sxs-lookup"><span data-stu-id="603ff-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="603ff-303">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-304">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-305">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-306">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-307">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-307">click **All groups**.</span></span>

6.  <span data-ttu-id="603ff-308">**검색** 에 관심이 있는 hello 그룹에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="603ff-309">클릭 **라이선스** toosee 현재 hello 라이선스 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="603ff-310">Hello 클릭 **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="603ff-311">선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="603ff-312">**선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="603ff-313">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="603ff-314">Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 그룹 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="603ff-315">Hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="603ff-316">toodo이 더 빨리 고려 임시로 라이선스 toohello 사용자를 직접 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="603ff-317">[사용자에게 라이선스를 할당합니다](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="603ff-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="603ff-318">조건부 액세스 정책과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="603ff-319">특정 조건부 액세스 정책 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="603ff-320">toocheck 또는 단일 조건부 액세스 정책의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="603ff-321">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-322">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-323">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-324">클릭 **엔터프라이즈 응용 프로그램** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-325">hello 클릭 **조건부 액세스** 탐색 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="603ff-326">검사 하려는 hello 정책을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="603ff-327">특정 조건, 할당 또는 사용자 액세스를 차단할 수 있는 기타 설정이 없는지 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="603ff-328">이 정책 tooensure 것 적용 되지 않는 기호 안함 toodo이, 집합 hello tootemporarily 비활성화를 지정할 수 있습니다 **정책 사용** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추 .</span><span class="sxs-lookup"><span data-stu-id="603ff-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="603ff-329">특정 응용 프로그램의 조건부 액세스 정책 확인</span><span class="sxs-lookup"><span data-stu-id="603ff-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="603ff-330">toocheck 단일 응용 프로그램의 현재 구성 된 조건부 액세스 정책을 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="603ff-331">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-332">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-333">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-334">클릭 **엔터프라이즈 응용 프로그램** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-335">**모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-335">click **All applications**.</span></span>

6.  <span data-ttu-id="603ff-336">검색은 toosign tooby 응용 프로그램에서 시도 관심 있는 또는 사용자를 환영 hello 응용 프로그램에 대 한 표시 이름 또는 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="603ff-337">Hello 응용 프로그램에 대 한 원하는 보이지 않으면 클릭 hello **필터** 단추 및 hello 목록의 hello 범위가 너무 확장 되는**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="603ff-338">Toosee 더 많은 열을 클릭 hello **열** 응용 프로그램에 대 한 추가 세부 정보 tooadd 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="603ff-339">hello 클릭 **조건부 액세스** 탐색 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="603ff-340">검사 하려는 hello 정책을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="603ff-341">특정 조건, 할당 또는 사용자 액세스를 차단할 수 있는 기타 설정이 없는지 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="603ff-342">이 정책 tooensure 것 적용 되지 않는 기호 안함 toodo이, 집합 hello tootemporarily 비활성화를 지정할 수 있습니다 **정책 사용** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추 .</span><span class="sxs-lookup"><span data-stu-id="603ff-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="603ff-343">특정 조건부 액세스 정책 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="603ff-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="603ff-344">toocheck 또는 단일 조건부 액세스 정책의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="603ff-345">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="603ff-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="603ff-346">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="603ff-347">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="603ff-348">클릭 **엔터프라이즈 응용 프로그램** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="603ff-349">hello 클릭 **조건부 액세스** 탐색 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="603ff-350">검사 하려는 hello 정책을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="603ff-351">Hello 설정 하 여 hello 정책을 사용 하지 않도록 **정책 사용** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="603ff-352">응용 프로그램 동의와 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="603ff-352">Problems with application consent</span></span>

<span data-ttu-id="603ff-353">Hello 적절 한 사용 권한을 승인 작업이 발생 하지 않았기 때문에 응용 프로그램 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="603ff-354">응용 프로그램 동의 문제를 해결할 수 있는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="603ff-355">사용자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="603ff-356">응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="603ff-357">단일 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="603ff-358">다중 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="603ff-359">사용자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="603ff-360">모든 열린 ID 연결 사용이 가능한 응용 프로그램에 사용 권한을 요청 하는, toohello 응용 프로그램의 로그인 화면 탐색 hello 로그인 한 사용자에 대 한 사용자의 동의 수준 toohello 응용 프로그램을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="603ff-361">원할 경우 toodo이 프로그래밍 방식으로 참조 [개별 사용자의 동의 요청](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent)합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="603ff-362">응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="603ff-363">에 대 한 **hello V1 응용 프로그램 모델을 사용 하 여 개발 된 응용 프로그램에만**를 추가 하 여이 관리자 수준 동의 toooccur 강제로 수 "**? = 프롬프트 admin\_동의**" toohello 끝날은 응용 프로그램의 로그인 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="603ff-364">에 대 한 **hello V2 응용 프로그램 모델을 사용 하 여 개발 하는 모든 응용 프로그램**, hello hello 지침에 따라이 관리자 권한으로 동의 toooccur를 적용할 수 있습니다 **디렉터리에서 hello 권한 요청 관리자** 섹션 [hello 관리자 동의 끝점을 사용 하 여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="603ff-365">단일 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="603ff-366">에 대 한 **단일 테 넌 트 응용 프로그램** (예: 개발 중인 하거나 조직에서 소유), 사용 권한을 요청 하는 수행할 수 있습니다는 **관리자 수준의 동의** 대신 모든 작업 전역 관리자로 로그인 하 고 hello 클릭 하 여 사용자 **권한을 부여** hello hello 위쪽에 단추 **응용 프로그램 레지스트리-&gt; 모든 응용 프로그램-&gt; -응용 프로그램을 선택 합니다. &gt; 필요한 권한** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="603ff-367">에 대 한 **hello V1 또는 V2 응용 프로그램 모델을 사용 하 여 개발 하는 모든 응용 프로그램**, hello hello 지침에 따라이 관리자 권한으로 동의 toooccur를 적용할 수 있습니다 **hello 사용 권한 요청을 디렉터리 관리자** 섹션 [hello 관리자 동의 끝점을 사용 하 여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="603ff-368">다중 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="603ff-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="603ff-369">권한을 요청하는 **다중 테넌트 응용 프로그램**의 경우(예: 타사 또는 Microsoft에서 개발하는 응용 프로그램) **관리 수준 동의** 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="603ff-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="603ff-370">전역 관리자로 로그인 하 고 hello 클릭할 **권한을 부여** hello에 따라 단추 **엔터프라이즈 응용 프로그램-&gt; 모든 응용 프로그램-&gt; 앱-선택&gt; 사용 권한** 블레이드 (사용 가능한 빨리).</span><span class="sxs-lookup"><span data-stu-id="603ff-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="603ff-371">Hello hello 지침에 따라는 관리자 권한으로 동의 toooccur이도 강제 적용할 수 **hello 권한을 디렉터리 관리자의 요청** 섹션 [hello 관리자 동의 끝점를사용하여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="603ff-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="603ff-372">다음 단계</span><span class="sxs-lookup"><span data-stu-id="603ff-372">Next steps</span></span>
[<span data-ttu-id="603ff-373">Hello 관리자 동의 끝점을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="603ff-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

