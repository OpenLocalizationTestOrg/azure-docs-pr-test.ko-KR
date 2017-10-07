---
title: "aaaProblem toohello 액세스 패널 웹 사이트에 로그인 | Microsoft Docs"
description: "Toosign toouse에서 시도 하는 동안 발생할 수 있는 지침 tootroubleshoot 문제 hello 액세스 패널"
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="aac9b-103">Toohello 액세스 패널 웹 사이트에 로그인 하는 문제</span><span class="sxs-lookup"><span data-stu-id="aac9b-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="aac9b-104">액세스 패널 hello 활성화 있는 사용자가 회사 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 관리자에 게 Azure AD는 웹 기반 포털이 부여 해 준에 대 한 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="aac9b-105">Azure AD 버전을 가진 사용자는 셀프 서비스 그룹 및 hello 액세스 패널을 통해 응용 프로그램 관리 기능 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="aac9b-106">액세스 패널 hello는 hello Azure 포털에서에서 분리 되 고 사용자가 toohave Azure 구독이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="aac9b-107">Azure AD에 회사 또는 학교 계정이 있는 경우 사용자가 액세스 패널 toohello 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="aac9b-108">사용자는 Azure AD에서 직접 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="aac9b-109">사용자는 AD FS(Active Directory Federation Services)를 사용하여 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="aac9b-110">사용자는 Windows Server Active Directory에서 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="aac9b-111">사용자는 Azure 또는 Office 365에 대 한 구독을 보유 하 고 hello Azure 포털 또는 Office 365 응용 프로그램에서 사용, 경우 할 것 수 toouse toosign에 다시 필요 없이 액세스 패널을 원활 하 게 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="aac9b-112">인증 되지 않은 사용자의 Azure AD에서 자신의 계정에 대 한 hello 사용자 이름 및 암호를 사용 하 여에서 증명된 toosign 수.입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="aac9b-113">Hello 조직에서 페더레이션을 구성한 경우 만으로는 hello 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="aac9b-114">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="aac9b-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="aac9b-115">Hello 사용자가 로그인 하 여 toohello에 있는지 확인 **올바른 URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="aac9b-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="aac9b-116">Hello 사용자의 브라우저 hello URL tooits가 추가 되었는지 확인 **신뢰할 수 있는 사이트**</span><span class="sxs-lookup"><span data-stu-id="aac9b-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="aac9b-117">Hello 사용자의 계정이 인지 확인 **활성화** 에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="aac9b-118">Hello 사용자의 계정이 인지 확인 **잠겨 있지 않으면입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="aac9b-119">있는지 hello 사용자 확인 **암호를 만료 하거나 잊어버린 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="aac9b-120">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="aac9b-121">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="aac9b-122">다음 사항을 확인 한 사용자의 **인증 연락처 정보** toodate tooallow Multi-factor Authentication 또는 조건부 액세스 정책 toobe 적용 중일 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="aac9b-123">확인 되었는지 tooalso try 브라우저의 쿠키를 지우고 toosign에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="aac9b-124">액세스 패널 hello에 대 한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="aac9b-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="aac9b-125">hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="aac9b-126">toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="aac9b-127">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="aac9b-128">암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="aac9b-129">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="aac9b-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="aac9b-130">Windows 10 Anniversary Edition 이상 Edge</span><span class="sxs-lookup"><span data-stu-id="aac9b-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="aac9b-131">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="aac9b-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="aac9b-132">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="aac9b-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="aac9b-133">Hello 사용자 계정과 관련 된 문제</span><span class="sxs-lookup"><span data-stu-id="aac9b-133">Problems with hello user’s account</span></span>

<span data-ttu-id="aac9b-134">액세스 패널 액세스 toohello tooa 문제 hello 사용자 계정으로 인해 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="aac9b-135">다음 몇 가지 방법으로 사용자 및 해당 계정 설정과 관련된 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="aac9b-136">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="aac9b-137">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="aac9b-138">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="aac9b-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="aac9b-139">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="aac9b-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="aac9b-140">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="aac9b-141">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="aac9b-142">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="aac9b-143">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="aac9b-144">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="aac9b-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="aac9b-145">Azure Active Directory에 사용자의 계정이 존재하는지 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="aac9b-146">아래의 hello 단계를 수행 하는 사용자의 계정이 표시 되 면 toocheck:</span><span class="sxs-lookup"><span data-stu-id="aac9b-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-147">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-148">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-149">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-150">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-151">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-151">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-152">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-153">Hello 속성의 hello 사용자 개체 toobe 고 없는 데이터가 누락 된 표시 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="aac9b-154">사용자의 계정 상태 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-154">Check a user’s account status</span></span>

<span data-ttu-id="aac9b-155">toocheck 사용자의 계정 상태, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-156">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-157">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-158">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-159">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-160">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-160">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-161">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-162">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-162">click **Profile**.</span></span>

8.  <span data-ttu-id="aac9b-163">**설정** 되도록 **블록 로그인** 너무 설정 되어**아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="aac9b-164">사용자의 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="aac9b-164">Reset a user’s password</span></span>

