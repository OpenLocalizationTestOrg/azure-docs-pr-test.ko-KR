---
title: "Windows 유니버설에서 Engagement API를 사용하는 방법"
description: "Windows 유니버설에서 Engagement API를 사용하는 방법"
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
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="574a5-103">Windows 유니버설에서 Engagement API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="574a5-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="574a5-104">이 문서는 [Windows 유니버설에서 Engagement를 통합하는 방법](mobile-engagement-windows-store-integrate-engagement.md)문서를 보완하는 추가 문서로, Engagement API를 사용하여 응용 프로그램 통계를 보고하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="574a5-105">Engagement에서 응용 프로그램 세션, 활동, 충돌 및 기술 정보만 보고하도록 하려는 경우, 가장 간단한 방법은 모든 `Page` 서브클래스가 `EngagementPage` 클래스에서 상속되도록 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="574a5-106">응용 프로그램 관련 이벤트, 오류, 작업을 보고하는 등 추가 작업을 수행하려는 경우 또는 `EngagementPage` 클래스에서 구현되는 것과는 다른 방식으로 응용 프로그램 활동을 보고해야 하는 경우에는 Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="574a5-107">Engagement API는 `EngagementAgent` 클래스를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="574a5-108">해당 메서드는 `EngagementAgent.Instance`을(를) 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="574a5-109">에이전트 모듈이 초기화되지 않은 경우에도 각 API 호출은 연기되며 에이전트를 사용할 수 있게 되면 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="574a5-110">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="574a5-110">Engagement concepts</span></span>
<span data-ttu-id="574a5-111">다음 요소는 Windows 유니버설 플랫폼과 관련된 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) 을 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="574a5-112">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="574a5-112">`Session` and `Activity`</span></span>
<span data-ttu-id="574a5-113">*작업*은 일반적으로 단일 응용 프로그램 페이지와 연결됩니다. 즉 *작업*은 페이지를 표시하면 시작되며 페이지를 닫으면 중지됩니다. `EngagementPage` 클래스를 사용하여 Engagement SDK를 통합하는 경우 이러한 방식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="574a5-114">하지만 Engagement API를 사용하여 *활동* 을 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="574a5-115">이렇게 하면 지정된 페이지를 여러 하위 부분으로 분할하여 해당 페이지의 사용에 대해 더 많은 세부 정보(예: 이 페이지 내에서 대화 상자를 사용하는 빈도와 기간)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="574a5-116">활동 보고</span><span class="sxs-lookup"><span data-stu-id="574a5-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="574a5-117">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="574a5-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-118">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-119">사용자 활동이 변경될 때마다 `StartActivity()` 을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="574a5-120">이 함수를 처음 호출하면 새 사용자 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="574a5-121">응용 프로그램을 닫을 때 SDK는 EndActivity 메서드를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="574a5-122">따라서 사용자 활동이 변경될 때마다 StartActivity 메서드를 호출하는 것이 좋으며 EndActivity 메서드는 호출하지 않는 것이 좋습니다. EndActivity 메서드를 호출하면 현재 세션이 강제로 종료되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="574a5-123">예</span><span class="sxs-lookup"><span data-stu-id="574a5-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="574a5-124">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="574a5-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-125">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="574a5-126">활동과 세션이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-126">This ends the activity and the session.</span></span> <span data-ttu-id="574a5-127">반드시 필요한 경우가 아니면 이 메서드를 호출해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-128">예</span><span class="sxs-lookup"><span data-stu-id="574a5-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="574a5-129">작업 보고</span><span class="sxs-lookup"><span data-stu-id="574a5-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="574a5-130">작업 시작</span><span class="sxs-lookup"><span data-stu-id="574a5-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-131">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-132">작업을 사용하여 일정 기간 동안의 특정 태스크를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-133">예</span><span class="sxs-lookup"><span data-stu-id="574a5-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="574a5-134">작업 종료</span><span class="sxs-lookup"><span data-stu-id="574a5-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-135">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="574a5-136">작업에 의해 추적되는 태스크가 종료되는 즉시 해당 작업에 대해 작업 이름을 제공하여 EndJob 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-137">예</span><span class="sxs-lookup"><span data-stu-id="574a5-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="574a5-138">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="574a5-138">Reporting Events</span></span>
<span data-ttu-id="574a5-139">이벤트에는 다음의 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-139">There is three types of events :</span></span>

