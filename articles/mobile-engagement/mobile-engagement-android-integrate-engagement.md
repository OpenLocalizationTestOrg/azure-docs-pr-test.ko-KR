---
title: "Azure Mobile Engagement Android SDK 통합"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="d3c8b-103">Android에서 Engagement를 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="d3c8b-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3c8b-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="d3c8b-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="d3c8b-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d3c8b-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d3c8b-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d3c8b-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d3c8b-107">Android</span><span class="sxs-lookup"><span data-stu-id="d3c8b-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="d3c8b-108">이 절차는 Android 응용 프로그램에서 Engagement의 분석 및 모니터링 기능을 활성화하는 가장 간단한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3c8b-109">Android SDK API의 최소 수준은 10 이상(Android 2.3.3 이상)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="d3c8b-110">다음 단계를 통해 사용자, 세션, 작업, 크래시 및 기술과 관련된 모든 통계를 계산하는 데 필요한 로그의 보고서를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="d3c8b-111">이벤트, 오류, 작업 등의 기타 통계는 응용 프로그램별로 다르므로, 해당 통계를 계산하는 데 필요한 로그 보고는 Engagement API를 사용하여 수동으로 수행해야 합니다. 관련 설명은 [Android에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-android-use-engagement-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="d3c8b-112">Android 프로젝트에 Engagement SDK 및 서비스 포함</span><span class="sxs-lookup"><span data-stu-id="d3c8b-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="d3c8b-113">[여기](https://aka.ms/vq9mfn)에서 Android SDK를 다운로드합니다. `mobile-engagement-VERSION.jar`을 가져와서 Android 프로젝트의 폴더에 넣습니다(`libs` 폴더가 아직 존재하지 않는 경우 생성).</span><span class="sxs-lookup"><span data-stu-id="d3c8b-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3c8b-114">ProGuard로 응용 프로그램 패키지를 빌드하는 경우 일부 클래스를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="d3c8b-115">다음 구성 코드 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="d3c8b-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="d3c8b-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="d3c8b-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="d3c8b-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="d3c8b-118">시작 관리자 작업에서 다음 메서드를 호출하여 Engagement 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d3c8b-119">응용 프로그램의 연결 문자열은 Azure 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="d3c8b-120">없는 경우 다음 Android 권한을 `<application>` 태그 앞에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="d3c8b-121">`<application>` 태그와 `</application>` 태그 사이에 다음 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="d3c8b-122">`<Your application name>`은(는) 응용 프로그램의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="d3c8b-123">`android:label` 특성을 통해 휴대폰의 "서비스 실행 중" 화면에서 최종 사용자에게 표시될 참여 서비스의 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="d3c8b-124">이 특성을 `"<Your application name>Service"`(예: `"AcmeFunGameService"`)(으)로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="d3c8b-125">또한 `android:process` 특성을 지정하면 Engagement 서비스가 자체 프로세스에서 실행됩니다. 그리고 응용 프로그램과 동일한 프로세스에서 Engagement를 실행하면 주/UI 스레드의 응답성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="d3c8b-126">`Application.onCreate()` 및 기타 응용 프로그램 콜백에 배치한 코드는 Engagement 서비스를 비롯하여 모든 응용 프로그램 프로세스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="d3c8b-127">이로 인해 Engagement 프로세스, 중복 브로드캐스트 수신기 또는 서비스에서의 불필요한 메모리 할당 및 스레드와 같은 원치 않는 부작용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="d3c8b-128">`Application.onCreate()`을(를) 재정의하는 경우 `Application.onCreate()` 함수의 시작 부분에 다음 코드 조각을 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="d3c8b-129">그리고 `Application.onTerminate()`, `Application.onLowMemory()` 및 `Application.onConfigurationChanged(...)`에 대해 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="d3c8b-130">또한 `Application`을(를) 확장하는 대신 `EngagementApplication`을(를) 확장할 수도 있습니다. 콜백 `Application.onCreate()`은(는) 프로세스 검사를 수행하고 현재 프로세스가 Engagement 서비스를 호스트하는 프로세스가 아닌 경우에만 `Application.onApplicationProcessCreate()`을(를) 호출합니다. 그리고 다른 콜백에 대해서도 동일한 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="d3c8b-131">기본 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="d3c8b-132">권장 방법: `Activity` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="d3c8b-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="d3c8b-133">Engagement에서 사용자, 세션, 작업, 충돌 및 기술 통계를 계산하는 데 필요한 모든 로그의 보고서를 활성화하려면 모든 `*Activity` 하위 클래스가 해당 `Engagement*Activity` 클래스에서 상속하도록 설정해야 합니다. 예를 들어 레거시 작업이 `ListActivity`을(를) 확장하는 경우 `EngagementListActivity`을(를) 확장하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="d3c8b-134">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="d3c8b-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="d3c8b-135">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="d3c8b-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="d3c8b-136">`EngagementListActivity` 또는 `EngagementExpandableListActivity`을(를) 사용할 경우 `super.onCreate(...);`을(를) 호출하기 전에 `requestWindowFeature(...);`을(를) 호출해야 합니다. 그렇지 않으면 충돌이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="d3c8b-137">이러한 클래스는 `src` 폴더에서 찾을 수 있으며 프로젝트에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="d3c8b-138">또한 클래스는 **JavaDoc**에도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="d3c8b-139">대체 방법: `startActivity()` 및 `endActivity()` 수동 호출</span><span class="sxs-lookup"><span data-stu-id="d3c8b-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="d3c8b-140">`Activity` 클래스를 오버로드할 수 없거나 오버로드하지 않으려는 경우 `EngagementAgent`의 메서드를 직접 호출하여 작업을 시작하고 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3c8b-141">Android SDK는 응용 프로그램이 닫힐 때에도 `endActivity()` 메서드를 호출하지 않습니다(Android에서 응용 프로그램은 실제로 닫히지 않음).</span><span class="sxs-lookup"><span data-stu-id="d3c8b-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="d3c8b-142">따라서 *모든* 작업의 `onResume` 콜백에서는 `startActivity()` 메서드를, *모든* 작업의 `onPause()` 콜백에서는 `endActivity()` 메서드를 호출하는 것이 *상당히* 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="d3c8b-143">이것이 세션이 손실되지 않도록 하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="d3c8b-144">세션이 손실되는 경우 Engagement 서비스의 Engagement 백 엔드에 대한 연결이 끊기지 않습니다(세션이 보류 중인 한 서비스가 연결된 상태를 유지하므로).</span><span class="sxs-lookup"><span data-stu-id="d3c8b-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="d3c8b-145">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="d3c8b-146">이 예제는 `EngagementActivity` 클래스 및 해당 변형과 매우 비슷합니다. 해당 소스 코드는 `src` 폴더에 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="d3c8b-147">테스트</span><span class="sxs-lookup"><span data-stu-id="d3c8b-147">Test</span></span>
<span data-ttu-id="d3c8b-148">이제 에뮬레이터와 장치에서 모바일 앱을 실행하고 모니터 탭에서 세션을 등록하는지 확인하여 통합을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="d3c8b-149">다음 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="d3c8b-150">위치 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-150">Location reporting</span></span>
<span data-ttu-id="d3c8b-151">위치가 보고되도록 하려는 경우 몇 줄의 구성을 `<application>` 태그와 `</application>` 태그 사이에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="d3c8b-152">지연 영역 위치 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-152">Lazy area location reporting</span></span>
<span data-ttu-id="d3c8b-153">지연 영역 위치 보고를 통해 국가, 지역 및 장치와 연결된 위치를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="d3c8b-154">이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="d3c8b-155">장치 영역은 세션당 한번 이하로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="d3c8b-156">GPS는 전혀 사용되지 않으므로 이러한 위치 보고는 배터리에 거의 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="d3c8b-157">보고된 영역은 사용자, 세션, 이벤트 및 오류에 대한 지리적 통계를 계산 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="d3c8b-158">이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="d3c8b-159">지연 영역 위치 보고를 사용하도록 설정하려면 이 절차의 앞에서 설명한 구성을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d3c8b-160">또한 아직 없는 경우 다음 권한도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="d3c8b-161">또는 응용 프로그램에서 이미 사용하고 있는 경우 ``ACCESS_FINE_LOCATION`` 을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="d3c8b-162">실시간 위치 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-162">Real time location reporting</span></span>
<span data-ttu-id="d3c8b-163">실시간 위치 보고를 통해 장치와 연결된 위도와 경도를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="d3c8b-164">기본적으로 이 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용하고, 보고는 응용 프로그램이 포그라운드로 실행될 때(즉, 세션 중)만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="d3c8b-165">실시간 위치는 통계를 계산하는 데 사용되지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="d3c8b-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="d3c8b-166">유일한 용도는 도달률 캠페인에서 실시간 지리적 펜스 \<Reach-Audience-geofencing\> 사용을 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="d3c8b-167">실시간 위치 보고를 사용하도록 설정하려면 이 절차의 앞에서 설명한 구성을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d3c8b-168">또한 아직 없는 경우 다음 권한도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="d3c8b-169">또는 응용 프로그램에서 이미 사용하고 있는 경우 ``ACCESS_FINE_LOCATION`` 을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="d3c8b-170">GPS 기반 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-170">GPS based reporting</span></span>
<span data-ttu-id="d3c8b-171">기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="d3c8b-172">훨씬 더 정밀한 GPS 기반 위치의 사용을 설정하려면 구성 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d3c8b-173">또한 아직 없는 경우 다음 권한도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="d3c8b-174">백그라운드 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-174">Background reporting</span></span>
<span data-ttu-id="d3c8b-175">기본적으로 실시간 위치 보고는 응용 프로그램이 포그라운드로 실행되는 경우(즉, 세션 중)에만 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="d3c8b-176">백그라운드에서도 보고를 활성화하려면 구성 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="d3c8b-177">응용 프로그램이 백그라운드에서 실행될 때 GPS를 활성화한 경우에도 네트워크 기반 위치만 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="d3c8b-178">백그라운드 위치 보고는 사용자가 해당 장치를 재부팅하는 경우 중지됩니다. 다음을 추가하면 부팅 시 자동으로 다시 시작하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="d3c8b-179">또한 아직 없는 경우 다음 권한도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="d3c8b-180">Android M 권한</span><span class="sxs-lookup"><span data-stu-id="d3c8b-180">Android M permissions</span></span>
<span data-ttu-id="d3c8b-181">Android M부터는 일부 권한이 런타임 시 관리되며 사용자 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="d3c8b-182">Android API Level 23을 대상으로 하는 경우 새 앱 설치에 대해서는 기본적으로 런타임 권한이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="d3c8b-183">그렇지 않으면 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="d3c8b-184">사용자는 장치 설정 메뉴에서 이러한 권한을 설정/해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="d3c8b-185">시스템 메뉴에서 권한을 해제하면 응용 프로그램의 백그라운드 프로세스가 중단되며 이것은 시스템 동작으로 백그라운드로 푸시 알림을 받는 기능에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="d3c8b-186">Mobile Engagement의 컨텍스트에서 런타임 시 승인이 필요한 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="d3c8b-187">`WRITE_EXTERNAL_STORAGE` (이에 대한 Android API Level 23을 대상으로 할 때만 해당)</span><span class="sxs-lookup"><span data-stu-id="d3c8b-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="d3c8b-188">외부 저장소는 도달률 큰 그림 기능에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="d3c8b-189">사용자에게 이 권한을 요청하는 것이 번거롭다고 생각되는 경우, 큰 그림 기능을 사용하지 않는 비용으로 Mobile Engagement에 대해서만 사용하는 경우 권한을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="d3c8b-190">위치 기능의 경우 표준 시스템 대화 상자를 사용하여 사용자에 대한 권한을 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="d3c8b-191">사용자가 승인하면 ``EngagementAgent``에 알려 실시간으로 변경 내용을 고려하도록 해야 합니다. 그렇지 않으면 사용자가 다음에 응용 프로그램을 시작할 때 변경 내용이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="d3c8b-192">다음은 사용 권한을 요청하고 ``EngagementAgent``에 긍정적인 경우 결과를 전달하는 응용 프로그램의 활동에 사용할 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="d3c8b-193">고급 보고</span><span class="sxs-lookup"><span data-stu-id="d3c8b-193">Advanced reporting</span></span>
<span data-ttu-id="d3c8b-194">필요에 따라 응용 프로그램 관련 이벤트, 오류 및 작업을 보고하려는 경우 `EngagementAgent` 클래스의 메서드를 통해 Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="d3c8b-195">`EngagementAgent.getInstance()` 정적 메서드를 호출하여 이 클래스의 개체를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="d3c8b-196">Engagement API는 모든 Engagement의 고급 기능 사용을 허용하며 Android의 Engagement API 사용 방법(및 `EngagementAgent` 클래스의 기술 문서)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="d3c8b-197">고급 구성(AndroidManifest.xml의)</span><span class="sxs-lookup"><span data-stu-id="d3c8b-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="d3c8b-198">절전 모드 해제 잠금</span><span class="sxs-lookup"><span data-stu-id="d3c8b-198">Wake locks</span></span>
<span data-ttu-id="d3c8b-199">Wifi를 사용하는 경우 또는 화면이 꺼져 있을 때 실시간으로 통계를 보내려면 다음과 같은 선택적 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="d3c8b-200">충돌 보고서</span><span class="sxs-lookup"><span data-stu-id="d3c8b-200">Crash report</span></span>
<span data-ttu-id="d3c8b-201">크래시 보고를 비활성화하려는 경우 `<application>` 태그와 `</application>` 태그 사이에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="d3c8b-202">버스트 임계값</span><span class="sxs-lookup"><span data-stu-id="d3c8b-202">Burst threshold</span></span>
<span data-ttu-id="d3c8b-203">기본적으로 Engagement 서비스는 로그를 실시간으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="d3c8b-204">응용 프로그램이 로그를 매우 자주 보고하는 경우 로그를 버퍼링한 후 정기적으로 한 번에 모두 보고하는 것이 좋습니다. 이를 "버스트 모드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="d3c8b-205">그렇게 하려면 `<application>` 태그와 `</application>` 태그 사이에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="d3c8b-206">버스트 모드를 사용하는 경우 배터리 수명은 약간 길어지지만 Engagement 모니터에 영향을 주게 됩니다. 모든 세션 및 작업 기간이 버스트 임계값으로 반올림되므로 버스트 임계값보다 짧은 세션과 작업은 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="d3c8b-207">30000(30초) 이하의 버스트 임계값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="d3c8b-208">세션 시간 제한</span><span class="sxs-lookup"><span data-stu-id="d3c8b-208">Session timeout</span></span>
<span data-ttu-id="d3c8b-209">기본적으로 세션은 마지막 작업(일반적으로 홈 또는 뒤로 키를 누르거나, 휴대폰을 유휴로 설정하거나, 다른 응용 프로그램으로 이동함으로써 발생)의 종료 10초 후에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="d3c8b-210">그러면 사용자가 응용 프로그램을 종료하고 빠르게 응용 프로그램으로 돌아갈 때(이미지를 선택하거나 알림을 확인하는 등의 작업을 통해)마다 세션 분할을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="d3c8b-211">이 매개 변수를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-211">You may want to modify this parameter.</span></span> <span data-ttu-id="d3c8b-212">그렇게 하려면 `<application>` 태그와 `</application>` 태그 사이에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="d3c8b-213">로그 보고 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="d3c8b-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="d3c8b-214">메서드 호출 사용</span><span class="sxs-lookup"><span data-stu-id="d3c8b-214">Using a method call</span></span>
<span data-ttu-id="d3c8b-215">Engagement에서 로그 전송을 중지하려면 다음을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="d3c8b-216">이 호출은 영구적이며, 공유 기본 설정 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="d3c8b-217">이 함수를 호출할 때 Engagement가 활성 상태인 경우 서비스가 중지되는 데 1분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="d3c8b-218">그러나 다음에 응용 프로그램을 시작할 때는 서비스가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="d3c8b-219">또한 `true`(으)로 동일한 함수를 호출하여 로그 보고를 다시 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="d3c8b-220">고유한 `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="d3c8b-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="d3c8b-221">이 함수를 호출하지 않고 기존 `PreferenceActivity`에서 직접 이 설정을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="d3c8b-222">다음과 같이 `AndroidManifest.xml` 파일의 기본 설정 파일을(원하는 모드에서) `application meta-data`와(과) 함께 사용하도록 Engagement를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="d3c8b-223">`engagement:agent:settings:name` 키는 공유 기본 설정 파일의 이름을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="d3c8b-224">`engagement:agent:settings:mode` 키는 공유 기본 설정 파일의 모드를 정의하는 데 사용되며, `PreferenceActivity`에서와 동일한 모드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="d3c8b-225">모드는 숫자로 전달해야 합니다. 코드에서 상수 플래그의 조합을 사용하는 경우 전체 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="d3c8b-226">Engagement는 이 설정을 관리하기 위한 기본 설정 파일 내에서 항상 `engagement:key` 부울 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="d3c8b-227">다음 `AndroidManifest.xml` 예제는 기본값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="d3c8b-228">이제 다음과 같은 기본 설정 레이아웃에서 `CheckBoxPreference` 을(를) 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c8b-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
