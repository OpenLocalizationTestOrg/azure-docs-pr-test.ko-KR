---
title: "tooan 페더레이션에 대해 구성 된 Azure AD 갤러리 응용 프로그램 로그인 aaaProblems single sign on | Microsoft Docs"
description: "암호 single sign on에 대해 구성 된 Azure AD 갤러리 응용 프로그램과 tootroubleshoot 발급 하는 방법"
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="ca1df-103">Tooan 페더레이션된 single sign-on에 대해 구성 된 Azure AD 갤러리 응용 프로그램에에서 로그인 하는 문제</span><span class="sxs-lookup"><span data-stu-id="ca1df-103">Problems signing in tooan Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="ca1df-104">액세스 패널 hello 활성화 있는 사용자가 회사 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 관리자에 게 Azure AD는 웹 기반 포털이 부여 해 준에 대 한 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="ca1df-105">Azure AD 버전을 가진 사용자는 셀프 서비스 그룹 및 hello 액세스 패널을 통해 응용 프로그램 관리 기능 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="ca1df-106">액세스 패널 hello는 hello Azure 포털에서에서 분리 되 고 사용자가 toohave Azure 구독이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="ca1df-107">toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="ca1df-108">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="ca1df-109">액세스 패널 hello에 대 한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="ca1df-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="ca1df-110">hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="ca1df-111">toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="ca1df-112">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="ca1df-113">암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="ca1df-114">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="ca1df-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="ca1df-115">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="ca1df-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="ca1df-116">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="ca1df-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="ca1df-117">hello 암호 기반 SSO 확장 브라우저 확장 될 지에 대해 지원 되는 경우 Windows 10에서에 지에 대해 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="ca1df-118">Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ca1df-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="ca1df-119">아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="ca1df-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="ca1df-120">열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="ca1df-121">클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="ca1df-122">Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="ca1df-123">브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="ca1df-124">**추가** hello 확장 tooyour 브라우저.</span><span class="sxs-lookup"><span data-stu-id="ca1df-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="ca1df-125">브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="ca1df-126">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="ca1df-127">Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ca1df-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="ca1df-128">Hello 직접 링크 아래에서 Chrome 및 Firefox에 대 한 hello 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="ca1df-129">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="ca1df-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="ca1df-130">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="ca1df-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="ca1df-131">Internet Explorer에 대한 그룹 정책 설정</span><span class="sxs-lookup"><span data-stu-id="ca1df-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="ca1df-132">할 수 있도록 tooremotely 설치 hello 액세스 패널 확장 Internet Explorer에 대 한 사용자의 컴퓨터에서 그룹 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="ca1df-133">hello 필수 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="ca1df-134">설정한 후 [Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), 사용자의 컴퓨터 tooyour 도메인에 가입한 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="ca1df-135">Hello "설정 편집" 권한이 tooedit hello 그룹 정책 개체 (GPO) 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="ca1df-136">기본적으로 hello 다음 보안 그룹의 멤버는이 권한이 있는: Domain Administrators, 엔터프라이즈 관리자 및 Group Policy Creator Owners 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="ca1df-137">[자세히 알아봅니다](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca1df-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="ca1df-138">Hello 자습서에 따라 [tooDeploy 그룹 정책을 사용 하 여 Internet Explorer에 대 한 액세스 패널 확장을 hello 하는 방법을](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) tooconfigure hello 그룹 정책 하 고 toousers 배포 하는 방법에 대 한 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="ca1df-139">Internet Explorer에서 액세스 패널 hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ca1df-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="ca1df-140">Hello에 따라 [문제 해결 hello Internet Explorer에 대 한 액세스 패널 확장이](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) IE hello 확장 구성에 액세스에 대 한 진단 도구 및 단계별 지침 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="ca1df-141">Azure AD 갤러리 응용 프로그램에 대 한 sign-on tooconfigure 암호 single 방법</span><span class="sxs-lookup"><span data-stu-id="ca1df-141">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="ca1df-142">tooconfigure hello Azure AD 갤러리에서 응용 프로그램 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ca1df-143">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ca1df-143">Add an application from hello Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="ca1df-144">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ca1df-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="ca1df-145">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="ca1df-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="ca1df-146">Hello Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ca1df-146">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="ca1df-147">아래의 hello 단계를 수행 하는 tooadd hello Azure AD 갤러리에서에서 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="ca1df-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ca1df-148">열기 hello [Azure 포털](https://portal.azure.com) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="ca1df-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ca1df-149">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca1df-150">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca1df-151">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca1df-152">hello 클릭 **추가** hello hello 오른쪽 위 모서리에 있는 단추 **엔터프라이즈 응용 프로그램** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="ca1df-153">Hello에 **이름을 입력** hello에서 텍스트 상자에 붙여넣습니다 **hello 갤러리에서 추가** 섹션, hello 응용 프로그램의 형식 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-153">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="ca1df-154">Single sign on tooconfigure 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-154">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="ca1df-155">Hello 응용 프로그램을 추가 하기 전에 hello에서 이름을 변경할 수 **이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-155">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="ca1df-156">클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-156">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="ca1df-157">짧은 시간 후 수 toosee hello 응용 프로그램의 구성 블레이드에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-157">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ca1df-158">암호 single sign on에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ca1df-158">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ca1df-159">tooconfigure single sign on 응용 프로그램에 대 한 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-159">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ca1df-160">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="ca1df-160">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ca1df-161">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-161">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca1df-162">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-162">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca1df-163">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-163">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca1df-164">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-164">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ca1df-165">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ca1df-165">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ca1df-166">Hello 응용 프로그램 선택 tooconfigure single sign on</span><span class="sxs-lookup"><span data-stu-id="ca1df-166">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="ca1df-167">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-167">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ca1df-168">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ca1df-168">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ca1df-169">[Toohello 응용 프로그램 사용자를 할당](#_How_to_assign)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-169">[Assign users toohello application](#_How_to_assign).</span></span>

10. <span data-ttu-id="ca1df-170">Hello 사용자의 hello 행을 선택 하 고를 클릭 하 여 hello 사용자 대신 자격 증명도 제공할 수 또한 **업데이트 자격 증명** hello 사용자를 대신해 서 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-170">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ca1df-171">그렇지 않은 경우 사용자 수 증명된 tooenter hello 자격 증명 자체 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-171">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="ca1df-172">사용자가 toohello 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="ca1df-172">Assign users toohello application</span></span>

<span data-ttu-id="ca1df-173">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="ca1df-173">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ca1df-174">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="ca1df-174">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ca1df-175">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-175">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ca1df-176">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-176">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ca1df-177">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-177">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ca1df-178">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-178">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="ca1df-179">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="ca1df-179">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ca1df-180">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-180">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ca1df-181">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-181">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ca1df-182">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-182">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ca1df-183">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-183">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ca1df-184">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-184">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ca1df-185">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-185">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ca1df-186">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-186">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ca1df-187">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-187">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="ca1df-188">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-188">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ca1df-189">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-189">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="ca1df-190">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-190">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="ca1df-191">짧은 기간 hello 사용자가 선택한 수 수 toolaunch에서 이러한 응용 프로그램 액세스 패널 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-191">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a><span data-ttu-id="ca1df-192">단계는 hello 문제가 해결 되지 않으면 이러한 문제를 해결 하는 경우</span><span class="sxs-lookup"><span data-stu-id="ca1df-192">If these troubleshoot steps don't resolve hello issue</span></span> 
<span data-ttu-id="ca1df-193">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-193">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="ca1df-194">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="ca1df-194">Correlation error ID</span></span>

-   <span data-ttu-id="ca1df-195">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="ca1df-195">UPN (user email address)</span></span>

-   <span data-ttu-id="ca1df-196">TenantID</span><span class="sxs-lookup"><span data-stu-id="ca1df-196">TenantID</span></span>

-   <span data-ttu-id="ca1df-197">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="ca1df-197">Browser type</span></span>

-   <span data-ttu-id="ca1df-198">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="ca1df-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="ca1df-199">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="ca1df-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca1df-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca1df-200">Next steps</span></span>
[<span data-ttu-id="ca1df-201">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca1df-201">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
