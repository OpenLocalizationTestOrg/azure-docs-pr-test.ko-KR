---
title: "Azure Mobile Engagement 웹 SDK 통합 | Microsoft Docs"
description: "Azure Mobile Engagement 웹 SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="3e91a-103">웹 응용 프로그램에 Azure Mobile Engagement 통합</span><span class="sxs-lookup"><span data-stu-id="3e91a-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e91a-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="3e91a-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="3e91a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3e91a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="3e91a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3e91a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="3e91a-107">Android</span><span class="sxs-lookup"><span data-stu-id="3e91a-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="3e91a-108">이 문서의 절차에서는 웹 응용 프로그램에서 Azure Mobile Engagement의 분석 및 모니터링 기능을 활성화하는 가장 간단한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="3e91a-109">다음 단계를 수행하여 사용자, 세션, 활동, 작동 중단 및 기술과 관련된 모든 통계를 계산하는 데 필요한 로그 보고를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="3e91a-110">이벤트, 오류, 작업 등의 응용 프로그램 종속 통계의 경우 Azure Mobile Engagement API를 사용하여 로그 보고를 수동으로 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="3e91a-111">자세한 내용은 [웹 응용 프로그램에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-web-use-engagement-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e91a-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="3e91a-112">소개</span><span class="sxs-lookup"><span data-stu-id="3e91a-112">Introduction</span></span>
<span data-ttu-id="3e91a-113">[Azure Mobile Engagement 웹 SDK 다운로드](http://aka.ms/P7b453)Mobile Engagement 웹 SDK는 단일 JavaScript 파일인 azure-engagement.js로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="3e91a-114">이 파일은 사이트 또는 웹 응용 프로그램의 각 페이지에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e91a-115">이 스크립트를 실행하려면 먼저 응용 프로그램의 Mobile Engagement를 구성하기 위해 작성한 스크립트 또는 코드 조각을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="3e91a-116">브라우저 호환성</span><span class="sxs-lookup"><span data-stu-id="3e91a-116">Browser compatibility</span></span>
<span data-ttu-id="3e91a-117">Mobile Engagement 웹 SDK는 크로스 도메인 AJAX 요청 외에 네이티브 JSON 인코딩 및 디코딩을 사용합니다(W3C CORS 사양 사용).</span><span class="sxs-lookup"><span data-stu-id="3e91a-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="3e91a-118">다음 브라우저와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="3e91a-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="3e91a-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="3e91a-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="3e91a-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="3e91a-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="3e91a-121">Firefox 3.5+</span></span>
* <span data-ttu-id="3e91a-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="3e91a-122">Chrome 4+</span></span>
* <span data-ttu-id="3e91a-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="3e91a-123">Safari 6+</span></span>
* <span data-ttu-id="3e91a-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="3e91a-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="3e91a-125">Mobile Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="3e91a-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="3e91a-126">다음 예제와 같은 전역 `azureEngagement` JavaScript 개체를 만드는 스크립트를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="3e91a-127">사이트에 여러 개의 페이지가 있을 수 있으므로 이 예제에서는 이 스크립트가 모든 페이지에 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="3e91a-128">이 예제에서 JavaScript 개체 이름은 `azure-engagement-conf.js`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="3e91a-129">응용 프로그램에 대한 `connectionString` 값이 Azure 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3e91a-130">`appVersionName` 및 `appVersionCode`는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="3e91a-131">그러나 분석할 때 프로세스 버전 정보가 처리될 수 있도록 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="3e91a-132">페이지에 Mobile Engagement 스크립트 포함</span><span class="sxs-lookup"><span data-stu-id="3e91a-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="3e91a-133">다음 방법 중 하나를 사용하여 페이지에 Mobile Engagement 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="3e91a-134">또는 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="3e91a-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="3e91a-135">Alias</span><span class="sxs-lookup"><span data-stu-id="3e91a-135">Alias</span></span>
<span data-ttu-id="3e91a-136">Mobile Engagement 웹 SDK 스크립트는 로드되면 SDK API에 액세스하기 위한 **engagement** 별칭을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="3e91a-137">SDK 구성을 정의하는 데는 이 별칭을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="3e91a-138">이 별칭은 이 설명서에서 참조로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="3e91a-139">기본 별칭이 페이지의 다른 전역 변수와 충돌할 경우 다음과 같이 Mobile Engagement 웹 SDK를 로드하기 전에 구성에서 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="3e91a-140">기본 보고</span><span class="sxs-lookup"><span data-stu-id="3e91a-140">Basic reporting</span></span>
<span data-ttu-id="3e91a-141">Mobile Engagement의 기본 보고 기능에는 사용자, 세션, 활동 및 작동 중단에 대한 통계와 같은 세션 수준 통계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="3e91a-142">세션 추적</span><span class="sxs-lookup"><span data-stu-id="3e91a-142">Session tracking</span></span>
<span data-ttu-id="3e91a-143">Mobile Engagement 세션은 일련의 활동으로 나뉘며 각각이 이름으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="3e91a-144">기존 웹 사이트는 사이트의 각 페이지에서 서로 다른 활동을 선언하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="3e91a-145">현재 페이지가 절대 변경되지 않는 웹 사이트 또는 웹 응용 프로그램에서는 페이지 내부와 같이 좀 더 작은 규모로 활동을 추적하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="3e91a-146">현재 사용자 활동을 시작하든 변경하든 `engagement.agent.startActivity` 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="3e91a-147">예:</span><span class="sxs-lookup"><span data-stu-id="3e91a-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="3e91a-148">Mobile Engagement 서버는 응용 프로그램 페이지가 닫히고 3분 이내에 열린 세션을 자동으로 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="3e91a-149">또는 `engagement.agent.endActivity`를 호출하여 세션을 수동으로 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="3e91a-150">이렇게 하면 현재 사용자 활동이 'Idle'로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="3e91a-151">`engagement.agent.startActivity` 의 새 호출이 세션을 다시 시작하지 않는 한, 세션은 10초 후에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="3e91a-152">다음과 같이 전역 Engagement 개체에서 10초의 지연을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="3e91a-153">이 단계에서는 AJAX를 호출할 수 없으므로 `onunload` 콜백에서 `engagement.agent.endActivity`를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="3e91a-154">고급 보고</span><span class="sxs-lookup"><span data-stu-id="3e91a-154">Advanced reporting</span></span>
<span data-ttu-id="3e91a-155">필요에 따라 응용 프로그램 관련 이벤트, 오류 및 작업을 보고하려는 경우 Mobile Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="3e91a-156">`engagement.agent` 개체를 통해 Mobile Engagement API에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="3e91a-157">Mobile Engagement API의 Mobile Engagement에서 모든 고급 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="3e91a-158">이 API는 [웹 응용 프로그램에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-web-use-engagement-api.md)문서에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="3e91a-159">AJAX 호출에 사용되는 URL 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3e91a-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="3e91a-160">Mobile Engagement 웹 SDK에서 사용되는 URL을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="3e91a-161">예를 들어 로그 URL(로깅을 위한 SDK 끝점)을 다시 정의하기 위해 다음과 같이 구성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="3e91a-162">URL 함수가 `/`, `//`, `http://` 또는 `https://`로 시작하는 문자열을 반환한다면 기본 구성표가 사용되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="3e91a-163">기본적으로 해당 URL에는 `https://` 구성표가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="3e91a-164">기본 구성표를 사용자 지정하고 싶다면 다음과 같이 구성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3e91a-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
