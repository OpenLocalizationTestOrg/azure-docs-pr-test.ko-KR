---
title: "aaaAnalyze Azure Application Insights의 흐름에서는 사용자를 사용 하는 사용자 탐색 패턴 | Microsoft docs"
description: "Hello 페이지 및 웹 앱의 기능 간에 사용자가 탐색 하는 방식을 분석 합니다."
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
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a><span data-ttu-id="f766e-103">Application Insights에서 사용자 흐름을 사용하여 사용자 탐색 패턴 분석</span><span class="sxs-lookup"><span data-stu-id="f766e-103">Analyze user navigation patterns with User Flows in Application Insights</span></span>

![Application Insights 사용자 흐름 도구](./media/app-insights-usage-flows/flows.png)

<span data-ttu-id="f766e-105">hello 사용자 흐름 도구 hello 페이지 및 사이트의 기능 간에 사용자가 탐색 하는 방식을 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-105">hello User Flows tool visualizes how users navigate between hello pages and features of your site.</span></span> <span data-ttu-id="f766e-106">다음과 같은 질문에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-106">It's great for answering questions like:</span></span>
* <span data-ttu-id="f766e-107">사용자가 사이트 페이지에서 벗어나려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="f766e-107">How do users navigate away from a page on your site?</span></span>
* <span data-ttu-id="f766e-108">사용자가 사이트 페이지에서 어디를 클릭하나요?</span><span class="sxs-lookup"><span data-stu-id="f766e-108">What do users click on a page on your site?</span></span>
* <span data-ttu-id="f766e-109">사용자가 사이트에서 가장 변동는 배치 있는 hello?</span><span class="sxs-lookup"><span data-stu-id="f766e-109">Where are hello places that users churn most from your site?</span></span>
* <span data-ttu-id="f766e-110">여기서 사용자가 반복 hello 동일한 작업을 반복 하는 장소 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f766e-110">Are there places where users repeat hello same action over and over?</span></span>

<span data-ttu-id="f766e-111">hello 사용자 흐름 도구 초기 페이지 뷰 또는 지정 하는 이벤트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-111">hello User Flows tool starts from an initial page view or event that you specify.</span></span> <span data-ttu-id="f766e-112">페이지 보기 및 사용자는 나중에 세션에서 두 단계를 나중에, 등 즉시 연결 하는 사용자 지정 이벤트 표시 hello이 페이지 보기 또는 사용자 지정 이벤트를 전달 하는 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-112">Given this page view or custom event, User Flows shows hello page views and custom events that users sent immediately afterwards during a session, two steps afterwards, and so forth.</span></span> <span data-ttu-id="f766e-113">다양한 두께의 선은 사용자가 따라간 각 경로의 횟수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-113">Lines of varying thickness show how many times each path was followed by users.</span></span> <span data-ttu-id="f766e-114">특별 한 "세션이 종료" 노드는 사용자 수 이후에 보낸 메시지 페이지 뷰 또는 사용자 지정 이벤트가 없습니다 hello 앞에 노드를 사이트에 사용자가 아마도 왼쪽 강조 표시를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-114">Special "Session Ended" nodes show how many users sent no page views or custom events after hello preceding node, highlighting where users probably left your site.</span></span>



> [!NOTE]
> <span data-ttu-id="f766e-115">Application Insights 리소스 페이지 뷰 또는 사용자 지정 이벤트 toouse hello 사용자 흐름 도구에 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-115">Your Application Insights resource must contain page views or custom events toouse hello User Flows tool.</span></span> <span data-ttu-id="f766e-116">[Tooset 앱 toocollect 페이지를 자동으로 hello Application Insights JavaScript SDK로 보는 방법에 대해 알아봅니다](app-insights-javascript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-116">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a><span data-ttu-id="f766e-117">초기 페이지 보기 또는 사용자 지정 이벤트를 선택하여 시작</span><span class="sxs-lookup"><span data-stu-id="f766e-117">Start by choosing an initial page view or custom event</span></span>

![사용자 흐름에 대한 초기 이벤트 선택](./media/app-insights-usage-flows/flows-initial-event.png)

<span data-ttu-id="f766e-119">hello 사용자 흐름 도구를 사용 하는 질문에 대답 시작 tooget 초기 페이지 뷰 또는 사용자 지정 이벤트 tooserve hello 시작 hello 시각화에 대 한 지점으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-119">tooget started answering questions with hello User Flows tool, choose an initial page view or custom event tooserve as hello starting point for hello visualization:</span></span>
1. <span data-ttu-id="f766e-120">Hello hello 링크를 클릭 "않으면 사용자가 수행할 작업 후...?"</span><span class="sxs-lookup"><span data-stu-id="f766e-120">Click hello link in hello "What do users do after...?"</span></span> <span data-ttu-id="f766e-121">제목, 또는 hello 편집 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-121">title, or click hello Edit button.</span></span> 
2. <span data-ttu-id="f766e-122">Hello "초기 이벤트" 드롭다운에서 페이지 보기 또는 사용자 지정 이벤트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-122">Select a page view or custom event from hello "Initial event" dropdown.</span></span>
3. <span data-ttu-id="f766e-123">"그래프 만들기"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-123">Click "Create graph".</span></span>

