---
title: "Azure Mobile Engagement 사용자 인터페이스 - 도달률 방법"
description: "Azure Mobile Engagement의 사용자 인터페이스 개요"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 33a0a9d0c399cb7f0a791c4c16dde2e2d62364ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-using-and-managing-pushes-to-reach-out-to-your-end-users"></a><span data-ttu-id="f5763-103">사용 시작 및 최종 사용자에게 도달하는 푸시 관리 방법</span><span class="sxs-lookup"><span data-stu-id="f5763-103">How to get started using and managing pushes to reach out to your end users</span></span>
<span data-ttu-id="f5763-104">SDK가 응용 프로그램에 완전히 통합되면 UI의 도달률 섹션을 사용하기 시작하여 응용 프로그램의 사용자에게 푸시 알림을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span></span>  

## <a name="do-your-first-push-notification-campaign"></a><span data-ttu-id="f5763-105">첫 번째 푸시 알림 캠페인 수행</span><span class="sxs-lookup"><span data-stu-id="f5763-105">Do Your First Push Notification Campaign</span></span>
* <span data-ttu-id="f5763-106">Reach가 SDK와 함께 앱에 통합되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-106">Confirm that your Reach is integrated into your app with the SDK.</span></span> 
* <span data-ttu-id="f5763-107">응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-107">Select your application</span></span>

![First1][1]

* <span data-ttu-id="f5763-109">"도달률" 섹션으로 이동하여 "새 알림"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-109">Go to the "Reach" Section and Click "New announcement"</span></span>

![First2][2]

* <span data-ttu-id="f5763-111">새 캠페인을 만들고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-111">Create a new campaign and name it</span></span>
  
![First3][3]

* <span data-ttu-id="f5763-113">알림을 배달하는 방식을 앱 내에서만으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-113">Select how the notification should be delivered, as In-app only</span></span>

![First4][4]

* <span data-ttu-id="f5763-115">푸시하려는 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-115">Create the message you want to push</span></span>

![First5][5]

* <span data-ttu-id="f5763-117">알림 제목을 작성할 수 있습니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="f5763-117">You may write a title on the notification (Optional).</span></span>
* <span data-ttu-id="f5763-118">푸시 메시지 내용을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-118">Write push message content.</span></span>
* <span data-ttu-id="f5763-119">이미지를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-119">You can upload an image.</span></span> <span data-ttu-id="f5763-120">파일의 크기는 32,768바이트를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span></span>
* <span data-ttu-id="f5763-121">또한 추가 옵션을 선택할 수 있지만, 이 자습서의 주제에 집중하기 위해 나중에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span></span>
* <span data-ttu-id="f5763-122">콘텐츠 형식을 알림만으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-122">Select the content type as Notification only</span></span>

![First6][6]

* <span data-ttu-id="f5763-124">푸시 캠페인을 만듭니다. 그러면 해당 캠페인이 캠페인 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-124">Create your push campaign and it will appear in your campaign list.</span></span>

![First7][7]

## <a name="test-your-push-notification-campaign"></a><span data-ttu-id="f5763-126">푸시 알림 캠페인 테스트</span><span class="sxs-lookup"><span data-stu-id="f5763-126">Test Your Push Notification Campaign</span></span>
![Test1][8]

* <span data-ttu-id="f5763-128">장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-128">Register your device.</span></span>
* <span data-ttu-id="f5763-129">푸시하려는 장치의 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-129">Click on the checkbox of the device you want to push.</span></span>
* <span data-ttu-id="f5763-130">"테스트" 단추를 클릭하여 장치에 푸시를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-130">Click on the "Test" button to send the push to the device.</span></span>

![Test2][9]

* <span data-ttu-id="f5763-132">캠페인을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-132">Activate the campaign</span></span>

![Test3][10]

* <span data-ttu-id="f5763-134">캠페인을 만들었으므로 사용자에게 알림을 푸시하려면 캠페인을 활성화하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span></span>

## <a name="send-personalized-pushes"></a><span data-ttu-id="f5763-135">개인 설정 푸시 보내기</span><span class="sxs-lookup"><span data-stu-id="f5763-135">Send Personalized Pushes</span></span>
* <span data-ttu-id="f5763-136">이 예제에서는 푸시 알림에 사용자 지정 리베이트 코드를 입력하는 푸시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-136">This example creates a push where a custom rebate code is entered into the push notification.</span></span>

![Personalize1][11]

