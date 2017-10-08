---
title: "aaaMobile Engagement 개념 | Microsoft Docs"
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
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a><span data-ttu-id="7b52c-103">Azure Mobile Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="7b52c-103">Azure Mobile Engagement concepts</span></span>
<span data-ttu-id="7b52c-104">Mobile Engagement는 몇 가지 개념 일반적인 tooall 지원 플랫폼을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-104">Mobile Engagement defines a few concepts common tooall supported platforms.</span></span> <span data-ttu-id="7b52c-105">이 문서에서는 이러한 개념을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-105">This article briefly describes those concepts.</span></span>

<span data-ttu-id="7b52c-106">이 문서는 좋은 시작은 새 tooMobile 참여 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-106">This article is a good start if you are new tooMobile Engagement.</span></span> <span data-ttu-id="7b52c-107">또한 자세한 세부 정보 및 예제도 가능한 제한 된이 문서에서 설명 하는 hello 개념을 구체화 합니다 대로 사용 하는 있는지 tooread hello 설명서 특정 toohello 플랫폼을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-107">Also make sure tooread hello documentation specific toohello platform you are using, as it will refine hello concepts described in this article with more details and examples as well as possible limitations.</span></span>

## <a name="devices-and-users"></a><span data-ttu-id="7b52c-108">장치 및 사용자</span><span class="sxs-lookup"><span data-stu-id="7b52c-108">Devices and users</span></span>
<span data-ttu-id="7b52c-109">Mobile Engagement는 각 장치에 대한 고유 식별자를 생성하여 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-109">Mobile Engagement identifies users by generating a unique identifier for each device.</span></span> <span data-ttu-id="7b52c-110">이 식별자 hello 장치 식별자 라고 합니다. (또는 `deviceid`).</span><span class="sxs-lookup"><span data-stu-id="7b52c-110">This identifier is called hello device identifier (or `deviceid`).</span></span> <span data-ttu-id="7b52c-111">모든 응용 프로그램 실행 hello 동일 하는 방식으로 생성 됩니다 장치 공유 hello 동일한 장치 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-111">It is generated in such a way that all applications running of hello same device share hello same device identifier.</span></span>

<span data-ttu-id="7b52c-112">암시적으로 Mobile Engagement 장치 toobelong tooexactly 한 사용자를 고려 하 따라서 사용자 및 장치는 해당 하는 개념을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-112">Implicitly, it means that Mobile Engagement considers one device toobelong tooexactly one user, and thus, users and devices are equivalent concepts.</span></span>

## <a name="sessions-and-activities"></a><span data-ttu-id="7b52c-113">세션 및 작업</span><span class="sxs-lookup"><span data-stu-id="7b52c-113">Sessions and activities</span></span>
<span data-ttu-id="7b52c-114">세션은 hello 시간 hello 사용자 로부터 사용자가 수행 하는 hello 응용 프로그램의 용도 중 하나를 사용 하 여 hello 사용자 중지 될 때까지 시작.</span><span class="sxs-lookup"><span data-stu-id="7b52c-114">A session is one use of hello application performed by a user, from hello time hello user starts using it, until hello user stops.</span></span>

<span data-ttu-id="7b52c-115">활동은 사용자가 수행 하는 hello 응용 프로그램의 지정된 된 하위 부분의 용도 중 하나 (일반적으로 화면 하지만 어느 것에 적합 한 toohello 응용 프로그램 수)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-115">An activity is one use of a given sub-part of hello application performed by one user (it is usually a screen, but it can be anything suitable toohello application).</span></span>

<span data-ttu-id="7b52c-116">사용자는 한번에 하나의 동작만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-116">A user can only perform one activity at a time.</span></span>

<span data-ttu-id="7b52c-117">활동 이름 (제한 된 too64 문자 수)으로 식별 및 (1024 바이트의 hello 제한)에서 필요에 따라 몇 가지 추가 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-117">An activity is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

<span data-ttu-id="7b52c-118">세션은 사용자가 수행한 작업의 hello 시퀀스에서 자동으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-118">Sessions are automatically computed from hello sequence of activities performed by users.</span></span> <span data-ttu-id="7b52c-119">Hello 사용자 자신의 첫 번째 활동을 시작 하 고 그 그의 마지막 작업이 끝나면 중지는 세션 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-119">A session starts when hello user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="7b52c-120">즉, 세션을 명시적으로 시작 되거나 중지 toobe 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-120">This means that a session does not need toobe explicitly started or stopped.</span></span> <span data-ttu-id="7b52c-121">대신, 작업이 명시적으로 시작되거나 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-121">Instead, activities are explicitly started or stopped.</span></span> <span data-ttu-id="7b52c-122">작업이 보고되지 않으면 세션이 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-122">If no activity is reported, no session is reported.</span></span>

