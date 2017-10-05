---
title: "Azure Application Insights의 원격 분석 샘플링 | Microsoft Docs"
description: "제어에서 원격 분석의 양을 유지하는 방법입니다."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: ceaeced414c9c302fba335b4578bcdcbfaef0410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="d2c3d-103">Application Insights의 샘플링</span><span class="sxs-lookup"><span data-stu-id="d2c3d-103">Sampling in Application Insights</span></span>


<span data-ttu-id="d2c3d-104">샘플링은 [Azure Application Insights](app-insights-overview.md)의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d2c3d-105">응용 프로그램 데이터의 올바른 분석을 통계적으로 유지하는 동안 원격 분석 트래픽 및 저장소를 줄일 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-105">It is the recommended way to reduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="d2c3d-106">필터는 관련된 항목을 선택하여 진단 조사를 수행할 때 항목 간을 탐색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-106">The filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="d2c3d-107">포털에서 메트릭 개수가 나타나면 통계에 영향을 최소화하기 위해 샘플링을 고려하도록 다시 정상화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-107">When metric counts are presented to you in the portal, they are renormalized to take account of the sampling, to minimize any effect on the statistics.</span></span>

<span data-ttu-id="d2c3d-108">샘플링은 트래픽 및 데이터 비용을 줄여주며 제한을 피하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="d2c3d-109">개요:</span><span class="sxs-lookup"><span data-stu-id="d2c3d-109">In brief:</span></span>
* <span data-ttu-id="d2c3d-110">샘플링에 1 유지  *n*  기록 되 고 나머지를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-110">Sampling retains 1 in *n* records and discards the rest.</span></span> <span data-ttu-id="d2c3d-111">예를 들어 20%의 샘플링 속도로 5개의 이벤트 1을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="d2c3d-112">응용 프로그램이 다양한 원격 분석을 보내는 경우 샘플링은 ASP.NET 웹 서버 앱에서 자동으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="d2c3d-113">샘플링을 가격 책정 페이지의 포털 또는 .config 파일의 ASP.NET SDK에서 수동으로 설정하여 네트워크 트래픽을 줄일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-113">You can also set sampling manually, either in the portal on the pricing page; or in the ASP.NET SDK in the .config file, to also reduce the network traffic.</span></span>
* <span data-ttu-id="d2c3d-114">사용자 지정 이벤트를 기록하고 일련의 이벤트가 유지되는지 아니면 함께 무시되는지 확인하려는 경우 동일한 OperationId 값을 갖는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-114">If you log custom events and you want to make sure that a set of events is either retained or discarded together, make sure that they have the same OperationId value.</span></span>
* <span data-ttu-id="d2c3d-115">샘플링 제  *n*  속성의 각 레코드에 보고 `itemCount`, 검색에 나타나는 이름 "요청 수" 또는 "이벤트 개수"입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-115">The sampling divisor *n* is reported in each record in the property `itemCount`, which in Search appears under the friendly name "request count" or "event count".</span></span> <span data-ttu-id="d2c3d-116">샘플링이 작업 중이지 않을 때 `itemCount==1`입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="d2c3d-117">분석 쿼리를 작성하는 경우 [샘플링을 고려](app-insights-analytics-tour.md#counting-sampled-data)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="d2c3d-118">특히, 레코드를 단순히 세는 대신 `summarize sum(itemCount)`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="d2c3d-119">샘플링 유형</span><span class="sxs-lookup"><span data-stu-id="d2c3d-119">Types of sampling</span></span>
<span data-ttu-id="d2c3d-120">다음은 세 가지 대체 샘플링 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="d2c3d-121">**적응 샘플링** 은 ASP.NET 앱의 SDK에서 전송되는 원격 분석의 양을 자동으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-121">**Adaptive sampling** automatically adjusts the volume of telemetry sent from the SDK in your ASP.NET app.</span></span> <span data-ttu-id="d2c3d-122">기본 버전은 SDK v 2.0.0-beta3입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="d2c3d-123">현재 ASP.NET 서버 측 원격 분석만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="d2c3d-124">**고정 비율 샘플링** 은 ASP.NET 서버와 사용자 브라우저에서 전송되는 원격 분석의 양을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-124">**Fixed-rate sampling** reduces the volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="d2c3d-125">비율은 사용자가 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-125">You set the rate.</span></span> <span data-ttu-id="d2c3d-126">클라이언트와 서버는 샘플링을 동기화하므로 검색에서 관련된 페이지 보기 및 요청 사이를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-126">The client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="d2c3d-127">**수집 샘플링**은 Azure Portal에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-127">**Ingestion sampling** works in the Azure portal.</span></span> <span data-ttu-id="d2c3d-128">설정한 속도에 따라 앱에서 들어오는 원격 분석 중 일부를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-128">It discards some of the telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="d2c3d-129">원격 분석 트래픽을 줄이지는 않지만 월간 할당량 내로 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="d2c3d-130">수집 샘플링의 가장 큰 장점은 앱을 다시 배포하지 않고 설정할 수 있으며, 모든 서버와 클라이언트에 균일하게 작동한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-130">The big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="d2c3d-131">적응 또는 고정 비율 샘플링이 작업 중인 경우 수집 샘플링은 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="d2c3d-132">수집 샘플링</span><span class="sxs-lookup"><span data-stu-id="d2c3d-132">Ingestion sampling</span></span>
<span data-ttu-id="d2c3d-133">이 샘플링 형식은 웹 서버, 브라우저 및 장치의 원격 분석이 Application Insights 서비스 끝점에 도달하는 지점에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-133">This form of sampling operates at the point where the telemetry from your web server, browsers, and devices reaches the Application Insights service endpoint.</span></span> <span data-ttu-id="d2c3d-134">앱에서 전송되는 원격 분석 트래픽을 줄이지는 않지만 Application Insights에서 처리 및 보존(및 청구)되는 양을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-134">Although it doesn't reduce the telemetry traffic sent from your app, it does reduce the amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="d2c3d-135">앱이 월간 할당량을 자주 초과하지만 SDK 기반의 샘플링 유형 중 하나를 사용할 옵션이 없는 경우 이 샘플링 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-135">Use this type of sampling if your app often goes over its monthly quota and you don't have the option of using either of the SDK-based types of sampling.</span></span> 

