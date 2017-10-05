---
title: "Azure AD 갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성할 때 발생하는 문제 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에 이미 나열된 응용 프로그램에 대해 암호 Single Sign-On을 구성할 때 발생하는 일반적인 문제 이해"
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
ms.openlocfilehash: 58d29996a922fac6d295e753ba5d66d32e745a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="5f7fc-103">Azure AD 갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="5f7fc-103">Problem configuring password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="5f7fc-104">이 문서는 Azure AD 갤러리 응용 프로그램에 대해 **암호 Single Sign-On**을 구성할 때 발생하는 일반적인 문제를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-104">This article help you to understand the common problems people face when configuring **Password Single Sign-on** with an Azure AD Gallery application.</span></span>

## <a name="credentials-are-filled-in-but-the-extension-does-not-submit-them"></a><span data-ttu-id="5f7fc-105">자격 증명은 입력했지만 확장에서 제출하지 않음</span><span class="sxs-lookup"><span data-stu-id="5f7fc-105">Credentials are filled in, but the extension does not submit them</span></span>

<span data-ttu-id="5f7fc-106">이 문제는 일반적으로 응용 프로그램 공급업체에서 최근에 로그인 페이지를 변경하여 필드를 추가했거나, 사용자 이름 및 암호 필드 감지에 사용하는 기반 식별자를 변경했거나, 응용 프로그램의 로그인 경험 방식을 수정한 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-106">This typically happens if the application vendor has changed their sign in page recently to add a field, change an underlying identifier we used to detect the username and password fields, or modify how the sign in experience works for their application.</span></span> <span data-ttu-id="5f7fc-107">다행스럽게도 많은 경우에 Microsoft와 응용 프로그램 공급업체가 협력하여 이 문제를 신속하게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-107">Fortunately, in many instances, Microsoft can work with application vendors to rapidly resolve these issues.</span></span>

<span data-ttu-id="5f7fc-108">Microsoft에는 이렇게 통합이 깨졌을 때 자동으로 감지할 기술이 있지만, 문제를 즉시 발견하지 못하거나 해결할 때까지 시간이 걸리는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-108">While Microsoft has technologies to automatically detect when these integrations break, but sometimes we are not able to find these issues right away, or they take some time to fix.</span></span> <span data-ttu-id="5f7fc-109">이러한 통합이 올바르게 작동하지 않는 경우에는 가능한 한 빨리 해결할 수 있도록 지원 사례를 열어 주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-109">In the case when one of these integrations does not work correctly, we would appreciate if you opened a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="5f7fc-110">또한 **이 응용 프로그램의 공급업체와 연락된 경우는 응용 프로그램을 Azure Active Directory와 기본적으로 통합하기 위한 작업을 함께 진행할 수 있도록** **Microsoft로 보내 주세요**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-110">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="5f7fc-111">공급업체에서 작업을 시작할 수 있도록 [Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램 나열](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)로 보내 주시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-111">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="credentials-are-filled-in-and-submitted-but-the-page-indicates-the-credentials-are-incorrect"></a><span data-ttu-id="5f7fc-112">자격 증명을 입력하고 제출했지만 페이지에 자격 증명이 잘못되었다고 표시됨</span><span class="sxs-lookup"><span data-stu-id="5f7fc-112">Credentials are filled in and submitted, but the page indicates the credentials are incorrect</span></span>

<span data-ttu-id="5f7fc-113">이 문제를 해결하려면 먼저 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-113">To resolve this issue, first check the following:</span></span>

