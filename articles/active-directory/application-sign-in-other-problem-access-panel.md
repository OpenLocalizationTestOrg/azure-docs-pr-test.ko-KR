---
title: "액세스 패널의 응용 프로그램에 로그인하는 문제 | Microsoft Docs"
description: "myapps.microsoft.com의 Microsoft Azure AD 액세스 패널에서 응용 프로그램에 액세스하는 문제를 해결하는 방법"
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
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="dc1bf-103">액세스 패널의 응용 프로그램에 로그인하는 문제</span><span class="sxs-lookup"><span data-stu-id="dc1bf-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="dc1bf-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여 받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="dc1bf-105">이러한 응용 프로그램은 Azure AD 포털에서 사용자를 대신하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="dc1bf-106">응용 프로그램을 액세스 패널에 표시하려면 응용 프로그램이 올바르게 구성되어 있고, 사용자나 그 사용자가 속한 그룹에 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="dc1bf-107">사용자가 볼 수 있는 앱의 종류는 다음과 같은 범주로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="dc1bf-108">Office 365 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="dc1bf-108">Office 365 Applications</span></span>

-   <span data-ttu-id="dc1bf-109">페더레이션 기반 SSO로 구성된 Microsoft 및 타사 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="dc1bf-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="dc1bf-110">암호 기반 SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="dc1bf-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="dc1bf-111">기존 SSO 솔루션을 사용한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="dc1bf-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="dc1bf-112">먼저 확인해야 할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="dc1bf-112">General issues to check first</span></span>

