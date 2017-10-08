---
title: "Mobile Engagement 웹 SDK Api aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement에 대 한 최신 업데이트 및 hello 웹 SDK에 대 한 절차 hello"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="a2a24-103">웹 응용 프로그램에 Azure Mobile Engagement API hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a2a24-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="a2a24-104">이 문서는 너무 방법을 알려 주는 추가 toohello 문서[Mobile Engagement 웹 응용 프로그램에서 통합](mobile-engagement-web-integrate-engagement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="a2a24-105">응용 프로그램 통계 toouse Azure Mobile Engagement API tooreport hello 하는 방법에 대 한 자세한 정보 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="a2a24-106">hello Mobile Engagement API에서 제공 hello `engagement.agent` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="a2a24-107">Azure Mobile Engagement 웹 SDK 별칭은 기본 hello `engagement`합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="a2a24-108">Hello SDK 구성에서이 별칭을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="a2a24-109">Mobile Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="a2a24-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="a2a24-110">hello 다음과 같은 부분이 구체화 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) hello 웹 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a2a24-111">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="a2a24-111">`Session` and `Activity`</span></span>
<span data-ttu-id="a2a24-112">Hello 사용자 유지 두 작업 사이 몇 개의 초 동안 유휴 상태, hello 사용자의 일련의 활동은으로 분할 두 개의 고유한 세션.</span><span class="sxs-lookup"><span data-stu-id="a2a24-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="a2a24-113">이러한 몇 초 hello 세션 제한 시간을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="a2a24-114">웹 응용 프로그램 사용자 활동의 hello 끝을 단독으로 선언 하지 않습니다 (호출 hello 여 `engagement.agent.endActivity` 함수), hello Mobile Engagement 서버 hello를 자동으로 만료 hello 응용 프로그램 페이지를 닫은 후 3 분 이내에 사용자 세션.</span><span class="sxs-lookup"><span data-stu-id="a2a24-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="a2a24-115">이 hello 서버에 대 한 세션 제한 시간을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="a2a24-116">기본적으로 catch되지 않은 JavaScript 예외에 대한 자동화된 보고서는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="a2a24-117">그러나 충돌을 보고할 수 있습니다 hello를 사용 하 여 수동으로 `sendCrash` 함수 (충돌 보고에 hello 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="a2a24-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a2a24-118">활동 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-118">Reporting activities</span></span>
<span data-ttu-id="a2a24-119">사용자 작업에 대 한 보고에 사용자가 새 작업을 시작 하 고 hello 사용자 hello 현재 활동 종료 될 때 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a2a24-120">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="a2a24-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="a2a24-121">Toocall 필요한 `startActivity()` 각 시간 사용자 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="a2a24-122">첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="a2a24-123">사용자는 hello 현재 작업 종료</span><span class="sxs-lookup"><span data-stu-id="a2a24-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="a2a24-124">Toocall 필요한 `endActivity()` hello 사용자의 마지막 작업을 완료 하는 때 한 번 이상.</span><span class="sxs-lookup"><span data-stu-id="a2a24-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="a2a24-125">그러면 hello 사용자가 현재 유휴 및 hello 세션 제한 시간이 만료 되 면 닫힐 toobe hello 사용자 세션에 필요 함을 hello Mobile Engagement 웹 SDK 알리게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="a2a24-126">호출 하는 경우 `startActivity()` hello 세션이 재개 되 단순히 hello 세션 제한 시간 만료 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="a2a24-127">Hello 탐색기 창이 닫힌 경우에 대 한 신뢰할 수 있는 호출이 이기 때문에 웹 환경 내의 사용자 활동의 어렵거나 toocatch hello 끝 방식은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="a2a24-128">서버에서 자동으로 만료 Mobile Engagement hello 이유는 hello 사용자 세션 hello 응용 프로그램 페이지를 닫은 후 3 분 이내입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="a2a24-129">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-129">Reporting events</span></span>
<span data-ttu-id="a2a24-130">이벤트에 대한 보고에서는 세션 이벤트와 독립 실행형 이벤트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="a2a24-131">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="a2a24-131">Session events</span></span>
<span data-ttu-id="a2a24-132">세션 이벤트에는 일반적으로 사용 되는 tooreport hello 동작 hello 사용자 세션 동안 사용자가 수행한는입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="a2a24-133">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="a2a24-134">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="a2a24-135">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="a2a24-135">Standalone events</span></span>
<span data-ttu-id="a2a24-136">세션 이벤트와 달리 독립 실행형 이벤트 세션의 hello 컨텍스트 외부 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="a2a24-137">이를 위해서는 ``engagement.agent.sendSessionEvent`` 대신 ``engagement.agent.sendEvent``를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="a2a24-138">오류 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-138">Reporting errors</span></span>
<span data-ttu-id="a2a24-139">오류에 대한 보고에서는 세션 오류와 독립 실행형 오류를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="a2a24-140">세션 오류</span><span class="sxs-lookup"><span data-stu-id="a2a24-140">Session errors</span></span>
<span data-ttu-id="a2a24-141">일반적으로 세션 오류는 영향을 주는 hello 사용자에 hello 사용자 세션 동안 사용 되는 tooreport hello 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="a2a24-142">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="a2a24-143">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="a2a24-144">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="a2a24-144">Standalone errors</span></span>
<span data-ttu-id="a2a24-145">세션 오류와 달리 세션의 hello 컨텍스트 외부 독립 실행형 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="a2a24-146">이를 위해서는 `engagement.agent.sendSessionError` 대신 `engagement.agent.sendError`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="a2a24-147">작업 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-147">Reporting jobs</span></span>
<span data-ttu-id="a2a24-148">작업에 대한 보고에서는 작업 중에 발생한 오류 및 이벤트 보고와 작동 중단 보고를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="a2a24-149">**예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-149">**Example:**</span></span>

<span data-ttu-id="a2a24-150">Toomonitor AJAX 요청을 사용 하도록 하려는 경우에 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="a2a24-151">작업 중 오류 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-151">Reporting errors during a job</span></span>
<span data-ttu-id="a2a24-152">오류는 현재 사용자 세션 toohello 대신 작업을 실행 하는 관련된 tooa 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="a2a24-153">**예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-153">**Example:**</span></span>

<span data-ttu-id="a2a24-154">원하는 tooreport AJAX 요청 하면 오류가 발생 하는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="a2a24-155">작업 중 이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-155">Reporting events during a job</span></span>
<span data-ttu-id="a2a24-156">이벤트에는 작업을 실행 하는 대신 현재 사용자 세션 toohello 고마워요 toohello 관련된 tooa 수 `engagement.agent.sendJobEvent` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="a2a24-157">이 함수는 `engagement.agent.sendJobError`와 똑같이 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="a2a24-158">작동 중단 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-158">Reporting crashes</span></span>
<span data-ttu-id="a2a24-159">사용 하 여 hello `sendCrash` 함수 tooreport 수동으로 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="a2a24-160">hello `crashid` 인수는 충돌의 hello 형식을 식별 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="a2a24-161">hello `crash` 인수를 문자열로 hello 충돌의 hello 스택 추적을 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="a2a24-162">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a2a24-162">Extra parameters</span></span>
<span data-ttu-id="a2a24-163">임의의 데이터 tooan 이벤트, 오류, 활동 또는 작업을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="a2a24-164">hello 데이터는 JSON 개체 (하지만 하지는 배열 또는 기본 형식) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="a2a24-165">**예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="a2a24-166">제한</span><span class="sxs-lookup"><span data-stu-id="a2a24-166">Limits</span></span>
<span data-ttu-id="a2a24-167">키, 값 형식 및 크기에 대 한 정규식의 hello 영역에서 tooextra 매개 변수를 적용 하는 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="a2a24-168">구성</span><span class="sxs-lookup"><span data-stu-id="a2a24-168">Keys</span></span>
<span data-ttu-id="a2a24-169">각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="a2a24-170">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="a2a24-171">값</span><span class="sxs-lookup"><span data-stu-id="a2a24-171">Values</span></span>
<span data-ttu-id="a2a24-172">값은 제한 toostring, 숫자 및 부울 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="a2a24-173">크기</span><span class="sxs-lookup"><span data-stu-id="a2a24-173">Size</span></span>
<span data-ttu-id="a2a24-174">추가 기능 제한 too1, 024 자 (Mobile Engagement 웹 SDK hello json에서 인코딩합니다) 후 호출당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="a2a24-175">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="a2a24-175">Reporting application information</span></span>
<span data-ttu-id="a2a24-176">Hello를 사용 하 여 수동으로 추적 정보 (또는 다른 응용 프로그램 관련 정보)를 보고할 수 `sendAppInfo()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="a2a24-177">이 정보는 증분 방식으로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="a2a24-178">특정 장치에 대 한 특정 키에 대 한 최신 값 hello만 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="a2a24-179">이벤트, 기타와 같은 모든 JSON 개체 tooabstract 응용 프로그램 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="a2a24-180">배열 또는 하위 개체는 플랫 문자열(JSON 직렬화 사용)로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="a2a24-181">**예제:**</span><span class="sxs-lookup"><span data-stu-id="a2a24-181">**Example:**</span></span>

<span data-ttu-id="a2a24-182">보내는 hello 사용자의 성 및 생년월일에 대 한 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="a2a24-183">제한</span><span class="sxs-lookup"><span data-stu-id="a2a24-183">Limits</span></span>
<span data-ttu-id="a2a24-184">Tooapplication 정보를 적용 하는 제한은 키 및 크기에 대 한 정규식의 hello 영역 에서입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="a2a24-185">구성</span><span class="sxs-lookup"><span data-stu-id="a2a24-185">Keys</span></span>
<span data-ttu-id="a2a24-186">각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="a2a24-187">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a2a24-188">크기</span><span class="sxs-lookup"><span data-stu-id="a2a24-188">Size</span></span>
<span data-ttu-id="a2a24-189">응용 프로그램 정보는 제한 된 too1, (Mobile Engagement 웹 SDK hello json에서 인코딩합니다) 후 호출당 024 자입니다.</span><span class="sxs-lookup"><span data-stu-id="a2a24-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="a2a24-190">앞 예제는 hello, hello JSON 전송 toohello 서버는 44 자:</span><span class="sxs-lookup"><span data-stu-id="a2a24-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
