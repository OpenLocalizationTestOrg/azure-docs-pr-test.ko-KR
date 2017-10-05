---
title: "암호 Single Sign-On에 대해 구성된 Azure AD 갤러리 응용 프로그램에 로그인하는 문제 | Microsoft Docs"
description: "암호 Single Sign-On에 대해 구성된 Azure AD 갤러리 응용 프로그램에 로그인하는 것과 관련된 문제를 해결하는 지침을 제공하는 문제 영역을 설명합니다."
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="6b669-103">암호 Single Sign-On에 대해 구성된 Azure AD 갤러리 응용 프로그램에 로그인하는 문제</span><span class="sxs-lookup"><span data-stu-id="6b669-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="6b669-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여 받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="6b669-105">또한 Azure AD 버전의 사용자는 액세스 패널을 통해 셀프 서비스 그룹 및 앱 관리 기능을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="6b669-106">액세스 패널은 Azure Portal과 별개이며, 사용자에게 Azure 구독을 요구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="6b669-107">액세스 패널에서 암호 기반 SSO(Single Sign-On)를 사용하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="6b669-108">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="6b669-109">액세스 패널에 대한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="6b669-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="6b669-110">액세스 패널에는 JavaScript를 지원하고 CSS를 사용하도록 설정한 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="6b669-111">액세스 패널에서 암호 기반 SSO(Single Sign-On)를 사용하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="6b669-112">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="6b669-113">암호 기반 SSO의 경우 최종 사용자 브라우저는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="6b669-114">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="6b669-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="6b669-115">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="6b669-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="6b669-116">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="6b669-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="6b669-117">브라우저 확장이 Edge에서 지원되는 경우 Windows 10의 Edge에 암호 기반 SSO 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="6b669-118">액세스 패널 브라우저 확장을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="6b669-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="6b669-119">액세스 패널 브라우저 확장을 설치하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="6b669-120">지원되는 브라우저 중 하나에서 [액세스 패널](https://myapps.microsoft.com)을 열고 Azure AD에서 **사용자**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="6b669-121">액세스 패널에서 **암호-SSO 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="6b669-122">소프트웨어를 설치하라는 프롬프트에서 **지금 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="6b669-123">브라우저에 따라 다운로드 링크로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="6b669-124">브라우저에 확장을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="6b669-125">브라우저에서 요청하면 확장을 **사용** 또는 **허용**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="6b669-126">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="6b669-127">액세스 패널에 로그인하고 암호 SSO 응용 프로그램을 **시작**할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="6b669-128">아래와 같은 직접 링크에서 Chrome 및 Firefox에 대한 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="6b669-129">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="6b669-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="6b669-130">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="6b669-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="6b669-131">Internet Explorer에 대한 그룹 정책 설정</span><span class="sxs-lookup"><span data-stu-id="6b669-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="6b669-132">사용자의 컴퓨터에 Internet Explorer용 액세스 패널 확장을 원격으로 설치할 수 있는 그룹 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="6b669-133">필수 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-133">The prerequisites include:</span></span>

-   <span data-ttu-id="6b669-134">[Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)를 설정하고, 사용자 컴퓨터를 도메인에 가입시킨 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="6b669-135">그룹 정책 개체(GPO)를 편집하는 "설정 편집" 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="6b669-136">기본적으로 도메인 관리자, 엔터프라이즈 관리자 및 그룹 정책 작성자/소유자 보안 그룹의 멤버에게 이 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="6b669-137">[자세히 알아보기](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b669-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="6b669-138">자습서에 따라 그룹 정책을 구성하고 사용자에게 배포하는 방법에 대한 단계별 지침은 [그룹 정책을 사용하여 Internet Explorer용 액세스 패널 확장을 배포하는 방법](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="6b669-139">Internet Explorer에서 액세스 패널 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6b669-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="6b669-140">진단 도구 및 IE용 확장을 구성하는 방법에 대한 단계별 지침에 액세스하려면 [Internet Explorer의 액세스 패널 확장 문제 해결](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) 가이드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="6b669-141">비갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="6b669-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="6b669-142">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="6b669-143">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="6b669-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="6b669-144">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="6b669-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="6b669-145">응용 프로그램에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6b669-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="6b669-146">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="6b669-146">Add a non-gallery application</span></span>

<span data-ttu-id="6b669-147">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="6b669-148">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="6b669-149">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6b669-150">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6b669-151">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6b669-152">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="6b669-153">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="6b669-154">**이름** 텍스트 상자에 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="6b669-155">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-155">Select **Add.**</span></span>

<span data-ttu-id="6b669-156">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="6b669-157">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="6b669-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="6b669-158">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="6b669-159">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="6b669-160">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6b669-161">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6b669-162">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6b669-163">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="6b669-164">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6b669-165">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="6b669-166">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6b669-167">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="6b669-168">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="6b669-169">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="6b669-170">URL에서 로그인 필드가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="6b669-171">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-171">Assign users to the application.</span></span>

11. <span data-ttu-id="6b669-172">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="6b669-173">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="6b669-174">응용 프로그램에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="6b669-174">Assign users to the application</span></span>

<span data-ttu-id="6b669-175">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="6b669-176">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6b669-177">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6b669-178">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6b669-179">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6b669-180">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="6b669-181">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6b669-182">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="6b669-183">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6b669-184">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="6b669-185">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="6b669-186">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="6b669-187">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="6b669-188">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="6b669-189">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="6b669-190">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="6b669-191">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="6b669-192">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="6b669-193">짧은 시간 후에 선택한 사용자는 액세스 패널에서 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="6b669-194">이러한 문제 해결 단계가 문제를 해결하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="6b669-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="6b669-195">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b669-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="6b669-196">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="6b669-196">Correlation error ID</span></span>

-   <span data-ttu-id="6b669-197">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="6b669-197">UPN (user email address)</span></span>

-   <span data-ttu-id="6b669-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="6b669-198">TenantID</span></span>

-   <span data-ttu-id="6b669-199">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="6b669-199">Browser type</span></span>

-   <span data-ttu-id="6b669-200">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="6b669-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="6b669-201">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="6b669-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b669-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b669-202">Next steps</span></span>
[<span data-ttu-id="6b669-203">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="6b669-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

