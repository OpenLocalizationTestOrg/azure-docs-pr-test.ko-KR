---
title: "게임 앱에 대 한 aaaAzure Mobile Engagement 구현"
description: "게임 앱 시나리오 tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="b1d63-103">게임 앱에서 Mobile Engagement 구현</span><span class="sxs-lookup"><span data-stu-id="b1d63-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="b1d63-104">개요</span><span class="sxs-lookup"><span data-stu-id="b1d63-104">Overview</span></span>
<span data-ttu-id="b1d63-105">새 낚시 기반 롤플레이/전략 게임 앱을 출시했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="b1d63-106">6 개월 동안 실행 되 고 hello 게임이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="b1d63-107">이 게임의 거 대 한 성공 다운로드 수많은 있기 및 hello 보존은 매우 높은 비교 tooother 시작 게임 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="b1d63-108">Hello 분기별 검토 회의 이해 관계자 (ARPU) 사용자 당 평균 수익 tooincrease 필요한 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="b1d63-109">프리미엄 게임 내 패키지가 특별 제공으로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="b1d63-110">이러한 게임 팩 hello 게임에서 사용자가 tooupgrade hello 모양과 어 줄 및 lures 또는 tackles 성능을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="b1d63-111">그러나 패키지 판매는 매우 낮은 실정입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-111">However, package sales are very low.</span></span> <span data-ttu-id="b1d63-112">결정 되므로 분석 도구를 사용한 첫 번째 tooanalyze hello 고객 환경 및 engagement 프로그램 tooincrease 판매 사용 하 여 프로그램 toodevelop 나오는 조각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="b1d63-113">Hello에 따라 [Azure Mobile Engagement 설명서와 모범 사례](mobile-engagement-getting-started-best-practices.md) engagement 전략을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="b1d63-114">목표 및 KPI</span><span class="sxs-lookup"><span data-stu-id="b1d63-114">Objectives and KPIs</span></span>
<span data-ttu-id="b1d63-115">Hello 게임에 대 한 주요 이해 관계자 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="b1d63-116">모든 주요 목표-15 %tooincrease 프리미엄 패키지 sales에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="b1d63-117">만들 비즈니스 핵심 성과 지표 (Kpi) toomeasure 및 드라이브이 목표</span><span class="sxs-lookup"><span data-stu-id="b1d63-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="b1d63-118">Hello 게임의 수준에서 이러한 패키지를 구매는?</span><span class="sxs-lookup"><span data-stu-id="b1d63-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="b1d63-119">사용자 당, 세션당, 일주일, 및 한 달 hello 수익 이란?</span><span class="sxs-lookup"><span data-stu-id="b1d63-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="b1d63-120">Hello 즐겨 찾는 구매 유형은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="b1d63-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="b1d63-121">Hello 1 부에서 [시작 가이드](mobile-engagement-getting-started-best-practices.md) toodefine 목표 및 Kpi를 hello 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="b1d63-122">Hello 비즈니스 Kpi 정의 되었으며,로 Engagement Kpi toodetermine 새 사용자 추세 및 보존 hello 모바일 제품 관리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="b1d63-123">보존을 모니터링 하 고 hello 다음 간격에 걸쳐 사용: 매일, 2 일 마다, 매주, 매월 및 3 개월 마다 해당 날짜</span><span class="sxs-lookup"><span data-stu-id="b1d63-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="b1d63-124">활성 사용자 수</span><span class="sxs-lookup"><span data-stu-id="b1d63-124">Active user counts</span></span>
* <span data-ttu-id="b1d63-125">hello 앱 등급 hello에 저장</span><span class="sxs-lookup"><span data-stu-id="b1d63-125">hello app rating in hello store</span></span>

<span data-ttu-id="b1d63-126">다음 기술 Kpi hello hello IT 팀의에서 권장 사항에 따라, 질문 다음 tooanswer hello가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="b1d63-127">사용자 경로(방문한 페이지, 사용자가 이곳에서 사용한 시간)</span><span class="sxs-lookup"><span data-stu-id="b1d63-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="b1d63-128">세션별 발생한 중단 또는 버그 수</span><span class="sxs-lookup"><span data-stu-id="b1d63-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="b1d63-129">사용자가 실행하는 OS 버전</span><span class="sxs-lookup"><span data-stu-id="b1d63-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="b1d63-130">내 사용자를 위해 화면의 평균 크기 hello 이란?</span><span class="sxs-lookup"><span data-stu-id="b1d63-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="b1d63-131">사용자가 사용하는 인터넷 연결 종류</span><span class="sxs-lookup"><span data-stu-id="b1d63-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="b1d63-132">각 KPI에 대 한 hello 모바일 제품 관리자 hello 데이터 그녀가 필요한 및 그녀의 플레이 북에서 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="b1d63-133">Engagement 프로그램 및 통합</span><span class="sxs-lookup"><span data-stu-id="b1d63-133">Engagement program and integration</span></span>
<span data-ttu-id="b1d63-134">고급 engagement 프로그램을 구축 하기 전에 hello 프로젝트를 담당 모바일 프로젝트 디렉터 hello 제품 hello 사용자가 사용 된 방법 및 시기에 대 한 심층적 이해가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="b1d63-135">3 개월 후 그의 앱에 푸시 알림 sales hello 모바일 프로젝트 디렉터 충분 한 데이터 tooenhance 수집 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="b1d63-136">알아낸 사실은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-136">He learns that:</span></span>

* <span data-ttu-id="b1d63-137">첫 번째 구매 hello hello 수준 14에서 일반적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="b1d63-138">90%의 경우, hello 구매 $3에 대 한 새 전설의 웨는입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="b1d63-139">경우 80%가 hello 제품을 계속 하 고 더 많은 구매를 수행한 사용자가 구입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="b1d63-140">사용자 조건이 충족 hello 수준 20, $10/주 이상 toospend 시작입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="b1d63-141">사용자 수준 16, 24 및 32에서 toobuy 프리미엄 패키지는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="b1d63-142">앱 판매 toocreate 특정 푸시 알림 시퀀스 tooincrease를 결정 하는 hello 모바일 프로젝트 디렉터 toothis 분석을 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="b1d63-143">세 가지 푸시 순서, 즉 시작 프로그램, 판매 프로그램 및 비활성 프로그램을 만들고 이대로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d63-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="b1d63-144">자세한 내용은 참조 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="b1d63-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
