---
title: "딥 링크를 사용하여 응용 프로그램에 로그인하는 문제 | Microsoft Docs"
description: "Azure AD를 사용하여 딥 링크 URL에서 응용 프로그램에 액세스하는 문제를 해결하는 방법"
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="4b79f-103">딥 링크를 사용하여 응용 프로그램에 로그인하는 문제</span><span class="sxs-lookup"><span data-stu-id="4b79f-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="4b79f-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여 받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="4b79f-105">이러한 응용 프로그램은 Azure AD 포털에서 사용자를 대신하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="4b79f-106">응용 프로그램을 액세스 패널에 표시하려면 응용 프로그램이 올바르게 구성되어 있고, 사용자나 그 사용자가 속한 그룹에 할당되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="4b79f-107">딥 링크 또는 사용자 액세스 URL은 사용자가 해당 브라우저 URL 막대에서 직접 암호 SSO 응용 프로그램에 액세스하는 데 사용할 수 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="4b79f-108">사용자는 이 링크로 이동하여 액세스 패널로 이동하지 않고도 응용 프로그램에 자동으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="4b79f-109">사용자는 동일한 링크를 Office 365 응용 프로그램 실행 프로그램에서 이러한 응용 프로그램에 액세스하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="4b79f-110">먼저 확인해야 할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="4b79f-110">General issues to check first</span></span>

-   <span data-ttu-id="4b79f-111">액세스 패널에 대한 최소 요구 사항을 충족하는 **브라우저**를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="4b79f-112">사용자의 브라우저에서 해당 **신뢰할 수 있는 사이트**에 응용 프로그램의 URL을 추가했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="4b79f-113">응용 프로그램이 올바르게 **구성**되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="4b79f-114">사용자의 계정이 로그인에 대해 **활성화**되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="4b79f-115">사용자의 계정이 **잠겨 있지 않는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="4b79f-116">사용자의 **암호가 만료되거나 기억하지 못하는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="4b79f-117">**Multi-Factor Authentication**에서 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="4b79f-118">**조건부 액세스 정책** 또는 **ID 보호** 정책이 사용자 액세스를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="4b79f-119">사용자의 **인증 연락처 정보**를 최신으로 유지하여 Multi-Factor Authentication 또는 조건부 액세스 정책을 적용할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="4b79f-120">브라우저의 쿠키를 지우고 다시 로그인하려고 시도할 수도 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="4b79f-121">딥 링크 확인</span><span class="sxs-lookup"><span data-stu-id="4b79f-121">Checking the deeplink</span></span>

<span data-ttu-id="4b79f-122">올바른 딥 링크가 있는지 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-123">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4b79f-124">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b79f-125">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b79f-126">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b79f-127">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4b79f-128">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b79f-129">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="4b79f-130">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b79f-131">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="4b79f-132">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="4b79f-133">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4b79f-134">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="4b79f-135">딥 링크를 확인하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="4b79f-136">**사용자 액세스 URL** 레이블을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="4b79f-137">딥 링크가 URL과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="4b79f-138">액세스 패널 브라우저 확장을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b79f-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="4b79f-139">액세스 패널 브라우저 확장을 설치하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-140">지원되는 브라우저 중 하나에서 [액세스 패널](https://myapps.microsoft.com)을 열고 Azure AD에서 **사용자**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="4b79f-141">액세스 패널에서 **암호-SSO 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="4b79f-142">소프트웨어를 설치하라는 프롬프트에서 **지금 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="4b79f-143">브라우저에 따라 다운로드 링크로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="4b79f-144">브라우저에 확장을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="4b79f-145">브라우저에서 요청하면 확장을 **사용** 또는 **허용**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="4b79f-146">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="4b79f-147">액세스 패널에 로그인하고 암호 SSO 응용 프로그램을 **시작**할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="4b79f-148">아래와 같은 직접 링크에서 Chrome 및 Firefox에 대한 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="4b79f-149">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="4b79f-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="4b79f-150">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="4b79f-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4b79f-151">Azure AD 갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b79f-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4b79f-152">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4b79f-153">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="4b79f-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="4b79f-154">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="4b79f-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4b79f-155">Azure AD 갤러리에서 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="4b79f-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="4b79f-156">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-157">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="4b79f-158">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b79f-159">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b79f-160">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b79f-161">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4b79f-162">**갤러리에서 추가** 섹션의 **이름 입력** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="4b79f-163">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="4b79f-164">응용 프로그램을 추가하기 전에 **이름** 텍스트 상자에서 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="4b79f-165">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="4b79f-166">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="4b79f-167">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="4b79f-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="4b79f-168">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-169">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4b79f-170">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b79f-171">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b79f-172">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b79f-173">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4b79f-174">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b79f-175">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4b79f-176">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b79f-177">**암호 기반의 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4b79f-178">[응용 프로그램에 사용자를 할당합니다](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="4b79f-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="4b79f-179">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="4b79f-180">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4b79f-181">비갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b79f-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4b79f-182">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4b79f-183">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="4b79f-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="4b79f-184">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="4b79f-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="4b79f-185">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="4b79f-185">Add a non-gallery application</span></span>

<span data-ttu-id="4b79f-186">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-187">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="4b79f-188">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b79f-189">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b79f-190">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b79f-191">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="4b79f-192">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="4b79f-193">**이름** 텍스트 상자에 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="4b79f-194">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-194">Select **Add.**</span></span>

<span data-ttu-id="4b79f-195">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="4b79f-196">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="4b79f-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="4b79f-197">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-198">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4b79f-199">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b79f-200">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b79f-201">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b79f-202">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="4b79f-203">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b79f-204">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4b79f-205">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b79f-206">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4b79f-207">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="4b79f-208">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="4b79f-209">URL에서 로그인 필드가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="4b79f-210">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-210">Assign users to the application.</span></span>

11. <span data-ttu-id="4b79f-211">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="4b79f-212">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="4b79f-213">응용 프로그램에 사용자를 직접 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b79f-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="4b79f-214">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="4b79f-215">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4b79f-216">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4b79f-217">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4b79f-218">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4b79f-219">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4b79f-220">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4b79f-221">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="4b79f-222">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4b79f-223">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4b79f-224">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4b79f-225">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4b79f-226">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="4b79f-227">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="4b79f-228">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="4b79f-229">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="4b79f-230">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="4b79f-231">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="4b79f-232">짧은 시간 후에 선택한 사용자는 액세스 패널에서 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="4b79f-233">이러한 문제 해결 단계가 문제를 해결하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="4b79f-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="4b79f-234">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b79f-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="4b79f-235">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="4b79f-235">Correlation error ID</span></span>

-   <span data-ttu-id="4b79f-236">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="4b79f-236">UPN (user email address)</span></span>

-   <span data-ttu-id="4b79f-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="4b79f-237">TenantID</span></span>

-   <span data-ttu-id="4b79f-238">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="4b79f-238">Browser type</span></span>

-   <span data-ttu-id="4b79f-239">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="4b79f-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="4b79f-240">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="4b79f-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b79f-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b79f-241">Next steps</span></span>
[<span data-ttu-id="4b79f-242">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="4b79f-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