<span data-ttu-id="f5763-138">개인 설정은 앱 정보 태그에서 마커를 바꿈으로써 작동되므로 먼저 사용자가 적절한 앱 정보를 정의하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span></span> <span data-ttu-id="f5763-139">이 예제에서 대상 사용자는 이름이 rebate_code인 앱 정보 태그를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-139">In this example the targeted users will have an app info tag named rebate_code defined.</span></span>
<span data-ttu-id="f5763-140">위에서 알 수 있듯이 푸시 알림 내용에는 ${rebate_code} 마커가 포함되어 있는데 이 마커는 앱 정보 태그의 실제 내용으로 교체되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span></span>

> [!WARNING]
> <span data-ttu-id="f5763-141">앱 정보 태그가 사용자에 대해 정의되지 않은 경우 사용자는 푸시를 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-141">If the app info tag is not defined for the user, the user will not receive the push.</span></span>

* <span data-ttu-id="f5763-142">결과</span><span class="sxs-lookup"><span data-stu-id="f5763-142">Result</span></span>

![Personalize2][12]

### <a name="you-can-further-personalize-the-text-your-notification"></a><span data-ttu-id="f5763-144">알림의 텍스트 추가 개인 설정 가능</span><span class="sxs-lookup"><span data-stu-id="f5763-144">You can further personalize the text your notification</span></span>
![Personalize3][13]

* <span data-ttu-id="f5763-146">알림의 제목 포함</span><span class="sxs-lookup"><span data-stu-id="f5763-146">Including the title of the notification,</span></span>
* <span data-ttu-id="f5763-147">메시지의 내용 지정</span><span class="sxs-lookup"><span data-stu-id="f5763-147">And the content of the message.</span></span>
* <span data-ttu-id="f5763-148">알림의 유형(텍스트 뷰 또는 웹 뷰) 선택</span><span class="sxs-lookup"><span data-stu-id="f5763-148">Choose the type of announcement (Text view or Web view)</span></span>

![Personalize4][14]

### <a name="the-body-of-an-announcement-may-also-be-personalized-with"></a><span data-ttu-id="f5763-150">알림의 본문도 다음을 통해 개인 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-150">The body of an announcement may also be personalized with:</span></span>
* <span data-ttu-id="f5763-151">방문 페이지를 사용자 지정하려는 경우 작업 URL</span><span class="sxs-lookup"><span data-stu-id="f5763-151">The action URL, should you want to customize the landing page</span></span>
* <span data-ttu-id="f5763-152">제목</span><span class="sxs-lookup"><span data-stu-id="f5763-152">The title,</span></span>
* <span data-ttu-id="f5763-153">메시지의 본문</span><span class="sxs-lookup"><span data-stu-id="f5763-153">The body of the message.</span></span>

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a><span data-ttu-id="f5763-154">푸시 알림 차별화(앱 내부 또는 외부에서)</span><span class="sxs-lookup"><span data-stu-id="f5763-154">Differentiate Your Push Notification (in or out of app)</span></span>
* <span data-ttu-id="f5763-155">푸시할 알림 유형을 선택하고, 응용 프로그램을 선택하고, "도달률" 섹션으로 이동하여 푸시 캠페인을 선택하거나 생성하고, "알림" 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span></span>
* <span data-ttu-id="f5763-156">원하는 "배달 모드"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-156">Click on the "delivery mode" you want.</span></span>
* <span data-ttu-id="f5763-157">특정 작업(화면)에서 알림의 발생을 원하는 경우 "작업 제한" 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span></span>

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a><span data-ttu-id="f5763-159">"앱 외부에서만" 배달 모드</span><span class="sxs-lookup"><span data-stu-id="f5763-159">"Out of App Only" delivery mode</span></span>
![Differentiate2][16]

<span data-ttu-id="f5763-161">"앱 외부에서만" 배달 모드는 응용 프로그램이 닫힌 경우 푸시 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span></span> <span data-ttu-id="f5763-162">이 모드가 표준 푸시 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-162">This is the standard push notification.</span></span>
<span data-ttu-id="f5763-163">"앱 외부에서만"을 선택한 경우 응용 프로그램이 빌드되고 있는 플랫폼(APNS 또는 GCM)의 인증서를 이미 제공했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span></span>

