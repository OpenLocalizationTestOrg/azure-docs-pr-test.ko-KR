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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="3b98a-103">어떻게 tooIntegrate Engagement iOS에서</span><span class="sxs-lookup"><span data-stu-id="3b98a-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b98a-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="3b98a-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="3b98a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3b98a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="3b98a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3b98a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="3b98a-107">Android</span><span class="sxs-lookup"><span data-stu-id="3b98a-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="3b98a-108">이 절차에서는 hello 가장 간단한 방법은 tooactivate Engagement의 분석 및 iOS 응용 프로그램의 함수 모니터링을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="3b98a-109">hello Engagement SDK 필요 iOS7 + 및 Xcode 8 +: hello 배포 대상 응용 프로그램의 이상 이어야 합니다 iOS 7입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="3b98a-110">XCode 7에 실제로 종속 경우 hello를 사용할 수 있습니다 [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="3b98a-111">10 iOS 장치 참조에서 실행 되는 동안이 이전 버전의 hello 모듈이에 알려진된 버그가 있습니다 [reach 모듈 통합 hello](mobile-engagement-ios-integrate-engagement-reach.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="3b98a-112">Toouse hello SDK v3.2.4를 선택한 다음 방금 hello를 건너뛸 경우 `UserNotifications.framework` hello 다음 단계에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="3b98a-113">단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivate hello 보고서의 로그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="3b98a-114">hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 iOS 응용 프로그램에서 API 태그를 지정 하는 Mobile Engagement](mobile-engagement-ios-use-engagement-api.md) 후 이러한 통계 응용 프로그램이 종속 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="3b98a-115">IOS 프로젝트에 hello Engagement SDK를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="3b98a-116">Hello iOS SDK 다운로드에서 [여기](http://aka.ms/qk2rnj)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="3b98a-117">Hello Engagement SDK tooyour iOS 프로젝트 추가: 프로젝트 및 선택 사항에 Xcode에서 마우스 오른쪽 단추로 클릭 **"파일을 너무 추가..."** hello 선택 `EngagementSDK` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="3b98a-118">계약 추가 프레임 워크 toowork 필요: hello 프로젝트 탐색기에서 프로젝트 창을 열고 선택 hello 올바른 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="3b98a-119">그런 다음 hello를 열고 **"빌드 단계"** 탭 및 hello **"링크 이진 파일과 라이브러리"** 메뉴에서 이러한 프레임 워크 추가:</span><span class="sxs-lookup"><span data-stu-id="3b98a-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="3b98a-120">`UserNotifications.framework`-으로 hello 링크 설정`Optional`</span><span class="sxs-lookup"><span data-stu-id="3b98a-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="3b98a-121">`AdSupport.framework`-으로 hello 링크 설정`Optional`</span><span class="sxs-lookup"><span data-stu-id="3b98a-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="3b98a-122">hello AdSupport 프레임 워크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="3b98a-123">서비스는 프레임 워크 toocollect hello IDFA이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="3b98a-124">그러나 IDFA 수집을 해제할 수 있습니다 \<ios sdk-engagement idfa\> 이 ID에 대 한 hello 새 Apple 정책과 toocomply</span><span class="sxs-lookup"><span data-stu-id="3b98a-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="3b98a-125">Hello Engagement SDK를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="3b98a-126">응용 프로그램 대리자 toomodify 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="3b98a-127">구현 파일의 hello 위쪽 hello Engagement 에이전트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="3b98a-128">Hello 메서드 내부 Engagement 초기화 '**applicationDidFinishLaunching:**'또는'**응용 프로그램: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="3b98a-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="3b98a-129">기본 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="3b98a-130">권장 방법: `UIViewController` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="3b98a-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="3b98a-131">Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 만들 수 있습니다 모든 프로그램 `UIViewController` hello에서 하위 클래스 상속 `EngagementViewController` 클래스 (동일한 규칙 에 대 한 `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="3b98a-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="3b98a-132">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="3b98a-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="3b98a-133">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="3b98a-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="3b98a-134">대체 메서드: 수동으로 `startActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="3b98a-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="3b98a-135">처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `UIViewController` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent`의 메서드를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b98a-136">hello를 자동으로 호출 하는 hello iOS SDK `endActivity()` hello 응용 프로그램을 닫으면 메서드.</span><span class="sxs-lookup"><span data-stu-id="3b98a-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="3b98a-137">즉, *항상* toocall hello 권장 `startActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무*NEVER* 호출 hello `endActivity` 이 메서드를 사용 하면 호출 이후 메서드 현재 세션 toobe hello 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="3b98a-138">위치 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-138">Location reporting</span></span>
<span data-ttu-id="3b98a-139">서비스 약관 Apple 응용 프로그램 통계 용도로 추적 toouse 위치를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="3b98a-140">따라서 좋습니다 tooenable 위치 보고서 응용 프로그램 hello 위치는 또 다른 이유에 대 한 추적을 사용 하는 경우에.</span><span class="sxs-lookup"><span data-stu-id="3b98a-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="3b98a-141">IOS 8 이상에서는 응용 프로그램 hello 키에 대 한 문자열을 설정 하 여 위치 확인 서비스를 사용 하는 방법에 대 한 설명을 제공 해야 [NSLocationWhenInUseUsageDescription] 또는 [NSLocationAlwaysUsageDescription]앱의 Info.plist 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="3b98a-142">Tooreport 위치 Engagement와 hello 백그라운드에서 원하는 NSLocationAlwaysUsageDescription hello 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="3b98a-143">다른 모든 경우에 NSLocationWhenInUseUsageDescription hello 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="3b98a-144">참고 iOS 11에서 NSLocationAlwaysAndWhenInUseUsageDescription와 NSLocationWhenInUseUsageDescription tooreport 배경 위치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="3b98a-145">지연 영역 위치 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-145">Lazy area location reporting</span></span>
<span data-ttu-id="3b98a-146">Tooreport hello 국가, 지역 및 연결 된 위치를 사용 하면 지연 된 영역 위치 보고 toodevices 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="3b98a-147">이러한 유형의 위치 보고에서는 네트워크 위치(셀 ID 또는 WIFI 기반)만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="3b98a-148">hello 장치 영역의 세션당 한 번만 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="3b98a-149">hello GPS은 사용 되지 않거나, 고 따라서 이러한 유형의 위치 보고서에 거의 (하지 toosay 없음) hello 배터리에 미치는 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="3b98a-150">보고 된 영역은 사용자, 세션, 이벤트 및 오류에 대 한 사용 되는 toocompute 지리적 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="3b98a-151">이 영역은 도달률 캠페인의 기준으로도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="3b98a-152">장치는 검색 된 감사 toohello 수에 대해 보고 하는 영역을 마지막으로 hello [장치 API]합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="3b98a-153">tooenable 지연 된 영역 위치 보고는 hello hello Engagement 에이전트를 초기화 한 후 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="3b98a-154">실시간 위치 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-154">Real time location reporting</span></span>
<span data-ttu-id="3b98a-155">Tooreport hello 위도 및 경도 연결을 사용 하면 실시간 위치 보고 toodevices 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="3b98a-156">기본적으로 네트워크 위치 (셀 ID 또는 WIFI에 따라)에 사용 하 여 이러한 유형의 위치를 보고 하 고 hello 보고는 활성 (즉, 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="3b98a-157">실시간으로 위치는 *하지* toocompute 통계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="3b98a-158">유일한 목적은 실시간 지리적 펜스 tooallow hello 사용 하는 \<지 오 펜싱 Reach-대상 그룹\> Reach 캠페인의 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="3b98a-159">tooenable 실시간 위치 보고는 hello hello Engagement 에이전트를 초기화 한 후 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="3b98a-160">GPS 기반 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-160">GPS based reporting</span></span>
<span data-ttu-id="3b98a-161">기본적으로 실시간 위치 보고에서는 네트워크 기반 위치만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="3b98a-162">GPS tooenable hello 사용 (임 훨씬 더 정확 하 게) 위치를 기반으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="3b98a-163">백그라운드 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-163">Background reporting</span></span>
<span data-ttu-id="3b98a-164">기본적으로 실시간 위치 보고는 활성 (즉, 동안 세션) 포그라운드에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="3b98a-165">백그라운드에서도 보고 tooenable hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="3b98a-166">Hello 응용 프로그램은 백그라운드에서 실행을 기반으로 하는 네트워크 위치 뿐 보고, 사용 하도록 설정한 경우에 hello GPS 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="3b98a-167">이 함수의 구현을 호출 합니다 [startMonitoringSignificantLocationChanges] 응용 프로그램이 hello 배경으로 전환 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3b98a-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="3b98a-168">것은 자동으로 다시 시작 hello 배경으로 응용 프로그램 새 위치 이벤트가 도착 하는 경우 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="3b98a-169">고급 보고</span><span class="sxs-lookup"><span data-stu-id="3b98a-169">Advanced reporting</span></span>
<span data-ttu-id="3b98a-170">필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업을 하려는 경우 필요한 toouse hello Engagement API의 hello hello 메서드를 통해 `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="3b98a-171">Hello를 호출 하 여이 클래스의 개체를 검색할 수 `[EngagementAgent shared]` 정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="3b98a-172">hello Engagement API toouse Engagement의 고급 기능을 모두 허용 하 고 어떻게 hello에 자세히 설명 되어 tooUse iOS에서 Engagement API (뿐만 아니라 hello의 기술 문서 hello 에서처럼에서 `EngagementAgent` 클래스).</span><span class="sxs-lookup"><span data-stu-id="3b98a-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="3b98a-173">IDFA 컬렉션 비활성화</span><span class="sxs-lookup"><span data-stu-id="3b98a-173">Disable IDFA collection</span></span>
<span data-ttu-id="3b98a-174">기본적으로 Engagement ´ ֲ hello [IDFA] toouniquely 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="3b98a-175">하지만 hello 응용 프로그램에서 다른 곳에서 보급을 사용 하지 않는 경우 있습니다 수에서 거부 hello 앱 스토어 검토 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="3b98a-176">Hello 전처리기 매크로 추가 하 여 IDFA 수집을 해제할 수 있습니다 `ENGAGEMENT_DISABLE_IDFA` pch 파일에서 (또는 hello `Build Settings` 응용 프로그램의).</span><span class="sxs-lookup"><span data-stu-id="3b98a-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="3b98a-177">한지 참조가 너무 이렇게 하면`ASIdentifierManager`, `advertisingIdentifier` 또는 `isAdvertisingTrackingEnabled` hello 응용 프로그램 빌드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="3b98a-178">통합 hello에 **prefix.pch** 파일:</span><span class="sxs-lookup"><span data-stu-id="3b98a-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="3b98a-179">Hello Engagement 테스트 로그를 확인 하 여 hello IDFA 수집은 응용 프로그램에서 제대로 해제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="3b98a-180">통합 테스트 hello 참조\<ios-sdk-engagement-테스트-idfa\> 자세한 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="3b98a-181">로그 보고 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="3b98a-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="3b98a-182">메서드 호출 사용</span><span class="sxs-lookup"><span data-stu-id="3b98a-182">Using a method call</span></span>
<span data-ttu-id="3b98a-183">로그 보내기 Engagement toostop 하려는 경우 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="3b98a-184">이 호출은 영구적 이므로: 사용 하 여 `NSUserDefaults` toostore hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="3b98a-185">로그 다시 hello와 같은 함수를 호출 하 여 보고를 사용 하도록 설정할 수 `YES`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="3b98a-186">설정 번들의 통합</span><span class="sxs-lookup"><span data-stu-id="3b98a-186">Integration in your settings bundle</span></span>
<span data-ttu-id="3b98a-187">이 함수를 호출하지 않고, 기존 `Settings.bundle` 파일에서 이 설정을 직접 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b98a-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="3b98a-188">문자열 hello `engagement_agent_enabled` hello 기본 설정 식별자 해야 관련된 tooa 토글 스위치 사용 되어야 합니다 (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="3b98a-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="3b98a-189">다음 예의 hello `Settings.bundle` 표시 방법을 tooimplement 것:</span><span class="sxs-lookup"><span data-stu-id="3b98a-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
