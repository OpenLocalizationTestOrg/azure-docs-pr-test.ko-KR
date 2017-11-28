---
title: "Azure Mobile Engagement iOS SDK 릴리스 정보 | Microsoft Docs"
description: "Azure Mobile Engagement용 iOS SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 9bdaa57f9902373ccf796ff109332b64c66bf9e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="040e2-103">Azure Mobile Engagement iOS SDK 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="040e2-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="040e2-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="040e2-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="040e2-105">백그라운드에서 지워진 배지를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="040e2-106">기본 큐에서 호출되지 않는 API에 대한 XCode 9의 경고를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="040e2-107">도달률 설문에서 메모리 누수를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="040e2-108">iOS 6.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="040e2-109">이 버전부터 응용 프로그램의 배포 대상은 iOS 7 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-109">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="040e2-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="040e2-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="040e2-111">백그라운드에서 로그 전달을 개선하였습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="040e2-112">4.0.0(09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="040e2-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="040e2-113">iOS 10 장치에서 알림이 작동하지 않는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="040e2-114">XCode 7은 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="040e2-115">3.2.4(2016년 6월 30일)</span><span class="sxs-lookup"><span data-stu-id="040e2-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="040e2-116">기술 로그 및 기타 로그 간 집계를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="040e2-117">3.2.3(06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="040e2-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="040e2-118">앱이 백그라운드에 있을 때 전달 피드백이 보고되지 않는 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-118">Fixed the bug where delivery feedback is not reported when app is in the background.</span></span>
* <span data-ttu-id="040e2-119">기술 로그의 전송이 최적화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-119">Optimized the sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="040e2-120">3.2.2(2016/04/07)</span><span class="sxs-lookup"><span data-stu-id="040e2-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="040e2-121">경우에 따라 충돌을 일으킬 수 있는 HTTP 요청 취소에 대한 버그가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-121">Fixed bug on HTTP request cancellation which sometimes leads to crash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="040e2-122">3.2.1(2015/12/11)</span><span class="sxs-lookup"><span data-stu-id="040e2-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="040e2-123">딥 링크를 사용하는 알림에서 새 앱 인스턴스를 트리거할 때의 지연을 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-123">Fixed the delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="040e2-124">3.2.0(2015/10/08)</span><span class="sxs-lookup"><span data-stu-id="040e2-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="040e2-125">**Xcode 7**과 연동되도록 SDK의 Bitcode를 활성화했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-125">Enabled Bitcode in the SDK to make it work with **Xcode 7**.</span></span>
* <span data-ttu-id="040e2-126">앱 내 알림 메시지와 관련된 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-126">Fixed bugs related to in-app notifications.</span></span>
* <span data-ttu-id="040e2-127">배터리가 부족한 경우 및 기타 이러한 시나리오에서 앱 내 알림 메시지를 더욱 안정적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-127">Made the in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="040e2-128">타사 라이브러리에서 생성하는 추가 콘솔 로그를 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="040e2-129">3.1.0(08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="040e2-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="040e2-130">타사 라이브러리와 iOS 9 호환성 버그를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="040e2-131">설문 조사 결과, 응용 프로그램 정보 또는 추가 데이터를 보내는 동안 충돌을 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="040e2-132">3.0.0(2015/06/19)</span><span class="sxs-lookup"><span data-stu-id="040e2-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="040e2-133">Mobile Engagement는 자동 푸시 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="040e2-134">iOS 4.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="040e2-135">이 버전부터 응용 프로그램의 배포 대상은 iOS 6 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-135">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="040e2-136">2.2.0(05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="040e2-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="040e2-137">iOS 6 이전 장치에 대한 Mobile Engagement 장치 ID는 설치 시 생성된 GUID를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-137">The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="040e2-138">2.1.0(2015/04/24)</span><span class="sxs-lookup"><span data-stu-id="040e2-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="040e2-139">Swift 호환성을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="040e2-140">알림을 클릭하면 이제 응용 프로그램을 연 직후에 작업 URL이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-140">When clicking on a notification, the action URL is now executed right after the application is opened.</span></span>
* <span data-ttu-id="040e2-141">SDK 패키지에 누락된 헤더 파일을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="040e2-142">모바일 고객 관리 크래시 리포터를 사용할 수 없는 문제를 해결하였습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-142">Fixed an issue when the Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="040e2-143">2.0.0(2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="040e2-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="040e2-144">Azure Mobile Engagement의 최초 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="040e2-145">appId/sdkKey 구성이 연결 문자열 구성으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="040e2-146">임의의 XMPP 엔터티에서 임의의 XMPP 메시지를 보내고 받기 위한 API가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-146">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="040e2-147">장치 간에 메시지를 보내고 받기 위한 API가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-147">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="040e2-148">보안이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-148">Security improvements.</span></span>
* <span data-ttu-id="040e2-149">SmartAd 추적 기능이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="040e2-149">SmartAd tracking removed.</span></span>