<span data-ttu-id="d2c3d-136">할당량 및 가격 블레이드에서 샘플링 주기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-136">Set the sampling rate in the Quotas and Pricing blade:</span></span>

![응용 프로그램 개요 블레이드에서 설정, 할당량, 샘플을 차례로 클릭한 다음 샘플링 주기를 선택하고 업데이트를 클릭합니다.](./media/app-insights-sampling/04.png)

<span data-ttu-id="d2c3d-138">다른 샘플링 유형과 마찬가지로 알고리즘에 관련 원격 분석 항목이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-138">Like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="d2c3d-139">예를 들어 검색에서 원격 분석을 검사하는 경우 특정 예외와 관련된 요청을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-139">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> <span data-ttu-id="d2c3d-140">요청 빈도 및 예외 처리 빈도와 같은 메트릭 수는 올바르게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="d2c3d-141">샘플링에서 무시된 데이터 요소는 [연속 내보내기](app-insights-export-telemetry.md)와 같은 Application Insights 기능에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="d2c3d-142">SDK 기반 적응 또는 고정 비율 샘플링이 작동되는 동안에는 수집 샘플링이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="d2c3d-143">SDK의 샘플링 비율이 100%보다 작으면 설정된 수집 샘플링 설정이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-143">If the sampling rate at the SDK is less than 100%, then the ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="d2c3d-144">타일에 표시된 값은 수집 샘플링에 대해 설정한 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-144">The value shown on the tile indicates the value that you set for ingestion sampling.</span></span> <span data-ttu-id="d2c3d-145">SDK 샘플링이 작업 중인 경우 실제 샘플링 속도를 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-145">It doesn't represent the actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="d2c3d-146">웹 서버의 적응 샘플링</span><span class="sxs-lookup"><span data-stu-id="d2c3d-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="d2c3d-147">적응 샘플링은 ASP.NET v 2.0.0-beta3 이상용 Application Insights SDK에 사용할 수 있으며, 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-147">Adaptive sampling is available for the Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="d2c3d-148">적응 샘플링은 웹 서버 앱에서 Application Insights 서비스로 보내는 원격 분석의 양에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-148">Adaptive sampling affects the volume of telemetry sent from your web server app to the Application Insights service.</span></span> <span data-ttu-id="d2c3d-149">이 양은 지정된 최대 트래픽 속도 내에서 유지되도록 자동으로 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-149">The volume is adjusted automatically to keep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="d2c3d-150">적은 양의 원격 분석에서는 작동하지 않으므로 사용량이 적은 웹 사이트 또는 디버그 중인 앱은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="d2c3d-151">목표 양을 달성하기 위해 생성된 원격 분석 중 일부가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-151">To achieve the target volume, some of the telemetry generated is discarded.</span></span> <span data-ttu-id="d2c3d-152">그러나 다른 샘플링 유형과 마찬가지로 알고리즘에 관련 원격 분석 항목이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-152">But like other types of sampling, the algorithm retains related telemetry items.</span></span> <span data-ttu-id="d2c3d-153">예를 들어 검색에서 원격 분석을 검사하는 경우 특정 예외와 관련된 요청을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-153">For example, when you're inspecting the telemetry in Search, you'll be able to find the request related to a particular exception.</span></span> 

