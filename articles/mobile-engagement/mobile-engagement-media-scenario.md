---
title: "미디어 응용 프로그램에 대 한 aaaAzure Mobile Engagement 구현"
description: "미디어 응용 프로그램 시나리오 tooimplement Azure Mobile Engagement"
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
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a><span data-ttu-id="ba719-103">미디어 앱에 Mobile Engagement 구현</span><span class="sxs-lookup"><span data-stu-id="ba719-103">Implement Mobile Engagement with Media App</span></span>
## <a name="overview"></a><span data-ttu-id="ba719-104">개요</span><span class="sxs-lookup"><span data-stu-id="ba719-104">Overview</span></span>
<span data-ttu-id="ba719-105">John은 큰 미디어 회사의 모바일 프로젝트 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-105">John is a mobile project manager for a big media company.</span></span> <span data-ttu-id="ba719-106">최근에 새로운 앱을 출시했는데 다운로드 수가 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-106">He recently launched a new app that has a very high download count.</span></span> <span data-ttu-id="ba719-107">다운로드 목표는 달성했지만 사용자당 투자 수익률(ROI)은 필요 조건을 충족하지 못하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-107">He has hit his goals for download but, still his Return On Investment(ROI) per user does not meet his requirements.</span></span> 

<span data-ttu-id="ba719-108">John은 이미 ROI가 너무 낮은 이유를 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-108">John has already identified why his ROI is too low.</span></span> <span data-ttu-id="ba719-109">사용자들이 앱 사용을 2주 후에 중단하는 경우가 빈번하고 이들 중 대부분이 다시 돌아오지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-109">Users frequently stop using his app after only 2 weeks and most of them never come back.</span></span> <span data-ttu-id="ba719-110">그의 응용 프로그램의 tooincrease hello 보존을 하고자 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-110">He wants tooincrease hello retention of his app.</span></span>

<span data-ttu-id="ba719-111">몇 가지 초기 테스트를 마친 후 그이 알고 그의 사용자가 일어났거나 그 toocontinue 자신의 응용 프로그램을 사용 하 여 푸시 알림 광범위 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-111">After some initial testing, he has learned when he engages his users with push notifications, they tend toocontinue using his app.</span></span> <span data-ttu-id="ba719-112">또한 활성화 하지 않은 사용자가는 종종 알림 보내 그에 따라 toohello 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-112">Also users that were inactive will often return toohello app depending on notifications he sends them.</span></span> <span data-ttu-id="ba719-113">이한일은 푸시 알림 고급 대상 지정을 사용 하 여 자신의 앱에 대 한 tooinvest Engagement 프로그램의 일부 종류에서를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-113">John decides tooinvest in some kind of Engagement Program for his app which uses advanced targeting with push notifications.</span></span>

<span data-ttu-id="ba719-114">이한일은 hello 읽기 최근에 [Azure Mobile Engagement 설명서와 모범 사례](mobile-engagement-getting-started-best-practices.md) 및 hello 가이드에서 tooimplement hello 권장 사항을 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-114">John has recently read hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) and has decided tooimplement hello recommendations from hello guide.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="ba719-115">목표 및 KPI</span><span class="sxs-lookup"><span data-stu-id="ba719-115">Objectives and KPIs</span></span>
<span data-ttu-id="ba719-116">John의 앱에 대한 주요 관련자</span><span class="sxs-lookup"><span data-stu-id="ba719-116">Key stakeholders for John's app meet.</span></span> <span data-ttu-id="ba719-117">사용자가 미디어를 소비하면 광고를 통해 수입이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-117">Business is generated from ads as users consume his media.</span></span> <span data-ttu-id="ba719-118">사용자당 소비되는 콘텐츠를 증가시키면 John의 수익도 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-118">By increasing content consumed per user, John increases his revenues.</span></span> <span data-ttu-id="ba719-119">하나의 기본 목표에 동의 하는 모든: 25% 씩 광고에서 tooincrease 판매 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-119">All agree on one main objective: tooincrease sales from ads by 25%.</span></span> <span data-ttu-id="ba719-120">만들 비즈니스 핵심 성과 지표 (Kpi) toomeasure 및 드라이브이 목표</span><span class="sxs-lookup"><span data-stu-id="ba719-120">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="ba719-121">사용자당 클릭한 광고 수</span><span class="sxs-lookup"><span data-stu-id="ba719-121">Number of ads clicked per user</span></span>
* <span data-ttu-id="ba719-122">방문한 페이지 수(사용자별/세션별/주별/월별)</span><span class="sxs-lookup"><span data-stu-id="ba719-122">How many article pages visited (per user/ per session/ per week / per month…)</span></span>
* <span data-ttu-id="ba719-123">즐겨찾는 범주는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ba719-123">What are favorite categories</span></span>

