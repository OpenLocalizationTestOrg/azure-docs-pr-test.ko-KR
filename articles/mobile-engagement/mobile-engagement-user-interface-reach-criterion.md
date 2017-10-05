---
title: "Azure Mobile Engagement 사용자 인터페이스 - 도달률 기준"
description: "Azure Mobile Engagement를 사용하여 대상 지정 기준을 사용하여 선택한 사용자 하위 집합에 푸시 캠페인을 보내는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 803b44721d0ab1ac7b5a8074e18857fc57adb724
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-targeting-criteria-to-send-push-campaigns-to-a-select-subset-of-your-users"></a><span data-ttu-id="30cd4-103">대상 지정 기준을 사용하여 선택한 사용자 하위 집합에 푸시 캠페인을 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="30cd4-103">How to use targeting criteria to send push campaigns to a select subset of your users</span></span>
<span data-ttu-id="30cd4-104">"새 기준" 단추를 사용하여 특정 기준에 따라 대상을 지정하는 방식은 Azure Mobile Engagement에서 가장 유용한 개념 중 하나입니다. 이 방법을 사용하면 모든 대상을 스팸으로 처리하는 대신 고객이 반응을 보이도록 할 관련성이 높은 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span></span> <span data-ttu-id="30cd4-105">표준 기준에 따라 대상을 제한하고 푸시를 시뮬레이트하여 알림을 수신할 사용자 수를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span></span>

<span data-ttu-id="30cd4-106">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="30cd4-106">**See also:**</span></span>

* <span data-ttu-id="30cd4-107">[UI 설명서 - 도달률 - 새 푸시 캠페인][Link 27]</span><span class="sxs-lookup"><span data-stu-id="30cd4-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="30cd4-108">대상 기준에는 다음 항목이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-108">Audience criteria can include:</span></span>
* <span data-ttu-id="30cd4-109">* * Technicals: * * 대상 분석 및 모니터링 섹션에서 볼 수 있는 동일한 기술 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-109">**Technicals: ** You can target based on the same technical information you can see in the Analytics and Monitor sections.</span></span> <span data-ttu-id="30cd4-110">**참고 항목** [UI 설명서 - 분석][Link 15],  [UI 설명서 - 모니터][Link 16]</span><span class="sxs-lookup"><span data-stu-id="30cd4-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="30cd4-111">**위치:** 지역 펜싱과 함께 "실시간 위치 보고"를 사용하는 응용 프로그램은 지리적 위치를 기준으로 사용하여 GPS 위치에서 대상 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span></span> <span data-ttu-id="30cd4-112">"지연 영역 위치 보고" 호출을 사용하여 휴대폰 위치에서 대상 그룹을 지정할 수도 있습니다(SDK에서 "실시간으로 위치 보고" 및 "지연 영역 위치 보고"를 활성화해야 함).</span><span class="sxs-lookup"><span data-stu-id="30cd4-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span></span> <span data-ttu-id="30cd4-113">**참고 항목:** [SDK 설명서 - iOS - 통합][Link 5], [SDK 설명서 - Android - 통합][Link 5]</span><span class="sxs-lookup"><span data-stu-id="30cd4-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="30cd4-114">**도달률 피드백:** 알림, 설문 조사 및 데이터 푸시의 도달률 피드백을 통해 이전 도달률 알림의 피드백에 따라 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="30cd4-115">이렇게 하면 두세 개의 도달률 캠페인 후 처음보다 더 효율적으로 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span></span> <span data-ttu-id="30cd4-116">또한 이미 특정 이전 캠페인을 받은 사용자에게 캠페인이 전송되지 않도록 설정하여 이미 유사한 콘텐츠가 포함된 알림을 받은 사용자를 필터링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span></span> <span data-ttu-id="30cd4-117">여전히 활성 상태인 특정 캠페인에 포함된 사용자가 새 푸시를 받지 않도록 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="30cd4-118">**참고 항목:** [UI 설명서 - 도달률 - 푸시 콘텐츠][Link 29]</span><span class="sxs-lookup"><span data-stu-id="30cd4-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="30cd4-119">**설치 추적:** 사용자가 앱을 설치한 위치를 기준으로 정보를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="30cd4-120">**참고 항목:** [UI 설명서 - 설정][Link 20]</span><span class="sxs-lookup"><span data-stu-id="30cd4-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="30cd4-121">**사용자 프로필:** 표준 사용자 정보와 직접 만든 사용자 지정 앱 정보를 기준으로 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span></span> <span data-ttu-id="30cd4-122">이러한 대상에는 현재 로그인되어 있는 사용자와 특정 질문(단순히 이전 캠페인에 응답한 방식만이 아니라 앱 자체에서 설정하여 응답하도록 요청한 질문)에 대답한 사용자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span></span> <span data-ttu-id="30cd4-123">앱에 대해 정의한 모든 앱 정보가 이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="30cd4-124">세그먼트: 여러 기준을 포함하는 특정 사용자 동작을 기준으로 작성한 세그먼트에 따라 대상을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="30cd4-125">앱에 대해 정의한 모든 세그먼트가 이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="30cd4-126">**참고 항목:** [UI 설명서 - 세그먼트][Link 18]</span><span class="sxs-lookup"><span data-stu-id="30cd4-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="30cd4-127">**앱 정보:** "설정"에서 사용자 지정 앱 정보 태그를 만들어 사용자 동작을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span></span> <span data-ttu-id="30cd4-128">**참고 항목:** [UI 설명서 - 설정][Link 20]</span><span class="sxs-lookup"><span data-stu-id="30cd4-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="30cd4-129">예제:</span><span class="sxs-lookup"><span data-stu-id="30cd4-129">Example:</span></span>
<span data-ttu-id="30cd4-130">앱 내 구매 작업을 수행한 사용자에게만 알림을 푸시하려는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="30cd4-131">응용 프로그램 설정 페이지로 이동하여 "앱 정보" 메뉴를 선택하고 "새 앱 정보"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-131">Go to your application settings page, select the "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="30cd4-132">"inAppPurchase"라는 새 부울 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="30cd4-133">사용자가 앱 내 구매를 정상적으로 수행하면 응용 프로그램에서 sendAppInfo("inAppPurchase", ...) 함수를 사용하여 이 앱 정보를 "true"로 설정하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="30cd4-134">응용 프로그램에서 이 작업을 수행하지 않으려는 경우 장치 API를 사용하여 백 엔드에서 해당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span></span>
5. <span data-ttu-id="30cd4-135">그런 후에는 대상을 "inAppPurchase"가 "true"로 설정된 사용자로 제한하는 기준을 사용하여 알림을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span></span>

