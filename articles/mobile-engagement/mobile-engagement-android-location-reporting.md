---
title: "aaaLocation Azure Mobile Engagement Android SDK에 대 한 보고"
description: "설명 방법을 tooconfigure 위치 Azure Mobile Engagement Android SDK에 대 한 보고"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="312ba-103">Azure Mobile Engagement Android SDK에 대한 위치 보고</span><span class="sxs-lookup"><span data-stu-id="312ba-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="312ba-104">Android</span><span class="sxs-lookup"><span data-stu-id="312ba-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="312ba-105">이 항목에서는 설명 방법을 toodo 위치 Android 응용 프로그램에 대 한 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="312ba-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="312ba-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="312ba-107">위치 보고</span><span class="sxs-lookup"><span data-stu-id="312ba-107">Location reporting</span></span>
<span data-ttu-id="312ba-108">위치 toobe 보고 하려는 경우 필요한 tooadd 몇 줄의 구성 (hello 사이 `<application>` 및 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="312ba-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="312ba-109">지연 영역 위치 보고</span><span class="sxs-lookup"><span data-stu-id="312ba-109">Lazy area location reporting</span></span>
<span data-ttu-id="312ba-110">지연 된 영역 위치 보고 보고 hello 국가, 지역 및 장치가 연결 된 위치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="312ba-111">이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="312ba-112">hello 장치 영역의 세션당 한 번만 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="312ba-113">hello GPS은 사용 되지 않거나, 따라서 이러한 유형의 위치 보고서 대 한 영향이 낮은 hello 배터리 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="312ba-114">보고 된 영역은 사용자, 세션, 이벤트 및 오류에 대 한 사용 되는 toocompute 지리적 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="312ba-115">이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="312ba-116">이 절차 앞부분에서 설명한 hello 구성을 사용 하 여 보고 하는 지연 된 영역 위치를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="312ba-117">Toospecify 위치 권한이 있어야합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="312ba-118">다음 코드에서는 ``COARSE`` 권한을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="312ba-119">앱에서 필요한 경우 대신 ``ACCESS_FINE_LOCATION`` 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="312ba-120">실시간 위치 보고</span><span class="sxs-lookup"><span data-stu-id="312ba-120">Real-time location reporting</span></span>
<span data-ttu-id="312ba-121">실시간 위치 보고 보고 hello 위도 및 경도 장치와 연관 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="312ba-122">기본적으로 이러한 형식의 위치 보고에서는 셀 ID 또는 WIFI를 기반으로 하는 네트워크 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="312ba-123">hello 보고는 hello 응용 프로그램 (예를 들어 세션) 포그라운드에서 실행 될 때 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="312ba-124">실시간 위치는 *하지* toocompute 통계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="312ba-125">유일한 목적은 실시간 지리적 펜스 tooallow hello 사용 하는 \<지 오 펜싱 Reach-대상 그룹\> Reach 캠페인의 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="312ba-126">tooenable 실시간 위치 보고, 줄을 추가한 코드 toowhere의 hello Engagement 연결 문자열에서에서 설정한 hello 시작 관리자 활동이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="312ba-127">hello 결과 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="312ba-128">GPS 기반 보고</span><span class="sxs-lookup"><span data-stu-id="312ba-128">GPS based reporting</span></span>
<span data-ttu-id="312ba-129">기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="312ba-130">훨씬 더 정확 하 게 되는 GPS 기반 위치, tooenable hello 사용 hello 구성 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="312ba-131">또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="312ba-132">백그라운드 보고</span><span class="sxs-lookup"><span data-stu-id="312ba-132">Background reporting</span></span>
<span data-ttu-id="312ba-133">기본적으로 실시간 위치 보고는 활성 (예를 들어 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="312ba-134">이 구성 개체를 사용 하는 백그라운드에서도 보고 tooenable hello:</span><span class="sxs-lookup"><span data-stu-id="312ba-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="312ba-135">Hello 응용 프로그램이 백그라운드에서 실행 위치에만 네트워크 기반 보고를 사용 하도록 설정한 경우에 hello GPS.</span><span class="sxs-lookup"><span data-stu-id="312ba-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="312ba-136">Hello 사용자가 장치를 다시 부팅 hello 배경 위치 보고서 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="312ba-137">이 코드를 추가 하는 toomake 부팅 시 자동으로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="312ba-138">또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="312ba-139">Android M 권한</span><span class="sxs-lookup"><span data-stu-id="312ba-139">Android M permissions</span></span>
<span data-ttu-id="312ba-140">Android M부터는 일부 권한이 런타임 시 관리되며 사용자 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="312ba-141">Android API 수준 23 대상 경우 새 응용 프로그램 설치에 대해 기본적으로 hello 런타임 권한은 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="312ba-142">그렇지 않으면 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="312ba-143">있습니다 수 설정/해제 hello 장치 설정 메뉴에서 이러한 권한 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="312ba-144">시스템 동작 이므로 백그라운드에서 기능 tooreceive 푸시에 어떠한 영향도 미치지 hello 응용 프로그램의 백그라운드 프로세스 hello 해제 hello 시스템 메뉴에서 사용 권한을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="312ba-145">Mobile Engagement 위치 보고의 hello 컨텍스트에서 런타임 시 승인이 필요한 hello 사용 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="312ba-146">표준 시스템 대화 상자를 사용 하 여 hello 사용자에서 권한을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="312ba-147">Hello 사용자가을 승인 하는 경우 ``EngagementAgent`` tootake 실시간 계정으로 변경 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="312ba-148">그렇지 않으면 hello 변경 처리 hello 다음 시간 hello 사용자를 실행 하는 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="312ba-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="312ba-149">양수 응용 프로그램 toorequest 사용 권한 및 앞으로 hello 결과 활동에서 다음 코드 샘플 toouse은 너무``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="312ba-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