<span data-ttu-id="ba719-124">John은 주요 관련자들과의 회의에 근거하여 비즈니스 KPI를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-124">Based on John's meeting with key stakeholders he has defined his Business KPIs.</span></span> <span data-ttu-id="ba719-125">그 뒤에 오는 hello의 1 부 [Azure Mobile Engagement 설명서와 모범 사례](mobile-engagement-getting-started-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-125">He follows Part 1 of hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md).</span></span> 

<span data-ttu-id="ba719-126">다음으로, 그 다음 목표에 도달 하면 Engagement Kpi tooensure hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-126">Next, he creates hello following Engagement KPIs tooensure that objectives are reached:</span></span>

* <span data-ttu-id="ba719-127">보존 간격 뒤 hello 모니터링: 매일, 매주, 격주 및 월별 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-127">Monitor retention across hello following intervals: daily, weekly, bi-weekly and monthly.</span></span>
* <span data-ttu-id="ba719-128">활성 사용자 수</span><span class="sxs-lookup"><span data-stu-id="ba719-128">Active users counts</span></span>
* <span data-ttu-id="ba719-129">hello 앱 등급 hello 응용 프로그램에서 저장</span><span class="sxs-lookup"><span data-stu-id="ba719-129">hello app rating in hello app stores</span></span>

<span data-ttu-id="ba719-130">다음 기술 Kpi hello hello IT 팀의에서 권장 사항에 따라, 질문 다음 tooanswer hello가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-130">Based on recommendations from hello IT team, hello following Technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="ba719-131">사용자 경로(방문한 페이지, 사용자가 이곳에서 보낸 시간)</span><span class="sxs-lookup"><span data-stu-id="ba719-131">What is my user path (which page is visited, how many time users spend on it)</span></span>
* <span data-ttu-id="ba719-132">세션당 발생한 충돌 수 또는 버그 수</span><span class="sxs-lookup"><span data-stu-id="ba719-132">Number of crashes or bugs encountered per session?</span></span>
* <span data-ttu-id="ba719-133">사용자가 실행하는 OS 버전</span><span class="sxs-lookup"><span data-stu-id="ba719-133">What OS versions are my users running?</span></span>
* <span data-ttu-id="ba719-134">내 사용자를 위해 화면의 평균 크기 hello 이란?</span><span class="sxs-lookup"><span data-stu-id="ba719-134">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="ba719-135">사용자가 사용하는 인터넷 연결 종류</span><span class="sxs-lookup"><span data-stu-id="ba719-135">What kind of internet connections do my users have?</span></span>

<span data-ttu-id="ba719-136">각 KPI에 대 한 필요한 hello 데이터를 분류 하는 그 및 그의 플레이 북의 hello 적절 한 위치에 기록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-136">For each KPI, he classifies hello data required and he records it in hello proper location of his playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="ba719-137">Engagement 프로그램 및 통합</span><span class="sxs-lookup"><span data-stu-id="ba719-137">Engagement program and integration</span></span>
<span data-ttu-id="ba719-138">John은 KPI 정의를 완료한 후에 4개의 Engagement 프로그램과 목표를 정의하여 Engagement 전략 단계를 시작합니다.![][1]</span><span class="sxs-lookup"><span data-stu-id="ba719-138">Now that John has finished defining his KPIs, he starts his Engagement strategy phase by defining 4 engagement programs and their objectives: ![][1]</span></span>