<span data-ttu-id="f766e-124">hello 시각화의 hello "1 단계" 열 어떤 사용자가 점에 만족 하셨나요 가장 자주 위쪽에서 아래쪽에서 대부분 tooleast를 자주 정렬 hello 초기 이벤트 바로 다음을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-124">hello "Step 1" column of hello visualization shows what users did most frequently just after hello initial event, ordered top-to-bottom from most- tooleast-frequent.</span></span> <span data-ttu-id="f766e-125">사이트를 통해 어떤 사용자가 그 후 모든 hello 방법으로 사용자의 사진 만드는 hello "2 단계" 및 그 열 표시 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-125">hello "Step 2" and subsequent columns show what users did thereafter, creating a picture of all hello ways users have navigated through your site.</span></span>

<span data-ttu-id="f766e-126">기본적으로 hello 사용자 흐름 도구만 hello를 페이지 보기 및 사이트에서 사용자 지정 이벤트의 지난 24 시간 동안 임의로 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-126">By default, hello User Flows tool randomly samples only hello last 24 hours of page views and custom event from your site.</span></span> <span data-ttu-id="f766e-127">Hello 시간 범위를 늘리고 hello 편집 메뉴에서 무작위 샘플링에 대 한 성능 및 정확도의 hello 균형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-127">You can increase hello time range and change hello balance of performance and accuracy for random sampling in hello Edit menu.</span></span>

<span data-ttu-id="f766e-128">일부 hello 페이지 뷰 및 사용자 지정 이벤트 관련 tooyou 하지 않으면 hello "X"를 클릭 하려는 toohide hello 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-128">If some of hello page views and custom events aren't relevant tooyou, click hello "X" on hello nodes you want toohide.</span></span> <span data-ttu-id="f766e-129">원하는 toohide hello 노드를 선택한 후에 hello 시각화 아래 hello "그래프 만들기" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-129">Once you've selected hello nodes you want toohide, click hello "Create graph" button below hello visualization.</span></span> <span data-ttu-id="f766e-130">toosee 모든 hello 노드가 숨겨진 hello 편집 단추를 클릭 하 여 다음에 hello "이벤트 제외" 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-130">toosee all of hello nodes you've hidden, click hello Edit button, then look at hello "Excluded events" section.</span></span>

<span data-ttu-id="f766e-131">페이지 뷰 또는 사용자 지정 이벤트는 누락 된 hello 시각화에서 toosee 예상:</span><span class="sxs-lookup"><span data-stu-id="f766e-131">If page views or custom events are missing that you expect toosee on hello visualization:</span></span>
* <span data-ttu-id="f766e-132">Hello hello 편집 메뉴에서 "제외 된 이벤트" 섹션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-132">Check hello "Excluded events" section in hello Edit menu.</span></span>
* <span data-ttu-id="f766e-133">Hello 편집 메뉴 tooinclude 작음-자주 사용 하는 이벤트 hello 시각화에서에서 hello "세부 정보 수준" 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-133">Use hello "Detail level" control in hello Edit menu tooinclude less-frequent events in hello visualization.</span></span>
* <span data-ttu-id="f766e-134">Hello 페이지 보기 또는 원하는 사용자 지정 이벤트는 사용자가 자주 전달 되 면 hello 편집 메뉴에서 hello 시각화의 증가 hello 시간 범위를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-134">If hello page view or custom event you expect is sent infrequently by users, try increasing hello time range of hello visualization in hello Edit menu.</span></span>
* <span data-ttu-id="f766e-135">있는지 hello 페이지 보기 또는 hello Application Insights SDK 사이트의 hello 소스 코드에 의해 수집 된 toobe 설정 하려는 사용자 지정 이벤트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-135">Make sure hello page view or custom event you expect is set up toobe collected by hello Application Insights SDK in hello source code of your site.</span></span> [<span data-ttu-id="f766e-136">사용자 지정 이벤트 수집에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-136">Learn more about collecting custom events.</span></span>](app-insights-api-custom-events-metrics.md)

<span data-ttu-id="f766e-137">원하는 경우 hello 시각화를 사용 하 여 hello "단계 수가" 슬라이더 hello에서의 단계를 자세히 toosee 메뉴를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-137">If you want toosee more steps in hello visualization, use hello "Number of steps" slider in hello Edit menu.</span></span>

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a><span data-ttu-id="f766e-138">페이지 또는 기능을 방문한 후에 사용자가 어디로 이동하고 어떤 항목을 클릭하나요?</span><span class="sxs-lookup"><span data-stu-id="f766e-138">After visiting a page or feature, where do users go and what do they click?</span></span>

