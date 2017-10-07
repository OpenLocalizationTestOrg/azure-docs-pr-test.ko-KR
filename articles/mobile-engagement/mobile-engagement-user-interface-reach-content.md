---
title: "aaaAzure Mobile Engagement 사용자 인터페이스-콘텐츠 도달"
description: "Azure Mobile Engagement에서 푸시 알림 hello 서로 다른 형식의 toomanage hello 고유한 콘텐츠 캠페인 하는 방법에 대해 알아봅니다"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="7a41d-103">Toomanage 푸시 알림 캠페인의 hello 서로 다른 형식의 콘텐츠를 고유한 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7a41d-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="7a41d-104">공지, 여론 조사, 데이터 푸시 및 타일 (Windows Phone만 해당)는 새로운 reach 캠페인 toomodify hello 콘텐츠 hello 콘텐츠 섹션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="7a41d-105">푸시 캠페인의 hello 콘텐츠 설정에는 캠페인의 특정 toohello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="7a41d-106">콘텐츠 형식:</span><span class="sxs-lookup"><span data-stu-id="7a41d-106">Content types:</span></span>
* <span data-ttu-id="7a41d-107">알림</span><span class="sxs-lookup"><span data-stu-id="7a41d-107">Announcements</span></span>
* <span data-ttu-id="7a41d-108">설문 조사</span><span class="sxs-lookup"><span data-stu-id="7a41d-108">Polls</span></span>
* <span data-ttu-id="7a41d-109">데이터 푸시</span><span class="sxs-lookup"><span data-stu-id="7a41d-109">Data pushes</span></span>
* <span data-ttu-id="7a41d-110">파일(Windows Phone 전용)</span><span class="sxs-lookup"><span data-stu-id="7a41d-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="7a41d-111">알림의 내용</span><span class="sxs-lookup"><span data-stu-id="7a41d-111">Content of Announcements</span></span>
 ![도달률 콘텐츠1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="7a41d-113">공지의 hello 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="7a41d-114">알림 전용: 단순한 표준 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="7a41d-115">사용자가 클릭, 추가 보기 없음 나타나지만 hello 작업만 연결 된 경우 tooit 발생 하는지 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="7a41d-116">텍스트 알림: hello 사용자 toohave 텍스트 보기를 살펴보면 맞물릴 때 알리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="7a41d-117">웹 공지: hello 사용자 toohave 웹 보기를 살펴보면 맞물릴 때 알리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="7a41d-118">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a41d-118">See also</span></span>
* <span data-ttu-id="7a41d-119">[도달률 - 방법 - 알림][Link 3]</span><span class="sxs-lookup"><span data-stu-id="7a41d-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="7a41d-120">웹 뷰 알림 정보</span><span class="sxs-lookup"><span data-stu-id="7a41d-120">About Web View Announcements:</span></span>
<span data-ttu-id="7a41d-121">Hello HTML 코드나 JavaScript 코드 여기에서 제공한에 hello 패턴 "{deviceid}"을 찾아 hello 알림이 표시 hello 장치의 hello 식별자로 자동으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="7a41d-122">이것은 외부에서 프로그램을 쉽게 tooretrieve Azure Mobile Engagement 장치 식별자 웹 백오피스에 호스트 되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="7a41d-123">전체 화면 웹 보기 (hello 기본 작업 및 끝내기 단추 없이 제공) toocreate 하려는 경우 웹 보기 공지의 JavaScript 코드에서 함수를 수행 하는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="7a41d-124">hello 공지 작업 수행: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="7a41d-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="7a41d-125">hello 알림이에서 종료: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="7a41d-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="7a41d-126">작업 선택</span><span class="sxs-lookup"><span data-stu-id="7a41d-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="7a41d-127">작업 URL 정보</span><span class="sxs-lookup"><span data-stu-id="7a41d-127">About Action URLs:</span></span>
<span data-ttu-id="7a41d-128">대상으로 지정된 장치의 운영 체제에서 해석할 수 있는 모든 URL을 작업 URL로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="7a41d-129">응용 프로그램 수 있는 모든 전용 URL (예: toomake 사용자 점프 tooa 특정 화면) 지원 작업 URL로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="7a41d-130">{Deviceid} hello 패턴의 각 항목은 자동으로 hello 동작을 수행 하는 hello 장치의 hello 식별자로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="7a41d-131">이 백오피스에 호스트 된 외부 웹 서비스를 통해 사용 되는 tooeasily Azure Mobile Engagement 장치 식별자를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="7a41d-132">**Android + iOS 작업**</span><span class="sxs-lookup"><span data-stu-id="7a41d-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="7a41d-133">웹 페이지 열기</span><span class="sxs-lookup"><span data-stu-id="7a41d-133">Open a web page</span></span>
  * <span data-ttu-id="7a41d-134">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="7a41d-135">예:http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="7a41d-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="7a41d-136">메일 보내기</span><span class="sxs-lookup"><span data-stu-id="7a41d-136">Send an e-mail</span></span>
  * <span data-ttu-id="7a41d-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="7a41d-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="7a41d-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="7a41d-139">문자 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="7a41d-139">Send a SMS</span></span>
  * <span data-ttu-id="7a41d-140">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="7a41d-141">예: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="7a41d-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="7a41d-142">특정 번호로 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="7a41d-142">Dial a phone number</span></span>
  * <span data-ttu-id="7a41d-143">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="7a41d-144">예: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="7a41d-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="7a41d-145">**Android 전용 작업**</span><span class="sxs-lookup"><span data-stu-id="7a41d-145">**Android only actions**</span></span>
  * <span data-ttu-id="7a41d-146">Hello Play 스토어의 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="7a41d-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="7a41d-147">market://details?id=\[app package\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="7a41d-148">예: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="7a41d-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="7a41d-149">지리적 위치에 따른 검색 시작</span><span class="sxs-lookup"><span data-stu-id="7a41d-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="7a41d-150">geo:0,0?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="7a41d-151">예: geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="7a41d-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="7a41d-152">**iOS 전용 작업**</span><span class="sxs-lookup"><span data-stu-id="7a41d-152">**iOS only actions**</span></span>
  * <span data-ttu-id="7a41d-153">Hello 앱 스토어의 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="7a41d-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="7a41d-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="7a41d-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="7a41d-155">예:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="7a41d-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="7a41d-156">Windows 작업</span><span class="sxs-lookup"><span data-stu-id="7a41d-156">Windows Actions</span></span>
  * <span data-ttu-id="7a41d-157">웹 페이지 열기</span><span class="sxs-lookup"><span data-stu-id="7a41d-157">Open a web page</span></span>
  * <span data-ttu-id="7a41d-158">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="7a41d-159">예:http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="7a41d-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="7a41d-160">메일 보내기</span><span class="sxs-lookup"><span data-stu-id="7a41d-160">Send an e-mail</span></span>
  * <span data-ttu-id="7a41d-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="7a41d-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="7a41d-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="7a41d-163">문자 메시지 보내기(Skype 스토어 앱 필요)</span><span class="sxs-lookup"><span data-stu-id="7a41d-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="7a41d-164">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="7a41d-165">예: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="7a41d-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="7a41d-166">특정 번호로 전화 걸기(Skype 스토어 앱 필요)</span><span class="sxs-lookup"><span data-stu-id="7a41d-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="7a41d-167">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="7a41d-168">예: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="7a41d-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="7a41d-169">Hello Play 스토어의 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="7a41d-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="7a41d-170">ms-windows-store:PDP?PFN=\[app package ID\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="7a41d-171">예: ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="7a41d-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="7a41d-172">Bing 지도 검색 수행</span><span class="sxs-lookup"><span data-stu-id="7a41d-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="7a41d-173">bingmaps:?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="7a41d-174">예: bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="7a41d-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="7a41d-175">사용자 지정 체계 사용</span><span class="sxs-lookup"><span data-stu-id="7a41d-175">Use a custom scheme</span></span>
  * <span data-ttu-id="7a41d-176">\[사용자 지정 체계\]://\[사용자 지정 체계 매개 변수\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="7a41d-177">예: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="7a41d-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="7a41d-178">패키지 데이터 사용(확장명 읽기를 위한 스토어 앱 필요)</span><span class="sxs-lookup"><span data-stu-id="7a41d-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="7a41d-179">\[folder\]\[data\].\[extension\]</span><span class="sxs-lookup"><span data-stu-id="7a41d-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="7a41d-180">예: myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="7a41d-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="7a41d-181">추적 URL 작성</span><span class="sxs-lookup"><span data-stu-id="7a41d-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="7a41d-182">참조의 hello "설정" 섹션을 hello <UI Documentation> 추적 URL을 만드는 지침을 사용 하면 사용자가 toodownload 다른 응용 프로그램 중 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="7a41d-183">공지의 hello 텍스트 정의</span><span class="sxs-lookup"><span data-stu-id="7a41d-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="7a41d-184">Hello 제목, 내용 및 공지의 단추 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="7a41d-185">사용자가 toothis 캠페인 응답 하는 방법의 hello reach 피드백에 따라 이후 캠페인의 대상 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="7a41d-186">대상 그룹 지정 여부이 캠페인만 푸시된, 회신, 조치를 취한, 또는 종료의 hello 피드백에 따라 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="7a41d-187">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a41d-187">See also</span></span>
* <span data-ttu-id="7a41d-188">[UI 설명서 - 도달률 - 새 푸시 기준][Link 28]</span><span class="sxs-lookup"><span data-stu-id="7a41d-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="7a41d-189">설문 조사의 내용</span><span class="sxs-lookup"><span data-stu-id="7a41d-189">Content of Polls</span></span>
![도달률 콘텐츠2][31] 

<span data-ttu-id="7a41d-191">Hello 제목, 설명 및 공지의 단추 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="7a41d-192">질문 및 답변 tooyour 질문 hello에 대 한 가지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="7a41d-193">사용자가 toothis 캠페인 응답 하는 방법의 hello reach 피드백에 따라 이후 캠페인의 대상 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="7a41d-194">이 캠페인에 대한 응답 방법(푸시만, 회신, 작업, 종료)에 따라 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="7a41d-195">대상 그룹은 설문 조사 응답 피드백을 hello 질문 및 대답 선택 조건으로 사용 되는 위치에 기반 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="7a41d-196">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a41d-196">See also</span></span>
* <span data-ttu-id="7a41d-197">[UI 설명서 - 도달률 - 새 푸시 기준][Link 28]</span><span class="sxs-lookup"><span data-stu-id="7a41d-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="7a41d-198">데이터 푸시의 내용</span><span class="sxs-lookup"><span data-stu-id="7a41d-198">Content of Data Pushes</span></span>
![도달률 콘텐츠3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="7a41d-200">데이터의 hello 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="7a41d-201">텍스트</span><span class="sxs-lookup"><span data-stu-id="7a41d-201">Text</span></span>
* <span data-ttu-id="7a41d-202">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="7a41d-202">Binary data</span></span>
* <span data-ttu-id="7a41d-203">Base64 데이터</span><span class="sxs-lookup"><span data-stu-id="7a41d-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="7a41d-204">데이터의 hello 내용 정의</span><span class="sxs-lookup"><span data-stu-id="7a41d-204">Define hello content of your data</span></span>
* <span data-ttu-id="7a41d-205">Toopush 텍스트 데이터를 선택한 경우 복사한 hello 텍스트 hello "콘텐츠" 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="7a41d-206">Toopush를 선택한 경우 데이터를 이진 또는 base64 hello "파일을 업로드 합니다." 단추 tooupload 사용자 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="7a41d-207">사용자가 toothis 캠페인 응답 하는 방법의 hello reach 피드백에 따라 이후 캠페인의 대상 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="7a41d-208">이 캠페인에 대한 응답 방법(푸시만, 회신, 작업, 종료)에 따라 대상을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="7a41d-209">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a41d-209">See also</span></span>
* <span data-ttu-id="7a41d-210">[UI 설명서 - 도달률 - 새 푸시 기준][Link 28]</span><span class="sxs-lookup"><span data-stu-id="7a41d-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="7a41d-211">타일의 내용(Windows Phone 전용)</span><span class="sxs-lookup"><span data-stu-id="7a41d-211">Content of Tiles (Windows Phone only)</span></span>
![도달률 콘텐츠4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="7a41d-213">타일의 hello 내용 정의</span><span class="sxs-lookup"><span data-stu-id="7a41d-213">Define hello content of your tile</span></span>
<span data-ttu-id="7a41d-214">hello 타일 페이로드는 hello 텍스트 toobe Windows Phone 장치에서 앱의 hello 타일에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="7a41d-215">타일 푸시에는 Windows Phone 대 한 네이티브 푸시의 hello Microsoft 푸시 알림 서비스 (MPNS) 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="7a41d-216">hello 타일 푸시 형식은 hello 푸시 유형만 응답 하지 않은 있고 따라서 타일 푸시 캠페인의 hello 결과에 미래의 캠페인의 대상 그룹 hello를 빌드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a41d-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="7a41d-217">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7a41d-217">See also</span></span>
* <span data-ttu-id="7a41d-218">[API 설명서 - 도달률 API - 네이티브 푸시][Link 4]</span><span class="sxs-lookup"><span data-stu-id="7a41d-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

