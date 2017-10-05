---
title: "Mobile Engagement 개념 | Microsoft Docs"
description: "Azure Mobile Engagement 개념"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 8450651528007b4527366b89a6ad7615169f93c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-concepts"></a><span data-ttu-id="90d77-103">Azure Mobile Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="90d77-103">Azure Mobile Engagement concepts</span></span>
<span data-ttu-id="90d77-104">Mobile Engagement는 지원되는 모든 플랫폼에 공통되는 몇 가지 개념을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-104">Mobile Engagement defines a few concepts common to all supported platforms.</span></span> <span data-ttu-id="90d77-105">이 문서에서는 이러한 개념을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-105">This article briefly describes those concepts.</span></span>

<span data-ttu-id="90d77-106">Mobile Engagement를 처음 사용하는 경우 이 문서부터 참조하면 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-106">This article is a good start if you are new to Mobile Engagement.</span></span> <span data-ttu-id="90d77-107">또한 사용 중인 플랫폼과 관련된 문서를 읽어보세요. 자세한 정보 및 예제뿐만 아니라 가능한 제한 사항을 통해 이 문서에 설명된 개념을 구체적으로 설명해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-107">Also make sure to read the documentation specific to the platform you are using, as it will refine the concepts described in this article with more details and examples as well as possible limitations.</span></span>

## <a name="devices-and-users"></a><span data-ttu-id="90d77-108">장치 및 사용자</span><span class="sxs-lookup"><span data-stu-id="90d77-108">Devices and users</span></span>
<span data-ttu-id="90d77-109">Mobile Engagement는 각 장치에 대한 고유 식별자를 생성하여 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-109">Mobile Engagement identifies users by generating a unique identifier for each device.</span></span> <span data-ttu-id="90d77-110">이 식별자를 장치 식별자(또는 `deviceid`)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-110">This identifier is called the device identifier (or `deviceid`).</span></span> <span data-ttu-id="90d77-111">식별자는 동일한 장치에서 실행하는 모든 응용 프로그램이 동일한 장치 식별자를 공유하는 방식으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-111">It is generated in such a way that all applications running of the same device share the same device identifier.</span></span>

<span data-ttu-id="90d77-112">암시적으로 Mobile Engagement는 한 장치가 정확히 한 명의 사용자에게 속하는 것으로 간주하므로, 사용자와 장치는 동등한 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-112">Implicitly, it means that Mobile Engagement considers one device to belong to exactly one user, and thus, users and devices are equivalent concepts.</span></span>

## <a name="sessions-and-activities"></a><span data-ttu-id="90d77-113">세션 및 작업</span><span class="sxs-lookup"><span data-stu-id="90d77-113">Sessions and activities</span></span>
<span data-ttu-id="90d77-114">세션은 사용자가 응용 프로그램을 한 번 사용하는 것으로, 사용을 시작한 시간부터 중지할 때까지의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-114">A session is one use of the application performed by a user, from the time the user starts using it, until the user stops.</span></span>

