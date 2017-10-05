---
title: "Azure Mobile Engagement 사용자 인터페이스 - 모니터"
description: "Azure Mobile Engagement를 사용하여 응용 프로그램에 대한 실시간 데이터를 모니터링하는 방법 알아보기"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5f8a02e35db93585e0fe46d77b3ad18b94c99597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-monitor-real-time-data-about-your-application"></a><span data-ttu-id="e5d41-103">응용 프로그램에 대한 실시간 데이터를 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="e5d41-103">How to monitor real-time data about your application</span></span>
<span data-ttu-id="e5d41-104">이 문서에서는 **Mobile Engagement** 포털의 **모니터링** 탭을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-104">This article describes the **MONITOR** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="e5d41-105">**Mobile Engagement** 포털을 사용하여 모바일 앱을 모니터링하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="e5d41-106">포털 사용을 시작하려면 먼저 **Azure Mobile Engagement** 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> 

<span data-ttu-id="e5d41-107">UI의 모니터 섹션에서는 실시간 분석 정보를 제공하며, 이전부터 UI의 [분석](mobile-engagement-user-interface-analytics.md) 섹션에 있었던 거의 대부분의 정보에 대해 임계값에 도달하면 전송할 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-107">The Monitor section of the UI provides real-time analytics information and allows you to set alerts when thresholds are reached for most of the same information that is available historically in the [ANALYTICS](mobile-engagement-user-interface-analytics.md) section of the UI.</span></span> <span data-ttu-id="e5d41-108">분석 및 모니터링에서 사용되는 용어와 약어의 정의는 [개념](http://go.microsoft.com/fwlink/?LinkId=525555) 항목의 **용어집** 섹션을 참조하세요. 이러한 용어로는 활성 사용자, 새 사용자, 재방문 사용자, 세션, 사용자 경로 그래프, 사용자 맵, 추적 URL, 추세, 활동, 이벤트, 작업, 오류, 추가 정보, 작동 중단, 앱 정보 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-108">See the **Glossary** section in the [Concepts](http://go.microsoft.com/fwlink/?LinkId=525555) topic for definitions of terms and abbreviations in Analytics and Monitoring (such as the following: Active User, New user, Retained User, Session, User Path Graph, Users Map, Tracking URLs, Trends, Activity, Event, Job, Error, Extra Info, Crash, and App-info).</span></span>

> [!NOTE]
> <span data-ttu-id="e5d41-109">**Mobile Engagement** 포털 UI의 여러 섹션에는 **도움말 표시** 단추가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-109">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="e5d41-110">섹션에 대해 더 자세한 문맥 정보를 보려면 이 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-110">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a><span data-ttu-id="e5d41-111">모니터 - 세션, 작업, 이벤트, 오류 및 작동 중단</span><span class="sxs-lookup"><span data-stu-id="e5d41-111">Monitor - Sessions, Jobs, Events, Errors, and Crashes</span></span>
<span data-ttu-id="e5d41-112">현재 세션 및 특정 화면을 사용 중인 사용자나 특정 작업을 수행 중인 사용자의 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-112">You can see how many users are currently in session and on specific screens or doing specific actions.</span></span> <span data-ttu-id="e5d41-113">세션, 작업, 이벤트, 오류 및 작동 중단을 기준으로 구분된 사용자 활동을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-113">You can view user activity divided by Sessions, Jobs, Events, Errors, and Crashes.</span></span> <span data-ttu-id="e5d41-114">현재 정보를 보고 지난 1시간, 1일 또는 1주 동안의 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-114">You can see the current information and show the information from the last hour, day, or week.</span></span> <span data-ttu-id="e5d41-115">각 범주의 모든 정보를 볼 수도 있고 특정 세션/작업/이벤트/오류/작동 중단을 기준으로 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-115">You can see all of the information in each category or sort by the specific Session, Job, Event, Error, and Crash.</span></span>  <span data-ttu-id="e5d41-116">푸시 캠페인 등의 이벤트 중에 라이브 모니터링을 수행하면 푸시 알림을 보낸 직후에 작업이 다소 증가하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-116">Live monitoring is helpful to use during events such as a Push campaign to see if there is an uptick in action right after you send your Push notification.</span></span>

![Monitor1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a><span data-ttu-id="e5d41-118">모니터를 통해 문제 해결 - 이벤트 - 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e5d41-118">Troubleshooting with Monitor - Events - Details</span></span>
<span data-ttu-id="e5d41-119">테스트 장치의 응용 프로그램에서 이벤트를 생성한 다음 모니터 - 이벤트 - 세부 정보에서 해당 이벤트를 찾으면 매우 쉽게 테스트 장치의 장치 ID를 찾고 Azure Mobile Engagement와 통합된 분석, 모니터링 및 세그먼트가 응용 프로그램에서 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-119">Generating an event in your application from your test device and finding it in Monitor - Events - Details is one of the easiest ways to find your Device ID for your test device and to confirm that Azure Mobile Engagement integration of Analytics, Monitoring, and Segments is working from your application.</span></span> <span data-ttu-id="e5d41-120">테스트 장치의 장치 ID를 찾은 후에는 "내 계정 - 장치"에서 테스트 장치에 해당 ID를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-120">Once you have the Device ID of your test device, you can add it to your test devices in “My Account - Devices”.</span></span> <span data-ttu-id="e5d41-121">이벤트를 생성할 수 없는 경우 SDK가 설치된 Android/iOS/Web/Windows/Windows Phone 앱에 Azure Mobile Engagement가 올바르게 통합되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-121">If you can't generate an event, make sure that Azure Mobile Engagement is correctly integrated in your Android/iOS/Web/Windows/Windows Phone app with the SDK.</span></span>

<span data-ttu-id="e5d41-122">자세한 내용은 [SDK 설명서][Link 5]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5d41-122">For more information, see:  [SDK Documentation][Link 5]</span></span>

![Monitor2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a><span data-ttu-id="e5d41-124">모니터를 통해 문제 해결 - 작동 중단 - 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e5d41-124">Troubleshooting with Monitor - Crashes - Details</span></span>
<span data-ttu-id="e5d41-125">모니터 - 작동 중단 - 세부 정보에서 앱에 대한 작동 중단 정보를 검토하여 앱의 작동이 중단되는 이유를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-125">You can review crash information about your app from Monitor - Crashes - Details to help determine why your app is crashing.</span></span> <span data-ttu-id="e5d41-126">또한 Android/iOS/Web/Windows/Windows Phone용 각 SDK 버전의 릴리스 정보에서 각 SDK 버전의 알려진 문제를 찾아보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-126">You should also look up known issues with each version of the SDK in the release notes for each version of the SDK for Android/iOS/Web/Windows/Windows Phone.</span></span>

<span data-ttu-id="e5d41-127">자세한 내용은 [SDK 설명서 - 릴리스 정보][Link 5]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5d41-127">For more information, see:  [SDK Documentation - Release notes][Link 5]</span></span>

![Monitor3][16]

## <a name="monitor---alerts"></a><span data-ttu-id="e5d41-129">모니터 - 경고</span><span class="sxs-lookup"><span data-stu-id="e5d41-129">Monitor - Alerts</span></span>
<span data-ttu-id="e5d41-130">전자 메일 또는 인스턴트 메시지를 통해 자동으로 전송할 경고에 대한 조건을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-130">You can also specify conditions for Alerts that will be automatically sent to you via e-mail or instant message.</span></span> <span data-ttu-id="e5d41-131">Google의 GTalk, Apple의 iChat 등 XMPP 호환 서비스가 지원됩니다. 경고는 초/분/시간당 특정 세션, 작업, 이벤트, 오류 또는 작동 중단 수보다 크거나(>) 작은(<) 미리 정의된 검색 임계값을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-131">(Any XMPP-compliant services like Google's GTalk or Apple's iChat are supported.) Alerts are based on a pre-defined detection threshold greater than (>) or less than (<) a specific number of Sessions, Jobs, Events, Errors, or Crashes per second, minute, or hour.</span></span> <span data-ttu-id="e5d41-132">경고는 지정된 유형의 모든 활동을 모니터링할 수도 있고 특정 작업, 이벤트 또는 오류 활동만 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-132">Alerts can monitor all activities of a given type, or just monitor a specific Job, Event, or Error activity.</span></span> 

<span data-ttu-id="e5d41-133">경고 트리거 시 지정된 간격당 알림을 두 개 이상 받지 않도록 같은 경고에 대해 알림을 두 개로 구분하여 간격을 유지할 최소 시간(분)인 최소 검색 속도를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5d41-133">You can also specify a Minimum Detection Rate, which is the minimum amount of minutes that will separate two notifications for the same alert to make sure that when your alert is triggered, you will never receive more than 1 notification per interval specified.</span></span>

![Monitor4][17]

## <a name="see-also"></a><span data-ttu-id="e5d41-135">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e5d41-135">See also</span></span>
* <span data-ttu-id="e5d41-136">[개념][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e5d41-136">[Concepts][Link 6]</span></span>
* <span data-ttu-id="e5d41-137">[문제 해결 가이드 서비스][Link 24]</span><span class="sxs-lookup"><span data-stu-id="e5d41-137">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
