---
title: "비갤러리 응용 프로그램에 대해 암호 Single Sign-On 구성 문제 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에 나열되지 않은 사용자 지정 비갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성할 때 발생하는 일반적인 문제 이해"
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
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="0e7e3-103">비갤러리 응용 프로그램에 대해 암호 Single Sign-On 구성 문제</span><span class="sxs-lookup"><span data-stu-id="0e7e3-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="0e7e3-104">이 문서는 비갤러리 응용 프로그램에 대해 **암호 Single Sign-On**을 구성할 때 발생하는 일반적인 문제를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="0e7e3-105">응용 프로그램에 대한 로그인 필드를 캡처하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e7e3-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="0e7e3-106">로그인 필드 캡처는 HTML 기반 로그인 페이지에 대해서만 지원되고 Flash나 기타 비HTML 기반 기술을 사용하는 로그인 페이지처럼 **비표준 로그인 페이지에 대해서는 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="0e7e3-107">두 가지 방법으로 사용자 지정 응용 프로그램에 대한 로그인 필드를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="0e7e3-108">자동 로그인 필드 캡처</span><span class="sxs-lookup"><span data-stu-id="0e7e3-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="0e7e3-109">수동 로그인 필드 캡처</span><span class="sxs-lookup"><span data-stu-id="0e7e3-109">Manual sign-in field capture</span></span>

<span data-ttu-id="0e7e3-110">**자동 로그인 필드 캡처**는 **사용자 이름 및 암호 입력에 대해 잘 알려진 DIV ID** 필드를 사용하는 경우 대부분의 HTML 기반 로그인 페이지에서 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="0e7e3-111">자동 로그인 필드 캡처는 페이지의 HTML을 스크랩하여 특정 기준과 일치하는 DIV ID를 찾은 다음 나중에 암호를 재생할 수 있도록 이 응용 프로그램에 대한 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="0e7e3-112">**수동 로그인 필드 캡처**는 응용 프로그램 **공급업체에서 로그인에 대해 사용되는 입력 필드에 레이블을 지정하지 않은** 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="0e7e3-113">또한 수동 로그인 필드 캡처는 **공급업체에서 자동으로 검색할 수 없는 여러 필드를 렌더링하는 경우**에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="0e7e3-114">해당 필드가 있는 페이지 위치를 알려주면 Azure AD에서는 로그인 페이지에 있는 많은 필드에 대해 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="0e7e3-115">일반적으로 **자동 로그인 필드 캡처가 작동하지 않는 경우 수동 옵션을 사용해 보는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="0e7e3-116">응용 프로그램에 대한 로그인 필드를 자동으로 캡처하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e7e3-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="0e7e3-117">**자동 로그인 필드 캡처**를 사용하여 응용 프로그램에 대한 **암호 기반 Single Sign-On**을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="0e7e3-118">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0e7e3-119">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0e7e3-120">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0e7e3-121">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0e7e3-122">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0e7e3-123">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0e7e3-124">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="0e7e3-125">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0e7e3-126">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="0e7e3-127">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="0e7e3-128">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="0e7e3-129">**제공하는 URL에서 로그인 필드가 표시되는지 확인합니다**.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="0e7e3-130">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="0e7e3-131">이렇게 하면 사용자 이름과 암호 입력 상자에 해당 URL을 자동으로 가져오고, Azure AD를 통해 액세스 패널 브라우저 확장을 사용하여 해당 응용 프로그램에 암호를 안전하게 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="0e7e3-132">응용 프로그램에 대한 로그인 필드를 수동으로 캡처하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e7e3-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="0e7e3-133">로그인 필드를 수동으로 캡처하려면 먼저 액세스 패널 브라우저 확장이 설치되어 있고 **inPrivate, incognito 또는 개인 모드에서 실행 중이 아니어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="0e7e3-134">브라우저 확장을 설치하려면 [액세스 패널 브라우저 확장을 설치하는 방법](#i-cannot-manually-detect-sign-in-fields-for-my-application) 섹션의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="0e7e3-135">**수동 로그인 필드 캡처**를 사용하여 응용 프로그램에 대한 **암호 기반 Single Sign-On**을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="0e7e3-136">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0e7e3-137">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0e7e3-138">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0e7e3-139">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0e7e3-140">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="0e7e3-141">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0e7e3-142">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="0e7e3-143">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0e7e3-144">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="0e7e3-145">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="0e7e3-146">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="0e7e3-147">**제공하는 URL에서 로그인 필드가 표시되는지 확인합니다**.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="0e7e3-148">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="0e7e3-149">이렇게 하면 사용자 이름과 암호 입력 상자에 해당 URL을 자동으로 가져오고, Azure AD를 통해 액세스 패널 브라우저 확장을 사용하여 해당 응용 프로그램에 암호를 안전하게 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="0e7e3-150">이 작업에 실패하는 경우 12단계를 계속하여 **수동 로그인 필드 캡처를 사용하도록 로그인 모드를 변경**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="0e7e3-151">**&lt;앱 이름&gt; 암호 Single Sign-On 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="0e7e3-152">**로그인 필드 수동 검색** 구성 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="0e7e3-153">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-153">Click **Ok**.</span></span>

