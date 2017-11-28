---
title: "aaaProblems hello 액세스 패널에서 tooan 응용 프로그램에 서명 | Microsoft Docs"
description: "응용 프로그램에 액세스 하는 tootroubleshoot 문제 myapps.microsoft.com에서 Microsoft Azure AD 액세스 패널 hello 하는 방법"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="30345-103">Hello 액세스 패널에서 tooan 응용 프로그램에 로그인 하는 문제</span><span class="sxs-lookup"><span data-stu-id="30345-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="30345-104">hello 액세스 패널은 작업으로는 사용할 수 있는 웹 기반 포털 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 hello Azure AD 관리자가 부여 해 준에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="30345-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="30345-105">이러한 응용 프로그램 hello Azure AD 포털에서 hello 사용자를 대신 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30345-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="30345-106">hello 응용 프로그램을 올바르게 구성 되어야 합니다. 및 할당 된 toohello 사용자 또는 그룹 hello 사용자가 hello 액세스 패널에에서 toosee hello 응용 프로그램의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="30345-107">사용자 표시 될 수는 앱의 hello 유형 hello 다음 범주에에서 속합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="30345-108">Office 365 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30345-108">Office 365 Applications</span></span>

-   <span data-ttu-id="30345-109">페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30345-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="30345-110">암호 기반 SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30345-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="30345-111">기존 SSO 솔루션을 사용한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30345-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="30345-112">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="30345-112">General issues toocheck first</span></span>

