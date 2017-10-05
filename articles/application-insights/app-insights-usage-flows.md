---
title: "Azure Application Insights에서 사용자 흐름을 사용하여 사용자 탐색 패턴 분석 | Microsoft docs"
description: "페이지와 웹앱의 기능 간에 사용자가 탐색하는 방법을 분석합니다."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d17ed3dff08f00a1d6a2108608e42b29f95fbd84
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a><span data-ttu-id="9a09e-103">Application Insights에서 사용자 흐름을 사용하여 사용자 탐색 패턴 분석</span><span class="sxs-lookup"><span data-stu-id="9a09e-103">Analyze user navigation patterns with User Flows in Application Insights</span></span>

![Application Insights 사용자 흐름 도구](./media/app-insights-usage-flows/flows.png)

<span data-ttu-id="9a09e-105">사용자 흐름 도구는 페이지와 웹앱의 기능 간에 사용자가 탐색하는 방법을 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-105">The User Flows tool visualizes how users navigate between the pages and features of your site.</span></span> <span data-ttu-id="9a09e-106">다음과 같은 질문에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-106">It's great for answering questions like:</span></span>
* <span data-ttu-id="9a09e-107">사용자가 사이트 페이지에서 벗어나려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-107">How do users navigate away from a page on your site?</span></span>
* <span data-ttu-id="9a09e-108">사용자가 사이트 페이지에서 어디를 클릭하나요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-108">What do users click on a page on your site?</span></span>
* <span data-ttu-id="9a09e-109">사용자가 사이트에서 가장 많이 이탈하는 위치는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-109">Where are the places that users churn most from your site?</span></span>
* <span data-ttu-id="9a09e-110">사용자가 동일한 작업을 반복하는 위치가 있나요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-110">Are there places where users repeat the same action over and over?</span></span>

<span data-ttu-id="9a09e-111">사용자 흐름 도구는 지정하는 초기 페이지 보기 또는 이벤트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-111">The User Flows tool starts from an initial page view or event that you specify.</span></span> <span data-ttu-id="9a09e-112">이 페이지 보기 또는 사용자 지정 이벤트에 따라 사용자 흐름은 세션 중, 두 단계 전후에서 사용자가 즉시 전송하는 페이지 보기 및 사용자 지정 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-112">Given this page view or custom event, User Flows shows the page views and custom events that users sent immediately afterwards during a session, two steps afterwards, and so forth.</span></span> <span data-ttu-id="9a09e-113">다양한 두께의 선은 사용자가 따라간 각 경로의 횟수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-113">Lines of varying thickness show how many times each path was followed by users.</span></span> <span data-ttu-id="9a09e-114">특별한 "종료된 세션" 노드는 이전 노드 이후에 페이지 보기 또는 사용자 지정 이벤트를 전송한 사용자 수를 표시하고 사이트에 사용자가 남아 있는 위치를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-114">Special "Session Ended" nodes show how many users sent no page views or custom events after the preceding node, highlighting where users probably left your site.</span></span>



> [!NOTE]
> <span data-ttu-id="9a09e-115">Application Insights 리소스는 사용자 흐름 도구를 사용하기 위한 페이지 보기 또는 사용자 지정 이벤트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-115">Your Application Insights resource must contain page views or custom events to use the User Flows tool.</span></span> <span data-ttu-id="9a09e-116">[Application Insights JavaScript SDK를 사용하여 자동으로 페이지 뷰를 수집하도록 앱을 설정하는 방법에 대해 알아봅니다](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9a09e-116">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a><span data-ttu-id="9a09e-117">초기 페이지 보기 또는 사용자 지정 이벤트를 선택하여 시작</span><span class="sxs-lookup"><span data-stu-id="9a09e-117">Start by choosing an initial page view or custom event</span></span>

![사용자 흐름에 대한 초기 이벤트 선택](./media/app-insights-usage-flows/flows-initial-event.png)

<span data-ttu-id="9a09e-119">사용자 흐름 도구에 대한 질문에 대답하기 시작하려면 시각화에 대한 시작점으로 사용할 초기 페이지 보기 또는 사용자 지정 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-119">To get started answering questions with the User Flows tool, choose an initial page view or custom event to serve as the starting point for the visualization:</span></span>
1. <span data-ttu-id="9a09e-120">"이후에 사용자가 수행할 작업은 무엇인가요...?"에 있는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-120">Click the link in the "What do users do after...?"</span></span> <span data-ttu-id="9a09e-121">또는 편집 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-121">title, or click the Edit button.</span></span> 
2. <span data-ttu-id="9a09e-122">"초기 이벤트" 드롭다운 목록에서 페이지 보기 또는 사용자 지정 이벤트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-122">Select a page view or custom event from the "Initial event" dropdown.</span></span>
3. <span data-ttu-id="9a09e-123">"그래프 만들기"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-123">Click "Create graph".</span></span>

