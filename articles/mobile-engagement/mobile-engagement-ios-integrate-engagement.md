---
title: "Azure Mobile Engagement iOS SDK 통합 | Microsoft Docs"
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
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="6123e-103">IOS에서 Engagement를 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="6123e-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6123e-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="6123e-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="6123e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="6123e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="6123e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="6123e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="6123e-107">Android</span><span class="sxs-lookup"><span data-stu-id="6123e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="6123e-108">이 절차에서는 iOS 응용 프로그램에서 Engagement의 분석 및 모니터링 기능을 활성화하는 가장 간단한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="6123e-109">Engagement SDK에는 iOS7 이상 및 Xcode 8 이상이 필요합니다. 응용 프로그램의 배포 대상은 iOS 7 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="6123e-110">XCode 7을 사용하는 경우 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="6123e-111">iOS 10 장치에서 실행되는 경우 이 이전 버전의 도달률 모듈에서는 알려진 버그가 있습니다. 자세한 내용은 [도달률 모듈 통합](mobile-engagement-ios-integrate-engagement-reach.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6123e-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="6123e-112">SDK v3.2.4를 사용하도록 선택하는 경우 다음 단계의 `UserNotifications.framework` 가져오기로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="6123e-113">다음 단계만 수행하면 사용자, 세션, 활동, 작동 중단 및 기술과 관련된 모든 통계를 계산하는 데 필요한 로그 보고를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="6123e-114">이벤트, 오류, 작업 등의 기타 통계는 응용 프로그램별로 다르므로, 해당 통계를 계산하는 데 필요한 로그 보고는 Engagement API를 사용하여 수동으로 수행해야 합니다. 관련 설명은 [iOS 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-ios-use-engagement-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6123e-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="6123e-115">IOS 프로젝트에 Engagement SDK를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="6123e-116">[여기](http://aka.ms/qk2rnj)에서 iOS SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="6123e-117">iOS 프로젝트에 Engagement SDK를 추가합니다. Xcode에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **"다음에 파일 추가..."**를 선택하고 `EngagementSDK` 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="6123e-118">Engagement가 작동하려면 추가 프레임워크가 필요합니다. 프로젝트 탐색기에서 프로젝트 창을 열고 올바른 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="6123e-119">그런 다음 **"빌드 단계"** 탭을 열고 **"이진 파일과 라이브러리 연결"** 메뉴에서 다음 프레임워크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="6123e-120">`UserNotifications.framework` - 링크를 `Optional`(으)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="6123e-121">`AdSupport.framework` - 링크를 `Optional`(으)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="6123e-122">AdSupport 프레임워크는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="6123e-123">Engagement에서 IDFA를 수집하려면 이 프레임워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="6123e-124">그러나 이 ID와 관련된 새 Apple 정책을 준수하기 위해 IDFA 컬렉션을 비활성화할 수 있습니다(\<ios-sdk-engagement-idfa\>).</span><span class="sxs-lookup"><span data-stu-id="6123e-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="6123e-125">Engagement SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="6123e-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="6123e-126">다음과 같이 응용 프로그램 대리자를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="6123e-127">구현 파일의 맨 위에서 Engagement 에이전트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="6123e-128">'**applicationDidFinishLaunching:**' 또는 '**application:didFinishLaunchingWithOptions:**' 메서드에서 Engagement를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="6123e-129">기본 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="6123e-130">권장 방법: `UIViewController` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="6123e-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="6123e-131">Engagement에서 사용자, 세션, 활동, 크래시 및 기술 통계를 계산하기 위해 필요한 모든 로그의 보고서를 활성화하려면 모든 `UIViewController` 하위 클래스에서 `EngagementViewController` 클래스를 상속하도록 설정하면 됩니다(`UITableViewController` -\>`EngagementTableViewController`에 대한 동일한 규칙).</span><span class="sxs-lookup"><span data-stu-id="6123e-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="6123e-132">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="6123e-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="6123e-133">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="6123e-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="6123e-134">대체 메서드: 수동으로 `startActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="6123e-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="6123e-135">`UIViewController` 클래스를 오버로드할 수 없거나 하지 않으려는 경우 `EngagementAgent`의 메서드를 직접 호출하여 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6123e-136">응용 프로그램이 닫힐 때 iOS SDK에서 `endActivity()` 메서드를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="6123e-137">따라서 사용자 활동이 변경될 때마다 `startActivity` 메서드를 호출하는 것이 *상당히* 좋으며 `endActivity` 메서드는 호출하지 *않는* 것이 좋습니다. 이 메서드를 호출하면 현재 세션이 강제로 종료되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="6123e-138">위치 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-138">Location reporting</span></span>
<span data-ttu-id="6123e-139">Apple 서비스 약관에서는 응용 프로그램이 통계 용도로만 위치 추적 사용을 사용하도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="6123e-140">따라서 응용 프로그램이 다른 이유로도 추적 위치를 사용하는 경우에만 보고서 위치를 활성화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="6123e-141">iOS 8부터는 앱의 Info.plist 파일에서 [NSLocationWhenInUseUsageDescription] 또는 [NSLocationAlwaysUsageDescription] 키에 대한 문자열을 설정하여 앱이 위치 서비스를 사용하는 방법에 대한 설명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="6123e-142">Engagement로 백그라운드에서 위치를 보고하려는 경우 NSLocationAlwaysUsageDescription 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="6123e-143">다른 모든 경우에는 NSLocationWhenInUseUsageDescription 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="6123e-144">iOS 11에서 백그라운드 위치를 보고하려면 NSLocationAlwaysAndWhenInUseUsageDescription 및 NSLocationWhenInUseUsageDescription이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="6123e-145">지연 영역 위치 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-145">Lazy area location reporting</span></span>
<span data-ttu-id="6123e-146">지연 영역 위치 보고를 통해 국가, 지역 및 장치와 연결된 위치를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="6123e-147">이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="6123e-148">장치 영역은 세션당 한번 이하로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="6123e-149">GPS는 전혀 사용되지 않으므로 이러한 위치 보고는 배터리에 거의 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="6123e-150">보고된 영역은 사용자, 세션, 이벤트 및 오류에 대한 지리적 통계를 계산 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="6123e-151">이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="6123e-152">[장치 API]덕분에 장치에 대해 마지막으로 알려진 영역을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="6123e-153">지연 영역 위치 보고를 사용하려면 Engagement 에이전트를 초기화한 후 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="6123e-154">실시간 위치 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-154">Real time location reporting</span></span>
<span data-ttu-id="6123e-155">실시간 위치 보고를 통해 장치와 연결된 위도와 경도를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="6123e-156">기본적으로 이 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용하고, 보고는 응용 프로그램이 포그라운드로 실행될 때(즉, 세션 중)만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="6123e-157">실시간 위치는 통계를 계산하는 데 사용되지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="6123e-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="6123e-158">유일한 용도는 도달률 캠페인에서 실시간 지리적 펜스 \<Reach-Audience-geofencing\> 사용을 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="6123e-159">실시간 위치 보고를 활성화하려면 Engagement 에이전트를 초기화한 후 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="6123e-160">GPS 기반 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-160">GPS based reporting</span></span>
<span data-ttu-id="6123e-161">기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="6123e-162">훨씬 더 정밀한 GPS 기반 위치의 사용을 설정하려면 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="6123e-163">백그라운드 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-163">Background reporting</span></span>
<span data-ttu-id="6123e-164">기본적으로 실시간 위치 보고는 응용 프로그램이 포그라운드로 실행되는 경우(즉, 세션 중)에만 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="6123e-165">백그라운드에서도 보고를 활성화하려면 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="6123e-166">응용 프로그램이 백그라운드에서 실행될 때 GPS를 활성화한 경우에도 네트워크 기반 위치만 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="6123e-167">이 함수의 구현은 응용 프로그램이 백그라운드로 전환되는 경우 [startMonitoringSignificantLocationChanges] 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="6123e-168">새 위치 이벤트가 도달하는 경우 응용 프로그램을 백그라운드로 자동으로 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="6123e-169">고급 보고</span><span class="sxs-lookup"><span data-stu-id="6123e-169">Advanced reporting</span></span>
<span data-ttu-id="6123e-170">필요에 따라 응용 프로그램 관련 이벤트, 오류 및 작업을 보고하려는 경우 `EngagementAgent` 클래스의 메서드를 통해 Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="6123e-171">`[EngagementAgent shared]` 정적 메서드를 호출하여 이 클래스의 개체를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="6123e-172">Engagement API는 모든 Engagement의 고급 기능 사용을 허용하며 iOS의 Engagement API 사용 방법(및 `EngagementAgent` 클래스의 기술 문서)에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="6123e-173">IDFA 컬렉션 비활성화</span><span class="sxs-lookup"><span data-stu-id="6123e-173">Disable IDFA collection</span></span>
<span data-ttu-id="6123e-174">기본적으로 Engagement에서 [IDFA] 를 사용하여 사용자를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="6123e-175">그러나 앱의 다른 위치에서 알림을 사용하지 않는 경우 앱 스토어 검토 프로세스를 통해 거부될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="6123e-176">pch 파일에서(또는 응용 프로그램의 `Build Settings`에서) 전처리기 매크로 `ENGAGEMENT_DISABLE_IDFA`을(를) 추가하여 IDFA 컬렉션을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="6123e-177">따라서 응용 프로그램 빌드에서 `ASIdentifierManager`, `advertisingIdentifier` 또는 `isAdvertisingTrackingEnabled`에 대한 참조가 없다는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="6123e-178">**prefix.pch** 파일의 통합:</span><span class="sxs-lookup"><span data-stu-id="6123e-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="6123e-179">Engagement 테스트 로그를 확인하여 응용 프로그램에서 IDFA 컬렉션이 제대로 비활성화되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="6123e-180">자세한 내용은 통합 테스트\<ios-sdk-engagement-test-idfa\> 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6123e-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="6123e-181">로그 보고 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="6123e-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="6123e-182">메서드 호출 사용</span><span class="sxs-lookup"><span data-stu-id="6123e-182">Using a method call</span></span>
<span data-ttu-id="6123e-183">Engagement에서 로그 전송을 중지하려면 다음을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="6123e-184">이 호출은 영구적이며, `NSUserDefaults` 을(를) 사용하여 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="6123e-185">또한 `YES`(으)로 동일한 함수를 호출하여 로그 보고를 다시 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="6123e-186">설정 번들의 통합</span><span class="sxs-lookup"><span data-stu-id="6123e-186">Integration in your settings bundle</span></span>
<span data-ttu-id="6123e-187">이 함수를 호출하지 않고, 기존 `Settings.bundle` 파일에서 이 설정을 직접 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="6123e-188">문자열 `engagement_agent_enabled`은(는) 기본 설정 식별자로 사용해야 하며 토글 스위치(`PSToggleSwitchSpecifier`)와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="6123e-189">`Settings.bundle` 의 다음 예제에서는 구현 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6123e-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

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
<span data-ttu-id="6123e-190">[장치 API]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="6123e-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="6123e-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="6123e-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="6123e-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="6123e-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="6123e-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="6123e-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="6123e-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="6123e-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
