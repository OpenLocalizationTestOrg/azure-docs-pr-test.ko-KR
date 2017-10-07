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
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Azure Mobile Engagement Android SDK에 대한 위치 보고
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

이 항목에서는 설명 방법을 toodo 위치 Android 응용 프로그램에 대 한 보고 합니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>위치 보고
위치 toobe 보고 하려는 경우 필요한 tooadd 몇 줄의 구성 (hello 사이 `<application>` 및 `</application>` 태그).

### <a name="lazy-area-location-reporting"></a>지연 영역 위치 보고
지연 된 영역 위치 보고 보고 hello 국가, 지역 및 장치가 연결 된 위치 수 있습니다. 이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다. hello 장치 영역의 세션당 한 번만 보고 됩니다. hello GPS은 사용 되지 않거나, 따라서 이러한 유형의 위치 보고서 대 한 영향이 낮은 hello 배터리 합니다.

보고 된 영역은 사용자, 세션, 이벤트 및 오류에 대 한 사용 되는 toocompute 지리적 통계입니다. 이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.

이 절차 앞부분에서 설명한 hello 구성을 사용 하 여 보고 하는 지연 된 영역 위치를 사용 하도록 설정 합니다.

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Toospecify 위치 권한이 있어야합니다. 다음 코드에서는 ``COARSE`` 권한을 사용합니다.

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

앱에서 필요한 경우 대신 ``ACCESS_FINE_LOCATION`` 을 사용할 수 있습니다.

### <a name="real-time-location-reporting"></a>실시간 위치 보고
실시간 위치 보고 보고 hello 위도 및 경도 장치와 연관 수 있습니다. 기본적으로 이러한 형식의 위치 보고에서는 셀 ID 또는 WIFI를 기반으로 하는 네트워크 위치만 사용합니다. hello 보고는 hello 응용 프로그램 (예를 들어 세션) 포그라운드에서 실행 될 때 활성화 됩니다.

실시간 위치는 *하지* toocompute 통계를 사용 합니다. 유일한 목적은 실시간 지리적 펜스 tooallow hello 사용 하는 \<지 오 펜싱 Reach-대상 그룹\> Reach 캠페인의 기준입니다.

tooenable 실시간 위치 보고, 줄을 추가한 코드 toowhere의 hello Engagement 연결 문자열에서에서 설정한 hello 시작 관리자 활동이 있습니다. hello 결과 hello 다음과 같이 표시 됩니다.

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>GPS 기반 보고
기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다. 훨씬 더 정확 하 게 되는 GPS 기반 위치, tooenable hello 사용 hello 구성 개체를 사용 합니다.

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>백그라운드 보고
기본적으로 실시간 위치 보고는 활성 (예를 들어 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다. 이 구성 개체를 사용 하는 백그라운드에서도 보고 tooenable hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Hello 응용 프로그램이 백그라운드에서 실행 위치에만 네트워크 기반 보고를 사용 하도록 설정한 경우에 hello GPS.
> 
> 

Hello 사용자가 장치를 다시 부팅 hello 배경 위치 보고서 중지 됩니다. 이 코드를 추가 하는 toomake 부팅 시 자동으로 다시 시작 합니다.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Android M 권한
Android M부터는 일부 권한이 런타임 시 관리되며 사용자 승인이 필요합니다.

Android API 수준 23 대상 경우 새 응용 프로그램 설치에 대해 기본적으로 hello 런타임 권한은 비활성화 되어 있습니다. 그렇지 않으면 기본적으로 활성화됩니다.

있습니다 수 설정/해제 hello 장치 설정 메뉴에서 이러한 권한 합니다. 시스템 동작 이므로 백그라운드에서 기능 tooreceive 푸시에 어떠한 영향도 미치지 hello 응용 프로그램의 백그라운드 프로세스 hello 해제 hello 시스템 메뉴에서 사용 권한을 해제 합니다.

Mobile Engagement 위치 보고의 hello 컨텍스트에서 런타임 시 승인이 필요한 hello 사용 권한은 다음과 같습니다.

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

표준 시스템 대화 상자를 사용 하 여 hello 사용자에서 권한을 요청 합니다. Hello 사용자가을 승인 하는 경우 ``EngagementAgent`` tootake 실시간 계정으로 변경 하는 합니다. 그렇지 않으면 hello 변경 처리 hello 다음 시간 hello 사용자를 실행 하는 hello 응용 프로그램입니다.

양수 응용 프로그램 toorequest 사용 권한 및 앞으로 hello 결과 활동에서 다음 코드 샘플 toouse은 너무``EngagementAgent``:

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
