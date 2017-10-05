---
title: "Azure Mobile Engagement용 Android SDK 통합"
description: "Android 앱에서 Azure Mobile Engagement SDK를 통합하는 방법에 대해 설명합니다"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="95ee4-103">Azure Mobile Engagement용 Android SDK 통합</span><span class="sxs-lookup"><span data-stu-id="95ee4-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95ee4-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="95ee4-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="95ee4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="95ee4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="95ee4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="95ee4-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="95ee4-107">Android</span><span class="sxs-lookup"><span data-stu-id="95ee4-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="95ee4-108">이 문서는 Azure Mobile Engagement Android SDK에 사용 가능한 모든 통합 및 구성 옵션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="95ee4-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95ee4-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95ee4-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="95ee4-110">고급 기능</span><span class="sxs-lookup"><span data-stu-id="95ee4-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="95ee4-111">보고 기능</span><span class="sxs-lookup"><span data-stu-id="95ee4-111">Reporting Features</span></span>
<span data-ttu-id="95ee4-112">이러한 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95ee4-112">You can add these features:</span></span>

1. [<span data-ttu-id="95ee4-113">고급 보고 옵션</span><span class="sxs-lookup"><span data-stu-id="95ee4-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="95ee4-114">위치 보고 옵션</span><span class="sxs-lookup"><span data-stu-id="95ee4-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="95ee4-115">고급 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="95ee4-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="95ee4-116">알림:</span><span class="sxs-lookup"><span data-stu-id="95ee4-116">Notifications:</span></span>
[<span data-ttu-id="95ee4-117">Android 앱에서 도달률(알림)을 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="95ee4-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="95ee4-118">Google Cloud Messaging (GCM): [GCM과 Mobile Engagement를 통합하는 방법](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="95ee4-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="95ee4-119">Amazon Device Messaging (ADM): [ADM과 Mobile Engagement를 통합하는 방법](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="95ee4-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="95ee4-120">태그 계획 구현:</span><span class="sxs-lookup"><span data-stu-id="95ee4-120">Tag plan implementation:</span></span>
[<span data-ttu-id="95ee4-121">Android 앱에서 고급 Mobile Engagement API 태깅을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="95ee4-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="95ee4-122">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="95ee4-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="95ee4-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="95ee4-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="95ee4-124">`EngagementApplication` 클래스에서도 `EngagementAgentUtils.isInDedicatedEngagementProcess`를 호출할 때 드물게 발생할 수 있는 충돌을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="95ee4-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="95ee4-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="95ee4-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="95ee4-126">Android 8 지원(이전 버전의 SDK는 Android 8에서 작동하지 않음)</span><span class="sxs-lookup"><span data-stu-id="95ee4-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="95ee4-127">지원 라이브러리에 대한 종속성이 더 이상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95ee4-127">No more dependency on support library.</span></span>
* <span data-ttu-id="95ee4-128">`EngagementFragmentActivity` 클래스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="95ee4-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="95ee4-129">Android 8의 [백그라운드 실행 제한](https://developer.android.com/preview/features/background.html)으로 인해 사용자가 장치를 조작할 때까지 백그라운드의 로그가 지연될 수 있습니다. 장치가 절전 모드인 경우 이로 인해 푸시 캠페인 **배달됨** 및 **시스템 알림 표시됨** 통계가 지연될 수 있습니다(알림은 계속 표시되며, 문제없이 실시간으로 울리고 진동함).</span><span class="sxs-lookup"><span data-stu-id="95ee4-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="95ee4-130">[백그라운드 위치 제한](https://developer.android.com/preview/features/background-location-limits.html)으로 인해 Android 8에서는 백그라운드의 실시간 위치가 자주 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95ee4-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="95ee4-131">모든 버전에 대한 내용은 [전체 릴리스 정보](mobile-engagement-android-release-notes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95ee4-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="95ee4-132">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="95ee4-132">Upgrade procedures</span></span>
<span data-ttu-id="95ee4-133">이전 버전의 SDK를 응용 프로그램에 이미 통합한 경우에는 [업그레이드 절차](mobile-engagement-android-upgrade-procedure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95ee4-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

