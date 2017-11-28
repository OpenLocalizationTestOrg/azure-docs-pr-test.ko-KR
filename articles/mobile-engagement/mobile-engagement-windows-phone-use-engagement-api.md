---
title: "Windows Phone Silverlight에서 Engagement API aaaHow tooUse hello"
description: "TooUse는 Windows Phone Silverlight에서 Engagement API hello 하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="d1b77-103">TooUse는 Windows Phone Silverlight에서 Engagement API hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1b77-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="d1b77-104">이 문서는 추가 기능 toohello 문서 [방법을 Windows Phone Silverlight 앱에서 Mobile Engagement toointegrate](mobile-engagement-windows-phone-integrate-engagement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="d1b77-105">어떻게 toouse hello Engagement API tooreport 응용 프로그램 통계에 대 한 깊이 세부 정보에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="d1b77-106">응용 프로그램의 세션, 활동, 충돌 및 기술 정보 Engagement tooreport 원하는 경우 가장 간단한 hello toomake 모든를 방식으로 프로그램 `PhoneApplicationPage` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="d1b77-107">예를 들어 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, 필요한 경우 더 많은 toodo 하려는 경우 또는 tooreport 응용 프로그램의 활동에에서 있으면 다른 방식으로 hello hello에 구현 하는 보다 `EngagementPage` toouse hello 필요 클래스 API 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="d1b77-108">hello Engagement API에서 제공 hello `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="d1b77-109">통해 toothose 메서드에 액세스할 수 있습니다 `EngagementAgent.Instance`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="d1b77-110">Hello 에이전트 모듈 초기화 되지 않은 경우에에 각 호출 toohello API 지연 되 고 hello 에이전트를 사용할 수 있는 경우 다시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="d1b77-111">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="d1b77-111">Engagement concepts</span></span>
<span data-ttu-id="d1b77-112">다음 부분 hello hello Windows Phone 플랫폼에 대 한 hello Mobile Engagement 개념을 구체화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="d1b77-113">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="d1b77-113">`Session` and `Activity`</span></span>
<span data-ttu-id="d1b77-114">*활동* toosay hello 된 hello 응용 프로그램의 한 페이지는 주로 *활동* hello 페이지가 표시 되 고 hello 페이지를 닫을 때 중지 될 때 시작: hello 좋다고 때 hello SDK 서비스는 hello를 사용 하 여 통합 된 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="d1b77-115">하지만 *활동* hello Engagement API를 사용 하 여 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="d1b77-116">이렇게 하면 toosplit 지정한 페이지에 대 한 자세한 내용은 hello 사용 현황 (예: tooknown 얼마나 자주 및이 페이지 안에 대화 상자 사용 되는 시간)이이 페이지의 여러 하위 부분 tooget 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="d1b77-117">활동 보고</span><span class="sxs-lookup"><span data-stu-id="d1b77-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="d1b77-118">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="d1b77-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-119">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-120">Toocall 필요한 `StartActivity()` 각 시간 hello 사용자 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="d1b77-121">첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1b77-122">hello SDK hello 응용 프로그램이 닫힐 때 자동으로 hello EndActivity 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="d1b77-123">따라서 좋습니다 toocall hello StartActivity 메서드 hello 사용자 변경 및 hello이이 메서드를 호출 하는 이후 EndActivity 메서드 강제로 hello 현재 세션 toobe tooNEVER 호출의 hello 작업이 종료 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="d1b77-124">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="d1b77-125">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="d1b77-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-126">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="d1b77-127">Toocall 필요한 `EndActivity()` hello 사용자 자신의 마지막 활동을 완료 하는 때 한 번 이상.</span><span class="sxs-lookup"><span data-stu-id="d1b77-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="d1b77-128">이 hello Engagement SDK hello 사용자가 현재 유휴 및 hello 사용자 세션에 필요 하며 toobe 닫힌 hello 세션 시간 제한 한 번 만료 됩니다를 통해 알립니다 (호출 하는 경우 `StartActivity()` hello 세션 계속 단순히 hello 세션 제한 시간 만료 되기 전에).</span><span class="sxs-lookup"><span data-stu-id="d1b77-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-129">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="d1b77-130">작업 보고</span><span class="sxs-lookup"><span data-stu-id="d1b77-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="d1b77-131">작업 시작</span><span class="sxs-lookup"><span data-stu-id="d1b77-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-132">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-133">시간 동안 hello 작업 tootrack의 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-134">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="d1b77-135">작업 종료</span><span class="sxs-lookup"><span data-stu-id="d1b77-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-136">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="d1b77-137">추적 작업에 의해 작업이 종료 되는 즉시 hello 작업 이름을 제공 하 여이 작업에 대 한 hello 작업 끝 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-138">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="d1b77-139">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="d1b77-139">Reporting Events</span></span>
<span data-ttu-id="d1b77-140">이벤트에는 다음의 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-140">There is three types of events :</span></span>