* <span data-ttu-id="574a5-140">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="574a5-140">Standalone events</span></span>
* <span data-ttu-id="574a5-141">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="574a5-141">Session events</span></span>
* <span data-ttu-id="574a5-142">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="574a5-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="574a5-143">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="574a5-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-144">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-145">독립 실행형 이벤트는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-146">예</span><span class="sxs-lookup"><span data-stu-id="574a5-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="574a5-147">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="574a5-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-148">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-149">세션 이벤트는 일반적으로 사용자가 세션 중에 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-150">예</span><span class="sxs-lookup"><span data-stu-id="574a5-150">Example</span></span>
<span data-ttu-id="574a5-151">**데이터 제외:**</span><span class="sxs-lookup"><span data-stu-id="574a5-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="574a5-152">**데이터 포함:**</span><span class="sxs-lookup"><span data-stu-id="574a5-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="574a5-153">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="574a5-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-154">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-155">작업 이벤트는 일반적으로 사용자가 작업 중에 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-156">예</span><span class="sxs-lookup"><span data-stu-id="574a5-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="574a5-157">오류 보고</span><span class="sxs-lookup"><span data-stu-id="574a5-157">Reporting Errors</span></span>
<span data-ttu-id="574a5-158">세 가지 유형의 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-158">There are three types of errors :</span></span>

