---
title: "Unity Android 배포에 대 한 Azure Mobile Engagement와 시작 됨 aaaGet"
description: "자세한 내용은 방법 tooiOS 장치를 배포 하는 Unity 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
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
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="f8aab-103">Unity Android 배포용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="f8aab-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="f8aab-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 앱 사용량과 tooan Android 장치를 배포할 때 Unity 응용 프로그램의 알림을 toosegmented 사용자 밀어넣기 toosend 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="f8aab-105">이 자습서에서는 hello 클래식 Unity 롤 볼 자습서 hello 시작 지점으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="f8aab-106">이 hello 단계를 수행 해야 [자습서](mobile-engagement-unity-roll-a-ball.md) hello 자습서 아래 전시 우리는 Mobile Engagement 통합 hello 계속 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="f8aab-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="f8aab-107">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="f8aab-108">Unity 편집기</span><span class="sxs-lookup"><span data-stu-id="f8aab-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="f8aab-109">Mobile Engagement Unity SDK</span><span class="sxs-lookup"><span data-stu-id="f8aab-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="f8aab-110">Google Android SDK</span><span class="sxs-lookup"><span data-stu-id="f8aab-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="f8aab-111">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f8aab-112">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f8aab-113">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8aab-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="f8aab-114"><a id="setup-azme"></a>Android 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="f8aab-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="f8aab-115"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="f8aab-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="f8aab-116">Hello Unity 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="f8aab-116">Import hello Unity package</span></span>
1. <span data-ttu-id="f8aab-117">Hello 다운로드 [Mobile Engagement Unity 패키지](https://aka.ms/azmeunitysdk) 고 tooyour 로컬 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="f8aab-118">너무 이동**자산 패키지 가져오기-> 사용자 지정 패키지->** 및 선택 hello 패키지 단계 위에 hello을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="f8aab-119">모든 파일을 선택했는지 확인하고 **가져오기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="f8aab-120">가져오기에 성공 하려면 프로젝트의 가져온 hello SDK 파일 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="f8aab-121">Hello EngagementConfiguration 업데이트</span><span class="sxs-lookup"><span data-stu-id="f8aab-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="f8aab-122">Hello를 열고 **EngagementConfiguration** hello SDK 폴더 및 update hello에서 스크립트 파일 **ANDROID\_연결\_문자열** hello 연결 문자열에서 가져온 Azure 포털 안녕하세요 이전 버전에서.</span><span class="sxs-lookup"><span data-stu-id="f8aab-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="f8aab-123">Hello 파일 저장</span><span class="sxs-lookup"><span data-stu-id="f8aab-123">Save hello file</span></span> 
3. <span data-ttu-id="f8aab-124">**파일 -> Engagement -> Android 매니페스트 생성**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="f8aab-125">Mobile Engagement SDK hello로 추가 하는 hello 플러그 인이 고 클릭 하 여 프로젝트 설정을 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="f8aab-126">Hello는 업데이트할 때마다 있는지 tooexecute이 확인 **EngagementConfiguration** 파일 그렇지 않으면 hello 응용 프로그램에서 변경 내용을 반영 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="f8aab-127">기본 추적에 대 한 hello 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="f8aab-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="f8aab-128">Hello를 열고 **PlayerController** 스크립트가 편집을 위해 toohello 플레이어 개체를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="f8aab-129">Hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f8aab-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="f8aab-130">Hello toohello 다음 추가 `Start()` 메서드</span><span class="sxs-lookup"><span data-stu-id="f8aab-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="f8aab-131">배포 하 고 hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="f8aab-131">Deploy and run hello app</span></span>
<span data-ttu-id="f8aab-132">Android SDK가이 Unity 앱 tooyour 장치 toodeploy를 시도 하기 전에 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="f8aab-133">Android 장치 tooyour 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="f8aab-134">**파일 -> 빌드 설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="f8aab-135">**Android**를 선택한 후 **플랫폼 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="f8aab-136">**플레이어 설정** 을 클릭하고 유효한 번들 식별자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="f8aab-137">마지막으로 **빌드 및 실행**</span><span class="sxs-lookup"><span data-stu-id="f8aab-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="f8aab-138">수 tooprovide 폴더 이름 toostore hello Android 패키지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="f8aab-139">모든 작업이 제대로 hello 패키지 되는 연결 된 배포 tooyour 경우가 경우 장치의 휴대폰에서 Unity 게임을 표시 됩니다!</span><span class="sxs-lookup"><span data-stu-id="f8aab-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="f8aab-140"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="f8aab-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="f8aab-141"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="f8aab-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="f8aab-142">Hello EngagementConfiguration 업데이트</span><span class="sxs-lookup"><span data-stu-id="f8aab-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="f8aab-143">Hello를 열고 **EngagementConfiguration** hello SDK 폴더 및 update hello에서 스크립트 파일 **ANDROID\_GOOGLE\_번호** hello로 **Google 프로젝트 번호** hello Google 클라우드 개발자 포털에서 이전에 얻은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="f8aab-144">이 문자열 값 이므로 tooenclose 있는지 확인 해야 큰따옴표에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="f8aab-145">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-145">Save hello file.</span></span> 
3. <span data-ttu-id="f8aab-146">**파일 -> Engagement -> Android 매니페스트 생성**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="f8aab-147">Mobile Engagement SDK hello로 추가 하는 hello 플러그 인이 고 클릭 하 여 프로젝트 설정을 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="f8aab-148">Hello 앱 tooreceive 알림 구성</span><span class="sxs-lookup"><span data-stu-id="f8aab-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="f8aab-149">Hello를 열고 **PlayerController** 스크립트가 편집을 위해 toohello 플레이어 개체를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="f8aab-150">Hello toohello 다음 추가 `Start()` 메서드</span><span class="sxs-lookup"><span data-stu-id="f8aab-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="f8aab-151">Hello 응용 프로그램을 업데이트 했으므로 배포 하 고 장치 hello 지침 아래에 제공 된 기준에 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8aab-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

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
