---
title: "Microsoft 응용 프로그램에 로그인하는 문제 | Microsoft Docs"
description: "Office 365와 같은 Azure AD를 사용하여 자사 Microsoft 응용 프로그램에 로그인할 때 직면하는 일반적인 문제 해결"
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="70290-103">Microsoft 응용 프로그램에 로그인하는 문제</span><span class="sxs-lookup"><span data-stu-id="70290-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="70290-104">타사 SaaS 응용 프로그램 또는 Single Sign-On을 위해 Azure AD와 통합하는 다른 응용 프로그램과는 약간 다른 방법으로 Microsoft 응용 프로그램(예: Office 365 Exchange, SharePoint, Yammer 등)을 할당하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="70290-105">사용자는 세 가지 방법으로 Microsoft 게시 응용 프로그램에 대한 액세스 권한을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="70290-106">Office 365 또는 기타 유료 도구 모음에 있는 응용 프로그램의 경우 사용자는 **라이선스 할당**을 통해 해당 사용자 계정으로 직접 액세스가 부여되거나 그룹 기반 라이선스 할당 기능을 사용하여 그룹을 통해 액세스가 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="70290-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="70290-107">Microsoft 또는 타사에서 누구나 자유롭게 사용하도록 게시한 응용 프로그램의 경우 사용자는 **사용자 동의**를 통해 액세스 권한을 부여받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="70290-108">즉, 해당 Azure AD 회사 또는 학교 계정을 사용하여 응용 프로그램에 로그인하고 해당 계정에 대한 일부 제한된 데이터 집합에 대한 액세스 권한을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="70290-109">Microsoft 또는 타사에서 누구나 자유롭게 사용하도록 게시한 응용 프로그램의 경우 사용자도 **관리자 동의**를 통해 액세스 권한을 부여받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="70290-110">즉, 관리자는 전역 관리자 계정 사용하여 응용 프로그램에 로그인하고 조직의 모든 사용자에게 액세스 권한을 부여하도록 조직의 모든 사용자가 응용 프로그램을 사용할 수 있게 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="70290-111">문제를 해결하려면 [고려할 응용 프로그램 액세스의 일반적인 문제 영역](#general-problem-areas-with-application-access-to-consider)으로 시작하고 [연습: Microsoft 응용 프로그램 액세스를 해결하는 단계](#walkthrough-steps-to-troubleshoot-microsoft-application-access)를 읽고 세부 정보를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="70290-112">고려할 응용 프로그램 액세스의 일반적인 문제 영역</span><span class="sxs-lookup"><span data-stu-id="70290-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="70290-113">시작할 위치를 파악하는 경우 자세히 알아볼 수 있는 일반적인 문제 영역의 목록은 다음과 같습니다. 하지만 신속하게 [연습: Microsoft 응용 프로그램 액세스를 해결하는 단계](#walkthrough-steps-to-troubleshoot-microsoft-application-access) 연습을 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="70290-114">사용자의 계정과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="70290-115">그룹과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="70290-116">조건부 액세스 정책과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="70290-117">응용 프로그램 동의와 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="70290-118">Microsoft 응용 프로그램 액세스 문제를 해결하는 단계</span><span class="sxs-lookup"><span data-stu-id="70290-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="70290-119">사용자가 Microsoft 응용 프로그램에 로그인할 수 없는 경우 발생하는 몇 가지 일반적인 문제는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="70290-120">먼저 확인해야 할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="70290-120">General issues to check first</span></span>

  * <span data-ttu-id="70290-121">사용자가 로컬 응용 프로그램 URL이 아닌 **올바른 URL**에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="70290-122">사용자의 계정이 **잠겨 있지 않는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="70290-123">Azure Active Directory에 **사용자의 계정이 존재해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="70290-124">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="70290-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="70290-125">사용자의 계정이 로그인에 대해 **활성화**되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="70290-126">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="70290-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="70290-127">사용자의 **암호가 만료되거나 기억하지 못하는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="70290-128">[사용자의 암호 재설정](#reset-a-users-password) 또는 [셀프 서비스 암호 재설정 사용](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="70290-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="70290-129">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="70290-130">[사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status) 또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="70290-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="70290-131">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="70290-132">[특정 조건부 액세스 정책 확인](#problems-with-conditional-access-policies) 또는 [특정 응용 프로그램의 조건부 액세스 정책 확인](#check-a-specific-applications-conditional-access-policy) 또는 [특정 조건부 액세스 정책 사용 안 함](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="70290-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="70290-133">사용자의 **인증 연락처 정보**를 최신으로 유지하여 Multi-Factor Authentication 또는 조건부 액세스 정책을 적용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="70290-134">[사용자의 Multi-Factor Authentication 상태 확인](#check-a-users-multi-factor-authentication-status) 또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="70290-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="70290-135">라이선스를 필요로 하는 **Microsoft** **응용 프로그램**(예: office 365)의 경우 위의 일반 문제를 확인하면 확인할 몇 가지 특정 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="70290-136">사용자를 확인하거나 **라이선스를 할당합니다.**</span><span class="sxs-lookup"><span data-stu-id="70290-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="70290-137">[사용자의 할당된 라이선스 확인](#check-a-users-assigned-licenses) 또는 [그룹의 할당된 라이선스 확인](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="70290-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="70290-138">라이선스가 **정적 그룹****에 할당되는** 경우 해당 그룹의 **사용자가 구성원인지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="70290-139">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="70290-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="70290-140">라이선스가 **동적 그룹****에 할당되는** 경우 **동적 그룹 규칙을 올바르게 설정했는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="70290-141">동적 그룹의 구성원 자격 조건 확인</span><span class="sxs-lookup"><span data-stu-id="70290-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="70290-142">라이선스가 **동적 그룹****에 할당되는** 경우 동적 그룹이 해당 구성원의 **처리를 완료했는지** 및 **사용자가 구성원인지** 확인합니다(시간이 걸릴 수 있음).</span><span class="sxs-lookup"><span data-stu-id="70290-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="70290-143">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="70290-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="70290-144">라이선스가 할당되었는지 확인하면 라이선스가 **만료되지 않았는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="70290-145">라이선스가 액세스하는 **응용 프로그램에 적용되는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="70290-146">라이선스를 필요로 하지 않는 **Microsoft** **응용 프로그램**의 경우 확인할 몇 가지 다른 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="70290-147">응용 프로그램이 **사용자 수준 사용 권한**을 요청하는 경우(예: "이 사용자의 사서함에 액세스") 사용자가 응용 프로그램에 로그인하고 **사용자 수준 동의 작업**을 수행하여 응용 프로그램이 해당 데이터에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="70290-148">응용 프로그램이 **관리자 수준 사용 권한**을 요청하는 경우(예: "모든 사용자의 사서함 액세스 권한") 전역 관리자가 조직의 **모든 사용자를 대신하여 관리자 수준 동의 작업**을 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="70290-149">사용자의 계정과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-149">Problems with the user’s account</span></span>

<span data-ttu-id="70290-150">응용 프로그램에 할당된 사용자와 관련된 문제로 인해 응용 프로그램 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="70290-151">다음 몇 가지 방법으로 사용자 및 해당 계정 설정과 관련된 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="70290-152">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="70290-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="70290-153">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="70290-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="70290-154">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="70290-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="70290-155">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="70290-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="70290-156">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="70290-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="70290-157">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="70290-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="70290-158">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="70290-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="70290-159">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="70290-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="70290-160">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="70290-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="70290-161">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="70290-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="70290-162">사용자의 계정이 있는지를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-163">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-164">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-165">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-166">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-167">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-167">click **All users**.</span></span>

6.  <span data-ttu-id="70290-168">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-169">사용자 개체의 속성이 예상한 대로 표시되고 데이터가 누락되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="70290-170">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="70290-170">Check a user’s account status</span></span>

<span data-ttu-id="70290-171">사용자의 계정 상태를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-172">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-173">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-174">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-175">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-176">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-176">click **All users**.</span></span>

6.  <span data-ttu-id="70290-177">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-178">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-178">click **Profile**.</span></span>

8.  <span data-ttu-id="70290-179">**설정** 아래에서 **로그인 차단**이 **아니오**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="70290-180">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="70290-180">Reset a user’s password</span></span>

<span data-ttu-id="70290-181">사용자의 암호를 다시 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-182">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-183">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-184">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-185">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-186">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-186">click **All users**.</span></span>

6.  <span data-ttu-id="70290-187">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-188">사용자 블레이드 맨 위에 있는 **암호 재설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="70290-189">표시되는 **암호 재설정** 블레이드에서 **암호 재설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="70290-190">사용자를 위한 **임시 암호** 또는 **새 암호 입력**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="70290-191">사용자에게 이 새 암호를 전달하고 다음 번에 Azure Active Directory에 로그인하는 동안 이 암호를 변경하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="70290-192">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="70290-192">Enable self-service password reset</span></span>

<span data-ttu-id="70290-193">셀프 서비스 암호 재설정을 사용하려면 아래 배포 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="70290-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="70290-194">사용자가 Azure Active Directory 암호를 재설정할 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="70290-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="70290-195">사용자가 Active Directory 온-프레미스 암호를 재설정하거나 변경하도록 설정</span><span class="sxs-lookup"><span data-stu-id="70290-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="70290-196">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="70290-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="70290-197">사용자의 Multi-Factor Authentication 상태를 확인하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-198">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-199">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-200">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-201">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-202">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-202">click **All users**.</span></span>

6.  <span data-ttu-id="70290-203">블레이드 맨 위에 있는 **Multi-Factor Authentication** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="70290-204">**Multi-factor Authentication 관리 포털**을 일단 로드하면 **사용자** 탭인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="70290-205">검색, 필터링 또는 정렬을 사용하여 사용자 목록에서 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="70290-206">사용자 목록에서 사용자를 선택하고 원하는 대로 Multi-Factor Authentication을 **사용**, **사용 안 함** 또는 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="70290-207">**참고**: 사용자가 **강제된** 상태인 경우 일시적으로 **사용 안 함**으로 설정하여 해당 계정으로 다시 돌아올 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="70290-208">다시 돌아오면 해당 상태를 **사용**으로 변경하여 다음 번에 로그인하는 도중 해당 연락처 정보를 다시 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="70290-209">또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)에 있는 단계를 수행하여 이 데이터를 확인하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="70290-210">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="70290-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="70290-211">Multi-Factor Authentication, 조건부 액세스, ID 보호 및 암호 재설정에 사용되는 사용자의 인증 연락처 정보를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-212">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-213">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-214">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-215">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-216">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-216">click **All users**.</span></span>

6.  <span data-ttu-id="70290-217">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-218">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-218">click **Profile**.</span></span>

8.  <span data-ttu-id="70290-219">**인증 연락처 정보**까지 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="70290-220">필요에 따라 사용자 및 업데이트에 등록된 데이터를 **검토**합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="70290-221">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="70290-221">Check a user’s group memberships</span></span>

<span data-ttu-id="70290-222">사용자의 그룹 구성원 자격을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-223">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-224">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-225">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-226">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-227">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-227">click **All users**.</span></span>

6.  <span data-ttu-id="70290-228">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-229">**그룹**을 클릭하여 사용자가 구성원으로 참여하는 그룹을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="70290-230">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="70290-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="70290-231">사용자의 할당된 라이선스를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-232">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-233">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-234">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-235">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-236">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-236">click **All users**.</span></span>

6.  <span data-ttu-id="70290-237">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-238">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="70290-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="70290-239">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="70290-239">Assign a user a license</span></span> 

<span data-ttu-id="70290-240">사용자에게 라이선스를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-241">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-242">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-243">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-244">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-245">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-245">click **All users**.</span></span>

6.  <span data-ttu-id="70290-246">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-247">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="70290-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="70290-248">**할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="70290-249">사용 가능한 제품 목록에서 **하나 이상의 제품**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="70290-250">**선택 사항** 제품을 상세하게 할당하려면 **할당 옵션** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="70290-251">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="70290-252">**할당** 단추를 클릭하여 이러한 라이선스를 이 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="70290-253">그룹과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-253">Problems with groups</span></span>

<span data-ttu-id="70290-254">응용 프로그램에 할당된 그룹과 관련된 문제로 인해 응용 프로그램 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="70290-255">다음 몇 가지 방법으로 그룹 및 구성원 자격과 관련된 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="70290-256">그룹의 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="70290-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="70290-257">동적 그룹의 구성원 자격 조건 확인</span><span class="sxs-lookup"><span data-stu-id="70290-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="70290-258">그룹의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="70290-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="70290-259">그룹의 라이선스 다시 처리</span><span class="sxs-lookup"><span data-stu-id="70290-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="70290-260">그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="70290-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="70290-261">그룹의 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="70290-261">Check a group’s membership</span></span>

<span data-ttu-id="70290-262">그룹의 구성원 자격을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-263">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-264">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-265">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-266">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-267">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-267">click **All groups**.</span></span>

6.  <span data-ttu-id="70290-268">관심이 있는 그룹을 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-269">**구성원**을 클릭하여 이 그룹에 할당된 사용자의 목록을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="70290-270">동적 그룹의 구성원 자격 조건 확인</span><span class="sxs-lookup"><span data-stu-id="70290-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="70290-271">동적 그룹의 구성원 자격 조건을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-272">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-273">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-274">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-275">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-276">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-276">click **All groups**.</span></span>

6.  <span data-ttu-id="70290-277">관심이 있는 그룹을 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-278">**동적 구성원 자격 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="70290-279">이 그룹에 대해 정의된 **단순** 또는 **고급** 규칙을 검토하고 이 그룹의 구성원으로 포함하려는 사용자가 이러한 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="70290-280">그룹의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="70290-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="70290-281">그룹의 할당된 라이선스를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-282">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-283">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-284">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-285">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-286">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-286">click **All groups**.</span></span>

6.  <span data-ttu-id="70290-287">관심이 있는 그룹을 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-288">**라이선스**를 클릭하여 그룹이 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="70290-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="70290-289">그룹의 라이선스 다시 처리</span><span class="sxs-lookup"><span data-stu-id="70290-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="70290-290">그룹의 할당된 라이선스를 다시 처리하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-291">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-292">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-293">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-294">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-295">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-295">click **All groups**.</span></span>

6.  <span data-ttu-id="70290-296">관심이 있는 그룹을 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-297">**라이선스**를 클릭하여 그룹이 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="70290-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="70290-298">**다시 처리** 단추를 클릭하여 이 그룹의 구성원에게 할당된 라이선스가 최신인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="70290-299">그룹의 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="70290-300">시간을 단축하려면 일시적으로 라이선스를 사용자에게 직접 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="70290-301">[사용자에게 라이선스를 할당합니다](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="70290-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="70290-302">그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="70290-302">Assign a group a license</span></span>

<span data-ttu-id="70290-303">그룹에 라이선스를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="70290-304">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-305">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-306">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-307">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-308">**모든 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-308">click **All groups**.</span></span>

6.  <span data-ttu-id="70290-309">관심이 있는 그룹을 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="70290-310">**라이선스**를 클릭하여 그룹이 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="70290-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="70290-311">**할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="70290-312">사용 가능한 제품 목록에서 **하나 이상의 제품**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="70290-313">**선택 사항** 제품을 상세하게 할당하려면 **할당 옵션** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="70290-314">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="70290-315">**할당** 단추를 클릭하여 이러한 라이선스를 이 그룹에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="70290-316">그룹의 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="70290-317">시간을 단축하려면 일시적으로 라이선스를 사용자에게 직접 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="70290-318">[사용자에게 라이선스를 할당합니다](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="70290-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="70290-319">조건부 액세스 정책과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="70290-320">특정 조건부 액세스 정책 확인</span><span class="sxs-lookup"><span data-stu-id="70290-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="70290-321">단일 조건부 액세스 정책을 확인하거나 유효성을 검사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="70290-322">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-323">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-324">필터 검색 상자에 **"Azure Active Directory**"를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-325">탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-326">**조건부 액세스** 탐색 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="70290-327">검사하려는 정책을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="70290-328">특정 조건, 할당 또는 사용자 액세스를 차단할 수 있는 기타 설정이 없는지 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="70290-329">일시적으로 이 정책을 사용하지 않도록 설정하여 로그인에 영향을 주지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="70290-330">이를 위해 **정책 사용** 토글을 **아니오**로 설정하고 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="70290-331">특정 응용 프로그램의 조건부 액세스 정책 확인</span><span class="sxs-lookup"><span data-stu-id="70290-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="70290-332">단일 응용 프로그램의 현재 구성된 조건부 액세스 정책을 확인하거나 유효성을 검사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="70290-333">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-334">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-335">필터 검색 상자에 **"Azure Active Directory**"를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-336">탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-337">**모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-337">click **All applications**.</span></span>

6.  <span data-ttu-id="70290-338">응용 프로그램 표시 이름 또는 응용 프로그램 ID를 기준으로 관심이 있는 응용 프로그램이나 로그인하려는 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="70290-339">찾고 있는 응용 프로그램이 보이지 않으면 **필터** 단추를 클릭하고 목록 범위를 **모든 응용 프로그램**으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="70290-340">더 많은 열을 표시하려면 **열** 단추를 클릭하여 응용 프로그램의 추가 세부 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="70290-341">**조건부 액세스** 탐색 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="70290-342">검사하려는 정책을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="70290-343">특정 조건, 할당 또는 사용자 액세스를 차단할 수 있는 기타 설정이 없는지 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="70290-344">일시적으로 이 정책을 사용하지 않도록 설정하여 로그인에 영향을 주지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="70290-345">이를 위해 **정책 사용** 토글을 **아니오**로 설정하고 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="70290-346">특정 조건부 액세스 정책 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="70290-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="70290-347">단일 조건부 액세스 정책을 확인하거나 유효성을 검사하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="70290-348">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70290-349">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70290-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70290-350">필터 검색 상자에 **"Azure Active Directory**"를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70290-351">탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="70290-352">**조건부 액세스** 탐색 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="70290-353">검사하려는 정책을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="70290-354">**정책 사용** 토글을 **아니오**로 설정하여 정책을 사용하지 않도록 설정하고 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70290-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="70290-355">응용 프로그램 동의와 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="70290-355">Problems with application consent</span></span>

<span data-ttu-id="70290-356">적절한 사용 권한 동의 작업이 발생하지 않았기 때문에 응용 프로그램 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="70290-357">응용 프로그램 동의 문제를 해결할 수 있는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="70290-358">사용자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="70290-359">응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="70290-360">단일 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="70290-361">다중 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="70290-362">사용자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="70290-363">사용 권한을 요청하는 Open ID Connect 사용 응용 프로그램에서 응용 프로그램의 로그인 화면으로 이동하면 로그인한 사용자의 응용 프로그램에 대한 사용자 수준 동의가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="70290-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="70290-364">이 작업을 프로그래밍 방식으로 수행하려는 경우 [개별 사용자의 동의 요청](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70290-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="70290-365">응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="70290-366">**V1 응용 프로그램 모델을 사용하여 개발된 응용 프로그램**의 경우에만 응용 프로그램의 로그인 URL의 끝에 “**?prompt=admin\_consent**”를 추가하여 발생하는 이 관리자 수준 동의를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="70290-367">**V2 응용 프로그램 모델을 사용하여 개발된 응용 프로그램**의 경우 [관리 동의 끝점 사용](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)의 **디렉터리 관리에서 사용 권한 요청** 섹션 아래에 있는 지침에 따라 발생하는 이 관리자 수준 동의를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="70290-368">단일 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="70290-369">사용 권한을 요청하는 **단일 테넌트 응용 프로그램**의 경우(예: 사용자가 개발하거나 조직에서 소유한 응용 프로그램) 전역 관리자로 로그인하고 **응용 프로그램 레지스트리 -&gt; 모든 응용 프로그램 -&gt; 앱 선택 -&gt; 필요한 권한 -** 블레이드의 맨 위에 있는 **권한 부여** 단추를 클릭하여 모든 사용자를 대신하여 **관리 수준 동의** 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="70290-370"> **V1 또는 V2 응용 프로그램 모델을 사용하여 개발된 응용 프로그램**의 경우 [관리 동의 끝점 사용](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)의 **디렉터리 관리에서 사용 권한 요청** 섹션 아래에 있는 지침에 따라 발생하는 이 관리자 수준 동의를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="70290-371">다중 테넌트 응용 프로그램에 대해 관리자 수준 동의 작업 수행</span><span class="sxs-lookup"><span data-stu-id="70290-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="70290-372">권한을 요청하는 **다중 테넌트 응용 프로그램**의 경우(예: 타사 또는 Microsoft에서 개발하는 응용 프로그램) **관리 수준 동의** 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="70290-373">전역 관리자로 로그인하고 **엔터프라이즈 응용 프로그램 -&gt; 모든 응용 프로그램 -&gt; 앱 선택 -&gt; 사용 권한** 블레이드에서 **권한 부여** 단추를 클릭합니다(곧 사용 가능).</span><span class="sxs-lookup"><span data-stu-id="70290-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="70290-374">또한 [관리 동의 끝점 사용](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)의 **디렉터리 관리에서 사용 권한 요청** 섹션 아래에 있는 지침에 따라 발생하는 이 관리자 수준 동의를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70290-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70290-375">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70290-375">Next steps</span></span>
[<span data-ttu-id="70290-376">관리 동의 끝점 사용</span><span class="sxs-lookup"><span data-stu-id="70290-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