> [!NOTE]
> <span data-ttu-id="30cd4-136">앱 정보 태그 이외의 기준에 따라 대상을 지정하려는 경우에는 푸시를 보내기 전에 Azure Mobile Engagement에서 사용자 장치의 정보를 수집해야 하므로 푸시가 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span></span> <span data-ttu-id="30cd4-137">배지 업데이트 등의 복합 푸시 구성 옵션을 사용하는 경우에도 푸시가 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="30cd4-138">Azure Mobile Engagement에서 가장 빠르게 푸시를 보내려는 경우 푸시 API에서 "일회성" 캠페인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="30cd4-139">두 번째로 빠른 방법은 도달률 API나 UI에서 도달률 캠페인에 대해 앱 정보 태그만 푸시 기준으로 사용하는 것입니다. 앱 정보 태그는 서버 쪽에 저장되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span></span> <span data-ttu-id="30cd4-140">푸시 캠페인에 대해 다른 대상 지정 기준을 사용하는 푸시 방법이 가장 유동적이기는 하지만 속도는 가장 느립니다. Azure Mobile Engagement는 캠페인을 보내려면 장치를 쿼리해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="30cd4-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span></span>

![도달률 기준1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="30cd4-142">기준 옵션 적용 대상:</span><span class="sxs-lookup"><span data-stu-id="30cd4-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="30cd4-143">**기술 정보**</span><span class="sxs-lookup"><span data-stu-id="30cd4-143">**Technicals**</span></span>     
* <span data-ttu-id="30cd4-144">펌웨어 이름: 펌웨어 이름</span><span class="sxs-lookup"><span data-stu-id="30cd4-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="30cd4-145">펌웨어 버전: 펌웨어 버전</span><span class="sxs-lookup"><span data-stu-id="30cd4-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="30cd4-146">장치 모델: 장치 모델</span><span class="sxs-lookup"><span data-stu-id="30cd4-146">Device model:    Device model</span></span>
* <span data-ttu-id="30cd4-147">장치 제조업체: 장치 제조업체</span><span class="sxs-lookup"><span data-stu-id="30cd4-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="30cd4-148">응용 프로그램 버전: 응용 프로그램 버전</span><span class="sxs-lookup"><span data-stu-id="30cd4-148">Application version:    Application version</span></span>
* <span data-ttu-id="30cd4-149">통신 회사 이름: 통신 회사 이름, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="30cd4-150">통신 회사 국가: 통신 회사 국가, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="30cd4-151">네트워크 유형: 네트워크 유형</span><span class="sxs-lookup"><span data-stu-id="30cd4-151">Network type:    Network type</span></span>
* <span data-ttu-id="30cd4-152">로캘: 로캘</span><span class="sxs-lookup"><span data-stu-id="30cd4-152">Locale:    Locale</span></span>
* <span data-ttu-id="30cd4-153">화면 크기: 화면 크기</span><span class="sxs-lookup"><span data-stu-id="30cd4-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="30cd4-154">**위치**</span><span class="sxs-lookup"><span data-stu-id="30cd4-154">**Location**</span></span>      
* <span data-ttu-id="30cd4-155">마지막으로 확인된 지역: 국가, 지역, 구/군/시</span><span class="sxs-lookup"><span data-stu-id="30cd4-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="30cd4-156">실시간 지리적 펜스: 지점(이름/작업), 원형 지점(이름, 위도, 경도, 미터 단위 반경)</span><span class="sxs-lookup"><span data-stu-id="30cd4-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="30cd4-157">**도달률 피드백**</span><span class="sxs-lookup"><span data-stu-id="30cd4-157">**Reach feedback**</span></span>     
* <span data-ttu-id="30cd4-158">알림 피드백: 알림, 피드백</span><span class="sxs-lookup"><span data-stu-id="30cd4-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="30cd4-159">설문 조사 피드백: 설문 조사, 피드백</span><span class="sxs-lookup"><span data-stu-id="30cd4-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="30cd4-160">설문 조사 응답 피드백: 설문 조사 응답 피드백, 질문, 선택 항목</span><span class="sxs-lookup"><span data-stu-id="30cd4-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="30cd4-161">데이터 푸시 피드백: 데이터 푸시, 피드백</span><span class="sxs-lookup"><span data-stu-id="30cd4-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="30cd4-162">**설치 추적**</span><span class="sxs-lookup"><span data-stu-id="30cd4-162">**Install Tracking**</span></span>     
* <span data-ttu-id="30cd4-163">스토어: 스토어, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="30cd4-164">원본: 원본, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="30cd4-165">**사용자 프로필**</span><span class="sxs-lookup"><span data-stu-id="30cd4-165">**User profile**</span></span>     
* <span data-ttu-id="30cd4-166">성별: 남성 또는 여성, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="30cd4-167">생년월일: 연산자, 날짜, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="30cd4-168">옵트인(opt in): true 또는 false, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="30cd4-169">**앱 정보**</span><span class="sxs-lookup"><span data-stu-id="30cd4-169">**App Info**</span></span>      
* <span data-ttu-id="30cd4-170">문자열: 문자열, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-170">String:    String, undefined</span></span>
* <span data-ttu-id="30cd4-171">날짜: 연산자, 날짜, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="30cd4-172">정수: 연산자, 숫자, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="30cd4-173">부울: true 또는 false, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="30cd4-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="30cd4-174">**세그먼트**</span><span class="sxs-lookup"><span data-stu-id="30cd4-174">**Segment**</span></span>    
* <span data-ttu-id="30cd4-175">드롭다운 목록의 세그먼트 이름, 제외 항목(이 세그먼트에 포함되지 않은 대상 사용자)</span><span class="sxs-lookup"><span data-stu-id="30cd4-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

