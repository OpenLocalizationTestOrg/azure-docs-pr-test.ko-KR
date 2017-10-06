---
title: "Azure Application Insights에서 웹 응용 프로그램은 성능 변경의 aaaSmart 진단 | Microsoft Docs"
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
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="28964-103">앱 원격 분석에서 급격한 변화 진단</span><span class="sxs-lookup"><span data-stu-id="28964-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="28964-104">*이 기능은 미리 보기 상태입니다.*</span><span class="sxs-lookup"><span data-stu-id="28964-104">*This feature is in preview.*</span></span>

<span data-ttu-id="28964-105">단 한 번의 클릭으로 웹앱의 성능 또는 사용 현황의 급격한 변화를 진단해 보세요.</span><span class="sxs-lookup"><span data-stu-id="28964-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="28964-106">시간 차트를 만들 때마다 hello 스마트 진단 기능을 사용할 수 있는 [분석](app-insights-analytics.md) 에 [Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="28964-107">Hello 추세 스파이크 또는 dip를 같은 결과를에서 한 비정상적인 변경 있을 때마다 스마트 진단 차원과 hello 변경을 설명할 수 있는 관련된 값의 패턴을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="28964-108">Hello 문제를 빠르게 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="28964-109">이 예제에서는 스마트 진단 hello 변경과 관련 된 속성 값의 패턴을 식별 했습니다 하 고 결과 해당 패턴 없는 hello 차이 강조 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![예제 분석 진단 결과](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="28964-111">데이터 변경 진단</span><span class="sxs-lookup"><span data-stu-id="28964-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="28964-112">분석에서 쿼리를 실행하고 시간 차트로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="28964-113">강조 표시된 최대 사용 지점이 있는 경우 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![최대 사용 지점](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="28964-115">진단 하는 데 몇 초 toodiscover 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="28964-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="28964-116">진단 결과 탭 hello 데이터 불연속성 설명 하는 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28964-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="28964-118">hello 텍스트를 hello shift와 toocorrelate 나타나는 hello 차원 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28964-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="28964-119">이 예제에서는 특정 요청 및 특정 브라우저 버전과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="28964-120">Hello 차트 hello 필터 true 및 false와의 hello 두 구성 요소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="28964-121">hello false 구성 요소는 변경 되지 않은 추세를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28964-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="28964-122">즉, hello 문제가 있는 차원 조합으로 진단에서 확인을 제외 하는 경우 hello 원격 분석 결과에 변경 내용이 없는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="28964-123">반면, 해당 조합이 내의 hello 결과 조사 hello 강조 표시 영역 내에서 큰 변화를 표시지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="28964-124">이렇게 하면 진단 hello 변경에 설명 하는 속성의 조합을 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="28964-125">보다 toohover hello 패턴 복잡 한 경우 필요한 경우 **모두 표시** toosee hello 차원.</span><span class="sxs-lookup"><span data-stu-id="28964-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![모두 표시](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="28964-127">경우 진단에 대 한 '결과' 페이지 나타납니다 hello 없는 중요 한 패턴 toonotify를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="28964-128">이 시점에서 쿼리를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-128">At this point, you may change your query.</span></span> <span data-ttu-id="28964-129">예를 들어 잠재적으로 더 나은 결과 및 추가 분석에 대 한 분석 쿼리를 범주화 하 고 hello 시간 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="28964-130">특정 브라우저에서 웹 사이트의 특정 페이지에 문제가 있는지 hello 지식으로 무장 된, 이제 직선 toohello 문제 페이지 돌아가서 최근 변경 내용을 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="28964-131">Hello 데모를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="28964-131">Try hello demo</span></span>

<span data-ttu-id="28964-132">[여기를 클릭 toosee 데모](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) 예제 데이터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="28964-133">작동 방법</span><span class="sxs-lookup"><span data-stu-id="28964-133">How it works</span></span>

<span data-ttu-id="28964-134">Hello 기반의 고급 감독 되지 않은 기계 학습 알고리즘을 사용 하 여 스마트 진단 [DiffPatterns](app-insights-analytics-reference.md) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="28964-135">데이터 변경 hello를 설명할 수 있는 후보 패턴을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="28964-136">Hello 메트릭에서 각 후보의 hello 영향 분석 하 고 가장 hello 변경 연관 hello 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28964-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="28964-137">진단 지점은 없나요?</span><span class="sxs-lookup"><span data-stu-id="28964-137">No diagnostic points?</span></span>

<span data-ttu-id="28964-138">스마트 진단 hello 다음 조건을 충족 하는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="28964-139">스마트 진단 설정이 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28964-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="28964-140">분석에서 hello 설정 아이콘 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="28964-141">hello 분석 설정에서 스마트 진단 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="28964-142">시간 축: hello hello 차트의 x 축 유형 이어야 `datetime`합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="28964-143">꺾은선형 또는 영역 차트: 진단은 이러한 종류의 차트에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="28964-144">사용 하 여 `| render timechart` 또는 `| render areachart` 쿼리의; hello 끝에서 하거나 hello 드롭다운 선택기에서 줄 또는 영역형 차트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="28964-145">불연속성: 중요 한 불연속성에에서 있어야 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="28964-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="28964-146">포인트 tooanalyze 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="28964-147">개 이상 hello 쿼리 절을 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="28964-148">Hello 전에 이름 정의 포함 하는 프로젝트 절 없이 절을 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="28964-149">관련 문서</span><span class="sxs-lookup"><span data-stu-id="28964-149">Related articles</span></span>

 * [<span data-ttu-id="28964-150">Analytics 자습서</span><span class="sxs-lookup"><span data-stu-id="28964-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="28964-151">[검색 스마트](app-insights-proactive-diagnostics.md) 자동으로 tooperformance 문제 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="28964-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
