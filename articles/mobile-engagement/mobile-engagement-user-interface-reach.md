---
title: "Mobile Engagement 사용자 인터페이스 Reach aaaAzure"
description: "자세한 방법을 tooreach toohello 사용자가 Azure Mobile Engagement를 사용 하 여 푸시 알림 응용 프로그램의"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="e7e0b-103">어떻게 tooreach toohello 사용자가 푸시 알림 응용 프로그램의</span><span class="sxs-lookup"><span data-stu-id="e7e0b-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="e7e0b-104">이 문서에서는 hello 설명 **도달** hello 탭 **Mobile Engagement** 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="e7e0b-105">Hello를 사용 하 여 **Mobile Engagement** 포털 toomonitor 모바일 앱을 관리 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="e7e0b-106">먼저 toocreate hello 포털을 사용 하 여 해당 toostart 참고는 **Azure Mobile Engagement** 계정.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="e7e0b-107">자세한 내용은 [Azure Mobile Engagement 계정 만들기](mobile-engagement-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="e7e0b-108">hello는 hello 푸시 캠페인 관리 도구 만들기/편집/활성화/완료/모니터를 수행할 수 있는 UI는 hello의 섹션에 도달 하 고 푸시 알림 캠페인 및 hello Reach API (및 hello 낮은의 일부 요소를 통해 액세스할 수 있는 기능에 대 한 통계 가져오기 수준 푸시 API)입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="e7e0b-109">Hello Api 또는 hello UI 사용 하는 여부 toointegrate 필요는 Azure Mobile Engagement와 hello 사용 하려면 먼저 SDK로 각 플랫폼에 대 한 응용 프로그램에 Reach 캠페인에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="e7e0b-110">섹션의 hello **Mobile Engagement** 포털 UI hello 포함 **도움말 표시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="e7e0b-111">이 단추 tooget 섹션에 대 한 자세한 컨텍스트 정보를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="e7e0b-112">4가지 푸시 알림 유형</span><span class="sxs-lookup"><span data-stu-id="e7e0b-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="e7e0b-113">공지 사항-내 응용 프로그램 또는 toosend tooanother 위치를 리디렉션하는 toosend 광고 메시지 toousers 허용을 tooa 웹 페이지 또는 응용 프로그램 외부에서 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="e7e0b-114">-설문에 질문 하 여 toogather 정보를 최종 사용자가 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="e7e0b-115">데이터 푸시-toosend 이진 또는 base64 데이터 파일을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="e7e0b-116">데이터 푸시에 포함 된 hello 정보는 응용 프로그램에서 사용자의 현재 환경과 tooyour 응용 프로그램 toomodify를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="e7e0b-117">응용 프로그램 데이터 푸시의 toobe 수 tooprocess hello 데이터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="e7e0b-118">캠페인 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e7e0b-118">Campaign Details</span></span>
<span data-ttu-id="e7e0b-119">또는 tooopen 클릭할 수 있는 편집, 복제, 삭제 또는 활성화 되지 아직 이름 위로 이동 하 여 캠페인을 활성화할 수 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="e7e0b-120">이름 위로 이동 하 여 활성화 된 캠페인을 복제할 수 있습니다 또는 tooopen 클릭할 수 있는 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="e7e0b-121">그러나 활성화된 캠페인은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="e7e0b-123">도달률 피드백</span><span class="sxs-lookup"><span data-stu-id="e7e0b-123">Reach Feedback</span></span>
<span data-ttu-id="e7e0b-124">클릭 **통계** Reach 캠페인의 toosee hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="e7e0b-125">hello **간단한** 보기 hello 형태의 캠페인이 활성화 된 후 변경 사항에 대 한 열 막대 그래프의 시각적 표현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="e7e0b-126">hello **고급** 보기 hello 푸시 캠페인에 대 한 보다 세부적인 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="e7e0b-127">이러한 세부 정보를 보내는 경우 테스트 캠페인, 즉 밀어넣기 보낸된 tooa 테스트 장치를 사용할 수 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="e7e0b-128">이러한 세부 정보를 해석해야 하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="e7e0b-129">**푸시** -이 hello toohello 장치에 푸시된 메시지 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="e7e0b-130">이 숫자는 hello 푸시 캠페인을 만드는 동안 지정한 hello 대상에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="e7e0b-131">모든 대상 사용자를 지정 하지 않으면이 푸시 tooall hello 등록 된 장치 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="e7e0b-132">다른 모든 푸시 서비스와 마찬가지로 우리 누르지 마십시오 hello 알림을 toohello 장치 직접 대신 toohello 해당 플랫폼 푸시 하지만 특정 푸시 알림 서비스 (PNS-APNS/GCM/WNS) toohello 장치 hello 알림을 제공할 수 있기를 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="e7e0b-133">**배달** -으로 Mobile Engagement SDK가 메시지를 성공적으로 hello PNS toohello 장치에 의해 전달 되 고 승인 hello 수를 지정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="e7e0b-134">*전송됨 수가 푸시됨 수 보다 작은 이유:*</span><span class="sxs-lookup"><span data-stu-id="e7e0b-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="e7e0b-135">Hello 사용자가 hello 장치에서 hello 앱을 제거 하지만 hello PNS 알지 못하기 म ध hello 푸시 toohello PNS hello 시 hello 메시지 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="e7e0b-136">Hello 장치 hello 앱에 표시 되지만 hello 장치 자체 오랜 시간 동안 오프 라인 상태 였던 hello PNS이 실패 합니다 toodeliver hello 메시지 toohello 장치.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="e7e0b-137">Hello 메시지 배달 toohello 장치는 hello 응용 프로그램에서 Mobile Engagement SDK hello hello hello 메시지 내용을 인식 하지 못하는 경우, 해당 메시지를 삭제 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="e7e0b-138">Hello 알림 hello 응용 프로그램에서 사용자 지정 hello hello SDK 및 drop hello 메시지에 예외를 catch를 생성 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="e7e0b-139">Hello 장치에서 앱 hello 경우 hello 플랫폼에서 보낸 hello 수 toounderstand hello 최신 버전의 hello 푸시 메시지는 Mobile Engagement SDK의 버전을 사용 하지만이 hello 앱 hello 알림 후 업그레이드 된 경우에 발생도 발생할 수 있습니다. hello s 서비스 플랫폼에서 디스패치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="e7e0b-140">hello **고급** 탭 손실 된 메시지 수 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="e7e0b-141">IOS 장치에서 메시지 경우가 않습니다 배달 되지 중 하나가 hello 장치의 된 배터리 부족 또는 hello 앱이 원격 알림을 처리할 때 상당한 양의 power 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="e7e0b-142">이것이 hello iOS 장치는 한계입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="e7e0b-143">**표시** -이 메시지에 표시 되는 성공적으로 toohello 응용 프로그램 사용자의 hello 알림 센터의 푸시/아웃-의-응용 프로그램 시스템 알림 또는 hello 내에서 앱에서 알림을 hello 형태로 hello 장치에서 모바일 hello 수를 지정 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="e7e0b-144">hello **고급** 탭 알려 개수 시스템 알림 값과 개수 않은 앱에서 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="e7e0b-145">*표시 된 이유 (대기 toobe 표시) Delivered 수보다 작지 계산*</span><span class="sxs-lookup"><span data-stu-id="e7e0b-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="e7e0b-146">Hello 알림 캠페인 종료 날짜에 hello 알림이 전달 않았습니다 있지만 hello 시간 tooopen를 제공 하는 경우에이 되었고 toohello 응용 프로그램 사용자 표시를 하는 경우 표시 되지 않은 되므로 만료 이미 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="e7e0b-147">Hello 알림이 앱에 알림 이면 hello 알림은 hello 앱 사용자가 hello 앱을 열 때 표시만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="e7e0b-148">Hello 응용 프로그램 사용자 hello 앱을 열지 않았습니다 경우에서 hello SDK hello 알림을 전달 되었지만 아직 hello 앱을 열 때까지 표시를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="e7e0b-149">Hello 알림이 앱에 알림 구성과 toobe 배달 될 hello 알림을 보고 될도 특정 활동/화면에 표시 되지만 배달 될 때까지 아직 hello 사용자는 특정 화면에 hello 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="e7e0b-150">**사용자 상호 작용** -이 메시지는 hello 응용 프로그램 사용자와 상호 작용에 조치를 취 했거나 종료 된 요소인 hello 메시지가 포함 됩니다 hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="e7e0b-151">*hello 응용 프로그램 사용자 동작 hello 같은 방법으로 다음 중 하나에 알림을 수행할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="e7e0b-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="e7e0b-152">Hello 알림 시스템/아웃-의-응용 프로그램 알림 또는 앱 내 알림이 전송 알림 전용으로 경우 hello 앱 사용자가 hello 알림을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="e7e0b-153">Hello 알림을은 텍스트 또는 웹 보기는 앱에서 알림 또는 여론 조사 후 응용 프로그램 사용자를 환영 하는 경우 hello hello 알림이 실행 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="e7e0b-154">앱에서 알림을 웹 보기와 다음 hello 웹 보기 [Android 에서만] URL에 대 한 응용 프로그램 사용자 클릭 hello hello 알림이 하는 경우</span><span class="sxs-lookup"><span data-stu-id="e7e0b-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="e7e0b-155">*hello 응용 프로그램 사용자 중 한 가지 방법으로 다음 hello 알림이 종료 될 수 있습니다.:*</span><span class="sxs-lookup"><span data-stu-id="e7e0b-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="e7e0b-156">직접 hello 알림 hello 닫기 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="e7e0b-157">외출 넘기기가 또는 hello 알림을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="e7e0b-158">텍스트/웹 콘텐츠 및 여론을 사용 하 여 앱에서 알림을 일반적으로 표시 된 toohello 응용 프로그램 사용자는 두 단계로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="e7e0b-159">알림이 먼저 표시 하 고 hello 후속 폴링/텍스트/웹 콘텐츠 표시에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="e7e0b-160">hello 응용 프로그램 사용자 수에서 이러한 단계 중 하나를 종료 하 고 hello 고급 뷰에서 hello 세부 정보를 캡처하여이 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="e7e0b-161">**조치를 취한** -이 hello 했어야 hello 응용 프로그램 사용자가 명시적으로 조치를 취한 메시지 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="e7e0b-162">이렇게 하면 응용 프로그램 사용자 수에서 hello 알림을 푸시할 hello 메시지에 의해 interested 된 대로 hello 가장 흥미로운 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="e7e0b-163">IOS 및 Windows 플랫폼 hello 사용자에 앱을 열어 hello 및 hello 캠페인은 "언제 든 지" 캠페인 hello에 표시 되 앱과 앱에서 알림을 둘 다 수 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="e7e0b-164">표시 된 개수 hello Delivered 보다 높은 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="e7e0b-165">Hello 사용자 상호 작용 또는 작업 hello 알림이 다음에 hello 사용자 상호 작용/Actioned 개수 Delivered 보다 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e0b-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="e7e0b-167">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e7e0b-167">See also</span></span>
* <span data-ttu-id="e7e0b-168">[개념][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e7e0b-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="e7e0b-169">[문제 해결 가이드 서비스][Link 24]</span><span class="sxs-lookup"><span data-stu-id="e7e0b-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

