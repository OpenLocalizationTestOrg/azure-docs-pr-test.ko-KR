---
title: "Android에서 Engagement API를 사용하는 방법"
description: "최신 Android SDK - Android에서 Engagement API를 사용하는 방법"
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
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="962ce-103">Android에서 Engagement API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="962ce-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="962ce-104">이 문서는 [Android Mobile Engagement SDK에 대한 고급 보고 옵션](mobile-engagement-android-advanced-reporting.md)문서의 추가 자료입니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="962ce-105">Engagement API를 사용하여 응용 프로그램 통계를 보고하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="962ce-106">Engagement에서 응용 프로그램의 세션, 활동, 충돌 및 기술 정보만 보고하길 원하는 경우 가장 간단한 방법은 모든 `Activity` 하위 클래스가 해당 `EngagementActivity` 클래스에서 상속하도록 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="962ce-107">응용 프로그램 관련 이벤트, 오류, 작업을 보고하는 등 추가 작업을 수행하려는 경우 또는 `EngagementActivity` 클래스에서 구현되는 것과는 다른 방식으로 응용 프로그램 활동을 보고해야 하는 경우에는 Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="962ce-108">Engagement API는 `EngagementAgent` 클래스를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="962ce-109">이 클래스의 인스턴스는 `EngagementAgent.getInstance(Context)` 정적 메서드를 호출하여 검색할 수 있습니다(반환되는 `EngagementAgent` 개체는 단일 항목임).</span><span class="sxs-lookup"><span data-stu-id="962ce-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="962ce-110">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="962ce-110">Engagement concepts</span></span>
<span data-ttu-id="962ce-111">다음 요소는 Android 플랫폼과 관련된 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md)을 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="962ce-112">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="962ce-112">`Session` and `Activity`</span></span>
<span data-ttu-id="962ce-113">두 *작업* 간에 몇 초 넘게 유휴 상태로 있는 경우 *작업*의 시퀀스가 두 개의 *세션*으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="962ce-114">이러한 몇 초를 "세션 제한 시간"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="962ce-115">*작업*은 일반적으로 단일 응용 프로그램 화면과 연결됩니다. 즉, *작업*은 화면을 표시하면 시작되며 화면을 닫으면 중지됩니다. `EngagementActivity` 클래스를 사용하여 Engagement SDK를 통합하는 경우 이러한 방식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="962ce-116">하지만 Engagement API를 사용하여 *활동* 을 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="962ce-117">이렇게 하면 지정된 화면을 여러 하위 부분으로 분할하여 해당 화면의 사용에 대해 더 많은 세부 정보(예: 이 화면 내에서 대화 상자를 사용하는 빈도와 기간)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="962ce-118">활동 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="962ce-119">Android에서 Engagement를 통합하는 방법 문서에 설명된 `EngagementActivity` 클래스와 변형을 사용하는 경우 이 섹션에 설명된 것과 같은 활동을 보고할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="962ce-120">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="962ce-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="962ce-121">사용자 활동이 변경될 때마다 `startActivity()` 을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="962ce-122">이 함수를 처음 호출하면 새 사용자 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="962ce-123">이 함수는 각 활동 `onResume` 콜백에서 호출하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="962ce-124">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="962ce-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="962ce-125">사용자가 마지막 활동을 완료하면 `endActivity()`을(를) 한 번 이상 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="962ce-126">이 작업은 Engagement SDK에 사용자가 현재 유휴 상태이며, 세션 제한 시간이 만료되면 사용자 세션을 종료해야 한다는 것을 알립니다. 세션 제한 시간이 만료되기 전에 `startActivity()`을(를) 호출하는 경우 세션이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="962ce-127">이 함수는 각 활동 `onPause` 콜백에서 호출하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="962ce-128">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="962ce-129">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="962ce-129">Session events</span></span>
<span data-ttu-id="962ce-130">세션 이벤트는 일반적으로 사용자가 세션 중에 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="962ce-131">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="962ce-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="962ce-132">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="962ce-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="962ce-133">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="962ce-133">Standalone Events</span></span>
<span data-ttu-id="962ce-134">세션 이벤트와 반대로 독립 실행형 이벤트는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="962ce-135">**예:**</span><span class="sxs-lookup"><span data-stu-id="962ce-135">**Example:**</span></span>

<span data-ttu-id="962ce-136">브로드캐스트 수신기가 트리거될 때 발생하는 이벤트를 보고하려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="962ce-137">오류 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="962ce-138">세션 오류</span><span class="sxs-lookup"><span data-stu-id="962ce-138">Session errors</span></span>
<span data-ttu-id="962ce-139">세션 오류는 일반적으로 세션 중에 사용자에게 영향을 주는 오류를 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="962ce-140">**예제:**</span><span class="sxs-lookup"><span data-stu-id="962ce-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="962ce-141">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="962ce-141">Standalone errors</span></span>
<span data-ttu-id="962ce-142">세션 오류와 달리 독립 실행형 오류는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="962ce-143">**예:**</span><span class="sxs-lookup"><span data-stu-id="962ce-143">**Example:**</span></span>

