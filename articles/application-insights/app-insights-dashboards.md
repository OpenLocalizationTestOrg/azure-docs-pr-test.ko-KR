---
title: "Azure Application Insights의 대시보드 및 탐색 | Microsoft Docs"
description: "키 APM 차트 및 쿼리의 뷰를 만듭니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="cedc5-103">Application Insights 포털에서 탐색 및 대시보드</span><span class="sxs-lookup"><span data-stu-id="cedc5-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="cedc5-104">[프로젝트에서 Application Insights를 설정](app-insights-overview.md)하면 앱의 성능 및 사용에 대한 원격 분석 데이터가 [Azure Portal](https://portal.azure.com)에서 프로젝트의 Application Insights 리소스에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="cedc5-105">원격 분석 찾기</span><span class="sxs-lookup"><span data-stu-id="cedc5-105">Find your telemetry</span></span>
<span data-ttu-id="cedc5-106">[Azure Portal](https://portal.azure.com)에 로그인하고 앱에 대해 만든 Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![찾아보기를 클릭하고 Application Insights를 선택한 후 앱을 선택합니다.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="cedc5-108">앱의 개요 블레이드(페이지)는 앱의 주요 진단 메트릭 요약을 보여 주며 포털의 다른 기능에 대한 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![원격 분석을 보기 위한 주요 경로](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="cedc5-110">차트 및 표를 사용자 지정하고 이를 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="cedc5-111">이런 방식으로 중앙 대시보드에 있는 여러 다른 앱의 주요 원격 분석을 함께 불러올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="cedc5-112">대시보드</span><span class="sxs-lookup"><span data-stu-id="cedc5-112">Dashboards</span></span>
<span data-ttu-id="cedc5-113">[Microsoft Azure 포털](https://portal.azure.com) 에 로그인한 후 가장 먼저 표시되는 것이 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="cedc5-114">[Azure Application Insights](app-insights-overview.md)의 원격 분석을 포함하여, 모든 Azure 리소스에서 가장 중요한 차트를 이곳에 한데 모을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![사용자 지정 대시보드입니다.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="cedc5-116">Application Insights의 앱과 같이 **특정 리소스로 이동**합니다. 왼쪽 막대를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="cedc5-117">**현재 대시보드도 돌아가거나** 최근의 다른 뷰로 전환합니다. 왼쪽 위에 있는 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="cedc5-118">**대시보드 전환**: 대시보드 제목에 있는 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="cedc5-119">대시보드 도구 모음을 사용하여 **대시보드를 만들고, 편집하고, 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="cedc5-120">**대시보드 편집**: 타일을 포인터로 가리킨 다음 그 위쪽 막대를 사용하여 타일을 이동, 사용자 지정 또는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="cedc5-121">대시보드 추가</span><span class="sxs-lookup"><span data-stu-id="cedc5-121">Add to a dashboard</span></span>
<span data-ttu-id="cedc5-122">특히 흥미로운 블레이드나 차트를 보는 경우 그 사본을 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="cedc5-123">이 경우 다음에 대시보드로 돌아가면 해당 블레이드나 차트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-123">You'll see it next time you return there.</span></span>

![차트를 고정하려면 차트 위에 마우스를 놓고 헤더에서 "..."를 클릭합니다.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="cedc5-125">대시보드에 차트를 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-125">Pin chart to dashboard.</span></span> <span data-ttu-id="cedc5-126">차트의 복사본이 대시보드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="cedc5-127">전체 블레이드를 대시보드에 고정합니다 - 대시보드에서 클릭할 수 있는 타일로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="cedc5-128">현재 대시보드 돌아가려면 왼쪽 위의 모퉁이를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="cedc5-129">그런 다음 현재 보기로 돌아가려면 드롭다운 메뉴를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="cedc5-130">차트는 타일로 그룹화되고 타일은 둘 이상의 차트를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="cedc5-131">타일 전체를 대시보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="cedc5-132">차트는 차트의 시간 범위에 따라 달라지는 빈도로 자동으로 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="cedc5-133">시간 범위 최대 1시간: 5분마다 새로 고침</span><span class="sxs-lookup"><span data-stu-id="cedc5-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="cedc5-134">시간 범위 1 - 24시간: 15분마다 새로 고침</span><span class="sxs-lookup"><span data-stu-id="cedc5-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="cedc5-135">시간 범위 24시간 초과: (시간 범위)/60</span><span class="sxs-lookup"><span data-stu-id="cedc5-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="cedc5-136">분석에서 모든 쿼리를 고정</span><span class="sxs-lookup"><span data-stu-id="cedc5-136">Pin any query in Analytics</span></span>
<span data-ttu-id="cedc5-137">[공유](#share-dashboards-with-your-team) 대시보드에 [분석 차트를 고정](app-insights-analytics-using.md#pin-to-dashboard)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="cedc5-138">그러면 임의 쿼리의 차트를 표준 메트릭과 함께 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="cedc5-139">결과는 1시간마다 자동으로 다시 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="cedc5-140">즉시 다시 계산하려면 새로 고침 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="cedc5-141">브라우저 새로 고침은 다시 계산하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="cedc5-142">대시보드에서 타일을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="cedc5-143">타일이 대시보드에 있으면, 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![차트를 편집하려면 차트를 마우스로 가리킵니다.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="cedc5-145">타일에 차트 추가</span><span class="sxs-lookup"><span data-stu-id="cedc5-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="cedc5-146">메트릭, group-by 차원 및 차트의 스타일(테이블, 그래프)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="cedc5-147">끌어서 다이어그램을 확대합니다. timespan을 다시 설정하려면 실행 취소 단추를 클릭합니다. 타일에서 차트에 대한 필터 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="cedc5-148">타일 제목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-148">Set tile title.</span></span>

<span data-ttu-id="cedc5-149">메트릭 탐색기 블레이드에서 고정된 타일에는 개요 블레이드에서 고정된 타일보다 편집 옵션이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="cedc5-150">고정해 놓은 원래 타일은 편집의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="cedc5-151">대시보드 사이 전환</span><span class="sxs-lookup"><span data-stu-id="cedc5-151">Switch between dashboards</span></span>
<span data-ttu-id="cedc5-152">둘 이상의 대시보드를 저장하고 해당 대시보드 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="cedc5-153">차트나 블레이드를 고정하면 현재 대시보드에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![대시보드 간에 전환하려면 대시보드를 클릭하고 저장된 대시보드를 선택합니다.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="cedc5-157">예를 들어 단체방에서 전체 화면을 표시하는 대시보드와 일반 개발용 대시보드를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="cedc5-158">대시보드에서 블레이드는 타일로 표시됩니다. 이를 클릭하면 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="cedc5-159">차트는 원래 위치에 있는 차트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-159">A chart replicates the chart in its original location.</span></span>

![타일이 나타내는 블레이드를 열려면 타일을 클릭합니다.](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="cedc5-161">대시보드 공유</span><span class="sxs-lookup"><span data-stu-id="cedc5-161">Share dashboards</span></span>
<span data-ttu-id="cedc5-162">대시보드를 만들면 다른 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-162">When you've created a dashboard, you can share it with other users.</span></span>

![대시보드 헤더에서 공유를 클릭합니다.](./media/app-insights-dashboards/41.png)

<span data-ttu-id="cedc5-164">[역할 및 액세스 제어](app-insights-resources-roles-access-control.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cedc5-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="cedc5-165">앱 탐색</span><span class="sxs-lookup"><span data-stu-id="cedc5-165">App navigation</span></span>
<span data-ttu-id="cedc5-166">개요 블레이드는 앱에 대한 자세한 정보를 제공하는 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="cedc5-167">**모든 차트 또는 타일** - 원하는 타일 또는 차트를 클릭하여 표시되는 내용에 대한 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="cedc5-168">개요 블레이드 단추</span><span class="sxs-lookup"><span data-stu-id="cedc5-168">Overview blade buttons</span></span>
![개요 블레이드 위쪽 탐색 모음](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="cedc5-170">[**메트릭 탐색기**](app-insights-metrics-explorer.md) - 성능 및 사용에 대한 사용자 고유의 차트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="cedc5-171">[**검색**](app-insights-diagnostic-search.md) - 요청, 예외 또는 로그 추적과 같은 이벤트의 특정 인스턴스를 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="cedc5-172">[**분석**](app-insights-analytics.md) - 원격 분석을 통해 강력한 쿼리를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="cedc5-173">**시간 범위** - 블레이드의 모든 차트에서 표시되는 범위를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="cedc5-174">**삭제** - 앱에 대한 Application Insights 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="cedc5-175">또한 앱 코드에서 Application Insights 패키지를 제거하거나 앱에서 [계측 키](app-insights-create-new-resource.md#copy-the-instrumentation-key)를 편집하여 다른 Application Insights 리소스에 원격 분석을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="cedc5-176">Essentials 탭</span><span class="sxs-lookup"><span data-stu-id="cedc5-176">Essentials tab</span></span>
* <span data-ttu-id="cedc5-177">[계측 키](app-insights-create-new-resource.md#copy-the-instrumentation-key) - 이 앱 리소스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="cedc5-178">가격 - 기능을 사용할 수 있게 하고 볼륨 한도를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="cedc5-179">앱 탐색 모음</span><span class="sxs-lookup"><span data-stu-id="cedc5-179">App navigation bar</span></span>
![왼쪽 탐색 모음](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="cedc5-181">**개요** - 앱 개요 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="cedc5-182">**활동 로그** - 경고 및 Azure 관리 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="cedc5-183">[**액세스 제어**](app-insights-resources-roles-access-control.md) - 팀 멤버 및 다른 사용자에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="cedc5-184">[**태그**](../azure-resource-manager/resource-group-using-tags.md) - 태그를 사용하여 다른 사용자와 앱을 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="cedc5-185">조사</span><span class="sxs-lookup"><span data-stu-id="cedc5-185">INVESTIGATE</span></span>

* <span data-ttu-id="cedc5-186">[**응용 프로그램 맵**](app-insights-app-map.md) - 종속성 정보에서 파생된 응용 프로그램의 구성 요소를 표시하는 활성 맵입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="cedc5-187">[**스마트 감지**](app-insights-proactive-diagnostics.md) - 최근 성능 경고를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="cedc5-188">[**라이브 스트림**](app-insights-live-stream.md) - 거의 즉각적인 고정된 메트릭 집합을 제공하며, 새 빌드를 배포 또는 디버깅할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="cedc5-189">[**가용성/웹 테스트**](app-insights-monitor-web-app-availability.md) - 전세계에서 웹앱에 일반 요청을 전송합니다.*</span><span class="sxs-lookup"><span data-stu-id="cedc5-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="cedc5-190">[**오류, 성능**](app-insights-web-monitor-performance.md) - 사용자의 앱에 대한 요청 및 사용자 앱의 [종속성](app-insights-asp-net-dependencies.md)에 대한 요청의 예외, 실패율 및 응답 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="cedc5-191">[**성능**](app-insights-web-monitor-performance.md) - 응답 시간, 종속성 응답 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="cedc5-192">[서버](app-insights-web-monitor-performance.md) - 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="cedc5-193">[상태 모니터를 설치하면](app-insights-monitor-performance-live-website-now.md)사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="cedc5-194">**브라우저** - 페이지 뷰 및 AJAX 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="cedc5-195">[웹 페이지를 계측할 때](app-insights-javascript.md)사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="cedc5-196">**사용** - 페이지 조회수, 사용자 및 세션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="cedc5-197">[웹 페이지를 계측할 때](app-insights-javascript.md)사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="cedc5-198">구성</span><span class="sxs-lookup"><span data-stu-id="cedc5-198">CONFIGURE</span></span>

* <span data-ttu-id="cedc5-199">**시작하기** - 인라인 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="cedc5-200">**속성** - 계측 키, 구독 및 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="cedc5-201">[경고](app-insights-alerts.md) -메트릭 경고 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="cedc5-202">[연속 내보내기](app-insights-export-telemetry.md) - Azure Storage에 대한 원격 분석 내보내기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="cedc5-203">[성능 테스트](app-insights-monitor-web-app-availability.md#performance-tests) -웹 사이트에 대한 종합 부하를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="cedc5-204">[할당량 및 가격 책정](app-insights-pricing.md)과 [수집 샘플링](app-insights-sampling.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="cedc5-205">**API 액세스** - [릴리스 주석](app-insights-annotations.md)을 작성하고 데이터 액세스 API에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="cedc5-206">[**작업 항목**](app-insights-diagnostic-search.md#create-work-item) - 작업 추적 시스템과 연결하여 원격 분석을 검사하는 동안 버그를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="cedc5-207">설정</span><span class="sxs-lookup"><span data-stu-id="cedc5-207">SETTINGS</span></span>

* <span data-ttu-id="cedc5-208">[**잠금**](../azure-resource-manager/resource-group-lock-resources.md) - Azure 리소스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="cedc5-209">[**스크립트 자동화**](app-insights-powershell.md) - Azure 리소스의 정의를 내보내서 새로운 리소스의 템플릿으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cedc5-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="cedc5-210">비디오</span><span class="sxs-lookup"><span data-stu-id="cedc5-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="cedc5-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cedc5-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="cedc5-212">메트릭 탐색기</span><span class="sxs-lookup"><span data-stu-id="cedc5-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="cedc5-213">필터 및 세그먼트 메트릭</span><span class="sxs-lookup"><span data-stu-id="cedc5-213">Filter and segment metrics</span></span> |![검색 예제](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="cedc5-215">진단 검색</span><span class="sxs-lookup"><span data-stu-id="cedc5-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="cedc5-216">이벤트 찾기 및 검사, 관련 이벤트, 버그 만들기</span><span class="sxs-lookup"><span data-stu-id="cedc5-216">Find and inspect events, related events, and create bugs</span></span> |![검색 예제](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="cedc5-218">분석</span><span class="sxs-lookup"><span data-stu-id="cedc5-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="cedc5-219">강력한 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="cedc5-219">Powerful query language</span></span> |![검색 예제](./media/app-insights-dashboards/63.png) |