![사용자가 클릭할 수 있는 toounderstand 사용자 흐름 사용](./media/app-insights-usage-flows/flows-one-step.png)

<span data-ttu-id="f766e-140">초기 이벤트 페이지 보기 이면 hello 시각화의 hello 첫 번째 열 ("단계 1")는 hello 페이지를 방문한 직후 사용자가 신속 하 게 toounderstand 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-140">If your initial event is a page view, hello first column ("Step 1") of hello visualization is a quick way toounderstand what users did immediately after visiting hello page.</span></span> <span data-ttu-id="f766e-141">창 다음 toohello 사용자 흐름 시각화에서에서 사이트를 열어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="f766e-141">Try opening your site in a window next toohello User Flows visualization.</span></span> <span data-ttu-id="f766e-142">사용자가 hello "1 단계" 열에 있는 이벤트 목록은 페이지 toohello hello 상호 작용 하는 방법의 예상과 다를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-142">Compare your expectations of how users interact with hello page toohello list of events in hello "Step 1" column.</span></span> <span data-ttu-id="f766e-143">종종 무효 tooyour 팀 보이는 hello 페이지에는 UI 요소는 hello 페이지에서 대부분 사용 하는 hello 간에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-143">Often, a UI element on hello page that seems insignificant tooyour team can be among hello most-used on hello page.</span></span> <span data-ttu-id="f766e-144">디자인 개선 tooyour 사이트에 대 한 좋은 시작 지점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-144">It can be a great starting point for design improvements tooyour site.</span></span>

<span data-ttu-id="f766e-145">초기 이벤트는 사용자 지정 이벤트, 사용자가 해당 작업을 수행 하는 바로 뒤 म hello 첫 번째 열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-145">If your initial event is a custom event, hello first column shows what users did just after performing that action.</span></span> <span data-ttu-id="f766e-146">페이지 보기와 마찬가지로 경우 hello 동작의 사용자 일치 팀의 목표와 기대치를 관찰 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-146">As with page views, consider if hello observed behavior of your users matches your team's goals and expectations.</span></span> <span data-ttu-id="f766e-147">선택한 초기 이벤트 "Added 항목 tooShopping 카트" 예를 들어 확인 toosee 경우 "Go tooCheckout" 및 "완료 구매" hello 시각화 잠시 후에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-147">If your selected initial event is "Added Item tooShopping Cart", for example, look toosee if "Go tooCheckout" and "Completed Purchase" appear in hello visualization shortly thereafter.</span></span> <span data-ttu-id="f766e-148">사용자 동작이 예상과 다를 경우 hello 시각화 toounderstand 어떻게 사용자는 가져오는 "트랩" 현재 사이트의 설계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-148">If user behavior is much different from your expectations, use hello visualization toounderstand how users are getting "trapped" by your site's current design.</span></span>

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a><span data-ttu-id="f766e-149">사용자가 사이트에서 가장 변동는 배치 있는 hello?</span><span class="sxs-lookup"><span data-stu-id="f766e-149">Where are hello places that users churn most from your site?</span></span>

<span data-ttu-id="f766e-150">높은 접속 나타나는 "세션이 종료" 노드에 대 한 조사식 흐름 특히 초기에 hello 시각화의 열에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-150">Watch for "Session Ended" nodes that appear high-up in a column in hello visualization, especially early in a flow.</span></span> <span data-ttu-id="f766e-151">이 많은 사용자가 다음 페이지와 상호 작용 UI의 이전 경로 hello 후 사이트에서 churned 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-151">This means many users probably churned from your site after following hello preceding path of pages and UI interactions.</span></span> <span data-ttu-id="f766e-152">예를 들어, 전자 상거래 사이트에서 구매를 완료한 후와 같은 경우 종종 변동이 예상됩니다. 하지만 변동은 일반적으로 설계 상의 문제, 성능 저하 또는 개선될 수 있는 사이트 관련 기타 문제를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-152">Sometimes churn is expected - after completing a purchase on an eCommerce site, for example - but usually churn is a sign of design problems, poor performance, or other issues with your site that can be improved.</span></span>