<span data-ttu-id="d2c3d-154">요청 빈도 및 예외 처리 빈도와 같은 메트릭 수는 샘플링 주기에 맞게 보정되도록 조정되므로 메트릭 탐색기에서 거의 정확한 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-154">Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="d2c3d-155">최신 *시험판* 버전의 Application Insights로 **프로젝트의 NuGet 패키지를 업데이트**합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, NuGet 패키지 관리를 선택하고 **시험판 포함**을 선택한 다음 Microsoft.ApplicationInsights.Web을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-155">**Update your project's NuGet** packages to the latest *pre-release* version of Application Insights: Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="d2c3d-156">[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)의 `AdaptiveSamplingTelemetryProcessor` 노드에서 여러 매개 변수를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in the `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="d2c3d-157">표시된 수치는 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-157">The figures shown are the default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="d2c3d-158">대상 비율은 **각 서버 호스트에**대한 것을 목표로 하는 적응 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-158">The target rate that the adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="d2c3d-159">여러 호스트에서 웹앱을 실행하는 경우 Application Insights 포털에서 트래픽을 대상 비율 범위 내에서 유지하기 위해 이 값을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-159">If your web app runs on many hosts, reduce this value so as to remain within your target rate of traffic at the Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="d2c3d-160">현재 비율의 원격 분석 간격이 다시 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-160">The interval at which the current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="d2c3d-161">평가는 이동 평균으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="d2c3d-162">원격 분석이 급격히 증가하는 경우 이 간격을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-162">You might want to shorten this interval if your telemetry is liable to sudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="d2c3d-163">샘플링 비율 값을 변경한 후 더 적은 데이터를 캡처하기 위해 샘플링 비율을 다시 낮출 수 있는 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-163">When sampling percentage value changes, how soon after are we allowed to lower sampling percentage again to capture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="d2c3d-164">샘플링 비율 값을 변경한 후 더 많은 데이터를 캡처하기 위해 샘플링 비율을 다시 높일 수 있는 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-164">When sampling percentage value changes, how soon after are we allowed to increase sampling percentage again to capture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="d2c3d-165">샘플링 비율이 변경됨에 따라 사용자가 설정할 수 있는 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-165">As sampling percentage varies, what is the minimum value we're allowed to set.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="d2c3d-166">샘플링 비율이 변경됨에 따라 사용자가 설정할 수 있는 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-166">As sampling percentage varies, what is the maximum value we're allowed to set.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="d2c3d-167">이동 평균 계산에서 가중치는 가장 최근의 값에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-167">In the calculation of the moving average, the weight assigned to the most recent value.</span></span> <span data-ttu-id="d2c3d-168">1보다 작거나 같은 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-168">Use a value equal to or less than 1.</span></span> <span data-ttu-id="d2c3d-169">값이 작을수록 알고리즘은 갑작스런 변화에 덜 반응합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-169">Smaller values make the algorithm less reactive to sudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="d2c3d-170">앱을 막 시작했을 때 할당된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-170">The value assigned when the app has just started.</span></span> <span data-ttu-id="d2c3d-171">디버깅하는 동안 이 값을 줄이지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="d2c3d-172">샘플링하지 않으려는 형식의 세미콜론으로 구분된 목록</span><span class="sxs-lookup"><span data-stu-id="d2c3d-172">A semi-colon delimited list of types that you do not want to be sampled.</span></span> <span data-ttu-id="d2c3d-173">인식되는 형식: 종속성, 이벤트, 예외, 페이지 보기, 요청, 추적</span><span class="sxs-lookup"><span data-stu-id="d2c3d-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="d2c3d-174">지정된 형식의 모든 인스턴스가 전송되고 지정되지 않은 형식은 샘플링됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-174">All instances of the specified types are transmitted; the types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="d2c3d-175">샘플링하려는 형식의 세미콜론으로 구분된 목록</span><span class="sxs-lookup"><span data-stu-id="d2c3d-175">A semi-colon delimited list of types that you want to be sampled.</span></span> <span data-ttu-id="d2c3d-176">인식되는 형식: 종속성, 이벤트, 예외, 페이지 보기, 요청, 추적</span><span class="sxs-lookup"><span data-stu-id="d2c3d-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="d2c3d-177">지정된 형식이 샘플링되고 다른 형식의 모든 인스턴스가 항상 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-177">The specified types are sampled; all instances of the other types will always be transmitted.</span></span>


