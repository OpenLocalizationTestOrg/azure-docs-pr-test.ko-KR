---
title: "Azure Mobile Engagement 사용자 인터페이스 - 설정"
description: "Azure Mobile Engagement를 사용하여 응용 프로그램의 전역 설정을 관리하는 방법 알아보기"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af5c81df2b9f288161b38625d3ac2adde8fb195d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-global-settings-of-your-application"></a><span data-ttu-id="fa6f4-103">응용 프로그램의 전역 설정을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="fa6f4-103">How to manage the global settings of your application</span></span>
<span data-ttu-id="fa6f4-104">응용 프로그램에서 제공하는 **설정** 메뉴 옵션은 응용 프로그램의 플랫폼과 응용 프로그램에 대해 부여한 권한에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-104">The **Settings** menu options available for an application vary, depending on the platform of the application and the permissions you have been granted for the application.</span></span> <span data-ttu-id="fa6f4-105">설정에는 세부 정보, 프로젝트, 네이티브 푸시, 푸시 속도, 태그(앱 정보) 및 상업적 압력 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-105">Settings include the following: Details, Projects, Native Push, Push Speed, Tag (app info), and Commercial Pressure.</span></span> <span data-ttu-id="fa6f4-106">설정 섹션의 태그(앱 정보) 메뉴 옵션은 응용 프로그램(SDK 사용) 또는 백 엔드(장치 API 사용)에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-106">The Tag (app info) menu option of the Settings section can be managed by your application (using the SDK) or by your backend (using the Device API).</span></span> 

> [!NOTE]
> <span data-ttu-id="fa6f4-107">**Mobile Engagement** 포털 UI의 여러 섹션에는 **도움말 표시** 단추가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-107">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="fa6f4-108">섹션에 대해 더 자세한 문맥 정보를 보려면 이 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-108">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="details"></a><span data-ttu-id="fa6f4-109">세부 정보</span><span class="sxs-lookup"><span data-stu-id="fa6f4-109">Details</span></span>
<span data-ttu-id="fa6f4-110">응용 프로그램의 이름과 설명을 변경하고 응용 프로그램 소유자와 역할 권한을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-110">Allows you to change the name and description of your application, view the owner of your application and your role permissions.</span></span> 

<span data-ttu-id="fa6f4-111">분석 구성에서는 주의 시작 요일과 보존 기간을 확인하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-111">Analytics configuration enables  you to view or change the day weeks start on and the retention time in day(s).</span></span>

  ![settings1][46]

## <a name="projects"></a><span data-ttu-id="fa6f4-113">프로젝트</span><span class="sxs-lookup"><span data-stu-id="fa6f4-113">Projects</span></span>
<span data-ttu-id="fa6f4-114">응용 프로그램을 표시할 모든 프로젝트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-114">Allows you to select all projects you want your application to appear in.</span></span> 

<span data-ttu-id="fa6f4-115">또한 프로젝트를 검색하고 응용 프로그램이 속한 프로젝트의 이름, 설명, 소유자, 역할 권한을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-115">You can also search for a project and view the name, description, owner and your role permissions of any project your application is part of.</span></span>

<span data-ttu-id="fa6f4-116">자세한 내용은 [UI 설명서 - 홈][Link 13]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-116">For more information, see: [UI Documentation – Home][Link 13]</span></span>

  ![settings3][48]

## <a name="native-push"></a><span data-ttu-id="fa6f4-118">네이티브 푸시</span><span class="sxs-lookup"><span data-stu-id="fa6f4-118">Native Push</span></span>
<span data-ttu-id="fa6f4-119">네이티브 푸시에 사용할 새 인증서를 등록하거나 기존 인증서를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-119">Allows you to register a new certificate or delete and existing certificate for use with native push.</span></span> <span data-ttu-id="fa6f4-120">Azure Mobile Engagement에서는 네이티브 푸시를 통해 응용 프로그램이 실행 중이지 않을 때라도 언제든지 응용 프로그램에 푸시를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-120">Native Push enables Azure Mobile Engagement to push to your application at any time, even when it is not running.</span></span> 

<span data-ttu-id="fa6f4-121">하나 이상의 네이티브 푸시 서비스에 대해 자격 증명이나 인증서를 제공한 후에는 도달률 캠페인을 만들 때 "항상"을 선택할 수 있으며 푸시 API에서 "알림 구성 요소" 매개 변수도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-121">After providing credentials or certificates for at least one Native Push service, you can select "Any time" when creating Reach Campaigns, and also use the "notifier" parameter in the PUSH API.</span></span>

### <a name="apple-push-notification-service-apns"></a><span data-ttu-id="fa6f4-122">APNS(Apple 푸시 알림 서비스)</span><span class="sxs-lookup"><span data-stu-id="fa6f4-122">Apple Push Notification Service (APNS)</span></span>
<span data-ttu-id="fa6f4-123">Apple 푸시 알림 서비스를 사용하여 네이티브 푸시를 사용하도록 설정하려면 인증서를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-123">To enable Native Push using the Apple Push Notification Service you will need to register your certificate.</span></span> <span data-ttu-id="fa6f4-124">인증서 유형은 개발(DEV) 또는 프로덕션(PROD)으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-124">You will need to specify the type of certificate as either development (DEV) or production (PROD).</span></span> <span data-ttu-id="fa6f4-125">그런 후에 인증서와 암호를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-125">Then you will need upload your certificate and the password.</span></span>

