---
title: "Azure Mobile Engagement 사용자 인터페이스 - 도달률 캠페인"
description: "Azure Mobile Engagement를 사용하여 푸시 알림 캠페인을 만들고 관리하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fc88db8db11d1ed12fa95c2087c9a32b21bf4de5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="ed019-103">푸시 알림 캠페인을 만들고 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="ed019-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="ed019-104">UI의 도달률 섹션을 사용하면 복합 수식을 통해 푸시 알림을 보내는 데 필요한 모든 정보를 제공하여 새 푸시 캠페인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="ed019-105">푸시 캠페인 옵션은 알림, 설문 조사, 데이터 푸시 및 타일(Windows Phone에만 해당)의 4가지 캠페인 유형에 따라 약간씩 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="ed019-106">옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="ed019-106">Option Applies to:</span></span>
* <span data-ttu-id="ed019-107">언어: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-108">캠페인: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-109">알림: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="ed019-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="ed019-110">콘텐츠: 각 캠페인 유형에서 고유함</span><span class="sxs-lookup"><span data-stu-id="ed019-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="ed019-111">대상: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-112">시간 프레임: 알림, 설문 조사, 타일</span><span class="sxs-lookup"><span data-stu-id="ed019-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="ed019-113">테스트: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![도달률 캠페인1][20]

