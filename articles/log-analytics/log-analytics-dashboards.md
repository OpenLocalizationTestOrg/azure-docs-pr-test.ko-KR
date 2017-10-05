---
title: "Azure Log Analytics에서 사용자 지정 대시보드 만들기 | Microsoft Docs"
description: "이 가이드는 Log Analytics 대시보드가 저장된 모든 로그 검색을 시각화하여 환경을 보는 단일 렌즈를 제공하는 방법을 이해하는 데 도움이 됩니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a90d9c620221bffbb225fb060b997af2f5e90390
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="93b27-103">Log Analytics에서 사용할 사용자 지정 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="93b27-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="93b27-104">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우, 새 대시보드를 만들거나 기존 대시보드를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-104">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="93b27-105">이 가이드는 Log Analytics 대시보드가 저장된 모든 로그 검색을 시각화하여 환경을 보는 단일 렌즈를 제공하는 방법을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![예제 대시보드](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="93b27-107">OMS 포털에서 만든 모든 사용자 지정 대시보드는 OMS 모바일 앱에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-107">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="93b27-108">앱에 대한 자세한 내용은 다음 페이지를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="93b27-108">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="93b27-109">Microsoft 스토어의 OMS 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="93b27-109">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="93b27-110">Apple iTunes의 OMS 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="93b27-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![모바일 대시보드](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="93b27-112">내 대시보드를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="93b27-112">How do I create my dashboard?</span></span>
<span data-ttu-id="93b27-113">시작하려면 OMS 개요 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-113">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="93b27-114">왼쪽에 **내 대시보드** 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-114">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="93b27-115">타일을 클릭하여 대시보드로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-115">Click it to drill down into your dashboard.</span></span>

![개요](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="93b27-117">타일 추가</span><span class="sxs-lookup"><span data-stu-id="93b27-117">Adding a tile</span></span>
<span data-ttu-id="93b27-118">대시보드에서 타일은 저장된 로그 검색을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="93b27-119">OMS에는 여러 저장된 로그 검색이 미리 만들어져 있으므로 바로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="93b27-120">시작 방법에 대해 개괄적으로 설명하는 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-120">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="93b27-121">내 대시보드 보기에서 **사용자 지정**을 클릭하기만 하면 사용자 지정 모드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-121">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![그림](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="93b27-123">페이지 오른쪽에 열리는 패널에는 작업 영역의 저장된 로그 검색이 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-123">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="93b27-124">저장된 로그 검색을 타일로 시각화하려면 저장된 검색 위에 마우스를 가져간 다음 **더하기** 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-124">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![타일 추가 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="93b27-126">**더하기** 기호를 클릭하면 내 대시보드 보기에 새 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-126">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![타일 추가 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="93b27-128">타일 편집</span><span class="sxs-lookup"><span data-stu-id="93b27-128">Edit a tile</span></span>
<span data-ttu-id="93b27-129">내 대시보드 보기에서 **사용자 지정**을 클릭하기만 하면 사용자 지정 모드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-129">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="93b27-130">편집하려는 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-130">Click the tile you want to edit.</span></span> <span data-ttu-id="93b27-131">오른쪽 패널이 편집할 수 있도록 바뀌고 다양한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-131">The right panel changes to edit, and gives a selection of options:</span></span>

![타일 편집](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![타일 편집](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="93b27-134">타일 시각화</span><span class="sxs-lookup"><span data-stu-id="93b27-134">Tile visualizations</span></span>
<span data-ttu-id="93b27-135">다음 세 종류의 타일 시각화 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-135">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="93b27-136">차트 종류</span><span class="sxs-lookup"><span data-stu-id="93b27-136">chart type</span></span> | <span data-ttu-id="93b27-137">수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="93b27-137">what it does</span></span> |
| --- | --- |
| ![가로 막대형 차트](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="93b27-139">로그 검색 결과가 필드에 따라 집계되는지 여부에 따라 저장된 로그 검색 결과의 타임라인이 막대형 그래프 또는 필드별 결과 목록 형태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![메트릭](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="93b27-141">총 로그 검색 결과 적중 횟수를 타일에 숫자로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="93b27-142">메트릭 타일을 사용하면 임계값에 도달할 때 타일이 강조 표시되도록 임계값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-142">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="93b27-144">저장된 로그 검색 결과 적중의 타임라인이 값과 함께 꺾은선 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="93b27-145">임계값</span><span class="sxs-lookup"><span data-stu-id="93b27-145">Threshold</span></span>
<span data-ttu-id="93b27-146">메트릭 시각화를 사용하여 타일에 임계값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-146">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="93b27-147">타일에 임계값을 만들려면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-147">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="93b27-148">값이 선택된 임계값을 초과하거나 미만일 때 타일을 강조 표시할지 여부를 선택하고 아래에서 임계값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-148">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="93b27-149">대시보드 구성</span><span class="sxs-lookup"><span data-stu-id="93b27-149">Organizing the dashboard</span></span>
<span data-ttu-id="93b27-150">대시보드를 구성하려면 내 대시보드 보기로 이동한 다음 **사용자 지정**을 클릭하여 사용자 지정 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-150">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="93b27-151">이동할 타일을 클릭하고 끌어서 원하는 위치로 타일을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-151">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![대시보드 구성](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="93b27-153">타일 제거</span><span class="sxs-lookup"><span data-stu-id="93b27-153">Remove a tile</span></span>
<span data-ttu-id="93b27-154">타일을 제거하려면 내 대시보드 보기로 이동한 다음 **사용자 지정**을 클릭하여 사용자 지정 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-154">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="93b27-155">제거할 타일을 선택한 다음 오른쪽 패널에서 **타일 제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-155">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![타일 제거](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="93b27-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93b27-157">Next steps</span></span>
* <span data-ttu-id="93b27-158">알림을 생성하고 문제를 해결하기 위해 Log Analytics에서 [경고](log-analytics-alerts.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93b27-158">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
