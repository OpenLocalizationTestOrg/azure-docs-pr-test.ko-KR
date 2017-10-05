---
title: "Azure Mobile Engagement 웹 SDK API | Microsoft Docs"
description: "Azure Mobile Engagement용 웹 SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="57287-103">웹 응용 프로그램에서 Azure Mobile Engagement API 사용</span><span class="sxs-lookup"><span data-stu-id="57287-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="57287-104">이 문서는 [웹 응용 프로그램에서 Mobile Engagement를 통합](mobile-engagement-web-integrate-engagement.md)하는 방법을 안내하는 문서를 보완하는 추가 문서로,</span><span class="sxs-lookup"><span data-stu-id="57287-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="57287-105">Azure Mobile Engagement API를 사용하여 응용 프로그램 통계를 보고하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="57287-106">Mobile Engagement API는 `engagement.agent` 개체를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="57287-107">기본 Azure Mobile Engagement 웹 SDK 별칭은 `engagement`입니다.</span><span class="sxs-lookup"><span data-stu-id="57287-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="57287-108">SDK 구성에서 이 별칭을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="57287-109">Mobile Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="57287-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="57287-110">다음 요소는 웹 플랫폼과 관련된 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) 을 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="57287-111">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="57287-111">`Session` and `Activity`</span></span>
<span data-ttu-id="57287-112">두 활동 간에 몇 초 넘게 유휴 상태로 있는 경우 활동의 사용자 시퀀스가 두 개의 세션으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="57287-113">이러한 몇 초를 세션 제한 시간이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="57287-114">웹 응용 프로그램이 직접 사용자 활동 종료를 선언하지 않으면( `engagement.agent.endActivity` 함수 호출), Mobile Engagement 서버에서 응용 프로그램 페이지가 닫히고 3분 이내에 사용자 세션을 자동 만료시킵니다.</span><span class="sxs-lookup"><span data-stu-id="57287-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="57287-115">이를 서버 세션 시간 제한이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="57287-116">기본적으로 catch되지 않은 JavaScript 예외에 대한 자동화된 보고서는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="57287-117">그러나 `sendCrash` 함수를 사용하면 수동으로 작동 중단을 보고할 수 있습니다(작동 중단 보고에 대한 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="57287-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="57287-118">활동 보고</span><span class="sxs-lookup"><span data-stu-id="57287-118">Reporting activities</span></span>
<span data-ttu-id="57287-119">사용자 활동에 대한 보고에는 사용자가 새 활동을 시작한 시간 및 사용자가 현재 활동을 종료한 시간이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="57287-120">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="57287-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="57287-121">사용자 활동이 변경될 때마다 `startActivity()` 을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="57287-122">이 함수를 처음 호출하면 새 사용자 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="57287-123">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="57287-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="57287-124">사용자가 마지막 활동을 완료하면 `endActivity()` 을(를) 한 번 이상 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="57287-125">이 작업은 Mobile Engagement 웹 SDK에 사용자가 현재 유휴 상태이며, 세션 제한 시간이 만료되면 사용자 세션을 종료해야 한다는 것을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="57287-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="57287-126">세션 제한 시간이 만료되기 전에 `startActivity()` 를 호출하는 경우 세션이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="57287-127">탐색기 창이 닫혔을 때는 신뢰할 수 있는 호출 없으므로 웹 환경 내에서는 사용자가 활동을 종료한 것을 알아내기 어렵거나 불가능한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="57287-128">그래서 Mobile Engagement 서버에서 응용 프로그램 페이지가 닫히고 3분 이내에 사용자 세션을 자동 만료시키는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57287-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="57287-129">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="57287-129">Reporting events</span></span>
<span data-ttu-id="57287-130">이벤트에 대한 보고에서는 세션 이벤트와 독립 실행형 이벤트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="57287-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="57287-131">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="57287-131">Session events</span></span>
<span data-ttu-id="57287-132">세션 이벤트는 일반적으로 사용자가 세션 중에 사용자가 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="57287-133">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="57287-134">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="57287-135">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="57287-135">Standalone events</span></span>
<span data-ttu-id="57287-136">세션 이벤트와 달리 독립 실행형 이벤트는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="57287-137">이를 위해서는 ``engagement.agent.sendSessionEvent`` 대신 ``engagement.agent.sendEvent``를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="57287-138">오류 보고</span><span class="sxs-lookup"><span data-stu-id="57287-138">Reporting errors</span></span>
<span data-ttu-id="57287-139">오류에 대한 보고에서는 세션 오류와 독립 실행형 오류를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="57287-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="57287-140">세션 오류</span><span class="sxs-lookup"><span data-stu-id="57287-140">Session errors</span></span>
<span data-ttu-id="57287-141">세션 오류는 일반적으로 사용자 세션 중에 사용자에게 영향을 주는 오류를 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="57287-142">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="57287-143">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="57287-144">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="57287-144">Standalone errors</span></span>
<span data-ttu-id="57287-145">세션 오류와 달리 독립 실행형 오류는 세션의 컨텍스트 외부에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="57287-146">이를 위해서는 `engagement.agent.sendSessionError` 대신 `engagement.agent.sendError`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="57287-147">작업 보고</span><span class="sxs-lookup"><span data-stu-id="57287-147">Reporting jobs</span></span>
<span data-ttu-id="57287-148">작업에 대한 보고에서는 작업 중에 발생한 오류 및 이벤트 보고와 작동 중단 보고를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="57287-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="57287-149">**예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-149">**Example:**</span></span>

