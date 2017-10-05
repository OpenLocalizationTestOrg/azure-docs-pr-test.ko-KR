---
title: "액세스 패널 웹 사이트에 로그인할 때 발생하는 문제 | Microsoft Docs"
description: "액세스 패널을 사용하여 로그인하려고 하는 동안 발생할 수 있는 문제를 해결하기 위한 지침"
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
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="93ed2-103">액세스 패널 웹 사이트에 로그인할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="93ed2-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="93ed2-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="93ed2-105">또한 Azure AD 버전의 사용자는 액세스 패널을 통해 셀프 서비스 그룹 및 앱 관리 기능을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="93ed2-106">액세스 패널은 Azure Portal과 별개이며, 사용자에게 Azure 구독을 요구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="93ed2-107">사용자는 Azure AD에서 회사 또는 학교 계정이 있는 경우 액세스 패널에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="93ed2-108">사용자는 Azure AD에서 직접 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="93ed2-109">사용자는 AD FS(Active Directory Federation Services)를 사용하여 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="93ed2-110">사용자는 Windows Server Active Directory에서 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="93ed2-111">사용자가 Azure 또는 Office 365에 대한 구독을 가지고 있고 Azure Portal 또는 Office 365 응용 프로그램을 사용하고 있으면, 다시 로그인할 필요 없이 액세스 패널을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="93ed2-112">인증되지 않은 사용자는 Azure AD 계정에 대한 사용자 이름과 암호를 사용하여 로그인하도록 요청받습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="93ed2-113">조직에서 페더레이션을 구성한 경우 사용자 이름만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="93ed2-114">먼저 확인해야 할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="93ed2-114">General issues to check first</span></span> 

