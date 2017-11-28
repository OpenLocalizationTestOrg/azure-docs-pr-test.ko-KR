---
title: "Azure Mobile Engagement Android SDK 통합"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="a4038-103">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="a4038-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="a4038-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="a4038-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="a4038-105">`EngagementApplication` 클래스에서도 `EngagementAgentUtils.isInDedicatedEngagementProcess`를 호출할 때 드물게 발생할 수 있는 충돌을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="a4038-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="a4038-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="a4038-107">Android 8 지원(이전 버전의 SDK는 Android 8에서 작동하지 않음)</span><span class="sxs-lookup"><span data-stu-id="a4038-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="a4038-108">지원 라이브러리에 대한 종속성이 더 이상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-108">No more dependency on support library.</span></span>
* <span data-ttu-id="a4038-109">`EngagementFragmentActivity` 클래스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="a4038-110">Android 8의 [백그라운드 실행 제한](https://developer.android.com/preview/features/background.html)으로 인해 사용자가 장치를 조작할 때까지 백그라운드의 로그가 지연될 수 있습니다. 장치가 절전 모드인 경우 이로 인해 푸시 캠페인 **배달됨** 및 **시스템 알림 표시됨** 통계가 지연될 수 있습니다(알림은 계속 표시되며, 문제없이 실시간으로 울리고 진동함).</span><span class="sxs-lookup"><span data-stu-id="a4038-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="a4038-111">[백그라운드 위치 제한](https://developer.android.com/preview/features/background-location-limits.html)으로 인해 Android 8에서는 백그라운드의 실시간 위치가 자주 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="a4038-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="a4038-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="a4038-113">Android 7의 앱 내 알림 텍스트 색을 이전 Android 버전과 동일하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="a4038-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="a4038-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="a4038-115">더 이상 WIFI 잠금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-115">No more WIFI lock.</span></span>
* <span data-ttu-id="a4038-116">Init 이전에 getDeviceId를 호출할 경우 교착 상태를 해결합니다.(4.2.0에 유입된 버그)</span><span class="sxs-lookup"><span data-stu-id="a4038-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="a4038-117">4.2.2(2016/05/17)</span><span class="sxs-lookup"><span data-stu-id="a4038-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="a4038-118">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="a4038-119">4.2.1(2016/05/10)</span><span class="sxs-lookup"><span data-stu-id="a4038-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="a4038-120">보안: 웹 보기 로컬 파일 액세스를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="a4038-121">보안: 사용되지 않고 보호되지 않는 `PreferenceActivity` 클래스를 확장하는 `EngagementPreferenceActivity` 클래스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="a4038-122">보안: 도달률 활동에서 현재 `exported="false"`을(를) 사용하도록 문서화되어 있으며 이 플래그는 이전 SDK 버전에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="a4038-123">4.2.0(2016/03/11)</span><span class="sxs-lookup"><span data-stu-id="a4038-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="a4038-124">SDK는 이제 MIT에 따라 사용이 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="a4038-125">SDK 초기화 시에 사용자 지정 장치 식별자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="a4038-126">4.1.5(2016/02/01)</span><span class="sxs-lookup"><span data-stu-id="a4038-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="a4038-127">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="a4038-128">4.1.4(2016/01/26)</span><span class="sxs-lookup"><span data-stu-id="a4038-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="a4038-129">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="a4038-130">4.1.3(2015/12/9)</span><span class="sxs-lookup"><span data-stu-id="a4038-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="a4038-131">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="a4038-132">4.1.2(2015/11/25)</span><span class="sxs-lookup"><span data-stu-id="a4038-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="a4038-133">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="a4038-134">4.1.1(2015/11/04)</span><span class="sxs-lookup"><span data-stu-id="a4038-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="a4038-135">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="a4038-136">4.1.0(08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="a4038-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="a4038-137">Android M에 대한 새 권한 모델을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="a4038-138">`AndroidManifest.xml`을 사용하는 대신 이제 런타임 시 위치 기능을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="a4038-139">사용 권한 버그 수정: `ACCESS_FINE_LOCATION`을 사용하는 경우 `ACCESS_COARSE_LOCATION`이 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="a4038-140">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="a4038-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="a4038-141">4.0.0(07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="a4038-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="a4038-142">내부 프로토콜이 분석을 수행하고 더 안정적으로 푸시하도록 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="a4038-143">네이티브 푸시(GCM/ADM)가 이제 앱 알림에도 사용되므로 모든 푸시 캠페인 유형에 대한 네이티브 푸시 자격 증명을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="a4038-144">큰 그림 알림을 수정합니다. 푸시된 후 10초만 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="a4038-145">웹 보기에서 버그 수정: 링크를 클릭하면 기본 작업 URL도 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="a4038-146">로컬 저장소 관리와 관련된 드문 충돌을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="a4038-147">동적 구성 문자열 관리를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="a4038-148">EULA를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="a4038-149">3.0.0(2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="a4038-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="a4038-150">Azure Mobile Engagement의 최초 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="a4038-151">appId 구성이 연결 문자열 구성으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="a4038-152">임의의 XMPP 엔터티에서 임의의 XMPP 메시지를 보내고 받기 위한 API가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="a4038-153">장치 간에 메시지를 보내고 받기 위한 API가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="a4038-154">보안이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-154">Security improvements.</span></span>
* <span data-ttu-id="a4038-155">Google Play 및 SmartAd 추적을 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4038-155">Google Play and SmartAd tracking removed.</span></span>

