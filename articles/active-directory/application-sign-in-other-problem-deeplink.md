---
title: "딥 링크를 사용 하 여 tooan 응용 프로그램에 로그인 aaaProblems | Microsoft Docs"
description: "어떻게 응용 프로그램에서 Azure AD를 사용 하 여 딥 링크 URL 액세스 tootroubleshoot 문제"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="ec2e9-103">문제는 딥 링크를 사용 하 여 tooan 응용 프로그램에 로그인</span><span class="sxs-lookup"><span data-stu-id="ec2e9-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="ec2e9-104">hello 액세스 패널은 작업으로는 사용할 수 있는 웹 기반 포털 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 hello Azure AD 관리자가 부여 해 준에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="ec2e9-105">이러한 응용 프로그램 hello Azure AD 포털에서 hello 사용자를 대신 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="ec2e9-106">hello 응용 프로그램을 올바르게 구성 되어야 합니다. 및 할당 된 toohello 사용자 또는 그룹 hello 사용자가 hello 액세스 패널에에서 toosee hello 응용 프로그램의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="ec2e9-107">딥 링크 또는 사용자 액세스 Url은 사용자가 tooaccess password SSO 응용 프로그램 직접 자신의 브라우저 URL에서 막대를 사용할 수 있습니다는 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="ec2e9-108">Toothis 링크를 이동 하 여 사용자가 자동으로 상태가 toogo toohello 액세스 패널을 먼저 필요 없이 hello 응용 프로그램에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="ec2e9-109">이 hello 같은 링크는 사용자가 사용 하 여 tooaccess hello Office 365 응용 프로그램 실행 프로그램에서 이러한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="ec2e9-110">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="ec2e9-110">General issues toocheck first</span></span>

-   <span data-ttu-id="ec2e9-111">사용 하 여 있는지 확인 한 **브라우저** hello hello 액세스 패널에 대 한 최소 요구 사항을 충족 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="ec2e9-112">Hello 사용자의 브라우저 hello 응용 프로그램 tooits의 hello URL이 추가 되었는지 확인 **신뢰할 수 있는 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="ec2e9-113">Toocheck hello 응용 프로그램 인지 확인 **구성** 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="ec2e9-114">Hello 사용자의 계정이 인지 확인 **활성화** 에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="ec2e9-115">Hello 사용자의 계정이 인지 확인 **잠겨 있지 않으면입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="ec2e9-116">있는지 hello 사용자 확인 **암호를 만료 하거나 잊어버린 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="ec2e9-117">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="ec2e9-118">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="ec2e9-119">다음 사항을 확인 한 사용자의 **인증 연락처 정보** toodate tooallow Multi-factor Authentication 또는 조건부 액세스 정책 toobe 적용 중일 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="ec2e9-120">확인 되었는지 tooalso try 브라우저의 쿠키를 지우고 toosign에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="ec2e9-121">Hello 딥 링크를 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="ec2e9-121">Checking hello deeplink</span></span>

