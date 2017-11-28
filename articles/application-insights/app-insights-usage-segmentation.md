---
title: "Azure Application Insights에서 aaaUser, 세션 및 이벤트 분석 | Microsoft docs"
description: "웹앱의 사용자 인구 통계 분석입니다."
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="f1204-103">Application Insights의 사용자, 세션 및 이벤트 분석</span><span class="sxs-lookup"><span data-stu-id="f1204-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="f1204-104">사람들이 사용자의 웹앱을 사용하는 경우, 가장 큰 관심을 갖는 페이지, 사용자가 있는 위치 및 사용하는 브라우저 및 운영 체제를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="f1204-105">[Azure Application Insights](app-insights-overview.md)를 사용하여 업무 및 원격 사용을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="f1204-106">시작</span><span class="sxs-lookup"><span data-stu-id="f1204-106">Get started</span></span>

<span data-ttu-id="f1204-107">Hello 사용자, 세션 또는 이벤트 블레이드 hello Application Insights 포털에서에서 데이터를 아직 표시 되지 않으면 [tooget hello 사용량 도구를 시작 하는 방법에 대해 알아봅니다](app-insights-usage-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="f1204-108">hello 사용자, 세션 및 이벤트 조각화 도구</span><span class="sxs-lookup"><span data-stu-id="f1204-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="f1204-109">동일한 도구 tooslice 분리 및 분할에서에서 원격 분석 세 가지 관점에서 웹 응용 프로그램을 hello 블레이드를 사용 하는 hello 사용 중 3 개.</span><span class="sxs-lookup"><span data-stu-id="f1204-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="f1204-110">를 필터링 및 hello 데이터 분할 hello 상대 사용의 다른 페이지 및 기능에 대 한 통찰력을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="f1204-111">**사용자 도구**: 사용자의 앱 및 해당 기능을 사용한 사람의 수.</span><span class="sxs-lookup"><span data-stu-id="f1204-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="f1204-112">사용자 수는 브라우저 쿠키에 저장되는 익명 ID를 사용하여 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="f1204-113">여러 브라우저 또는 컴퓨터를 사용하는 한 사람은 둘 이상의 사용자로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="f1204-114">**세션 도구**: 앱의 특정 페이지 및 기능을 포함하는 사용자 활동 세션의 수.</span><span class="sxs-lookup"><span data-stu-id="f1204-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="f1204-115">사용자의 비활동 상태가 30분 경과된 이후 또는 연속해서 24시간 사용한 후에 세션 수가 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="f1204-116">**이벤트 도구**: 앱의 특정 페이지 및 기능이 사용되는 빈도.</span><span class="sxs-lookup"><span data-stu-id="f1204-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="f1204-117">사용자가 [앱을 계측](app-insights-javascript.md)한 경우 페이지 보기 횟수는 브라우저가 앱에서 페이지를 로드할 때 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="f1204-118">사용자 지정 이벤트는 주로 사용자 상호 작용 하는 단추를 클릭 하거나 일부 작업의 완료를 hello와 같은 응용 프로그램에서 발생 하는 것에 대 한 항목을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="f1204-119">코드에에서 삽입할 앱 너무[사용자 지정 이벤트를 생성](app-insights-api-custom-events-metrics.md#trackevent)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![사용 도구](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="f1204-121">특정 사용자에 대해 쿼리</span><span class="sxs-lookup"><span data-stu-id="f1204-121">Querying for Certain Users</span></span> 

<span data-ttu-id="f1204-122">Hello 위쪽 hello 사용자 도구에 hello 쿼리 옵션을 조정 하 여 서로 다른 사용자 그룹을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="f1204-123">사용한 사람: 사용자 지정 이벤트 및 페이지 보기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="f1204-124">기간: 시간 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="f1204-125">: 하 여 일정 시간 동안 또는 브라우저 또는 도시와 같은 다른 속성 데이터를 toobucket hello 하는 방법을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="f1204-126">분할에: toosplit 또는 세그먼트 hello 데이터 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="f1204-127">필터 추가: hello 쿼리 toocertain 사용자, 세션 또는 브라우저 또는 도시 등의 속성을 기준으로 이벤트를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="f1204-128">보고서 저장 및 공유</span><span class="sxs-lookup"><span data-stu-id="f1204-128">Saving and sharing reports</span></span> 
<span data-ttu-id="f1204-129">Hello 공유 보고서 섹션의에서 모든 액세스 toothis Application Insights 리소스를 가진 다른 사용자와 공유 하거나 hello 내 보고서 섹션의 두 개인 정당한 tooyou, 사용자가 보고서를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="f1204-130">보고서 저장 또는 속성을 편집 하는 동안 보고서는 지속적으로 "현재 상대 시간 범위" toosave 시간의 일부 고정된 크기를 다시 살펴보자면, 데이터 새로 고침을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="f1204-131">"현재 절대 시간 범위" toosave 고정된 데이터 집합을 사용 하 여 보고서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="f1204-132">Application Insights에서 데이터는 90 일 이상 된 절대 시간 범위를 사용 하 여 보고서 이후 경과한 경우 저장 하므로 90 일 동안만 저장 점을 염두에 hello 보고서를 빈 상태로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="f1204-133">예제 인스턴스</span><span class="sxs-lookup"><span data-stu-id="f1204-133">Example instances</span></span>

<span data-ttu-id="f1204-134">hello 인스턴스 "예" 섹션에서는 몇 가지 개별 사용자, 세션 또는 hello 현재 쿼리를 통해 일치 하는 이벤트에 대 한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="f1204-135">또한 tooaggregates에서 개인의 hello 동작 하는 방법과 고려 실제로 사용자 응용 프로그램의 사용 방법에 대 한 통찰력을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="f1204-136">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f1204-136">Insights</span></span> 

<span data-ttu-id="f1204-137">hello Insights 사이드바 공용 속성을 공유 하는 사용자의 큰 클러스터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="f1204-138">이러한 클러스터는 사람들이 사용자의 앱을 사용하는 방식에 대한 놀라운 추세를 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="f1204-139">예를 들어, 모든 응용 프로그램의 hello 사용의 40%는 하나의 기능을 사용 하는 사용자에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="f1204-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1204-140">Next steps</span></span>
- <span data-ttu-id="f1204-141">tooenable 사용 경험을 보내기 시작 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1204-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="f1204-142">사용자 지정 이벤트 또는 페이지 뷰 탐색 hello 사용 도구 toolearn 이미 보낼 사용자 서비스를 사용할 방법.</span><span class="sxs-lookup"><span data-stu-id="f1204-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="f1204-143">깔때기</span><span class="sxs-lookup"><span data-stu-id="f1204-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="f1204-144">보존</span><span class="sxs-lookup"><span data-stu-id="f1204-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="f1204-145">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="f1204-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="f1204-146">통합 문서</span><span class="sxs-lookup"><span data-stu-id="f1204-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="f1204-147">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="f1204-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

