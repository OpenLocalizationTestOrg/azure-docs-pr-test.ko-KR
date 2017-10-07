---
title: "aaaAzure Mobile Engagement 문제 해결 가이드-SDK"
description: "Azure Mobile Engagement에서 SDK 통합 문제 해결"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="e2165-103">SDK 통합 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="e2165-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="e2165-104">hello 다음은 Azure Mobile Engagement 응용 프로그램에 통합 하는 방법에 발생할 수 있는 관련 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="e2165-105">응용 프로그램의 다른 영역에서 발생한 오류를 통해 검색된 SDK 문제</span><span class="sxs-lookup"><span data-stu-id="e2165-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="e2165-106">문제</span><span class="sxs-lookup"><span data-stu-id="e2165-106">Issue</span></span>
* <span data-ttu-id="e2165-107">분석, 모니터링, 구분 또는 대시보드의 UI 데이터 수집 오류</span><span class="sxs-lookup"><span data-stu-id="e2165-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="e2165-108">푸시 오류(푸시가 앱 내부 또는 외부나 두 위치에서 모두 작동하지 않음)</span><span class="sxs-lookup"><span data-stu-id="e2165-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="e2165-109">고급 기능 오류(추적, 지리적 위치 또는 플랫폼별 푸시 미작동)</span><span class="sxs-lookup"><span data-stu-id="e2165-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="e2165-110">API 오류(API에서 자동 오류가 자주 발생하며 오류 메시지가 표시되지 않음)</span><span class="sxs-lookup"><span data-stu-id="e2165-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="e2165-111">서비스 오류(Azure Mobile Engagement 기능이 응용 프로그램에서 작동하지 않음)</span><span class="sxs-lookup"><span data-stu-id="e2165-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="e2165-112">원인</span><span class="sxs-lookup"><span data-stu-id="e2165-112">Causes</span></span>
* <span data-ttu-id="e2165-113">오류 (예: 한 UI 데이터 컬렉션 오류, 푸시 오류, 고급 기능 실패, API 오류, 응용 프로그램 충돌 또는 명백한 서비스 응용 프로그램에 의해 검색 됩니다 toobe hello Azure Mobile Engagement SDK로 해결 해야 하는 대부분의 문제 작동 중단)입니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="e2165-114">Azure Mobile Engagement의 특정 기능은 하기 전에 응용 프로그램에서 작동 하지 않았습니다, toocomplete hello 통합을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="e2165-115">Azure Mobile Engagement의 특정 기능은 작동 중지 있다면 hello Azure Mobile Engagement SDK로 tooupgrade toohello 마지막 버전을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="e2165-116">다른 버전의 Azure Mobile Engagement (Android, iOS, Windows 및 Windows Phone)에서 지 원하는 각 플랫폼에 대 한 Azure Mobile Engagement SDK hello 임을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="e2165-117">SDK 통합</span><span class="sxs-lookup"><span data-stu-id="e2165-117">SDK Integration</span></span>
* <span data-ttu-id="e2165-118">Azure Mobile Engagement가 SDK에 올바르게 통합되지 않았습니다(분석).</span><span class="sxs-lookup"><span data-stu-id="e2165-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="e2165-119">도달률이 SDK에 올바르게 통합되지 않았습니다(앱 내 푸시/앱 외부 푸시).</span><span class="sxs-lookup"><span data-stu-id="e2165-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="e2165-120">인증서가 만료되었거나 프로덕션/개발 버전이 잘못되었습니다(iOS에만 해당).</span><span class="sxs-lookup"><span data-stu-id="e2165-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="e2165-121">GCM 또는 ADM이 SDK에 올바르게 통합되지 않았습니다(Android에만 해당 - 서비스별 푸시).</span><span class="sxs-lookup"><span data-stu-id="e2165-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="e2165-122">추적이 SDK에 올바르게 통합되지 않았습니다(설치 스토어 추적).</span><span class="sxs-lookup"><span data-stu-id="e2165-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="e2165-123">지연 위치 또는 GPS 위치가 SDK에 올바르게 통합되지 않았습니다(지리적 위치 기준 대상 지정).</span><span class="sxs-lookup"><span data-stu-id="e2165-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="e2165-124">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="e2165-124">**See also:**</span></span>