<span data-ttu-id="ec2e9-122">아래의 hello 단계를 수행 하는 toocheck hello 올바른 딥 링크를 설정한 경우:</span><span class="sxs-lookup"><span data-stu-id="ec2e9-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-123">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ec2e9-124">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec2e9-125">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec2e9-126">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec2e9-127">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ec2e9-128">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ec2e9-129">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="ec2e9-130">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="ec2e9-131">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="ec2e9-132">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="ec2e9-133">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ec2e9-134">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="ec2e9-135">Hello 응용 프로그램에 대 한 hello 검사 hello 딥 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="ec2e9-136">Hello 레이블의 찾을 **사용자 액세스 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="ec2e9-137">딥 링크가 URL과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="ec2e9-138">Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ec2e9-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="ec2e9-139">아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="ec2e9-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-140">열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="ec2e9-141">클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="ec2e9-142">Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="ec2e9-143">브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="ec2e9-144">**추가** hello 확장 tooyour 브라우저.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="ec2e9-145">브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="ec2e9-146">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="ec2e9-147">Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ec2e9-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="ec2e9-148">Hello 직접 링크 아래에서 Chrome 및 Firefox에 대 한 hello 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="ec2e9-149">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="ec2e9-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="ec2e9-150">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="ec2e9-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="ec2e9-151">Azure AD 갤러리 응용 프로그램에 대 한 sign-on tooconfigure 암호 single 방법</span><span class="sxs-lookup"><span data-stu-id="ec2e9-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="ec2e9-152">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ec2e9-153">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ec2e9-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="ec2e9-154">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ec2e9-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ec2e9-155">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ec2e9-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ec2e9-156">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="ec2e9-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-157">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="ec2e9-158">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec2e9-159">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec2e9-160">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec2e9-161">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="ec2e9-162">Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="ec2e9-163">Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="ec2e9-164">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="ec2e9-165">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="ec2e9-166">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ec2e9-167">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ec2e9-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ec2e9-168">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-169">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ec2e9-170">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec2e9-171">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec2e9-172">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec2e9-173">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ec2e9-174">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ec2e9-175">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ec2e9-176">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ec2e9-177">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ec2e9-178">[Toohello 응용 프로그램 사용자를 할당](#how-to-assign-a-user-to-an-application-directly)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="ec2e9-179">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ec2e9-180">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ec2e9-181">Tooconfigure 암호 로그온 갤러리가 아닌 응용 프로그램에 대 한 단일 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ec2e9-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ec2e9-182">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ec2e9-183">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ec2e9-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="ec2e9-184">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ec2e9-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="ec2e9-185">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ec2e9-185">Add a non-gallery application</span></span>

<span data-ttu-id="ec2e9-186">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="ec2e9-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-187">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="ec2e9-188">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec2e9-189">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec2e9-190">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec2e9-191">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="ec2e9-192">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="ec2e9-193">Hello에 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="ec2e9-194">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-194">Select **Add.**</span></span>

<span data-ttu-id="ec2e9-195">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ec2e9-196">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ec2e9-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ec2e9-197">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-198">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ec2e9-199">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec2e9-200">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec2e9-201">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec2e9-202">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="ec2e9-203">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ec2e9-204">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ec2e9-205">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ec2e9-206">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ec2e9-207">Hello 입력 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="ec2e9-208">사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="ec2e9-209">Hello 로그인 필드 hello URL에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="ec2e9-210">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="ec2e9-211">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ec2e9-212">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="ec2e9-213">어떻게 tooassign 사용자 tooan 응용 프로그램을 직접</span><span class="sxs-lookup"><span data-stu-id="ec2e9-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="ec2e9-214">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="ec2e9-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ec2e9-215">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ec2e9-216">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec2e9-217">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec2e9-218">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec2e9-219">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ec2e9-220">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ec2e9-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ec2e9-221">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ec2e9-222">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ec2e9-223">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ec2e9-224">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ec2e9-225">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ec2e9-226">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ec2e9-227">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ec2e9-228">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="ec2e9-229">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ec2e9-230">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="ec2e9-231">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="ec2e9-232">짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="ec2e9-233">이러한 문제 해결 단계 hello 하지 않는 경우에 hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="ec2e9-234">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="ec2e9-235">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="ec2e9-235">Correlation error ID</span></span>

-   <span data-ttu-id="ec2e9-236">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="ec2e9-236">UPN (user email address)</span></span>

-   <span data-ttu-id="ec2e9-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="ec2e9-237">TenantID</span></span>

-   <span data-ttu-id="ec2e9-238">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="ec2e9-238">Browser type</span></span>

-   <span data-ttu-id="ec2e9-239">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="ec2e9-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="ec2e9-240">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="ec2e9-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec2e9-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec2e9-241">Next steps</span></span>
[<span data-ttu-id="ec2e9-242">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2e9-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