* <span data-ttu-id="d1b77-141">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="d1b77-141">Standalone events</span></span>
* <span data-ttu-id="d1b77-142">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="d1b77-142">Session events</span></span>
* <span data-ttu-id="d1b77-143">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="d1b77-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="d1b77-144">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="d1b77-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-145">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-146">독립 실행형 이벤트 세션의 hello 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-147">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="d1b77-148">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="d1b77-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-149">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-150">세션 이벤트는 세션 동안 사용자가 수행 하는 일반적으로 사용 되는 tooreport hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-151">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-151">Example</span></span>
<span data-ttu-id="d1b77-152">**데이터 제외:**</span><span class="sxs-lookup"><span data-stu-id="d1b77-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="d1b77-153">**데이터 포함:**</span><span class="sxs-lookup"><span data-stu-id="d1b77-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="d1b77-154">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="d1b77-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-155">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-156">작업 이벤트는 일반적으로 사용 되는 tooreport hello 동작 하는 동안 사용자가 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-157">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="d1b77-158">오류 보고</span><span class="sxs-lookup"><span data-stu-id="d1b77-158">Reporting Errors</span></span>
<span data-ttu-id="d1b77-159">오류에는 다음의 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-159">There is three types of errors :</span></span>

* <span data-ttu-id="d1b77-160">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="d1b77-160">Standalone errors</span></span>
* <span data-ttu-id="d1b77-161">세션 오류</span><span class="sxs-lookup"><span data-stu-id="d1b77-161">Session errors</span></span>
* <span data-ttu-id="d1b77-162">작업 오류</span><span class="sxs-lookup"><span data-stu-id="d1b77-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="d1b77-163">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="d1b77-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-164">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-165">반대 toosession 오류 세션의 hello 컨텍스트 외부에서 독립 실행형 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-166">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="d1b77-167">세션 오류</span><span class="sxs-lookup"><span data-stu-id="d1b77-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-168">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-169">세션 오류는 일반적으로 사용 되는 tooreport hello 오류 hello 사용자 세션 동안 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-170">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="d1b77-171">작업 오류</span><span class="sxs-lookup"><span data-stu-id="d1b77-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-172">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="d1b77-173">오류 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-174">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="d1b77-175">작동 중단 보고</span><span class="sxs-lookup"><span data-stu-id="d1b77-175">Reporting Crashes</span></span>
<span data-ttu-id="d1b77-176">hello 에이전트 충돌와 두 개의 메서드 toodeal를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="d1b77-177">예외 보내기</span><span class="sxs-lookup"><span data-stu-id="d1b77-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-178">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="d1b77-179">예</span><span class="sxs-lookup"><span data-stu-id="d1b77-179">Example</span></span>
<span data-ttu-id="d1b77-180">언제든지 다음을 호출하여 예외를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="d1b77-181">Hello에 대 한 선택적 매개 변수 tooterminate hello engagement 세션을 사용할 수도 있습니다 동시 hello 크래시를 보내는 것 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="d1b77-182">toodo를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="d1b77-183">이렇게 하면 hello 세션 및 작업 닫힙니다 hello 크래시 보내는 직후 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="d1b77-184">처리되지 않은 예외 보내기</span><span class="sxs-lookup"><span data-stu-id="d1b77-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="d1b77-185">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="d1b77-186">또한 engagement 메서드 toosend 처리 되지 않은 예외를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="d1b77-187">Hello silverlight UnhandledException 이벤트 처리기 내에서 사용할 때 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="d1b77-188">이 방법은 **항상** 호출 된 후 hello engagement 세션 및 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="d1b77-189">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-189">Example</span></span>
<span data-ttu-id="d1b77-190">Tooimplement를 사용할 수 있습니다 (특히 경우 hello 자동 충돌 보고 서비스의 기능을 사용 하지 않도록 설정한) 자신만 UnhandledException 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="d1b77-191">예를 들어 hello에에서 `Application_UnhandledException` hello 방식의 `App.xaml.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="d1b77-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="d1b77-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="d1b77-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="d1b77-193">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="d1b77-194">Hello 사용자 컨트롤에서 벗어나면 앞으로 응용 프로그램 hello Deactivated 이벤트 발생 한 후 hello 운영 체제는 유휴 상태가 tooput hello 응용 프로그램을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="d1b77-195">그런 다음 hello 응용 프로그램 삭제 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="d1b77-196">이 프로세스에서 응용 프로그램 종료 되지만 hello 상태 hello 응용 프로그램과 hello hello 응용 프로그램 내에서 개별 페이지에 대 한 일부 데이터 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="d1b77-197">Tooinsert 있는 `EngagementAgent.Instance.OnActivated(e)` hello에 `Application_Activated` hello App.xaml.cs 파일 tooreset hello hello 응용 프로그램 삭제 표시 됨으로 되었을 때 Engagement 에이전트에서에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1b77-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="d1b77-198">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="d1b77-199">장치 ID</span><span class="sxs-lookup"><span data-stu-id="d1b77-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="d1b77-200">이 메서드를 호출 하 여 hello engagement 장치 id를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="d1b77-201">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="d1b77-201">Extras parameters</span></span>
<span data-ttu-id="d1b77-202">임의의 데이터에 연결 된 tooan 이벤트, 오류, 작업 또는 작업 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="d1b77-203">사전을 사용하여 이러한 데이터를 구조화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="d1b77-204">모든 형식의 키와 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="d1b77-205">기타 데이터 tooinsert 추가 기능에서 사용자 정의 형식을 선택 해야 하므로 tooadd이이 형식에 대 한 데이터 계약 직렬화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="d1b77-206">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-206">Example</span></span>
<span data-ttu-id="d1b77-207">아래 예제에서는 "Person"이라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="d1b77-208">그런 다음 추가 됩니다 한 `Person` 인스턴스 tooan 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="d1b77-209">다른 형식의 개체를 두면 해당 tostring () 메서드 구현된 tooreturn 사람이 읽을 수 있는 문자열 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="d1b77-210">제한</span><span class="sxs-lookup"><span data-stu-id="d1b77-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="d1b77-211">구성</span><span class="sxs-lookup"><span data-stu-id="d1b77-211">Keys</span></span>
<span data-ttu-id="d1b77-212">각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="d1b77-213">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="d1b77-214">크기</span><span class="sxs-lookup"><span data-stu-id="d1b77-214">Size</span></span>
<span data-ttu-id="d1b77-215">추가 항목은 너무 제한**1024** 호출당 문자.</span><span class="sxs-lookup"><span data-stu-id="d1b77-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="d1b77-216">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="d1b77-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="d1b77-217">참조</span><span class="sxs-lookup"><span data-stu-id="d1b77-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="d1b77-218">수동으로 hello SendAppInfo() 함수를 사용 하 여 정보 (또는 다른 응용 프로그램 관련 정보가) 추적을 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="d1b77-219">이러한 정보를 점진적으로 보낼 수 있는 참고: 지정된 된 장치에 대 한 지정된 된 키에 대 한 최신 값 hello만 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="d1b77-220">이벤트, 기타 같이 사전을 사용 하 여\<개체, 개체\> tooattach 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="d1b77-221">예제</span><span class="sxs-lookup"><span data-stu-id="d1b77-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="d1b77-222">제한</span><span class="sxs-lookup"><span data-stu-id="d1b77-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="d1b77-223">구성</span><span class="sxs-lookup"><span data-stu-id="d1b77-223">Keys</span></span>
<span data-ttu-id="d1b77-224">각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="d1b77-225">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="d1b77-226">크기</span><span class="sxs-lookup"><span data-stu-id="d1b77-226">Size</span></span>
<span data-ttu-id="d1b77-227">응용 프로그램 정보는 너무 제한적**1024** 호출당 문자.</span><span class="sxs-lookup"><span data-stu-id="d1b77-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="d1b77-228">Hello 앞의 예제 JSON 전송 toohello 서버 hello 44 자입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="d1b77-229">로깅</span><span class="sxs-lookup"><span data-stu-id="d1b77-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="d1b77-230">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="d1b77-230">Enable Logging</span></span>
<span data-ttu-id="d1b77-231">hello SDK hello IDE 콘솔에서 구성 된 tooproduce 테스트 로그 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="d1b77-232">이러한 로그는 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b77-232">These logs are not activated by default.</span></span> <span data-ttu-id="d1b77-233">toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d1b77-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