<span data-ttu-id="9a09e-124">시각화의 "1단계" 열에서는 초기 이벤트 바로 이후에 사용자가 가장 자주 사용하는 항목을 빈도가 높은 항목부터 낮은 차순으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-124">The "Step 1" column of the visualization shows what users did most frequently just after the initial event, ordered top-to-bottom from most- to least-frequent.</span></span> <span data-ttu-id="9a09e-125">"2단계" 및 후속 열에서는 이후 사용자가 수행한 작업을 표시하고 사이트를 통해 사용자가 탐색한 방법으로 그림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-125">The "Step 2" and subsequent columns show what users did thereafter, creating a picture of all the ways users have navigated through your site.</span></span>

<span data-ttu-id="9a09e-126">기본적으로 사용자 흐름 도구는 최근 24시간 동안 사이트에서 페이지 보기 및 사용자 지정 이벤트를 무작위로 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-126">By default, the User Flows tool randomly samples only the last 24 hours of page views and custom event from your site.</span></span> <span data-ttu-id="9a09e-127">시간 범위를 늘리고 편집 메뉴에서 무작위 샘플링에 대한 성능 및 정확도의 균형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-127">You can increase the time range and change the balance of performance and accuracy for random sampling in the Edit menu.</span></span>

<span data-ttu-id="9a09e-128">일부 페이지 뷰 및 사용자 지정 이벤트가 사용자와 연관이 없는 경우 숨기려면 노드에서 "X"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-128">If some of the page views and custom events aren't relevant to you, click the "X" on the nodes you want to hide.</span></span> <span data-ttu-id="9a09e-129">숨기려는 노드를 선택한 다음 시각화 아래에서 "그래프 만들기" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-129">Once you've selected the nodes you want to hide, click the "Create graph" button below the visualization.</span></span> <span data-ttu-id="9a09e-130">숨겨진 모든 노드를 보려면 편집 단추를 클릭한 다음 "제외된 이벤트" 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-130">To see all of the nodes you've hidden, click the Edit button, then look at the "Excluded events" section.</span></span>

<span data-ttu-id="9a09e-131">페이지 보기 또는 사용자 지정 이벤트가 누락된 경우 시각화에 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-131">If page views or custom events are missing that you expect to see on the visualization:</span></span>
* <span data-ttu-id="9a09e-132">편집 메뉴에서 "제외된 이벤트" 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-132">Check the "Excluded events" section in the Edit menu.</span></span>
* <span data-ttu-id="9a09e-133">편집 메뉴에서 "세부 정보 수준" 제어를 사용하여 시각화에 자주 사용하지 않는 이벤트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-133">Use the "Detail level" control in the Edit menu to include less-frequent events in the visualization.</span></span>
* <span data-ttu-id="9a09e-134">원하는 페이지 보기 또는 사용자 지정 이벤트를 사용자가 자주 전달하는 경우 편집 메뉴에서 시각화의 시간 범위를 늘려 주세요.</span><span class="sxs-lookup"><span data-stu-id="9a09e-134">If the page view or custom event you expect is sent infrequently by users, try increasing the time range of the visualization in the Edit menu.</span></span>
* <span data-ttu-id="9a09e-135">원하는 페이지 보기 또는 사용자 지정 이벤트가 사이트의 소스 코드에 있는 Application Insights SDK를 통해 수집되도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-135">Make sure the page view or custom event you expect is set up to be collected by the Application Insights SDK in the source code of your site.</span></span> [<span data-ttu-id="9a09e-136">사용자 지정 이벤트 수집에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-136">Learn more about collecting custom events.</span></span>](app-insights-api-custom-events-metrics.md)

<span data-ttu-id="9a09e-137">시각화에서 더 많은 단계를 확인하려는 경우 편집 메뉴에서 "단계 수" 슬라이더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-137">If you want to see more steps in the visualization, use the "Number of steps" slider in the Edit menu.</span></span>

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a><span data-ttu-id="9a09e-138">페이지 또는 기능을 방문한 후에 사용자가 어디로 이동하고 어떤 항목을 클릭하나요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-138">After visiting a page or feature, where do users go and what do they click?</span></span>