### <a name="see-also"></a><span data-ttu-id="f5763-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f5763-164">See also</span></span>
* <span data-ttu-id="f5763-165">[Apple 푸시 알림 서비스 - 인증서](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging - 인증서](http://developer.android.com/google/gcm/index.html)</span><span class="sxs-lookup"><span data-stu-id="f5763-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span></span> 

### <a name="in-app-only-delivery-mode"></a><span data-ttu-id="f5763-166">"앱 내에서만" 배달 모드</span><span class="sxs-lookup"><span data-stu-id="f5763-166">"in-App Only" delivery mode</span></span>
![Differentiate3][17]

<span data-ttu-id="f5763-168">"앱 내에서만" 배달 모드는 응용 프로그램이 실행 중인 경우 푸시 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-168">"In-App Only" delivery mode provides push notification when the application is running.</span></span>
<span data-ttu-id="f5763-169">이 알림의 경우 APNS 및 GCM 시스템을 통해 이동할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-169">For this notification, you do not need to go through the APNS and GCM system.</span></span>
<span data-ttu-id="f5763-170">앱 내 배달 시스템을 사용하여 최종 사용자에게 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-170">You can use the in-app delivery system to reach your end-users.</span></span>
<span data-ttu-id="f5763-171">알림을 완벽하게 사용자 지정할 수 있으며 알림이 표시되는 작업(화면)을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span></span>

### <a name="anytime-delivery-mode"></a><span data-ttu-id="f5763-172">"항상" 배달 모드</span><span class="sxs-lookup"><span data-stu-id="f5763-172">"Anytime" delivery mode</span></span>
<span data-ttu-id="f5763-173">"항상" 배달 모드를 선택하면 응용 프로그램의 실행 여부와 상관없이 최종 사용자에게 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span></span>
<span data-ttu-id="f5763-174">"항상"을 선택한 경우 응용 프로그램이 빌드되고 있는 플랫폼(APNS 또는 GCM)의 인증서를 이미 제공했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span></span> 

## <a name="schedule-a-push-campaign"></a><span data-ttu-id="f5763-175">푸시 캠페인 예약</span><span class="sxs-lookup"><span data-stu-id="f5763-175">Schedule a Push Campaign</span></span>
### <a name="plan-to-start-a-campaign"></a><span data-ttu-id="f5763-176">캠페인 시작 계획</span><span class="sxs-lookup"><span data-stu-id="f5763-176">Plan to Start a campaign</span></span>
![Shedule1][18]

<span data-ttu-id="f5763-178">3월 21일인데, 3월 22일 자정에 발표를 계획한 알림이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span></span> <span data-ttu-id="f5763-179">이 경우 푸시를 수행하기 위해 인터페이스 앞에 대기하고 있지 않아도 됩니다!</span><span class="sxs-lookup"><span data-stu-id="f5763-179">You don’t have to stay in front of the interface to do a push!</span></span> <span data-ttu-id="f5763-180">정확한 시간에 알림이 전송되도록 미리 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-180">You can plan in advance the exact minute notifications will be sent.</span></span>

* <span data-ttu-id="f5763-181">"없음" 확인란의 선택을 취소하고 시작 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-181">Un-check the "None" checkbox and select a start time</span></span> 
* <span data-ttu-id="f5763-182">푸시 캠페인을 시작할 날짜 및 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-182">Choose the date and the time you want to start the push campaign.</span></span>

### <a name="plan-to-end-a-campaign"></a><span data-ttu-id="f5763-183">캠페인 종료 계획</span><span class="sxs-lookup"><span data-stu-id="f5763-183">Plan to end a campaign</span></span>
![Shedule2][19]

<span data-ttu-id="f5763-185">3월 25일 오후 3시에 캠페인을 중지하고 싶지만, 그 시간에 해당 장소에 없다는 것을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span></span>
<span data-ttu-id="f5763-186">이 경우 푸시를 수행하려고 인터페이스 앞에 대기하고 있지 않아도 됩니다!</span><span class="sxs-lookup"><span data-stu-id="f5763-186">You don’t have to stay in front of the interface to push!</span></span> <span data-ttu-id="f5763-187">정확한 시간에 캠페인이 중지되도록 미리 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-187">You can plan in advance the exact minute your campaign will stop.</span></span>

* <span data-ttu-id="f5763-188">"없음" 확인란을 클릭하거나 종료 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-188">Click on the "None" checkbox or select a end time</span></span>
* <span data-ttu-id="f5763-189">푸시 캠페인을 완료할 날짜 및 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-189">Choose the date and the time you want to finish the push campaign.</span></span>

### <a name="end-a-campaign-manually"></a><span data-ttu-id="f5763-190">캠페인 수동 종료</span><span class="sxs-lookup"><span data-stu-id="f5763-190">End a campaign manually</span></span>
![Shedule3][20]

<span data-ttu-id="f5763-192">기본적으로 "없음" 확인란이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-192">By default, the "None" check-boxes are selected.</span></span>
<span data-ttu-id="f5763-193">이는 도달률 섹션에서 캠페인을 활성화하는 즉시 캠페인이 시작되며 도달률 섹션에서 캠페인을 중지하면 종료된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span></span>

> [!NOTE]
> <span data-ttu-id="f5763-194">종료 날짜 없이 작성된 캠페인은 푸시를 장치에 로컬로 저장하며, 캠페인을 수동으로 종료하더라도 다음 번에 앱을 열 때 해당 푸시를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span></span>

## <a name="enhance-a-push-notification-with-a-text-view"></a><span data-ttu-id="f5763-195">텍스트 뷰로 푸시 알림 개선</span><span class="sxs-lookup"><span data-stu-id="f5763-195">Enhance a Push Notification with a Text View</span></span>
### <a name="what-is-a-text-view"></a><span data-ttu-id="f5763-196">텍스트 뷰란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f5763-196">What is a Text View?</span></span>
![TextView1][21]

<span data-ttu-id="f5763-198">텍스트 뷰는 텍스트 내용이 있는 팝업입니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-198">A text view is a pop-up with text content.</span></span> <span data-ttu-id="f5763-199">이 팝업은 최종 사용자가 푸시 알림을 클릭한 후에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-199">This pop-up appears after the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="f5763-200">텍스트 뷰를 사용하면 최종 사용자에게 더 많은 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-200">A text view allows you to present more content to your end-user.</span></span> <span data-ttu-id="f5763-201">또한 텍스트 뷰는 앱의 페이지로 이동하고 스토어로 리디렉션하고 웹 페이지를 열고 메일을 보내고 지역 검색을 시작하는 등의 작업에 대한 호출을 제공할 수 있는 기회도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-text-view"></a><span data-ttu-id="f5763-202">예: 텍스트 뷰</span><span class="sxs-lookup"><span data-stu-id="f5763-202">Example: Text View</span></span>
* <span data-ttu-id="f5763-203">"도달률" 섹션에서 푸시 알림 캠페인을 만들고 캠페인에 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span></span>

![TextView2][22]

* <span data-ttu-id="f5763-205">알림에 표시할 메시지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-205">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="f5763-206">알림 콘텐츠 유형으로 "텍스트"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-206">Select the Announcement Content Type of “text”</span></span>

![TextView3][23]

> [!NOTE]
> <span data-ttu-id="f5763-208">텍스트 뷰를 푸시할 경우 항상 알림이 먼저 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-208">When you push a text view, it always comes with a notification first.</span></span> 

* <span data-ttu-id="f5763-209">텍스트를 정의합니다. 텍스트 알림 내용을 선택하면 하위 섹션이 표시됩니다. 이 섹션에서 표시할 텍스트를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span></span>

![TextView4][24]

* <span data-ttu-id="f5763-211">메시지의 상단에 표시할 제목을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-211">Write the title that will appear at the top of the message.</span></span>
* <span data-ttu-id="f5763-212">텍스트 뷰의 주요 내용을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-212">Write the main content of the text view.</span></span>
* <span data-ttu-id="f5763-213">실행 단추에 표시할 내용을 작성합니다. 실행 단추를 사용하면 응용 프로그램의 페이지를 열고 앱 스토어 또는 제공할 수 있는 종류의 소스로 리디렉션하는 등 응용 프로그램에서 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="f5763-214">끝내기 단추에 표시할 내용을 작성합니다. 끝내기 단추를 클릭하면 텍스트 뷰가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span></span>
* <span data-ttu-id="f5763-215">푸시 알림 캠페인을 만듭니다. 그러면 해당 캠페인이 캠페인 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-215">Create your push notification campaign and it will appear on the campaign list.</span></span>

![TextView5][25]

* <span data-ttu-id="f5763-217">푸시 알림 캠페인을 활성화하여 텍스트 뷰를 최종 사용자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-217">Activate your push notification campaign to send the text view to your users.</span></span>

![TextView6][26]

* <span data-ttu-id="f5763-219">결과</span><span class="sxs-lookup"><span data-stu-id="f5763-219">Result</span></span>

![TextView7][27]

* <span data-ttu-id="f5763-221">사용자가 알림을 받고 해당 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-221">The user receives the notification and click on it.</span></span>
* <span data-ttu-id="f5763-222">텍스트 뷰는 사용자가 조작할 수 있는 팝업으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-222">The text view appears as a pop-up allowing the user to interact with it.</span></span>

## <a name="enhance-a-push-notification-with-a-web-view"></a><span data-ttu-id="f5763-223">웹 뷰로 푸시 알림 개선</span><span class="sxs-lookup"><span data-stu-id="f5763-223">Enhance a Push Notification with a Web View</span></span>
### <a name="what-is-a-web-view"></a><span data-ttu-id="f5763-224">웹 뷰란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f5763-224">What is a Web View?</span></span>
![WebView1][28]

<span data-ttu-id="f5763-226">웹 뷰는 웹 콘텐츠가 있는 팝업입니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-226">A web view is a pop-up with web content.</span></span> <span data-ttu-id="f5763-227">이 팝업은 최종 사용자가 푸시 알림을 클릭한 경우에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-227">This pop-up appears when the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="f5763-228">웹 뷰를 사용하면 최종 사용자와 더 많은 상호 작용을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-228">A web view allows you to have more interaction with the end-user.</span></span>
<span data-ttu-id="f5763-229">또한 웹 뷰는 앱 스토어로 리디렉션하고 웹 페이지를 열고 메일을 보내고 지역 검색을 시작하는 등의 작업에 대한 호출을 제공할 수 있는 기회도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-web-view"></a><span data-ttu-id="f5763-230">예: 웹 뷰</span><span class="sxs-lookup"><span data-stu-id="f5763-230">Example: Web View</span></span>
* <span data-ttu-id="f5763-231">"도달률" 섹션에서 푸시 캠페인을 만들고 캠페인의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span></span>

![WebView2][29]

* <span data-ttu-id="f5763-233">알림에 표시할 메시지를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-233">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="f5763-234">알림 콘텐츠 유형으로 "웹"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-234">Select the Announcement Content Type as “web”</span></span>

![WebView3][30]

### <a name="about-announcement-types"></a><span data-ttu-id="f5763-236">알림 유형 정보:</span><span class="sxs-lookup"><span data-stu-id="f5763-236">About Announcement types:</span></span>
* <span data-ttu-id="f5763-237">알림 전용: 단순한 표준 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-237">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="f5763-238">즉, 사용자가 알림을 클릭해도 추가 뷰는 표시되지 않으며 해당 알림과 연결된 작업만 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="f5763-239">텍스트 알림: 사용자가 텍스트 뷰를 확인하도록 하는 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="f5763-240">웹 알림: 사용자가 웹 뷰를 확인하도록 하는 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>
  <span data-ttu-id="f5763-241">"웹 알림" 콘텐츠를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-241">Select the "Web announcement" content.</span></span>

> [!NOTE]
> <span data-ttu-id="f5763-242">웹 뷰를 푸시할 경우 항상 알림이 먼저 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-242">When you push a web view, it always comes with a notification first.</span></span>

* <span data-ttu-id="f5763-243">웹 콘텐츠를 정의합니다. 웹 알림 콘텐츠를 선택하면 하위 섹션이 표시됩니다. 이 섹션에서 표시할 웹 뷰 콘텐츠를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span></span>

![WebView4][31]

* <span data-ttu-id="f5763-245">메시지의 상단에 표시할 제목을 작성합니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="f5763-245">Write the title that will appear at the top of the message (optional).</span></span>
* <span data-ttu-id="f5763-246">여기에 HTML 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-246">Write your HTML code here.</span></span>
* <span data-ttu-id="f5763-247">소스 편집 모드 단추를 클릭하여 편집으로 전환하고 어떤 모양으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-247">Click on the source editing mode button to switch edition and see how it looks like.</span></span>
* <span data-ttu-id="f5763-248">실행 단추에 표시할 내용을 작성합니다. 실행 단추를 사용하면 응용 프로그램의 페이지를 열고 스토어 또는 제공할 수 있는 종류의 소스로 리디렉션하는 등 응용 프로그램에서 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="f5763-249">끝내기 단추에 표시할 내용을 작성합니다. 끝내기 단추를 클릭하면 웹 뷰가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span></span>
* <span data-ttu-id="f5763-250">결과</span><span class="sxs-lookup"><span data-stu-id="f5763-250">Result</span></span>

![WebView5][32]

* <span data-ttu-id="f5763-252">사용자가 알림을 받고 해당 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-252">The user receive the notification and click on it.</span></span>
* <span data-ttu-id="f5763-253">텍스트 뷰는 사용자가 조작할 수 있는 팝업으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5763-253">The text view appears as a pop-up allowing the user to interact with it.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

