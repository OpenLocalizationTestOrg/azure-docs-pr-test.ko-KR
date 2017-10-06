---
title: "aaaHow tooUse hello Android에서 Engagement API"
description: "최신 Android SDK-tooUse Android에서 Engagement API hello 하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="9dfb0-103">TooUse는 Android에서 Engagement API hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9dfb0-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="9dfb0-104">이 문서는 추가 기능 toohello 문서 [Android Mobile Engagement SDK에 대 한 고급 보고 옵션](mobile-engagement-android-advanced-reporting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="9dfb0-105">어떻게 toouse hello Engagement API tooreport 응용 프로그램 통계에 대 한 깊이 세부 정보에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="9dfb0-106">응용 프로그램의 세션, 활동, 충돌 및 기술 정보 Engagement tooreport 하려면, 다음 hello 가장 간단한 방법은 임을 toomake 모든 염두에 둬야 프로그램 `Activity` hello 해당 하위 클래스 상속 `EngagementActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="9dfb0-107">예를 들어 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, 필요한 경우 더 많은 toodo 하려는 경우 또는 tooreport 응용 프로그램의 활동에에서 있으면 다른 방식으로 hello hello에 구현 하는 보다 `EngagementActivity` toouse hello 필요 클래스 API 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="9dfb0-108">hello Engagement API에서 제공 hello `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="9dfb0-109">Hello를 호출 하 여이 클래스의 인스턴스를 검색할 수 있습니다 `EngagementAgent.getInstance(Context)` 정적 메서드 (해당 hello 참고 `EngagementAgent` 반환 된 개체는 단일).</span><span class="sxs-lookup"><span data-stu-id="9dfb0-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="9dfb0-110">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="9dfb0-110">Engagement concepts</span></span>
<span data-ttu-id="9dfb0-111">hello 다음과 같은 부분이 구체화 hello 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md), hello Android 플랫폼에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="9dfb0-112">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="9dfb0-112">`Session` and `Activity`</span></span>
<span data-ttu-id="9dfb0-113">Hello 사용자 유휴 두 개 이상의 몇 초 유지 *활동*, 그의 시퀀스의 다음 *활동* 분할 되며 두 개의 고유한 *세션*합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="9dfb0-114">이러한 몇 초 hello "세션 시간 제한" 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="9dfb0-115">*활동* toosay hello 된 hello 응용 프로그램의 한 화면은 주로 *활동* hello 화면에 표시 되 고 hello 화면을 닫으면이 중지 될 때 시작:이 hello 경우 hello Engagement SDK가 통합 hello를 사용 하 여 `EngagementActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="9dfb0-116">하지만 *활동* hello Engagement API를 사용 하 여 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="9dfb0-117">이렇게 하면 toosplit 각된 화면에 대 한 자세한 내용은 hello 사용 현황 (예: tooknown 얼마나 자주 및이 화면 안에 대화 상자 사용 되는 시간)이 화면의 여러 하위 부분 tooget 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="9dfb0-118">활동 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9dfb0-119">Hello를 사용 하는 경우이 섹션에 설명 된 tooreport 활동과 같은 활동 필요 하지 않습니다 `EngagementActivity` 클래스 및 변형 방법을 hello에 설명 된 대로 Android 문서에 Engagement tooIntegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="9dfb0-120">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="9dfb0-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="9dfb0-121">Toocall 필요한 `startActivity()` 각 시간 hello 사용자 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="9dfb0-122">첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="9dfb0-123">각 작업에 대해이 함수는 가장 좋은 곳 toocall hello `onResume` 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="9dfb0-124">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="9dfb0-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="9dfb0-125">Toocall 필요한 `endActivity()` hello 사용자 자신의 마지막 활동을 완료 하는 때 한 번 이상.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="9dfb0-126">이 hello Engagement SDK hello 사용자가 현재 유휴 및 hello 사용자 세션에 필요 하며 toobe 닫힌 hello 세션 시간 제한 한 번 만료 됩니다를 통해 알립니다 (호출 하는 경우 `startActivity()` hello 세션이 재개 되 단순히 hello 세션 제한 시간 만료 되기 전에).</span><span class="sxs-lookup"><span data-stu-id="9dfb0-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="9dfb0-127">각 작업에 대해이 함수는 가장 좋은 곳 toocall hello `onPause` 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="9dfb0-128">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="9dfb0-129">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="9dfb0-129">Session events</span></span>
<span data-ttu-id="9dfb0-130">세션 이벤트는 세션 동안 사용자가 수행 하는 일반적으로 사용 되는 tooreport hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="9dfb0-131">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="9dfb0-132">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="9dfb0-133">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="9dfb0-133">Standalone Events</span></span>
<span data-ttu-id="9dfb0-134">반대 toosession 이벤트 독립 실행형 이벤트 세션의 hello 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="9dfb0-135">**예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-135">**Example:**</span></span>

<span data-ttu-id="9dfb0-136">브로드캐스트 수신기 트리거될 때 발생 하는 tooreport 이벤트를 원하는 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="9dfb0-137">오류 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="9dfb0-138">세션 오류</span><span class="sxs-lookup"><span data-stu-id="9dfb0-138">Session errors</span></span>
<span data-ttu-id="9dfb0-139">세션 오류는 일반적으로 사용 되는 tooreport hello 오류 hello 사용자 세션 동안 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="9dfb0-140">**예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="9dfb0-141">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="9dfb0-141">Standalone errors</span></span>
<span data-ttu-id="9dfb0-142">반대 toosession 오류 세션의 hello 컨텍스트 외부에서 독립 실행형 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="9dfb0-143">**예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-143">**Example:**</span></span>

<span data-ttu-id="9dfb0-144">hello 다음 예제에서는 tooreport 오류가 hello 메모리 부족 hello 전화 응용 프로그램 프로세스 동안 될 때마다 실행 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="9dfb0-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="9dfb0-145">작업 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="9dfb0-146">예제</span><span class="sxs-lookup"><span data-stu-id="9dfb0-146">Example</span></span>
<span data-ttu-id="9dfb0-147">로그인 프로세스의 기간을 tooreport hello 일정 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="9dfb0-148">작업 중 오류 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-148">Report Errors during a Job</span></span>
<span data-ttu-id="9dfb0-149">오류 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="9dfb0-150">**예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-150">**Example:**</span></span>

<span data-ttu-id="9dfb0-151">Tooreport 한다고 가정 하면 수행 하는 동안 로그인 프로세스:</span><span class="sxs-lookup"><span data-stu-id="9dfb0-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="9dfb0-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="9dfb0-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="9dfb0-153">작업 중 이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-153">Reporting Events during a job</span></span>
<span data-ttu-id="9dfb0-154">이벤트 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="9dfb0-155">**예제:**</span><span class="sxs-lookup"><span data-stu-id="9dfb0-155">**Example:**</span></span>

<span data-ttu-id="9dfb0-156">소셜 네트워크는 한 작업 tooreport hello 총 시간 사용는 hello 하는 동안 사용자가 연결 된 toohello 서버 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="9dfb0-157">hello 사용자 연결을 유지할 수 백그라운드에서 hello 전화는 절전 모드 또는 다른 응용 프로그램을 사용 하는 경우에 이므로 세션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="9dfb0-158">hello 사용자 친구에서 메시지를 받을 수, 작업 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="9dfb0-159">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="9dfb0-159">Extra parameters</span></span>
<span data-ttu-id="9dfb0-160">임의의 데이터에 연결 된 tooevents, 오류, 활동 및 작업 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="9dfb0-161">이 데이터는 구조화될 수 있으며, Android의 번들 클래스를 사용합니다. 이 클래스는 실제로 Android Intent의 추가 매개 변수처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="9dfb0-162">번들은 배열이나 다른 번들 인스턴스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dfb0-163">Parcelable 또는 순차 가능 매개 변수 모드로 전환할 경우 해야 자신의 `toString()` 메서드는 구현 된 tooreturn 사람이 읽을 수는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="9dfb0-164">`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="9dfb0-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="9dfb0-165">추가 매개 변수의 스파스 배열은 지원되지 않습니다. 즉, 배열로 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="9dfb0-166">추가 매개 변수에서 배열을 사용하기 전에 표준 배열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="9dfb0-167">예제</span><span class="sxs-lookup"><span data-stu-id="9dfb0-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="9dfb0-168">제한</span><span class="sxs-lookup"><span data-stu-id="9dfb0-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="9dfb0-169">구성</span><span class="sxs-lookup"><span data-stu-id="9dfb0-169">Keys</span></span>
<span data-ttu-id="9dfb0-170">각 키 hello에 `Bundle` hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="9dfb0-171">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="9dfb0-172">크기</span><span class="sxs-lookup"><span data-stu-id="9dfb0-172">Size</span></span>
<span data-ttu-id="9dfb0-173">추가 항목은 너무 제한**1024** (한 번 인코딩된 json에서 hello Engagement 서비스에 의해) 호출당 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="9dfb0-174">Hello 앞의 예제 JSON 전송 toohello 서버 hello 58 자입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="9dfb0-175">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="9dfb0-175">Reporting Application Information</span></span>
<span data-ttu-id="9dfb0-176">Hello를 사용 하 여 정보 (또는 다른 응용 프로그램 관련 정보가) 추적을 수동으로 보고할 수 있습니다 `sendAppInfo()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="9dfb0-177">이러한 정보를 점진적으로 보낼 수 있는 참고: 지정된 된 장치에 대 한 지정된 된 키에 대 한 최신 값 hello만 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="9dfb0-178">이벤트, 기타 hello 번들 클래스는 응용 프로그램 정보를 사용 하는 tooabstract 마찬가지로 배열 또는 하위 묶습니다 (JSON 직렬화를 사용 하 여) 플랫 문자열으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="9dfb0-179">예제</span><span class="sxs-lookup"><span data-stu-id="9dfb0-179">Example</span></span>
<span data-ttu-id="9dfb0-180">코드 샘플 toosend 사용자 성별 및 생년월일 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="9dfb0-181">제한</span><span class="sxs-lookup"><span data-stu-id="9dfb0-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="9dfb0-182">구성</span><span class="sxs-lookup"><span data-stu-id="9dfb0-182">Keys</span></span>
<span data-ttu-id="9dfb0-183">각 키 hello에 `Bundle` hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="9dfb0-184">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="9dfb0-185">크기</span><span class="sxs-lookup"><span data-stu-id="9dfb0-185">Size</span></span>
<span data-ttu-id="9dfb0-186">응용 프로그램 정보는 너무 제한적**1024** (한 번 인코딩된 json에서 hello Engagement 서비스에 의해) 호출당 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="9dfb0-187">Hello 앞의 예제 JSON 전송 toohello 서버 hello 44 자입니다.</span><span class="sxs-lookup"><span data-stu-id="9dfb0-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