<span data-ttu-id="962ce-144">다음 예제에서는 응용 프로그램 프로세스가 실행되는 동안 휴대폰의 메모리가 부족할 때마다 오류를 보고하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="962ce-145">작업 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="962ce-146">예</span><span class="sxs-lookup"><span data-stu-id="962ce-146">Example</span></span>
<span data-ttu-id="962ce-147">로그인 프로세스의 기간을 보고하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="962ce-148">작업 중 오류 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-148">Report Errors during a Job</span></span>
<span data-ttu-id="962ce-149">오류는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="962ce-150">**예:**</span><span class="sxs-lookup"><span data-stu-id="962ce-150">**Example:**</span></span>

<span data-ttu-id="962ce-151">프로세스에 로그인하는 동안 오류를 보고하려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="962ce-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="962ce-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="962ce-153">작업 중 이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-153">Reporting Events during a job</span></span>
<span data-ttu-id="962ce-154">이벤트는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="962ce-155">**예:**</span><span class="sxs-lookup"><span data-stu-id="962ce-155">**Example:**</span></span>

<span data-ttu-id="962ce-156">소셜 네트워크가 있으며 작업을 사용하여 사용자가 서버에 연결되어 있는 총 시간을 보고한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="962ce-157">사용자가 다른 응용 프로그램을 사용하거나 휴대폰이 절전 모드에 있는 경우에도 사용자가 백그라운드에서 연결을 유지할 수 있으므로, 세션이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="962ce-158">사용자는 친구로부터 메시지를 받을 수 있습니다. 이것이 작업 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-158">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="962ce-159">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="962ce-159">Extra parameters</span></span>
<span data-ttu-id="962ce-160">이벤트, 오류, 활동 또는 작업에 임의 데이터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="962ce-161">이 데이터는 구조화될 수 있으며, Android의 번들 클래스를 사용합니다. 이 클래스는 실제로 Android Intent의 추가 매개 변수처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="962ce-162">번들은 배열이나 다른 번들 인스턴스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="962ce-163">패키지 가능한 또는 직렬화 가능한 매개 변수를 넣는 경우 해당 `toString()` 메서드가 사람이 읽을 수 있는 문자열을 반환하도록 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="962ce-164">`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="962ce-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="962ce-165">추가 매개 변수의 스파스 배열은 지원되지 않습니다. 즉, 배열로 직렬화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="962ce-166">추가 매개 변수에서 배열을 사용하기 전에 표준 배열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="962ce-167">예제</span><span class="sxs-lookup"><span data-stu-id="962ce-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="962ce-168">제한</span><span class="sxs-lookup"><span data-stu-id="962ce-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="962ce-169">구성</span><span class="sxs-lookup"><span data-stu-id="962ce-169">Keys</span></span>
<span data-ttu-id="962ce-170">`Bundle` 의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="962ce-171">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="962ce-172">크기</span><span class="sxs-lookup"><span data-stu-id="962ce-172">Size</span></span>
<span data-ttu-id="962ce-173">추가 매개 변수는 호출당 **1024** 자(Engagement 서비스를 통해 JSON에서 한 번 인코딩됨)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="962ce-174">위의 예제에서 서버로 전송된 JSON의 길이는 58자입니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="962ce-175">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="962ce-175">Reporting Application Information</span></span>
<span data-ttu-id="962ce-176">`sendAppInfo()` 함수를 사용하면 추적 정보 또는 기타 응용 프로그램 관련 정보를 수동으로 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="962ce-177">이러한 정보는 증분 방식으로 보낼 수 있습니다. 그러면 특정 장치에 대해 지정한 키의 최신 값만 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="962ce-178">이벤트 추가 매개 변수와 마찬가지로, 번들 클래스는 응용 프로그램 정보를 추상화는 데 사용됩니다. 배열 또는 하위 번들은 단순 문자열로 처리됩니다(JSON 직렬화를 사용하여).</span><span class="sxs-lookup"><span data-stu-id="962ce-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="962ce-179">예제</span><span class="sxs-lookup"><span data-stu-id="962ce-179">Example</span></span>
<span data-ttu-id="962ce-180">사용자 성별 및 생년월일을 보내는 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="962ce-181">제한</span><span class="sxs-lookup"><span data-stu-id="962ce-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="962ce-182">구성</span><span class="sxs-lookup"><span data-stu-id="962ce-182">Keys</span></span>
<span data-ttu-id="962ce-183">`Bundle` 의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="962ce-184">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="962ce-185">크기</span><span class="sxs-lookup"><span data-stu-id="962ce-185">Size</span></span>
<span data-ttu-id="962ce-186">응용 프로그램 정보는 호출당 **1024** 자(Engagement 서비스를 통해 JSON에서 한 번 인코딩됨)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="962ce-187">위의 예제에서 서버로 전송된 JSON의 길이는 44자입니다.</span><span class="sxs-lookup"><span data-stu-id="962ce-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