-   <span data-ttu-id="dc1bf-113">액세스 패널에 대한 최소 요구 사항을 충족하는 **브라우저**를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="dc1bf-114">사용자의 브라우저에서 해당 **신뢰할 수 있는 사이트**에 응용 프로그램의 URL을 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="dc1bf-115">응용 프로그램이 올바르게 **구성**되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="dc1bf-116">사용자의 계정이 로그인에 대해 **활성화**되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="dc1bf-117">사용자의 계정이 **잠겨 있지 않는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="dc1bf-118">사용자의 **암호가 만료되거나 기억하지 못하는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="dc1bf-119">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="dc1bf-120">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="dc1bf-121">사용자의 **인증 연락처 정보**를 최신으로 유지하여 Multi-Factor Authentication 또는 조건부 액세스 정책을 적용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="dc1bf-122">브라우저의 쿠키를 지우고 다시 로그인하려고 시도할 수도 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="dc1bf-123">액세스 패널에 대한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="dc1bf-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="dc1bf-124">액세스 패널에는 JavaScript를 지원하고 CSS를 사용하도록 설정한 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="dc1bf-125">액세스 패널에서 암호 기반 SSO(Single Sign-On)를 사용하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="dc1bf-126">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="dc1bf-127">암호 기반 SSO의 경우 최종 사용자 브라우저는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="dc1bf-128">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="dc1bf-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="dc1bf-129">Windows 10 Anniversary Edition 이상 Edge</span><span class="sxs-lookup"><span data-stu-id="dc1bf-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="dc1bf-130">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="dc1bf-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="dc1bf-131">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="dc1bf-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="dc1bf-132">액세스 패널 브라우저 확장을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="dc1bf-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="dc1bf-133">액세스 패널 브라우저 확장을 설치하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-134">지원되는 브라우저 중 하나에서 [액세스 패널](https://myapps.microsoft.com)을 열고 Azure AD에서 **사용자**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="dc1bf-135">액세스 패널에서 **암호-SSO 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="dc1bf-136">소프트웨어를 설치하라는 프롬프트에서 **지금 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="dc1bf-137">브라우저에 따라 다운로드 링크로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="dc1bf-138">브라우저에 확장을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="dc1bf-139">브라우저에서 요청하면 확장을 **사용** 또는 **허용**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="dc1bf-140">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="dc1bf-141">액세스 패널에 로그인하고 암호 SSO 응용 프로그램을 **시작**할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="dc1bf-142">아래와 같은 직접 링크에서 Chrome 및 Edge에 대한 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="dc1bf-143">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="dc1bf-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="dc1bf-144">Edge 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="dc1bf-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="dc1bf-145">Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="dc1bf-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="dc1bf-146">Azure AD 갤러리에서 Enterprise Single Sign-On 기능을 사용하도록 설정된 모든 응용 프로그램은 단계별 자습서를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="dc1bf-147">[Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)에 액세스하면 자세한 단계별 지침을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="dc1bf-148">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="dc1bf-149">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="dc1bf-150">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="dc1bf-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="dc1bf-151">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="dc1bf-152">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="dc1bf-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="dc1bf-153">응용 프로그램에서 Azure AD 메타데이터 값 구성(로그온 URL, 발급자, 로그아웃 URL 및 인증서)</span><span class="sxs-lookup"><span data-stu-id="dc1bf-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="dc1bf-154">응용 프로그램에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="dc1bf-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="dc1bf-155">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="dc1bf-156">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-157">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="dc1bf-158">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-159">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-160">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-161">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="dc1bf-162">**갤러리에서 추가** 섹션의 **이름 입력** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="dc1bf-163">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="dc1bf-164">응용 프로그램을 추가하기 전에 **이름** 텍스트 상자에서 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="dc1bf-165">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="dc1bf-166">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="dc1bf-167">Azure AD 갤러리에서 응용 프로그램의 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="dc1bf-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="dc1bf-168">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-170">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-171">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-172">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-173">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dc1bf-174">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-175">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="dc1bf-176">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-177">**모드** 드롭다운에서 **SAML 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="dc1bf-178">**도메인 및 URL**에 필요한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="dc1bf-179">이러한 값은 응용 프로그램 공급업체에서 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="dc1bf-180">응용 프로그램을 SP에서 시작한 SSO로 구성하려면 로그온 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="dc1bf-181">일부 응용 프로그램의 경우는 식별자도 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="dc1bf-182">응용 프로그램을 IdP에서 시작한 SSO로 구성하려면 회신 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="dc1bf-183">일부 응용 프로그램의 경우는 식별자도 필수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="dc1bf-184">**선택 사항:** 선택적인 값을 보려면 **고급 URL 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="dc1bf-185">**사용자 특성**의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="dc1bf-186">**선택 사항:** 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="dc1bf-187">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="dc1bf-187">To add an attribute:</span></span>

   1. <span data-ttu-id="dc1bf-188">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-188">click **Add attribute**.</span></span> <span data-ttu-id="dc1bf-189">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="dc1bf-190">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-190">Click **Save.**</span></span> <span data-ttu-id="dc1bf-191">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="dc1bf-192">응용 프로그램의 Single Sign-On을 구성하는 방법에 관한 문서에 액세스하려면 **&lt;응용 프로그램 이름&gt; 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="dc1bf-193">또한 응용 프로그램에 SSO를 설정하는 데 필요한 메타데이터 URL 및 인증서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="dc1bf-194">구성을 저장하려면 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="dc1bf-195">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="dc1bf-196">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="dc1bf-197">사용자 식별자를 선택하거나 사용자 특성을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-198">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-199">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-200">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-201">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-202">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dc1bf-203">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-204">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="dc1bf-205">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-206">**사용자 특성** 섹션 아래의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="dc1bf-207">사용자를 인증하려면 선택한 옵션이 응용 프로그램의 예상 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="dc1bf-208">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="dc1bf-209">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="dc1bf-210">사용자 특성을 추가하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭하여 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="dc1bf-211">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="dc1bf-211">To add an attribute:</span></span>

   1. <span data-ttu-id="dc1bf-212">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-212">click **Add attribute**.</span></span> <span data-ttu-id="dc1bf-213">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="dc1bf-214">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-214">Click **Save.**</span></span> <span data-ttu-id="dc1bf-215">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="dc1bf-216">Azure AD 메타데이터 또는 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="dc1bf-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="dc1bf-217">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-218">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-219">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-220">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-221">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-222">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dc1bf-223">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-224">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="dc1bf-225">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-226">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="dc1bf-227">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="dc1bf-228">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="dc1bf-229">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="dc1bf-230">비갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="dc1bf-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="dc1bf-231">비갤러리 응용 프로그램을 구성하려면 Azure AD 프리미엄이 있어야 하며 응용 프로그램에서 SAML 2.0을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="dc1bf-232">Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="dc1bf-233">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="dc1bf-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="dc1bf-234">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="dc1bf-235">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="dc1bf-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="dc1bf-236">응용 프로그램에서 Azure AD 메타데이터 값 구성(로그온 URL, 발급자, 로그아웃 URL 및 인증서)</span><span class="sxs-lookup"><span data-stu-id="dc1bf-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="dc1bf-237">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="dc1bf-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="dc1bf-238">Azure AD 갤러리에 없는 응용 프로그램에 대해 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-239">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-240">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-241">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-242">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-243">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="dc1bf-244">**고유한 응용 프로그램 추가** 섹션에서 **비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="dc1bf-245">**이름** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="dc1bf-246">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="dc1bf-247">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="dc1bf-248">**모드** 드롭다운에서 **SAML 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="dc1bf-249">**도메인 및 URL**에 필요한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="dc1bf-250">이러한 값은 응용 프로그램 공급업체에서 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="dc1bf-251">응용 프로그램을 IdP에서 시작한 SSO로 구성하려면 회신 URL과 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="dc1bf-252">**선택 사항:** 응용 프로그램을 SP에서 시작한 SSO로 구성하려면 로그온 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="dc1bf-253">**사용자 특성**의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="dc1bf-254">**선택 사항:** 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="dc1bf-255">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="dc1bf-255">To add an attribute:</span></span>

   1. <span data-ttu-id="dc1bf-256">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-256">click **Add attribute**.</span></span> <span data-ttu-id="dc1bf-257">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="dc1bf-258">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-258">Click **Save.**</span></span> <span data-ttu-id="dc1bf-259">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="dc1bf-260">응용 프로그램의 Single Sign-On을 구성하는 방법에 관한 문서에 액세스하려면 **&lt;응용 프로그램 이름&gt; 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="dc1bf-261">또한 응용 프로그램에 필요한 Azure AD URL과 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="dc1bf-262">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="dc1bf-263">사용자 식별자를 선택하거나 사용자 특성을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-264">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-265">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-266">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-267">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-268">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dc1bf-269">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-270">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="dc1bf-271">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-272">**사용자 특성** 섹션 아래의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="dc1bf-273">사용자를 인증하려면 선택한 옵션이 응용 프로그램의 예상 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dc1bf-274">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="dc1bf-275">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="dc1bf-276">사용자 특성을 추가하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭하여 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="dc1bf-277">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="dc1bf-277">To add an attribute:</span></span>

   <span data-ttu-id="dc1bf-278">1. **특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-278">1.click **Add attribute**.</span></span> <span data-ttu-id="dc1bf-279">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="dc1bf-280">2. **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-280">2 Click **Save.**</span></span> <span data-ttu-id="dc1bf-281">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="dc1bf-282">Azure AD 메타데이터 또는 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="dc1bf-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="dc1bf-283">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-284">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-285">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-286">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-287">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-288">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="dc1bf-289">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-290">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="dc1bf-291">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-292">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="dc1bf-293">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="dc1bf-294">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="dc1bf-295">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="dc1bf-296">Azure AD 갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="dc1bf-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="dc1bf-297">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="dc1bf-298">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="dc1bf-299">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="dc1bf-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="dc1bf-300">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="dc1bf-301">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-302">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="dc1bf-303">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-304">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-305">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-306">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="dc1bf-307">**갤러리에서 추가** 섹션의 **이름 입력** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="dc1bf-308">Single Sign-On을 구성하려는 응용 프로그램 선택</span><span class="sxs-lookup"><span data-stu-id="dc1bf-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="dc1bf-309">응용 프로그램을 추가하기 전에 **이름** 텍스트 상자에서 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="dc1bf-310">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="dc1bf-311">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="dc1bf-312">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="dc1bf-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="dc1bf-313">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-314">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-315">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-316">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-317">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-318">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="dc1bf-319">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-320">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="dc1bf-321">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-322">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="dc1bf-323">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-323">Assign users to the application.</span></span>

