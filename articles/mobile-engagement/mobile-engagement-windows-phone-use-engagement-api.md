---
title: "Windows Phone Silverlight에서 Engagement API를 사용하는 방법"
description: "Windows Phone Silverlight에서 Engagement API를 사용하는 방법"
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
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="687d4-103">Windows Phone Silverlight에서 Engagement API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="687d4-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="687d4-104">이 문서는 [Windows Phone Silverlight 앱에 Mobile Engagement를 통합하는 방법](mobile-engagement-windows-phone-integrate-engagement.md) 문서를 보완하는 추가 문서로,</span><span class="sxs-lookup"><span data-stu-id="687d4-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="687d4-105">Engagement API를 사용하여 응용 프로그램 통계를 보고하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="687d4-106">Engagement에서 응용 프로그램 세션, 활동, 작동 중단, 기술 정보만 보고하도록 하려는 경우 가장 간단한 방법은 모든 `PhoneApplicationPage` 서브클래스가 `EngagementPage` 클래스에서 상속하도록 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="687d4-107">응용 프로그램 관련 이벤트, 오류, 작업을 보고하는 등 추가 작업을 수행하려는 경우 또는 `EngagementPage` 클래스에서 구현되는 것과는 다른 방식으로 응용 프로그램 활동을 보고해야 하는 경우에는 Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="687d4-108">Engagement API는 `EngagementAgent` 클래스를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="687d4-109">해당 메서드는 `EngagementAgent.Instance`을(를) 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="687d4-110">에이전트 모듈이 초기화되지 않은 경우에도 각 API 호출은 연기되며 에이전트를 사용할 수 있게 되면 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="687d4-111">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="687d4-111">Engagement concepts</span></span>
<span data-ttu-id="687d4-112">다음 요소는 Windows Phone 플랫폼과 관련된 Mobile Engagement 개념을 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="687d4-113">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="687d4-113">`Session` and `Activity`</span></span>
<span data-ttu-id="687d4-114">*작업*은 일반적으로 단일 응용 프로그램 페이지와 연결됩니다. 즉 *작업*은 페이지를 표시하면 시작되며 페이지를 닫으면 중지됩니다. `EngagementPage` 클래스를 사용하여 Engagement SDK를 통합하는 경우 이러한 방식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="687d4-115">하지만 Engagement API를 사용하여 *활동* 을 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="687d4-116">이렇게 하면 지정된 페이지를 여러 하위 부분으로 분할하여 해당 페이지의 사용에 대해 더 많은 세부 정보(예: 이 페이지 내에서 대화 상자를 사용하는 빈도와 기간)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="687d4-117">활동 보고</span><span class="sxs-lookup"><span data-stu-id="687d4-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="687d4-118">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="687d4-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-119">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-120">사용자 활동이 변경될 때마다 `StartActivity()` 을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="687d4-121">이 함수를 처음 호출하면 새 사용자 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="687d4-122">응용 프로그램을 닫을 때 SDK는 EndActivity 메서드를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="687d4-123">따라서 사용자 활동이 변경될 때마다 StartActivity 메서드를 호출하는 것이 좋으며 EndActivity 메서드는 호출하지 않는 것이 좋습니다. EndActivity 메서드를 호출하면 현재 세션이 강제로 종료되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="687d4-124">예</span><span class="sxs-lookup"><span data-stu-id="687d4-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="687d4-125">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="687d4-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-126">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="687d4-127">사용자가 마지막 활동을 완료하면 `EndActivity()`을(를) 한 번 이상 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="687d4-128">이 작업은 Engagement SDK에 사용자가 현재 유휴 상태이며, 세션 제한 시간이 만료되면 사용자 세션을 종료해야 한다는 것을 알립니다. 세션 제한 시간이 만료되기 전에 `StartActivity()`을(를) 호출하는 경우 세션이 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-129">예제</span><span class="sxs-lookup"><span data-stu-id="687d4-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="687d4-130">작업 보고</span><span class="sxs-lookup"><span data-stu-id="687d4-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="687d4-131">작업 시작</span><span class="sxs-lookup"><span data-stu-id="687d4-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-132">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-133">작업을 사용하여 일정 기간 동안의 특정 태스크를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-134">예</span><span class="sxs-lookup"><span data-stu-id="687d4-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="687d4-135">작업 종료</span><span class="sxs-lookup"><span data-stu-id="687d4-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-136">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="687d4-137">작업에 의해 추적되는 태스크가 종료되는 즉시 해당 작업에 대해 작업 이름을 제공하여 EndJob 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-138">예</span><span class="sxs-lookup"><span data-stu-id="687d4-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="687d4-139">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="687d4-139">Reporting Events</span></span>
<span data-ttu-id="687d4-140">이벤트에는 다음의 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-140">There is three types of events :</span></span>

