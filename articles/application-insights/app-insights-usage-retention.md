---
title: "Azure Application Insights를 사용한 웹 응용 프로그램에 대 한 보존 분석 aaaUser | Microsoft docs"
description: "Tooyour 앱 반환 하는 몇 명 입니까?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="fce8a-103">Application Insights를 사용한 웹 응용 프로그램의 사용자 재방문 주기 분석</span><span class="sxs-lookup"><span data-stu-id="fce8a-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="fce8a-104">hello 보존 기능인 [Azure Application Insights](app-insights-overview.md) tooyour 응용 프로그램 및 특정 작업을 수행 하거나 목표를 달성 얼마나 자주 사용 하면 사용자 수를 분석할 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="fce8a-105">예를 들어 게임 사이트를 실행 하는 경우 우위 후 반환 hello 번호로 게임 손실 된 후 toohello 사이트를 반환 하는 사용자의 hello 숫자를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="fce8a-106">이러한 지식이 있으면 사용자 환경 및 비즈니스 전략을 둘 다 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="fce8a-107">시작</span><span class="sxs-lookup"><span data-stu-id="fce8a-107">Get started</span></span>

<span data-ttu-id="fce8a-108">Hello 보존 도구 hello Application Insights 포털에서 데이터를 아직 표시 되지 않으면 [tooget hello 사용량 도구를 시작 하는 방법에 대해 알아봅니다](app-insights-usage-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="fce8a-109">hello 보존 도구</span><span class="sxs-lookup"><span data-stu-id="fce8a-109">hello Retention tool</span></span>

![재방문 주기 도구](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="fce8a-111">hello 도구 모음 toocreate 새 보존 보고서 사용자가 사용, 기존 보존 보고서를 열고, 현재 보존 보고서 저장 또는 다른 이름으로 저장, toosaved 보고서 변경 내용이 되돌릴, 전자 메일 또는 직접 연결 및 액세스 hello를 통해 공유 보고서 hello 보고서에서 데이터 새로 고침 설명서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="fce8a-112">기본적으로 재방문 주기는 기간에 따라 작업을 한 후 다시 방문하고 다른 작업을 한 모든 사용자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="fce8a-113">특정 사용자 활동에 이벤트 toonarrow hello 포커스의 여러 조합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="fce8a-114">속성에 대해 하나 이상의 필터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-114">Add one or more filters on properties.</span></span> <span data-ttu-id="fce8a-115">예를 들어 특정 국가 또는 하위 지역에 있는 사용자에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="fce8a-116">클릭 **업데이트** hello 필터를 설정한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="fce8a-117">hello 전반적인 보존 차트 요약해 서 보여주는 사용자 보존 hello 특정 기간에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="fce8a-118">hello 표 형식으로 사용자 수가 hello 유지 따라 toohello 쿼리 작성기 # 2를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="fce8a-119">각 행에 표시 된 기간 hello 시간에 모든 이벤트를 수행한 사용자의 코 호트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="fce8a-120">Hello 행의 각 셀 이후 기간에 적어도 한 번 해당 코 호트의 반환을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="fce8a-121">일부 사용자는 둘 이상의 기간에 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="fce8a-122">상위 5 개 반환 이벤트 toogive 사용자가 자신의 보존 보고서를 더 잘 이해를 hello insights 카드 상위 5 개 시작 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![재방문 주기 마우스 가리키기](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="fce8a-124">사용자가 셀 hello 보존 tool tooaccess hello 분석 단추 위로 수 및 도구 설명 바로 hello 셀에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="fce8a-125">hello 분석 단추 hello 셀에서 미리 입력된 쿼리 toogenerate 사용자와 사용자 toohello 분석 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="fce8a-126">비즈니스 이벤트 tootrack 보존을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fce8a-126">Use business events tootrack retention</span></span>

<span data-ttu-id="fce8a-127">tooget hello 가장 유용한 보존 분석, 중요 한 비즈니스 활동을 나타내는 측정값 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="fce8a-128">예를 들어 많은 사용자가 표시 하는 hello 게임을 재생 하지 않고 앱에서 페이지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="fce8a-129">방금 hello 페이지 뷰를 추적 하는 것은 얼마나 많은 사람들이 반환 tooplay hello 게임 후 이전에 지속적인 부정확 한 예상을 제공 따라서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="fce8a-130">플레이어 반환 명확히 tooget 앱 실제로 수행 하는 경우 사용자 지정 이벤트를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="fce8a-131">것이 좋습니다 toocode 사용자 지정 이벤트 및 보존 분석에 사용 하는 주요 비즈니스 동작을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="fce8a-132">toocapture hello 게임 결과 한 줄의 코드 toosend 사용자 지정 이벤트 tooApplication Insights toowrite가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="fce8a-133">Node.JS 또는 hello 웹 페이지 코드에 해당 작성, 하는 경우 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="fce8a-134">또는 ASP.NET 서버 코드:</span><span class="sxs-lookup"><span data-stu-id="fce8a-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="fce8a-135">[사용자 지정 이벤트 작성에 대해 자세히 알아봅니다](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="fce8a-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fce8a-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fce8a-136">Next steps</span></span>
- <span data-ttu-id="fce8a-137">tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.</span><span class="sxs-lookup"><span data-stu-id="fce8a-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="fce8a-138">사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.</span><span class="sxs-lookup"><span data-stu-id="fce8a-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="fce8a-139">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="fce8a-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="fce8a-140">깔때기</span><span class="sxs-lookup"><span data-stu-id="fce8a-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="fce8a-141">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="fce8a-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="fce8a-142">통합 문서</span><span class="sxs-lookup"><span data-stu-id="fce8a-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="fce8a-143">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="fce8a-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


