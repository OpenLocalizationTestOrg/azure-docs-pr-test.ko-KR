---
title: "Windows Phone Silverlight 앱용 Azure Mobile Engagement 시작"
description: "Windows Phone Silverlight 앱에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="82cf5-103">Windows Phone Silverlight 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="82cf5-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="82cf5-104">이 항목에서는 Azure Mobile Engagement를 사용하여 Windows Phone Silverlight 응용 프로그램에서 구분된 사용자에게 푸시 알림을 보내고 앱 사용량을 파악하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="82cf5-105">이 자습서에서는 Mobile Engagement를 사용하는 간단한 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="82cf5-106">여기서는 MPNS(Microsoft 푸시 알림 서비스)를 사용하여 푸시 알림을 받고 기본적인 데이터를 수집하는 빈 Windows Phone Silverlight 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="82cf5-107">Azure Mobile Engagement 서비스는 2018년 3월에 사용 중지되며 현재 기존 고객에게만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="82cf5-108">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82cf5-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="82cf5-109">Windows Phone 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="82cf5-110">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82cf5-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="82cf5-111">Windows Phone 8.1(비 Silverlight)을 대상으로 하는 경우 [Windows 유니버설 자습서](mobile-engagement-windows-store-dotnet-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82cf5-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="82cf5-112">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="82cf5-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="82cf5-113">Visual Studio 2013</span></span>
* <span data-ttu-id="82cf5-114">[MicrosoftAzure.MobileEngagement] Nuget 패키지</span><span class="sxs-lookup"><span data-stu-id="82cf5-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="82cf5-115">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="82cf5-116">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="82cf5-117">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82cf5-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="82cf5-118"><a id="setup-azme"></a>Windows Phone 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="82cf5-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="82cf5-119"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="82cf5-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="82cf5-120">이 자습서에서는 데이터를 수집하고 푸시 알림을 보내는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="82cf5-121">전체 통합 설명서는 [Mobile Engagement Windows Phone SDK 통합](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="82cf5-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="82cf5-122">여기서는 통합을 시연하기 위해 Visual Studio를 사용하여 기본적인 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="82cf5-123">새 Windows Phone Silverlight 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="82cf5-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="82cf5-124">다음 단계에서는 Visual Studio 2015를 사용한다고 가정하지만 이전 버전의 Visual Studio에서도 단계는 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="82cf5-125">Visual Studio를 시작하고 **홈** 화면에서 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="82cf5-126">팝업에서 **Windows 8** -> **Windows Phone** -> **비어 있는 앱(Windows Phone Silverlight)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="82cf5-127">앱 **이름** 및 **솔루션 이름**을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="82cf5-128">**Windows Phone 8.0** 또는 **Windows Phone 8.1**을 대상으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="82cf5-129">이제 Azure Mobile Engagement SDK를 통합할 새 Windows Phone Silverlight 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="82cf5-130">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="82cf5-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="82cf5-131">프로젝트에서 [MicrosoftAzure.MobileEngagement] Nuget 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="82cf5-132">Properties 폴더 아래에 있는 `WMAppManifest.xml`을 열고 `<Capabilities />` 태그에 다음이 선언되어 있는지 확인합니다(선언되어 있지 않은 경우 추가).</span><span class="sxs-lookup"><span data-stu-id="82cf5-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="82cf5-133">이제 앞서 Mobile Engagement 앱에 대해 복사한 연결 문자열을 `Resources\EngagementConfiguration.xml` 파일의 `<connectionString>` 태그와 `</connectionString>` 태그 사이에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="82cf5-134">파일 `App.xaml.cs`에서:</span><span class="sxs-lookup"><span data-stu-id="82cf5-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="82cf5-135">a.</span><span class="sxs-lookup"><span data-stu-id="82cf5-135">a.</span></span> <span data-ttu-id="82cf5-136">`using` 구문 추가:</span><span class="sxs-lookup"><span data-stu-id="82cf5-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="82cf5-137">b.</span><span class="sxs-lookup"><span data-stu-id="82cf5-137">b.</span></span> <span data-ttu-id="82cf5-138">SDK를 `Application_Launching` 메서드에서 초기화:</span><span class="sxs-lookup"><span data-stu-id="82cf5-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="82cf5-139">c.</span><span class="sxs-lookup"><span data-stu-id="82cf5-139">c.</span></span> <span data-ttu-id="82cf5-140">다음 코드를 `Application_Activated`에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="82cf5-141"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="82cf5-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="82cf5-142">데이터 보내기를 시작하고 사용자가 활성 상태인지 확인하려면 Mobile Engagement 백 엔드에 화면(활동)을 하나 이상 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="82cf5-143">MainPage.xaml.cs에서 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="82cf5-144">**PhoneApplicationPage** 앞에 있는 **MainPage**의 기본 클래스를 **EngagementPage**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="82cf5-145">`MainPage.xml` 파일에서:</span><span class="sxs-lookup"><span data-stu-id="82cf5-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="82cf5-146">a.</span><span class="sxs-lookup"><span data-stu-id="82cf5-146">a.</span></span> <span data-ttu-id="82cf5-147">다음 줄을 네임스페이스 선언에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="82cf5-148">b.</span><span class="sxs-lookup"><span data-stu-id="82cf5-148">b.</span></span> <span data-ttu-id="82cf5-149">XML 태그 이름의 `phone:PhoneApplicationPage`를 `engagement:EngagementPage`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="82cf5-150"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="82cf5-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="82cf5-151"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="82cf5-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="82cf5-152">Mobile Engagement에서는 캠페인 컨텍스트에서 푸시 알림 및 앱 내 메시징을 사용하여 사용자와 상호 작용하고 사용자에게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="82cf5-153">Mobile Engagement 포털에서는 이 모듈을 도달률이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="82cf5-154">다음 섹션에서는 이러한 알림과 메시지를 받도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="82cf5-155">MPNS 푸시 알림을 받도록 앱 설정</span><span class="sxs-lookup"><span data-stu-id="82cf5-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="82cf5-156">새 기능을 `WMAppManifest.xml` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="82cf5-157">도달률 SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="82cf5-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="82cf5-158">다음과 같이 `App.xaml.cs`에서 에이전트 초기화 직후 **Application_Launching** 함수의 `EngagementReach.Instance.Init();`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="82cf5-159">다음과 같이 `App.xaml.cs`에서 에이전트 초기화 직후 **Application_Activated** 함수의 `EngagementReach.Instance.OnActivated(e);`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="82cf5-160">모든 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-160">You're all set.</span></span> <span data-ttu-id="82cf5-161">이제 이 기본 통합을 제대로 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="82cf5-162"><a id="send"></a>앱에 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="82cf5-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="82cf5-163">이제 앱이 열려 있는 경우 앱 내 알림으로 표시되고 그렇지 않을 경우 알림 메시지로 표시되는 알림이 장치에 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="82cf5-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="82cf5-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="82cf5-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