10. <span data-ttu-id="dc1bf-324">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="dc1bf-325">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="dc1bf-326">비갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="dc1bf-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="dc1bf-327">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="dc1bf-328">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="dc1bf-329">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="dc1bf-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="dc1bf-330">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="dc1bf-330">Add a non-gallery application</span></span>

<span data-ttu-id="dc1bf-331">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-332">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="dc1bf-333">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-334">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-335">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-336">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="dc1bf-337">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="dc1bf-338">**이름** 텍스트 상자에 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="dc1bf-339">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-339">Select **Add.**</span></span>

<span data-ttu-id="dc1bf-340">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="dc1bf-341">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="dc1bf-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="dc1bf-342">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-343">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc1bf-344">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-345">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-346">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-347">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="dc1bf-348">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-349">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="dc1bf-350">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-351">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="dc1bf-352">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="dc1bf-353">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="dc1bf-354">URL에서 로그인 필드가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="dc1bf-355">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-355">Assign users to the application.</span></span>

11. <span data-ttu-id="dc1bf-356">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="dc1bf-357">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="dc1bf-358">응용 프로그램에 사용자를 직접 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="dc1bf-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="dc1bf-359">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="dc1bf-360">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="dc1bf-361">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc1bf-362">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc1bf-363">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc1bf-364">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dc1bf-365">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dc1bf-366">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="dc1bf-367">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc1bf-368">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="dc1bf-369">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="dc1bf-370">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="dc1bf-371">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="dc1bf-372">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="dc1bf-373">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="dc1bf-374">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="dc1bf-375">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="dc1bf-376">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="dc1bf-377">짧은 시간 후에 선택한 사용자는 액세스 패널에서 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="dc1bf-378">이러한 문제 해결 단계가 문제를 해결하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="dc1bf-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="dc1bf-379">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc1bf-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="dc1bf-380">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="dc1bf-380">Correlation error ID</span></span>

-   <span data-ttu-id="dc1bf-381">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="dc1bf-381">UPN (user email address)</span></span>

-   <span data-ttu-id="dc1bf-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="dc1bf-382">TenantID</span></span>

-   <span data-ttu-id="dc1bf-383">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="dc1bf-383">Browser type</span></span>

-   <span data-ttu-id="dc1bf-384">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="dc1bf-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="dc1bf-385">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="dc1bf-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc1bf-386">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc1bf-386">Next steps</span></span>
[<span data-ttu-id="dc1bf-387">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="dc1bf-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

