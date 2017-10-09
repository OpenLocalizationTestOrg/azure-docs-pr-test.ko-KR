---
title: "웹 앱에 대 한 Azure Mobile Engagement 시작 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure Mobile Engagement 웹 앱에 대 한 분석 및 푸시 알림입니다."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="35e48-103">Web Apps용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="35e48-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="35e48-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 웹 응용 프로그램 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="35e48-105">hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="35e48-106">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35e48-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="35e48-107">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="35e48-108">Visual Studio 2015 또는 원하는 다른 편집기</span><span class="sxs-lookup"><span data-stu-id="35e48-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="35e48-109">웹 SDK</span><span class="sxs-lookup"><span data-stu-id="35e48-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="35e48-110">이 웹 SDK의 미리 보기에만 hello 순간에 분석 지원 및 브라우저 또는 앱에서 푸시 알림을 보내는 아직 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="35e48-111">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="35e48-112">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="35e48-113">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35e48-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="35e48-114">웹앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="35e48-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="35e48-115"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="35e48-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="35e48-116">이 자습서는 basic 통합"," hello 필요한 최소 집합 toocollect 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="35e48-117">또한 Visual Studio 외부에서 만든 모든 웹 응용 프로그램과 hello 단계를 수행 하는 경우 기본 웹 응용 프로그램을 Visual Studio toodemonstrate hello 통합으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="35e48-118">새 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="35e48-118">Create a new Web App</span></span>
<span data-ttu-id="35e48-119">hello 다음 단계에서는 가정 hello를 사용 하 여 Visual Studio 2015의 hello 단계는 이전 버전의 Visual Studio에서 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="35e48-120">Visual Studio를 시작 및 hello **홈** 화면에서 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="35e48-121">Hello 팝업에 선택 **웹** -> **ASP.Net 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="35e48-122">Hello 앱 입력 **이름**, **위치** 및 **솔루션 이름**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="35e48-123">Hello에 **´ ï ´** 선택 팝업에서 **빈** 아래 **ASP.Net 4.5 템플릿** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="35e48-124">이제는 Azure Mobile Engagement 웹 SDK hello 통합할 새 빈 웹 응용 프로그램 프로젝트를 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="35e48-125">응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="35e48-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="35e48-126">라는 새 폴더를 만들어 **javascript** 솔루션에 hello 웹 SDK JS 파일을 추가 하 고 **azure engagement.js** 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="35e48-127">라는 새 파일 추가 **main.js** 이 hello 코드 다음 javascript 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="35e48-128">있는지 tooupdate hello 연결 문자열을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="35e48-129">이 `azureEngagement` 개체를 사용 하는 tooaccess 웹 SDK 메서드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![js 파일이 포함된 Visual Studio입니다.][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="35e48-131">실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="35e48-131">Enable real-time monitoring</span></span>
<span data-ttu-id="35e48-132">순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상의 활동 toohello Mobile Engagement 백 엔드를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="35e48-133">웹 응용 프로그램의 hello 컨텍스트에서 활동은 웹 페이지.</span><span class="sxs-lookup"><span data-stu-id="35e48-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="35e48-134">호출 하는 새 페이지를 만들고 **home.html** 솔루션 및 웹 앱에 대 한 페이지 hello 시작으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="35e48-135">Hello body 태그 내 hello 다음을 추가 하 여 이전에이 페이지에에서 추가 하는 hello 두 javascript를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="35e48-136">Hello body 태그 toocall EngagementAgent 업데이트 `startActivity` 메서드</span><span class="sxs-lookup"><span data-stu-id="35e48-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="35e48-137">**home.html**은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35e48-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="35e48-138">실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="35e48-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="35e48-139">분석 확장</span><span class="sxs-lookup"><span data-stu-id="35e48-139">Extend analytics</span></span>
<span data-ttu-id="35e48-140">다음은 현재 분석에 사용할 수 있는 웹 SDK와 함께 사용할 수 있는 모든 hello 메서드:</span><span class="sxs-lookup"><span data-stu-id="35e48-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="35e48-141">작업/웹 페이지:</span><span class="sxs-lookup"><span data-stu-id="35e48-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="35e48-142">이벤트</span><span class="sxs-lookup"><span data-stu-id="35e48-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="35e48-143">오류</span><span class="sxs-lookup"><span data-stu-id="35e48-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="35e48-144">작업</span><span class="sxs-lookup"><span data-stu-id="35e48-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