-   <span data-ttu-id="30345-113">사용 하 여 있는지 확인 한 **브라우저** hello hello 액세스 패널에 대 한 최소 요구 사항을 충족 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="30345-114">Hello 사용자의 브라우저 hello 응용 프로그램 tooits의 hello URL이 추가 되었는지 확인 **신뢰할 수 있는 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="30345-115">Toocheck hello 응용 프로그램 인지 확인 **구성** 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="30345-116">Hello 사용자의 계정이 인지 확인 **활성화** 에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="30345-117">Hello 사용자의 계정이 인지 확인 **잠겨 있지 않으면입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="30345-118">있는지 hello 사용자 확인 **암호를 만료 하거나 잊어버린 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="30345-119">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="30345-120">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="30345-121">다음 사항을 확인 한 사용자의 **인증 연락처 정보** toodate tooallow Multi-factor Authentication 또는 조건부 액세스 정책 toobe 적용 중일 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="30345-122">확인 되었는지 tooalso try 브라우저의 쿠키를 지우고 toosign에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="30345-123">액세스 패널 hello에 대 한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="30345-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="30345-124">hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="30345-125">toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="30345-126">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="30345-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="30345-127">암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="30345-128">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="30345-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="30345-129">Windows 10 Anniversary Edition 이상 Edge</span><span class="sxs-lookup"><span data-stu-id="30345-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="30345-130">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="30345-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="30345-131">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="30345-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="30345-132">Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="30345-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="30345-133">아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="30345-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-134">열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="30345-135">클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="30345-136">Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="30345-137">브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="30345-138">**추가** hello 확장 tooyour 브라우저.</span><span class="sxs-lookup"><span data-stu-id="30345-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="30345-139">브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="30345-140">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="30345-141">Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="30345-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="30345-142">Hello 직접 링크 아래에서 Edge 및 Chrome에 대 한 hello 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="30345-143">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="30345-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="30345-144">Edge 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="30345-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="30345-145">Single sign on Azure AD 갤러리 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="30345-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="30345-146">Enterprise Single Sign-on 기능을 사용 하도록 설정 하는 hello Azure AD 갤러리에 있는 모든 응용 프로그램에는 단계별 자습서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="30345-147">Hello에 액세스할 수 있습니다 [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) 세부 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="30345-148">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="30345-149">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="30345-150">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="30345-151">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="30345-152">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="30345-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="30345-153">Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="30345-154">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="30345-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="30345-155">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="30345-156">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="30345-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-157">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="30345-158">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-159">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-160">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-161">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드</span><span class="sxs-lookup"><span data-stu-id="30345-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="30345-162">Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="30345-163">Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="30345-164">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="30345-165">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="30345-166">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="30345-167">Single sign on hello Azure AD 갤러리에서 응용 프로그램에 대 한 구성</span><span class="sxs-lookup"><span data-stu-id="30345-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="30345-168">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-170">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-171">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-172">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-173">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="30345-174">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-175">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="30345-176">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-177">선택 **SAML 기반 로그온** hello에서 **모드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="30345-178">필요한 hello 값을 입력 **도메인 및 Url입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="30345-179">Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="30345-180">SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="30345-181">일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="30345-182">IdP에서 시작한 SSO, hello 필수 값입니다. 회신 URL로 tooconfigure hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="30345-183">일부 응용 프로그램에 대 한 hello 식별자도 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="30345-184">**선택 사항:** 클릭 **고급 URL 설정 표시** toosee hello 선택적 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="30345-185">Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="30345-186">**선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="30345-187">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="30345-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="30345-188">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-188">click **Add attribute**.</span></span> <span data-ttu-id="30345-189">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="30345-190">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-190">Click **Save.**</span></span> <span data-ttu-id="30345-191">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30345-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="30345-192">클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="30345-193">또한 hello 메타 데이터 Url 및 hello 응용 프로그램과 함께 필요한 인증서 toosetup SSO에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="30345-194">클릭 **저장** toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="30345-195">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="30345-196">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="30345-197">tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="30345-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-198">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-199">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-200">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-201">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-202">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="30345-203">Hello를 사용 하 여 원하는 여기 tooshow hello 응용 프로그램을 표시 되지 않으면 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-204">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="30345-205">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-206">Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="30345-207">hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.</span><span class="sxs-lookup"><span data-stu-id="30345-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="30345-208">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="30345-209">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="30345-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="30345-210">tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="30345-211">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="30345-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="30345-212">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-212">click **Add attribute**.</span></span> <span data-ttu-id="30345-213">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="30345-214">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-214">Click **Save.**</span></span> <span data-ttu-id="30345-215">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30345-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="30345-216">Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="30345-217">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-218">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-219">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-220">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-221">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-222">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="30345-223">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-224">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="30345-225">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-226">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="30345-227">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="30345-228">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="30345-229">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="30345-230">Single sign on 갤러리가 아닌 응용 프로그램에 대 한 tooconfigure 페더레이션 하는 방법</span><span class="sxs-lookup"><span data-stu-id="30345-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="30345-231">toohave Azure AD premium이 필요 tooconfigure 갤러리가 아닌 응용 프로그램 및 hello 응용 프로그램이 SAML 2.0을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="30345-232">Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="30345-233">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="30345-234">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="30345-235">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="30345-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="30345-236">Hello 응용 프로그램 (로그온 URL, 발급자, 로그 아웃 URL 및 인증서)에 Azure AD 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="30345-237">Azure ad (로그온 URL, 식별자, 회신 URL) hello 응용 프로그램의 메타 데이터 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="30345-238">tooconfigure single sign on hello Azure AD 갤러리에 없는 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-239">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-240">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-241">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-242">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-243">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드</span><span class="sxs-lookup"><span data-stu-id="30345-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="30345-244">클릭 **비 갤러리 응용 프로그램** hello에 **위해 자신의 앱 추가** 섹션</span><span class="sxs-lookup"><span data-stu-id="30345-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="30345-245">Hello에 hello 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="30345-246">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="30345-247">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="30345-248">선택 **SAML 기반 로그온** hello에 **모드** 드롭다운</span><span class="sxs-lookup"><span data-stu-id="30345-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="30345-249">필요한 hello 값을 입력 **도메인 및 Url입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="30345-250">Hello 응용 프로그램 공급 업체에서 이러한 값을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="30345-251">IdP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 회신 URL hello 및 hello 식별자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="30345-252">**선택 사항:** SP에서 시작한 SSO와 tooconfigure hello 응용 프로그램 hello 로그인 URL에 필요한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="30345-253">Hello에 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="30345-254">**선택 사항:** 클릭 **보기 및 다른 모든 사용자 특성 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="30345-255">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="30345-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="30345-256">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-256">click **Add attribute**.</span></span> <span data-ttu-id="30345-257">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="30345-258">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-258">Click **Save.**</span></span> <span data-ttu-id="30345-259">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30345-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="30345-260">클릭 **구성 &lt;응용 프로그램 이름&gt;**  방법은 tooaccess 설명서 tooconfigure single sign on hello 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="30345-261">또한 Azure AD Url 및 hello 응용 프로그램에 필요한 인증서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="30345-262">사용자의 Id를 선택 하 고 사용자 특성 전송 toobe toohello 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="30345-263">tooselect hello 사용자 식별자 또는 사용자 특성 추가, 아래의 hello 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="30345-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-264">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-265">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-266">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-267">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-268">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="30345-269">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-270">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="30345-271">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-272">Hello에서 **사용자 특성** 섹션에서 사용자 hello에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="30345-273">hello 선택된 된 옵션 두어야 hello 응용 프로그램 tooauthenticate hello 사용자에서 toomatch hello 예상 값.</span><span class="sxs-lookup"><span data-stu-id="30345-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="30345-274">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="30345-275">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="30345-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="30345-276">tooadd 사용자 특성을 클릭 하 여 **보기 및 다른 모든 사용자 특성을 편집** tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="30345-277">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="30345-277">tooadd an attribute:</span></span>

   <span data-ttu-id="30345-278">1. **특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-278">1.click **Add attribute**.</span></span> <span data-ttu-id="30345-279">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="30345-280">2. **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-280">2 Click **Save.**</span></span> <span data-ttu-id="30345-281">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30345-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="30345-282">Hello Azure AD 메타 데이터 또는 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="30345-283">toodownload hello에 대 한 응용 프로그램 메타 데이터 또는 Azure AD에서 인증서를 다음 hello 단계를 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-284">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-285">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-286">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-287">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-288">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="30345-289">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-290">Single sign on 구성한 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="30345-291">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-292">너무 이동**SAML 서명 인증서** 섹션에서 다음 클릭 **다운로드** 열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="30345-293">어떤 hello 응용 프로그램에 single sign-on 구성 필요한 경우에 따라 메타 데이터 XML hello 또는 인증서를 환영 hello 옵션 toodownload를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="30345-294">Azure AD URL tooget hello 메타 데이터를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="30345-295">hello 메타 데이터를 XML 파일로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="30345-296">Azure AD 갤러리 응용 프로그램에 대 한 sign-on tooconfigure 암호 single 방법</span><span class="sxs-lookup"><span data-stu-id="30345-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="30345-297">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="30345-298">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="30345-299">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="30345-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="30345-300">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="30345-301">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="30345-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-302">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="30345-303">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-304">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-305">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-306">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드</span><span class="sxs-lookup"><span data-stu-id="30345-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="30345-307">Hello에 **이름을 입력** hello에서 textbox **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름</span><span class="sxs-lookup"><span data-stu-id="30345-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="30345-308">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="30345-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="30345-309">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="30345-310">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="30345-311">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="30345-312">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="30345-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="30345-313">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-314">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-315">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-316">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-317">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-318">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="30345-319">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-320">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="30345-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="30345-321">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-322">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="30345-323">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="30345-324">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="30345-325">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="30345-326">Tooconfigure 암호 로그온 갤러리가 아닌 응용 프로그램에 대 한 단일 하는 방법</span><span class="sxs-lookup"><span data-stu-id="30345-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="30345-327">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="30345-328">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="30345-329">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="30345-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="30345-330">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="30345-330">Add a non-gallery application</span></span>