<span data-ttu-id="fa6f4-126">자세한 내용은 [SDK 설명서 - iOS - Apple 푸시 알림을 받도록 응용 프로그램을 준비하는 방법][Link 5]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-126">For more information, see: [SDK Documentation - iOS - How to Prepare your Application for Apple Push notifications][Link 5]</span></span>

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a><span data-ttu-id="fa6f4-128">WPNS(Windows 푸시 알림 서비스)</span><span class="sxs-lookup"><span data-stu-id="fa6f4-128">Windows Push Notification Service (WPNS)</span></span>
<span data-ttu-id="fa6f4-129">Windows 알림 서비스를 사용하여 네이티브 푸시를 사용하도록 설정하려면 응용 프로그램의 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-129">To enable Native Push using Windows Notification Service, you must provide your application's credentials.</span></span> <span data-ttu-id="fa6f4-130">이렇게 하려면 패키지 SID(보안 식별자)와 비밀 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-130">You will need your Package security identifier (SID) and your Secret key.</span></span>

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a><span data-ttu-id="fa6f4-132">Google Cloud Messaging for Android(GCM)</span><span class="sxs-lookup"><span data-stu-id="fa6f4-132">Google Cloud Messaging for Android (GCM)</span></span>
<span data-ttu-id="fa6f4-133">GCM을 사용하여 네이티브 푸시를 사용하도록 설정하려면 Google의 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-133">To enable Native Push using GCM, you need to follow the instructions from Google.</span></span> <span data-ttu-id="fa6f4-134">그런 후에 IP 제한 없이 구성된 서버의 단순 API 키를 붙여 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-134">Then you must paste a server simple API key, configured without IP restrictions.</span></span> <span data-ttu-id="fa6f4-135">이렇게 하려면 Android v1.12.0 이상 버전용 SDK를 통합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-135">Requires integration with the SDK for Android v1.12.0+.</span></span>

<span data-ttu-id="fa6f4-136">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-136">For more information, see:</span></span> 

* <span data-ttu-id="fa6f4-137">[SDK 설명서 Android GCM을 통합하는 방법][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fa6f4-137">[SDK Documentation Android How to Integrate GCM][Link 5]</span></span>
* [<span data-ttu-id="fa6f4-138">Google 개발자 GCM 가이드</span><span class="sxs-lookup"><span data-stu-id="fa6f4-138">Google Developer GCM Guide</span></span>](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a><span data-ttu-id="fa6f4-139">Amazon Device Messaging for Android(ADM)</span><span class="sxs-lookup"><span data-stu-id="fa6f4-139">Amazon Device Messaging for Android (ADM)</span></span>
<span data-ttu-id="fa6f4-140">ADM을 사용하여 네이티브 푸시를 사용하도록 설정하려면 클라이언트 ID와 클라이언트 암호로 구성된 Amazon <OAuth credentials>을(를) 제공해야 합니다. 이렇게 하려면 Android v2.1.0 이상 버전용 SDK를 통합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-140">To enable Native Push using ADM, you must provide Amazon <OAuth credentials> consisting of a Client ID and Client Secret (Requires integration with SDK for Android v2.1.0+).</span></span>

<span data-ttu-id="fa6f4-141">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-141">For more information, see:</span></span> 

* <span data-ttu-id="fa6f4-142">[SDK 설명서 Android ADM을 통합하는 방법][Link 5]</span><span class="sxs-lookup"><span data-stu-id="fa6f4-142">[SDK Documentation Android How to Integrate ADM][Link 5]</span></span>
* [<span data-ttu-id="fa6f4-143">Amazon 개발자 ADM 설명서</span><span class="sxs-lookup"><span data-stu-id="fa6f4-143">Amazon Developer ADM Documentation</span></span>](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a><span data-ttu-id="fa6f4-145">푸시 속도</span><span class="sxs-lookup"><span data-stu-id="fa6f4-145">Push Speed</span></span>
<span data-ttu-id="fa6f4-146">응용 프로그램의 현재 푸시 속도가 표시되며 원하는 푸시 속도를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa6f4-146">Shows the current push speed of your application and allows you to define the push speed of your application.</span></span>

  ![settings7][52]

## <a name="tag-app-info"></a><span data-ttu-id="fa6f4-148">태그(앱 정보)</span><span class="sxs-lookup"><span data-stu-id="fa6f4-148">Tag (app info)</span></span>
![settings11][56]

## <a name="commercial-pressure"></a><span data-ttu-id="fa6f4-150">상업적 압력</span><span class="sxs-lookup"><span data-stu-id="fa6f4-150">Commercial Pressure</span></span>
![settings12][57]

## <a name="see-also"></a><span data-ttu-id="fa6f4-152">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fa6f4-152">See also</span></span>
* <span data-ttu-id="fa6f4-153">[개념][Link 6]</span><span class="sxs-lookup"><span data-stu-id="fa6f4-153">[Concepts][Link 6]</span></span>
* <span data-ttu-id="fa6f4-154">[문제 해결 가이드 서비스][Link 24]</span><span class="sxs-lookup"><span data-stu-id="fa6f4-154">[Troubleshooting Guide Service][Link 24]</span></span>

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