<span data-ttu-id="ba719-139">John은 각 프로그램에 대한 푸시 알림을 자세히 열거하면서 깊이 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-139">Then John goes deeper by detailing push notifications for each program.</span></span> <span data-ttu-id="ba719-140">푸시 알림은 다섯 가지 요소로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-140">Push notification are defined by five elements:</span></span>

1. <span data-ttu-id="ba719-141">목표: hello 알림 hello 목표 란</span><span class="sxs-lookup"><span data-stu-id="ba719-141">Objective: what is hello objective of hello notification</span></span>
2. <span data-ttu-id="ba719-142">Hello 목표 연결할 수는 방법</span><span class="sxs-lookup"><span data-stu-id="ba719-142">How hello objective will be reached</span></span>
3. <span data-ttu-id="ba719-143">대상: 알림을 받을 사람을 hello?</span><span class="sxs-lookup"><span data-stu-id="ba719-143">Target: who will receive hello notification?</span></span>
4. <span data-ttu-id="ba719-144">내용: hello 단어 및 hello 형식의 hello 알림 (App/Out의 앱에서) 란</span><span class="sxs-lookup"><span data-stu-id="ba719-144">Content: What is hello wording and hello format of hello notification (In App/Out of App)</span></span>
5. <span data-ttu-id="ba719-145">경우에: 어떤는 hello 최상의 순간 toosend이 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="ba719-145">When: what is hello best moment toosend this push notification</span></span>
   
    ![][2]

<span data-ttu-id="ba719-146">자세한 내용은 참조 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-146">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).</span></span>

<span data-ttu-id="ba719-147">Toocollect 및 IT 팀 tooimplement hello 솔루션과 그의 태그를 공동으로 계획 하는 쓰기 toohello 파트 2/hello 백서 이한일은 사용 하 여 대상 섹션 toodefine 그에 데이터를 따르는입니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-147">According toohello part 2 of hello white paper John uses target section toodefine what data he has toocollect and writes his Tag Plan jointly with IT team tooimplement hello solution.</span></span> <span data-ttu-id="ba719-148">구현 1주일 후, 사용자 승인 테스트 후에 John은 드디어 프로그램을 출시할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-148">After 1 week of implementation and user acceptance testing, John can finally launch his programs.</span></span>

## <a name="program-results"></a><span data-ttu-id="ba719-149">프로그램 결과</span><span class="sxs-lookup"><span data-stu-id="ba719-149">Program Results</span></span>
<span data-ttu-id="ba719-150">4개월 후 John은 프로그램의 성과를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-150">4 months later, John reviews performances of programs.</span></span> <span data-ttu-id="ba719-151">시작 프로그램 hello 및 hello 매주 프로그램의 목표 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-151">hello Welcome Program and hello Weekly Program are meeting his goals.</span></span> <span data-ttu-id="ba719-152">hello 하나만 세션과 사용자 수가 감소 하 고 hello 응용 프로그램의 더 많은 기능을 사용 하 고 연결 수를 주별로 hello 수 두 배 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-152">hello number of user with only one session decreases, more features of hello app are being used and hello number of connections per week has doubled.</span></span>

<span data-ttu-id="ba719-153">hello **비활성 프로그램** 되어 사용자 경향을 이해 하는 John 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-153">hello **Inactive Program** is helping John understand user tendencies.</span></span> <span data-ttu-id="ba719-154">Hello 비활성 사용자의 15 %toohello 앱 돌아와서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-154">It appears that 15% of hello inactive users come back toohello app.</span></span> <span data-ttu-id="ba719-155">하지만 이들 대부분이 1달 이상 활성 상태를 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-155">However most of them don’t stay active more than 1 month.</span></span> <span data-ttu-id="ba719-156">John은 알림을 추가하고 콘텐츠 선택 범위를 확장하여 이렇게 반복되는 상황을 잠재적으로 최적화할 수 있다고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-156">John foresees a potential optimization of this sequence with additional notifications and expanding his content choices.</span></span>

