---
title: "aaaProblem 암호 single sign on 갤러리가 아닌 응용 프로그램에 대 한 구성 | Microsoft Docs"
description: "암호 Single sign-on 나열 되지 않은 사용자 지정 갤러리 아닌 응용 프로그램에 대 한 hello Azure AD 응용 프로그램 갤러리에서에서 구성할 때 일반적인 문제 사람이 면 hello 이해"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9cf88-103">비갤러리 응용 프로그램에 대해 암호 Single Sign-On 구성 문제</span><span class="sxs-lookup"><span data-stu-id="9cf88-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9cf88-104">이 문서가 도움이 되었나요 toounderstand hello 일반적인 문제 사람 얼굴을 구성할 때 **암호 single sign on** 갤러리 아닌 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="9cf88-105">어떻게 toocapture 로그인 응용 프로그램에 대 한 필드</span><span class="sxs-lookup"><span data-stu-id="9cf88-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="9cf88-106">로그인 필드 캡처는 HTML 기반 로그인 페이지에 대해서만 지원되고 Flash나 기타 비HTML 기반 기술을 사용하는 로그인 페이지처럼 **비표준 로그인 페이지에 대해서는 지원되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="9cf88-107">두 가지 방법으로 사용자 지정 응용 프로그램에 대한 로그인 필드를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="9cf88-108">자동 로그인 필드 캡처</span><span class="sxs-lookup"><span data-stu-id="9cf88-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="9cf88-109">수동 로그인 필드 캡처</span><span class="sxs-lookup"><span data-stu-id="9cf88-109">Manual sign-in field capture</span></span>