* <span data-ttu-id="687d4-141">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="687d4-141">Standalone events</span></span>
* <span data-ttu-id="687d4-142">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="687d4-142">Session events</span></span>
* <span data-ttu-id="687d4-143">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="687d4-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="687d4-144">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="687d4-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-145">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-146">독립 실행형 이벤트는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-147">예</span><span class="sxs-lookup"><span data-stu-id="687d4-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="687d4-148">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="687d4-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-149">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-150">세션 이벤트는 일반적으로 사용자가 세션 중에 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-151">예</span><span class="sxs-lookup"><span data-stu-id="687d4-151">Example</span></span>
<span data-ttu-id="687d4-152">**데이터 제외:**</span><span class="sxs-lookup"><span data-stu-id="687d4-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="687d4-153">**데이터 포함:**</span><span class="sxs-lookup"><span data-stu-id="687d4-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="687d4-154">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="687d4-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-155">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-156">작업 이벤트는 일반적으로 사용자가 작업 중에 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-157">예</span><span class="sxs-lookup"><span data-stu-id="687d4-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="687d4-158">오류 보고</span><span class="sxs-lookup"><span data-stu-id="687d4-158">Reporting Errors</span></span>
<span data-ttu-id="687d4-159">오류에는 다음의 세 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-159">There is three types of errors :</span></span>

