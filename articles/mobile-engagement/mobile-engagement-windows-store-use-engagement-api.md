---
title: "aaaHow tooUse hello에 Windows 유니버설 Engagement API"
description: "TooUse는 Engagement API에서 유니버설 Windows hello 하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="a75f8-103">TooUse는 Engagement API에서 유니버설 Windows hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a75f8-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="a75f8-104">이 문서는 추가 기능 toohello 문서 [어떻게 tooIntegrate Windows 유니버설에 Engagement](mobile-engagement-windows-store-integrate-engagement.md): 방법을 toouse hello Engagement API tooreport 응용 프로그램 통계에 대 한 깊이 세부 정보에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="a75f8-105">응용 프로그램의 세션, 활동, 충돌 및 기술 정보 Engagement tooreport 하려면, 다음 hello 가장 간단한 방법은 임을 toomake 모든 염두에 둬야 프로그램 `Page` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="a75f8-106">예를 들어 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, 필요한 경우 더 많은 toodo 하려는 경우 또는 tooreport 응용 프로그램의 활동에에서 있으면 다른 방식으로 hello hello에 구현 하는 보다 `EngagementPage` toouse hello 필요 클래스 API 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="a75f8-107">hello Engagement API에서 제공 hello `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="a75f8-108">통해 toothose 메서드에 액세스할 수 있습니다 `EngagementAgent.Instance`합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="a75f8-109">Hello 에이전트 모듈 초기화 되지 않은 경우에에 각 호출 toohello API 지연 되 고 hello 에이전트를 사용할 수 있는 경우 다시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="a75f8-110">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="a75f8-110">Engagement concepts</span></span>
<span data-ttu-id="a75f8-111">hello 다음과 같은 부분이 구체화 hello 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) hello 유니버설 Windows 플랫폼에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a75f8-112">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="a75f8-112">`Session` and `Activity`</span></span>
<span data-ttu-id="a75f8-113">*활동* toosay hello 된 hello 응용 프로그램의 한 페이지는 주로 *활동* hello 페이지가 표시 되 고 hello 페이지를 닫을 때 중지 될 때 시작: hello 좋다고 때 hello SDK 서비스는 hello를 사용 하 여 통합 된 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="a75f8-114">하지만 *활동* hello Engagement API를 사용 하 여 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="a75f8-115">이 몇 개에 지정된 된 페이지 하위 부분 tooget (예: tooknow 얼마나 자주 및이 페이지 안에 대화 상자 사용 되는 시간)이이 페이지의 hello 사용에 대 한 자세한 내용은 toosplit이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a75f8-116">활동 보고</span><span class="sxs-lookup"><span data-stu-id="a75f8-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a75f8-117">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="a75f8-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-118">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-119">Toocall 필요한 `StartActivity()` 각 시간 hello 사용자 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="a75f8-120">첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a75f8-121">hello SDK hello 응용 프로그램이 닫힐 때 자동으로 hello EndActivity 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="a75f8-122">따라서 좋습니다 toocall hello StartActivity 메서드 hello 사용자의 hello 활동 변경 되 고이 메서드를 호출 하는 이후 EndActivity 메서드 hello 강제로 hello 현재 세션 toobe tooNEVER 호출이 종료 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="a75f8-123">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="a75f8-124">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="a75f8-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-125">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="a75f8-126">Hello 활동 및 hello 세션 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="a75f8-127">반드시 필요한 경우가 아니면 이 메서드를 호출해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-128">예</span><span class="sxs-lookup"><span data-stu-id="a75f8-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="a75f8-129">작업 보고</span><span class="sxs-lookup"><span data-stu-id="a75f8-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="a75f8-130">작업 시작</span><span class="sxs-lookup"><span data-stu-id="a75f8-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-131">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-132">시간 동안 hello 작업 tootrack의 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-133">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="a75f8-134">작업 종료</span><span class="sxs-lookup"><span data-stu-id="a75f8-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-135">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="a75f8-136">추적 작업에 의해 작업이 종료 되는 즉시 hello 작업 이름을 제공 하 여이 작업에 대 한 hello 작업 끝 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-137">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="a75f8-138">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="a75f8-138">Reporting Events</span></span>
<span data-ttu-id="a75f8-139">이벤트에는 다음의 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-139">There is three types of events :</span></span>

