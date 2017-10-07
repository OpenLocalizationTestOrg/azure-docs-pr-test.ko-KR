---
title: "Mobile Engagement 웹 SDK 통합 aaaAzure | Microsoft Docs"
description: "최신 업데이트 및 hello Azure Mobile Engagement 웹 SDK에 대 한 절차 hello"
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
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="da5e7-103">웹 응용 프로그램에 Azure Mobile Engagement 통합</span><span class="sxs-lookup"><span data-stu-id="da5e7-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da5e7-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="da5e7-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="da5e7-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="da5e7-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="da5e7-106">iOS</span><span class="sxs-lookup"><span data-stu-id="da5e7-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="da5e7-107">Android</span><span class="sxs-lookup"><span data-stu-id="da5e7-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="da5e7-108">hello 가장 간단한 방법은 tooactivate hello 분석 워크 로드와 웹 응용 프로그램에서 Azure Mobile Engagement의 함수 모니터링이 문서의 hello 절차에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="da5e7-109">Hello 단계 tooactivate hello 로그 있는 보고서를 필요한 toocompute 사용자, 세션, 활동, 충돌 및 technicals 하는 방법에 대 한 모든 통계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="da5e7-110">이벤트, 오류, 작업 및 등의 응용 프로그램에 따라 통계에 대 한 hello Azure Mobile Engagement API를 사용 하 여 로그 보고서를 수동으로 활성화 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="da5e7-111">자세한 내용은 [어떻게 toouse hello 고급 Mobile Engagement 웹 응용 프로그램에서 API 태깅](mobile-engagement-web-use-engagement-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="da5e7-112">소개</span><span class="sxs-lookup"><span data-stu-id="da5e7-112">Introduction</span></span>
<span data-ttu-id="da5e7-113">[Hello Azure Mobile Engagement 웹 SDK 다운로드](http://aka.ms/P7b453)합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="da5e7-114">hello 모바일 Engagement 웹 SDK는 단일 JavaScript 파일 요소로 제공 되며, azure engagement.js 있는 사이트 또는 웹 응용 프로그램의 각 페이지에서 tooinclude 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da5e7-115">이 스크립트를 실행 하기 전에 스크립트를 실행 하거나 코드 조각 tooconfigure Mobile Engagement 응용 프로그램에 대해 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="da5e7-116">브라우저 호환성</span><span class="sxs-lookup"><span data-stu-id="da5e7-116">Browser compatibility</span></span>
<span data-ttu-id="da5e7-117">Mobile Engagement 웹 SDK hello 네이티브 JSON 인코딩 및 디코딩, 또한: toocross 도메인 AJAX 요청 (hello W3C CORS 사양에 의존)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="da5e7-118">브라우저를 수행 하는 hello와 호환 되는지:</span><span class="sxs-lookup"><span data-stu-id="da5e7-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="da5e7-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="da5e7-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="da5e7-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="da5e7-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="da5e7-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="da5e7-121">Firefox 3.5+</span></span>
* <span data-ttu-id="da5e7-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="da5e7-122">Chrome 4+</span></span>
* <span data-ttu-id="da5e7-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="da5e7-123">Safari 6+</span></span>
* <span data-ttu-id="da5e7-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="da5e7-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="da5e7-125">Mobile Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="da5e7-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="da5e7-126">전역 만드는 스크립트를 작성 `azureEngagement` hello 다음 예제와 같이 JavaScript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="da5e7-127">사이트에 여러 개의 페이지가 있을 수 있으므로 이 예제에서는 이 스크립트가 모든 페이지에 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="da5e7-128">이 예제에서는 hello JavaScript 개체 이름은 `azure-engagement-conf.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="da5e7-129">hello `connectionString` hello Azure 포털을 응용 프로그램에 표시 됩니다에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="da5e7-130">`appVersionName` 및 `appVersionCode`는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="da5e7-131">그러나 분석할 때 프로세스 버전 정보가 처리될 수 있도록 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="da5e7-132">페이지에 Mobile Engagement 스크립트 포함</span><span class="sxs-lookup"><span data-stu-id="da5e7-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="da5e7-133">Mobile Engagement 스크립트 tooyour 페이지 hello 같은 방법으로 다음 중 하나에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="da5e7-134">또는 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="da5e7-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="da5e7-135">Alias</span><span class="sxs-lookup"><span data-stu-id="da5e7-135">Alias</span></span>
<span data-ttu-id="da5e7-136">Hello 만듭니다 hello Mobile Engagement 웹 SDK 스크립트를 로드 한 다음 **engagement** 별칭 tooaccess hello SDK Api입니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="da5e7-137">이 별칭 toodefine hello SDK 구성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="da5e7-138">이 별칭은 이 설명서에서 참조로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="da5e7-139">Note는 hello 기본 별칭 충돌 페이지에서 다른 전역 변수를 재정의할 수 hello 구성에서 다음과 같이 hello Mobile Engagement 웹 SDK를 로드 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="da5e7-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="da5e7-140">기본 보고</span><span class="sxs-lookup"><span data-stu-id="da5e7-140">Basic reporting</span></span>
<span data-ttu-id="da5e7-141">Mobile Engagement의 기본 보고 기능에는 사용자, 세션, 활동 및 작동 중단에 대한 통계와 같은 세션 수준 통계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="da5e7-142">세션 추적</span><span class="sxs-lookup"><span data-stu-id="da5e7-142">Session tracking</span></span>
<span data-ttu-id="da5e7-143">Mobile Engagement 세션은 일련의 활동으로 나뉘며 각각이 이름으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="da5e7-144">기존 웹 사이트는 사이트의 각 페이지에서 서로 다른 활동을 선언하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="da5e7-145">웹 사이트 또는 웹 응용 프로그램의 어떤 hello에서 현재 페이지는 바뀌지 경우 hello 페이지 내에서 같은 소규모, tootrack hello 활동을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="da5e7-146">하거나, toostart 또는 변경 hello 현재 사용자 작업을 호출 hello `engagement.agent.startActivity` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="da5e7-147">예:</span><span class="sxs-lookup"><span data-stu-id="da5e7-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="da5e7-148">Mobile Engagement 서버 hello hello 응용 프로그램 페이지를 닫은 후 3 분 이내 세션이 열린를 자동으로 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="da5e7-149">또는 `engagement.agent.endActivity`를 호출하여 세션을 수동으로 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="da5e7-150">이 옵션은 현재 사용자 활동 too'Idle hello 설정 합니다.'</span><span class="sxs-lookup"><span data-stu-id="da5e7-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="da5e7-151">hello 세션 하지 않는 한 10 초 후 종료 됩니다 새 호출을 통해서도`engagement.agent.startActivity` hello 세션을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="da5e7-152">Hello 글로벌 engagement 개체에 hello 10 초 지연 시간을 다음과 같이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="da5e7-153">사용할 수 없는 `engagement.agent.endActivity` hello에 `onunload` 콜백이이 단계에서 AJAX 호출을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="da5e7-154">고급 보고</span><span class="sxs-lookup"><span data-stu-id="da5e7-154">Advanced reporting</span></span>
<span data-ttu-id="da5e7-155">필요에 따라 tooreport 응용 프로그램별 이벤트, 오류 및 작업을 하려는 경우에 toouse hello Mobile Engagement API 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="da5e7-156">Hello를 통해 Mobile Engagement API hello 액세스 `engagement.agent` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="da5e7-157">모든 hello 고급 hello Mobile Engagement API에서에서 Mobile Engagement의 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="da5e7-158">hello API hello 문서에 자세히 설명 되어 [어떻게 toouse hello 고급 Mobile Engagement 웹 응용 프로그램에서 API 태깅](mobile-engagement-web-use-engagement-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="da5e7-159">AJAX 호출에 사용 되는 hello Url을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="da5e7-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="da5e7-160">Mobile Engagement 웹 SDK를 사용 하 여 해당 hello Url을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="da5e7-161">예를 들어 tooredefine hello 로그 URL (hello SDK 끝점 로깅에 대 한), hello 구성을 재정의할 수 있습니다 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="da5e7-162">URL 함수로 시작 하는 문자열을 반환 하는 경우 `/`, `//`, `http://`, 또는 `https://`, hello 기본 스키마가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="da5e7-163">기본적으로 hello `https://` 구성표 해당 Url에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="da5e7-164">Toocustomize hello 기본 체계를 사용 하도록 하려는 경우 다음과 같이 hello 구성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="da5e7-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