## <a name="languages"></a><span data-ttu-id="ed019-115">언어</span><span class="sxs-lookup"><span data-stu-id="ed019-115">Languages</span></span>
<span data-ttu-id="ed019-116">언어 드롭다운 메뉴를 사용하여 서로 다른 언어를 사용하도록 설정된 장치에 각기 다른 푸시 버전을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="ed019-117">기본적으로 모든 장치는 사용하도록 설정된 언어에 관계없이 같은 푸시를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="ed019-118">장치에서 다른 언어를 사용하도록 설정한 사용자는 기본 언어 버전 푸시를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="ed019-119">대부분의 푸시 캠페인 옵션에서는 선택한 각 추가 언어에 대해 대체 콘텐츠를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![도달률 캠페인2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="ed019-121">다른 언어 적용 대상</span><span class="sxs-lookup"><span data-stu-id="ed019-121">Language differences apply to:</span></span>
* <span data-ttu-id="ed019-122">언어: 기본 언어 외에 고유 언어를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="ed019-123">캠페인: 모든 언어에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="ed019-124">알림: 기본 언어 이외의 각 언어에 대해 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="ed019-125">콘텐츠: 기본 언어 이외의 각 언어에 대해 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="ed019-126">대상: 개별 언어 기준별로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="ed019-127">시간 프레임: 모든 언어에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="ed019-128">테스트: 한 번에 한 언어로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="ed019-129">지원되는 언어</span><span class="sxs-lookup"><span data-stu-id="ed019-129">Supported Languages:</span></span>
* <span data-ttu-id="ed019-130">아랍어(ar)</span><span class="sxs-lookup"><span data-stu-id="ed019-130">Arabic (ar)</span></span> 
* <span data-ttu-id="ed019-131">불가리아어(bg)</span><span class="sxs-lookup"><span data-stu-id="ed019-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="ed019-132">카탈로니아어(ca)</span><span class="sxs-lookup"><span data-stu-id="ed019-132">Catalan (ca)</span></span> 
* <span data-ttu-id="ed019-133">중국어(zh)</span><span class="sxs-lookup"><span data-stu-id="ed019-133">Chinese (zh)</span></span> 
* <span data-ttu-id="ed019-134">크로아티아어(hr)</span><span class="sxs-lookup"><span data-stu-id="ed019-134">Croatian (hr)</span></span> 
* <span data-ttu-id="ed019-135">체코어(cs)</span><span class="sxs-lookup"><span data-stu-id="ed019-135">Czech (cs)</span></span> 
* <span data-ttu-id="ed019-136">덴마크어(da)</span><span class="sxs-lookup"><span data-stu-id="ed019-136">Danish (da)</span></span> 
* <span data-ttu-id="ed019-137">네덜란드어(nl)</span><span class="sxs-lookup"><span data-stu-id="ed019-137">Dutch (nl)</span></span> 
* <span data-ttu-id="ed019-138">영어(en)</span><span class="sxs-lookup"><span data-stu-id="ed019-138">English (en)</span></span> 
* <span data-ttu-id="ed019-139">핀란드어(fi)</span><span class="sxs-lookup"><span data-stu-id="ed019-139">Finnish (fi)</span></span> 
* <span data-ttu-id="ed019-140">프랑스어(fr)</span><span class="sxs-lookup"><span data-stu-id="ed019-140">French (fr)</span></span> 
* <span data-ttu-id="ed019-141">독일어(de)</span><span class="sxs-lookup"><span data-stu-id="ed019-141">German (de)</span></span> 
* <span data-ttu-id="ed019-142">그리스어(el)</span><span class="sxs-lookup"><span data-stu-id="ed019-142">Greek (el)</span></span> 
* <span data-ttu-id="ed019-143">히브리어(he)</span><span class="sxs-lookup"><span data-stu-id="ed019-143">Hebrew (he)</span></span> 
* <span data-ttu-id="ed019-144">힌디어(hi)</span><span class="sxs-lookup"><span data-stu-id="ed019-144">Hindi (hi)</span></span> 
* <span data-ttu-id="ed019-145">헝가리어(hu)</span><span class="sxs-lookup"><span data-stu-id="ed019-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="ed019-146">인도네시아어(id)</span><span class="sxs-lookup"><span data-stu-id="ed019-146">Indonesian (id)</span></span> 
* <span data-ttu-id="ed019-147">이탈리아어(it)</span><span class="sxs-lookup"><span data-stu-id="ed019-147">Italian (it)</span></span> 
* <span data-ttu-id="ed019-148">일본어(ja)</span><span class="sxs-lookup"><span data-stu-id="ed019-148">Japanese (ja)</span></span> 
* <span data-ttu-id="ed019-149">한국어(ko)</span><span class="sxs-lookup"><span data-stu-id="ed019-149">Korean (ko)</span></span> 
* <span data-ttu-id="ed019-150">라트비아어(lv)</span><span class="sxs-lookup"><span data-stu-id="ed019-150">Latvian (lv)</span></span> 
* <span data-ttu-id="ed019-151">리투아니아어(lt)</span><span class="sxs-lookup"><span data-stu-id="ed019-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="ed019-152">말레이어(macrolanguage)(ms)</span><span class="sxs-lookup"><span data-stu-id="ed019-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="ed019-153">노르웨이어 복말(nb)</span><span class="sxs-lookup"><span data-stu-id="ed019-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="ed019-154">폴란드어(pl)</span><span class="sxs-lookup"><span data-stu-id="ed019-154">Polish (pl)</span></span> 
* <span data-ttu-id="ed019-155">포르투갈어(pt)</span><span class="sxs-lookup"><span data-stu-id="ed019-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="ed019-156">루마니아어(ro)</span><span class="sxs-lookup"><span data-stu-id="ed019-156">Romanian (ro)</span></span> 
* <span data-ttu-id="ed019-157">러시아어(ru)</span><span class="sxs-lookup"><span data-stu-id="ed019-157">Russian (ru)</span></span> 
* <span data-ttu-id="ed019-158">세르비아어(sr)</span><span class="sxs-lookup"><span data-stu-id="ed019-158">Serbian (sr)</span></span> 
* <span data-ttu-id="ed019-159">슬로바키아어(sk)</span><span class="sxs-lookup"><span data-stu-id="ed019-159">Slovak (sk)</span></span> 
* <span data-ttu-id="ed019-160">슬로베니아어(sl)</span><span class="sxs-lookup"><span data-stu-id="ed019-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="ed019-161">스페인어(es)</span><span class="sxs-lookup"><span data-stu-id="ed019-161">Spanish (es)</span></span> 
* <span data-ttu-id="ed019-162">스웨덴어(sv)</span><span class="sxs-lookup"><span data-stu-id="ed019-162">Swedish (sv)</span></span> 
* <span data-ttu-id="ed019-163">타갈로그어(tl)</span><span class="sxs-lookup"><span data-stu-id="ed019-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="ed019-164">태국어(th)</span><span class="sxs-lookup"><span data-stu-id="ed019-164">Thai (th)</span></span> 
* <span data-ttu-id="ed019-165">터키어(tr)</span><span class="sxs-lookup"><span data-stu-id="ed019-165">Turkish (tr)</span></span> 
* <span data-ttu-id="ed019-166">우크라이나어(uk)</span><span class="sxs-lookup"><span data-stu-id="ed019-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="ed019-167">베트남어(vi)</span><span class="sxs-lookup"><span data-stu-id="ed019-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="ed019-168">캠페인</span><span class="sxs-lookup"><span data-stu-id="ed019-168">Campaign</span></span>
<span data-ttu-id="ed019-169">캠페인 섹션을 사용하면 캠페인 이름과 범주를 설정할 수 있을 뿐 아니라 푸시 캠페인의 대상 섹션을 무시하고 대신 하위 수준 푸시 API의 일부 요소와 도달률 API를 통해 이 캠페인을 보낼지 여부도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="ed019-170">미리 정의된 설정에 따라 앱 내 알림을 제어하기 위해 사용자 지정 알림 템플릿에서 범주를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="ed019-171">도달률 API를 통해 기존 "범주" 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="ed019-172">도달률 캠페인의 "캠페인" 섹션에서 "대상을 무시하고 API를 통해 사용자에게 푸시 전송" 옵션을 사용하는 경우에는 캠페인이 자동으로 전송되지 않으며 도달률 API를 통해 수동으로 캠페인을 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![도달률 캠페인3][22]

### <a name="option-applies-to"></a><span data-ttu-id="ed019-174">옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="ed019-174">Option Applies to:</span></span>
* <span data-ttu-id="ed019-175">이름: 모두</span><span class="sxs-lookup"><span data-stu-id="ed019-175">Name:    All</span></span>
* <span data-ttu-id="ed019-176">범주: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="ed019-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="ed019-177">대상을 무시하고 API를 통해 사용자에게 푸시 전송: 모두</span><span class="sxs-lookup"><span data-stu-id="ed019-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="ed019-178">알림</span><span class="sxs-lookup"><span data-stu-id="ed019-178">Notification</span></span>
<span data-ttu-id="ed019-179">알림 섹션을 사용하여 푸시의 기본적인 설정을 지정할 수 있습니다. 이러한 설정으로는 푸시 제목, 메시지, 앱 내 이미지, 푸시 해제 가능 여부 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="ed019-180">대부분의 알림 설정은 사용 중인 장치의 플랫폼에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="ed019-181">푸시를 전송할 위치로 "앱 내" 또는 "앱 외부" 중 하나를 선택하거나 둘 다를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="ed019-182">사용자는 장치 운영 체제 수준에서 푸시를 "옵트인(opt in)" 또는 "옵트아웃(opt out)"할 수 있으며 Azure Mobile Engagement에서는 이 설정을 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="ed019-183">또한 "앱 내" 푸시와 "앱 외부" 푸시는 도달률 API에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="ed019-184">푸시 API를 사용하여 "앱 외부" 푸시를 처리할 수도 있습니다. 앱 외부나 앱 내의 다른 위치로 연결하는 딥 링크를 포함한 사진이나 HTML 콘텐츠를 사용하여 푸시를 사용자 지정할 수 있습니다. 이렇게 하려면 Android SDK 2.1.0 이상의 범주가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="ed019-185">아이콘 또는 iOS 배지를 변경하고 텍스트 또는 웹 콘텐츠(html 콘텐츠와 앱 내부/외부의 다른 위치에 대한 URL 링크가 포함된 팝업)를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="ed019-186">푸시가 수신되면 Android 장치가 벨소리를 재생하거나 진동하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="ed019-187">장치가 벨소리를 재생하거나 진동하도록 하려면 Android 매니페스트 파일에 올바른 SDK 권한이 있어야 합니다. 모든 장치에서 화면 크기가 다르므로 현재 Android의 "큰 사진" 크기에 대한 업계 표준은 없지만 거의 모든 화면 크기에서는 400x100 크기의 사진을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="ed019-188">배달 유형</span><span class="sxs-lookup"><span data-stu-id="ed019-188">Delivery Types:</span></span>
* <span data-ttu-id="ed019-189">앱 외부 전용: 사용자가 응용 프로그램을 사용하지 않을 때 알림이 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="ed019-190">앱 외부 전용 알림을 보내려면 Apple 또는 Google의 인증서(APNS 또는 GCM 인증서)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="ed019-191">앱 내 전용: 응용 프로그램이 실행 중일 때만 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="ed019-192">알림은 Capptain 배달 시스템을 통해 사용자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="ed019-193">푸시의 시각적 레이아웃/표시를 완전히 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="ed019-194">항상: 이 옵션을 사용하면 응용 프로그램이 실행 중인지 여부에 관계없이 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![도달률 캠페인4][23]

### <a name="option-applies-to"></a><span data-ttu-id="ed019-196">옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="ed019-196">Option Applies to:</span></span>
* <span data-ttu-id="ed019-197">알림: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="ed019-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="ed019-198">Content</span><span class="sxs-lookup"><span data-stu-id="ed019-198">Content</span></span>
<span data-ttu-id="ed019-199">콘텐츠 섹션을 사용하면 알림, 설문 조사, 데이터 푸시, 타일(Windows Phone 전용)의 콘텐츠를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="ed019-200">푸시 캠페인의 콘텐츠 설정은 캠페인의 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="ed019-201">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ed019-201">See also</span></span>
* <span data-ttu-id="ed019-202">[UI 설명서 - 도달률 - 푸시 콘텐츠][Link 29]</span><span class="sxs-lookup"><span data-stu-id="ed019-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![도달률 캠페인5][24]

## <a name="audience"></a><span data-ttu-id="ed019-204">대상</span><span class="sxs-lookup"><span data-stu-id="ed019-204">Audience</span></span>
<span data-ttu-id="ed019-205">대상 섹션을 사용하여 표준 항목 목록을 정의해 캠페인을 제한하거나 사용자 지정된 기준에 따라 캠페인을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="ed019-206">대상을 제한하는 표준 옵션 집합을 사용하면 신규/이전 사용자 또는 네이티브 푸시 사용자에게만 푸시를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="ed019-207">또한 할당량을 설정하여 푸시를 받는 사용자 수를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="ed019-208">사용자를 대상으로 지정하는 기준을 하나 이상 포함하도록 캠페인을 필터링하는 방법에 대한 식을 수동으로 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="ed019-209">대상 식은 수동으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-209">You can manually type an audience expression.</span></span> <span data-ttu-id="ed019-210">이러한 식은 기준 간의 관계를 명시적으로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="ed019-211">기준을 설명하는 식별자는 대문자로 시작해야 하며 공백은 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="ed019-212">'and', 'or', 'not' 연산자와 '(', ')'를 사용하여 기준 간의 관계를 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="ed019-213">예: "Criterion1 or (Criterion1 and not Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="ed019-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="ed019-214">캠페인에 큰 대상을 포함하면 서버 쪽 대상 검색 속도가 느려질 수 있습니다(특히 여러 캠페인을 동시에 시작하려는 경우).</span><span class="sxs-lookup"><span data-stu-id="ed019-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="ed019-215">가능하면 캠페인을 한 번에 하나만 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="ed019-216">많이 필요한 경우 캠페인을 한 번에 4개까지만 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="ed019-217">앱을 아직 설치해 두었으며 사용 중인 사용자만 검색하면 되도록 활성 사용자에게만 푸시를 보냅니다. 이렇게 하려면 "네이티브 푸시를 사용하여 연결할 수 있는 사용자만 참여" 및 "활성 사용자만 참여" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="ed019-218">대상을 정의한 후에는 시뮬레이트 단추를 사용하여 해당 푸시를 수신할 사용자의 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="ed019-219">그러면 이 대상을 통해 대상으로 지정될 수 있는 알려진 사용자 수가 계산됩니다. 이 결과는 무작위 사용자 샘플을 기준으로 한 예상치입니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="ed019-220">응용 프로그램을 제거한 사용자도 이 대상에 포함되기는 하지만 이러한 사용자에게는 푸시가 배달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="ed019-221">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ed019-221">See also</span></span>
* <span data-ttu-id="ed019-222">[UI 설명서 - 도달률 - 새 푸시 기준][Link 28]</span><span class="sxs-lookup"><span data-stu-id="ed019-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![도달률 캠페인6][25]

### <a name="edit-expression"></a><span data-ttu-id="ed019-224">식 편집</span><span class="sxs-lookup"><span data-stu-id="ed019-224">Edit expression</span></span>
![도달률 캠페인7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="ed019-226">대상 제한 옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="ed019-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="ed019-227">사용자 하위 집합만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-228">이전 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-229">새 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-230">유휴 사용자만 참여: 알림, 설문 조사, 타일</span><span class="sxs-lookup"><span data-stu-id="ed019-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="ed019-231">활성 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="ed019-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="ed019-232">네이티브 푸시를 사용하여 연결할 수 있는 사용자만 참여: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="ed019-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="ed019-233">시간 프레임</span><span class="sxs-lookup"><span data-stu-id="ed019-233">Time Frame</span></span>
<span data-ttu-id="ed019-234">기간 섹션을 사용하여 푸시를 보낼 시간을 설정할 수도 있습니다. 캠페인을 즉시 시작하려는 경우에는 기간을 비워 두면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="ed019-235">최종 사용자의 표준 시간대를 사용하는 경우 아시아 지역 최종 사용자의 경우에는 캠페인이 예상보다 하루 일찍 시작할 수 있으며 세계의 모든 표준 시간대가 캠페인에 대해 설정된 기간과 일치할 때까지 작은 푸시 배치가 한 번에 하나씩 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="ed019-236">또한 캠페인은 푸시를 시작하기 전에 휴대폰에서 시간을 요청해야 하므로, 최종 사용자의 표준 시간대를 사용하면 캠페인이 지연될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="ed019-237">종료 날짜가 없는 캠페인은 푸시를 로컬로 캐시할 수 있으므로 캠페인을 수동으로 종료한 후에도 푸시가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="ed019-238">이 동작을 방지하려면이 캠페인에 대해 구체적인 종료 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="ed019-239">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ed019-239">See also</span></span>
* <span data-ttu-id="ed019-240">[도달률 - 방법 - 예약][Link 3]</span><span class="sxs-lookup"><span data-stu-id="ed019-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![도달률 캠페인8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="ed019-242">설정 적용 대상</span><span class="sxs-lookup"><span data-stu-id="ed019-242">Settings Apply to:</span></span>
* <span data-ttu-id="ed019-243">시간 프레임: 알림, 설문 조사, 타일</span><span class="sxs-lookup"><span data-stu-id="ed019-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="ed019-244">테스트</span><span class="sxs-lookup"><span data-stu-id="ed019-244">Test</span></span>
<span data-ttu-id="ed019-245">테스트 섹션을 사용하면 캠페인을 저장하기 전에 원하는 테스트 장치로 이 푸시를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="ed019-246">이 캠페인에 대해 사용자 지정 언어를 구성한 경우에는 각 언어에서 푸시를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="ed019-247">테스트 장치는 "내 계정"에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="ed019-248">푸시를 "테스트"하는 단추를 사용할 때는 서버 쪽 데이터가 기록되지 않으며 실제 푸시 캠페인에 대해서만 데이터기 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed019-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="ed019-249">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ed019-249">See also</span></span>
* <span data-ttu-id="ed019-250">[UI 설명서 - 내 계정][Link 14]</span><span class="sxs-lookup"><span data-stu-id="ed019-250">[UI Documentation - My Account][Link 14]</span></span>

![도달률 캠페인9][28]

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

