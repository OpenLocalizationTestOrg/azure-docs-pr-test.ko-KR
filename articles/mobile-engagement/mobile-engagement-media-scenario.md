---
title: "미디어 앱에 대한 Azure Mobile Engagement 구현"
description: "Azure Mobile Engagement 구현을 위한 미디어 앱 시나리오"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c1591c3e436981e621830916cf0cdc4b7f395d7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a><span data-ttu-id="b1590-103">미디어 앱에 Mobile Engagement 구현</span><span class="sxs-lookup"><span data-stu-id="b1590-103">Implement Mobile Engagement with Media App</span></span>
## <a name="overview"></a><span data-ttu-id="b1590-104">개요</span><span class="sxs-lookup"><span data-stu-id="b1590-104">Overview</span></span>
<span data-ttu-id="b1590-105">John은 큰 미디어 회사의 모바일 프로젝트 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-105">John is a mobile project manager for a big media company.</span></span> <span data-ttu-id="b1590-106">최근에 새로운 앱을 출시했는데 다운로드 수가 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-106">He recently launched a new app that has a very high download count.</span></span> <span data-ttu-id="b1590-107">다운로드 목표는 달성했지만 사용자당 투자 수익률(ROI)은 필요 조건을 충족하지 못하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-107">He has hit his goals for download but, still his Return On Investment(ROI) per user does not meet his requirements.</span></span> 

<span data-ttu-id="b1590-108">John은 이미 ROI가 너무 낮은 이유를 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-108">John has already identified why his ROI is too low.</span></span> <span data-ttu-id="b1590-109">사용자들이 앱 사용을 2주 후에 중단하는 경우가 빈번하고 이들 중 대부분이 다시 돌아오지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-109">Users frequently stop using his app after only 2 weeks and most of them never come back.</span></span> <span data-ttu-id="b1590-110">그는 앱에 대한 재방문 주기를 높이고 싶어합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-110">He wants to increase the retention of his app.</span></span>

<span data-ttu-id="b1590-111">초기 테스트를 통해 사용자에게 푸시 알림을 사용하면 계속해서 앱을 사용하는 경향이 있다는 것을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-111">After some initial testing, he has learned when he engages his users with push notifications, they tend to continue using his app.</span></span> <span data-ttu-id="b1590-112">또한 사용자에게 보내는 알림에 따라서 비활성 사용자가 앱으로 돌아오는 경우가 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-112">Also users that were inactive will often return to the app depending on notifications he sends them.</span></span> <span data-ttu-id="b1590-113">John은 앱을 위해서 푸시 알림을 통한 고급 타기팅을 사용하는 일종의 Engagement  프로그램에 투자하기로 결심합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-113">John decides to invest in some kind of Engagement Program for his app which uses advanced targeting with push notifications.</span></span>

<span data-ttu-id="b1590-114">John은 최근에 [Azure Mobile Engagement - 모범 사례 시작 가이드](mobile-engagement-getting-started-best-practices.md) 를 읽고 난 후 가이드에 포함된 권장 사항을 구현하기로 결심합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-114">John has recently read the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) and has decided to implement the recommendations from the guide.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="b1590-115">목표 및 KPI</span><span class="sxs-lookup"><span data-stu-id="b1590-115">Objectives and KPIs</span></span>
<span data-ttu-id="b1590-116">John의 앱에 대한 주요 관련자</span><span class="sxs-lookup"><span data-stu-id="b1590-116">Key stakeholders for John's app meet.</span></span> <span data-ttu-id="b1590-117">사용자가 미디어를 소비하면 광고를 통해 수입이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-117">Business is generated from ads as users consume his media.</span></span> <span data-ttu-id="b1590-118">사용자당 소비되는 콘텐츠를 증가시키면 John의 수익도 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-118">By increasing content consumed per user, John increases his revenues.</span></span> <span data-ttu-id="b1590-119">광고를 통해 매출을 25%까지 높인다는 한 가지 주요 목표에 모두 동의합니다. </span><span class="sxs-lookup"><span data-stu-id="b1590-119">All agree on one main objective: To increase sales from ads by 25%.</span></span> <span data-ttu-id="b1590-120">이들은 목표를 평가하고 진행하기 위해서 비즈니스 KPI(핵심 성과 지표)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-120">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="b1590-121">사용자당 클릭한 광고 수</span><span class="sxs-lookup"><span data-stu-id="b1590-121">Number of ads clicked per user</span></span>
* <span data-ttu-id="b1590-122">방문한 페이지 수(사용자별/세션별/주별/월별)</span><span class="sxs-lookup"><span data-stu-id="b1590-122">How many article pages visited (per user/ per session/ per week / per month…)</span></span>
* <span data-ttu-id="b1590-123">즐겨찾는 범주는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b1590-123">What are favorite categories</span></span>

