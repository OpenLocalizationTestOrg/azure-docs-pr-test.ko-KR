---
title: "Azure Application Insights를 사용한 웹 응용 프로그램의 사용자 재방문 주기 분석 | Microsoft Docs"
description: "앱으로 돌아온 사용자는 몇 명이나 되나요?"
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
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="818fc-103">Application Insights를 사용한 웹 응용 프로그램의 사용자 재방문 주기 분석</span><span class="sxs-lookup"><span data-stu-id="818fc-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="818fc-104">[Azure Application Insights](app-insights-overview.md)의 재방문 주기 기능은 앱으로 돌아온 사용자 수와 특정 작업을 수행하거나 목표를 달성하는 빈도를 분석하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="818fc-105">예를 들어 게임 사이트를 실행하는 경우 게임에서 진 후에 사이트로 돌아오는 사용자 수와 이긴 후에 돌아온 사용자 수를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="818fc-106">이러한 지식이 있으면 사용자 환경 및 비즈니스 전략을 둘 다 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="818fc-107">시작</span><span class="sxs-lookup"><span data-stu-id="818fc-107">Get started</span></span>

<span data-ttu-id="818fc-108">Application Insights 포털의 재방문 주기 도구에서 아직 데이터가 표시되지 않으면 [사용 도구 시작 방법을 알아봅니다](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="818fc-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="818fc-109">재방문 주기 도구</span><span class="sxs-lookup"><span data-stu-id="818fc-109">The Retention tool</span></span>

![재방문 주기 도구](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="818fc-111">도구 모음을 사용하면 사용자가 새 재방문 주기 보고서를 만들고, 기존 재방문 주기 보고서를 열고, 현재 재방문 주기 보고서 저장하거나 저장된 보고서로 만들어진 변경 내용을 되돌리고, 보고서에서 데이터 새로 고치고, 이메일 또는 직접 링크를 통해 보고서를 공유하고 설명서 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="818fc-112">기본적으로 재방문 주기는 기간에 따라 작업을 한 후 다시 방문하고 다른 작업을 한 모든 사용자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="818fc-113">다른 이벤트의 조합을 선택하여 특정 사용자 작업에 대한 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="818fc-114">속성에 대해 하나 이상의 필터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-114">Add one or more filters on properties.</span></span> <span data-ttu-id="818fc-115">예를 들어 특정 국가 또는 하위 지역에 있는 사용자에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="818fc-116">필터를 설정한 후에 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="818fc-117">전체 재방문 주기 차트는 선택한 기간에 걸친 사용자 재방문 주기의 요약을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="818fc-118">표는 #2의 쿼리 작성기에 따라 재방문한 사용자 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="818fc-119">각 행은 표시된 기간에 이벤트를 실행한 사용자의 코호트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="818fc-120">행의 각 셀은 이후 기간에 1번 이상 돌아온 해당 코호트 수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="818fc-121">일부 사용자는 둘 이상의 기간에 돌아올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="818fc-122">insights 카드는 상위 5개 시작 이벤트 및 상위 5개 반환되는 이벤트를 표시하여 사용자가 자신의 재방문 주기 보고서를 더 잘 이해할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![재방문 주기 마우스 가리키기](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="818fc-124">사용자가 셀의 의미를 설명하는 분석 단추 및 도구 팁에 액세스하려면 재방문 주기 도구에서 셀을 마우스로 가리키면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="818fc-125">분석 단추를 통해 셀에서 사용자를 생성하는 미리 입력된 쿼리를 사용하여 분석 도구로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="818fc-126">비즈니스 이벤트를 사용하여 재방문 주기 추적</span><span class="sxs-lookup"><span data-stu-id="818fc-126">Use business events to track retention</span></span>

<span data-ttu-id="818fc-127">유용한 재방문 주기 분석 기능을 최대한 활용하려면 유의한 비즈니스 활동을 나타내는 이벤트를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="818fc-128">예를 들어 많은 사용자는 앱에서 페이지를 열기만 하고 표시되는 게임을 재생하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="818fc-129">따라서 페이지 보기만 추적하면 이전에 게임을 즐긴 후에 돌아와서 게임을 재생한 사용자 수를 정확히 추정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="818fc-130">돌아온 플레이어를 명확히 분선하기 위해 앱은 사용자가 실제로 게임을 할 때 사용자 지정 이벤트를 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="818fc-131">주요 비즈니스 작업을 나타내는 사용자 지정 이벤트를 코딩하고 재방문 주기 분석에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="818fc-132">게임 결과를 캡처하려면 Application Insights에 사용자 지정 이벤트를 전송하는 코드 줄을 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="818fc-133">웹 페이지 코드 또는 Node.JS에서 작성할 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="818fc-134">또는 ASP.NET 서버 코드:</span><span class="sxs-lookup"><span data-stu-id="818fc-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="818fc-135">[사용자 지정 이벤트 작성에 대해 자세히 알아봅니다](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="818fc-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="818fc-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="818fc-136">Next steps</span></span>
- <span data-ttu-id="818fc-137">사용 현황 환경을 활성화하려면 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views) 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="818fc-138">사용자 지정 이벤트 또는 페이지 보기를 이미 보낸 경우 사용자가 서비스를 사용하는 방법에 대해 알아보려면 사용 현황 도구를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="818fc-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="818fc-139">사용자, 세션, 이벤트</span><span class="sxs-lookup"><span data-stu-id="818fc-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="818fc-140">깔때기</span><span class="sxs-lookup"><span data-stu-id="818fc-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="818fc-141">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="818fc-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="818fc-142">통합 문서</span><span class="sxs-lookup"><span data-stu-id="818fc-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="818fc-143">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="818fc-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


