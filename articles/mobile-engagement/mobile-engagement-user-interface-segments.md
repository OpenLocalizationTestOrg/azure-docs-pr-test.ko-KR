---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 세그먼트"
description: "자세한 내용은 방법 toocreate Azure Mobile Engagement를 사용 하 여 사용자가 tooidentify 사용 패턴의 세그먼트를 관리 하 고"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="4c83e-103">어떻게 toocreate 사용자 tooidentify 사용 패턴의 세그먼트를 관리 하 고</span><span class="sxs-lookup"><span data-stu-id="4c83e-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="4c83e-104">이 문서에서는 hello 설명 **세그먼트** hello 탭 **Mobile Engagement** 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="4c83e-105">Hello를 사용 하 여 **Mobile Engagement** 포털 toomonitor 모바일 앱을 관리 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="4c83e-106">hello UI의 hello 세그먼트 섹션 toowork를 hello 응용 프로그램에서 얻을 수 및 hello 세그먼트 API를 통해 액세스할 수도 있는 분석 및 hello 다른 동작에 따라 사용자가 분할에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="4c83e-107">세그먼트는 생성 되 고 hello 최신 분석 정보에 따라 24 시간 마다 된 다시 계산 후 24 시간 동안 먼저 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="4c83e-108">세그먼트의 계산 된 후 "tooday 기록 일" 차트 매일 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="4c83e-109">섹션의 hello **Mobile Engagement** 포털 UI hello 포함 **도움말 표시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="4c83e-110">이 단추 tooget 섹션에 대 한 자세한 컨텍스트 정보를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="4c83e-111">세그먼트 만들기</span><span class="sxs-lookup"><span data-stu-id="4c83e-111">Create Segments</span></span>
<span data-ttu-id="4c83e-112">Hello의 too60 일을 특정 기간에 too10 조건을 바탕으로 세그먼트를 만들 수 있습니다 hello 분석 섹션에서 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="4c83e-113">예를 들어 특정 페이지를 볼 수 있거나 hello 내 앱 내에서 특정 콘텐츠에 대 한 최근 10 일 동안 검색 hello 사람에 따라 세그먼트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="4c83e-114">이 정보는 hello 분석 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="4c83e-115">따라서 toocreate 세그먼트를 사용할 수 있으며 설정한 다음 푸시 알림 tootarget이 사용자가 tooget의 하위이 집합으로 toocome 백 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c83e-116">계산된 세그먼트는 편집할 수 없으며 복제(복사) 또는 소멸(삭제)만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="4c83e-117">Hello 내에서 세그먼트를 복제할 수 있는 동일한 응용 프로그램 (와 동일한 AppID hello), 및 다른 응용 프로그램 (서로 다른 AppID)에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="4c83e-119">예제 세그먼트</span><span class="sxs-lookup"><span data-stu-id="4c83e-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="4c83e-121">세그먼트를 사용 하면 응용 프로그램의 toosegment hello 최종 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="4c83e-122">사용자 구분은 중요한 마케팅 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="4c83e-123">Azure Mobile Engagement tooget 기록 데이터를 허용 하 고 사용자 지정 세그먼트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="4c83e-124">이 강력한 도구를 통해 응용 프로그램에서 고객의 경험에 대 한 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="4c83e-125">또한 세그먼트는 쉽게 분석이 가능하고 푸시 대상으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="4c83e-126">일반적인 사용 사례는 되도록 toosend 푸시 알림 tooencourage 최종 사용자에 게 toorate hello 스토어에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="4c83e-127">알림 tooall 최종 사용자에 게 보내기, 보다 hello 지난 달에 대 한 매일 응용 프로그램을 사용 하 고 유용한 사용자 환경을 했을 수 있는 사용자만 지정 하는 세그먼트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="4c83e-128">이처럼 대상이 자세하게 지정된 더 적은 수의 푸시 알림을 보내면 ROI가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="4c83e-130">만들 수 있습니다 세그먼트 hello 주요 Azure Mobile Engagement 요소 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="4c83e-131">이벤트: 해당 대상으로 한 특정 이벤트 일주일에 두 번 이상 발생 하는 hello 응용 프로그램의 세그먼트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="4c83e-132">세션: hello 5 번 이상 지난 주 응용 프로그램을 사용한 사용자의 세그먼트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="4c83e-133">활동: 지난 달에 특정 페이지나 콘텐츠를 사용한 횟수가 10회 정도인 사용자의 세그먼트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="4c83e-134">작업: 매일 2회 넘게 작업을 완료한 사용자의 세그먼트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="4c83e-135">충돌: 10 배 이상 지난 주 충돌이 발생 한 적이 있는 모든 hello 사용자의 세그먼트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="4c83e-136">이 세그먼트에 대해 사과 메시지나 쿠폰을 푸시로 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="4c83e-137">오류: 이상 100 번 지난 3 일 오류가 적이 있는 모든 hello 사용자의 세그먼트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="4c83e-138">응용 프로그램 정보: 마지막 25 일 hello 동안 수행 된 사용자 지정 앱 정보를 대상으로 하는 세그먼트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="4c83e-140">toouse 세그먼트 최적의 방법으로, 해야에서 수행 했던 hello SDK의 통합을 사용자 지정 된 응용 프로그램 "앱 정보" 태그의 태그 지정 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="4c83e-141">그런 다음 hello 인터페이스의 toohello 홈 페이지를 이동 hello 응용 프로그램을 선택 하 고 hello "세그먼트" 섹션에서을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="4c83e-142">Hello "세그먼트" 섹션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="4c83e-143">Toocreate 새 세그먼트를 단추 하는 hello "새 세그먼트"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="4c83e-144">실제 예: "세션" 정보를 기준으로 간단한 세그먼트 만들기</span><span class="sxs-lookup"><span data-stu-id="4c83e-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="4c83e-145">모든 hello 최종 사용자에 게 앱 50 회 이상에서 사용 hello 지난주의 세그먼트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="4c83e-146">여기에서만 hello 최종 사용자가 세션당 응용 프로그램에서 30 초 이상 투자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="4c83e-147">이 응용 프로그램에서 긍정적인 경험을가지고 있는 모든 hello 최종 사용자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="4c83e-148">그런 다음 생성 hello 세그먼트 사용된 toopush 알림 toothese 최종 사용자에 게 tooask 수에 toorate hello에서 응용 프로그램을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="4c83e-150">세그먼트 이름을 순서 toofind 부여 hello "세그먼트" 목록에서 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="4c83e-151">Hello에 "만들기" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="4c83e-153">세션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="4c83e-155">"지난 주"의 hello 기간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="4c83e-156">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="4c83e-158">선택 hello hello 목록 간에 관련 된 연산자: =; ≥, ≤ 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="4c83e-159">Hello 원하는 횟수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="4c83e-160">Hello 원하는 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="4c83e-161">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-161">Click next.</span></span>
   <span data-ttu-id="4c83e-162">이 예에서는 해당 over hello 지난 주 일치 사용자 최소 50 세션을 적용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="4c83e-164">세션 조각화 hello에 대 한 기준으로 세션당 hello 길이 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="4c83e-165">Hello 연산자 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="4c83e-166">세션당 hello 길이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="4c83e-167">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-167">Click Next.</span></span>
   <span data-ttu-id="4c83e-168">이 예제에서는 모두 hello hello 번째 섹션에 맞춰져 있으며 분할 된 세션에서 선택 하 세션당 30 초 이상 소요한가 hello 사용자만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="4c83e-170">Hello에서 완료 순서 tooretrieve 기준의 이름을 깔때기, 고 마침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="4c83e-172">조건과 설정이 끝난 hello 세그먼트 깔때기형에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="4c83e-173">세그먼트는 분석 데이터를 기준으로 하므로 매일 한 번씩 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="4c83e-174">이 예제에서는 47,7 hello 총 최종 사용자가 %hello 조건과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c83e-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="4c83e-175">Hello 사용자에 게 우수한 환경을 했을 수 있어야 합니다 될 가능성이 tooprovide 알림을 강제 하는 경우 더 높은 등급 나눠 주고 hello 저장소에 toorate hello 앱.</span><span class="sxs-lookup"><span data-stu-id="4c83e-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="4c83e-176">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4c83e-176">See also</span></span>
* <span data-ttu-id="4c83e-177">[개념][Link 6]</span><span class="sxs-lookup"><span data-stu-id="4c83e-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="4c83e-178">[문제 해결 가이드 서비스][Link 24]</span><span class="sxs-lookup"><span data-stu-id="4c83e-178">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

