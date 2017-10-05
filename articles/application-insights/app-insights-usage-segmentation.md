---
title: "Azure Application Insights의 사용자, 세션 및 이벤트 분석 | Microsoft Docs"
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="7b797-103">Application Insights의 사용자, 세션 및 이벤트 분석</span><span class="sxs-lookup"><span data-stu-id="7b797-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="7b797-104">사람들이 사용자의 웹앱을 사용하는 경우, 가장 큰 관심을 갖는 페이지, 사용자가 있는 위치 및 사용하는 브라우저 및 운영 체제를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="7b797-105">[Azure Application Insights](app-insights-overview.md)를 사용하여 업무 및 원격 사용을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="7b797-106">시작</span><span class="sxs-lookup"><span data-stu-id="7b797-106">Get started</span></span>

<span data-ttu-id="7b797-107">Application Insights 포털에 사용자, 세션 또는 이벤트 블레이드에서 아직 데이터가 표시되지 않으면 [사용 도구 시작 방법을 알아봅니다](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b797-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="7b797-108">사용자, 세션 및 이벤트 구분 도구</span><span class="sxs-lookup"><span data-stu-id="7b797-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="7b797-109">이러한 세 가지 사용 블레이드는 동일한 도구를 사용하여 3가지 관점에서 웹앱의 원격 분석을 분할 및 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="7b797-110">데이터를 필터링하고 분할하여 여러 다른 페이지 및 기능의 상대적 사용을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="7b797-111">**사용자 도구**: 사용자의 앱 및 해당 기능을 사용한 사람의 수.</span><span class="sxs-lookup"><span data-stu-id="7b797-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="7b797-112">사용자 수는 브라우저 쿠키에 저장되는 익명 ID를 사용하여 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="7b797-113">여러 브라우저 또는 컴퓨터를 사용하는 한 사람은 둘 이상의 사용자로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="7b797-114">**세션 도구**: 앱의 특정 페이지 및 기능을 포함하는 사용자 활동 세션의 수.</span><span class="sxs-lookup"><span data-stu-id="7b797-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="7b797-115">사용자의 비활동 상태가 30분 경과된 이후 또는 연속해서 24시간 사용한 후에 세션 수가 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="7b797-116">**이벤트 도구**: 앱의 특정 페이지 및 기능이 사용되는 빈도.</span><span class="sxs-lookup"><span data-stu-id="7b797-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="7b797-117">사용자가 [앱을 계측](app-insights-javascript.md)한 경우 페이지 보기 횟수는 브라우저가 앱에서 페이지를 로드할 때 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="7b797-118">사용자 지정 이벤트는 앱에서 어떤 동작이 한 번 발생하는 경우를 나타냅니다. 주로 단추 클릭 또는 특정 작업 완료 등과 같은 사용자 상호 작용이 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="7b797-119">앱에 [사용자 지정 이벤트를 생성](app-insights-api-custom-events-metrics.md#trackevent)하는 코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![사용 도구](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="7b797-121">특정 사용자에 대해 쿼리</span><span class="sxs-lookup"><span data-stu-id="7b797-121">Querying for Certain Users</span></span> 

<span data-ttu-id="7b797-122">사용자 도구 맨 위에 있는 쿼리 옵션을 조정하여 다른 사용자 그룹을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="7b797-123">사용한 사람: 사용자 지정 이벤트 및 페이지 보기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="7b797-124">기간: 시간 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="7b797-125">기준: 기간 또는 기타 속성(예: 브라우저 또는 도시) 중에서 데이터를 버킷팅하는 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="7b797-126">분할 기준: 데이터를 분할하거나 분리하는 기준 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="7b797-127">필터 추가: 속성(예: 브라우저 또는 도시)을 기준으로 특정 사용자, 세션 또는 이벤트로 쿼리를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="7b797-128">보고서 저장 및 공유</span><span class="sxs-lookup"><span data-stu-id="7b797-128">Saving and sharing reports</span></span> 
<span data-ttu-id="7b797-129">사용자 보고서를 내 보고서 섹션에서 사용자 본인만 볼 수 있게 저장하거나, 공유 보고서 섹션에서 이 Application Insights 리소스에 액세스할 수 있는 모든 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="7b797-130">보고서를 저장하거나 해당 속성을 편집하는 동안 "현재 상대 시간 범위"를 선택하여 보고서를 저장하면 정해진 시간 이전으로 돌아가 데이터가 계속 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="7b797-131">"현재 절대 시간 범위"를 선택하여 고정된 데이터 집합을 포함하는 보고서를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="7b797-132">Application Insights의 데이터는 90일 동안만 저장되므로 절대 시간 범위가 지정된 보고서를 저장하고 90일이 경과되면 보고서는 빈 상태로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="7b797-133">예제 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7b797-133">Example instances</span></span>

<span data-ttu-id="7b797-134">예제 인스턴스 섹션에서는 현재 쿼리와 일치하는 일부 개별 사용자, 세션 또는 이벤트에 대한 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="7b797-135">집계 외에, 개인의 동작을 고려하고 탐색하면 사람들이 실제로 앱을 사용하는 방식을 이해할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="7b797-136">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7b797-136">Insights</span></span> 

<span data-ttu-id="7b797-137">자세한 정보 사이드바에는 공통 속성을 공유하는 대규모 사용자 클러스터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="7b797-138">이러한 클러스터는 사람들이 사용자의 앱을 사용하는 방식에 대한 놀라운 추세를 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="7b797-139">예를 들어 모든 앱 사용의 40%를 단일 기능을 사용하는 사람들이 반영할 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="7b797-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b797-140">Next steps</span></span>
- <span data-ttu-id="7b797-141">사용 현황 환경을 활성화하려면 [사용자 지정 이벤트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) 또는 [페이지 보기](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views) 보내기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="7b797-142">사용자 지정 이벤트 또는 페이지 보기를 이미 보낸 경우 사용자가 서비스를 사용하는 방법에 대해 알아보려면 사용 현황 도구를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b797-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="7b797-143">깔때기</span><span class="sxs-lookup"><span data-stu-id="7b797-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="7b797-144">보존</span><span class="sxs-lookup"><span data-stu-id="7b797-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="7b797-145">사용자 흐름</span><span class="sxs-lookup"><span data-stu-id="7b797-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="7b797-146">통합 문서</span><span class="sxs-lookup"><span data-stu-id="7b797-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="7b797-147">사용자 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="7b797-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