![사용자 흐름을 사용하여 사용자가 클릭하는 위치 이해](./media/app-insights-usage-flows/flows-one-step.png)

<span data-ttu-id="9a09e-140">초기 이벤트가 페이지 보기인 경우 시각화의 첫 번째 열("1단계")은 페이지를 방문한 직후 사용자가 수행하는 작업을 신속하게 이해하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-140">If your initial event is a page view, the first column ("Step 1") of the visualization is a quick way to understand what users did immediately after visiting the page.</span></span> <span data-ttu-id="9a09e-141">사용자 흐름 시각화 옆에 있는 창에서 사이트를 열어 보세요.</span><span class="sxs-lookup"><span data-stu-id="9a09e-141">Try opening your site in a window next to the User Flows visualization.</span></span> <span data-ttu-id="9a09e-142">사용자가 "1단계" 열에 있는 이벤트 목록의 페이지와 상호 작용하는 방법을 예상과 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-142">Compare your expectations of how users interact with the page to the list of events in the "Step 1" column.</span></span> <span data-ttu-id="9a09e-143">종종 팀에서 불필요해 보이는 페이지의 UI 요소가 페이지에서 가장 많이 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-143">Often, a UI element on the page that seems insignificant to your team can be among the most-used on the page.</span></span> <span data-ttu-id="9a09e-144">사이트의 설계 향상을 위한 시작점으로 적당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-144">It can be a great starting point for design improvements to your site.</span></span>

<span data-ttu-id="9a09e-145">초기 이벤트가 사용자 지정 이벤트인 경우 첫 번째 열은 해당 작업을 수행한 직후에 사용자가 수행한 작업을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-145">If your initial event is a custom event, the first column shows what users did just after performing that action.</span></span> <span data-ttu-id="9a09e-146">페이지 보기에서 사용자의 관찰된 동작이 팀의 목표 및 예상과 일치하는지를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-146">As with page views, consider if the observed behavior of your users matches your team's goals and expectations.</span></span> <span data-ttu-id="9a09e-147">예를 들어, 선택한 초기 이벤트가 "장바구니에 추가된 항목"인 경우 곧이어 "체크아웃으로 이동" 및 "완료된 구매"가 시각화에 표시되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-147">If your selected initial event is "Added Item to Shopping Cart", for example, look to see if "Go to Checkout" and "Completed Purchase" appear in the visualization shortly thereafter.</span></span> <span data-ttu-id="9a09e-148">사용자 동작이 예상과 훨씬 다른 경우 시각화를 사용하여 사용자가 사이트의 현재 디자인에 의해 "포착"되는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-148">If user behavior is much different from your expectations, use the visualization to understand how users are getting "trapped" by your site's current design.</span></span>

## <a name="where-are-the-places-that-users-churn-most-from-your-site"></a><span data-ttu-id="9a09e-149">사용자가 사이트에서 가장 많이 이탈하는 위치는 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-149">Where are the places that users churn most from your site?</span></span>

<span data-ttu-id="9a09e-150">시각화의 열, 특히 흐름에서 높에 나타나는 "종료된 세션"에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-150">Watch for "Session Ended" nodes that appear high-up in a column in the visualization, especially early in a flow.</span></span> <span data-ttu-id="9a09e-151">즉, 많은 사용자가 페이지와 UI 상호 작용의 이전 경로를 따른 후에 사이트에서 변동했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-151">This means many users probably churned from your site after following the preceding path of pages and UI interactions.</span></span> <span data-ttu-id="9a09e-152">예를 들어, 전자 상거래 사이트에서 구매를 완료한 후와 같은 경우 종종 변동이 예상됩니다. 하지만 변동은 일반적으로 설계 상의 문제, 성능 저하 또는 개선될 수 있는 사이트 관련 기타 문제를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-152">Sometimes churn is expected - after completing a purchase on an eCommerce site, for example - but usually churn is a sign of design problems, poor performance, or other issues with your site that can be improved.</span></span>

<span data-ttu-id="9a09e-153">"종료된 세션" 노드가 이 Application Insights 리소스에 의해 수집된 원격 분석에만 기반한다는 점을 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-153">Keep in mind that "Session Ended" nodes are based only on telemetry collected by this Application Insights resource.</span></span> <span data-ttu-id="9a09e-154">Application Insights가 특정 사용자 상호 작용에 대한 원격 분석을 수신하지 못하면 사용자는 사용자 흐름 도구가 세션을 종료한 후에 해당 방법으로 사이트와 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-154">If Application Insights doesn't receive telemetry for certain user interactions, users could still have interacted with your site in those ways after the User Flows tool says the session ended.</span></span>