* <span data-ttu-id="e2165-125">[SDK 설명서 - 통합 가이드][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e2165-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="e2165-126">[문제 해결 가이드 - 푸시][Link 23]</span><span class="sxs-lookup"><span data-stu-id="e2165-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="e2165-127">SDK 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e2165-127">SDK Upgrade</span></span>
* <span data-ttu-id="e2165-128">이전 버전의 SDK (대개 관련된 toonewer 버전의 hello 장치 OS) hello로 tooupgrade SDK tooresolve 문제 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="e2165-129">장치에서 앱의 모든 이전 버전을 제거 하 고 hello 최신 버전의 응용 프로그램을 다시 설치, hello hello Azure Mobile Engagement UI tooconfirm 장치 응용 프로그램의 최신 버전 hello를 사용 하 고 있는지에서 장치 ID를 다시 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="e2165-130">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="e2165-130">**See also:**</span></span>

* [<span data-ttu-id="e2165-131">SDK 설명서 - 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="e2165-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="e2165-132">SDK 설명서 - 업그레이드 가이드</span><span class="sxs-lookup"><span data-stu-id="e2165-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="e2165-133">기타 SDK 관련 문제</span><span class="sxs-lookup"><span data-stu-id="e2165-133">SDK Other</span></span>
* <span data-ttu-id="e2165-134">Azure Mobile Engagement 하면이 응용 프로그램 매니페스트 "AndroidManifest.xml"에 오류 toowork (Android에만 해당) 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="e2165-135">SDK 통합 및 API 사용 된 일반적인 문제는 tooconfuse hello SDK 키 및 hello API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="e2165-136">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="e2165-136">**See also:**</span></span>

* <span data-ttu-id="e2165-137">[개념 - 용어집][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e2165-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="e2165-138">고급 코딩 문제</span><span class="sxs-lookup"><span data-stu-id="e2165-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="e2165-139">문제</span><span class="sxs-lookup"><span data-stu-id="e2165-139">Issue</span></span>
* <span data-ttu-id="e2165-140">플랫폼별 코드 직접 관련 되지 않은 tooAzure Mobile Engagement iOS, Android 및 Windows Phone 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="e2165-141">원인</span><span class="sxs-lookup"><span data-stu-id="e2165-141">Causes</span></span>
* <span data-ttu-id="e2165-142">Azure Mobile Engagement와 관련 된 코딩 문제를 고급 대부분의 일반적인 원인은 잘못 작성 된 플랫폼에 따라 특정 코드 직접 관련 되지 않은 tooAzure Mobile Engagement 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="e2165-143">Tooconsult 설명서 특정 toohello 플랫폼을 개발 하는 대 한 또한 tooAzure Mobile Engagement 설명서 (Android, iOS, 웹, Windows 및 Windows Phone) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="e2165-144">또한 "categories"를 잘못 구성 내부 또는 외부 hello 앱 (Android에만 해당)의 알림 tooanother 위치에서 연결 하는 것을 금지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="e2165-145">설정 하지 않으면 "UIKit.framework" iOS 코드를 보여 주는 "기호를 찾을 수 없음 오류"에서 "optional" 너무 오래 된 iOS 장치 (iOS에만 해당)에서 충돌 및/또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="e2165-146">만료 된 인증서 또는 hello 개발자 또는 Prod 버전의 hello 인증서를 사용 하 여 올바르게 하지, 원인 밀어넣기 (iOS에만 해당)을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="e2165-147">Azure Mobile Engagement 없습니다 (예: Android 및 iOS에서 푸시 hello system center의 작동 원리에 대 한 앱 외부)을 제어 하는 몇 가지 제한 사항 내재 된 tooa 플랫폼이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="e2165-148">Azure Mobile Engagement 참조에 대 한 iOS 및 Android 용 Azure Mobile Engagement에서 사용 되는 hello 내부 패키지의 전체 목록을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="e2165-149">Azure Mobile Engagement의 기능 중 일부는 특정 toohello 플랫폼 (Android, iOS, 웹, Windows 및 Windows Phone) 염두에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="e2165-150">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e2165-150">See also</span></span>
* <span data-ttu-id="e2165-151">[문제 해결 가이드 - 푸시][Link 23]</span><span class="sxs-lookup"><span data-stu-id="e2165-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="e2165-152">[SDK 설명서 - 릴리스 정보][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e2165-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="e2165-153">[SDK 설명서 - 업그레이드 가이드][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e2165-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="e2165-154">응용 프로그램 작동 중단</span><span class="sxs-lookup"><span data-stu-id="e2165-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="e2165-155">문제</span><span class="sxs-lookup"><span data-stu-id="e2165-155">Issue</span></span>
* <span data-ttu-id="e2165-156">Hello 최종 사용자의 장치에 응용 프로그램 작동이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="e2165-157">원인</span><span class="sxs-lookup"><span data-stu-id="e2165-157">Causes</span></span>
* <span data-ttu-id="e2165-158">Hello에서 크래시 정보를 볼 수 있습니다 *분석 UI* 또는 hello *분석 API*</span><span class="sxs-lookup"><span data-stu-id="e2165-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="e2165-159">Hello 오래 걸리고 hello 테스트 장치의 장치 ID를 찾을 수 있습니다는 최종 사용자 toohelp 프로그램 응용 프로그램 toocrash 발생 시킨 작업을 동일한 프로그램 충돌의 hello 원인을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="e2165-160">Toohello hello SDK의 최신 버전을 업그레이드 하 여 응용 프로그램 toocrash 시키는 hello Azure Mobile Engagement SDK가 있는 알려진된 문제를 해결 한 경우에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="e2165-161">충돌을 조사할 때 플랫폼에 대 한 있는지 toocheck hello 릴리스 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="e2165-162">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e2165-162">See also</span></span>
* <span data-ttu-id="e2165-163">[SDK 설명서 - 릴리스 정보][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e2165-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="e2165-164">[SDK 설명서 - 업그레이드 가이드][Link 5]</span><span class="sxs-lookup"><span data-stu-id="e2165-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="e2165-165">앱 스토어 업로드 오류</span><span class="sxs-lookup"><span data-stu-id="e2165-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="e2165-166">문제</span><span class="sxs-lookup"><span data-stu-id="e2165-166">Issue</span></span>
* <span data-ttu-id="e2165-167">오류 관련 toouploading hello 앱 tooApple, Google 또는 hello Windows 앱 스토어의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="e2165-168">원인</span><span class="sxs-lookup"><span data-stu-id="e2165-168">Causes</span></span>
* <span data-ttu-id="e2165-169">앱 저장 경우에 따라 앱이 차단을 사용 하는 특정 기능 (예: hello Apple 스토어 hello 스토어의 앱에서 IDFV hello 사용 되지 않으며 hello GooglePlay 저장소 hello 앱 간에 응용 프로그램 정보를 공유할 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="e2165-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="e2165-170">앱 toohello 스토어에 업로드 하는 데 문제가 있는 경우 해당 플랫폼 및 hello SDK의 현재 버전에 대 한 hello 릴리스 정보를 확인 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2165-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