<span data-ttu-id="b1590-124">John은 주요 관련자들과의 회의에 근거하여 비즈니스 KPI를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-124">Based on John's meeting with key stakeholders he has defined his Business KPIs.</span></span> <span data-ttu-id="b1590-125">그는 [Azure Mobile Engagement - 모범 사례 시작 가이드](mobile-engagement-getting-started-best-practices.md)의 1 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-125">He follows Part 1 of the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md).</span></span> 

<span data-ttu-id="b1590-126">그 후, 목표가 확실히 달성될 수 있도록 다음과 같은 Engagement KPI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-126">Next, he creates the following Engagement KPIs to ensure that objectives are reached:</span></span>

* <span data-ttu-id="b1590-127">하루, 일주일, 2주일, 한달 간격으로 재방문 주기 모니터링</span><span class="sxs-lookup"><span data-stu-id="b1590-127">Monitor retention across the following intervals: daily, weekly, bi-weekly and monthly.</span></span>
* <span data-ttu-id="b1590-128">활성 사용자 수</span><span class="sxs-lookup"><span data-stu-id="b1590-128">Active users counts</span></span>
* <span data-ttu-id="b1590-129">앱 스토어의 앱 순위 평가</span><span class="sxs-lookup"><span data-stu-id="b1590-129">The app rating in the app stores</span></span>

<span data-ttu-id="b1590-130">IT 팀의 권고에 따라 다음 질문에 답하기 위해 다음과 같은 기술 KPI가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-130">Based on recommendations from the IT team, the following Technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="b1590-131">사용자 경로(방문한 페이지, 사용자가 이곳에서 보낸 시간)</span><span class="sxs-lookup"><span data-stu-id="b1590-131">What is my user path (which page is visited, how many time users spend on it)</span></span>
* <span data-ttu-id="b1590-132">세션당 발생한 충돌 수 또는 버그 수</span><span class="sxs-lookup"><span data-stu-id="b1590-132">Number of crashes or bugs encountered per session?</span></span>
* <span data-ttu-id="b1590-133">사용자가 실행하는 OS 버전</span><span class="sxs-lookup"><span data-stu-id="b1590-133">What OS versions are my users running?</span></span>
* <span data-ttu-id="b1590-134">사용자의 평균 화면 크기</span><span class="sxs-lookup"><span data-stu-id="b1590-134">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="b1590-135">사용자가 사용하는 인터넷 연결 종류</span><span class="sxs-lookup"><span data-stu-id="b1590-135">What kind of internet connections do my users have?</span></span>

<span data-ttu-id="b1590-136">그는 각 KPI에 대해 필요한 데이터를 분류하고 플레이 북의 적절한 위치에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-136">For each KPI, he classifies the data required and he records it in the proper location of his playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="b1590-137">Engagement 프로그램 및 통합</span><span class="sxs-lookup"><span data-stu-id="b1590-137">Engagement program and integration</span></span>
<span data-ttu-id="b1590-138">John은 KPI 정의를 완료한 후에 4개의 Engagement 프로그램과 목표를 정의하여 Engagement 전략 단계를 시작합니다.![][1]</span><span class="sxs-lookup"><span data-stu-id="b1590-138">Now that John has finished defining his KPIs, he starts his Engagement strategy phase by defining 4 engagement programs and their objectives: ![][1]</span></span>