## <a name="events"></a><span data-ttu-id="7b52c-123">이벤트</span><span class="sxs-lookup"><span data-stu-id="7b52c-123">Events</span></span>
<span data-ttu-id="7b52c-124">이벤트는 사용 되는 tooreport 인스턴트 작업 (예: 단추 누름 또는 사용자가 읽을 문서)입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-124">Events are used tooreport instant actions (like button pressed or articles read by users).</span></span>

<span data-ttu-id="7b52c-125">이벤트 관련된 toohello 현재 세션 작업을 실행 하는 tooa 이거나 독립 실행형 이벤트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-125">An event can be related toohello current session, tooa running job, or it can be a standalone event.</span></span>

<span data-ttu-id="7b52c-126">이벤트 이름 (제한 된 too64 문자)으로 식별 되 고 (1024 바이트의 hello 제한)에서 필요에 따라 몇 가지 추가 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-126">An event is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

## <a name="error"></a><span data-ttu-id="7b52c-127">오류</span><span class="sxs-lookup"><span data-stu-id="7b52c-127">Error</span></span>
<span data-ttu-id="7b52c-128">오류는 hello 응용 프로그램 (예: 잘못 된 사용자 작업 또는 API 호출 실패)가 제대로 검색 하는 사용 되는 tooreport 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-128">Errors are used tooreport issues correctly detected by hello application (like incorrect user actions, or API call failures).</span></span>

<span data-ttu-id="7b52c-129">오류 관련된 toohello 현재 세션 작업을 실행 하는 tooa 이거나 독립 실행형 오류일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-129">An error can be related toohello current session, tooa running job, or it can be a standalone error.</span></span>

<span data-ttu-id="7b52c-130">오류가 이름 (제한 된 too64 문자)으로 식별 되 고 (1024 바이트의 hello 제한)에서 필요에 따라 몇 가지 추가 데이터를 포함할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-130">An error is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

## <a name="job"></a><span data-ttu-id="7b52c-131">작업</span><span class="sxs-lookup"><span data-stu-id="7b52c-131">Job</span></span>
<span data-ttu-id="7b52c-132">작업은 사용 되는 tooreport 작업 기간 필요 (마찬가지로 API 호출의 기간, 표시할 광고의 시간, 백그라운드 작업의 기간이 나 사용자 작업의 기간).</span><span class="sxs-lookup"><span data-stu-id="7b52c-132">Jobs are used tooreport actions having a duration (like duration of API calls, display time of ads, duration of background tasks or duration of user actions).</span></span>

<span data-ttu-id="7b52c-133">작업은 사용자 개입 없이 hello 백그라운드에서 작업을 수행할 수 있으므로 관련된 tooa 세션 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-133">A job is not related tooa session, because a task can be performed in hello background, without any user interaction.</span></span>

<span data-ttu-id="7b52c-134">작업 이름 (제한 된 too64 문자)으로 식별 되 있으며 (1024 바이트의 hello 제한)에서 필요에 따라 몇 가지 추가 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-134">A job is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

## <a name="crash"></a><span data-ttu-id="7b52c-135">크래시</span><span class="sxs-lookup"><span data-stu-id="7b52c-135">Crash</span></span>
<span data-ttu-id="7b52c-136">충돌은 hello hello 응용 프로그램에 의해 검색 되지 문제가 확인 오류가 발생 했습니다. 충돌 하는 Mobile Engagement SDK tooreport 응용 프로그램에서 자동으로 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-136">Crashes are issued automatically by hello Mobile Engagement SDK tooreport application failures where issues not detected by hello application make it crash.</span></span>

## <a name="application-information"></a><span data-ttu-id="7b52c-137">응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="7b52c-137">Application information</span></span>
<span data-ttu-id="7b52c-138">응용 프로그램 정보 (또는 앱 정보)는 사용 되는 tootag 사용자, 즉, tooassociate (이 비슷한 tooweb 쿠키를 제외 하 고 앱 정보 hello 서버 쪽 hello Azure Mobile Engagement 플랫폼에 저장 된) 응용 프로그램의 일부 데이터 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-138">Application information (or app info) is used tootag users, that is, tooassociate some data toohello users of an application (this is similar tooweb cookies, except that app info is stored on hello server side on hello Azure Mobile Engagement platform).</span></span>

<span data-ttu-id="7b52c-139">Hello Mobile Engagement SDK API를 사용 하 여 또는 hello Mobile Engagement 플랫폼 Device API를 사용 하 여 응용 프로그램 정보를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-139">App info can be registered by using hello Mobile Engagement SDK API or by using hello Mobile Engagement platform Device API.</span></span>

<span data-ttu-id="7b52c-140">앱 정보에는 키/값 쌍 연결된 tooa 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-140">App info is a key/value pair associated tooa device.</span></span> <span data-ttu-id="7b52c-141">hello 키는 hello 앱 정보 (제한 된 too64 ASCII 문자 [a-zA-Z], [0-9] 숫자 및 밑줄 [__])의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-141">hello key is hello name of hello app info (limited too64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]).</span></span> <span data-ttu-id="7b52c-142">hello 값 (제한 된 too1024 문자)는 문자열, 정수, 날짜 (yyyy-월-일) 또는 부울 (true 또는 false) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-142">hello value (limited too1024 characters) can be any string, integer, date (yyyy-MM-dd) or Boolean (true or false).</span></span>

