---
title: "Azure Application Insights에서 메트릭 aaaExploring | Microsoft Docs"
description: "메트릭 탐색기 차트 toointerpret 방법 등에 toocustomize 메트릭 탐색기 블레이드입니다."
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
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="4293f-103">Application Insights에서 메트릭 탐색</span><span class="sxs-lookup"><span data-stu-id="4293f-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="4293f-104">[Application Insights][start]의 메트릭은 응용 프로그램의 원격 분석에서 전송된 측정된 값 및 이벤트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="4293f-105">성능 문제를 감지하고 응용 프로그램 사용 방식의 추세를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="4293f-106">다양한 표준 메트릭이 있으며 사용자 고유의 사용자 지정 메트릭 및 이벤트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="4293f-107">메트릭 및 이벤트 수는 합계, 평균 또는 개수 등의 집계된 값에 대한 차트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="4293f-108">다음은 차트의 샘플 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="4293f-109">Hello Application Insights 포털에서 메트릭 차트에 모든 위치에서 찾을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="4293f-110">대부분의 경우에서은 사용자 지정할 수 있습니다, 그리고 및 더 많은 차트 toohello 블레이드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="4293f-111">Hello 개요 블레이드에에서 클릭 하 여 toomore 세부 (예: "서버" 제목이 없는 경우)는 차트, 하거나 클릭 **메트릭 탐색기** tooopen는 새 블레이드가 사용자 지정 차트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="4293f-112">시간 범위</span><span class="sxs-lookup"><span data-stu-id="4293f-112">Time range</span></span>
<span data-ttu-id="4293f-113">Hello hello 차트 또는 표에 모든 블레이드를 여는 시간 범위를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Hello Azure 포털에서에서 응용 프로그램의 열린 hello 개요 블레이드](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="4293f-115">일부 데이터가 표시되어야 하지만 아직 표시되지 않은 경우 새로 고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="4293f-116">차트 자체 간격에 따라 새로 고침 하지만 hello 간격을 더 큰 시간 범위에 대해 긴 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="4293f-117">차트에는 hello 분석 파이프라인을 통해 데이터 toocome 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="4293f-118">차트의 일부분으로 toozoom 위로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-118">toozoom into part of a chart, drag over it:</span></span>

![차트의 일부를 끕니다.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="4293f-120">확대/축소 실행 취소 단추 toorestore hello 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="4293f-121">세분성 및 지점 값</span><span class="sxs-lookup"><span data-stu-id="4293f-121">Granularity and point values</span></span>
<span data-ttu-id="4293f-122">마우스를 포인터로 hello 차트 toodisplay hello 값 hello 메트릭의 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![차트 위로 hello 마우스를 가져가고](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="4293f-124">특정 지점에서 hello 메트릭의 hello 값 hello 앞에 샘플링 간격에 걸쳐 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="4293f-125">hello 샘플링 간격 또는 "세분성" hello hello 블레이드 위쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![블레이드의 hello 헤더입니다.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="4293f-127">Hello 시간 범위 블레이드에서 hello 세분성을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-127">You can adjust hello granularity in hello Time range blade:</span></span>

![블레이드의 hello 헤더입니다.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="4293f-129">사용 가능한 hello 세분성 hello 시간 범위 선택에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="4293f-130">안녕하세요 명시적 세분성은 hello 시간 범위에 대 한 대안 toohello "자동" 세분성입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="4293f-131">차트 및 표 편집</span><span class="sxs-lookup"><span data-stu-id="4293f-131">Editing charts and grids</span></span>
<span data-ttu-id="4293f-132">새 차트 toohello 블레이드 tooadd:</span><span class="sxs-lookup"><span data-stu-id="4293f-132">tooadd a new chart toohello blade:</span></span>

![메트릭 탐색기에서 추가 차트 선택](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="4293f-134">선택 **편집** 는 기존 또는 새 차트 tooedit에 어떤 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![하나 이상의 메트릭 선택](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="4293f-136">함께 표시 될 수 있는 hello 조합에 대 한 제한 된 경우에 차트에서 메트릭을 하나 이상 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="4293f-137">메트릭을 하나, 일부 hello 다른 사람이 사용할 수 없습니다 선택.</span><span class="sxs-lookup"><span data-stu-id="4293f-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="4293f-138">코딩 하는 경우 [사용자 지정 메트릭] [ track] (호출 tooTrackMetric 및 TrackEvent) 앱에은 여기에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="4293f-139">데이터 분할</span><span class="sxs-lookup"><span data-stu-id="4293f-139">Segment your data</span></span>
<span data-ttu-id="4293f-140">메트릭 속성-서로 다른 운영 체제 클라이언트에서 페이지 보기 예를 들어 toocompare로 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="4293f-141">차트 또는 그리드 선택 하 고 그룹화에 전환 하 여 속성 toogroup 선택:</span><span class="sxs-lookup"><span data-stu-id="4293f-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![그룹화를 선택한 다음 그룹별에서 속성 선택](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="4293f-143">그룹화를 사용 하는 경우 hello 영역 및 가로 막대형 차트 종류는 누적된 디스플레이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="4293f-144">적합 한 hello 집계 메서드는 Sum입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="4293f-145">하지만 hello 집계 형식은 평균이 두 hello 선 또는 눈금 표시 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="4293f-146">코딩 하는 경우 [사용자 지정 메트릭] [ track] 앱에 속성 값을 포함 하 고, hello 목록에서 수 tooselect hello 속성 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="4293f-147">Hello 차트 너무 작으면 분할 된 데이터에 대 한?</span><span class="sxs-lookup"><span data-stu-id="4293f-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="4293f-148">높이 조정:</span><span class="sxs-lookup"><span data-stu-id="4293f-148">Adjust its height:</span></span>

![Hello 슬라이더를 조정 합니다.](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="4293f-150">집계 형식</span><span class="sxs-lookup"><span data-stu-id="4293f-150">Aggregation types</span></span>
<span data-ttu-id="4293f-151">일반적으로 기본적으로 hello 측면에 대 한 hello 범례를 차트 hello hello 일정 기간 동안 집계 hello 값을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="4293f-152">Hello 차트를 마우스로 가리키면 경우 hello 값 해당 시점에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="4293f-153">Hello 차트에서 각 데이터 요소에는 hello 샘플링 간격 또는 "세분성" 앞에 수신 hello 데이터 값에 대 한 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="4293f-154">hello 세분성 hello hello 블레이드 위쪽에 표시 되 고 hello 따라 달라 지 며 hello 차트의 전체 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="4293f-155">메트릭은 다른 방법으로 집계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="4293f-156">**Count** 는 hello 샘플링 간격에서 받은 hello 이벤트의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="4293f-157">요청과 같은 이벤트에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-157">It is used for events such as requests.</span></span> <span data-ttu-id="4293f-158">Hello 높이 hello 차트의 변형 hello 이벤트가 발생 하는 hello 속도 변형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="4293f-159">하지만 hello 샘플링 간격을 변경 하면 hello 숫자 값이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="4293f-160">**Sum** hello 샘플링 간격 또는 hello 차트의 hello 기간을 통해 받은 모든 hello 데이터 요소의 hello 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="4293f-161">**평균** 나눕니다 hello 간격을 통해 받은 데이터 요소의 hello 번호로 Sum hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="4293f-162">**고유** 개수는 사용자 및 계정의 수를 세는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="4293f-163">Hello 샘플링 간격에 대해 또는 hello 차트 hello 기간에 걸쳐 hello 그림 해당 시간에 다른 사용자의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="4293f-164">**%** - 각 집계의 백분율 버전은 세그먼트 차트에서만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="4293f-165">총 hello 항상 too100 %를 추가 하 고 hello 차트 hello 상대적 기여도 전체의 다른 구성 요소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![백분율 집계](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="4293f-167">Hello 집계 유형 변경</span><span class="sxs-lookup"><span data-stu-id="4293f-167">Change hello aggregation type</span></span>

![Hello 차트를 편집 하 고 집계를 선택](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="4293f-169">hello 기본 방법은 각 메트릭에 대 한 모든 메트릭을 선택 하지 않은 경우 또는 새 차트를 만들 때 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![모든 메트릭 toosee hello 기본값을 선택 취소](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="4293f-171">Y축 고정</span><span class="sxs-lookup"><span data-stu-id="4293f-171">Pin Y-axis</span></span> 
<span data-ttu-id="4293f-172">기본적으로 차트는 hello 데이터 범위에서 toogive 양자 hello 값의 시각적 표현 되는 최대값까지 0부터 시작 하는 Y 축 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="4293f-173">하지만 일부 경우에 둘 이상의 값에 약간의 변경이 검사 하는 hello 퀀텀 흥미로운 toovisually 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="4293f-174">같은 사용자 지정 항목에 대해이 사용 하이 여 hello y 축 범위 편집 기능 toopin hello y 축 최소값 또는 최대값 값 원하는 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="4293f-175">Y 축 범위가 설정 "고급 설정" 확인란 toobring hello 클릭</span><span class="sxs-lookup"><span data-stu-id="4293f-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![고급 설정을 클릭하고, 사용자 지정 범위를 선택한 후 최소값 및 최대값 지정](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="4293f-177">데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="4293f-177">Filter your data</span></span>
<span data-ttu-id="4293f-178">속성 값의 선택된 된 집합에 대 한 정당한 hello 메트릭을 toosee:</span><span class="sxs-lookup"><span data-stu-id="4293f-178">toosee just hello metrics for a selected set of property values:</span></span>

![필터를 클릭하고 속성을 확장하여 값 선택](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="4293f-180">특정 속성에 대 한 모든 값을 선택 하지 않은 동일한 모두를 선택 하 여 hello에: 필터는 해당 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="4293f-181">각 속성 값과 함께 이벤트 알림 hello를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="4293f-182">한 속성의 값을 선택 하면 다른 속성 값이 조정 됩니다 함께 hello를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="4293f-183">필터 블레이드 tooall hello 차트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="4293f-184">다른 필터를 적용 하려는 경우 toodifferent 차트를 만들고 다른 메트릭 블레이드를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="4293f-185">나란히 볼 수 있도록 차트 다른 블레이드 toohello 대시보드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="4293f-186">봇 및 웹 테스트 트래픽 제거</span><span class="sxs-lookup"><span data-stu-id="4293f-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="4293f-187">사용 하 여 hello 필터 **실제 또는 가상 트래픽** 확인 **실제**합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="4293f-188">**가상 트래픽 소스**로 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="4293f-189">tooadd 속성 toohello 필터 목록</span><span class="sxs-lookup"><span data-stu-id="4293f-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="4293f-190">자신이 선택한 범주에 대 한 toofilter 원격 분석 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="4293f-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="4293f-191">예를 들어 사용자를 서로 다른 범주로 나누고 데이터를 이러한 범주로 분할하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="4293f-192">[사용자 고유의 속성을 만듭니다](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="4293f-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="4293f-193">설정 된 [원격 분석 이니셜라이저](app-insights-api-custom-events-metrics.md#defaults) toohave SDK의 서로 다른 모듈에서 보낸 hello 표준 원격 분석을 포함 하 여 모든 원격 분석-에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="4293f-194">Hello 차트 종류를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-194">Edit hello chart type</span></span>
<span data-ttu-id="4293f-195">표와 그래프 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-195">Notice that you can switch between grids and graphs:</span></span>

![표 또는 그래프를 선택한 다음 차트 종류 선택](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="4293f-197">매트릭 블레이드 저장</span><span class="sxs-lookup"><span data-stu-id="4293f-197">Save your metrics blade</span></span>
<span data-ttu-id="4293f-198">차트를 만든 경우 즐겨찾기로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="4293f-199">여부 tooshare 사용 하 여 다른 팀 멤버, 조직 계정을 사용 하는 경우 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![즐겨찾기 선택](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="4293f-201">toosee hello 블레이드를 다시 **이동 toohello 개요 블레이드에** 즐겨찾기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![Hello 개요 블레이드에에서 즐겨찾기를 선택 합니다.](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="4293f-203">저장을 상대 시간 범위를 선택한 경우 hello 블레이드 hello 최신 메트릭을 사용 하 여 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="4293f-204">절대 시간 범위를 선택한 경우에 표시 됩니다 될 때마다 동일한 데이터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="4293f-205">Hello 블레이드를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="4293f-205">Reset hello blade</span></span>
<span data-ttu-id="4293f-206">블레이드를 편집 하는 경우 다음 원하는 tooget 백 toohello 원래 저장 집합 방금 재설정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![메트릭 탐색기의 hello 위쪽 hello 단추](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="4293f-208">라이브 메트릭 스트림</span><span class="sxs-lookup"><span data-stu-id="4293f-208">Live metrics stream</span></span>

<span data-ttu-id="4293f-209">원격 분석을 더 빠르게 즉시 보려면 [라이브 스트림](app-insights-live-stream.md)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="4293f-210">대부분 메트릭 집계 hello 프로세스로 인해 몇 분 tooappear를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="4293f-211">반면 라이브 메트릭은 짧은 대기 시간에 최적화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="4293f-212">경고 설정</span><span class="sxs-lookup"><span data-stu-id="4293f-212">Set alerts</span></span>
<span data-ttu-id="4293f-213">경고를 추가 하는 toobe 비정상적인 값이 모든 메트릭의 전자 메일 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="4293f-214">Toosend hello 전자 메일 toohello 계정 관리자 또는 toospecific 전자 메일 주소를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![메트릭 탐색기에서 경고 규칙, 경고 추가 선택](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="4293f-216">[경고에 대해 알아봅니다][alerts].</span><span class="sxs-lookup"><span data-stu-id="4293f-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="4293f-217">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="4293f-217">Continuous Export</span></span>
<span data-ttu-id="4293f-218">데이터를 외부에서 처리할 수 있도록 지속적으로 내보내려면 [연속 내보내기](app-insights-export-telemetry.md)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="4293f-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="4293f-219">Power BI</span></span>
<span data-ttu-id="4293f-220">데이터도 다양 한 뷰를 사용 하도록 하려는 경우 다음을 할 수 있습니다 [tooPower BI 내보내기](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="4293f-221">분석</span><span class="sxs-lookup"><span data-stu-id="4293f-221">Analytics</span></span>
<span data-ttu-id="4293f-222">[분석](app-insights-analytics.md) 더 다양 한 방식으로 tooanalyze 강력한 쿼리 언어를 사용 하 여 원격 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="4293f-223">Toocombine 또는 메트릭에서 결과 계산 하거나 응용 프로그램의 최근 성능 심층 탐구 수행 하는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="4293f-224">메트릭 차트에서 hello 분석 아이콘 tooget 클릭할 수 있는 직접 toohello 동등한 분석 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4293f-225">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4293f-225">Troubleshooting</span></span>
<span data-ttu-id="4293f-226">*차트에 데이터가 표시되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="4293f-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="4293f-227">필터는 hello 블레이드에서 tooall hello 차트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="4293f-228">는 하나의 차트에 중점 동안 하지 않은 설정 하는 다른 모든 hello 데이터를 제외 하는 필터 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="4293f-229">다른 차트에 서로 다른 필터가 tooset 원한다 면에서 만들 저장 다른 블레이드를 별도 즐겨찾기.</span><span class="sxs-lookup"><span data-stu-id="4293f-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="4293f-230">나란히 볼 수 있도록 해당를 toohello 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="4293f-231">차트 메트릭을 hello에 정의 되어 있지 않은 속성에 의해 그룹화 할 경우 다음 됩니다 아무 hello 차트에서.</span><span class="sxs-lookup"><span data-stu-id="4293f-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="4293f-232">'그룹화 기준'을 지우거나 다른 그룹화 속성을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="4293f-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="4293f-233">성능 데이터(CPU, IO 속도 등)는 Java 웹 서비스, Windows 데스크톱 앱, [IIS Web Apps 및 서비스(상태 모니터를 설치한 경우)](app-insights-monitor-performance-live-website-now.md) 및 [Azure Cloud Services](app-insights-azure.md)에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="4293f-234">Azure 웹 사이트에는 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4293f-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="4293f-235">비디오</span><span class="sxs-lookup"><span data-stu-id="4293f-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="4293f-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4293f-236">Next steps</span></span>
* [<span data-ttu-id="4293f-237">Application Insights를 사용하여 사용량 모니터링</span><span class="sxs-lookup"><span data-stu-id="4293f-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="4293f-238">진단 검색 사용</span><span class="sxs-lookup"><span data-stu-id="4293f-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