<span data-ttu-id="b1590-139">John은 각 프로그램에 대한 푸시 알림을 자세히 열거하면서 깊이 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-139">Then John goes deeper by detailing push notifications for each program.</span></span> <span data-ttu-id="b1590-140">푸시 알림은 다섯 가지 요소로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-140">Push notification are defined by five elements:</span></span>

1. <span data-ttu-id="b1590-141">목표: 알림의 목표</span><span class="sxs-lookup"><span data-stu-id="b1590-141">Objective: what is the objective of the notification</span></span>
2. <span data-ttu-id="b1590-142">목표를 달성하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1590-142">How the objective will be reached</span></span>
3. <span data-ttu-id="b1590-143">대상: 알림을 수신하는 사람</span><span class="sxs-lookup"><span data-stu-id="b1590-143">Target: who will receive the notification?</span></span>
4. <span data-ttu-id="b1590-144">콘텐츠: 알림 단어 선택 및 서식(앱 내부/앱 외부)</span><span class="sxs-lookup"><span data-stu-id="b1590-144">Content: What is the wording and the format of the notification (In App/Out of App)</span></span>
5. <span data-ttu-id="b1590-145">시기: 푸시 알림을 보내기에 가장 적합한 순간</span><span class="sxs-lookup"><span data-stu-id="b1590-145">When: what is the best moment to send this push notification</span></span>
   
    ![][2]