-   <span data-ttu-id="5f7fc-114">사용자가 먼저 저장된 자격 증명을 사용해서 **응용 프로그램 웹 사이트에 직접 로그인**을 시도하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-114">Have the user first try to **sign in to the application website directly** with the credentials stored for them.</span></span>

  * <span data-ttu-id="5f7fc-115">로그인이 되면 사용자가 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)의 **응용 프로그램** 섹션에서 **응용 프로그램 타일**에 있는 **자격 증명 업데이트** 단추를 클릭하여 문제가 없는 최신 사용자 이름 및 암호로 업데이트하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-115">If that works, then have the user click the **Update credentials** button on the **Application Tile** in the **Apps** section of the [Application Access Panel](https://myapps.microsoft.com/) to update them to the latest known working username and password.</span></span>

   * <span data-ttu-id="5f7fc-116">자신이나 다른 관리자가 이 사용자에게 자격 증명을 할당한 경우는 응용 프로그램의 **사용자 및 그룹** 탭으로 이동하여 할당을 선택하고 **자격 증명 업데이트** 단추를 클릭하여 사용자 또는 그룹의 응용 프로그램 할당을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-116">If you, or another administrator assigned the credentials for this user, find the user or group’s application assignment by navigating to the **Users & Groups** tab of the application, selecting the assignment and clicking the **Update Credentials** button.</span></span>

-   <span data-ttu-id="5f7fc-117">사용자가 직접 자격 증명을 할당한 경우는 사용자에게 **응용 프로그램에서 암호가 만료되지 않았는지 확인하라고 한** 다음, 만료되었으면 응용 프로그램에 직접 로그인하여 **만료된 암호를 업데이트**하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-117">If the user assigned their own credentials, have the user **check to be sure that their password has not expired in the application** and if so, **update their expired password** by signing in to the application directly.</span></span>

   * <span data-ttu-id="5f7fc-118">응용 프로그램에서 암호가 업데이트된 후에 사용자에게 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)의 **응용 프로그램** 섹션에서 **응용 프로그램 타일**에 있는 **자격 증명 업데이트** 단추를 클릭하여 문제가 없는 최신 사용자 이름 및 암호로 업데이트하라고 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-118">After the password has been updated in the application, request the user to click the **Update credentials** button on the **Application Tile** in the **Apps** section of the [Application Access Panel](https://myapps.microsoft.com/) to update them to the latest known working username and password.</span></span>

   * <span data-ttu-id="5f7fc-119">자신이나 다른 관리자가 이 사용자에게 자격 증명을 할당한 경우는 응용 프로그램의 **사용자 및 그룹** 탭으로 이동하여 할당을 선택하고 **자격 증명 업데이트** 단추를 클릭하여 사용자 또는 그룹의 응용 프로그램 할당을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-119">If you, or another administrator assigned the credentials for this user, find the user or group’s application assignment by navigating to the **Users & Groups** tab of the application, selecting the assignment and clicking the **Update Credentials** button.</span></span>