<span data-ttu-id="d2c3d-178">적응 샘플링을 **해제하려면** applicationinsights-config에서 AdaptiveSamplingTelemetryProcessor 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-178">**To switch off** adaptive sampling, remove the AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="d2c3d-179">대체: 코드에서 적응 샘플링 구성</span><span class="sxs-lookup"><span data-stu-id="d2c3d-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="d2c3d-180">.config 파일의 샘플링을 조정하는 대신 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-180">Instead of adjusting sampling in the .config file, you can use code.</span></span> <span data-ttu-id="d2c3d-181">이를 통해 샘플링 속도가 다시 계산될 때마다 호출되는 콜백 함수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-181">This allows you to specify a callback function that is invoked whenever the sampling rate is re-evaluated.</span></span> <span data-ttu-id="d2c3d-182">예를 들어 이를 사용하여 샘플링 속도를 사용하는 작업을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-182">You could use this, for example, to find out what sampling rate is being used.</span></span>

<span data-ttu-id="d2c3d-183">.config 파일에서 `AdaptiveSamplingTelemetryProcessor` 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-183">Remove the `AdaptiveSamplingTelemetryProcessor` node from the .config file.</span></span>

<span data-ttu-id="d2c3d-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust the settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report the sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d2c3d-185">([원격 분석 프로세서에 대해 알아봅니다](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="d2c3d-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="d2c3d-186">JavaScript를 사용하는 웹 페이지에 대한 샘플링</span><span class="sxs-lookup"><span data-stu-id="d2c3d-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="d2c3d-187">서버에서 고정 비율 샘플링에 대한 웹 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="d2c3d-188">[Application Insights에 대한 웹 페이지를 구성](app-insights-javascript.md)할 때 Application Insights 포털에서 얻은 코드 조각을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-188">When you [configure the web pages for Application Insights](app-insights-javascript.md), modify the snippet that you get from the Application Insights portal.</span></span> <span data-ttu-id="d2c3d-189">(ASP.NET 앱에서 코드 조각은 일반적으로 _Layout.cshtml로 이동합니다.)  계측 키 앞에 `samplingPercentage: 10,`과 같은 줄을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-189">(In ASP.NET apps, the snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before the instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="d2c3d-190">샘플링 비율의 경우 100/N(여기서 N은 정수)에 가까운 백분율을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-190">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="d2c3d-191">현재 샘플링은 다른 값을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="d2c3d-192">서버에서도 고정 비율 샘플링을 사용하도록 설정하는 경우 클라이언트와 서버가 동기화되므로 검색에서 관련된 페이지 보기 및 요청 사이를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-192">If you also enable fixed-rate sampling at the server, the clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="d2c3d-193">ASP.NET 웹 사이트에 대한 고정 비율 샘플링</span><span class="sxs-lookup"><span data-stu-id="d2c3d-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="d2c3d-194">고정 비율 샘플링은 웹 서버와 웹 브라우저에서 전송되는 트래픽을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-194">Fixed rate sampling reduces the traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="d2c3d-195">적응 샘플링과 달리 사용자가 결정한 고정 비율로 원격 분석을 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="d2c3d-196">또한 관련 항목이 유지되도록, 예를 들어 검색의 페이지 보기에서 관련 요청을 찾을 수 있도록 클라이언트와 서버의 샘플링을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-196">It also synchronizes the client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="d2c3d-197">샘플링 알고리즘에는 관련 항목이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-197">The sampling algorithm retains related items.</span></span> <span data-ttu-id="d2c3d-198">각 HTTP 요청 이벤트에 대해 해당 이벤트와 관련 이벤트가 삭제되거나 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="d2c3d-199">메트릭 탐색기에서 요청 및 예외 수와 같은 빈도는 거의 정확한 값이 되도록 계수가 곱해져 샘플링 주기에 맞게 보정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor to compensate for the sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="d2c3d-200">**시험판** 버전의 Application Insights로 *프로젝트의 NuGet 패키지를 업데이트* 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-200">**Update your project's NuGet packages** to the latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="d2c3d-201">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, NuGet 패키지 관리를 선택하고 **시험판 포함** 을 선택한 다음 Microsoft.ApplicationInsights.Web을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-201">Right-click the project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="d2c3d-202">**적응 샘플링을 사용하지 않도록 설정**: [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에서 `AdaptiveSamplingTelemetryProcessor` 노드를 제거하거나 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out the `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="d2c3d-203">**고정 비율 샘플링 모듈을 사용하도록 설정합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2c3d-203">**Enable the fixed-rate sampling module.**</span></span> <span data-ttu-id="d2c3d-204">다음 코드 조각을 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-204">Add this snippet to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="d2c3d-205">샘플링 비율의 경우 100/N(여기서 N은 정수)에 가까운 백분율을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-205">For the sampling percentage, choose a percentage that is close to 100/N where N is an integer.</span></span>  <span data-ttu-id="d2c3d-206">현재 샘플링은 다른 값을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="d2c3d-207">대체: 서버 코드에서 고정 비율 샘플링을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d2c3d-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="d2c3d-208">.config 파일에 샘플링 매개 변수를 설정하는 대신 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-208">Instead of setting the sampling parameter in the .config file, you can use code.</span></span> 

<span data-ttu-id="d2c3d-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d2c3d-210">([원격 분석 프로세서에 대해 알아봅니다](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="d2c3d-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-to-use-sampling"></a><span data-ttu-id="d2c3d-211">언제 샘플링을 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="d2c3d-211">When to use sampling?</span></span>
<span data-ttu-id="d2c3d-212">ASP.NET SDK 버전 2.0.0-beta3 이상을 사용하는 경우 적응 샘플링이 자동으로 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-212">Adaptive sampling is automatically enabled if you use the ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="d2c3d-213">사용하는 SDK 버전에 상관없이 서버에서 수집 샘플링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="d2c3d-214">대부분의 중소 응용 프로그램은 샘플링하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="d2c3d-215">가장 유용한 진단 정보 및 가장 정확한 통계는 모든 사용자 활동에서 데이터를 수집하여 구합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-215">The most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="d2c3d-216">샘플링의 주요 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-216">The main advantages of sampling are:</span></span>

* <span data-ttu-id="d2c3d-217">앱이 짧은 시간 간격으로 매우 높은 비율의 원격 분석을 전송할 때 Application Insights 서비스는 ("제한") 데이터 요소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="d2c3d-218">가격 책정 계층에 대한 데이터 요소의 [할당량](app-insights-pricing.md) 을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-218">To keep within the [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="d2c3d-219">원격 분석의 컬렉션에서 네트워크 트래픽을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-219">To reduce network traffic from the collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="d2c3d-220">어떤 유형의 샘플링을 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d2c3d-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="d2c3d-221">**다음과 같은 경우 수집 샘플링을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2c3d-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="d2c3d-222">원격 분석의 월간 할당량을 자주 초과하는 경우</span><span class="sxs-lookup"><span data-stu-id="d2c3d-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="d2c3d-223">샘플링을 지원하지 않는 SDK 버전(예: Java SDK 또는 ASP.NET 버전 2 미만)을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="d2c3d-223">You're using a version of the SDK that doesn't support sampling - for example, the Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="d2c3d-224">사용자의 웹 브라우저에서 많은 원격 분석이 전송되는 경우</span><span class="sxs-lookup"><span data-stu-id="d2c3d-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="d2c3d-225">**다음과 같은 경우 고정 비율 샘플링을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2c3d-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="d2c3d-226">ASP.NET 웹 서비스용 Application Insights SDK 버전 2.0.0 이상을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="d2c3d-226">You're using the Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="d2c3d-227">사용자가 클라이언트 및 서버 간의 동기화된 샘플링을 원하는 경우 [검색](app-insights-diagnostic-search.md)에서 이벤트를 조사하고 있을 때 클라이언트 및 서버에서 페이지 보기 및 http 요청과 같은 관련 이벤트 사이를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on the client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="d2c3d-228">사용자가 앱에 대한 적절한 샘플링 비율을 확신하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-228">You are confident of the appropriate sampling percentage for your app.</span></span> <span data-ttu-id="d2c3d-229">샘플링 비율은 정확한 메트릭을 가져오기 위해 충분히 높아야 하지만 가격 책정 할당량 및 조정 제한을 초과하는 비율보다 낮아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-229">It should be high enough to get accurate metrics, but below the rate that exceeds your pricing quota and the throttling limits.</span></span> 

<span data-ttu-id="d2c3d-230">**다음과 같은 경우 적응 샘플링을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="d2c3d-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="d2c3d-231">그렇지 않은 경우 적응 샘플링을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="d2c3d-232">이 샘플링은 ASP.NET 서버 SDK 버전 2.0.0-beta3 이상에서 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-232">This is enabled by default in the ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="d2c3d-233">특정 최소 속도까지 트래픽을 줄이지 않으므로 사용량이 적은 사이트에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="d2c3d-234">샘플링이 작업 중인지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d2c3d-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="d2c3d-235">적용된 위치에 관계 없이 실제 샘플링 주기를 검색하려면 다음과 같은 [분석 쿼리](app-insights-analytics.md) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-235">To discover the actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="d2c3d-236">보존된 각 레코드에서 `itemCount` 은 나타내는 원래 레코드 수를 나타내며 1 + 이전에 삭제된 레코드의 수와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-236">In each retained record, `itemCount` indicates the number of original records that it represents, equal to 1 + the number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="d2c3d-237">샘플링은 어떻게 작동되나요?</span><span class="sxs-lookup"><span data-stu-id="d2c3d-237">How does sampling work?</span></span>
<span data-ttu-id="d2c3d-238">고정 비율 및 적응 샘플링은 ASP.NET 버전 2.0.0 이상에서의 SDK 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-238">Fixed-rate and adaptive sampling are a feature of the SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="d2c3d-239">수집 샘플링은 Application Insights 서비스의 기능이며 SDK가 샘플링을 수행하지 않는 경우 작동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-239">Ingestion sampling is a feature of the Application Insights service, and can be in operation if the SDK is not performing sampling.</span></span> 

<span data-ttu-id="d2c3d-240">샘플링 알고리즘은 어떤 원격 분석 항목을 삭제할 것인지 및 유지(SDK 또는 Application Insights 서비스에)할 것인지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-240">The sampling algorithm decides which telemetry items to drop, and which ones to keep (whether it's in the SDK or in the Application Insights service).</span></span> <span data-ttu-id="d2c3d-241">샘플링 의사 결정은 상호 관련된 데이터 요소를 그대로 유지하려는 목표의 여러 규칙에 기반하며 이는 감소된 데이터 집합을 사용하더라도 실행할 수 있고 신뢰할 수 있는 Application Insights에서 진단 환경을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-241">The sampling decision is based on several rules that aim to preserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="d2c3d-242">예를 들어 실패한 요청의 경우 앱이 추가 원격 분석 항목을 전송하면(예: 해당 요청에서 기록된 예외 및 추적) 샘플링은 해당 요청 및 기타 원격 분석을 분할하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="d2c3d-243">전체를 유지하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="d2c3d-244">결과적으로 Application Insights에서 요청 세부 정보를 볼 때 항상 연결된 원격 분석 항목과 함께 요청을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-244">As a result, when you look at the request details in Application Insights, you can always see the request along with its associated telemetry items.</span></span> 

<span data-ttu-id="d2c3d-245">"사용자"를 정의하는 응용 프로그램의 경우(즉, 가장 일반적인 웹 응용 프로그램) 샘플링 의사 결정은 사용자 ID의 해시에 기반하며 이는특정 사용자에 대한 모든 원격 분석이 유지되거나 삭제된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-245">For applications that define "user" (that is, most typical web applications), the sampling decision is based on the hash of the user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="d2c3d-246">사용자를 정의하지 않는 응용 프로그램 형식의 경우(예: 웹 서비스) 샘플링 의사 결정은 요청의 작업 ID를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-246">For the types of applications that don't define users (such as web services) the sampling decision is based on the operation id of the request.</span></span> <span data-ttu-id="d2c3d-247">마지막으로 사용자 또는 작업 ID가 없는 원격 분석 항목의 경우(예: http 컨텍스트가 없는 비동기 스레드에서 보고된 원격 분석 항목) 샘플링은 단순히 각 형식의 원격 분석 항목 백분율을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-247">Finally, for the telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="d2c3d-248">원격 분석을 다시 표시하는 경우 Application Insights 서비스는 누락된 데이터 요소를 보완하기 위해 컬렉션의 시간에 사용된 동일한 샘플링 백분율로 메트릭을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-248">When presenting telemetry back to you, the Application Insights service adjusts the metrics by the same sampling percentage that was used at the time of collection, to compensate for the missing data points.</span></span> <span data-ttu-id="d2c3d-249">따라서 Application Insights에서 원격 분석을 보면 사용자는 실제 수에 가까운 통계적으로 올바른 근사치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-249">Hence, when looking at the telemetry in Application Insights, the users are seeing statistically correct approximations that are very close to the real numbers.</span></span>

<span data-ttu-id="d2c3d-250">근사치의 정확도는 주로 구성된 샘플링 비율에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-250">The accuracy of the approximation largely depends on the configured sampling percentage.</span></span> <span data-ttu-id="d2c3d-251">또한 아주 많은 사용자에게서 많은 양의 일반적으로 비슷한 요청을 처리하는 응용 프로그램에 대해 정확도가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-251">Also, the accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="d2c3d-252">반면에 상당한 부하가 있을 때 작동하지 않는 응용 프로그램의 경우 이러한 응용 프로그램이 일반적으로 할당량 내에 있으면서 제한에서 데이터 손실이 발생하지 않고 해당 원격 분석을 모두 보낼 수 있기에 샘플링은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-252">On the other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within the quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="d2c3d-253">이러한 자릿수의 형식 감소가 매우 바람직하지 않을 수 있기 때문에 Application Insights는 메트릭 및 세션 원격 분석 형식을 샘플링하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in the precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="d2c3d-254">적응 샘플링</span><span class="sxs-lookup"><span data-stu-id="d2c3d-254">Adaptive sampling</span></span>
<span data-ttu-id="d2c3d-255">적응 샘플링은 SDK에서 현재의 전송 속도를 모니터링하는 구성 요소를 추가하여 샘플링 비율이 대상 최대 비율 안에서 유지되도록 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-255">Adaptive sampling adds a component that monitors the current rate of transmission from the SDK, and adjusts the sampling percentage to try to stay within the target maximum rate.</span></span> <span data-ttu-id="d2c3d-256">조정은 정기적으로 다시 계산되고 발신 전송 속도의 이동 평균에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-256">The adjustment is recalculated at regular intervals, and is based on a moving average of the outgoing transmission rate.</span></span>

## <a name="sampling-and-the-javascript-sdk"></a><span data-ttu-id="d2c3d-257">샘플링 및 JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="d2c3d-257">Sampling and the JavaScript SDK</span></span>
<span data-ttu-id="d2c3d-258">클라이언트 측(JavaScript) SDK는 서버 측 SDK과 함께 고정 비율 샘플링에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-258">The client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with the server-side SDK.</span></span> <span data-ttu-id="d2c3d-259">계측된 페이지는 서버 측이 "샘플"로 결정한 동일한 사용자의 클라이언트 측 원격 분석만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-259">The instrumented pages will only send client-side telemetry from the same users for which the server-side made its decision to "sample in."</span></span> <span data-ttu-id="d2c3d-260">이 논리는 전체 클라이언트 및 서버 측에 대한 사용자 세션의 무결성을 유지하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-260">This logic is designed to maintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="d2c3d-261">결과적으로 Application Insights의 특정 원격 분석 항목에서 해당 사용자 또는 세션에 대한 다른 모든 원격 분석 항목을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="d2c3d-262">*위에 설명한 대로 내 클라이언트 및 서버 측 원격 분석은 조정된 샘플을 표시하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="d2c3d-263">서버 및 클라이언트 모두에서 고정 비율 샘플링을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="d2c3d-264">SDK 버전이 2.0 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-264">Make sure that the SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="d2c3d-265">클라이언트와 서버 모두에서 동일한 샘플링 비율을 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-265">Check that you set the same sampling percentage in both the client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d2c3d-266">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="d2c3d-266">Frequently Asked Questions</span></span>
<span data-ttu-id="d2c3d-267">*샘플링은 왜 간단히 "각 원격 분석 형식의 X 퍼센트를 수집"하지 않습니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="d2c3d-268">이 샘플링 방법이 메트릭 근사치에 매우 높은 정밀도를 제공하지만 사용자, 세션 및 요청 단위 당 진단 데이터를 연결하는 기능을 중단시키며 이는 진단에 있어 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability to correlate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="d2c3d-269">따라서 샘플링은 "앱 사용자의 X 퍼센트에 대해 모든 원격 분석 항목 수집" 또는 "앱 요청의 X퍼센트에 대한 모든 원격 분석 수집" 논리를 사용하여 더 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="d2c3d-270">요청과 연결되지 않은 원격 분석 항목의 경우(예: 배경 비동기 처리) "각 원격 분석 형식에 대해 모든 항목의 X퍼센트 수집"으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-270">For the telemetry items not associated with the requests (such as background asynchronous processing), the fall back is to "collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="d2c3d-271">*샘플링 비율은 시간이 지나면서 달라질 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-271">*Can the sampling percentage change over time?*</span></span>

* <span data-ttu-id="d2c3d-272">예, 적응 샘플링은 원격 분석의 현재 관찰된 양에 따라 샘플링 비율을 점차적으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-272">Yes, adaptive sampling gradually changes the sampling percentage, based on the currently observed volume of the telemetry.</span></span>

<span data-ttu-id="d2c3d-273">*고정 비율 샘플링을 사용하는 경우 내 앱에 가장 적합한 샘플링 비율을 어떻게 알 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work the best for my app?*</span></span>

* <span data-ttu-id="d2c3d-274">한 가지 방법은 적응 샘플링으로 시작하고 안정적인 비율(위 질문 참조)을 찾은 다음 해당 비율을 사용하여 고정 비율 샘플링으로 전환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-274">One way is to start with adaptive sampling, find out what rate it settles on (see the above question), and then switch to fixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="d2c3d-275">그렇지 않으면 추측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-275">Otherwise, you have to guess.</span></span> <span data-ttu-id="d2c3d-276">AI에서 현재 원격 분석 사용량을 분석하고 발생하는 모든 제한을 관찰하며 수집된 원격 분석의 양을 추정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate the volume of the collected telemetry.</span></span> <span data-ttu-id="d2c3d-277">선택된 가격 책정 계층과 함께 이러한 세 가지 입력은 수집된 원격 분석의 볼륨을 얼마나 줄여야 할지 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-277">These three inputs, together with your selected pricing tier, suggest how much you might want to reduce the volume of the collected telemetry.</span></span> <span data-ttu-id="d2c3d-278">그러나 사용자 수가 증가하거나 원격 분석의 양이 약간 다르게 변화되면 추정치가 무효화될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-278">However, an increase in the number of your users or some other shift in the volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="d2c3d-279">*샘플링 비율을 너무 낮게 구성하는 경우 어떻게 됩니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="d2c3d-280">샘플링 비율이 지나치게 낮으면(지나친 샘플링) Application Insights가 데이터의 볼륨을 축소하기 위해 데이터의 시각화를 보완하려고 할 때 근사치의 정확도가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-280">Excessively low sampling percentage (over-aggressive sampling) reduces the accuracy of the approximations, when Application Insights attempts to compensate the visualization of the data for the data volume reduction.</span></span> <span data-ttu-id="d2c3d-281">또한 종종 실패하거나 요청이 느린 경우 샘플링되기에 진단 환경은 부정적으로 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-281">Also, diagnostic experience might be negatively impacted, as some of the infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="d2c3d-282">*샘플링 비율을 너무 높게 구성하는 경우 어떻게 됩니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="d2c3d-283">샘플링 비율을 너무 높게 구성하면(충분히 공격적이지 않음) 수집된 원격 분석의 볼륨이 충분히 감소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in the volume of the collected telemetry.</span></span> <span data-ttu-id="d2c3d-284">여전히 제한에 관련된 원격 분석 데이터 손실이 발생할 수 있고 Application Insights를 사용하는 비용은 초과 요금때문에 계획된 것 보다 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-284">You may still experience telemetry data loss related to throttling, and the cost of using Application Insights might be higher than you planned due to overage charges.</span></span>

<span data-ttu-id="d2c3d-285">*샘플링을 어떤 플랫폼에서 사용할 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="d2c3d-286">SDK가 샘플링을 수행하지 않는 경우 특정 볼륨을 초과하는 모든 원격 분석에 대해 자동으로 수집 샘플링이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if the SDK is not performing sampling.</span></span> <span data-ttu-id="d2c3d-287">예를 들어 앱이 Java 서버를 사용하거나 이전 버전의 ASP.NET SDK를 사용하는 경우 수집 샘플링이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-287">This would work, for example, if your app uses a Java server, or if you are using an older version of the ASP.NET SDK.</span></span>
* <span data-ttu-id="d2c3d-288">ASP.NET SDK 버전 2.0.0 이상을 사용(Azure 또는 자체 서버에 호스트됨)하는 경우 기본적으로 적응 샘플링이지만 위에서 설명한 것처럼 고정 비율 샘플링으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch to fixed-rate as described above.</span></span> <span data-ttu-id="d2c3d-289">고정 비율 샘플링을 사용하면 SDK 브라우저는 자동으로 관련 이벤트를 샘플링하도록 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-289">With fixed-rate sampling, the browser SDK automatically synchronizes to sample related events.</span></span> 

<span data-ttu-id="d2c3d-290">*항상 보고 싶은 확실히 드문 이벤트가 있습니다. 이전의 샘플링 모듈에서 그 이벤트를 어떻게 가져올 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="d2c3d-290">*There are certain rare events I always want to see. How can I get them past the sampling module?*</span></span>

* <span data-ttu-id="d2c3d-291">기본 활성값이 아닌 새 TelemetryConfiguration을 사용하여 별도의 TelemetryClient 인스턴스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not the default Active one).</span></span> <span data-ttu-id="d2c3d-292">이를 사용하여 드문 이벤트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-292">Use that to send your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2c3d-293">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2c3d-293">Next steps</span></span>
* <span data-ttu-id="d2c3d-294">[필터링](app-insights-api-filtering-sampling.md) 은 SDK에서 보내는 항목을 더 엄격하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2c3d-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