<span data-ttu-id="7b52c-143">앱 정보 개수에 관계 없이 hello Mobile Engagement 가격 조건에 정의 된 hello 제한 내에서 관련된 tooa 장치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-143">Any number of app info can be associated tooa device, within hello limits defined by hello Mobile Engagement pricing terms.</span></span> <span data-ttu-id="7b52c-144">지정 된 키에 대 한 Mobile Engagement만은 hello 최신 값 집합 기록이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-144">For one given key, Mobile Engagement only keeps track of hello latest value set (no history).</span></span> <span data-ttu-id="7b52c-145">설정 또는 응용 프로그램 정보의 hello 값을 변경 하면 Mobile Engagement toore-이 앱에 설정 된 대상 그룹 조건 평가 정보 (있는 경우)에 해당 응용 프로그램 정보를 의미 합니다. 사용 되는 tootrigger 실시간 푸시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-145">Setting or changing hello value of an app info forces Mobile Engagement toore-evaluate audience criteria set on this app info (if any) meaning that app info can be used tootrigger realtime pushes.</span></span>

## <a name="extra-data"></a><span data-ttu-id="7b52c-146">추가 데이터</span><span class="sxs-lookup"><span data-stu-id="7b52c-146">Extra data</span></span>
<span data-ttu-id="7b52c-147">추가 데이터 (또는 추가 기능)는 일부 임의의 데이터 연결된 tooevents, 오류, 활동 및 작업 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-147">Extra data (or extras) is some arbitrary data that can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="7b52c-148">추가 기능 구성 유사한 tooJSON 개체: 키/값 쌍의 트리 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-148">Extras are structured similarly tooJSON objects: they are made of a tree of key/value pairs.</span></span> <span data-ttu-id="7b52c-149">키는 제한 too64 ASCII 문자 [zA-A-z], [0-9] 및 [__] 밑줄) hello extras의 총 크기는 제한 된 too1024 (한 번에서 인코딩된 문자 JSON에서 Mobile Engagement SDK hello).</span><span class="sxs-lookup"><span data-stu-id="7b52c-149">Keys are limited too64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]) and hello total size of extras is limited too1024 characters (once encoded in JSON by hello Mobile Engagement SDK).</span></span>

<span data-ttu-id="7b52c-150">키/값 쌍의 전체 트리 hello JSON 개체로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-150">hello whole tree of key/value pairs is stored as a JSON object.</span></span> <span data-ttu-id="7b52c-151">그럼에도 불구 하 고 유일한 hello 첫 번째 키/값 수준은 분해 된 toobe 액세스할 수 있는 toosome 세그먼트와 같은 함수를 고급 직접 (예를 들어 쉽게 정의한 10 번 이상 hello 이벤트 전송을 모든 사용자가 구성 된 "SciFi 팬" 라는 세그먼트 명명 된 content_type"hello 불필요 한 키"와 "content_viewed" hello에 scifi"집합 toohello 값" 지난 한 달).</span><span class="sxs-lookup"><span data-stu-id="7b52c-151">Nevertheless, only hello first level of keys/values is decomposed toobe directly accessible toosome advanced functions like Segments (for example, you can easily define a segment called “SciFi fans” that is made of all users having sent at least 10 times hello event named “content_viewed” with hello extra key “content_type” set toohello value “scifi” in hello last month).</span></span> <span data-ttu-id="7b52c-152">따라서 좋습니다 toosend만 extras 스칼라 값 (예: 문자열, 날짜, 정수 또는 부울 값)를 사용 하 여 키/값 쌍의 단순 목록을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b52c-152">It is thus highly recommended toosend only extras made of simple lists of key/value pairs using scalar values (for example, strings, dates, integers or Boolean).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b52c-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b52c-153">Next steps</span></span>
* [<span data-ttu-id="7b52c-154">Azure Mobile Engagement의 Windows 유니버설 SDK 개요</span><span class="sxs-lookup"><span data-stu-id="7b52c-154">Windows Universal SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-store-sdk-overview.md)
* [<span data-ttu-id="7b52c-155">Azure Mobile Engagement의 Windows Phone Silverlight SDK 개요</span><span class="sxs-lookup"><span data-stu-id="7b52c-155">Windows Phone Silverlight SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
* [<span data-ttu-id="7b52c-156">Azure Mobile Engagement용 iOS SDK</span><span class="sxs-lookup"><span data-stu-id="7b52c-156">iOS SDK for Azure Mobile Engagement</span></span>](mobile-engagement-ios-sdk-overview.md)
* [<span data-ttu-id="7b52c-157">Azure Mobile Engagement용 Android SDK</span><span class="sxs-lookup"><span data-stu-id="7b52c-157">Android SDK for Azure Mobile Engagement</span></span>](mobile-engagement-android-sdk-overview.md)