-   <span data-ttu-id="5f7fc-120">사용자가 아래 [액세스 패널 브라우저 확장을 설치하는 방법](#how-to-install-the-access-panel-browser-extension) 섹션의 단계에 따라 액세스 패널 브라우저 확장을 업데이트하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-120">Have the user update the access panel browser extension by following the steps below in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="5f7fc-121">액세스 패널 브라우저 확장이 실행 중이며 사용자의 브라우저에서 사용하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-121">Ensure that the access panel browser extension is running and enabled in your user’s browser.</span></span>

-   <span data-ttu-id="5f7fc-122">**incognito, inPrivate 또는 개인 모드**일 때 사용자가 액세스 패널의 응용 프로그램에 로그인하려고 하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-122">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="5f7fc-123">이러한 모드에서는 액세스 패널 확장이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-123">The access panel extension is not supported in these modes.</span></span>

<span data-ttu-id="5f7fc-124">이 방법이 통하지 않는 경우는 응용 프로그램 쪽에서 변경이 일어나 일시적으로 응용 프로그램과 Azure AD의 통합이 깨졌을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-124">In case this does not work, it could be the case that a change has occurred on the application side which has temporarily broken the application’s integration with Azure AD.</span></span> <span data-ttu-id="5f7fc-125">예를 들어, 응용 프로그램 공급업체에서 수동 입력과 자동 입력에 대해 다르게 작동하는 스크립트를 페이지에 포함하는 바람에 자동화 통합이 깨지는 경우에 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-125">For example, this can occur when the application vendor introduces a script on their page which behaves differently for manual vs automated input, which causes automated integration, like our own, to break.</span></span> <span data-ttu-id="5f7fc-126">다행스럽게도 많은 경우에 Microsoft와 응용 프로그램 공급업체가 협력하여 이 문제를 신속하게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-126">Fortunately, in many instances, Microsoft can work with application vendors to rapidly resolve these issues.</span></span>

<span data-ttu-id="5f7fc-127">Microsoft에는 이렇게 통합이 깨졌을 때 자동으로 감지할 기술이 있지만, 문제를 즉시 발견하지 못하거나 해결할 때까지 시간이 걸리는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-127">While Microsoft has technologies to automatically detect when these integrations break, but sometimes we are not able to find these issues right away, or they take some time to fix.</span></span> <span data-ttu-id="5f7fc-128">이러한 통합이 올바르게 작동하지 않는 경우에는 가능한 한 빨리 해결할 수 있도록 지원 사례를 열어 주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-128">In the case when one of these integrations does not work correctly, we would appreciate if you opened a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="5f7fc-129">또한 **이 응용 프로그램의 공급업체와 연락된 경우는 응용 프로그램을 Azure Active Directory와 기본적으로 통합하기 위한 작업을 함께 진행할 수 있도록** **Microsoft로 보내 주세요**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-129">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="5f7fc-130">공급업체에서 작업을 시작할 수 있도록 [Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램 나열](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)로 보내 주시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-130">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="the-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a><span data-ttu-id="5f7fc-131">Chrome 및 Firefox에서는 확장이 작동하지만 Internet Explorer에서는 작동하지 않음</span><span class="sxs-lookup"><span data-stu-id="5f7fc-131">The extension works in Chrome and Firefox, but not in Internet Explorer</span></span>

<span data-ttu-id="5f7fc-132">이 문제에는 두 가지 주요 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-132">There are two main causes to this issue:</span></span>

-   <span data-ttu-id="5f7fc-133">Internet Explorer의 보안 설정에 따라, 웹 사이트가 **신뢰할 수 있는 영역**에 속해 있지 않으면 응용 프로그램에서 스크립트 실행이 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-133">Depending on the security settings enabled in Internet Explorer, if the website is not part of a **Trusted Zone**, sometimes our script be blocked from executing for the application.</span></span>

  *  <span data-ttu-id="5f7fc-134">이 문제를 해결하려면 사용자에게 **Internet Explorer 보안 설정**에서 **응용 프로그램의 웹 사이트**를 **신뢰할 수 있는 사이트** 목록에 추가하라고 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-134">To resolve this, instruct the user to **Add the application’s website** to the **Trusted Sites** list within their **Internet Explorer security settings**.</span></span> <span data-ttu-id="5f7fc-135">사용자가 자세한 지침을 확인할 수 있도록 [사이트를 신뢰할 수 있는 사이트 목록에 추가하는 방법](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) 문서로 안내할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-135">You can send your users to the [How to add a site to my trusted sites list](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) article for detailed instructions.</span></span>

-   <span data-ttu-id="5f7fc-136">드물게 Internet Explorer의 보안 유효성 검사 때문에 스크립트 실행 속도보다 페이지 로드 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-136">In rare circumstances, Internet Explorer’s security validation can sometimes cause the page to load more slowly than the execution of our script.</span></span>

   * <span data-ttu-id="5f7fc-137">이런 상황은 브라우저 버전, 컴퓨터 속도, 방문한 사이트에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-137">Unfortunately, this situation can vary depending on the browser version, computer speed, or site visited.</span></span> <span data-ttu-id="5f7fc-138">그런 경우는 특정 응용 프로그램의 통합을 수정할 수 있도록 지원 팀에 문의해 주세요.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-138">In this case, we suggest that you contact support so we can fix the integration for this specific application.</span></span>

<span data-ttu-id="5f7fc-139">또한 **이 응용 프로그램의 공급업체와 연락된 경우는 응용 프로그램을 Azure Active Directory와 기본적으로 통합하기 위한 작업을 함께 진행할 수 있도록** **Microsoft로 보내 주세요**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-139">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="5f7fc-140">공급업체에서 작업을 시작할 수 있도록 [Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램 나열](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)로 보내 주시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-140">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="check-if-the-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a><span data-ttu-id="5f7fc-141">응용 프로그램의 로그인 페이지가 최근에 변경되었거나 추가 필드가 필요한지 확인</span><span class="sxs-lookup"><span data-stu-id="5f7fc-141">Check if the application’s login page has changed recently or requires an additional field</span></span>

<span data-ttu-id="5f7fc-142">응용 프로그램의 로그인 페이지가 최근에 변경된 경우는 그 때문에 통합이 깨질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-142">If the application’s login page has changed drastically, sometimes this causes our integrations to break.</span></span> <span data-ttu-id="5f7fc-143">이런 예로는 응용 프로그램 공급업체에서 로그인 필드, chaptcha 또는 다단계 인증을 경험에 추가하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-143">An example of this is when an application vendor adds a sign in field, a captcha, or multi-factor authentication to their experiences.</span></span> <span data-ttu-id="5f7fc-144">다행스럽게도 많은 경우에 Microsoft와 응용 프로그램 공급업체가 협력하여 이 문제를 신속하게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-144">Fortunately, in many instances, Microsoft can work with application vendors to rapidly resolve these issues.</span></span>

<span data-ttu-id="5f7fc-145">Microsoft에는 이렇게 통합이 깨졌을 때 자동으로 감지할 기술이 있지만, 문제를 즉시 발견하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-145">While Microsoft has technologies to automatically detect when these integrations break, but sometimes we are not able to find these issues right away.</span></span> <span data-ttu-id="5f7fc-146">아니면 해결할 때까지 시간이 오래 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-146">Otherwise they take some time to fix.</span></span> <span data-ttu-id="5f7fc-147">이러한 통합이 올바르게 작동하지 않는 경우에는 가능한 한 빨리 해결할 수 있도록 지원 사례를 열어 주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-147">In the case when one of these integrations does not work correctly, we would appreciate opening a support case so we can fix it as quickly as possible.</span></span>

<span data-ttu-id="5f7fc-148">또한 **이 응용 프로그램의 공급업체와 연락된 경우는 응용 프로그램을 Azure Active Directory와 기본적으로 통합하기 위한 작업을 함께 진행할 수 있도록** **Microsoft로 보내 주세요**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-148">In addition to this, **if you are in contact with this application’s vendor,** **send them our way** so we can work with them to natively integrate their application with Azure Active Directory.</span></span> <span data-ttu-id="5f7fc-149">공급업체에서 작업을 시작할 수 있도록 [Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램 나열](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)로 보내 주시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-149">You can send the vendor to the [Listing your application in the Azure Active Directory application gallery](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) to get them started.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="5f7fc-150">액세스 패널 브라우저 확장을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="5f7fc-150">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="5f7fc-151">액세스 패널 브라우저 확장을 설치하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-151">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="5f7fc-152">지원되는 브라우저 중 하나에서 [액세스 패널](https://myapps.microsoft.com)을 열고 Azure AD에서 **사용자**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-152">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="5f7fc-153">액세스 패널에서 **암호-SSO 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-153">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="5f7fc-154">소프트웨어를 설치하라는 프롬프트에서 **지금 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-154">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="5f7fc-155">브라우저에 따라 다운로드 링크로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-155">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="5f7fc-156">브라우저에 확장을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-156">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="5f7fc-157">브라우저에서 요청하면 확장을 **사용** 또는 **허용**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-157">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="5f7fc-158">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-158">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="5f7fc-159">액세스 패널에 로그인하고 암호 SSO 응용 프로그램을 **시작**할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-159">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="5f7fc-160">아래와 같은 직접 링크에서 Chrome 및 Firefox에 대한 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-160">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="5f7fc-161">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="5f7fc-161">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="5f7fc-162">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="5f7fc-162">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a><span data-ttu-id="5f7fc-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f7fc-163">Next steps</span></span>
[<span data-ttu-id="5f7fc-164">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="5f7fc-164">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