* <span data-ttu-id="a75f8-140">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="a75f8-140">Standalone events</span></span>
* <span data-ttu-id="a75f8-141">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="a75f8-141">Session events</span></span>
* <span data-ttu-id="a75f8-142">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="a75f8-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="a75f8-143">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="a75f8-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-144">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-145">독립 실행형 이벤트 세션의 hello 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-146">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="a75f8-147">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="a75f8-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-148">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-149">세션 이벤트는 세션 동안 사용자가 수행 하는 일반적으로 사용 되는 tooreport hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-150">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-150">Example</span></span>
<span data-ttu-id="a75f8-151">**데이터 제외:**</span><span class="sxs-lookup"><span data-stu-id="a75f8-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="a75f8-152">**데이터 포함:**</span><span class="sxs-lookup"><span data-stu-id="a75f8-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="a75f8-153">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="a75f8-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-154">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-155">작업 이벤트는 일반적으로 사용 되는 tooreport hello 동작 하는 동안 사용자가 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-156">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="a75f8-157">오류 보고</span><span class="sxs-lookup"><span data-stu-id="a75f8-157">Reporting Errors</span></span>
<span data-ttu-id="a75f8-158">세 가지 유형의 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-158">There are three types of errors :</span></span>

* <span data-ttu-id="a75f8-159">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="a75f8-159">Standalone errors</span></span>
* <span data-ttu-id="a75f8-160">세션 오류</span><span class="sxs-lookup"><span data-stu-id="a75f8-160">Session errors</span></span>
* <span data-ttu-id="a75f8-161">작업 오류</span><span class="sxs-lookup"><span data-stu-id="a75f8-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="a75f8-162">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="a75f8-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-163">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-164">반대 toosession 오류 세션의 hello 컨텍스트 외부에서 독립 실행형 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-165">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="a75f8-166">세션 오류</span><span class="sxs-lookup"><span data-stu-id="a75f8-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-167">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-168">세션 오류는 일반적으로 사용 되는 tooreport hello 오류 hello 사용자 세션 동안 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-169">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="a75f8-170">작업 오류</span><span class="sxs-lookup"><span data-stu-id="a75f8-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-171">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="a75f8-172">오류 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-173">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="a75f8-174">작동 중단 보고</span><span class="sxs-lookup"><span data-stu-id="a75f8-174">Reporting Crashes</span></span>
<span data-ttu-id="a75f8-175">hello 에이전트 충돌와 두 개의 메서드 toodeal를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="a75f8-176">예외 보내기</span><span class="sxs-lookup"><span data-stu-id="a75f8-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-177">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="a75f8-178">예</span><span class="sxs-lookup"><span data-stu-id="a75f8-178">Example</span></span>
<span data-ttu-id="a75f8-179">언제든지 다음을 호출하여 예외를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="a75f8-180">Hello에 대 한 선택적 매개 변수 tooterminate hello engagement 세션을 사용할 수도 있습니다 동시 hello 크래시를 보내는 것 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="a75f8-181">toodo를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="a75f8-182">이렇게 하면 hello 세션 및 작업 닫힙니다 hello 크래시 보내는 직후 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="a75f8-183">처리되지 않은 예외 보내기</span><span class="sxs-lookup"><span data-stu-id="a75f8-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="a75f8-184">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="a75f8-185">Engagement는 또한 메서드 toosend 처리 되지 않은 예외를 제공 해야 하는 경우 **비활성화** Engagement 자동 **크래시** 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="a75f8-186">Hello 응용 프로그램 UnhandledException 이벤트 처리기 내에서 사용할 때 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="a75f8-187">이 방법은 **항상** 호출 된 후 hello engagement 세션 및 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="a75f8-188">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-188">Example</span></span>
<span data-ttu-id="a75f8-189">Tooimplement를 사용할 수 있습니다 자신만 UnhandledExceptionEventArgs 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="a75f8-190">예를 들어 hello 추가 `Current_UnhandledException` hello 방식의 `App.xaml.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="a75f8-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="a75f8-191">App.xaml.cs의 "Public App(){}"에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="a75f8-192">장치 ID</span><span class="sxs-lookup"><span data-stu-id="a75f8-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="a75f8-193">이 메서드를 호출 하 여 hello engagement 장치 id를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="a75f8-194">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a75f8-194">Extras parameters</span></span>
<span data-ttu-id="a75f8-195">임의의 데이터에 연결 된 tooan 이벤트, 오류, 작업 또는 작업 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="a75f8-196">사전을 사용하여 이러한 데이터를 구조화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="a75f8-197">모든 형식의 키와 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="a75f8-198">기타 데이터 tooinsert 추가 기능에서 사용자 정의 형식을 선택 해야 하므로 tooadd이이 형식에 대 한 데이터 계약 직렬화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="a75f8-199">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-199">Example</span></span>
<span data-ttu-id="a75f8-200">아래 예제에서는 "Person"이라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="a75f8-201">그런 다음 추가 됩니다 한 `Person` 인스턴스 tooan 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="a75f8-202">다른 형식의 개체를 두면 해당 tostring () 메서드 구현된 tooreturn 사람이 읽을 수 있는 문자열 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="a75f8-203">제한</span><span class="sxs-lookup"><span data-stu-id="a75f8-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a75f8-204">구성</span><span class="sxs-lookup"><span data-stu-id="a75f8-204">Keys</span></span>
<span data-ttu-id="a75f8-205">각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="a75f8-206">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a75f8-207">크기</span><span class="sxs-lookup"><span data-stu-id="a75f8-207">Size</span></span>
<span data-ttu-id="a75f8-208">추가 항목은 너무 제한**1024** 호출당 문자.</span><span class="sxs-lookup"><span data-stu-id="a75f8-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="a75f8-209">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="a75f8-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="a75f8-210">참조</span><span class="sxs-lookup"><span data-stu-id="a75f8-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="a75f8-211">수동으로 hello SendAppInfo() 함수를 사용 하 여 정보 (또는 다른 응용 프로그램 관련 정보가) 추적을 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="a75f8-212">이 데이터를 증분 방식으로 보낼 수 있는 참고: 지정된 된 장치에 대 한 지정된 된 키에 대 한 최신 값 hello만 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="a75f8-213">이벤트, 기타 같이 사전을 사용 하 여\<개체, 개체\> tooattach 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="a75f8-214">예제</span><span class="sxs-lookup"><span data-stu-id="a75f8-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="a75f8-215">제한</span><span class="sxs-lookup"><span data-stu-id="a75f8-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a75f8-216">구성</span><span class="sxs-lookup"><span data-stu-id="a75f8-216">Keys</span></span>
<span data-ttu-id="a75f8-217">각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="a75f8-218">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a75f8-219">크기</span><span class="sxs-lookup"><span data-stu-id="a75f8-219">Size</span></span>
<span data-ttu-id="a75f8-220">응용 프로그램 정보는 너무 제한적**1024** 호출당 문자.</span><span class="sxs-lookup"><span data-stu-id="a75f8-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="a75f8-221">Hello 앞의 예제 JSON 전송 toohello 서버 hello 44 자입니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="a75f8-222">로깅</span><span class="sxs-lookup"><span data-stu-id="a75f8-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="a75f8-223">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="a75f8-223">Enable Logging</span></span>
<span data-ttu-id="a75f8-224">hello SDK hello IDE 콘솔에서 구성 된 tooproduce 테스트 로그 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="a75f8-225">이러한 로그는 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a75f8-225">These logs are not activated by default.</span></span> <span data-ttu-id="a75f8-226">toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="a75f8-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