## <a name="are-there-places-where-users-repeat-the-same-action-over-and-over"></a><span data-ttu-id="9a09e-155">사용자가 동일한 작업을 반복하는 위치가 있나요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-155">Are there places where users repeat the same action over and over?</span></span>

<span data-ttu-id="9a09e-156">시각화의 후속 단계를 통해 많은 사용자가 반복하는 페이지 보기 또는 사용자 지정 이벤트를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-156">Look for a page view or custom event that is repeated by many users across subsequent steps in the visualization.</span></span> <span data-ttu-id="9a09e-157">즉, 일반적으로 사용자가 사이트에서 반복 작업을 수행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-157">This usually means that users are performing repetitive actions on your site.</span></span> <span data-ttu-id="9a09e-158">반복 작업을 발견한 경우 반복 횟수를 줄이기 위해 사이트의 디자인을 변경하거나 새 기능을 추가하는 방법을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="9a09e-158">If you find repetition, think about changing the design of your site or adding new functionality to reduce repetition.</span></span> <span data-ttu-id="9a09e-159">예를 들어 테이블 요소의 각 행에서 반복되는 동작을 수행하는 사용자를 발견한 경우 대량 편집 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-159">For example, adding bulk edit functionality if you find users performing repetitive actions on each row of a table element.</span></span>

## <a name="common-questions"></a><span data-ttu-id="9a09e-160">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="9a09e-160">Common Questions</span></span>

### <a name="why-do-steps-appear-disconnected"></a><span data-ttu-id="9a09e-161">단계의 연결이 끊기는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-161">Why do steps appear disconnected?</span></span>

![단계의 연결이 끊긴 사용자 흐름](./media/app-insights-usage-flows/flows-disconnected.png)

<span data-ttu-id="9a09e-163">사용자 흐름 시각화의 단계(열)가 연결이 끊긴 경우 단계 간에 사용자가 취한 경로 중 어떤 것도 표시할 만큼 자주 사용하지 않았다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-163">If steps (columns) in a User Flows visualization are disconnected, it means none of the paths taken by users between the steps were frequent enough to be shown.</span></span> <span data-ttu-id="9a09e-164">연결된 단계를 표시하기 위해 시각화에서 자주 사용하지 않는 이벤트를 표시하려면 편집 메뉴에서 "세부 정보 수준" 슬라이더를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-164">To show less frequent events on the visualization so the steps appear connected, adjust the "Detail level" slider in the Edit menu.</span></span>

### <a name="does-the-initial-event-represent-the-first-time-the-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a><span data-ttu-id="9a09e-165">초기 이벤트는 이벤트가 처음으로 세션에 나타나는 경우인가요, 아니면 세션에 나타날 때마다 인가요?</span><span class="sxs-lookup"><span data-stu-id="9a09e-165">Does the initial event represent the first time the event appears in a session, or any time it appears in a session?</span></span>

<span data-ttu-id="9a09e-166">시각화의 초기 이벤트는 처음으로 사용자가 세션 중 해당 페이지 보기 또는 사용자 지정 이벤트를 전송한 경우만을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-166">The initial event on the visualization only represents the first time a user sent that page view or custom event during a session.</span></span> <span data-ttu-id="9a09e-167">사용자가 세션에서 여러 번 초기 이벤트를 전송할 수 있는 경우 "1단계" 열에서는 모든 인스턴스가 아닌 초기 이벤트의 *첫 번째* 인스턴스 이후에 사용자 동작 방식만을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a09e-167">If users can send the initial event multiple times in a session, then the "Step 1" column only shows how users behave after the *first* instance of initial event, not all instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a09e-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a09e-168">Next steps</span></span>

* [<span data-ttu-id="9a09e-169">사용 현황 개요</span><span class="sxs-lookup"><span data-stu-id="9a09e-169">Usage overview</span></span>](app-insights-usage-overview.md)
* [<span data-ttu-id="9a09e-170">사용자, 세션 및 이벤트</span><span class="sxs-lookup"><span data-stu-id="9a09e-170">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
* [<span data-ttu-id="9a09e-171">보존</span><span class="sxs-lookup"><span data-stu-id="9a09e-171">Retention</span></span>](app-insights-usage-retention.md)
* [<span data-ttu-id="9a09e-172">앱에 사용자 지정 이벤트 추가</span><span class="sxs-lookup"><span data-stu-id="9a09e-172">Adding custom events to your app</span></span>](app-insights-api-custom-events-metrics.md)