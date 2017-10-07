---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
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
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>어떻게 tooIntegrate Engagement Android에서
> [!div class="op_single_selector"]
> * [Windows 범용](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

이 절차에서는 hello 가장 간단한 방법은 tooactivate Engagement의 분석 및 Android 응용 프로그램의 함수 모니터링을 설명 합니다.

> [!IMPORTANT]
> Android SDK API의 최소 수준은 10 이상(Android 2.3.3 이상)이어야 합니다.
> 
> 

단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivates hello 보고서의 로그 됩니다. hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 Mobile Engagement에서 Android API 태깅](mobile-engagement-android-use-engagement-api.md) 이러한 이후 통계는 종속 응용 프로그램입니다.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Android 프로젝트에 hello Engagement SDK와 서비스를 포함 합니다.
다운로드에서 Android SDK hello [여기](https://aka.ms/vq9mfn) 가져오기 `mobile-engagement-VERSION.jar` hello로 만들어서 `libs` Android 프로젝트의 폴더 (아직 존재 하지 않는 경우 hello 라이브러리 폴더를 만듦) 합니다.

> [!IMPORTANT]
> ProGuard 응용 프로그램 패키지를 빌드하는 경우 일부 클래스 tookeep 할 수 있습니다. 다음 구성 코드 조각 hello를 사용할 수 있습니다.
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

Hello 시작 관리자 활동이 메서드 다음에 오는 호출 hello 여 Engagement 연결 문자열을 지정 합니다.

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

응용 프로그램에 대 한 연결 문자열 hello Azure 포털에 표시 됩니다.

* 누락 된 경우 추가 다음 Android 권한을 hello (hello 전에 `<application>` 태그).
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* 다음 단원을 hello 추가 (hello 사이 `<application>` 및 `</application>` 태그).
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* 변경 `<Your application name>` 응용 프로그램의 hello 이름별 합니다.

> [!TIP]
> hello `android:label` 특성을 사용 하면 있습니다 toochoose hello 이름 hello Engagement 서비스의 전화 번호의 hello "실행 서비스" 화면에서 toohello 최종 사용자에 게 표시 합니다. tooset이이 특성을 너무 권장`"<Your application name>Service"` (예: `"AcmeFunGameService"`).
> 
> 

지정 하 여 hello `android:process` 특성 Engagement 서비스는 hello (Engagement hello 응용 프로그램이 잠재적으로 응답이 main/UI 스레드를 만들게 될 동일한 프로세스에서 실행 하는) 자체 프로세스에서 실행 되도록 지정 합니다.

> [!NOTE]
> 모든 코드에 배치 `Application.onCreate()` 및 다른 응용 프로그램이 콜백에 hello Engagement 서비스를 포함 하는 응용 프로그램의 모든 프로세스에서 실행 됩니다. 원치 않는 부작용 (예: 불필요 한 메모리 할당 및 hello Engagement 프로세스, 중복 브로드캐스트 수신기 또는 서비스의 스레드) 것 같습니다.
> 
> 

재정의 하는 경우 `Application.onCreate()`, 다음 코드 조각 hello 맨 앞에 권장된 tooadd hello는 프로그램 `Application.onCreate()` 함수:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

할 수 있는 동일한 작업에 대 한 hello `Application.onTerminate()`, `Application.onLowMemory()` 및 `Application.onConfigurationChanged(...)`합니다.

확장할 수도 있습니다 `EngagementApplication` 확장 하는 대신 `Application`: 콜백 hello `Application.onCreate()` 프로세스 확인 및 호출 hello지 않습니다 `Application.onApplicationProcessCreate()` hello 현재 프로세스가 hello 하나의 호스팅 hello Engagement 서비스가 아닌 경우 hello 동일한 규칙이 적용에 대 한만 다른 콜백에 hello 합니다.

## <a name="basic-reporting"></a>기본 보고
### <a name="recommended-method-overload-your-activity-classes"></a>권장 방법: `Activity` 클래스 오버로드
Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 하기만 하면 모든 toomake 프로그램 `*Activity` hello 해당 하위 클래스 상속 `Engagement*Activity` 클래스 (예: 확장 하는 레거시 활동 경우 `ListActivity`, 확장 확인 `EngagementListActivity`).

**Engagement 사용 안 함:**

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

**Engagement 사용:**

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
> 사용 하는 경우 `EngagementListActivity` 또는 `EngagementExpandableListActivity`, 있는지 확인 호출 너무`requestWindowFeature(...);` 너무 hello 호출 전에 이루어집니다`super.onCreate(...);`, 그렇지 않으면 충돌이 발생 합니다.
> 
> 

Hello에서 이러한 클래스를 찾을 수 있습니다 `src` 폴더를 프로젝트에 복사할 수 있습니다. hello 클래스에에서도 포함 되어 hello **JavaDoc**합니다.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>대체 방법: `startActivity()` 및 `endActivity()` 수동 호출
처리할 수 없거나 toooverload 하지 않을 경우 사용자 `Activity` 클래스 대신 시작 하 고 호출 하 여 활동을 끝낼 수 `EngagementAgent`의 메서드를 직접 합니다.

> [!IMPORTANT]
> hello Android SDK를 호출 하지 않습니다. hello `endActivity()` hello 응용 프로그램이 닫힐 경우에 메서드 (android에서는 응용 프로그램은 실제로 하며 절대로 닫히지 않습니다). 즉, *항상* toocall hello 권장 `startActivity()` hello에 대 한 메서드 `onResume` 의 콜백에 *모든* 활동 및 hello `endActivity()` hello에 대 한 메서드 `onPause()` 콜백 *모든* 활동입니다. 이 hello 유일한 방법은 toobe 있는지 세션 유출 되지 것입니다. 세션은 누락 (hello 서비스 세션은 보류 중 상태로 연결 되어) 이후 hello Engagement 서비스 hello Engagement 백 엔드에서 연결이 끊기지 않도록 합니다.
> 
> 

다음은 예제입니다.

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

이 예에서는 매우 비슷한 toohello `EngagementActivity` 클래스 및 해당 소스 코드는 hello에 제공 된 변형, `src` 폴더입니다.

## <a name="test"></a>테스트
이제 에뮬레이터 또는 장치에서 모바일 앱을 실행 하 고 hello 모니터 탭에서 세션 등록 있는지 확인 하 여 확인 통합 하십시오.

hello 다음 섹션은 선택 사항입니다.

## <a name="location-reporting"></a>위치 보고
위치 toobe 보고 하려는 경우 필요한 tooadd 몇 줄의 구성 (hello 사이 `<application>` 및 `</application>` 태그).

### <a name="lazy-area-location-reporting"></a>지연 영역 위치 보고
Tooreport hello 국가, 지역 및 연결 된 위치를 사용 하면 지연 된 영역 위치 보고 toodevices 합니다. 이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다. hello 장치 영역의 세션당 한 번만 보고 됩니다. hello GPS은 사용 되지 않거나, 고 따라서 이러한 유형의 위치 보고서에 거의 (하지 toosay 없음) hello 배터리에 미치는 영향입니다.

보고 된 영역은 사용자, 세션, 이벤트 및 오류에 대 한 사용 되는 toocompute 지리적 통계입니다. 이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.

tooenable 지연 된 영역 위치 보고,이 절차 앞부분에서 설명한 hello 구성을 사용 하 여 수행할 수 있습니다.

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

또는 응용 프로그램에서 이미 사용하고 있는 경우 ``ACCESS_FINE_LOCATION`` 을 계속 사용할 수 있습니다.

### <a name="real-time-location-reporting"></a>실시간 위치 보고
Tooreport hello 위도 및 경도 연결을 사용 하면 실시간 위치 보고 toodevices 합니다. 기본적으로 네트워크 위치 (셀 ID 또는 WIFI에 따라)에 사용 하 여 이러한 유형의 위치를 보고 하 고 hello 보고는 활성 (즉, 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다.

실시간으로 위치는 *하지* toocompute 통계를 사용 합니다. 유일한 목적은 실시간 지리적 펜스 tooallow hello 사용 하는 \<지 오 펜싱 Reach-대상 그룹\> Reach 캠페인의 기준입니다.

tooenable 실시간 위치 보고,이 절차 앞부분에서 설명한 hello 구성을 사용 하 여 수행할 수 있습니다.

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

또는 응용 프로그램에서 이미 사용하고 있는 경우 ``ACCESS_FINE_LOCATION`` 을 계속 사용할 수 있습니다.

#### <a name="gps-based-reporting"></a>GPS 기반 보고
기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다. GPS tooenable hello 사용 (임 훨씬 더 정확 하 게) 위치를 기반으로 하 고 hello 구성 개체를 사용 합니다.

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>백그라운드 보고
기본적으로 실시간 위치 보고는 활성 (즉, 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다. tooenable hello 보고도 백그라운드에서 사용 하 여 hello 구성 개체:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Hello 응용 프로그램은 백그라운드에서 실행을 기반으로 하는 네트워크 위치 뿐 보고, 사용 하도록 설정한 경우에 hello GPS 합니다.
> 
> 

hello 배경 위치 보고서 hello 사용자 자신의 장치를 다시 부팅 하는 경우 중지 됩니다, 그리고 부팅 시 자동으로 다시 시작이 toomake를 추가할 수 있습니다.

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

또한 권한이 없는 경우 다음 tooadd hello가 필요 합니다.

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Android M 권한
Android M부터는 일부 권한이 런타임 시 관리되며 사용자 승인이 필요합니다.

Android API 수준 23을 대상으로 경우 hello 런타임 권한은 새 응용 프로그램 설치에는 기본적으로 해제 됩니다. 그렇지 않으면 기본적으로 활성화됩니다.

hello 사용자 수 설정/해제 hello 장치 설정 메뉴에서 이러한 권한 합니다. Hello 응용 프로그램의 백그라운드 프로세스를 중지 시스템 메뉴에서 사용 권한을 해제 하면,이 시스템 동작에 백그라운드에서 tooreceive 푸시 기능에 영향을 주지 않습니다.

Mobile Engagement의 hello 컨텍스트에서 런타임 시 승인이 필요한 hello 사용 권한은 다음과 같습니다.

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (이에 대한 Android API Level 23을 대상으로 할 때만 해당)

hello 외부 저장소 Reach 큰 그림 기능에 대해서만 사용 됩니다. 찾을 사용자에 게가 권한을 toobe 중단 요청을 제거할 수 있습니다 hello 비용의 큰 그림 기능을 해제 하지만 Mobile Engagement에 대해서만 사용 합니다.

Hello 위치 기능에 대 한 사용 권한을 toouser 표준 시스템 대화 상자를 사용 하 여 요청 해야 합니다. Tootell hello 사용자가을 승인한 경우 해야 ``EngagementAgent`` tootake 실제 시간 (hello 변경 처리 hello 다음 시간 hello 사용자를 실행 하는 hello 응용 프로그램)의 계정으로 변경 하는 합니다.

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>고급 보고
필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업을 하려는 경우 필요한 toouse hello Engagement API의 hello hello 메서드를 통해 `EngagementAgent` 클래스입니다. 이 클래스의 개체 hello 호출 하 여 검색할 수 `EngagementAgent.getInstance()` 정적 메서드입니다.

hello Engagement API toouse Engagement의 고급 기능을 모두 허용 하 고 어떻게 hello에 자세히 설명 되어 tooUse Android에서 Engagement API (뿐만 아니라 hello의 기술 문서 hello 에서처럼에서 `EngagementAgent` 클래스).

## <a name="advanced-configuration-in-androidmanifestxml"></a>고급 구성(AndroidManifest.xml의)
### <a name="wake-locks"></a>절전 모드 해제 잠금
Toobe Wifi를 사용 하는 경우 실시간으로 또는 hello 화면을 해제 통계는 전송 하려는 경우 다음 선택적 권한이 hello를 추가 합니다.

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>충돌 보고서
Toodisable 충돌 보고서를 원하는 경우 추가 (hello 사이 `<application>` 및 `</application>` 태그).

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>버스트 임계값
기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다. 더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우는 일반 기본 시간 ("버스트 모드" hello 라는)에서 한 번에 모두 있습니다. 따라서 추가 toodo (hello 사이 `<application>` 및 `</application>` 태그):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

hello 버스트 모드 약간 증가 hello 배터리 수명 하지만 영향을 주 hello Engagement 모니터: 모든 세션 및 작업 기간 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 둥근된 toohello 버스트 임계값도 됩니다. toouse 30000 (30 초) 보다 버스트 임계값 것이 좋습니다.

### <a name="session-timeout"></a>세션 시간 제한
기본적으로 세션은 (일반적으로 키를 눌러 hello 홈으로 발생 하거나는 유휴 hello 전화 설정 하거나 다른 응용 프로그램으로 이동 하 여 키를 백업)의 마지막 활동의 hello 끝 이후에 종료 10s 합니다. 이 tooavoid (수 발생할 그 이미지를 선택 하는 경우 확인 하는 등 알림입니다.) 세션 분할 각 시간 hello 사용자 끝내 고 toohello 응용 프로그램을 신속 하 게 반환 합니다. 이 매개 변수 toomodify를 할 수 있습니다. 따라서 추가 toodo (hello 사이 `<application>` 및 `</application>` 태그):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>로그 보고 사용 안 함
### <a name="using-a-method-call"></a>메서드 호출 사용
로그 보내기 Engagement toostop 하려는 경우 호출할 수 있습니다.

            EngagementAgent.getInstance(context).setEnabled(false);

이 호출은 영구적이며, 공유 기본 설정 파일을 사용합니다.

Engagement 활성 상태 이면이 함수를 호출할 때 서비스 toostop hello에 대 일 분 걸릴 수 있습니다. 그러나 다음 hello 응용 프로그램을 시작할 때 모든 hello에서 hello 서비스를 시작할 없습니다 것입니다.

로그 다시 hello와 같은 함수를 호출 하 여 보고를 사용 하도록 설정할 수 `true`합니다.

### <a name="integration-in-your-own-preferenceactivity"></a>고유한 `PreferenceActivity`
이 함수를 호출하지 않고 기존 `PreferenceActivity`에서 직접 이 설정을 통합할 수 있습니다.

Hello에서 Engagement toouse 기본 설정 파일 (hello 원하는 모드)를 구성할 수 있습니다 `AndroidManifest.xml` 파일 `application meta-data`:

* hello `engagement:agent:settings:name` 키는 hello 공유 기본 설정 파일의 사용 되는 toodefine hello 이름입니다.
* hello `engagement:agent:settings:mode` 키는 hello 공유 기본 설정 파일의 사용 되는 toodefine hello 모드, hello를 사용 해야 동일한 모드에서와 같이 프로그램 `PreferenceActivity`합니다. hello 모드 숫자 변수로 전달 되어야 합니다: 상수 플래그의 조합을 코드를 사용 하는 경우 hello 총 값을 확인 합니다.

항상 engagement hello를 사용 하 여 `engagement:key` 이 설정을 관리 하기 위한 hello 기본 설정 파일 내에서 부울 키입니다.

다음 예의 hello `AndroidManifest.xml` 표시 hello 기본값:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

추가 하 여 한 `CheckBoxPreference` 하나를 따르는 hello와 같은 기본 설정 레이아웃에서:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
