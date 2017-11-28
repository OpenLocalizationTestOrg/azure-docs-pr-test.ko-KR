---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 캠페인에 도달"
description: "Laern 어떻게 toocreate 및 푸시 알림 캠페인 Azure Mobile Engagement를 사용 하 여 관리"
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
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="c9d9b-103">어떻게 toocreate 및 푸시 알림 캠페인 관리</span><span class="sxs-lookup"><span data-stu-id="c9d9b-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="c9d9b-104">푸시 알림을 toosend 필요한 모든 hello 정보를 제공 하 여 복잡 한 수식을 사용 하 여 hello hello UI toocreate 새 푸시 캠페인의 도달 범위 섹션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="c9d9b-105">hello 푸시 캠페인의 옵션에 따라 약간 다 4 hello 캠페인 종류: 공지, 여론 조사, 데이터 푸시 및 타일 (Windows Phone만 해당).</span><span class="sxs-lookup"><span data-stu-id="c9d9b-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="c9d9b-106">옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-106">Option Applies to:</span></span>
* <span data-ttu-id="c9d9b-107">언어: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-108">캠페인: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-109">알림: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="c9d9b-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="c9d9b-110">콘텐츠: 각 캠페인 유형에서 고유함</span><span class="sxs-lookup"><span data-stu-id="c9d9b-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="c9d9b-111">대상: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-112">시간 프레임: 알림, 설문 조사, 타일</span><span class="sxs-lookup"><span data-stu-id="c9d9b-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="c9d9b-113">테스트: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![도달률 캠페인1][20]

