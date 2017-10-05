---
title: "iOS에서 Engagement API를 사용하는 방법"
description: "최신 iOS SDK - iOS에서 Engagement API를 사용하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="3c881-103">iOS에서 Engagement API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="3c881-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="3c881-104">이 문서는 iOS에 Engagement를 통합하는 방법 문서를 보완하는 추가 문서로, Engagement API를 사용하여 응용 프로그램 통계를 보고하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="3c881-105">Engagement에서 응용 프로그램 세션, 활동, 작동 중단 및 기술 정보만 보고하도록 하려는 경우 가장 간단한 방법은 모든 사용자 지정 `UIViewController` 개체가 해당 `EngagementViewController` 클래스에서 상속하도록 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="3c881-106">응용 프로그램 관련 이벤트, 오류, 작업을 보고하는 등 추가 작업을 수행하려는 경우 또는 `EngagementViewController` 클래스에서 구현되는 것과는 다른 방식으로 응용 프로그램 활동을 보고해야 하는 경우에는 Engagement API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="3c881-107">Engagement API는 `EngagementAgent` 클래스를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="3c881-108">이 클래스의 인스턴스는 `[EngagementAgent shared]` 정적 메서드를 호출하여 검색할 수 있습니다(반환되는 `EngagementAgent` 개체는 단일 항목임).</span><span class="sxs-lookup"><span data-stu-id="3c881-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="3c881-109">API를 호출하기 전에 메서드 `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`을(를) 호출하여 `EngagementAgent` 개체를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="3c881-110">Engagement 개념</span><span class="sxs-lookup"><span data-stu-id="3c881-110">Engagement concepts</span></span>
<span data-ttu-id="3c881-111">다음 요소는 iOS 플랫폼과 관련된 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) 을 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3c881-112">`Session` 및 `Activity`</span><span class="sxs-lookup"><span data-stu-id="3c881-112">`Session` and `Activity`</span></span>
<span data-ttu-id="3c881-113">*작업*은 일반적으로 단일 응용 프로그램 화면과 연결됩니다. 즉, *작업*은 화면을 표시하면 시작되며 화면을 닫으면 중지됩니다. `EngagementViewController` 클래스를 사용하여 Engagement SDK를 통합하는 경우 이러한 방식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="3c881-114">하지만 Engagement API를 사용하여 *활동* 을 수동으로 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="3c881-115">이렇게 하면 지정된 화면을 여러 하위 부분으로 분할하여 해당 화면의 사용에 대해 더 많은 세부 정보(예: 이 화면 내에서 대화 상자를 사용하는 빈도와 기간)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3c881-116">활동 보고</span><span class="sxs-lookup"><span data-stu-id="3c881-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3c881-117">사용자가 새 활동을 시작함</span><span class="sxs-lookup"><span data-stu-id="3c881-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="3c881-118">사용자 활동이 변경될 때마다 `startActivity()` 을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="3c881-119">이 함수를 처음 호출하면 새 사용자 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="3c881-120">사용자가 현재 활동을 종료함</span><span class="sxs-lookup"><span data-stu-id="3c881-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="3c881-121">단일 응용 프로그램 사용을 여러 세션으로 분할하려는 경우를 제외하고는 이 함수를 직접 호출하면 **안 됩니다**. 이 함수를 호출하면 현재 세션이 즉시 종료되므로 `startActivity()`를 후속 호출 시 새 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="3c881-122">응용 프로그램을 닫으면 SDK에서 이 함수를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="3c881-123">이벤트 보고</span><span class="sxs-lookup"><span data-stu-id="3c881-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="3c881-124">세션 이벤트</span><span class="sxs-lookup"><span data-stu-id="3c881-124">Session events</span></span>
<span data-ttu-id="3c881-125">세션 이벤트는 일반적으로 사용자가 세션 중에 수행하는 동작을 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="3c881-126">**추가 데이터가 없는 예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="3c881-127">**추가 데이터가 있는 예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="3c881-128">독립 실행형 이벤트</span><span class="sxs-lookup"><span data-stu-id="3c881-128">Standalone events</span></span>
<span data-ttu-id="3c881-129">세션 이벤트와 달리 독립 실행형 이벤트는 세션의 컨텍스트 외부에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="3c881-130">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="3c881-131">오류 보고</span><span class="sxs-lookup"><span data-stu-id="3c881-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="3c881-132">세션 오류</span><span class="sxs-lookup"><span data-stu-id="3c881-132">Session errors</span></span>
<span data-ttu-id="3c881-133">세션 오류는 일반적으로 세션 중에 사용자에게 영향을 주는 오류를 보고하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="3c881-134">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="3c881-135">독립 실행형 오류</span><span class="sxs-lookup"><span data-stu-id="3c881-135">Standalone errors</span></span>
<span data-ttu-id="3c881-136">세션 오류와 달리 독립 실행형 오류는 세션의 컨텍스트 외부에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="3c881-137">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="3c881-138">작업 보고</span><span class="sxs-lookup"><span data-stu-id="3c881-138">Reporting Jobs</span></span>
<span data-ttu-id="3c881-139">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-139">**Example:**</span></span>