<span data-ttu-id="9cf88-110">**자동 로그인 필드 캡처** 사용 하는 경우 대부분 HTML 기반 로그인 페이지를 사용 하 여 작동 **hello 사용자 이름 및 암호 입력에 대 한 잘 알려진 DIV Id** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="9cf88-111">이 작동 하는 hello 방식 및 하는 hello 페이지 toofind 특정 조건과 일치 하는 DIV Id의 HTML 긁히는 hello 암호 tooit를 나중에 재생 수 있도록이 응용 프로그램에 대 한 메타 데이터를 저장 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cf88-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="9cf88-112">**수동 로그인 필드 캡처** 응용 프로그램 hello hello 사례에서 사용할 수 있습니다 **공급 업체 레이블이 표시 되지 않을** hello에 로그온 하는 데 사용 되는 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="9cf88-113">수동 로그인 필드 캡처 hello 경우 hello 사용할 수도 있습니다 **여러 필드를 렌더링 하는 공급 업체** 자동으로 감지 될 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="9cf88-114">Azure AD 데이터를 저장할 수에 대 한 페이지에 서명 하는 hello에 만큼 필드 알려 주시면 hello 페이지에서 이러한 필드는 여기서으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="9cf88-115">일반적으로 **동안 hello 수동 옵션 자동 로그인 필드 캡처 작동 하지 않는 경우 항상 제안 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="9cf88-116">Tooautomatically 응용 프로그램에 대 한 로그인 필드 캡처 방식</span><span class="sxs-lookup"><span data-stu-id="9cf88-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="9cf88-117">tooconfigure **암호 기반 Single sign-on** 사용 하 여 응용 프로그램에 대 한 **자동 로그인 필드 캡처**, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="9cf88-118">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="9cf88-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9cf88-119">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9cf88-120">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9cf88-121">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9cf88-122">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="9cf88-123">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9cf88-124">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="9cf88-125">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9cf88-126">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9cf88-127">Hello 입력 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="9cf88-128">사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="9cf88-129">**Hello 로그인 필드를 제공 하는 hello URL에 표시 되는지 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="9cf88-130">Hello 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="9cf88-131">이렇게 하면, 사용자 이름에 해당 URL 이벤트를 자동으로 처리 합니다 우리 및 암호 입력 상자 하 고 사용 하 되 면 toouse Azure AD toosecurely hello 액세스 패널 브라우저 확장을 사용 하 여 toothat 응용 프로그램 암호를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="9cf88-132">Toomanually 응용 프로그램에 대 한 로그인 필드 캡처 방식</span><span class="sxs-lookup"><span data-stu-id="9cf88-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="9cf88-133">toomanually 캡처 로그인 필드, 있어야 hello 액세스 패널 브라우저 확장을 설치 하 고 **inPrivate, incognito 또는 개인 모드에서 실행 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="9cf88-134">tooinstall hello 브라우저 확장을 hello에 hello 단계 수행 [어떻게 tooinstall hello 액세스 패널 브라우저 확장](#i-cannot-manually-detect-sign-in-fields-for-my-application) 섹션.</span><span class="sxs-lookup"><span data-stu-id="9cf88-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="9cf88-135">tooconfigure **암호 기반 Single sign-on** 사용 하 여 응용 프로그램에 대 한 **수동 로그인 필드 캡처**, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="9cf88-136">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="9cf88-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9cf88-137">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9cf88-138">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9cf88-139">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9cf88-140">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="9cf88-141">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9cf88-142">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="9cf88-143">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9cf88-144">선택 hello 모드 **암호 기반 로그온 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9cf88-145">Hello 입력 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="9cf88-146">사용자가을 자신의 사용자 이름 및 암호 toosign 입력할 수 있는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="9cf88-147">**Hello 로그인 필드를 제공 하는 hello URL에 표시 되는지 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="9cf88-148">Hello 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="9cf88-149">이렇게 하면, 사용자 이름에 해당 URL 이벤트를 자동으로 처리 합니다 우리 및 암호 입력 상자 하 고 사용 하 되 면 toouse Azure AD toosecurely hello 액세스 패널 브라우저 확장을 사용 하 여 toothat 응용 프로그램 암호를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="9cf88-150">이 작업이 실패 하면 hello 경우에서 수 **변경 hello 로그인 모드 toouse 수동 로그인 필드 캡처** toostep 12 계속 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="9cf88-151">**&lt;앱 이름&gt; 암호 Single Sign-On 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="9cf88-152">선택 hello **로그인 필드를 수동으로 검색** 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="9cf88-153">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-153">Click **Ok**.</span></span>

15. <span data-ttu-id="9cf88-154">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-154">Click **Save**.</span></span>

16. <span data-ttu-id="9cf88-155">화면 지침 toouse hello 액세스 패널에 hello를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="9cf88-156">“해당 URL에서 로그인 필드를 찾을 수 없습니다” 오류가 표시됨</span><span class="sxs-lookup"><span data-stu-id="9cf88-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="9cf88-157">로그인 필드 자동 검색에 실패하면 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="9cf88-158">hello에서 단계를 시도 수동 로그인 필드 검색 hello 수행 하 여이 문제는 tooresolve [toomanually 응용 프로그램에 대 한 로그인 필드 캡처 방식](#how-to-manually-capture-sign-in-fields-for-an-application) 섹션.</span><span class="sxs-lookup"><span data-stu-id="9cf88-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="9cf88-159">"없습니다 toosave Single Sign on 구성" 오류가 발생</span><span class="sxs-lookup"><span data-stu-id="9cf88-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="9cf88-160">드문 경우 이지만 특정 hello single sign on 구성 업데이트가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="9cf88-161">tooresolve이 구성을 저장 하는 hello single sign on 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cf88-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="9cf88-162">Toofail를 일관 되 게 계속 열고 지원 케이스 정보를 제공 hello hello에 수집 된 [어떻게 toosee hello 세부 정보는 포털 알림](#i-cannot-manually-detect-sign-in-fields-for-my-application) 및 [tooget 알림 세부 정보 tooa 전송 하 여 도움말 하는 방법 지원 엔지니어가](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) 섹션.</span><span class="sxs-lookup"><span data-stu-id="9cf88-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="9cf88-163">응용 프로그램에 대한 로그인 필드를 수동으로 검색할 수 없음</span><span class="sxs-lookup"><span data-stu-id="9cf88-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="9cf88-164">일부 hello 동작 수동 검색이 작동 하지 않는 경우 표시 될 수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="9cf88-165">hello 수동 캡처 프로세스가 toowork, 나타나지만 캡처된 hello 필드가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="9cf88-166">hello 캡처 프로세스를 수행할 때 hello 오른쪽 필드 강조 표시 된 가져오기 안 함</span><span class="sxs-lookup"><span data-stu-id="9cf88-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="9cf88-167">hello 캡처 프로세스가 me toohello 응용 프로그램의 로그인 페이지 예상 대로 걸리지만 아무 일도 발생</span><span class="sxs-lookup"><span data-stu-id="9cf88-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="9cf88-168">수동 캡처 toowork, 나타나지만 SSO 내 사용자가 액세스 패널 hello에서 toohello 응용 프로그램을 이동할 때 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="9cf88-169">이러한 문제가 발생 하는 경우 hello 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="9cf88-170">Hello 최신 버전의 hello 액세스 패널 브라우저 확장이 있는지 확인 하십시오. **설치** 및 **활성화** hello에 hello 단계에 따라 [tooinstall 액세스 패널 브라우저 hello 하는 방법 확장](#how-to-install-the-access-panel-browser-extension) 섹션.</span><span class="sxs-lookup"><span data-stu-id="9cf88-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="9cf88-171">Hello 캡처 프로세스에 브라우저 하는 동안 려 하지 않았는지 확인 하십시오. **incognito, inPrivate, 또는 개인 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="9cf88-172">이러한 모드에는 hello 액세스 패널 확장이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="9cf88-173">사용자가 하는 동안 hello 액세스 패널에서 toohello 응용 프로그램에서 toosign 시도 하지 않는 확인 **incognito, inPrivate, 또는 개인 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="9cf88-174">이러한 모드에는 hello 액세스 패널 확장이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="9cf88-175">Hello 수동 캡처 프로세스를 다시 시도 하세요 hello 올바른 필드 위에 빨간색 hello 표식 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="9cf88-176">Hello 수동 캡처 프로세스가 toohang, 하거나 hello 로그인 페이지에서 수행 하지는 않습니다 (경우 3 위에), 아무것도 hello 수동 캡처 프로세스가 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="9cf88-177">하지만 키를 눌러 hello hello 프로세스를 완료 한 후이 이번 **F12** tooopen 브라우저의 개발자 콘솔 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="9cf88-178">한 번 hello를 열고 **콘솔** 유형과 **window.location= "&lt;hello 앱을 구성할 때 지정한 url에 hello 기호를 입력&gt;"** 누릅니다  **입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="9cf88-179">이 강제 페이지 hello 캡처 프로세스를 종료 하 고 캡처한 hello 필드 저장 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="9cf88-180">위 방법으로 해결되지 않는 경우 Microsoft에서 도와드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="9cf88-181">시도 하면 정보 뿐 아니라 hello hello에 수집 된 hello 세부 정보와 함께 지원 상담 [어떻게 toosee hello 세부 정보는 포털 알림](#i-cannot-manually-detect-sign-in-fields-for-my-application) 및 [tooget tooa 지원 알림 세부 정보를 전송 하 여 도움말 하는 방법 엔지니어](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) 섹션 (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="9cf88-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="9cf88-182">Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9cf88-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="9cf88-183">아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="9cf88-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="9cf88-184">열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="9cf88-185">클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="9cf88-186">Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="9cf88-187">브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="9cf88-188">**추가** hello 확장 tooyour 브라우저.</span><span class="sxs-lookup"><span data-stu-id="9cf88-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="9cf88-189">브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="9cf88-190">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="9cf88-191">Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="9cf88-192">Hello 직접 링크 아래에서 Chrome 및 Firefox에 대 한 hello 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="9cf88-193">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="9cf88-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="9cf88-194">Firefox 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="9cf88-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="9cf88-195">어떻게 포털 알림의 toosee hello 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9cf88-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="9cf88-196">다음 hello 단계를 수행 하 여 포털 알림에 대 한 hello 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="9cf88-197">hello 클릭 **알림** hello hello Azure 포털의 오른쪽 위에 있는 아이콘 (hello 벨)</span><span class="sxs-lookup"><span data-stu-id="9cf88-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="9cf88-198">에 모든 알림 선택는 **오류** 상태 (빨강 (!) 다음 toothem 순위가).</span><span class="sxs-lookup"><span data-stu-id="9cf88-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="9cf88-199">[!NOTE] **성공** 또는 **진행 중** 상태에서 알림을 클릭할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="9cf88-200">이 열린 hello **알림 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="9cf88-201">사용 하 여이 정보 직접 toounderstand hello 문제에 대 한 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="9cf88-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="9cf88-202">여전히 도움이 필요 하거나, 문제에는 지원 엔지니어 또는 hello 제품 그룹 tooget 도움말와이 정보를도 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="9cf88-203">Hello 클릭 **복사** **아이콘** toohello hello의 오른쪽 **오류 복사** textbox toocopy 모든 hello 지원 또는 제품 그룹 엔지니어와 알림 세부 정보 tooshare 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="9cf88-204">알림 세부 정보 tooa 지원 엔지니어 전송 하 여 tooget 도움말 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9cf88-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="9cf88-205">공유 하는 것이 중요 **세부 정보 아래에 나열 된 모든 hello** 신속 하 게 이용할 수 있도록, 한 도움이 필요한 경우 지원 엔지니어와 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="9cf88-206">있습니다 수 간편 하 게 **는 스크린샷을 만든** hello를 클릭 하 여 **복사 오류 아이콘**, toohello 오른쪽 hello에 찾을 **오류 복사** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="9cf88-207">알림 세부 정보 설명</span><span class="sxs-lookup"><span data-stu-id="9cf88-207">Notification Details Explained</span></span>

<span data-ttu-id="9cf88-208">아래 hello 의미 더 어떤 항목에는 각각 hello 알림 및 각각의 사용 예를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="9cf88-209">중요 알림 항목</span><span class="sxs-lookup"><span data-stu-id="9cf88-209">Essential Notification Items</span></span>

-   <span data-ttu-id="9cf88-210">**제목** – hello 알림 설명이 포함 된 제목을 hello</span><span class="sxs-lookup"><span data-stu-id="9cf88-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="9cf88-211">예제 - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="9cf88-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="9cf88-212">**설명** – hello에 대 한 hello 작업의 결과로 발생 한 문제 설명</span><span class="sxs-lookup"><span data-stu-id="9cf88-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="9cf88-213">예제 - **입력한 내부 url은 이미 다른 응용 프로그램에서 사용 중입니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="9cf88-214">**알림 Id** – hello hello 알림의 고유 id</span><span class="sxs-lookup"><span data-stu-id="9cf88-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="9cf88-215">예제 – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="9cf88-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="9cf88-216">**클라이언트 요청 Id** – 브라우저 수행한 hello 특정 요청 id</span><span class="sxs-lookup"><span data-stu-id="9cf88-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="9cf88-217">예제 – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="9cf88-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="9cf88-218">**스탬프의 UTC 시간** – hello는 hello 알림이 발생 한 utc에서 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="9cf88-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="9cf88-219">예제 – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="9cf88-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="9cf88-220">**내부 트랜잭션 Id** – hello toolook hello 오류 시스템에 사용 하는 내부 ID</span><span class="sxs-lookup"><span data-stu-id="9cf88-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="9cf88-221">예제 – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="9cf88-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="9cf88-222">**UPN** – hello 작업을 수행한 hello 사용자</span><span class="sxs-lookup"><span data-stu-id="9cf88-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="9cf88-223">예제 – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="9cf88-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="9cf88-224">**테 넌 트 Id** – hello 테 넌 트의 사용자 hello hello 작업을 수행한 hello 고유 ID는의 구성원</span><span class="sxs-lookup"><span data-stu-id="9cf88-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="9cf88-225">예제 – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="9cf88-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="9cf88-226">**사용자 개체 Id** – hello hello 작업을 수행한 hello 사용자의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="9cf88-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="9cf88-227">예제 – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="9cf88-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="9cf88-228">자세한 알림 항목</span><span class="sxs-lookup"><span data-stu-id="9cf88-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="9cf88-229">**표시 이름** – **(비어 있을 수 있습니다)** hello 오류에 대 한 보다 자세한 표시 이름</span><span class="sxs-lookup"><span data-stu-id="9cf88-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="9cf88-230">예* - **응용 프로그램 프록시 설정**</span><span class="sxs-lookup"><span data-stu-id="9cf88-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="9cf88-231">**상태** – hello hello 알림의 특정 상태</span><span class="sxs-lookup"><span data-stu-id="9cf88-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="9cf88-232">예* – **실패**</span><span class="sxs-lookup"><span data-stu-id="9cf88-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="9cf88-233">**개체 Id** – **(비어 있을 수 있습니다)** 개체 ID는 hello에 대 한 작업을 수행한 hello</span><span class="sxs-lookup"><span data-stu-id="9cf88-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="9cf88-234">예제 – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="9cf88-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="9cf88-235">**세부 정보** – hello를 자세하게 hello 작업의 결과로 발생 한 문제 설명</span><span class="sxs-lookup"><span data-stu-id="9cf88-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="9cf88-236">예제 – **내부 url 'http://bing.com/'은 이미 사용 중이므로 유효하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf88-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="9cf88-237">**오류 복사** – hello 클릭 **복사 아이콘** toohello hello의 오른쪽 **오류 복사** textbox toocopy 모든 지원 또는 제품 그룹 엔지니어와 알림 세부 정보 tooshare hello</span><span class="sxs-lookup"><span data-stu-id="9cf88-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="9cf88-238">예 – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="9cf88-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cf88-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cf88-239">Next steps</span></span>
[<span data-ttu-id="9cf88-240">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf88-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

