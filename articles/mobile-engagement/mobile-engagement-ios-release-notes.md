---
title: "aaaAzure Mobile Engagement iOS SDK 릴리스 정보 | Microsoft Docs"
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
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="f1807-103">Azure Mobile Engagement iOS SDK 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f1807-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="f1807-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="f1807-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="f1807-105">백그라운드에서 지워진 배지를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="f1807-106">기본 큐에서 호출되지 않는 API에 대한 XCode 9의 경고를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="f1807-107">도달률 설문에서 메모리 누수를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="f1807-108">iOS 6.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="f1807-109">적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 7입니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="f1807-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="f1807-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="f1807-111">백그라운드에서 로그 전달을 개선하였습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="f1807-112">4.0.0(09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="f1807-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="f1807-113">iOS 10 장치에서 알림이 작동하지 않는 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="f1807-114">XCode 7은 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="f1807-115">3.2.4(2016년 6월 30일)</span><span class="sxs-lookup"><span data-stu-id="f1807-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="f1807-116">기술 로그 및 기타 로그 간 집계를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="f1807-117">3.2.3(06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="f1807-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="f1807-118">고정된 hello 버그 hello 백그라운드에서 앱이 때 배달 피드백 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="f1807-119">최적화 된 hello 기술 로그의 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="f1807-120">3.2.2(2016/04/07)</span><span class="sxs-lookup"><span data-stu-id="f1807-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="f1807-121">수정 된 버그를 toocrash 때로는 크게 HTTP 요청 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="f1807-122">3.2.1(2015/12/11)</span><span class="sxs-lookup"><span data-stu-id="f1807-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="f1807-123">새 응용 프로그램 인스턴스 딥 링크와 알림이 트리거될 때 고정된 hello 지연</span><span class="sxs-lookup"><span data-stu-id="f1807-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="f1807-124">3.2.0(2015/10/08)</span><span class="sxs-lookup"><span data-stu-id="f1807-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="f1807-125">제대로 작동 하는 hello SDK toomake에서 Bitcode 활성화 **Xcode 7**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="f1807-126">수정 된 버그 관련 tooin 앱 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="f1807-127">앱에서 알림을 hello 배터리 부족 및 기타 이러한 시나리오의 경우 보다 안정적 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="f1807-128">타사 라이브러리에서 생성하는 추가 콘솔 로그를 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="f1807-129">3.1.0(08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="f1807-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="f1807-130">타사 라이브러리와 iOS 9 호환성 버그를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="f1807-131">설문 조사 결과, 응용 프로그램 정보 또는 추가 데이터를 보내는 동안 충돌을 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="f1807-132">3.0.0(2015/06/19)</span><span class="sxs-lookup"><span data-stu-id="f1807-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="f1807-133">Mobile Engagement는 자동 푸시 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="f1807-134">iOS 4.X에 대한 지원을 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="f1807-135">적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 6입니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="f1807-136">2.2.0(05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="f1807-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="f1807-137">장치에 대 한 hello Mobile Engagement 장치 id < iOS 6은 이제 설치 중에 생성 된 GUID를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="f1807-138">2.1.0(2015/04/24)</span><span class="sxs-lookup"><span data-stu-id="f1807-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="f1807-139">Swift 호환성을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="f1807-140">알림을 클릭할 때 URL이 이제 hello 동작 hello 응용 프로그램을 연 후 오른쪽을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="f1807-141">SDK 패키지에 누락된 헤더 파일을 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="f1807-142">Hello Mobile Engagement 크래시 보고서가 사용 되지 않을 때 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="f1807-143">2.0.0(2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="f1807-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="f1807-144">Azure Mobile Engagement의 최초 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="f1807-145">appId/sdkKey 구성이 연결 문자열 구성으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="f1807-146">API toosend를 제거 하 고 임의의 XMPP 엔터티에서 임의의 XMPP 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="f1807-147">API toosend를 제거 하 고 장치 간에 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="f1807-148">보안이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-148">Security improvements.</span></span>
* <span data-ttu-id="f1807-149">SmartAd 추적 기능이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1807-149">SmartAd tracking removed.</span></span>