<span data-ttu-id="b1590-146">자세한 내용은 [플레이 북](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1590-146">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).</span></span>

<span data-ttu-id="b1590-147">백서의 2 단계에 따라서 John은 대상 섹션을 사용하여 수집해야 하는 데이터가 무엇인지를 정의하고 솔루션을 구현하기 위하여 IT 팀과 공동으로 태그 계획을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-147">According to the part 2 of the white paper John uses target section to define what data he has to collect and writes his Tag Plan jointly with IT team to implement the solution.</span></span> <span data-ttu-id="b1590-148">구현 1주일 후, 사용자 승인 테스트 후에 John은 드디어 프로그램을 출시할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-148">After 1 week of implementation and user acceptance testing, John can finally launch his programs.</span></span>

## <a name="program-results"></a><span data-ttu-id="b1590-149">프로그램 결과</span><span class="sxs-lookup"><span data-stu-id="b1590-149">Program Results</span></span>
<span data-ttu-id="b1590-150">4개월 후 John은 프로그램의 성과를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-150">4 months later, John reviews performances of programs.</span></span> <span data-ttu-id="b1590-151">Welcome Program과 Weekly Program은 목표를 달성하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-151">The Welcome Program and the Weekly Program are meeting his goals.</span></span> <span data-ttu-id="b1590-152">한 세션만 사용하는 사용자 수는 감소되었고, 앱의 기능이 더 많이 사용되고 있으며 주별 연결 수는 두 배가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-152">The number of user with only one session decreases, more features of the app are being used and the number of connections per week has doubled.</span></span>

<span data-ttu-id="b1590-153">**Inactive Program** 은 John이 사용자 성향을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-153">The **Inactive Program** is helping John understand user tendencies.</span></span> <span data-ttu-id="b1590-154">비활성 사용자의 15%는 앱에 다시 돌아오는 것으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-154">It appears that 15% of the inactive users come back to the app.</span></span> <span data-ttu-id="b1590-155">하지만 이들 대부분이 1달 이상 활성 상태를 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-155">However most of them don’t stay active more than 1 month.</span></span> <span data-ttu-id="b1590-156">John은 알림을 추가하고 콘텐츠 선택 범위를 확장하여 이렇게 반복되는 상황을 잠재적으로 최적화할 수 있다고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-156">John foresees a potential optimization of this sequence with additional notifications and expanding his content choices.</span></span>

<span data-ttu-id="b1590-157">**Discover Program** 은 성과가 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-157">The **Discover Program** doesn’t work well.</span></span> <span data-ttu-id="b1590-158">교차 판매는 증가시켰지만 목표를 달성하기에는 부족합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-158">It increases cross selling but not enough to reach his objectives.</span></span> <span data-ttu-id="b1590-159">John은 적절한 타기팅을 진행하기에는 데이터가 부족하다는 점을 파악하고 적절한 콘텐츠를 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-159">John identifies that he doesn’t have enough data to make relevant targeting and propose appropriate content.</span></span> <span data-ttu-id="b1590-160">이 프로그램을 중지하고 Azure Mobile Engagement를 사용하여 “사설 푸시 알림”을 전송하는 것에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-160">He stops this program and focuses on sending “editorial push notifications” with Azure Mobile Engagement.</span></span> <span data-ttu-id="b1590-161">작가는 푸시 알림을 보내기 위한 CMS 솔루션을 이미 가지고 있으며 이것을 바꾸려고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-161">His journalists already have a CMS solution to send push notifications and they don’t want to change.</span></span>

<span data-ttu-id="b1590-162">John은 AZME 웹 인터페이스를 사용하지 않고도 도달률 캠페인을 관리할 수 있는 HTTP REST API인 도달률 API를 사용하기로 결심합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-162">John decides to use the Reach API which is an HTTP REST API that allows managing Reach campaigns without having to use AZME Web interface.</span></span> <span data-ttu-id="b1590-163">이 방식을 사용하면 John은 필요한 데이터를 수집할 수 있고 작가는 CMS 솔루션을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-163">With this approach John can collect the data he needs and allow his writers to keep using the CMS solution.</span></span>

<span data-ttu-id="b1590-164">기능이 제대로 작동하도록 하기 위해서 John은 IT 팀에게 다음과 같은 점에 계속 주목하도록 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-164">To ensure that feature works correctly, John asks IT team to be vigilant on the following points:</span></span>

1. <span data-ttu-id="b1590-165">**운영 체제** : 각자 푸시 알림을 관리하는 자신만의 규칙이 있기 때문에 John은 모든 케이스를 목록으로 모아서 API가 해당 케이스를 처리하는지 확인하기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-165">**Operation Systems** : They all have their own rules to administrate push notifications, so John decides to list all cases and checks if the APIs handle it.</span></span>
   <span data-ttu-id="b1590-166">예를 들어, Android 푸시 시스템은 전체적인 그림이 가능하지만 iOS의 경우는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-166">E.g : Android push system allows big picture which is not the case with iOS.</span></span>
2. <span data-ttu-id="b1590-167">**시간 프레임**: John은 캠페인에 시간 프레임을 설정하고 끝을 설정하는 API를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-167">**Time frame**: John wants an API, which set the time frame and set an end to campaigns.</span></span> <span data-ttu-id="b1590-168">사용자에게 지장을 줄 정도로 알림을 많이 보내지 않기를 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-168">He wants to preserve users from any disruptive notification bombing.</span></span>
3. <span data-ttu-id="b1590-169">**범주**: 마케팅 팀은 각각의 경고 유형에 대한 템플릿을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-169">**Categories**: Marketing team prepares template for each type of alerting.</span></span> <span data-ttu-id="b1590-170">John은 IT 팀에게 API 내부에 범주를 설정하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-170">John asks IT team to set categories inside the API.</span></span>

<span data-ttu-id="b1590-171">테스트를 거친 후에 John은 만족하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-171">After some tests John is satisfied.</span></span> <span data-ttu-id="b1590-172">API 덕분에 작가들은 자신의 CMS를 사용하여 푸시 알림을 보낼 수 있고 Azure Mobile Engagement는 이들의 동작 데이터를 모두 수집할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-172">Thanks to this API, journalists can still send push notifications with their CMS and Azure Mobile Engagement collects all behavioral data for them</span></span>

<span data-ttu-id="b1590-173">초반 4개월이 지난 후에, 전반적으로 만족할만한 성과가 결과에 반영되었고, John과 이사회는 확신을 갖게 되었으며, 사용자당 ROI가 15% 증가하고 모바일 매출이 총 매출의 17.5 %를 차지하면서 단 4개월 만에 7.5%가 증가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1590-173">After these 4 first months, results reflect a good overall performance and gives confidence for John and his board, ROI per user increases per 15% and mobile sales represent 17.5 % of total sales, an increase of 7.5% in only four months.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