* <span data-ttu-id="574a5-159">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="574a5-159">Standalone errors</span></span>
* <span data-ttu-id="574a5-160">세션 오류</span><span class="sxs-lookup"><span data-stu-id="574a5-160">Session errors</span></span>
* <span data-ttu-id="574a5-161">작업 오류</span><span class="sxs-lookup"><span data-stu-id="574a5-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="574a5-162">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="574a5-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-163">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-164">세션 오류와 달리 독립 실행형 오류는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-165">예</span><span class="sxs-lookup"><span data-stu-id="574a5-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="574a5-166">세션 오류</span><span class="sxs-lookup"><span data-stu-id="574a5-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-167">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-168">세션 오류는 일반적으로 세션 중에 사용자에게 영향을 주는 오류를 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-169">예</span><span class="sxs-lookup"><span data-stu-id="574a5-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="574a5-170">작업 오류</span><span class="sxs-lookup"><span data-stu-id="574a5-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-171">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="574a5-172">오류는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-173">예</span><span class="sxs-lookup"><span data-stu-id="574a5-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="574a5-174">작동 중단 보고</span><span class="sxs-lookup"><span data-stu-id="574a5-174">Reporting Crashes</span></span>
<span data-ttu-id="574a5-175">에이전트는 작동 중단을 처리하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="574a5-176">예외 보내기</span><span class="sxs-lookup"><span data-stu-id="574a5-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-177">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="574a5-178">예</span><span class="sxs-lookup"><span data-stu-id="574a5-178">Example</span></span>
<span data-ttu-id="574a5-179">언제든지 다음을 호출하여 예외를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="574a5-180">또한 선택적 매개 변수를 사용하여 작동 중단을 보냄과 동시에 Engagement 세션을 종료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="574a5-181">이렇게 하려면 다음을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="574a5-182">이 경우 작동 중단을 보낸 직후에 세션과 작업이 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="574a5-183">처리되지 않은 예외 보내기</span><span class="sxs-lookup"><span data-stu-id="574a5-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="574a5-184">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="574a5-185">Engagement의 자동 **충돌** 보고를 **사용 안 함**으로 설정한 경우에는 처리되지 않은 예외를 보내는 방법도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="574a5-186">이 방법은 응용 프로그램 UnhandledException 이벤트 처리기 내에서 사용하는 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="574a5-187">이 방법을 사용하는 경우 **항상** Engagement 세션과 작업이 호출된 후에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="574a5-188">예</span><span class="sxs-lookup"><span data-stu-id="574a5-188">Example</span></span>
<span data-ttu-id="574a5-189">이 방법을 사용하면 고유한 UnhandledExceptionEventArgs 처리기를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="574a5-190">예를 들어 다음과 같이 `App.xaml.cs` 파일의 `Current_UnhandledException` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="574a5-191">App.xaml.cs의 "Public App(){}"에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="574a5-192">장치 ID</span><span class="sxs-lookup"><span data-stu-id="574a5-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="574a5-193">이 메서드를 호출하여 Engagement 장치 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="574a5-194">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="574a5-194">Extras parameters</span></span>
<span data-ttu-id="574a5-195">이벤트, 오류, 활동 또는 작업에 임의 데이터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="574a5-196">사전을 사용하여 이러한 데이터를 구조화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="574a5-197">모든 형식의 키와 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="574a5-198">extras 데이터는 serialize되므로 원하는 형식을 extras에 삽입하려면 해당 형식용 데이터 계약을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="574a5-199">예</span><span class="sxs-lookup"><span data-stu-id="574a5-199">Example</span></span>
<span data-ttu-id="574a5-200">아래 예제에서는 "Person"이라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="574a5-201">그런 다음 `Person` 인스턴스를 extras에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="574a5-202">다른 형식의 개체를 추가할 때는 사용자가 읽을 수 있는 문자열을 반환하도록 해당 ToString() 메서드를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="574a5-203">제한</span><span class="sxs-lookup"><span data-stu-id="574a5-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="574a5-204">구성</span><span class="sxs-lookup"><span data-stu-id="574a5-204">Keys</span></span>
<span data-ttu-id="574a5-205">개체의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="574a5-206">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="574a5-207">크기</span><span class="sxs-lookup"><span data-stu-id="574a5-207">Size</span></span>
<span data-ttu-id="574a5-208">extras는 호출당 **1024** 자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="574a5-209">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="574a5-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="574a5-210">참조</span><span class="sxs-lookup"><span data-stu-id="574a5-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="574a5-211">SendAppInfo() 함수를 사용하면 추적 정보 또는 기타 응용 프로그램 관련 정보를 수동으로 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="574a5-212">이 데이터를 증분 방식으로 보낼 수 있습니다. 그러면 특정 장치에 대해 지정한 키의 최신 값만 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="574a5-213">이벤트 추가 항목과 마찬가지로 Dictionary\<object, object\>를 사용하여 데이터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="574a5-214">예제</span><span class="sxs-lookup"><span data-stu-id="574a5-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="574a5-215">제한</span><span class="sxs-lookup"><span data-stu-id="574a5-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="574a5-216">구성</span><span class="sxs-lookup"><span data-stu-id="574a5-216">Keys</span></span>
<span data-ttu-id="574a5-217">개체의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="574a5-218">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="574a5-219">크기</span><span class="sxs-lookup"><span data-stu-id="574a5-219">Size</span></span>
<span data-ttu-id="574a5-220">응용 프로그램 정보는 호출당 **1024** 자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="574a5-221">위의 예제에서 서버로 전송된 JSON의 길이는 44자입니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="574a5-222">로깅</span><span class="sxs-lookup"><span data-stu-id="574a5-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="574a5-223">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="574a5-223">Enable Logging</span></span>
<span data-ttu-id="574a5-224">SDK는 IDE 콘솔에서 테스트 로그를 생성하도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="574a5-225">이러한 로그는 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-225">These logs are not activated by default.</span></span> <span data-ttu-id="574a5-226">이를 사용자 지정하려면 속성 `EngagementAgent.Instance.TestLogEnabled`를 `EngagementTestLogLevel` 열거형에서 사용 가능한 값 중 하나로 업데이트합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="574a5-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

