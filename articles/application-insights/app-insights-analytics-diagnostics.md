---
title: "Azure Application Insights에서 웹앱 성능 변화의 스마트 진단 | Microsoft Docs"
description: "웹앱의 성능 원격 분석에서 스파이크 또는 단계의 자동 진단입니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="be475-103">앱 원격 분석에서 급격한 변화 진단</span><span class="sxs-lookup"><span data-stu-id="be475-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="be475-104">*이 기능은 미리 보기 상태입니다.*</span><span class="sxs-lookup"><span data-stu-id="be475-104">*This feature is in preview.*</span></span>

<span data-ttu-id="be475-105">단 한 번의 클릭으로 웹앱의 성능 또는 사용 현황의 급격한 변화를 진단해 보세요.</span><span class="sxs-lookup"><span data-stu-id="be475-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="be475-106">스마트 진단 기능은 [Application Insights](app-insights-overview.md)의 [분석](app-insights-analytics.md)에서 시간 차트를 만들 때마다 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="be475-107">급증이나 급강하 같이 결과의 추세에 비정상적인 변화가 있는 경우 스마트 진단은 변화를 설명할 수 있는 차원 및 관련 값의 패턴을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="be475-108">이 기능을 사용하면 문제를 신속하게 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="be475-109">다음 예제에서 스마트 진단은 변화와 관련된 속성 값의 패턴을 식별하고 해당 패턴이 있는 경우와 없는 경우 결과의 차이를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![예제 분석 진단 결과](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="be475-111">데이터 변경 진단</span><span class="sxs-lookup"><span data-stu-id="be475-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="be475-112">분석에서 쿼리를 실행하고 시간 차트로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="be475-113">강조 표시된 최대 사용 지점이 있는 경우 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![최대 사용 지점](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="be475-115">진단에서 패턴을 검색하려면 몇 초 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="be475-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="be475-116">진단 결과 탭에는 데이터 불연속성을 설명하는 패턴이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be475-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="be475-118">텍스트에는 변화와 연관이 있을 것 같은 차원 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be475-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="be475-119">이 예제에서는 특정 요청 및 특정 브라우저 버전과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="be475-120">차트의 두 가지 구성 요소인 true 및 false 필터로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="be475-121">false 구성 요소는 변경되지 않은 추세를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be475-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="be475-122">즉, 진단에서 식별한 문제가 있는 차원 조합을 제외하면 원격 분석 결과에 변화가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="be475-123">반면, 해당 조합 내의 결과는 강조 표시된 조사 영역 내의 큰 변화를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be475-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="be475-124">진단에서 변화를 설명하는 속성 조합을 발견했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be475-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="be475-125">패턴이 복잡할 경우 차원을 표시하려면 **모두 표시** 위로 마우스를 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![모두 표시](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="be475-127">진단에서 알림을 제공한 중요한 패턴을 찾지 못한 경우 '결과 없음' 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="be475-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="be475-128">이 시점에서 쿼리를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-128">At this point, you may change your query.</span></span> <span data-ttu-id="be475-129">예를 들어 분석 쿼리에서 시간 범위 및 범주화를 좁혀 추가 분석을 수행하고 더 나은 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="be475-130">특정 브라우저에서 웹 사이트의 특정 페이지에 문제가 있다는 사실을 알았으므로 이제 문제 페이지로 바로 이동하여 최근 변경 내용을 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="be475-131">데모 사용해 보기</span><span class="sxs-lookup"><span data-stu-id="be475-131">Try the demo</span></span>

<span data-ttu-id="be475-132">샘플 데이터에 대한 [데모를 보려면 여기를 클릭](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H)하세요.</span><span class="sxs-lookup"><span data-stu-id="be475-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="be475-133">작동 방법</span><span class="sxs-lookup"><span data-stu-id="be475-133">How it works</span></span>

<span data-ttu-id="be475-134">스마트 진단은 [DiffPatterns](app-insights-analytics-reference.md) 작업을 기반으로 한 자율적인 고급 기계 학습 알고리즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="be475-135">이 진단에서는 데이터 변경을 설명할 수 있는 후보 패턴을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="be475-136">메트릭에 대한 각 후보의 영향을 분석하고 변경과 가장 관련이 있는 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be475-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="be475-137">진단 지점은 없나요?</span><span class="sxs-lookup"><span data-stu-id="be475-137">No diagnostic points?</span></span>

<span data-ttu-id="be475-138">스마트 진단은 다음 조건이 충족되는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="be475-139">스마트 진단 설정이 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="be475-140">분석에서 설정 아이콘 아래에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="be475-141">[분석] 설정의 [스마트 진단] 옵션이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="be475-142">시간 축: 차트의 X축은 `datetime` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="be475-143">꺾은선형 또는 영역 차트: 진단은 이러한 종류의 차트에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="be475-144">쿼리의 끝에서 `| render timechart` 또는 `| render areachart`를 사용하거나 드롭다운 선택기에서 꺾은선형 또는 영역 차트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="be475-145">불연속성: 데이터에 중요한 불연속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="be475-146">분석할 지점이 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="be475-147">쿼리에 둘 이상의 요약 절이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="be475-148">요약 절 앞에 이름 정의를 포함하는 프로젝트 절이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be475-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="be475-149">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="be475-149">Related articles</span></span>

 * [<span data-ttu-id="be475-150">Analytics 자습서</span><span class="sxs-lookup"><span data-stu-id="be475-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="be475-151">[스마트 감지](app-insights-proactive-diagnostics.md)는 성능 문제에 대해 자동으로 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="be475-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>