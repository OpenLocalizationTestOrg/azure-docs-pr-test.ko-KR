---
title: "aaaGet Xamarin.Android에 대 한 Azure Mobile Engagement와 시작 됨"
description: "자세한 내용은 방법 toouse 분석 및 Xamarin.Android 앱에 대 한 푸시 알림을 사용 하 여 Azure Mobile Engagement 합니다."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="9643a-103">Xamarin.Android 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="9643a-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9643a-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 앱 사용량과 toosend 밀어넣기 Xamarin.Android 응용 프로그램의 알림을 toosegmented 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="9643a-105">이 자습서에는 hello 간단한 브로드캐스트 시나리오를 Mobile Engagement를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="9643a-106">해당 시나리오에서 기본 데이터를 수집하고 GCM(Google Cloud Messaging)을 사용하여 푸시 알림을 받는 빈 Xamarin.Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="9643a-107">hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="9643a-108">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9643a-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="9643a-109">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="9643a-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="9643a-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="9643a-111">Xamarin이 포함된 Visual Studio를 사용할 수도 있지만 이 자습서에서는 Xamarin Studio를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="9643a-112">또한 설치 지침은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9643a-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="9643a-113">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="9643a-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="9643a-114">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9643a-115">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9643a-116">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9643a-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="9643a-117"><a id="setup-azme"></a>Android 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="9643a-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9643a-118"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="9643a-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="9643a-119">이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="9643a-120">Xamarin Studio toodemonstrate hello 통합 기본 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="9643a-121">새 Xamarin.Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9643a-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="9643a-122">시작 **Xamarin Studio** 너무 이동**파일** -> **새로** -> **솔루션**</span><span class="sxs-lookup"><span data-stu-id="9643a-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="9643a-123">선택 **Android 앱** hello 선택한 언어 인지를 확인 한 다음 **C#** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="9643a-124">Hello 입력 **응용 프로그램 이름** 및 hello **조직 식별자**합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="9643a-125">있는지 toocheckmark 확인 **Google Play 서비스** 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="9643a-126">업데이트 hello **프로젝트 이름**, **솔루션 이름** 및 **위치** 필요 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="9643a-127">Xamarin Studio는 Mobile Engagement 통합할 hello 앱을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="9643a-128">응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="9643a-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="9643a-129">마우스 오른쪽 단추로 클릭 하 여 hello **패키지** hello 솔루션 창과 선택에서 폴더 **패키지 추가 중...**</span><span class="sxs-lookup"><span data-stu-id="9643a-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="9643a-130">Hello에 대 한 검색 **Microsoft Azure Mobile Engagement Xamarin SDK** tooyour 솔루션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="9643a-131">열기 **MainActivity.cs** hello 다음 추가 및 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9643a-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="9643a-132">Hello에 `OnCreate` 메서드를 다음 Mobile Engagement 백 엔드와 tooinitialize hello 연결 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="9643a-133">있는지 tooadd 확인 프로그램 **ConnectionString**합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="9643a-134">권한 및 서비스 선언 추가</span><span class="sxs-lookup"><span data-stu-id="9643a-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="9643a-135">Hello를 열고 **Manifest.xml** hello 속성 폴더는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="9643a-136">Hello XML 소스를 직접 업데이트할 수 있도록 원본 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="9643a-137">이러한 사용 권한을 toohello Manifest.xml 추가 (hello 아래 있는 **속성** 폴더) 바로 앞 또는 뒤 hello 프로젝트의 `<application>` 태그:</span><span class="sxs-lookup"><span data-stu-id="9643a-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="9643a-138">Hello hello 사이 다음 추가 `<application>` 및 `</application>` toodeclare hello 에이전트 서비스 태그를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="9643a-139">붙여 넣은 hello 코드에서 대체할 `"<Your application name>"` hello 레이블에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="9643a-140">이 hello에 표시 됩니다 **설정을** 메뉴 사용자 hello 장치에서 실행 되는 서비스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="9643a-141">예를 들어 hello 단어 "서비스" 해당 레이블에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="9643a-142">화면 tooMobile Engagement 보내기</span><span class="sxs-lookup"><span data-stu-id="9643a-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="9643a-143">순서 toostart 데이터를 보내고 hello 사용자는 활성 하나 이상 화면 toohello Mobile Engagement 백 엔드를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="9643a-144">이 작업을 위한-해당 hello 확인 `MainActivity` 에서 상속 `EngagementActivity` 대신 `Activity`합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="9643a-145">또는 `EngagementActivity`에서 상속할 수 없는 경우 `OnResume` 및 `OnPause`에 각각 `.StartActivity` 및 `.EndActivity` 메서드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="9643a-146"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="9643a-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9643a-147"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="9643a-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9643a-148">Mobile Engagement와 toointeract 있으며 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용자에 게 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="9643a-149">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="9643a-150">다음 섹션 hello에 응용 프로그램 tooreceive를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9643a-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