<span data-ttu-id="aac9b-165">tooreset 사용자의 암호를 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="aac9b-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-166">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-167">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-168">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-169">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-170">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-170">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-171">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-172">hello 클릭 **암호 재설정** hello hello 사용자 블레이드 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="aac9b-173">hello 클릭 **암호 재설정** hello에서 단추 **암호 재설정** 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="aac9b-174">복사 hello **임시 암호** 또는 **새 암호를 입력** hello 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="aac9b-175">이 새 암호 toohello 사용자 통신, 필요한 toochange tooAzure Active Directory에에서 로그인 하는 동안 다음 번이이 암호를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="aac9b-176">셀프 서비스 암호 재설정 사용</span><span class="sxs-lookup"><span data-stu-id="aac9b-176">Enable self-service password reset</span></span>

<span data-ttu-id="aac9b-177">tooenable 셀프 서비스 암호 재설정에 아래의 hello 배포 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="aac9b-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="aac9b-178">Azure Active Directory 암호 tooreset 사용자가 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="aac9b-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="aac9b-179">사용자가 tooreset를 사용 하거나 Active Directory 온-프레미스 암호 변경</span><span class="sxs-lookup"><span data-stu-id="aac9b-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="aac9b-180">사용자의 Multi-Factor Authentication 상태 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="aac9b-181">toocheck 사용자의 다단계 인증 상태, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="aac9b-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-182">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-183">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-184">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-185">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-186">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-186">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-187">hello 클릭 **Multi-factor Authentication** hello hello 블레이드 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="aac9b-188">한 번 hello **Multi-factor Authentication 관리 포털** 부하를 hello에 있는 확인 하십시오 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="aac9b-189">검색, 필터링 또는 정렬 하 여 hello 사용자 목록에서 hello 사용자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="aac9b-190">사용자의 hello 목록에서 선택 hello 사용자 및 **사용**, **사용 하지 않도록 설정**, 또는 **적용** 원하는 대로 다단계 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="aac9b-191">사용자가 있는 경우에 **Enforced** 상태 이면 너무 설정할 수 있습니다**비활성화 된** 일시적으로 toolet 다시 자신의 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="aac9b-192">인 다시 변경할 수 있습니다 다음 상태로 너무**Enabled** toorequire 다시 해당 toore 레지스터 그들의 연락처 정보 중 다음 번에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="aac9b-193">Hello의 hello 단계를 수행 수 또는 [사용자의 인증 연락처 정보를 확인](#check-a-users-authentication-contact-info) tooverify 하거나 하에이 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="aac9b-194">사용자의 인증 연락처 정보 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="aac9b-195">아래의 hello 단계를 수행 하는 사용자의 인증 연락처 정보 multi-factor authentication, 조건부 액세스, Id 보호 및 암호 재설정에 사용 되는 toocheck:</span><span class="sxs-lookup"><span data-stu-id="aac9b-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-196">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-197">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-198">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-199">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-200">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-200">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-201">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-202">**프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-202">click **Profile**.</span></span>

8.  <span data-ttu-id="aac9b-203">너무 아래로 스크롤하여**인증 연락처 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="aac9b-204">**검토** 필요에 따라 hello 데이터 hello 사용자 및 업데이트에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="aac9b-205">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-205">Check a user’s group memberships</span></span>

<span data-ttu-id="aac9b-206">toocheck 사용자의 그룹 구성원 자격, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-207">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-208">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-209">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-210">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-211">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-211">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-212">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-213">클릭 **그룹** toosee hello 사용자 그룹의 멤버인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="aac9b-214">사용자의 할당된 라이선스 확인</span><span class="sxs-lookup"><span data-stu-id="aac9b-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="aac9b-215">toocheck 사용자의 라이선스를 다음 단계에 따라 hello 할당:</span><span class="sxs-lookup"><span data-stu-id="aac9b-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-216">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-217">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-218">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-219">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-220">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-220">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-221">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-222">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="aac9b-223">사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="aac9b-223">Assign a user a license</span></span> 

<span data-ttu-id="aac9b-224">아래의 hello 단계를 수행 하는 라이선스 tooa 사용자 tooassign:</span><span class="sxs-lookup"><span data-stu-id="aac9b-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="aac9b-225">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="aac9b-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="aac9b-226">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aac9b-227">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aac9b-228">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="aac9b-229">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-229">click **All users**.</span></span>

6.  <span data-ttu-id="aac9b-230">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="aac9b-231">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="aac9b-232">Hello 클릭 **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="aac9b-233">선택 **하나 이상의 제품** hello 사용 가능한 제품 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="aac9b-234">**선택적** hello 클릭 **할당 옵션** 항목 toogranularly 제품을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="aac9b-235">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="aac9b-236">Hello 클릭 **할당** tooassign 이러한 라이선스 toothis 사용자 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="aac9b-237">이러한 문제 해결 단계 hello 문제가 해결 되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="aac9b-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="aac9b-238">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="aac9b-239">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="aac9b-239">Correlation error ID</span></span>

-   <span data-ttu-id="aac9b-240">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="aac9b-240">UPN (user email address)</span></span>

-   <span data-ttu-id="aac9b-241">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="aac9b-241">Tenant ID</span></span>

-   <span data-ttu-id="aac9b-242">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="aac9b-242">Browser type</span></span>

-   <span data-ttu-id="aac9b-243">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="aac9b-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="aac9b-244">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="aac9b-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="aac9b-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aac9b-245">Next steps</span></span>
[<span data-ttu-id="aac9b-246">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac9b-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