15. <span data-ttu-id="0e7e3-154">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-154">Click **Save**.</span></span>

16. <span data-ttu-id="0e7e3-155">화면의 지시에 따라 액세스 패널을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="0e7e3-156">“해당 URL에서 로그인 필드를 찾을 수 없습니다” 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="0e7e3-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="0e7e3-157">로그인 필드 자동 검색에 실패하면 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="0e7e3-158">이 문제를 해결하려면 [응용 프로그램에 대한 로그인 필드를 수동으로 캡처하는 방법](#how-to-manually-capture-sign-in-fields-for-an-application) 섹션의 단계에 따라 수동 로그인 필드 검색을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="0e7e3-159">“Single Sign-On 구성을 저장할 수 없음” 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="0e7e3-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="0e7e3-160">드물지만 Single Sign-On 구성 업데이트에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="0e7e3-161">이 문제를 해결하려면 Single Sign-On 구성을 다시 저장해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="0e7e3-162">계속 실패하는 경우 지원 케이스를 열고 [포털 알림의 세부 정보를 확인하는 방법](#i-cannot-manually-detect-sign-in-fields-for-my-application) 및 [지원 엔지니어에게 알림 세부 정보를 전송하여 도움을 얻는 방법](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) 섹션에서 수집한 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="0e7e3-163">응용 프로그램에 대한 로그인 필드를 수동으로 검색할 수 없음</span><span class="sxs-lookup"><span data-stu-id="0e7e3-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="0e7e3-164">수동 검색이 작동하지 않을 때 표시되는 동작은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="0e7e3-165">수동 캡처 프로세스가 작동하는 것 같지만 캡처된 필드가 잘못됨</span><span class="sxs-lookup"><span data-stu-id="0e7e3-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="0e7e3-166">캡처 프로세스를 수행할 때 올바른 필드가 강조 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="0e7e3-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="0e7e3-167">캡처 프로세스를 통해 예상대로 응용 프로그램의 로그인 페이지로 이동하지만 아무 일도 발생하지 않음</span><span class="sxs-lookup"><span data-stu-id="0e7e3-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="0e7e3-168">수동 캡처가 작동하는 것처럼 보이지만 사용자가 액세스 패널에서 응용 프로그램으로 이동할 때 SSO가 발생하지 않음</span><span class="sxs-lookup"><span data-stu-id="0e7e3-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="0e7e3-169">이러한 문제가 발생하는 경우 다음 사항을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="0e7e3-170">[액세스 패널 브라우저 확장을 설치하는 방법](#how-to-install-the-access-panel-browser-extension) 섹션의 단계에 따라 최신 버전의 액세스 패널 브라우저 확장을 **설치**하고 **활성화**했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="0e7e3-171">브라우저가 **incognito, inPrivate 또는 개인 모드**일 때 캡처 프로세스를 시도하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="0e7e3-172">이러한 모드에서는 액세스 패널 확장이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="0e7e3-173">**incognito, inPrivate 또는 개인 모드**일 때 사용자가 액세스 패널의 응용 프로그램에 로그인하려고 하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="0e7e3-174">이러한 모드에서는 액세스 패널 확장이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="0e7e3-175">빨간색 마커가 올바른 필드 위에 있는지 확인하고 수동 캡처 프로세스를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="0e7e3-176">수동 캡처 프로세스가 중단되거나 로그인 페이지에서 아무 일도 일어나지 않는 경우(위 사례 3) 수동 캡처 프로세스를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="0e7e3-177">그러나 이번에는 프로세스를 완료한 후 **F12** 단추를 눌러 브라우저의 개발자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="0e7e3-178">**콘솔**을 열고 **window.location=”&lt;앱을 구성할 때 지정한 로그인 URL 입력&gt;”**을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="0e7e3-179">그러면 캡처 프로세스를 종료하는 페이지 리디렉션이 실행되고 캡처한 필드가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="0e7e3-180">위 방법으로 해결되지 않는 경우 Microsoft에서 도와드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="0e7e3-181">[포털 알림의 세부 정보를 확인하는 방법](#i-cannot-manually-detect-sign-in-fields-for-my-application) 및 [지원 엔지니어에게 알림 세부 정보를 전송하여 도움을 얻는 방법](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) 섹션(해당하는 경우)에서 수집한 정보뿐만 아니라 시도한 내용의 세부 정보와 함께 지원 케이스를 여세요.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="0e7e3-182">액세스 패널 브라우저 확장을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e7e3-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="0e7e3-183">액세스 패널 브라우저 확장을 설치하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="0e7e3-184">지원되는 브라우저 중 하나에서 [액세스 패널](https://myapps.microsoft.com)을 열고 Azure AD에서 **사용자**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="0e7e3-185">액세스 패널에서 **암호-SSO 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="0e7e3-186">소프트웨어를 설치하라는 프롬프트에서 **지금 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="0e7e3-187">브라우저에 따라 다운로드 링크로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="0e7e3-188">브라우저에 확장을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="0e7e3-189">브라우저에서 요청하면 확장을 **사용** 또는 **허용**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="0e7e3-190">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="0e7e3-191">액세스 패널에 로그인하고 암호 SSO 응용 프로그램을 **시작**할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="0e7e3-192">아래와 같은 직접 링크에서 Chrome 및 Firefox에 대한 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="0e7e3-193">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="0e7e3-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="0e7e3-194">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="0e7e3-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="0e7e3-195">포털 알림의 세부 정보를 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e7e3-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="0e7e3-196">다음 단계를 수행하여 포털 알림의 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="0e7e3-197">Azure Portal의 오른쪽 위에 있는 **알림** 아이콘(벨)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="0e7e3-198">**오류** 상태(옆에 빨간색(!)이 있는)에서 알림을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="0e7e3-199">[!NOTE] **성공** 또는 **진행 중** 상태에서 알림을 클릭할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="0e7e3-200">**알림 세부 정보** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="0e7e3-201">이 정보를 사용하여 문제에 대한 자세한 내용을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="0e7e3-202">여전히 도움이 필요한 경우 문제에 대한 도움을 얻도록 이 정보를 지원 엔지니어 또는 제품 그룹과 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="0e7e3-203">**오류 복사** 텍스트 상자 오른쪽의 **복사** **아이콘**을 클릭하여 지원 또는 제품 그룹 엔지니어와 공유하도록 모든 알림 세부 정보를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="0e7e3-204">지원 엔지니어에게 알림 세부 정보를 전송하여 도움을 얻는 방법</span><span class="sxs-lookup"><span data-stu-id="0e7e3-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="0e7e3-205">도움이 필요한 경우 지원 엔지니어가 신속하게 도움을 줄 수 있도록 **아래에 나열된 모든 세부 정보**를 공유하는 것은 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="0e7e3-206">**스크린샷을 찍거나** **오류 복사** 텍스트 상자 오른쪽에 있는 **오류 복사 아이콘**을 클릭하여 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="0e7e3-207">알림 세부 정보 설명</span><span class="sxs-lookup"><span data-stu-id="0e7e3-207">Notification Details Explained</span></span>

<span data-ttu-id="0e7e3-208">다음은 각 알림 항목이 의미하는 내용을 자세히 설명하고 각 항목의 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7e3-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="0e7e3-209">중요 알림 항목</span><span class="sxs-lookup"><span data-stu-id="0e7e3-209">Essential Notification Items</span></span>

-   <span data-ttu-id="0e7e3-210">**제목** - 알림의 설명이 포함된 제목</span><span class="sxs-lookup"><span data-stu-id="0e7e3-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="0e7e3-211">예제 - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="0e7e3-212">**설명** – 작업의 결과로 발생한 문제에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="0e7e3-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="0e7e3-213">예제 - **입력한 내부 url은 이미 다른 응용 프로그램에서 사용 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="0e7e3-214">**알림 ID** - 알림의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="0e7e3-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="0e7e3-215">예제 – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="0e7e3-216">**클라이언트 요청 ID** -브라우저에서 만든 특정 요청 ID</span><span class="sxs-lookup"><span data-stu-id="0e7e3-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="0e7e3-217">예제 – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="0e7e3-218">**타임스탬프 UTC** – 알림이 발생한 동안의 타임스탬프(UTC)</span><span class="sxs-lookup"><span data-stu-id="0e7e3-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="0e7e3-219">예제 – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="0e7e3-220">**내부 트랜잭션 ID** – 시스템에서 오류를 찾는 데 사용할 수 있는 내부 ID</span><span class="sxs-lookup"><span data-stu-id="0e7e3-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="0e7e3-221">예제 – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="0e7e3-222">**UPN** – 작업을 수행한 사용자</span><span class="sxs-lookup"><span data-stu-id="0e7e3-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="0e7e3-223">예제 – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="0e7e3-224">**테넌트 ID** – 작업을 수행한 사용자가 구성원인 테넌트의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="0e7e3-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="0e7e3-225">예제 – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="0e7e3-226">**사용자 개체 ID** – 작업을 수행한 사용자의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="0e7e3-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="0e7e3-227">예제 – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="0e7e3-228">자세한 알림 항목</span><span class="sxs-lookup"><span data-stu-id="0e7e3-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="0e7e3-229">**표시 이름** – **(비어 있을 수 있음)** 오류에 대한 보다 자세한 표시 이름</span><span class="sxs-lookup"><span data-stu-id="0e7e3-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="0e7e3-230">예* - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="0e7e3-231">**상태** - 알림의 특정 상태</span><span class="sxs-lookup"><span data-stu-id="0e7e3-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="0e7e3-232">예* – **실패**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="0e7e3-233">**개체 ID** – **(비어 있을 수 있음)** 작업이 수행된 개체 ID</span><span class="sxs-lookup"><span data-stu-id="0e7e3-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="0e7e3-234">예제 – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="0e7e3-235">**세부 정보** – 작업의 결과로 발생한 문제에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="0e7e3-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="0e7e3-236">예제 – **내부 url 'http://bing.com/'은 이미 사용 중이므로 유효하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="0e7e3-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="0e7e3-237">**오류 복사** - **오류 복사** 텍스트 상자 오른쪽의 **복사 아이콘**을 클릭하여 지원 또는 제품 그룹 엔지니어와 공유하도록 모든 알림 세부 정보 복사</span><span class="sxs-lookup"><span data-stu-id="0e7e3-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="0e7e3-238">예 – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="0e7e3-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e7e3-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e7e3-239">Next steps</span></span>
[<span data-ttu-id="0e7e3-240">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="0e7e3-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

