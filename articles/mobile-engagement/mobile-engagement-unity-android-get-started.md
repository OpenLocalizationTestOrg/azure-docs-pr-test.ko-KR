---
title: "Unity Android 배포용 Azure Mobile Engagement 시작"
description: "iOS 장치에 Unity 앱을 배포하는 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="e7b58-103">Unity Android 배포용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="e7b58-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e7b58-104">이 항목에서는 Azure Mobile Engagement를 사용하여 앱 사용법을 이해하고 Android 장치에 배포할 때 Unity 응용 프로그램의 분할된 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="e7b58-105">이 자습서에서는 클래식 Unity Roll a Ball 자습서를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="e7b58-106">아래 자습서에서 소개하는 Mobile Engagement 통합을 진행하기 전에 이 [자습서](mobile-engagement-unity-roll-a-ball.md) 의 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="e7b58-107">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="e7b58-108">Unity 편집기</span><span class="sxs-lookup"><span data-stu-id="e7b58-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="e7b58-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="e7b58-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="e7b58-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="e7b58-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="e7b58-111">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e7b58-112">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e7b58-113">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7b58-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="e7b58-114"><a id="setup-azme"></a>Android 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="e7b58-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e7b58-115"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e7b58-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="e7b58-116">Unity 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="e7b58-116">Import the Unity package</span></span>
1. <span data-ttu-id="e7b58-117">[Mobile Engagement Unity 패키지](https://aka.ms/azmeunitysdk) 를 다운로드하고 이를 로컬 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="e7b58-118">**자산 -> 패키지 가져오기 -> 사용자 지정 패키지**로 이동하고 위의 단계에서 다운로드한 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="e7b58-119">모든 파일을 선택했는지 확인하고 **가져오기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="e7b58-120">가져오기에 성공하면 가져온 SDK 파일이 프로젝트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="e7b58-121">EngagementConfiguration 업데이트</span><span class="sxs-lookup"><span data-stu-id="e7b58-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="e7b58-122">SDK 폴더에서 **EngagementConfiguration** 스크립트 파일을 열고 **ANDROID\_CONNECTION\_STRING**을 Azure Portal에서 이전에 가져온 연결 문자열로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="e7b58-123">파일 저장</span><span class="sxs-lookup"><span data-stu-id="e7b58-123">Save the file</span></span> 
3. <span data-ttu-id="e7b58-124">**파일 -> Engagement -> Android 매니페스트 생성**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="e7b58-125">Mobile Engagement SDK에 의해 추가된 플러그 인이며 이를 클릭하면 프로젝트 설정이 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="e7b58-126">**EngagementConfiguration** 파일을 업데이트할 때마다 이를 실행해야 하며 그렇지 않으면 앱에 변경 내용이 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="e7b58-127">기본 추적을 위한 앱 구성</span><span class="sxs-lookup"><span data-stu-id="e7b58-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="e7b58-128">편집을 위해 Player 개체에 연결된 **PlayerController** 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="e7b58-129">다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="e7b58-130">다음을 `Start()` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="e7b58-131">앱 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="e7b58-131">Deploy and run the app</span></span>
<span data-ttu-id="e7b58-132">이 Unity 앱을 장치에 배포하려고 시도하기 전에 Android SDK가 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="e7b58-133">Android 장치를 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="e7b58-134">**파일 -> 빌드 설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="e7b58-135">**Android**를 선택한 후 **플랫폼 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="e7b58-136">**플레이어 설정** 을 클릭하고 유효한 번들 식별자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="e7b58-137">마지막으로 **빌드 및 실행**</span><span class="sxs-lookup"><span data-stu-id="e7b58-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="e7b58-138">Android 패키지를 저장할 폴더 이름을 입력하라는 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="e7b58-139">모든 항목이 제대로 진행되면 패키지가 연결된 장치에 배포되고 Unity 게임이 휴대폰에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="e7b58-140"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="e7b58-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e7b58-141"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="e7b58-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="e7b58-142">EngagementConfiguration 업데이트</span><span class="sxs-lookup"><span data-stu-id="e7b58-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="e7b58-143">SDK 폴더에서 **EngagementConfiguration** 스크립트 파일을 열고 **ANDROID\_GOOGLE\_NUMBER**를 Google Cloud Developer 포털에서 이전에 가져온 **Google Project Number**로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="e7b58-144">이 문자열 값은 큰따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="e7b58-145">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-145">Save the file.</span></span> 
3. <span data-ttu-id="e7b58-146">**파일 -> Engagement -> Android 매니페스트 생성**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="e7b58-147">Mobile Engagement SDK에 의해 추가된 플러그 인이며 이를 클릭하면 프로젝트 설정이 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="e7b58-148">알림을 받도록 앱 구성</span><span class="sxs-lookup"><span data-stu-id="e7b58-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="e7b58-149">편집을 위해 Player 개체에 연결된 **PlayerController** 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="e7b58-150">다음을 `Start()` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="e7b58-151">이제 앱이 업데이트되고 아래 제공된 지침에 따라 앱을 장치에서 배포 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7b58-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
