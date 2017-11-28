---
title: "Windows 유니버설 앱 SDK 콘텐츠"
description: "Azure Mobile Engagement용 Windows 유니버설 앱 SDK의 콘텐츠에 대해 알아봅니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="bfbb5-103">Windows 유니버설 앱 SDK 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="bfbb5-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="bfbb5-104">이 문서는 응용 프로그램에서 SDK가 배포한 콘텐츠를 나열하고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="bfbb5-105">`/Resources` 폴더</span><span class="sxs-lookup"><span data-stu-id="bfbb5-105">The `/Resources` folder</span></span>
<span data-ttu-id="bfbb5-106">이 폴더에는 Mobile Engagement에 필요한 모든 리소스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="bfbb5-107">앱에 맞게 리소스를 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="bfbb5-108">`EngagementConfiguration.xml` : Mobile Engagement 구성 파일입니다. 여기에서 Mobile Engagement 설정을 사용자 지정할 수 있습니다(Mobile Engagement 연결 문자열, 충돌 보고서...).</span><span class="sxs-lookup"><span data-stu-id="bfbb5-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="bfbb5-109">/html 폴더</span><span class="sxs-lookup"><span data-stu-id="bfbb5-109">/html folder</span></span>
* <span data-ttu-id="bfbb5-110">`EngagementNotification.html` : 앱 내 배너에 대한 `Notification` 웹 보기 HTML 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="bfbb5-111">`EngagementAnnouncement.html` : 앱 내 중간 보기에 대한 `Announcement` 웹 보기 HTML 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="bfbb5-112">/images 폴더</span><span class="sxs-lookup"><span data-stu-id="bfbb5-112">/images folder</span></span>
* <span data-ttu-id="bfbb5-113">`EngagementIconNotification.png` : 알림 왼쪽에 표시되는 브랜드 아이콘이며, 이것을 브랜드 아이콘으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="bfbb5-114">`EngagementIconOk.png` : 도달률 콘텐츠 페이지의 작업 또는 유효성 검사 단추용 `Ok` 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="bfbb5-115">`EngagementIconNOK.png` : 도달률 콘텐츠 페이지의 유효성 검사 단추를 사용하지 않도록 설정하면 `NOK` 아이콘이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="bfbb5-116">`EngagementIconClose.png` : 해제 단추에 대한 도달률 알림 및 콘텐츠용 `Close` 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="bfbb5-117">/overlay 폴더</span><span class="sxs-lookup"><span data-stu-id="bfbb5-117">/overlay folder</span></span>
* <span data-ttu-id="bfbb5-118">`EngagementPageOverlay.cs` : 오버레이 페이지는 자식에 Engagement 도달률 앱 내 UI를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbb5-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

