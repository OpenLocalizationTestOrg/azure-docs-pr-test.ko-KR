---
title: "Azure 로그 분석에서 사용자 지정 대시보드 aaaCreate | Microsoft Docs"
description: "이 가이드를 사용 하면 로그 분석 대시보드 시각화 방법을 저장 된 로그 검색이 모두 이해, 제공 단일 렌즈 tooview 환경입니다."
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
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="923ca-103">Log Analytics에서 사용할 사용자 지정 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="923ca-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="923ca-104">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 다음 기존 대시보드를 편집 하거나 새 대시보드를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="923ca-105">이 가이드를 사용 하면 로그 분석 대시보드 시각화 방법을 저장 된 로그 검색이 모두 이해, 제공 단일 렌즈 tooview 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![예제 대시보드](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="923ca-107">Hello OMS 포털에서 만드는 모든 hello 사용자 지정 대시보드 hello OMS 모바일 앱에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="923ca-108">Hello hello 앱에 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="923ca-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="923ca-109">Microsoft 스토어 hello에서 OMS 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="923ca-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="923ca-110">Apple iTunes의 OMS 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="923ca-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![모바일 대시보드](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="923ca-112">내 대시보드를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="923ca-112">How do I create my dashboard?</span></span>
<span data-ttu-id="923ca-113">toobegin, 이동 toohello OMS 개요 페이지</span><span class="sxs-lookup"><span data-stu-id="923ca-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="923ca-114">Hello 표시 **내 대시보드** 타일 hello 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="923ca-115">클릭 toodrill 아래로 대시보드에.</span><span class="sxs-lookup"><span data-stu-id="923ca-115">Click it toodrill down into your dashboard.</span></span>

![개요](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="923ca-117">타일 추가</span><span class="sxs-lookup"><span data-stu-id="923ca-117">Adding a tile</span></span>
<span data-ttu-id="923ca-118">대시보드에서 타일은 저장된 로그 검색을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="923ca-119">OMS에는 여러 저장된 로그 검색이 미리 만들어져 있으므로 바로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="923ca-120">사용 하 여 hello 다음 해당 개요를 어떻게 단계 toobegin 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="923ca-121">Hello 내 대시보드 보기를 클릭 하기만 하면 **사용자 지정** tooenter 사용자 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![그림](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="923ca-123">hello 열리는 패널에는 hello hello 페이지의 오른쪽에 작업 영역의 저장 된 로그 검색이 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="923ca-124">저장 된 로그 검색을 타일로 toovisualize 저장된 된 검색 위에 놓고 클릭 hello **플러스** 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![타일 추가 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="923ca-126">Hello를 클릭할 때 **플러스** 기호, 새 타일 hello 내 대시보드 보기에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![타일 추가 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="923ca-128">타일 편집</span><span class="sxs-lookup"><span data-stu-id="923ca-128">Edit a tile</span></span>
<span data-ttu-id="923ca-129">Hello 내 대시보드 보기를 클릭 하기만 하면 **사용자 지정** tooenter 사용자 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="923ca-130">Tooedit hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="923ca-131">오른쪽 패널 hello tooedit를 변경 하 고 바뀌고 다양 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![타일 편집](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![타일 편집](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="923ca-134">타일 시각화</span><span class="sxs-lookup"><span data-stu-id="923ca-134">Tile visualizations</span></span>
<span data-ttu-id="923ca-135">타일 시각화 toochoose의 세 가지 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="923ca-136">차트 종류</span><span class="sxs-lookup"><span data-stu-id="923ca-136">chart type</span></span> | <span data-ttu-id="923ca-137">수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="923ca-137">what it does</span></span> |
| --- | --- |
| ![가로 막대형 차트](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="923ca-139">로그 검색 결과가 필드에 따라 집계되는지 여부에 따라 저장된 로그 검색 결과의 타임라인이 막대형 그래프 또는 필드별 결과 목록 형태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![메트릭](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="923ca-141">총 로그 검색 결과 적중 횟수를 타일에 숫자로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="923ca-142">메트릭 타일 tooset hello 임계값에 도달할 때 hello 타일 강조 표시 하는 임계값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="923ca-144">저장된 로그 검색 결과 적중의 타임라인이 값과 함께 꺾은선 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="923ca-145">임계값</span><span class="sxs-lookup"><span data-stu-id="923ca-145">Threshold</span></span>
<span data-ttu-id="923ca-146">Hello 메트릭 시각화를 사용 하 여 타일에 임계값을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="923ca-147">Hello 타일에 임계값 toocreate에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="923ca-148">Hello 값이 초과 하거나 선택한 hello 임계값 미만일 경우 toohighlight hello 타일 hello 임계값 아래에 다음 설정 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="923ca-149">Hello 대시보드 구성</span><span class="sxs-lookup"><span data-stu-id="923ca-149">Organizing hello dashboard</span></span>
<span data-ttu-id="923ca-150">tooorganize 대시보드에 toohello 내 대시보드 보기를 탐색 하 고 클릭 **사용자 지정** tooenter 사용자 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="923ca-151">클릭 끌어서 hello 타일 toomove을 원하는 타일 toobe toowhere 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![대시보드 구성](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="923ca-153">타일 제거</span><span class="sxs-lookup"><span data-stu-id="923ca-153">Remove a tile</span></span>
<span data-ttu-id="923ca-154">바둑판식 배열 tooremove toohello 내 대시보드 보기를 탐색 하 고 클릭 **사용자 지정** tooenter 사용자 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="923ca-155">선택 hello 타일 tooremove, 원하는 다음 hello 오른쪽 패널에서 선택 **타일 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![타일 제거](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="923ca-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="923ca-157">Next steps</span></span>
* <span data-ttu-id="923ca-158">만들 [경고](log-analytics-alerts.md) 로그 분석 toogenerate 알림과 tooremediate 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="923ca-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
