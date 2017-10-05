---
title: "게임 앱에 대한 Azure Mobile Engagement 구현"
description: "Azure Mobile Engagement 구현을 위한 게임 앱 시나리오"
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
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="fe9e2-103">게임 앱에서 Mobile Engagement 구현</span><span class="sxs-lookup"><span data-stu-id="fe9e2-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="fe9e2-104">개요</span><span class="sxs-lookup"><span data-stu-id="fe9e2-104">Overview</span></span>
<span data-ttu-id="fe9e2-105">새 낚시 기반 롤플레이/전략 게임 앱을 출시했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="fe9e2-106">이 게임이 시작되고 6개월 동안 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="fe9e2-107">이 게임은 커다란 성공을 거두어 수백만 회의 다운로드를 기록했고 재방문 주기도 새로 시작한 다른 게임 앱에 비해 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="fe9e2-108">이에 관련자들은 분기별 검토 회의에서 ARPU(사용자당 평균 수익)를 올리기로 합의했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="fe9e2-109">프리미엄 게임 내 패키지가 특별 제공으로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="fe9e2-110">이러한 게임 팩을 통해 사용자는 게임의 낚싯줄 및 미끼와 낚시 도구의 모양 및 성능을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="fe9e2-111">그러나 패키지 판매는 매우 낮은 실정입니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-111">However, package sales are very low.</span></span> <span data-ttu-id="fe9e2-112">그래서 분석 도구를 사용하여 사용자 환경을 먼저 분석한 다음 Engagement 프로그램을 개발하여 고급 구분을 통해 판매를 늘리기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="fe9e2-113">[Azure Mobile Engagement - 모범 사례가 포함된 시작 가이드](mobile-engagement-getting-started-best-practices.md) 에 따라 Engagement 전략을 구축했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="fe9e2-114">목표 및 KPI</span><span class="sxs-lookup"><span data-stu-id="fe9e2-114">Objectives and KPIs</span></span>
<span data-ttu-id="fe9e2-115">주요 게임의 관련자들의 관심사가 충족되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="fe9e2-116">프리미엄 패키지 매출의 15% 증가라는 한 가지 주요 목표에 모두 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="fe9e2-117">이 목표를 측정하고 추진하기 위해 비즈니스 KPI(핵심 성과 지표)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="fe9e2-118">어느 게임 레벨에서 이러한 패키지를 구입하나요?</span><span class="sxs-lookup"><span data-stu-id="fe9e2-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="fe9e2-119">사용자별, 세션별, 주간 및 월간 수익은 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="fe9e2-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="fe9e2-120">즐겨찾는 구매 유형은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="fe9e2-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="fe9e2-121">[시작 가이드](mobile-engagement-getting-started-best-practices.md) 1부에서는 목표 및 KPI를 정의하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="fe9e2-122">지금 정의한 비즈니스 KPI를 사용하여 모바일 제품 관리자가 새로운 사용자 추세 및 재방문 주기를 확인하기 위한 Engagement KPI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="fe9e2-123">매일, 2일 간격, 매주, 매월, 3개월 간격을 사용해서 재방문 주기를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="fe9e2-124">활성 사용자 수</span><span class="sxs-lookup"><span data-stu-id="fe9e2-124">Active user counts</span></span>
* <span data-ttu-id="fe9e2-125">스토어의 앱 등급</span><span class="sxs-lookup"><span data-stu-id="fe9e2-125">The app rating in the store</span></span>

<span data-ttu-id="fe9e2-126">IT 팀의 권고에 따라 다음 질문에 답하기 위해 다음과 같은 기술 KPI가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="fe9e2-127">사용자 경로(방문한 페이지, 사용자가 이곳에서 사용한 시간)</span><span class="sxs-lookup"><span data-stu-id="fe9e2-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="fe9e2-128">세션별 발생한 중단 또는 버그 수</span><span class="sxs-lookup"><span data-stu-id="fe9e2-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="fe9e2-129">사용자가 실행하는 OS 버전</span><span class="sxs-lookup"><span data-stu-id="fe9e2-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="fe9e2-130">사용자의 평균 화면 크기</span><span class="sxs-lookup"><span data-stu-id="fe9e2-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="fe9e2-131">사용자가 사용하는 인터넷 연결 종류</span><span class="sxs-lookup"><span data-stu-id="fe9e2-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="fe9e2-132">각 KPI에 대해 모바일 제품 관리자가 필요한 데이터와 이 데이터의 플레이북 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="fe9e2-133">Engagement 프로그램 및 통합</span><span class="sxs-lookup"><span data-stu-id="fe9e2-133">Engagement program and integration</span></span>
<span data-ttu-id="fe9e2-134">고급 Engagement 프로그램을 구축하기 전에 프로젝트를 담당하는 모바일 프로젝트 책임자는 사용자들이 언제 어떻게 제품을 사용하는지에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="fe9e2-135">3개월 후 모바일 프로젝트 책임자가 앱 내 푸시 알림 판매를 개선하기 위한 충분한 데이터를 수집했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="fe9e2-136">알아낸 사실은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-136">He learns that:</span></span>

* <span data-ttu-id="fe9e2-137">일반적으로 레벨 14에서 첫 번째 구매가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="fe9e2-138">이런 사례의 90%가 3달러의 전설적인 새 무기를 구매했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="fe9e2-139">이런 사례의 80%에서 사용자가 구매를 한 후 제품을 계속 사용할 뿐만 아니라 추가로 더 구매합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="fe9e2-140">레벨 20을 통과한 사용자는 1주일에 10달러를 넘게 쓰기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="fe9e2-141">사용자들은 레벨 16, 24, 32에서 프리미엄 패키지를 구입하는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="fe9e2-142">이 분석을 이용하여 모바일 프로젝트 책임자는 앱 내 판매를 늘리기 위해 특정 푸시 알림 순서를 만들기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="fe9e2-143">세 가지 푸시 순서, 즉 시작 프로그램, 판매 프로그램 및 비활성 프로그램을 만들고 이대로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fe9e2-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="fe9e2-144">자세한 내용은 참조는 [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="fe9e2-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