<span data-ttu-id="ba719-157">hello **검색 프로그램** 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-157">hello **Discover Program** doesn’t work well.</span></span> <span data-ttu-id="ba719-158">그의 목적을 판매 중인 하지만 부족 tooreach 크로스 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-158">It increases cross selling but not enough tooreach his objectives.</span></span> <span data-ttu-id="ba719-159">이한일은 그 하지 않는 충분 한 데이터 toomake 관련 대상으로 지정 하 고 해당 콘텐츠를 제안 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-159">John identifies that he doesn’t have enough data toomake relevant targeting and propose appropriate content.</span></span> <span data-ttu-id="ba719-160">이 프로그램을 중지하고 Azure Mobile Engagement를 사용하여 “사설 푸시 알림”을 전송하는 것에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-160">He stops this program and focuses on sending “editorial push notifications” with Azure Mobile Engagement.</span></span> <span data-ttu-id="ba719-161">이미 그의 저널리스트 CMS 솔루션 toosend 푸시 알림을 있고 toochange 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-161">His journalists already have a CMS solution toosend push notifications and they don’t want toochange.</span></span>

<span data-ttu-id="ba719-162">이한일은은 toouse hello Reach API는 Reach 캠페인 toouse AZME 웹 인터페이스 필요 없이 관리를 허용 하는 HTTP REST API를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-162">John decides toouse hello Reach API which is an HTTP REST API that allows managing Reach campaigns without having toouse AZME Web interface.</span></span> <span data-ttu-id="ba719-163">John이 방법을 사용 하며 그의 작성자를 허용 합니다. 그 hello 데이터를 수집할 수 tookeep hello CMS 솔루션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-163">With this approach John can collect hello data he needs and allow his writers tookeep using hello CMS solution.</span></span>

<span data-ttu-id="ba719-164">기능이 올바르게 작동 하는 tooensure, John hello 지점 다음에 주의 IT 팀 toobe를 게 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-164">tooensure that feature works correctly, John asks IT team toobe vigilant on hello following points:</span></span>

1. <span data-ttu-id="ba719-165">**운영 체제** : 바쁘기 때문에 John toolist 모든 사례 및 검사 Api hello을 처리 하는 경우 자신의 규칙 tooadministrate 푸시 알림을가지고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-165">**Operation Systems** : They all have their own rules tooadministrate push notifications, so John decides toolist all cases and checks if hello APIs handle it.</span></span>
   <span data-ttu-id="ba719-166">예: Android 푸시 시스템 hello 경우 iOS와는 큰 그림을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-166">E.g : Android push system allows big picture which is not hello case with iOS.</span></span>
2. <span data-ttu-id="ba719-167">**시간 프레임**: 이한일은 hello에 대 한 시간대를 설정 하 고 최종 toocampaigns를 설정 하는 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-167">**Time frame**: John wants an API, which set hello time frame and set an end toocampaigns.</span></span> <span data-ttu-id="ba719-168">모든 장치를 중단 해야 알림 폭탄 테러 toopreserve 사용자가 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-168">He wants toopreserve users from any disruptive notification bombing.</span></span>
3. <span data-ttu-id="ba719-169">**범주**: 마케팅 팀은 각각의 경고 유형에 대한 템플릿을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-169">**Categories**: Marketing team prepares template for each type of alerting.</span></span> <span data-ttu-id="ba719-170">이한일은은 hello API 내 IT 팀 tooset 범주를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-170">John asks IT team tooset categories inside hello API.</span></span>

<span data-ttu-id="ba719-171">테스트를 거친 후에 John은 만족하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-171">After some tests John is satisfied.</span></span> <span data-ttu-id="ba719-172">감사 toothis API 저널리스트 여전히 해당 CMS에서 푸시 알림을 보내고에 모든 동작 데이터를 수집 하는 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ba719-172">Thanks toothis API, journalists can still send push notifications with their CMS and Azure Mobile Engagement collects all behavioral data for them</span></span>

<span data-ttu-id="ba719-173">초반 4개월이 지난 후에, 전반적으로 만족할만한 성과가 결과에 반영되었고, John과 이사회는 확신을 갖게 되었으며, 사용자당 ROI가 15% 증가하고 모바일 매출이 총 매출의 17.5 %를 차지하면서 단 4개월 만에 7.5%가 증가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba719-173">After these 4 first months, results reflect a good overall performance and gives confidence for John and his board, ROI per user increases per 15% and mobile sales represent 17.5 % of total sales, an increase of 7.5% in only four months.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