<span data-ttu-id="57287-150">AJAX 요청을 모니터링하려는 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="57287-151">작업 중 오류 보고</span><span class="sxs-lookup"><span data-stu-id="57287-151">Reporting errors during a job</span></span>
<span data-ttu-id="57287-152">오류는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="57287-153">**예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-153">**Example:**</span></span>

<span data-ttu-id="57287-154">AJAX 요청이 실패하면 오류를 보고하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="57287-155">작업 중 이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="57287-155">Reporting events during a job</span></span>
<span data-ttu-id="57287-156">`engagement.agent.sendJobEvent` 함수를 사용하면 이벤트를 현재 사용자 세션이 아니라 실행 중인 작업과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="57287-157">이 함수는 `engagement.agent.sendJobError`와 똑같이 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="57287-158">작동 중단 보고</span><span class="sxs-lookup"><span data-stu-id="57287-158">Reporting crashes</span></span>
<span data-ttu-id="57287-159">`sendCrash` 함수는 수동으로 작동 중단을 보고할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="57287-160">`crashid` 인수는 작동 중단 유형을 식별하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="57287-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="57287-161">`crash` 인수는 일반적으로 문자열로 된 작동 중단의 스택 추적입니다.</span><span class="sxs-lookup"><span data-stu-id="57287-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="57287-162">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="57287-162">Extra parameters</span></span>
<span data-ttu-id="57287-163">이벤트, 오류, 활동 또는 작업에 임의 데이터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="57287-164">이 데이터는 배열 또는 기본 형식을 제외한 어떤 JSON 개체도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="57287-165">**예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="57287-166">제한</span><span class="sxs-lookup"><span data-stu-id="57287-166">Limits</span></span>
<span data-ttu-id="57287-167">extras 매개 변수에 적용할 제한은 키, 값 형식 및 크기에 대한 정규식의 영역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="57287-168">구성</span><span class="sxs-lookup"><span data-stu-id="57287-168">Keys</span></span>
<span data-ttu-id="57287-169">개체의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="57287-170">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="57287-171">값</span><span class="sxs-lookup"><span data-stu-id="57287-171">Values</span></span>
<span data-ttu-id="57287-172">값은 문자열, 숫자, 부울 형식으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="57287-173">크기</span><span class="sxs-lookup"><span data-stu-id="57287-173">Size</span></span>
<span data-ttu-id="57287-174">extras는 호출당 1,024자(Mobile Engagement 웹 SDK가 JSON에서 인코딩된 후)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="57287-175">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="57287-175">Reporting application information</span></span>
<span data-ttu-id="57287-176">`sendAppInfo()` 함수를 사용하면 추적 정보 또는 기타 응용 프로그램 관련 정보를 수동으로 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="57287-177">이 정보는 증분 방식으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="57287-178">특정 장치에는 특정 키에 대한 최신 값만 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="57287-179">이벤트 extras처럼 JSON 개체를 사용하여 응용 프로그램 정보를 추상화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="57287-180">배열 또는 하위 개체는 플랫 문자열(JSON 직렬화 사용)로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="57287-181">**예제:**</span><span class="sxs-lookup"><span data-stu-id="57287-181">**Example:**</span></span>

<span data-ttu-id="57287-182">사용자 성별 및 생년월일을 보내는 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="57287-183">제한</span><span class="sxs-lookup"><span data-stu-id="57287-183">Limits</span></span>
<span data-ttu-id="57287-184">응용 프로그램에 적용할 제한은 키 및 크기에 대한 정규식의 영역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57287-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="57287-185">구성</span><span class="sxs-lookup"><span data-stu-id="57287-185">Keys</span></span>
<span data-ttu-id="57287-186">개체의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="57287-187">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57287-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="57287-188">크기</span><span class="sxs-lookup"><span data-stu-id="57287-188">Size</span></span>
<span data-ttu-id="57287-189">응용 프로그램 정보는 호출당 1,024자(Mobile Engagement 웹 SDK가 JSON에서 인코딩된 후)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="57287-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="57287-190">이전 예제에서 서버로 전송된 JSON의 길이는 44자입니다.</span><span class="sxs-lookup"><span data-stu-id="57287-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