-   <span data-ttu-id="93ed2-115">사용자가 **올바른 URL**(<https://myapps.microsoft.com>)에 로그인되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="93ed2-116">사용자의 브라우저에서 해당 **신뢰할 수 있는 사이트**에 URL을 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="93ed2-117">사용자의 계정이 로그인에 대해 **활성화**되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="93ed2-118">사용자의 계정이 **잠겨 있지 않는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="93ed2-119">사용자의 **암호가 만료되거나 기억하지 못하는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="93ed2-120">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="93ed2-121">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="93ed2-122">사용자의 **인증 연락처 정보**를 최신으로 유지하여 Multi-Factor Authentication 또는 조건부 액세스 정책을 적용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="93ed2-123">브라우저의 쿠키를 지우고 다시 로그인하려고 시도할 수도 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="93ed2-124">액세스 패널에 대한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="93ed2-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="93ed2-125">액세스 패널에는 JavaScript를 지원하고 CSS를 사용하도록 설정한 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="93ed2-126">액세스 패널에서 암호 기반 SSO(Single Sign-On)를 사용하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="93ed2-127">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="93ed2-128">암호 기반 SSO의 경우 최종 사용자 브라우저는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="93ed2-129">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="93ed2-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="93ed2-130">Windows 10 Anniversary Edition 이상 Edge</span><span class="sxs-lookup"><span data-stu-id="93ed2-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="93ed2-131">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="93ed2-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="93ed2-132">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="93ed2-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="93ed2-133">사용자의 계정과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="93ed2-133">Problems with the user’s account</span></span>

<span data-ttu-id="93ed2-134">사용자의 계정 문제로 인해 액세스 패널에 대한 액세스가 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="93ed2-135">다음 몇 가지 방법으로 사용자 및 해당 계정 설정과 관련된 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="93ed2-136">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="93ed2-137">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="93ed2-138">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="93ed2-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="93ed2-139">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="93ed2-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="93ed2-140">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="93ed2-141">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="93ed2-142">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="93ed2-143">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="93ed2-144">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="93ed2-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="93ed2-145">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="93ed2-146">사용자의 계정이 있는지를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-147">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-148">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-149">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-150">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-151">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-151">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-152">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-153">사용자 개체의 속성이 예상한 대로 표시되고 데이터가 누락되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="93ed2-154">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-154">Check a user’s account status</span></span>

<span data-ttu-id="93ed2-155">사용자의 계정 상태를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-156">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-157">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-158">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-159">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-160">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-160">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-161">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-162">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-162">click **Profile**.</span></span>

8.  <span data-ttu-id="93ed2-163">**설정** 아래에서 **로그인 차단**이 **아니오**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="93ed2-164">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="93ed2-164">Reset a user’s password</span></span>

<span data-ttu-id="93ed2-165">사용자의 암호를 다시 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-166">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-167">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-168">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-169">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-170">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-170">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-171">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-172">사용자 블레이드 맨 위에 있는 **암호 재설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="93ed2-173">표시되는 **암호 재설정** 블레이드에서 **암호 재설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="93ed2-174">사용자를 위한 **임시 암호** 또는 **새 암호 입력**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="93ed2-175">사용자에게 이 새 암호를 전달하고 다음 번에 Azure Active Directory에 로그인하는 동안 이 암호를 변경하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="93ed2-176">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="93ed2-176">Enable self-service password reset</span></span>

<span data-ttu-id="93ed2-177">셀프 서비스 암호 재설정을 사용하려면 아래 배포 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="93ed2-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="93ed2-178">사용자가 Azure Active Directory 암호를 재설정할 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="93ed2-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="93ed2-179">사용자가 Active Directory 온-프레미스 암호를 재설정하거나 변경하도록 설정</span><span class="sxs-lookup"><span data-stu-id="93ed2-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="93ed2-180">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="93ed2-181">사용자의 Multi-Factor Authentication 상태를 확인하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-182">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-183">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-184">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-185">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-186">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-186">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-187">블레이드 맨 위에 있는 **Multi-Factor Authentication** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="93ed2-188">**Multi-factor Authentication 관리 포털**을 일단 로드하면 **사용자** 탭인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="93ed2-189">검색, 필터링 또는 정렬을 사용하여 사용자 목록에서 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="93ed2-190">사용자 목록에서 사용자를 선택하고 원하는 대로 Multi-Factor Authentication을 **사용**, **사용 안 함** 또는 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="93ed2-191">사용자가 **강제된** 상태인 경우 일시적으로 **사용 안 함**으로 설정하여 해당 계정으로 다시 돌아올 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="93ed2-192">다시 돌아오면 해당 상태를 **사용**으로 변경하여 다음 번에 로그인하는 도중 해당 연락처 정보를 다시 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="93ed2-193">또는 [사용자의 인증 연락처 정보 확인](#check-a-users-authentication-contact-info)에 있는 단계를 수행하여 이 데이터를 확인하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="93ed2-194">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="93ed2-195">Multi-Factor Authentication, 조건부 액세스, ID 보호 및 암호 재설정에 사용되는 사용자의 인증 연락처 정보를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-196">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-197">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-198">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-199">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-200">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-200">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-201">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-202">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-202">click **Profile**.</span></span>

8.  <span data-ttu-id="93ed2-203">**인증 연락처 정보**까지 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="93ed2-204">필요에 따라 사용자 및 업데이트에 등록된 데이터를 **검토**합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="93ed2-205">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-205">Check a user’s group memberships</span></span>

<span data-ttu-id="93ed2-206">사용자의 그룹 구성원 자격을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-207">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-208">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-209">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-210">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-211">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-211">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-212">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-213">**그룹**을 클릭하여 사용자가 구성원으로 참여하는 그룹을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="93ed2-214">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="93ed2-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="93ed2-215">사용자의 할당된 라이선스를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-216">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-217">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-218">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-219">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-220">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-220">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-221">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-222">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="93ed2-223">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="93ed2-223">Assign a user a license</span></span> 

<span data-ttu-id="93ed2-224">사용자에게 라이선스를 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="93ed2-225">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="93ed2-226">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="93ed2-227">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="93ed2-228">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="93ed2-229">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-229">click **All users**.</span></span>

6.  <span data-ttu-id="93ed2-230">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="93ed2-231">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="93ed2-232">**할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="93ed2-233">사용 가능한 제품 목록에서 **하나 이상의 제품**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="93ed2-234">**선택 사항** 제품을 상세하게 할당하려면 **할당 옵션** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="93ed2-235">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="93ed2-236">**할당** 단추를 클릭하여 이러한 라이선스를 이 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="93ed2-237">이러한 문제 해결 단계로 문제가 해결되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="93ed2-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="93ed2-238">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93ed2-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="93ed2-239">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="93ed2-239">Correlation error ID</span></span>

-   <span data-ttu-id="93ed2-240">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="93ed2-240">UPN (user email address)</span></span>

-   <span data-ttu-id="93ed2-241">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="93ed2-241">Tenant ID</span></span>

-   <span data-ttu-id="93ed2-242">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="93ed2-242">Browser type</span></span>

-   <span data-ttu-id="93ed2-243">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="93ed2-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="93ed2-244">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="93ed2-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="93ed2-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93ed2-245">Next steps</span></span>
[<span data-ttu-id="93ed2-246">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="93ed2-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