<span data-ttu-id="f766e-153">"종료된 세션" 노드가 이 Application Insights 리소스에 의해 수집된 원격 분석에만 기반한다는 점을 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-153">Keep in mind that "Session Ended" nodes are based only on telemetry collected by this Application Insights resource.</span></span> <span data-ttu-id="f766e-154">Application Insights는 특정 사용자 상호 작용에 대 한 원격 분석을 받지 못하면, 사용자 수 여전히 있는와 상호 작용할 이러한 방법으로 사이트 hello 사용자 흐름 도구 표시 hello 세션이 종료 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-154">If Application Insights doesn't receive telemetry for certain user interactions, users could still have interacted with your site in those ways after hello User Flows tool says hello session ended.</span></span>

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a><span data-ttu-id="f766e-155">여기서 사용자가 반복 hello 동일한 작업을 반복 하는 장소 있습니까?</span><span class="sxs-lookup"><span data-stu-id="f766e-155">Are there places where users repeat hello same action over and over?</span></span>

<span data-ttu-id="f766e-156">페이지 보기 또는 hello 시각화의 후속 단계를 통해 많은 사용자가 반복 되는 사용자 지정 이벤트를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="f766e-156">Look for a page view or custom event that is repeated by many users across subsequent steps in hello visualization.</span></span> <span data-ttu-id="f766e-157">즉, 일반적으로 사용자가 사이트에서 반복 작업을 수행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-157">This usually means that users are performing repetitive actions on your site.</span></span> <span data-ttu-id="f766e-158">반복을 찾을 경우 사이트의 hello 디자인을 변경 하거나 새 기능 tooreduce 반복을 추가 하는 방법에 대 한 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-158">If you find repetition, think about changing hello design of your site or adding new functionality tooreduce repetition.</span></span> <span data-ttu-id="f766e-159">예를 들어 테이블 요소의 각 행에서 반복되는 동작을 수행하는 사용자를 발견한 경우 대량 편집 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-159">For example, adding bulk edit functionality if you find users performing repetitive actions on each row of a table element.</span></span>

## <a name="common-questions"></a><span data-ttu-id="f766e-160">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="f766e-160">Common Questions</span></span>

### <a name="why-do-steps-appear-disconnected"></a><span data-ttu-id="f766e-161">단계의 연결이 끊기는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f766e-161">Why do steps appear disconnected?</span></span>

![단계의 연결이 끊긴 사용자 흐름](./media/app-insights-usage-flows/flows-disconnected.png)

<span data-ttu-id="f766e-163">단계 (열) 사용자 흐름 시각화에서 연결이 끊긴 경우 자주 수행 하도록 toobe 표시 된 hello 단계 사이 사용자를 차지 하는 hello 경로 없음 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-163">If steps (columns) in a User Flows visualization are disconnected, it means none of hello paths taken by users between hello steps were frequent enough toobe shown.</span></span> <span data-ttu-id="f766e-164">덜 자주 이벤트 hello 시각화에서 tooshow hello 단계 연결 됨, 표시 슬라이더를 조정 hello "세부 정보 수준" hello 편집 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="f766e-164">tooshow less frequent events on hello visualization so hello steps appear connected, adjust hello "Detail level" slider in hello Edit menu.</span></span>

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a><span data-ttu-id="f766e-165">Hello 초기 이벤트 나타내는 hello 첫 번째 시간 hello 이벤트 세션에서 나타납니다 또는 세션에 나타나는 언제 든 지?</span><span class="sxs-lookup"><span data-stu-id="f766e-165">Does hello initial event represent hello first time hello event appears in a session, or any time it appears in a session?</span></span>

<span data-ttu-id="f766e-166">hello hello 시각화에서 초기 이벤트는만 hello를 세션 중 해당 페이지 보기 또는 사용자 지정 이벤트를 전송 하는 사용자는 처음으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f766e-166">hello initial event on hello visualization only represents hello first time a user sent that page view or custom event during a session.</span></span> <span data-ttu-id="f766e-167">사용자가 세션에서 여러 번 hello 초기 이벤트를 보낼 수 있으면 hello "1 단계" 열만 hello 후 사용자가 동작 하는 방법을 보여 줍니다 *첫 번째* 초기 이벤트의 인스턴스, 모든 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f766e-167">If users can send hello initial event multiple times in a session, then hello "Step 1" column only shows how users behave after hello *first* instance of initial event, not all instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f766e-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f766e-168">Next steps</span></span>

* [<span data-ttu-id="f766e-169">사용 현황 개요</span><span class="sxs-lookup"><span data-stu-id="f766e-169">Usage overview</span></span>](app-insights-usage-overview.md)
* [<span data-ttu-id="f766e-170">사용자, 세션 및 이벤트</span><span class="sxs-lookup"><span data-stu-id="f766e-170">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
* [<span data-ttu-id="f766e-171">보존</span><span class="sxs-lookup"><span data-stu-id="f766e-171">Retention</span></span>](app-insights-usage-retention.md)
* [<span data-ttu-id="f766e-172">사용자 지정 이벤트 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="f766e-172">Adding custom events tooyour app</span></span>](app-insights-api-custom-events-metrics.md)
