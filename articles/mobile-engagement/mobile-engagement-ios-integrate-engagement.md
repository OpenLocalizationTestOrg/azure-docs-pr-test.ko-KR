---
title: "Mobile Engagement iOS SDK 통합 aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement용 iOS SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>어떻게 tooIntegrate Engagement iOS에서
> [!div class="op_single_selector"]
> * [Windows 범용](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

이 절차에서는 hello 가장 간단한 방법은 tooactivate Engagement의 분석 및 iOS 응용 프로그램의 함수 모니터링을 설명 합니다.

hello Engagement SDK 필요 iOS7 + 및 Xcode 8 +: hello 배포 대상 응용 프로그램의 이상 이어야 합니다 iOS 7입니다.

> [!NOTE]
> XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다. 10 iOS 장치 참조에서 실행 되는 동안이 이전 버전의 hello 모듈이에 알려진된 버그가 있습니다 [reach 모듈 통합 hello](mobile-engagement-ios-integrate-engagement-reach.md) 내용을 확인 합니다. Toouse hello SDK v3.2.4를 선택한 다음 방금 hello를 건너뛸 경우 `UserNotifications.framework` hello 다음 단계에서 가져옵니다.
>
>

단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivate hello 보고서의 로그 됩니다. hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 iOS 응용 프로그램에서 API 태그를 지정 하는 Mobile Engagement](mobile-engagement-ios-use-engagement-api.md) 후 이러한 통계 응용 프로그램이 종속 되어 있습니다.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>IOS 프로젝트에 hello Engagement SDK를 포함 합니다.
* Hello iOS SDK 다운로드에서 [여기](http://aka.ms/qk2rnj)합니다.
* Hello Engagement SDK tooyour iOS 프로젝트 추가: 프로젝트 및 선택 사항에 Xcode에서 마우스 오른쪽 단추로 클릭 **"파일을 너무 추가..."** hello 선택 `EngagementSDK` 폴더입니다.
* 계약 추가 프레임 워크 toowork 필요: hello 프로젝트 탐색기에서 프로젝트 창을 열고 선택 hello 올바른 대상입니다. 그런 다음 hello를 열고 **"빌드 단계"** 탭 및 hello **"링크 이진 파일과 라이브러리"** 메뉴에서 이러한 프레임 워크 추가:

  * `UserNotifications.framework`-으로 hello 링크 설정`Optional`
  * `AdSupport.framework`-으로 hello 링크 설정`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> hello AdSupport 프레임 워크를 제거할 수 있습니다. 서비스는 프레임 워크 toocollect hello IDFA이 필요합니다. 그러나 IDFA 수집을 해제할 수 있습니다 \<ios sdk-engagement idfa\> 이 ID에 대 한 hello 새 Apple 정책과 toocomply
>
>

## <a name="initialize-hello-engagement-sdk"></a>Hello Engagement SDK를 초기화 합니다.
응용 프로그램 대리자 toomodify 필요합니다.

* 구현 파일의 hello 위쪽 hello Engagement 에이전트를 가져옵니다.

      [...]
      #import "EngagementAgent.h"
* Hello 메서드 내부 Engagement 초기화 '**applicationDidFinishLaunching:**'또는'**응용 프로그램: didFinishLaunchingWithOptions:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>기본 보고
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>권장 방법: `UIViewController` 클래스 오버로드
Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 만들 수 있습니다 모든 프로그램 `UIViewController` hello에서 하위 클래스 상속 `EngagementViewController` 클래스 (동일한 규칙 에 대 한 `UITableViewController`  - \> `EngagementTableViewController`).

**Engagement 사용 안 함:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Engagement 사용:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>대체 메서드: 수동으로 `startActivity()` 호출
처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `UIViewController` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent`의 메서드를 직접 합니다.

> [!IMPORTANT]
> hello를 자동으로 호출 하는 hello iOS SDK `endActivity()` hello 응용 프로그램을 닫으면 메서드. 즉, *항상* toocall hello 권장 `startActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무*NEVER* 호출 hello `endActivity` 이 메서드를 사용 하면 호출 이후 메서드 현재 세션 toobe hello 종료 되었습니다.
>
>

## <a name="location-reporting"></a>위치 보고
서비스 약관 Apple 응용 프로그램 통계 용도로 추적 toouse 위치를 허용 하지 않습니다. 따라서 좋습니다 tooenable 위치 보고서 응용 프로그램 hello 위치는 또 다른 이유에 대 한 추적을 사용 하는 경우에.

IOS 8 이상에서는 응용 프로그램 hello 키에 대 한 문자열을 설정 하 여 위치 확인 서비스를 사용 하는 방법에 대 한 설명을 제공 해야 [NSLocationWhenInUseUsageDescription] 또는 [NSLocationAlwaysUsageDescription]앱의 Info.plist 파일에 있습니다. Tooreport 위치 Engagement와 hello 백그라운드에서 원하는 NSLocationAlwaysUsageDescription hello 키를 추가 합니다. 다른 모든 경우에 NSLocationWhenInUseUsageDescription hello 키를 추가 합니다. 참고 iOS 11에서 NSLocationAlwaysAndWhenInUseUsageDescription와 NSLocationWhenInUseUsageDescription tooreport 배경 위치 해야 합니다.

### <a name="lazy-area-location-reporting"></a>지연 영역 위치 보고
Tooreport hello 국가, 지역 및 연결 된 위치를 사용 하면 지연 된 영역 위치 보고 toodevices 합니다. 이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다. hello 장치 영역의 세션당 한 번만 보고 됩니다. hello GPS은 사용 되지 않거나, 고 따라서 이러한 유형의 위치 보고서에 거의 (하지 toosay 없음) hello 배터리에 미치는 영향입니다.

보고 된 영역은 사용자, 세션, 이벤트 및 오류에 대 한 사용 되는 toocompute 지리적 통계입니다. 이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다. 장치는 검색 된 감사 toohello 수에 대해 보고 하는 영역을 마지막으로 hello [장치 API]합니다.

tooenable 지연 된 영역 위치 보고는 hello hello Engagement 에이전트를 초기화 한 후 다음 줄을 추가 합니다.

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>실시간 위치 보고
Tooreport hello 위도 및 경도 연결을 사용 하면 실시간 위치 보고 toodevices 합니다. 기본적으로 네트워크 위치 (셀 ID 또는 WIFI에 따라)에 사용 하 여 이러한 유형의 위치를 보고 하 고 hello 보고는 활성 (즉, 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다.

실시간으로 위치는 *하지* toocompute 통계를 사용 합니다. 유일한 목적은 실시간 지리적 펜스 tooallow hello 사용 하는 \<지 오 펜싱 Reach-대상 그룹\> Reach 캠페인의 기준입니다.

tooenable 실시간 위치 보고는 hello hello Engagement 에이전트를 초기화 한 후 다음 줄을 추가 합니다.

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>GPS 기반 보고
기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다. GPS tooenable hello 사용 (임 훨씬 더 정확 하 게) 위치를 기반으로 추가 합니다.

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>백그라운드 보고
기본적으로 실시간 위치 보고는 활성 (즉, 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다. 백그라운드에서도 보고 tooenable hello를 추가 합니다.

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Hello 응용 프로그램은 백그라운드에서 실행을 기반으로 하는 네트워크 위치 뿐 보고, 사용 하도록 설정한 경우에 hello GPS 합니다.
>
>

이 함수의 구현을 호출 합니다 [startMonitoringSignificantLocationChanges] 응용 프로그램이 hello 배경으로 전환 하는 경우. 것은 자동으로 다시 시작 hello 배경으로 응용 프로그램 새 위치 이벤트가 도착 하는 경우 유의 합니다.

## <a name="advanced-reporting"></a>고급 보고
필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업을 하려는 경우 필요한 toouse hello Engagement API의 hello hello 메서드를 통해 `EngagementAgent` 클래스입니다. Hello를 호출 하 여이 클래스의 개체를 검색할 수 `[EngagementAgent shared]` 정적 메서드입니다.

hello Engagement API toouse Engagement의 고급 기능을 모두 허용 하 고 어떻게 hello에 자세히 설명 되어 tooUse iOS에서 Engagement API (뿐만 아니라 hello의 기술 문서 hello 에서처럼에서 `EngagementAgent` 클래스).

## <a name="disable-idfa-collection"></a>IDFA 컬렉션 비활성화
기본적으로 Engagement ´ ֲ hello [IDFA] toouniquely 사용자를 식별 합니다. 하지만 hello 응용 프로그램에서 다른 곳에서 보급을 사용 하지 않는 경우 있습니다 수에서 거부 hello 앱 스토어 검토 프로세스입니다. Hello 전처리기 매크로 추가 하 여 IDFA 수집을 해제할 수 있습니다 `ENGAGEMENT_DISABLE_IDFA` pch 파일에서 (또는 hello `Build Settings` 응용 프로그램의). 한지 참조가 너무 이렇게 하면`ASIdentifierManager`, `advertisingIdentifier` 또는 `isAdvertisingTrackingEnabled` hello 응용 프로그램 빌드에 있습니다.

통합 hello에 **prefix.pch** 파일:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Hello Engagement 테스트 로그를 확인 하 여 hello IDFA 수집은 응용 프로그램에서 제대로 해제를 확인할 수 있습니다. 통합 테스트 hello 참조\<ios-sdk-engagement-테스트-idfa\> 자세한 정보에 대 한 설명서입니다.

## <a name="disable-log-reporting"></a>로그 보고 사용 안 함
### <a name="using-a-method-call"></a>메서드 호출 사용
로그 보내기 Engagement toostop 하려는 경우 호출할 수 있습니다.

    [[EngagementAgent shared] setEnabled:NO];

이 호출은 영구적 이므로: 사용 하 여 `NSUserDefaults` toostore hello 정보입니다.

로그 다시 hello와 같은 함수를 호출 하 여 보고를 사용 하도록 설정할 수 `YES`합니다.

### <a name="integration-in-your-settings-bundle"></a>설정 번들의 통합
이 함수를 호출하지 않고, 기존 `Settings.bundle` 파일에서 이 설정을 직접 통합할 수 있습니다. 문자열 hello `engagement_agent_enabled` hello 기본 설정 식별자 해야 관련된 tooa 토글 스위치 사용 되어야 합니다 (`PSToggleSwitchSpecifier`).

다음 예의 hello `Settings.bundle` 표시 방법을 tooimplement 것:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[장치 API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
