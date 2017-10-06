---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 조건에 도달"
description: "Toouse 대상 조건 toosend 푸시 캠페인 tooa Azure Mobile Engagement를 사용 하 여 사용자의 하위 집합을 선택 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="53daa-103">Toouse 대상 조건 toosend 푸시 캠페인 tooa 사용자의 하위 집합을 선택 하는 방법</span><span class="sxs-lookup"><span data-stu-id="53daa-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="53daa-104">Hello "새 기준" 단추와 특정 기준으로 대상 그룹을 대상으로 hello 가장 강력한 개념에 대해 Azure Mobile Engagement는 사용 하면 보내는 관련 대 한 푸시 알림 hello 고객 tooinstead 스팸 모든 사용자의 응답 하는 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="53daa-105">표준 기준에 따라 대상 그룹을 제한 하 고 푸시 toodetermine 시뮬레이션 얼마나 많은 사람들이 hello 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="53daa-106">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="53daa-106">**See also:**</span></span>

* <span data-ttu-id="53daa-107">[UI 설명서 - 도달률 - 새 푸시 캠페인][Link 27]</span><span class="sxs-lookup"><span data-stu-id="53daa-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="53daa-108">대상 기준에는 다음 항목이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-108">Audience criteria can include:</span></span>
* <span data-ttu-id="53daa-109">* * Technicals: * *에 따라 hello 대상 같은 기술 정보 hello 분석 및 모니터링 섹션에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="53daa-110">**참고 항목** [UI 설명서 - 분석][Link 15],  [UI 설명서 - 모니터][Link 16]</span><span class="sxs-lookup"><span data-stu-id="53daa-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="53daa-111">**위치:** "실시간 위치 보고"을 사용 하 여 지 오 펜싱을 사용 하는 응용 프로그램 기준 tootarget hello GPS 위치에서에서 대상 그룹으로 지리적 위치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="53daa-112">"지연 영역 위치 보고" 호출 또한 사용된 tootarget hello 휴대 전화 위치에서 대상 그룹을 수 ("실시간 위치 보고" 및 "지연 된 영역 위치 보고" 해야 활성화 hello SDK에서에서).</span><span class="sxs-lookup"><span data-stu-id="53daa-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="53daa-113">**참고 항목:** [SDK 설명서 - iOS - 통합][Link 5], [SDK 설명서 - Android - 통합][Link 5]</span><span class="sxs-lookup"><span data-stu-id="53daa-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="53daa-114">**도달률 피드백:** 알림, 설문 조사 및 데이터 푸시의 도달률 피드백을 통해 이전 도달률 알림의 피드백에 따라 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="53daa-115">이렇게 하면 toobetter 대상 두세 도달 보다 캠페인 청중 처음으로 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="53daa-116">사용할 수도 있습니다 toofilter 캠페인 tooNOT를 설정 하 여 유사 콘텐츠 관련 된 알림을 이미 받은 사용자가 특정 이전 캠페인을 이미 받은 toousers를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="53daa-117">여전히 활성 상태인 특정 캠페인에 포함된 사용자가 새 푸시를 받지 않도록 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="53daa-118">**참고 항목:** [UI 설명서 - 도달률 - 푸시 콘텐츠][Link 29]</span><span class="sxs-lookup"><span data-stu-id="53daa-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="53daa-119">**설치 추적:** 사용자가 앱을 설치한 위치를 기준으로 정보를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="53daa-120">**참고 항목:** [UI 설명서 - 설정][Link 20]</span><span class="sxs-lookup"><span data-stu-id="53daa-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="53daa-121">**사용자 프로필:** 표준 사용자 정보에 따라 대상 수 하 고 사용자가 만든 hello 사용자 지정 앱 정보를 기준으로 대상 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="53daa-122">사용자가 현재 로그인에 고 tooset 방금 어떻게가 응답 tooprevious 캠페인 대신 자체 hello 응용 프로그램에서 요청 했습니다 특정 질문에 답변 한 사용자가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="53daa-123">앱에 대해 정의한 모든 앱 정보가 이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="53daa-124">세그먼트: 여러 기준을 포함하는 특정 사용자 동작을 기준으로 작성한 세그먼트에 따라 대상을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="53daa-125">앱에 대해 정의한 모든 세그먼트가 이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="53daa-126">**참고 항목:** [UI 설명서 - 세그먼트][Link 18]</span><span class="sxs-lookup"><span data-stu-id="53daa-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="53daa-127">**응용 프로그램 정보:** "설정" tootrack 사용자 동작에서 사용자 지정 응용 프로그램 정보 태그를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="53daa-128">**참고 항목:** [UI 설명서 - 설정][Link 20]</span><span class="sxs-lookup"><span data-stu-id="53daa-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="53daa-129">예제:</span><span class="sxs-lookup"><span data-stu-id="53daa-129">Example:</span></span>
<span data-ttu-id="53daa-130">Toopush 원하는 알림만 toohello 하위 집합에서-app를 수행한 사용자의 동작을 구입 합니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="53daa-131">응용 프로그램 설정 페이지 tooyour hello "앱 정보" 메뉴를 선택한 "새 응용 프로그램 정보"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="53daa-132">"inAppPurchase"라는 새 부울 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="53daa-133">Hello 사용자 앱에서 바로 구매를 성공적으로 수행 하는 경우이 응용 프로그램 정보를 설정 하는 응용 프로그램을 "true" 너무 확인 (hello sendAppInfo ("inAppPurchase",...)를 사용 하 여 함수)</span><span class="sxs-lookup"><span data-stu-id="53daa-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="53daa-134">않으려면 toodo이 응용 프로그램에서 hello 장치 API를 사용 하 여 백 엔드에서 수행할 수 있습니다)</span><span class="sxs-lookup"><span data-stu-id="53daa-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="53daa-135">그런 다음 프로그램 알림 "inAppPurchase" 필요 청중 toousers 프로그램 제한 조건으로 설정 "true" 너무 toocreate만 필요)</span><span class="sxs-lookup"><span data-stu-id="53daa-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="53daa-136">응용 프로그램 정보 태그 이외의 기준에 따라 대상 컴퓨터가 있어야 사용자의 장치에서 Azure Mobile Engagement toogather 정보 hello 푸시 전송 되 고 지연 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="53daa-137">배지 업데이트 등의 복합 푸시 구성 옵션을 사용하는 경우에도 푸시가 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="53daa-138">Hello 푸시 API에서에서 "단일 쇼트" 캠페인을 사용 하는 hello 절대 가장 빠른 푸시 방법 Azure Mobile Engagement 에서입니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="53daa-139">Reach 캠페인 (에서 나 hello Reach API hello UI)에 대 한 푸시 기준으로 앱 정보 태그만 사용 하는 것이 응용 프로그램 정보 태그 hello 서버 쪽에서 저장 되므로 hello 다음 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="53daa-140">푸시 캠페인에 대 한 다른 대상 기준을 사용 하는 hello 가장 유연한 이자 가장 느린 푸시 방법은 Azure Mobile Engagement 순서 toosend hello 캠페인의 tooquery hello 장치에 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="53daa-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![도달률 기준1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="53daa-142">기준 옵션 적용 대상:</span><span class="sxs-lookup"><span data-stu-id="53daa-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="53daa-143">**기술 정보**</span><span class="sxs-lookup"><span data-stu-id="53daa-143">**Technicals**</span></span>     
* <span data-ttu-id="53daa-144">펌웨어 이름: 펌웨어 이름</span><span class="sxs-lookup"><span data-stu-id="53daa-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="53daa-145">펌웨어 버전: 펌웨어 버전</span><span class="sxs-lookup"><span data-stu-id="53daa-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="53daa-146">장치 모델: 장치 모델</span><span class="sxs-lookup"><span data-stu-id="53daa-146">Device model:    Device model</span></span>
* <span data-ttu-id="53daa-147">장치 제조업체: 장치 제조업체</span><span class="sxs-lookup"><span data-stu-id="53daa-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="53daa-148">응용 프로그램 버전: 응용 프로그램 버전</span><span class="sxs-lookup"><span data-stu-id="53daa-148">Application version:    Application version</span></span>
* <span data-ttu-id="53daa-149">통신 회사 이름: 통신 회사 이름, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="53daa-150">통신 회사 국가: 통신 회사 국가, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="53daa-151">네트워크 유형: 네트워크 유형</span><span class="sxs-lookup"><span data-stu-id="53daa-151">Network type:    Network type</span></span>
* <span data-ttu-id="53daa-152">로캘: 로캘</span><span class="sxs-lookup"><span data-stu-id="53daa-152">Locale:    Locale</span></span>
* <span data-ttu-id="53daa-153">화면 크기: 화면 크기</span><span class="sxs-lookup"><span data-stu-id="53daa-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="53daa-154">**위치**</span><span class="sxs-lookup"><span data-stu-id="53daa-154">**Location**</span></span>      
* <span data-ttu-id="53daa-155">마지막으로 확인된 지역: 국가, 지역, 구/군/시</span><span class="sxs-lookup"><span data-stu-id="53daa-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="53daa-156">실시간 지리적 펜스: 지점(이름/작업), 원형 지점(이름, 위도, 경도, 미터 단위 반경)</span><span class="sxs-lookup"><span data-stu-id="53daa-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="53daa-157">**도달률 피드백**</span><span class="sxs-lookup"><span data-stu-id="53daa-157">**Reach feedback**</span></span>     
* <span data-ttu-id="53daa-158">알림 피드백: 알림, 피드백</span><span class="sxs-lookup"><span data-stu-id="53daa-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="53daa-159">설문 조사 피드백: 설문 조사, 피드백</span><span class="sxs-lookup"><span data-stu-id="53daa-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="53daa-160">설문 조사 응답 피드백: 설문 조사 응답 피드백, 질문, 선택 항목</span><span class="sxs-lookup"><span data-stu-id="53daa-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="53daa-161">데이터 푸시 피드백: 데이터 푸시, 피드백</span><span class="sxs-lookup"><span data-stu-id="53daa-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="53daa-162">**설치 추적**</span><span class="sxs-lookup"><span data-stu-id="53daa-162">**Install Tracking**</span></span>     
* <span data-ttu-id="53daa-163">스토어: 스토어, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="53daa-164">원본: 원본, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="53daa-165">**사용자 프로필**</span><span class="sxs-lookup"><span data-stu-id="53daa-165">**User profile**</span></span>     
* <span data-ttu-id="53daa-166">성별: 남성 또는 여성, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="53daa-167">생년월일: 연산자, 날짜, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="53daa-168">옵트인(opt in): true 또는 false, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="53daa-169">**앱 정보**</span><span class="sxs-lookup"><span data-stu-id="53daa-169">**App Info**</span></span>      
* <span data-ttu-id="53daa-170">문자열: 문자열, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-170">String:    String, undefined</span></span>
* <span data-ttu-id="53daa-171">날짜: 연산자, 날짜, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="53daa-172">정수: 연산자, 숫자, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="53daa-173">부울: true 또는 false, 정의되지 않음</span><span class="sxs-lookup"><span data-stu-id="53daa-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="53daa-174">**세그먼트**</span><span class="sxs-lookup"><span data-stu-id="53daa-174">**Segment**</span></span>    
* <span data-ttu-id="53daa-175">드롭다운 목록의 세그먼트 이름, 제외 항목(이 세그먼트에 포함되지 않은 대상 사용자)</span><span class="sxs-lookup"><span data-stu-id="53daa-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

