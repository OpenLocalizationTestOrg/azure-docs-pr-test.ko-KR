---
title: "Web Apps용 Azure Mobile Engagement 시작 | Microsoft Docs"
description: "Web Apps에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: abcb04e4e0a3ae4fdba3a4ded20b3846ac3b21e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="d8f6c-103">Web Apps용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="d8f6c-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d8f6c-104">이 항목에서는 Azure Mobile Engagement를 사용하여 웹앱 사용량을 파악하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="d8f6c-105">Azure Mobile Engagement 서비스는 2018년 3월에 사용 중지되며 현재 기존 고객에게만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d8f6c-106">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="d8f6c-107">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="d8f6c-108">Visual Studio 2015 또는 원하는 다른 편집기</span><span class="sxs-lookup"><span data-stu-id="d8f6c-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="d8f6c-109">웹 SDK</span><span class="sxs-lookup"><span data-stu-id="d8f6c-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="d8f6c-110">이 웹 SDK는 미리 보기 상태이며 현재 분석을 지원하고 브라우저 또는 앱 내 푸시 알림을 보내도록 아직 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-110">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="d8f6c-111">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d8f6c-112">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d8f6c-113">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="d8f6c-114">웹앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="d8f6c-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d8f6c-115"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d8f6c-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="d8f6c-116">이 자습서에서는 데이터를 수집하는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-116">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span></span>

<span data-ttu-id="d8f6c-117">Visual Studio로 기본 웹앱을 만들어 통합을 보여 주지만 Visual Studio 외부에서 만든 웹 응용 프로그램으로 모든 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-117">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="d8f6c-118">새 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d8f6c-118">Create a new Web App</span></span>
<span data-ttu-id="d8f6c-119">다음 단계에서는 Visual Studio 2015를 사용한다고 가정하지만 이전 버전의 Visual Studio에서도 단계는 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-119">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="d8f6c-120">Visual Studio를 시작하고 **홈** 화면에서 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-120">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="d8f6c-121">팝업에서 **웹** -> **ASP.Net 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-121">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="d8f6c-122">앱 **이름**, **위치** 및 **솔루션 이름**을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-122">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="d8f6c-123">**템플릿 선택** 팝업의 **ASP.Net 4.5 템플릿**에서 **비어 있음**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-123">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="d8f6c-124">이제 Azure Mobile Engagement 웹 SDK를 통합할 새 비어 있는 웹앱 프로젝트가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-124">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="d8f6c-125">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d8f6c-125">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="d8f6c-126">솔루션에 **javascript**라는 새 폴더를 만들고 **azure-engagement.js**라는 웹 SDK JS 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-126">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="d8f6c-127">다음 코드를 사용하여 이 javascript 폴더에 **main.js** 라는 새 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-127">Add a new file called **main.js** in this javascript folder with the following code.</span></span> <span data-ttu-id="d8f6c-128">연결 문자열을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-128">Make sure to update the connection string.</span></span> <span data-ttu-id="d8f6c-129">`azureEngagement` 개체는 웹 SDK 메서드에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-129">This `azureEngagement` object will be used to access Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![js 파일이 포함된 Visual Studio입니다.][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="d8f6c-131">실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="d8f6c-131">Enable real-time monitoring</span></span>
<span data-ttu-id="d8f6c-132">데이터 보내기를 시작하고 사용자가 활성 상태인지 확인하려면 Mobile Engagement 백 엔드에 작업을 하나 이상 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-132">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span></span> <span data-ttu-id="d8f6c-133">웹앱의 컨텍스트에 있는 작업은 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-133">An activity in the context of a web app is a web page.</span></span> 

1. <span data-ttu-id="d8f6c-134">솔루션에서 **home.html** 라는 새 페이지를 만들고 웹앱에 대한 페이지의 시작으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-134">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span></span> 
2. <span data-ttu-id="d8f6c-135">본문 태그 안에 다음을 추가하여 이전에 이 페이지에 추가한 두 javascript를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-135">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="d8f6c-136">본문 태그를 업데이트하여 EngagementAgent의 `startActivity` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-136">Update the body tag to call EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="d8f6c-137">**home.html**은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="d8f6c-138">실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d8f6c-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="d8f6c-139">분석 확장</span><span class="sxs-lookup"><span data-stu-id="d8f6c-139">Extend analytics</span></span>
<span data-ttu-id="d8f6c-140">현재 분석에 사용할 수 있는 웹 SDK와 함께 사용할 수 있는 모든 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8f6c-140">Here are all the methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="d8f6c-141">작업/웹 페이지:</span><span class="sxs-lookup"><span data-stu-id="d8f6c-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="d8f6c-142">이벤트</span><span class="sxs-lookup"><span data-stu-id="d8f6c-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="d8f6c-143">오류</span><span class="sxs-lookup"><span data-stu-id="d8f6c-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="d8f6c-144">작업</span><span class="sxs-lookup"><span data-stu-id="d8f6c-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