<span data-ttu-id="30345-331">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="30345-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-332">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="30345-333">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-334">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-335">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-336">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드</span><span class="sxs-lookup"><span data-stu-id="30345-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="30345-337">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="30345-338">Hello에 응용 프로그램의 hello 이름을 입력 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="30345-339">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-339">Select **Add.**</span></span>

<span data-ttu-id="30345-340">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="30345-341">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="30345-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="30345-342">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-343">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="30345-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="30345-344">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-345">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-346">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-347">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="30345-348">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-349">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="30345-350">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-351">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="30345-352">Hello 입력 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="30345-353">사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="30345-354">Hello 로그인 필드 hello URL에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="30345-355">Toohello 응용 프로그램 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="30345-356">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="30345-357">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="30345-358">어떻게 tooassign 사용자 tooan 응용 프로그램을 직접</span><span class="sxs-lookup"><span data-stu-id="30345-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="30345-359">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="30345-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="30345-360">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="30345-361">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30345-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="30345-362">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="30345-363">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="30345-364">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="30345-365">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="30345-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="30345-366">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="30345-367">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="30345-368">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="30345-369">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="30345-370">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="30345-371">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="30345-372">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="30345-373">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="30345-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="30345-374">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="30345-375">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="30345-376">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="30345-377">짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="30345-378">이러한 문제 해결 단계 hello 하지 않는 경우 hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="30345-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="30345-379">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30345-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="30345-380">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="30345-380">Correlation error ID</span></span>

-   <span data-ttu-id="30345-381">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="30345-381">UPN (user email address)</span></span>

-   <span data-ttu-id="30345-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="30345-382">TenantID</span></span>

-   <span data-ttu-id="30345-383">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="30345-383">Browser type</span></span>

-   <span data-ttu-id="30345-384">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="30345-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="30345-385">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="30345-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="30345-386">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30345-386">Next steps</span></span>
[<span data-ttu-id="30345-387">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="30345-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