## <a name="languages"></a><span data-ttu-id="c9d9b-115">언어</span><span class="sxs-lookup"><span data-stu-id="c9d9b-115">Languages</span></span>
<span data-ttu-id="c9d9b-116">Hello 언어 드롭 다운 메뉴 toosend toouse 다른 언어로 설정 된 푸시 toodevices 프로그램의 다른 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="c9d9b-117">기본적으로 모든 장치 toouse 설정 된 언어에 관계 없이 동일한 푸시 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="c9d9b-118">사용자가 자신의 장치 집합 tooa 다른 언어와 hello 기본 언어 버전의 hello 푸시를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="c9d9b-119">Hello 푸시 캠페인 옵션의 대다수 사용 하면 toospecify 대체 콘텐츠 대 각 hello 추가 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![도달률 캠페인2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="c9d9b-121">다른 언어 적용 대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-121">Language differences apply to:</span></span>
* <span data-ttu-id="c9d9b-122">언어: 고유한 언어 추가 toohello 기본 언어에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="c9d9b-123">캠페인: 모든 언어에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="c9d9b-124">알림: 각 언어에 대 한 고유한 또한 toohello 기본 언어</span><span class="sxs-lookup"><span data-stu-id="c9d9b-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="c9d9b-125">내용: 각 언어에 대 한 고유한 또한 toohello 기본 언어</span><span class="sxs-lookup"><span data-stu-id="c9d9b-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="c9d9b-126">대상: 개별 언어 기준별로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="c9d9b-127">시간 프레임: 모든 언어에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="c9d9b-128">테스트: 한 번에 tooeach 언어 전송 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="c9d9b-129">지원되는 언어</span><span class="sxs-lookup"><span data-stu-id="c9d9b-129">Supported Languages:</span></span>
* <span data-ttu-id="c9d9b-130">아랍어(ar)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-130">Arabic (ar)</span></span> 
* <span data-ttu-id="c9d9b-131">불가리아어(bg)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="c9d9b-132">카탈로니아어(ca)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-132">Catalan (ca)</span></span> 
* <span data-ttu-id="c9d9b-133">중국어(zh)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-133">Chinese (zh)</span></span> 
* <span data-ttu-id="c9d9b-134">크로아티아어(hr)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-134">Croatian (hr)</span></span> 
* <span data-ttu-id="c9d9b-135">체코어(cs)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-135">Czech (cs)</span></span> 
* <span data-ttu-id="c9d9b-136">덴마크어(da)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-136">Danish (da)</span></span> 
* <span data-ttu-id="c9d9b-137">네덜란드어(nl)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-137">Dutch (nl)</span></span> 
* <span data-ttu-id="c9d9b-138">영어(en)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-138">English (en)</span></span> 
* <span data-ttu-id="c9d9b-139">핀란드어(fi)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-139">Finnish (fi)</span></span> 
* <span data-ttu-id="c9d9b-140">프랑스어(fr)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-140">French (fr)</span></span> 
* <span data-ttu-id="c9d9b-141">독일어(de)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-141">German (de)</span></span> 
* <span data-ttu-id="c9d9b-142">그리스어(el)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-142">Greek (el)</span></span> 
* <span data-ttu-id="c9d9b-143">히브리어(he)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-143">Hebrew (he)</span></span> 
* <span data-ttu-id="c9d9b-144">힌디어(hi)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-144">Hindi (hi)</span></span> 
* <span data-ttu-id="c9d9b-145">헝가리어(hu)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="c9d9b-146">인도네시아어(id)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-146">Indonesian (id)</span></span> 
* <span data-ttu-id="c9d9b-147">이탈리아어(it)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-147">Italian (it)</span></span> 
* <span data-ttu-id="c9d9b-148">일본어(ja)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-148">Japanese (ja)</span></span> 
* <span data-ttu-id="c9d9b-149">한국어(ko)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-149">Korean (ko)</span></span> 
* <span data-ttu-id="c9d9b-150">라트비아어(lv)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-150">Latvian (lv)</span></span> 
* <span data-ttu-id="c9d9b-151">리투아니아어(lt)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="c9d9b-152">말레이어(macrolanguage)(ms)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="c9d9b-153">노르웨이어 복말(nb)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="c9d9b-154">폴란드어(pl)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-154">Polish (pl)</span></span> 
* <span data-ttu-id="c9d9b-155">포르투갈어(pt)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="c9d9b-156">루마니아어(ro)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-156">Romanian (ro)</span></span> 
* <span data-ttu-id="c9d9b-157">러시아어(ru)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-157">Russian (ru)</span></span> 
* <span data-ttu-id="c9d9b-158">세르비아어(sr)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-158">Serbian (sr)</span></span> 
* <span data-ttu-id="c9d9b-159">슬로바키아어(sk)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-159">Slovak (sk)</span></span> 
* <span data-ttu-id="c9d9b-160">슬로베니아어(sl)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="c9d9b-161">스페인어(es)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-161">Spanish (es)</span></span> 
* <span data-ttu-id="c9d9b-162">스웨덴어(sv)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-162">Swedish (sv)</span></span> 
* <span data-ttu-id="c9d9b-163">타갈로그어(tl)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="c9d9b-164">태국어(th)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-164">Thai (th)</span></span> 
* <span data-ttu-id="c9d9b-165">터키어(tr)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-165">Turkish (tr)</span></span> 
* <span data-ttu-id="c9d9b-166">우크라이나어(uk)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="c9d9b-167">베트남어(vi)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="c9d9b-168">캠페인</span><span class="sxs-lookup"><span data-stu-id="c9d9b-168">Campaign</span></span>
<span data-ttu-id="c9d9b-169">사용할 수 있습니다 hello 캠페인 섹션 tooset hello 이름 및 캠페인의 범주도 마치 푸시 캠페인의 tooignore hello 대상 섹션을 계획 하 고 hello Reach API를 통해이 캠페인 (및 hello 낮은 수준 푸시 API를 사용 하 여 일부 요소)를 대신 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="c9d9b-170">범주는 미리 정의 된 설정에 따라 사용자 지정 알림 템플릿 toocontrol 앱 내 알림과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="c9d9b-171">Hello Reach API를 통해 기존 "범주" 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="c9d9b-172">Toosend 해야는 hello "대상 그룹 무시, 푸시가 전송 되지 hello API 통해 toousers" 옵션 사용 Reach 캠페인의 hello "는 캠페인" 섹션에 hello 캠페인은 자동으로 보내지 않습니다 hello Reach API를 통해 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![도달률 캠페인3][22]

### <a name="option-applies-to"></a><span data-ttu-id="c9d9b-174">옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-174">Option Applies to:</span></span>
* <span data-ttu-id="c9d9b-175">이름: 모두</span><span class="sxs-lookup"><span data-stu-id="c9d9b-175">Name:    All</span></span>
* <span data-ttu-id="c9d9b-176">범주: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="c9d9b-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="c9d9b-177">대상 그룹 무시, 푸시가 toousers hello API 통해 전송 되지: 모든</span><span class="sxs-lookup"><span data-stu-id="c9d9b-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="c9d9b-178">알림</span><span class="sxs-lookup"><span data-stu-id="c9d9b-178">Notification</span></span>
<span data-ttu-id="c9d9b-179">포함 하 여 푸시에 대 한 hello 알림 섹션 tooset 기본 설정을 사용할 수 있습니다: hello hello 푸시 hello 메시지, 앱에서 이미지의 제목 또는 해제 가능한 경우.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="c9d9b-180">다양 한 알림 설정을 장치의 플랫폼 특정 toohello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="c9d9b-181">푸시를 전송할 위치로 "앱 내" 또는 "앱 외부" 중 하나를 선택하거나 둘 다를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="c9d9b-182">(사용자가 "옵트인" 또는 "옵트아웃"을 "부족 app"에 푸시합니다 hello 운영 체제 수준 장치에서 입력 해야 하며 Azure Mobile Engagement는 금지 됩니다 수 toooverride이이 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="c9d9b-183">또한 hello Reach API 처리 "app" 및 "out 응용 프로그램의" 푸시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="c9d9b-184">hello 푸시 API 사용 가능 너무 푸시 "응용 프로그램의 초과" 사용된 toohandle.) 푸시 그림 또는 사용자 응용 프로그램 또는 tooanother 위치 (Android SDK 2.1.0 또는 필요한 이상 의도 범주) 응용 프로그램에서 외부 연결을 위한 딥 링크 등의 HTML 콘텐츠를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="c9d9b-185">Hello 아이콘 또는 iOS 배지를 변경할 수 있으며 텍스트 또는 웹 콘텐츠 (html 콘텐츠, URL 링크 tooanother 위치 내부 또는 외부 hello 앱의 팝업)를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="c9d9b-186">Android 장치 링을 만들거나 hello 푸시를 진동 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="c9d9b-187">(있는지 있습니다 됩니다 필요 hello에서 Android SDK 사용 권한 파일 tooring 매니페스트 또는 장치를 진동 올바른 기억 합니다.) 모든 장치에서 화면 크기가 다르므로 현재 Android의 "큰 사진" 크기에 대한 업계 표준은 없지만 거의 모든 화면 크기에서는 400x100 크기의 사진을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="c9d9b-188">배달 유형</span><span class="sxs-lookup"><span data-stu-id="c9d9b-188">Delivery Types:</span></span>
* <span data-ttu-id="c9d9b-189">앱 외부만: hello 사용자 hello 응용 프로그램을 사용 하지 않는 경우 hello 알림이 배달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="c9d9b-190">앱만 알림 부족 hello Apple 또는 Google (GCM 또는 APNS 인증서)에서 발급 한 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="c9d9b-191">앱에서만: hello 알림이 hello 응용 프로그램을 실행 하는 경우에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="c9d9b-192">hello 알림 hello Capptain 전달 시스템 tooreach hello 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="c9d9b-193">Hello 레이아웃/의 시각적 표시 빌드되고 푸시 완전히 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="c9d9b-194">언제 든 지:이 옵션 중 하나가 hello 응용 프로그램의 실행 알림을 보내는 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![도달률 캠페인4][23]

### <a name="option-applies-to"></a><span data-ttu-id="c9d9b-196">옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-196">Option Applies to:</span></span>
* <span data-ttu-id="c9d9b-197">알림: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="c9d9b-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="c9d9b-198">Content</span><span class="sxs-lookup"><span data-stu-id="c9d9b-198">Content</span></span>
<span data-ttu-id="c9d9b-199">공지, 여론 조사, 데이터 푸시 및 타일 (Windows Phone만 해당)의 hello 콘텐츠 섹션 toomodify hello 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="c9d9b-200">푸시 캠페인의 hello 콘텐츠 설정에는 캠페인의 특정 toohello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="c9d9b-201">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c9d9b-201">See also</span></span>
* <span data-ttu-id="c9d9b-202">[UI 설명서 - 도달률 - 푸시 콘텐츠][Link 29]</span><span class="sxs-lookup"><span data-stu-id="c9d9b-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![도달률 캠페인5][24]

## <a name="audience"></a><span data-ttu-id="c9d9b-204">대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-204">Audience</span></span>
<span data-ttu-id="c9d9b-205">Hello Audience 섹션 toodefine 표준 목록이 항목 toolimit 캠페인 또는 사용자 지정 된 기준에 따라 캠페인 제한에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="c9d9b-206">hello 표준 집합이 옵션 tooLimit 청중이 있습니다 toopush tooeither 기존 또는 새 사용자 또는 네이티브 푸시 사용자만.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="c9d9b-207">또한 사용자 받는 hello 푸시 할당량 toolimit hello 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="c9d9b-208">캠페인 필터링 된 tooinclude 방법에 대 한 hello 식을 수동으로 편집할 수 있습니다 하나 이상의 조건 tootarget 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="c9d9b-209">대상 식은 수동으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-209">You can manually type an audience expression.</span></span> <span data-ttu-id="c9d9b-210">이러한 식은 조건 간의 hello 관계를 명시적으로 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="c9d9b-211">기준을 설명하는 식별자는 대문자로 시작해야 하며 공백은 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="c9d9b-212">사용 하 여 hello hello 조건 사이 관계를 설명할 수 있습니다 'and', 'or', 'not' 연산자와 '(',')'입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="c9d9b-213">예: "Criterion1 or (Criterion1 and not Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="c9d9b-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="c9d9b-214">캠페인에 포함 하는 대규모 고객을 사용 하 여 hello 서버 쪽 검색을 대상으로 속도가 느려질 수 있음, 여러 캠페인에 동일한 hello toostart 사용 하려는 경우에 특히 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="c9d9b-215">가능하면 캠페인을 한 번에 하나만 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="c9d9b-216">hello 최대 4 개의 캠페인 한 번에만 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="c9d9b-217">푸시 tooyour 활성 사용자만 ("네이티브 푸시를 사용 하 여 도달할 수 있는 사용자만 참여" checkbox "활성 사용자만 참여" 및) 여전히 hello 앱이 설치를 사용 하는 사용자만 toobe 검색 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="c9d9b-218">대상 그룹에서 정의 되 면 hello를 사용할 수 있습니다 하는 사용자 수를이 푸시 받습니다 아웃 단추 toofind 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="c9d9b-219">이 옵션은 잠재적으로 대상 (이 사용자의 무작위 샘플을 기준으로 추정)이 대상이 그룹으로 알려진된 사용자의 hello 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="c9d9b-220">알아 두어야 하 hello 응용 프로그램을 제거한 사용자도이 대상 그룹에 속하지만 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="c9d9b-221">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c9d9b-221">See also</span></span>
* <span data-ttu-id="c9d9b-222">[UI 설명서 - 도달률 - 새 푸시 기준][Link 28]</span><span class="sxs-lookup"><span data-stu-id="c9d9b-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![도달률 캠페인6][25]

### <a name="edit-expression"></a><span data-ttu-id="c9d9b-224">식 편집</span><span class="sxs-lookup"><span data-stu-id="c9d9b-224">Edit expression</span></span>
![도달률 캠페인7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="c9d9b-226">대상 제한 옵션 적용 대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="c9d9b-227">사용자 하위 집합만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-228">이전 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-229">새 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-230">유휴 사용자만 참여: 알림, 설문 조사, 타일</span><span class="sxs-lookup"><span data-stu-id="c9d9b-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="c9d9b-231">활성 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)</span><span class="sxs-lookup"><span data-stu-id="c9d9b-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="c9d9b-232">네이티브 푸시를 사용하여 연결할 수 있는 사용자만 참여: 알림, 설문 조사</span><span class="sxs-lookup"><span data-stu-id="c9d9b-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="c9d9b-233">시간 프레임</span><span class="sxs-lookup"><span data-stu-id="c9d9b-233">Time Frame</span></span>
<span data-ttu-id="c9d9b-234">Hello 기간 섹션 tooset hello 푸시가 전송 되지 있고 즉시 hello 시간 프레임 빈 toostart hello 캠페인을 그대로 둘 수도 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="c9d9b-235">hello 최종 사용자 표준 시간대를 사용 하 여 시작할 수 있습니다 hello 캠페인 푸시 캠페인에 대 한 hello world 일치 hello 시간 내에 모든 표준 시간대 설정 될 때까지 한 번에 작은 일괄 처리 보내고 아시아의 최종 사용자에 대 한 보다 일찍 하루 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="c9d9b-236">Hello 최종 사용자 표준 시간대를 사용 하 여도 지연이 발생할 수 있습니다 캠페인에 hello 푸시를 시작 하기 전에 hello 전화에서 toorequest hello 시간에 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="c9d9b-237">종료 날짜가 없는 캠페인은 푸시를 로컬로 캐시할 수 있으므로 캠페인을 수동으로 종료한 후에도 푸시가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="c9d9b-238">tooavoid이 동작을 특정 캠페인에 대 한 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="c9d9b-239">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c9d9b-239">See also</span></span>
* <span data-ttu-id="c9d9b-240">[도달률 - 방법 - 예약][Link 3]</span><span class="sxs-lookup"><span data-stu-id="c9d9b-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![도달률 캠페인8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="c9d9b-242">설정 적용 대상</span><span class="sxs-lookup"><span data-stu-id="c9d9b-242">Settings Apply to:</span></span>
* <span data-ttu-id="c9d9b-243">시간 프레임: 알림, 설문 조사, 타일</span><span class="sxs-lookup"><span data-stu-id="c9d9b-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="c9d9b-244">테스트</span><span class="sxs-lookup"><span data-stu-id="c9d9b-244">Test</span></span>
<span data-ttu-id="c9d9b-245">Hello 캠페인을 저장 하기 전에 hello 테스트 섹션 toosend이 푸시 tooyour 자체 테스트 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="c9d9b-246">이 캠페인에 대 한 모든 사용자 지정 언어를 구성한 경우에 각 언어의 hello 푸시를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="c9d9b-247">테스트 장치는 "내 계정"에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="c9d9b-248">푸시 hello 단추를 사용 하는 경우 데이터는 기록 되지 서버 쪽 너무 "test", 실제 푸시 캠페인에 대 한 데이터는 기록만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9d9b-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="c9d9b-249">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c9d9b-249">See also</span></span>
* <span data-ttu-id="c9d9b-250">[UI 설명서 - 내 계정][Link 14]</span><span class="sxs-lookup"><span data-stu-id="c9d9b-250">[UI Documentation - My Account][Link 14]</span></span>

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

