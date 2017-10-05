---
title: "Azure Mobile Engagement Android SDK에 대한 위치 보고"
description: "Azure Mobile Engagement Android SDK에 대해 위치 보고를 구성하는 방법에 대해 설명합니다"
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
ms.openlocfilehash: 777d5719cce505b55dfb61c91dcac7e713b077a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="41443-103">Azure Mobile Engagement Android SDK에 대한 위치 보고</span><span class="sxs-lookup"><span data-stu-id="41443-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41443-104">Android</span><span class="sxs-lookup"><span data-stu-id="41443-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="41443-105">이 항목에서는 Android 응용 프로그램에서 위치 보고를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-105">This topic describes how to do location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41443-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41443-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="41443-107">위치 보고</span><span class="sxs-lookup"><span data-stu-id="41443-107">Location reporting</span></span>
<span data-ttu-id="41443-108">위치가 보고되도록 하려는 경우 몇 줄의 구성을 `<application>` 태그와 `</application>` 태그 사이에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-108">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="41443-109">지연 영역 위치 보고</span><span class="sxs-lookup"><span data-stu-id="41443-109">Lazy area location reporting</span></span>
<span data-ttu-id="41443-110">지연 영역 위치 보고를 통해 국가, 지역 및 장치와 연결된 위치를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-110">Lazy area location reporting enables reporting the country, region, and locality associated with devices.</span></span> <span data-ttu-id="41443-111">이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="41443-112">장치 영역은 세션당 한번 이하로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-112">The device area is reported at most once per session.</span></span> <span data-ttu-id="41443-113">GPS는 전혀 사용되지 않으므로 이러한 위치 보고 형식은 배터리에 미미한 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-113">The GPS is never used, and thus this type of location report has low impact on the battery.</span></span>

<span data-ttu-id="41443-114">보고된 영역은 사용자, 세션, 이벤트 및 오류에 대한 지리적 통계를 계산하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-114">Reported areas are used to compute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="41443-115">이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="41443-116">이 절차의 앞에서 설명한 구성을 사용하여 지연 영역 위치 보고를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-116">You enable lazy area location reporting by using the configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="41443-117">위치 권한도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-117">You also need to specify a location permission.</span></span> <span data-ttu-id="41443-118">다음 코드에서는 ``COARSE`` 권한을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="41443-119">앱에서 필요한 경우 대신 ``ACCESS_FINE_LOCATION`` 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="41443-120">실시간 위치 보고</span><span class="sxs-lookup"><span data-stu-id="41443-120">Real-time location reporting</span></span>
<span data-ttu-id="41443-121">실시간 위치 보고를 통해 장치와 연결된 위도와 경도를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-121">Real-time location reporting enables reporting the latitude and longitude associated with devices.</span></span> <span data-ttu-id="41443-122">기본적으로 이러한 형식의 위치 보고에서는 셀 ID 또는 WIFI를 기반으로 하는 네트워크 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="41443-123">이 보고 기능은 응용 프로그램이 포그라운드로 실행되는 경우(예: 세션 중)에만 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="41443-123">The reporting is only active when the application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="41443-124">실시간 위치는 통계를 계산하는 데 사용되지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="41443-124">Real-time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="41443-125">유일한 용도는 도달률 캠페인에서 실시간 지리적 펜스 \<Reach-Audience-geofencing\> 사용을 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41443-125">Their only purpose is to allow the use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="41443-126">실시간 위치 보고를 활성화하려면 시작 관리자 활동에서 Engagement 연결 문자열을 설정하는 위치에 코드 행을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-126">To enable real-time location reporting, add a line of code to where you set the Engagement connection string in the launcher activity.</span></span> <span data-ttu-id="41443-127">결과는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-127">The result looks like the following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need to specify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="41443-128">GPS 기반 보고</span><span class="sxs-lookup"><span data-stu-id="41443-128">GPS based reporting</span></span>
<span data-ttu-id="41443-129">기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="41443-130">훨씬 더 정밀한 GPS 기반 위치의 사용을 설정하려면 구성 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-130">To enable the use of GPS-based locations, which are far more precise, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="41443-131">또한 아직 없는 경우 다음 권한도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-131">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="41443-132">백그라운드 보고</span><span class="sxs-lookup"><span data-stu-id="41443-132">Background reporting</span></span>
<span data-ttu-id="41443-133">기본적으로 실시간 위치 보고는 응용 프로그램이 포그라운드로 실행되는 경우(예: 세션 중)에만 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="41443-133">By default, real-time location reporting is only active when the application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="41443-134">백그라운드에서도 보고를 활성화하려면 이 구성 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-134">To enable the reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="41443-135">응용 프로그램이 백그라운드에서 실행될 때 GPS를 활성화한 경우에도 네트워크 기반 위치만 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-135">When the application runs in background, only network-based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="41443-136">사용자가 장치를 다시 부팅하는 경우 백그라운드 위치 보고가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-136">If the user reboots their device, the background location report is stopped.</span></span> <span data-ttu-id="41443-137">부팅 시에 자동으로 다시 시작되도록 하려면 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-137">To make it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="41443-138">또한 아직 없는 경우 다음 권한도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-138">You also need to add the following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="41443-139">Android M 권한</span><span class="sxs-lookup"><span data-stu-id="41443-139">Android M permissions</span></span>
<span data-ttu-id="41443-140">Android M부터는 일부 권한이 런타임 시 관리되며 사용자 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="41443-141">Android API Level 23을 대상으로 하는 경우 새 앱 설치에 대해서는 기본적으로 런타임 권한이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-141">If you target Android API level 23, the runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="41443-142">그렇지 않으면 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="41443-143">장치 설정 메뉴에서 이러한 권한을 설정/해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-143">You can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="41443-144">시스템 메뉴에서 권한을 해제하면 응용 프로그램의 백그라운드 프로세스가 중단되며 이것은 시스템 동작으로 백그라운드로 푸시 알림을 받는 기능에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-144">Turning off permissions from the system menu kills the background processes of the application, which is a system behavior, and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="41443-145">Mobile Engagement 위치 보고의 컨텍스트에서 런타임 시 승인이 필요한 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="41443-145">In the context of Mobile Engagement location reporting, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="41443-146">표준 시스템 대화 상자를 사용하여 사용자로부터 권한을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-146">Request permissions from the user using a standard system dialog.</span></span> <span data-ttu-id="41443-147">사용자가 승인하는 경우 ``EngagementAgent`` 에 실시간으로 변경을 고려할 것을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="41443-147">If the user approves, tell ``EngagementAgent`` to take that change into account in real-time.</span></span> <span data-ttu-id="41443-148">그렇지 않으면 다음에 사용자가 응용 프로그램을 시작할 때 변경 내용이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="41443-148">Otherwise the change is processed the next time the user launches the application.</span></span>

<span data-ttu-id="41443-149">다음은 사용 권한을 요청하고 ``EngagementAgent``에 긍정적인 경우 결과를 전달하는 응용 프로그램의 활동에 사용할 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="41443-149">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