<span data-ttu-id="90d77-115">작업은 사용자가 수행하는 응용 프로그램의 지정된 하위 부분에 대한 한 번의 사용입니다(일반적으로 한 화면이지만 응용 프로그램에 적합한 어떤 항목이든 될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="90d77-115">An activity is one use of a given sub-part of the application performed by one user (it is usually a screen, but it can be anything suitable to the application).</span></span>

<span data-ttu-id="90d77-116">사용자는 한번에 하나의 동작만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-116">A user can only perform one activity at a time.</span></span>

<span data-ttu-id="90d77-117">작업은 이름(64자로 제한됨)으로 식별되고 선택적으로 추가 데이터(1024바이트로 제한됨)를 일부 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-117">An activity is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

<span data-ttu-id="90d77-118">세션은 사용자가 수행한 작업의 시퀀스에서 자동으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-118">Sessions are automatically computed from the sequence of activities performed by users.</span></span> <span data-ttu-id="90d77-119">사용자가 첫 번째 작업을 시작할 때 세션이 시작되고 마지막 작업을 끝내면 세션이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-119">A session starts when the user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="90d77-120">즉, 세션을 명시적으로 시작하거나 중지할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-120">This means that a session does not need to be explicitly started or stopped.</span></span> <span data-ttu-id="90d77-121">대신, 작업이 명시적으로 시작되거나 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-121">Instead, activities are explicitly started or stopped.</span></span> <span data-ttu-id="90d77-122">작업이 보고되지 않으면 세션이 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-122">If no activity is reported, no session is reported.</span></span>

## <a name="events"></a><span data-ttu-id="90d77-123">이벤트</span><span class="sxs-lookup"><span data-stu-id="90d77-123">Events</span></span>
<span data-ttu-id="90d77-124">이벤트는 인스턴트 동작(예: 사용자가 단추 누름 또는 문서 읽음)을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-124">Events are used to report instant actions (like button pressed or articles read by users).</span></span>

<span data-ttu-id="90d77-125">이벤트는 현재 세션 또는 실행 중인 작업과 관련될 수 있거나 독립 실행형이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-125">An event can be related to the current session, to a running job, or it can be a standalone event.</span></span>

<span data-ttu-id="90d77-126">이벤트는 이름(64자로 제한됨)으로 식별되고 선택적으로 추가 데이터(1024바이트로 제한됨)를 일부 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-126">An event is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="error"></a><span data-ttu-id="90d77-127">오류</span><span class="sxs-lookup"><span data-stu-id="90d77-127">Error</span></span>
<span data-ttu-id="90d77-128">오류는 응용 프로그램에서 올바르게 감지하는 문제(예: 잘못된 사용자 작업 또는 API 호출 실패)를 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-128">Errors are used to report issues correctly detected by the application (like incorrect user actions, or API call failures).</span></span>

<span data-ttu-id="90d77-129">오류는 현재 세션 또는 실행 중인 작업과 관련될 수 있거나 독립 실행형이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-129">An error can be related to the current session, to a running job, or it can be a standalone error.</span></span>

<span data-ttu-id="90d77-130">오류는 이름(64자로 제한됨)으로 식별되고 선택적으로 추가 데이터(1024바이트로 제한됨)를 일부 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-130">An error is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="job"></a><span data-ttu-id="90d77-131">작업</span><span class="sxs-lookup"><span data-stu-id="90d77-131">Job</span></span>
<span data-ttu-id="90d77-132">작업은 기간(예: API 호출 기간, 광고의 표시 시간, 백그라운드 작업의 기간 또는 사용자 작업의 기간)이 있는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-132">Jobs are used to report actions having a duration (like duration of API calls, display time of ads, duration of background tasks or duration of user actions).</span></span>

<span data-ttu-id="90d77-133">사용자 개입 없이 작업을 백그라운드에서 수행할 수 있으므로 작업은 특정 세션과 관련되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-133">A job is not related to a session, because a task can be performed in the background, without any user interaction.</span></span>

<span data-ttu-id="90d77-134">작업은 이름(64자로 제한됨)으로 식별되고 선택적으로 추가 데이터(1024바이트로 제한됨)를 일부 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-134">A job is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="crash"></a><span data-ttu-id="90d77-135">크래시</span><span class="sxs-lookup"><span data-stu-id="90d77-135">Crash</span></span>
<span data-ttu-id="90d77-136">크래시는 Mobile Engagement SDK에서 응용 프로그램에 의해 검색되지 않는 문제가 크래시로 지정되는 응용 프로그램 오류를 보고하기 위해 자동으로 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-136">Crashes are issued automatically by the Mobile Engagement SDK to report application failures where issues not detected by the application make it crash.</span></span>

## <a name="application-information"></a><span data-ttu-id="90d77-137">응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="90d77-137">Application information</span></span>
<span data-ttu-id="90d77-138">응용 프로그램 정보(또는 앱 정보)는 일부 데이터를 응용 프로그램의 사용자와 연결하기 위해 사용자를 태그하는 데 사용됩니다. 즉, 앱 정보가 Azure Mobile Engagement 플랫폼의 서버 측에 저장되는 점을 제외하면 웹 쿠키와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-138">Application information (or app info) is used to tag users, that is, to associate some data to the users of an application (this is similar to web cookies, except that app info is stored on the server side on the Azure Mobile Engagement platform).</span></span>

<span data-ttu-id="90d77-139">Mobile Engagement SDK의 API 또는 Mobile Engagement 플랫폼의 장치 API를 사용하여 앱 정보를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-139">App info can be registered by using the Mobile Engagement SDK API or by using the Mobile Engagement platform Device API.</span></span>

<span data-ttu-id="90d77-140">앱 정보는 장치에 연결된 키/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-140">App info is a key/value pair associated to a device.</span></span> <span data-ttu-id="90d77-141">키는 앱 정보의 이름(64자의 ASCII 문자 [zA-A-z], [0-9] 숫자 및 밑줄 [_]로 제한됨)입니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-141">The key is the name of the app info (limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]).</span></span> <span data-ttu-id="90d77-142">값(1024자로 제한됨)은 문자열, 정수, 날짜(yyyy-MM-dd) 또는 부울(true 또는 false)이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-142">The value (limited to 1024 characters) can be any string, integer, date (yyyy-MM-dd) or Boolean (true or false).</span></span>