* <span data-ttu-id="687d4-160">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="687d4-160">Standalone errors</span></span>
* <span data-ttu-id="687d4-161">세션 오류</span><span class="sxs-lookup"><span data-stu-id="687d4-161">Session errors</span></span>
* <span data-ttu-id="687d4-162">작업 오류</span><span class="sxs-lookup"><span data-stu-id="687d4-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="687d4-163">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="687d4-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-164">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-165">세션 오류와 달리 독립 실행형 오류는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-166">예</span><span class="sxs-lookup"><span data-stu-id="687d4-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="687d4-167">세션 오류</span><span class="sxs-lookup"><span data-stu-id="687d4-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-168">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-169">세션 오류는 일반적으로 세션 중에 사용자에게 영향을 주는 오류를 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-170">예</span><span class="sxs-lookup"><span data-stu-id="687d4-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="687d4-171">작업 오류</span><span class="sxs-lookup"><span data-stu-id="687d4-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-172">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="687d4-173">오류는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-174">예</span><span class="sxs-lookup"><span data-stu-id="687d4-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="687d4-175">작동 중단 보고</span><span class="sxs-lookup"><span data-stu-id="687d4-175">Reporting Crashes</span></span>
<span data-ttu-id="687d4-176">에이전트는 작동 중단을 처리하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="687d4-177">예외 보내기</span><span class="sxs-lookup"><span data-stu-id="687d4-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-178">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="687d4-179">예</span><span class="sxs-lookup"><span data-stu-id="687d4-179">Example</span></span>
<span data-ttu-id="687d4-180">언제든지 다음을 호출하여 예외를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="687d4-181">또한 선택적 매개 변수를 사용하여 작동 중단을 보냄과 동시에 Engagement 세션을 종료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="687d4-182">이렇게 하려면 다음을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="687d4-183">이 경우 작동 중단을 보낸 직후에 세션과 작업이 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="687d4-184">처리되지 않은 예외 보내기</span><span class="sxs-lookup"><span data-stu-id="687d4-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="687d4-185">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="687d4-186">Engagement에서는 처리되지 않은 예외를 보내는 방법도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="687d4-187">이 방법은 Silverlight UnhandledException 이벤트 처리기 내에서 사용하는 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="687d4-188">이 방법을 사용하는 경우 **항상** Engagement 세션과 작업이 호출된 후에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="687d4-189">예제</span><span class="sxs-lookup"><span data-stu-id="687d4-189">Example</span></span>
<span data-ttu-id="687d4-190">위에서 설명한 방법을 사용하여 UnhandledException 처리기를 직접 구현할 수 있습니다. 특히 Engagement의 자동 작동 중단 보고 기능을 사용하지 않도록 설정한 경우 이러한 처리기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="687d4-191">예를 들어 `App.xaml.cs` 파일의 `Application_UnhandledException` 메서드에서 해당 처리기를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="687d4-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="687d4-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="687d4-193">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="687d4-194">사용자가 정방향 탐색을 통해 응용 프로그램에서 벗어나면 Deactivated 이벤트가 발생하며, 운영 체제는 응용 프로그램을 유휴 상태로 설정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="687d4-195">그리고 나면 응용 프로그램에 삭제 표식이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="687d4-196">이 프로세스에서 응용 프로그램은 종료되지만 응용 프로그램 상태에 대한 일부 데이터와 응용 프로그램 내의 개별 페이지는 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="687d4-197">응용 프로그램에 삭제 표식이 설정된 경우 Engagement 에이전트를 다시 설정하려면 App.xaml.cs 파일에서 `Application_Activated` 메서드에 `EngagementAgent.Instance.OnActivated(e)`을(를) 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="687d4-198">예</span><span class="sxs-lookup"><span data-stu-id="687d4-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="687d4-199">장치 ID</span><span class="sxs-lookup"><span data-stu-id="687d4-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="687d4-200">이 메서드를 호출하여 Engagement 장치 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="687d4-201">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="687d4-201">Extras parameters</span></span>
<span data-ttu-id="687d4-202">이벤트, 오류, 활동 또는 작업에 임의 데이터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="687d4-203">사전을 사용하여 이러한 데이터를 구조화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="687d4-204">모든 형식의 키와 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="687d4-205">extras 데이터는 serialize되므로 원하는 형식을 extras에 삽입하려면 해당 형식용 데이터 계약을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="687d4-206">예</span><span class="sxs-lookup"><span data-stu-id="687d4-206">Example</span></span>
<span data-ttu-id="687d4-207">아래 예제에서는 "Person"이라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="687d4-208">그런 다음 `Person` 인스턴스를 extras에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="687d4-209">다른 형식의 개체를 추가할 때는 사용자가 읽을 수 있는 문자열을 반환하도록 해당 ToString() 메서드를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="687d4-210">제한</span><span class="sxs-lookup"><span data-stu-id="687d4-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="687d4-211">구성</span><span class="sxs-lookup"><span data-stu-id="687d4-211">Keys</span></span>
<span data-ttu-id="687d4-212">개체의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="687d4-213">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="687d4-214">크기</span><span class="sxs-lookup"><span data-stu-id="687d4-214">Size</span></span>
<span data-ttu-id="687d4-215">extras는 호출당 **1024** 자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="687d4-216">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="687d4-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="687d4-217">참조</span><span class="sxs-lookup"><span data-stu-id="687d4-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="687d4-218">SendAppInfo() 함수를 사용하면 추적 정보 또는 기타 응용 프로그램 관련 정보를 수동으로 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="687d4-219">이러한 정보는 증분 방식으로 보낼 수 있습니다. 그러면 특정 장치에 대해 지정한 키의 최신 값만 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="687d4-220">이벤트 추가 항목과 마찬가지로 Dictionary\<object, object\>를 사용하여 정보를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="687d4-221">예제</span><span class="sxs-lookup"><span data-stu-id="687d4-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="687d4-222">제한</span><span class="sxs-lookup"><span data-stu-id="687d4-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="687d4-223">구성</span><span class="sxs-lookup"><span data-stu-id="687d4-223">Keys</span></span>
<span data-ttu-id="687d4-224">개체의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="687d4-225">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="687d4-226">크기</span><span class="sxs-lookup"><span data-stu-id="687d4-226">Size</span></span>
<span data-ttu-id="687d4-227">응용 프로그램 정보는 호출당 **1024** 자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="687d4-228">위의 예제에서 서버로 전송된 JSON의 길이는 44자입니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="687d4-229">로깅</span><span class="sxs-lookup"><span data-stu-id="687d4-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="687d4-230">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="687d4-230">Enable Logging</span></span>
<span data-ttu-id="687d4-231">SDK는 IDE 콘솔에서 테스트 로그를 생성하도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="687d4-232">이러한 로그는 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-232">These logs are not activated by default.</span></span> <span data-ttu-id="687d4-233">이를 사용자 지정하려면 속성 `EngagementAgent.Instance.TestLogEnabled`를 `EngagementTestLogLevel` 열거형에서 사용 가능한 값 중 하나로 업데이트합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="687d4-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
