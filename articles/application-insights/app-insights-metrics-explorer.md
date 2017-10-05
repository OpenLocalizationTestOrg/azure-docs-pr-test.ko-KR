---
title: "Azure Application Insights에서 메트릭 탐색 | Microsoft Docs"
description: "메트릭 탐색기에 차트를 해석하는 방법 및 메트릭 탐색기 블레이드를 사용자 지정하는 방법입니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="e99ee-103">Application Insights에서 메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="e99ee-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="e99ee-104">[Application Insights][start]의 메트릭은 응용 프로그램의 원격 분석에서 전송된 측정된 값 및 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="e99ee-105">성능 문제를 감지하고 응용 프로그램 사용 방식의 추세를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="e99ee-106">다양한 표준 메트릭이 있으며 사용자 고유의 사용자 지정 메트릭 및 이벤트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="e99ee-107">메트릭 및 이벤트 수는 합계, 평균 또는 개수 등의 집계된 값에 대한 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="e99ee-108">다음은 차트의 샘플 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="e99ee-109">Application Insights 포털 어디에나 메트릭 차트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="e99ee-110">대부분의 경우 사용자 지정할 수 있으며 블레이드에 차트를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="e99ee-111">개요 블레이드에서 더 자세한 차트("Servers"와 같은 타일이 있음)를 클릭하거나 **메트릭 탐색기**를 클릭하여 사용자 지정 차트를 만들 수 있는 새 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="e99ee-112">시간 범위</span><span class="sxs-lookup"><span data-stu-id="e99ee-112">Time range</span></span>
<span data-ttu-id="e99ee-113">모든 블레이드의 차트 또는 표에서 다루는 시간 범위를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Azure 포털에서 응용 프로그램의 개요 블레이드 열기](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="e99ee-115">일부 데이터가 표시되어야 하지만 아직 표시되지 않은 경우 새로 고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="e99ee-116">차트는 특정 간격에 따라 자체적으로 새로 고쳐지지만 시간 범위가 더 클 경우 간격이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="e99ee-117">차트에 분석 파이프라인을 내놓기 위한 데이터에는 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="e99ee-118">차트의 일부를 확대하려면 해당 부분을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-118">To zoom into part of a chart, drag over it:</span></span>

![차트의 일부를 끕니다.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="e99ee-120">복원하려면 확대/축소 취소 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="e99ee-121">세분성 및 지점 값</span><span class="sxs-lookup"><span data-stu-id="e99ee-121">Granularity and point values</span></span>
<span data-ttu-id="e99ee-122">해당 지점에서 메트릭 값을 표시하려면 차트 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![차트 위로 마우스 이동](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="e99ee-124">특정 지점에서 메트릭 값은 이전 샘플링 간격에 걸쳐 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="e99ee-125">샘플링 간격 또는 "세분성"는 블레이드 위쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![블레이드의 헤더입니다.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="e99ee-127">시간 범위 블레이드에서 세분성을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-127">You can adjust the granularity in the Time range blade:</span></span>

![블레이드의 헤더입니다.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="e99ee-129">세분성은 선택한 시간 범위에 따라 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="e99ee-130">명시적 세분성은 시간 범위에 대한 "자동" 세분성의 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="e99ee-131">차트 및 표 편집</span><span class="sxs-lookup"><span data-stu-id="e99ee-131">Editing charts and grids</span></span>
<span data-ttu-id="e99ee-132">블레이드에 새 차트를 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="e99ee-132">To add a new chart to the blade:</span></span>

![메트릭 탐색기에서 추가 차트 선택](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="e99ee-134">기존 또는 새 차트에서 **편집**을 선택하여 표시되는 항목을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![하나 이상의 메트릭 선택](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="e99ee-136">함께 표시할 수 있는 조합에 관한 제한이 있지만 차트에 하나 이상의 메트릭을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="e99ee-137">한 메트릭을 선택하면 일부 다른 메트릭을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="e99ee-138">[사용자 지정 메트릭][track]을 앱으로 코딩한 경우(TrackMetric 및 TrackEvent 호출) 여기에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="e99ee-139">데이터 분할</span><span class="sxs-lookup"><span data-stu-id="e99ee-139">Segment your data</span></span>
<span data-ttu-id="e99ee-140">메트릭을 속성별로 분할할 수 있습니다. 예를 들어 서로 다른 운영 체제를 사용하는 클라이언트에서 페이지 보기를 비교하려는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="e99ee-141">차트 또는 표를 선택하고 그룹으로 전환하여 그룹별로 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![그룹화를 선택한 다음 그룹별에서 속성 선택](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="e99ee-143">그룹화를 사용하면 영역형 차트 및 가로 막대형 차트 유형이 누적형 디스플레이를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="e99ee-144">이것은 집계 방법이 합계일 때 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="e99ee-145">하지만 집계 유형이 평균이면 꺾은선형 또는 표 표시 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="e99ee-146">[사용자 지정 메트릭][track]을 앱으로 코딩하고 속성 값을 포함하는 경우 목록에서 속성을 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="e99ee-147">데이터를 분할하기에 차트가 너무 작나요?</span><span class="sxs-lookup"><span data-stu-id="e99ee-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="e99ee-148">높이 조정:</span><span class="sxs-lookup"><span data-stu-id="e99ee-148">Adjust its height:</span></span>

![슬라이더 조정](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="e99ee-150">집계 형식</span><span class="sxs-lookup"><span data-stu-id="e99ee-150">Aggregation types</span></span>
<span data-ttu-id="e99ee-151">기본적으로 옆쪽의 범례는 차트의 기간에 걸쳐 집계된 값을 일반적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="e99ee-152">차트 위로 마우스를 가져가면 해당 지점의 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="e99ee-153">차트에서 각 데이터 요소는 이전 샘플링 간격 또는 "세분성"으로 받은 데이터 값의 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="e99ee-154">세분성은 블레이드 위쪽에 표시되며 차트의 전체적인 시간 간격에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="e99ee-155">메트릭은 다른 방법으로 집계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="e99ee-156">**개수**는 샘플링 간격에서 받은 이벤트 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="e99ee-157">요청과 같은 이벤트에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-157">It is used for events such as requests.</span></span> <span data-ttu-id="e99ee-158">차트 높이의 편차는 이벤트가 발생하는 비율의 변동을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="e99ee-159">그러나 샘플링 간격을 변경하면 숫자 값이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="e99ee-160">**합계** 는 샘플링 간격 또는 차트의 기간 동안 받은 모든 데이터 요소의 값을 더합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="e99ee-161">**평균** 은 합계를 간격을 통해 받은 데이터 요소 수로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="e99ee-162">**고유** 개수는 사용자 및 계정의 수를 세는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="e99ee-163">그림에서는 샘플링 간격 또는 차트의 기간 동안 해당 시간에 표시된 서로 다른 사용자의 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="e99ee-164">**%** - 각 집계의 백분율 버전은 세그먼트 차트에서만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="e99ee-165">합계는 항상 최대 100%이며, 차트에는 합계의 여러 구성 요소의 상대적 기여도가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![백분율 집계](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="e99ee-167">집계 형식 변경</span><span class="sxs-lookup"><span data-stu-id="e99ee-167">Change the aggregation type</span></span>

![차트를 편집한 다음 집계를 선택합니다.](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="e99ee-169">각 메트릭에 대한 기본 방법은 새 차트를 만들거나 모든 메트릭을 선택 취소할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![모든 메트릭의 선택을 취소하여 기본값 표시](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="e99ee-171">Y축 고정</span><span class="sxs-lookup"><span data-stu-id="e99ee-171">Pin Y-axis</span></span> 
<span data-ttu-id="e99ee-172">기본적으로 차트는 값 퀀텀을 시각적으로 나타내기 위해 0부터 시작해서 데이터 범위의 최대값까지 Y축 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="e99ee-173">그렇지만 경우에 따라 값의 경미한 변화를 시각적으로 확인하기 위해 컨텀 이상에 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="e99ee-174">이와 같은 사용자 지정을 위해서는 Y축 범위 편집 기능을 사용하여 Y축 최소값 또는 최대값을 원하는 위치에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="e99ee-175">"고급 설정" 확인란을 클릭하여 Y축 범위 설정 표시</span><span class="sxs-lookup"><span data-stu-id="e99ee-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![고급 설정을 클릭하고, 사용자 지정 범위를 선택한 후 최소값 및 최대값 지정](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="e99ee-177">데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="e99ee-177">Filter your data</span></span>
<span data-ttu-id="e99ee-178">속성 값의 선택한 집합에 대한 메트릭 보기:</span><span class="sxs-lookup"><span data-stu-id="e99ee-178">To see just the metrics for a selected set of property values:</span></span>

![필터를 클릭하고 속성을 확장하여 값 선택](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="e99ee-180">특정 속성에 대한 값을 선택하지 않은 경우 모두 선택한 것과 동일합니다. 즉, 해당 속성에는 필터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="e99ee-181">각 속성 값과 함께 이벤트 수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="e99ee-182">한 속성 값을 선택하면 다른 속성 값과 함께 수가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="e99ee-183">필터는 블레이드의 모든 차트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="e99ee-184">여러 차트에 서로 다른 필터를 적용하려면 다른 메트릭 블레이드를 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="e99ee-185">필요한 경우 다른 블레이드의 차트를 대시보드에 고정하여 서로 나란히 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="e99ee-186">봇 및 웹 테스트 트래픽 제거</span><span class="sxs-lookup"><span data-stu-id="e99ee-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="e99ee-187">**실제 또는 가상 트래픽** 필터를 사용하여 **실제**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="e99ee-188">**가상 트래픽 소스**로 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="e99ee-189">필터 목록에 속성을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="e99ee-189">To add properties to the filter list</span></span>
<span data-ttu-id="e99ee-190">직접 선택한 범주에서 원격 분석을 필터링하려고 하시나요?</span><span class="sxs-lookup"><span data-stu-id="e99ee-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="e99ee-191">예를 들어 사용자를 서로 다른 범주로 나누고 데이터를 이러한 범주로 분할하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="e99ee-192">[사용자 고유의 속성을 만듭니다](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="e99ee-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="e99ee-193">[원격 분석 이니셜라이저](app-insights-api-custom-events-metrics.md#defaults) 에서 이를 설정하여 다른 SDK 모듈에서 보낸 표준 원격 분석을 포함하여 모든 원격 분석에 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="e99ee-194">차트 종류 편집</span><span class="sxs-lookup"><span data-stu-id="e99ee-194">Edit the chart type</span></span>
<span data-ttu-id="e99ee-195">표와 그래프 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-195">Notice that you can switch between grids and graphs:</span></span>

![표 또는 그래프를 선택한 다음 차트 종류 선택](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="e99ee-197">매트릭 블레이드 저장</span><span class="sxs-lookup"><span data-stu-id="e99ee-197">Save your metrics blade</span></span>
<span data-ttu-id="e99ee-198">차트를 만든 경우 즐겨찾기로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="e99ee-199">조직 계정을 사용하는 경우 다른 팀 구성원과 이를 공유할지 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![즐겨찾기 선택](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="e99ee-201">블레이드를 다시 보려면 **개요 블레이드로 이동** 하여 즐겨찾기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![개요 블레이드에서 즐겨찾기 선택](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="e99ee-203">저장했을 때 상대 시간을 선택한 경우 해당 블레이드가 최신 메트릭으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="e99ee-204">절대 시간 범위를 선택한 경우 매번 동일한 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="e99ee-205">블레이드 다시 설정</span><span class="sxs-lookup"><span data-stu-id="e99ee-205">Reset the blade</span></span>
<span data-ttu-id="e99ee-206">블레이드를 편집하지만 저장된 원본 세트로 되돌아가려는 경우 재설정을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![메트릭 탐색기 위쪽에 있는 단추](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="e99ee-208">라이브 메트릭 스트림</span><span class="sxs-lookup"><span data-stu-id="e99ee-208">Live metrics stream</span></span>

<span data-ttu-id="e99ee-209">원격 분석을 더 빠르게 즉시 보려면 [라이브 스트림](app-insights-live-stream.md)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="e99ee-210">대부분의 메트릭은 집계 프로세스 때문에 몇 분 정도 지나야 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="e99ee-211">반면 라이브 메트릭은 짧은 대기 시간에 최적화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="e99ee-212">경고 설정</span><span class="sxs-lookup"><span data-stu-id="e99ee-212">Set alerts</span></span>
<span data-ttu-id="e99ee-213">메트릭의 비정상적인 값에 대한 알림을 메일로 받으려면 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="e99ee-214">계정 관리자나 특정 메일 주소로 메일을 보내도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![메트릭 탐색기에서 경고 규칙, 경고 추가 선택](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="e99ee-216">[경고에 대해 알아봅니다][alerts].</span><span class="sxs-lookup"><span data-stu-id="e99ee-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="e99ee-217">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="e99ee-217">Continuous Export</span></span>
<span data-ttu-id="e99ee-218">데이터를 외부에서 처리할 수 있도록 지속적으로 내보내려면 [연속 내보내기](app-insights-export-telemetry.md)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="e99ee-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="e99ee-219">Power BI</span></span>
<span data-ttu-id="e99ee-220">보다 풍부한 데이터 보기를 사용하려는 경우 [Power BI를 내보낼](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="e99ee-221">분석</span><span class="sxs-lookup"><span data-stu-id="e99ee-221">Analytics</span></span>
<span data-ttu-id="e99ee-222">[분석](app-insights-analytics.md) 은 강력한 쿼리 언어를 사용하여 원격 분석을 분석하는 더욱 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="e99ee-223">메트릭의 결과를 결합하거나 계산하려는 경우 또는 앱의 최근 성능을 면밀히 조사하려는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="e99ee-224">메트릭 차트에서 분석 아이콘을 클릭하여 해당하는 분석 쿼리를 직접 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e99ee-225">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e99ee-225">Troubleshooting</span></span>
<span data-ttu-id="e99ee-226">*차트에 데이터가 표시되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="e99ee-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="e99ee-227">필터는 블레이드의 모든 차트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="e99ee-228">하나의 필터에 포커스를 둔 동안 다른 차트에서 모든 데이터를 제외하는 필터를 설정하지 않았는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e99ee-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="e99ee-229">여러 차트에서 서로 다른 필터를 설정하려면 해당 차트를 서로 다른 블레이드를 만들어 별도의 즐겨찾기로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="e99ee-230">필요한 경우 대시보드에 고정하여 서로 나란히 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="e99ee-231">메트릭에 정의되지 않은 속성으로 차트를 그룹화한 경우 차트에 아무 것도 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="e99ee-232">'그룹화 기준'을 지우거나 다른 그룹화 속성을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="e99ee-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="e99ee-233">성능 데이터(CPU, IO 속도 등)는 Java 웹 서비스, Windows 데스크톱 앱, [IIS Web Apps 및 서비스(상태 모니터를 설치한 경우)](app-insights-monitor-performance-live-website-now.md) 및 [Azure Cloud Services](app-insights-azure.md)에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="e99ee-234">Azure 웹 사이트에는 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e99ee-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="e99ee-235">비디오</span><span class="sxs-lookup"><span data-stu-id="e99ee-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="e99ee-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e99ee-236">Next steps</span></span>
* [<span data-ttu-id="e99ee-237">Application Insights를 사용하여 사용량 모니터링</span><span class="sxs-lookup"><span data-stu-id="e99ee-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="e99ee-238">진단 검색 사용</span><span class="sxs-lookup"><span data-stu-id="e99ee-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
