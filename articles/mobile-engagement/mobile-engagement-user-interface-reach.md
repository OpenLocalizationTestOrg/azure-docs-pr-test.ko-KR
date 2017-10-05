---
title: "Azure Mobile Engagement 사용자 인터페이스 - 도달률"
description: "푸시 알림으로 응용 프로그램의 사용자에게 알리는 방법 알아보기"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="09657-103">푸시 알림으로 응용 프로그램의 사용자에게 알리는 방법</span><span class="sxs-lookup"><span data-stu-id="09657-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="09657-104">이 문서에서는 **Mobile Engagement** 포털의 **도달률** 탭을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="09657-105">**Mobile Engagement** 포털을 사용하여 모바일 앱을 모니터링하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="09657-106">포털 사용을 시작하려면 먼저 **Azure Mobile Engagement** 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="09657-107">자세한 내용은 [Azure Mobile Engagement 계정 만들기](mobile-engagement-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09657-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="09657-108">UI의 도달률 섹션은 푸시 알림 캠페인과 기능을 작성/편집/활성화/완료/모니터링하고 관련 통계를 가져올 수 있는 푸시 캠페인 관리 도구입니다. 하위 수준 푸시 API의 일부 요소와 도달률 API를 통해서도 이러한 캠페인과 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="09657-109">API나 UI 중 어느 쪽을 사용하든 Azure Mobile Engagement 및 도달률을 모두 SDK와 함께 각 플랫폼의 응용 프로그램에 통합해야 도달률 캠페인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="09657-110">**Mobile Engagement** 포털 UI의 여러 섹션에는 **도움말 표시** 단추가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="09657-111">섹션에 대해 더 자세한 문맥 정보를 보려면 이 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="09657-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="09657-112">4가지 푸시 알림 유형</span><span class="sxs-lookup"><span data-stu-id="09657-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="09657-113">알림 - 사용자에게 광고 메시지를 보낼 수 있습니다. 사용자는 해당 메시지를 앱 내의 다른 위치로 리디렉션하거나 웹 페이지로 보내거나 앱 외부에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="09657-114">설문 조사 - 최종 사용자에게 질문을 하여 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="09657-115">데이터 푸시 - 이진 또는 base64 데이터 파일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="09657-116">데이터 푸시에 포함된 정보는 앱의 현재 사용자 환경을 수정하기 위해 응용 프로그램으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="09657-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="09657-117">응용 프로그램은 데이터 푸시의 데이터를 처리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="09657-118">캠페인 세부 정보</span><span class="sxs-lookup"><span data-stu-id="09657-118">Campaign Details</span></span>
<span data-ttu-id="09657-119">아직 활성화되지 않은 캠페인의 이름을 가리켜 해당 캠페인을 편집, 복제, 삭제 또는 활성화할 수 있으며 캠페인을 클릭하여 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="09657-120">이미 활성화된 캠페인의 이름을 가리켜 해당 캠페인을 복제할 수 있으며 캠페인을 클릭하여 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="09657-121">그러나 활성화된 캠페인은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="09657-123">도달률 피드백</span><span class="sxs-lookup"><span data-stu-id="09657-123">Reach Feedback</span></span>
<span data-ttu-id="09657-124">**통계** 를 클릭하여 도달률 캠페인의 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="09657-125">**간단한** 보기는 캠페인이 활성화된 후에 변경된 내용에 대한 열 막대 그래프의 형태로 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="09657-126">**고급** 보기는 푸시 캠페인에 대한 더 세부적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="09657-127">테스트 캠페인을 보내면 즉, 테스트 장치에 푸시를 전송하면 이러한 세부 정보를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="09657-128">이러한 세부 정보를 해석해야 하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="09657-129">**푸시됨** - 장치에 푸시된 메시지 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="09657-130">이 번호는 푸시 캠페인을 만들 동안 지정한 대상 사용자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="09657-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="09657-131">대상 사용자를 지정하지 않으면 이 푸시를 등록된 모든 장치에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="09657-132">다른 모든 푸시 서비스와 마찬가지로 알림을 장치에 직접 푸시하지 않지만 대신 해당 플랫폼 특정 푸시 알림 서비스(PNS-WNS/GCM/APNS)에 알림을 푸시하므로 장치에 알림을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="09657-133">**전달됨** - PNS에서 장치에 성공적으로 전달되고 Mobile Engagement SDK에서 받은 대로 승인된 메시지의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="09657-134">*전송됨 수가 푸시됨 수 보다 작은 이유:*</span><span class="sxs-lookup"><span data-stu-id="09657-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="09657-135">사용자가 장치에서 앱을 제거하지만 PNS에 푸시를 전송할 때 PNS가 알지 못한 경우 메시지는 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="09657-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="09657-136">장치에 앱이 있지만 장치 자체가 오랜 시간 동안 오프라인 상태라면 PNS는 장치로 메시지를 전송하는 데 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="09657-137">메시지가 장치에 전달되지만 앱의 Mobile Engagement SDK가 메시지의 콘텐츠를 인식하지 못하는 경우 해당 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="09657-138">앱의 알림을 사용자 지정하여 SDK에서 발견되는 예외를 생성하고 메시지를 삭제하는 경우 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="09657-139">또한 플랫폼에서 전송된 푸시 메시지의 최신 버전을 이해할 수 없지만 알림이 플랫폼에서 발송되기 전에 앱이 업그레이드될 때만 해당하는 Mobile Engagement SDK의 버전을 장치의 앱이 사용하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="09657-140">**고급** 탭은 얼마나 많은 메시지가 삭제되었는지 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="09657-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="09657-141">iOS 장치에서 장치의 배터리가 부족하거나 앱이 원격 알림을 처리할 때 상당한 양의 전원을 사용하는 경우 메시지가 가끔 배달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="09657-142">이는 iOS 장치의 한계입니다.</span><span class="sxs-lookup"><span data-stu-id="09657-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="09657-143">**표시됨** - 모바일 앱 내의 알림 센터 또는 앱 내 알림에서 시스템 푸시/앱 알림 형식의 장치에 있는 앱 사용자에게 성공적으로 표시되는 메시지의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="09657-144">**고급** 탭은 얼마나 많은 시스템 알림이 있었으며 얼마나 많은 앱 내 알림이 있었는지 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="09657-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="09657-145">*전송됨 수가 표시됨 수 보다 적은 이유(표시됨 대기 중)*</span><span class="sxs-lookup"><span data-stu-id="09657-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="09657-146">알림 캠페인이 종료 날짜에 있다면 알림이 전송되었을 가능성이 있습니다. 하지만 알림이 앱 사용자에게 열리고 표시되는 시간이 왔을 때 알림은 이미 만료되어 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="09657-147">알림이 앱 내 알림인 경우 앱 사용자가 앱을 열 때에만 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09657-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="09657-148">앱 사용자가 앱을 열지 않은 경우 SDK는 알림은 전송되었지만 앱이 열릴 때까지 표시되지 않은 것으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="09657-149">알림이 앱 내 알림이고 특정 활동/화면에 표시되도록 구성한 경우 알림은 전송되었지만 사용자가 특정 화면에서 앱을 열 때까지 전송되지 않은 것으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="09657-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="09657-150">**사용자 상호 작용** - 앱 사용자가 상호 작용하는 메시지의 수를 지정하고 작동하거나 종료되는 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="09657-151">*앱 사용자는 다음 방법 중 하나로 알림 작업을 수행할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="09657-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="09657-152">알림이 시스템/앱 알림이거나 앱 내 알림이 알림 전용으로 전송되면 앱 사용자는 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="09657-153">알림이 텍스트 또는 웹 보기나 설문 조사가 있는 앱 내 알림인 경우 앱 사용자는 알림에서 실행 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="09657-154">알림이 웹 보기가 있는 앱 내 알림인 경우 앱 사용자는 웹 보기 [Android 전용]에서 URL을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="09657-155">*앱 사용자는 다음 방법 중 하나로 알림을 끝낼 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="09657-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="09657-156">알림에서 직접 닫기 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="09657-157">알림을 바로 넘기거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="09657-158">텍스트/웹 콘텐츠 및 설문 조사를 사용한 앱 내 알림은 일반적으로 두 단계 프로세스에서 앱 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09657-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="09657-159">알림이 먼저 표시되고 클릭하면 후속 텍스트/웹/설문 조사 콘텐츠가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09657-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="09657-160">앱 사용자는 이러한 단계 중 하나를 종료할 수 있고 고급 보기에서 세부 정보가 이를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="09657-161">**작업이 수행됨** - 앱 사용자가 명시적으로 수행했던 메시지 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="09657-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="09657-162">얼마나 많은 앱 사용자가 알림에서 푸시한 메시지에 흥미를 갖는지를 알려주는 흥미로운 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="09657-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="09657-163">iOS 및 Windows 플랫폼에서 사용자가 앱을 열고 캠페인이 "시간 지정하지 않은" 캠페인이었다면 앱 알림 및 앱 내 알림은 모두 동시에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="09657-164">표시됨 수가 전송됨 수 보다 높아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="09657-165">사용자가 알림과 상호 작용하거나 작업하는 경우 사용자 상호 작용/작업함 수는 전송됨 보다 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09657-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="09657-167">참고 항목</span><span class="sxs-lookup"><span data-stu-id="09657-167">See also</span></span>
* <span data-ttu-id="09657-168">[개념][Link 6]</span><span class="sxs-lookup"><span data-stu-id="09657-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="09657-169">[문제 해결 가이드 서비스][Link 24]</span><span class="sxs-lookup"><span data-stu-id="09657-169">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