<span data-ttu-id="3c881-140">로그인 프로세스의 기간을 보고하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-140">Suppose you want to report the duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="3c881-141">작업 중 오류 보고</span><span class="sxs-lookup"><span data-stu-id="3c881-141">Report Errors during a Job</span></span>
<span data-ttu-id="3c881-142">오류는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="3c881-143">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-143">**Example:**</span></span>

<span data-ttu-id="3c881-144">로그인 프로세스 중의 오류를 보고하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="3c881-145">작업 중의 이벤트</span><span class="sxs-lookup"><span data-stu-id="3c881-145">Events during a job</span></span>
<span data-ttu-id="3c881-146">이벤트는 현재 사용자 세션이 아닌 실행 중인 작업에 관련될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="3c881-147">**예:**</span><span class="sxs-lookup"><span data-stu-id="3c881-147">**Example:**</span></span>

<span data-ttu-id="3c881-148">소셜 네트워크가 있으며 작업을 사용하여 사용자가 서버에 연결되어 있는 총 시간을 보고한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="3c881-149">사용자는 친구로부터 메시지를 받을 수 있습니다. 이것이 작업 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-149">The user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="3c881-150">extras 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3c881-150">Extra parameters</span></span>
<span data-ttu-id="3c881-151">이벤트, 오류, 활동 또는 작업에 임의 데이터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="3c881-152">이 데이터는 구조화할 수 있으며 iOS의 NSDictionary 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="3c881-153">extras는`arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` 또는 기타 `NSDictionary` 인스턴스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="3c881-154">extras 매개 변수는 JSON에서 serialize됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="3c881-155">위에서 설명한 것과 다른 개체를 전달하려는 경우에는 클래스에서 다음 메서드를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="3c881-156">-(NSString*) JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="3c881-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="3c881-157">해당 메서드는 개체의 JSON 표현을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="3c881-158">예</span><span class="sxs-lookup"><span data-stu-id="3c881-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="3c881-159">제한</span><span class="sxs-lookup"><span data-stu-id="3c881-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3c881-160">구성</span><span class="sxs-lookup"><span data-stu-id="3c881-160">Keys</span></span>
<span data-ttu-id="3c881-161">`NSDictionary` 의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="3c881-162">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3c881-163">크기</span><span class="sxs-lookup"><span data-stu-id="3c881-163">Size</span></span>
<span data-ttu-id="3c881-164">extras는 Engagement 에이전트에 의해 JSON으로 인코딩되고 나면 호출당 **1024** 자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="3c881-165">위의 예제에서 서버로 전송된 JSON의 길이는 58자입니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="3c881-166">응용 프로그램 정보 보고</span><span class="sxs-lookup"><span data-stu-id="3c881-166">Reporting Application Information</span></span>
<span data-ttu-id="3c881-167">`sendAppInfo:` 함수를 사용하면 추적 정보 또는 기타 응용 프로그램 관련 정보를 수동으로 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="3c881-168">이러한 정보는 증분 방식으로 보낼 수 있습니다. 그러면 특정 장치에 대해 지정한 키의 최신 값만 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="3c881-169">extras 이벤트와 마찬가지로 `NSDictionary` 클래스도 응용 프로그램 정보를 요약하는 데 사용됩니다. 배열 또는 하위 사전은 JSON serialization을 사용하여 플랫 문자열로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="3c881-170">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3c881-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="3c881-171">제한</span><span class="sxs-lookup"><span data-stu-id="3c881-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3c881-172">구성</span><span class="sxs-lookup"><span data-stu-id="3c881-172">Keys</span></span>
<span data-ttu-id="3c881-173">`NSDictionary` 의 각 키는 다음 정규식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="3c881-174">즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3c881-175">크기</span><span class="sxs-lookup"><span data-stu-id="3c881-175">Size</span></span>
<span data-ttu-id="3c881-176">응용 프로그램 정보s는 Engagement 에이전트에 의해 JSON으로 인코딩되고 나면 호출당 **1024** 자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="3c881-177">위의 예제에서 서버로 전송된 JSON의 길이는 44자입니다.</span><span class="sxs-lookup"><span data-stu-id="3c881-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