<span data-ttu-id="90d77-143">앱 정보는 개수에 관계없이 Mobile Engagement 가격 조건으로 정의된 제한 내에서 장치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-143">Any number of app info can be associated to a device, within the limits defined by the Mobile Engagement pricing terms.</span></span> <span data-ttu-id="90d77-144">지정된 단일 키에 대해 Mobile Engagement는 최신 값 집합의 추적(기록 제외)만 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-144">For one given key, Mobile Engagement only keeps track of the latest value set (no history).</span></span> <span data-ttu-id="90d77-145">앱 정보의 값을 설정 또는 변경하면 Mobile Engagement에서 이 앱 정보(있는 경우)에 대한 대상 기준을 다시 평가합니다. 즉, 앱 정보를 사용하여 실시간 푸시를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-145">Setting or changing the value of an app info forces Mobile Engagement to re-evaluate audience criteria set on this app info (if any) meaning that app info can be used to trigger realtime pushes.</span></span>

## <a name="extra-data"></a><span data-ttu-id="90d77-146">추가 데이터</span><span class="sxs-lookup"><span data-stu-id="90d77-146">Extra data</span></span>
<span data-ttu-id="90d77-147">추가 데이터(또는 기타 데이터)는 이벤트, 오류, 작업 및 작업에 연결할 수 있는 임의의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-147">Extra data (or extras) is some arbitrary data that can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="90d77-148">추가 데이터는 JSON 개체와 비슷하게 구조화됩니다. 이러한 데이터는 키/값 쌍의 트리로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-148">Extras are structured similarly to JSON objects: they are made of a tree of key/value pairs.</span></span> <span data-ttu-id="90d77-149">키가 64자의 ASCII 문자 [zA-A-z], 숫자 [0-9] 및 밑줄 [_]로 제한되며 추가 데이터의 총 크기는 1024 자(Mobile Engagement SDK에 의해 JSON에서 한번 인코딩됨)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-149">Keys are limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]) and the total size of extras is limited to 1024 characters (once encoded in JSON by the Mobile Engagement SDK).</span></span>

<span data-ttu-id="90d77-150">키/값 쌍의 전체 트리는 JSON 개체로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-150">The whole tree of key/value pairs is stored as a JSON object.</span></span> <span data-ttu-id="90d77-151">그러나 첫 번째 수준의 키/값은 Segments와 같은 일부 고급 함수에서 직접 액세스할 수 있도록 구성 해제됩니다. 예를 들어 지난 달에 추가 키 "content_type"이 "scifi" 값으로 설정된 "content_viewed"라는 이벤트를 10번 이상 전송한 모든 사용자로 구성된 "SciFi 팬" 세그먼트를 쉽게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-151">Nevertheless, only the first level of keys/values is decomposed to be directly accessible to some advanced functions like Segments (for example, you can easily define a segment called “SciFi fans” that is made of all users having sent at least 10 times the event named “content_viewed” with the extra key “content_type” set to the value “scifi” in the last month).</span></span> <span data-ttu-id="90d77-152">따라서 스칼라 값(예: 문자열, 날짜, 정수 또는 부울)을 사용하여 키/값 쌍의 간단한 목록으로 구성된 기타 데이터만 보내는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90d77-152">It is thus highly recommended to send only extras made of simple lists of key/value pairs using scalar values (for example, strings, dates, integers or Boolean).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90d77-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90d77-153">Next steps</span></span>
* [<span data-ttu-id="90d77-154">Azure Mobile Engagement의 Windows 유니버설 SDK 개요</span><span class="sxs-lookup"><span data-stu-id="90d77-154">Windows Universal SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-store-sdk-overview.md)
* [<span data-ttu-id="90d77-155">Azure Mobile Engagement의 Windows Phone Silverlight SDK 개요</span><span class="sxs-lookup"><span data-stu-id="90d77-155">Windows Phone Silverlight SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
* [<span data-ttu-id="90d77-156">Azure Mobile Engagement용 iOS SDK</span><span class="sxs-lookup"><span data-stu-id="90d77-156">iOS SDK for Azure Mobile Engagement</span></span>](mobile-engagement-ios-sdk-overview.md)
* [<span data-ttu-id="90d77-157">Azure Mobile Engagement용 Android SDK</span><span class="sxs-lookup"><span data-stu-id="90d77-157">Android SDK for Azure Mobile Engagement</span></span>](mobile-engagement-android-sdk-overview.md)

