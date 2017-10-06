---
title: "Azure Application Insights에서 aaaTelemetry 샘플링 | Microsoft Docs"
description: "어떻게 tookeep hello 양의 원격 분석 제어 합니다."
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
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="68f58-103">Application Insights의 샘플링</span><span class="sxs-lookup"><span data-stu-id="68f58-103">Sampling in Application Insights</span></span>


<span data-ttu-id="68f58-104">샘플링은 [Azure Application Insights](app-insights-overview.md)의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="68f58-105">이 응용 프로그램 데이터의 올바른 통계적으로 분석을 계속 사용 하면서 방식으로 tooreduce 원격 분석 트래픽 및 저장소를 권장 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="68f58-106">hello 필터 진단 조사를 수행 하는 경우 항목 간을 탐색할 수 있도록 관련 된 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="68f58-107">메트릭 개수 tooyou hello 포털에서 표시 하는 경우 이러한는 구하고 다시 정규화 된의 샘플링의 경우 모든 hello 통계에 영향을 toominimize hello tootake 계정.</span><span class="sxs-lookup"><span data-stu-id="68f58-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="68f58-108">샘플링은 트래픽 및 데이터 비용을 줄여주며 제한을 피하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="68f58-109">개요:</span><span class="sxs-lookup"><span data-stu-id="68f58-109">In brief:</span></span>
* <span data-ttu-id="68f58-110">샘플링에 1 유지  *n*  기록 되 고 hello 나머지를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="68f58-111">예를 들어 20%의 샘플링 속도로 5개의 이벤트 1을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="68f58-112">응용 프로그램이 다양한 원격 분석을 보내는 경우 샘플링은 ASP.NET 웹 서버 앱에서 자동으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="68f58-113">샘플링 중 하나에 hello 수동으로 설정할 수도 있습니다 가격 책정 페이지; hello에 포털 또는 hello.config 파일의 ASP.NET SDK hello에 tooalso는 hello 네트워크 트래픽이 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="68f58-114">사용자 지정 이벤트를 기록 경우 toomake 하는 이벤트 집합이 유지 되는지 아니면 함께 삭제 되었는지 같은 OperationId 값을 hello가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="68f58-115">hello 샘플링 divisor  *n*  hello 속성의 각 레코드에 보고 `itemCount`, 검색에는 hello 이름 "요청 수" 또는 "event count" 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="68f58-116">샘플링이 작업 중이지 않을 때 `itemCount==1`입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="68f58-117">분석 쿼리를 작성하는 경우 [샘플링을 고려](app-insights-analytics-tour.md#counting-sampled-data)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="68f58-118">특히, 레코드를 단순히 세는 대신 `summarize sum(itemCount)`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="68f58-119">샘플링 유형</span><span class="sxs-lookup"><span data-stu-id="68f58-119">Types of sampling</span></span>
<span data-ttu-id="68f58-120">다음은 세 가지 대체 샘플링 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="68f58-121">**적응 샘플링** ASP.NET 응용 프로그램에서 SDK hello에서 전송 하는 원격 분석의 hello 볼륨을 자동으로 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="68f58-122">기본 버전은 SDK v 2.0.0-beta3입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="68f58-123">현재 ASP.NET 서버 측 원격 분석만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="68f58-124">**고정 비율 샘플링** ASP.NET 서버 모두에서 사용자의 브라우저에서 전송 하는 원격 분석의 hello 볼륨을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="68f58-125">Hello 속도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-125">You set hello rate.</span></span> <span data-ttu-id="68f58-126">hello 클라이언트와 서버 동기화의 샘플링 되므로 해당에 검색 관련된 페이지 보기 및 요청 간에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="68f58-127">**수집 샘플링** hello Azure 포털에서에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="68f58-128">설정 하는 속도로 응용 프로그램에서 도착 하는 hello 원격 분석 중 일부를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="68f58-129">원격 분석 트래픽을 줄이지는 않지만 월간 할당량 내로 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="68f58-130">수집 샘플링의 큰 장점은 hello 응용 프로그램을 다시 배포 하지 않고 설정할 수 있습니다 및 모든 서버와 클라이언트에 대 한 균일 하 게 작동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="68f58-131">적응 또는 고정 비율 샘플링이 작업 중인 경우 수집 샘플링은 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="68f58-132">수집 샘플링</span><span class="sxs-lookup"><span data-stu-id="68f58-132">Ingestion sampling</span></span>
<span data-ttu-id="68f58-133">이러한 형태의 샘플링 웹 서버, 브라우저 및 장치에서 원격 분석 hello hello Application Insights 서비스 끝점에 도달 하면 여기서 hello 지점에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="68f58-134">Hello 양을 줄일 수는 있지만 응용 프로그램에서 전송 하는 hello 원격 분석 사용량을 줄이기 위해 하지 않는 것 처리 하 고 보존 (및 유료로 제공) Application Insights에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="68f58-135">이러한 종류의 샘플링을 사용 하 여 앱 월별 할당량을 초과 자주 초과 샘플링의 hello SDK 기반 유형 중 하나를 사용 하 여 hello 옵션이 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="68f58-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="68f58-136">Hello 샘플링 속도 hello 할당량 및 가격 책정 블레이드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Hello 응용 프로그램 개요 블레이드에서 샘플링 주기, 설정, 할당량, 샘플를 클릭 한 다음 선택한 업데이트를 클릭 합니다.](./media/app-insights-sampling/04.png)

<span data-ttu-id="68f58-138">다른 종류의 샘플링와 마찬가지로 hello 알고리즘 관련된 원격 분석 항목을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="68f58-139">예를 들어 검색의 hello 원격 분석을 검사 하려는 경우 수 toofind hello 요청과 관련 tooa 특정 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="68f58-140">요청 빈도 및 예외 처리 빈도와 같은 메트릭 수는 올바르게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="68f58-141">샘플링에서 무시된 데이터 요소는 [연속 내보내기](app-insights-export-telemetry.md)와 같은 Application Insights 기능에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="68f58-142">SDK 기반 적응 또는 고정 비율 샘플링이 작동되는 동안에는 수집 샘플링이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="68f58-143">100% 보다 작은 hello SDK hello 샘플링 비율을 사용 하는 경우 다음 hello 설정한 수집 샘플링 속도 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="68f58-144">hello 타일에 표시 된 hello 값 수집 샘플링에 대해 설정한 hello 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="68f58-145">샘플링 SDK가 작동 하는 경우 hello 실제 샘플링 속도 이므로 나타낼 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="68f58-146">웹 서버의 적응 샘플링</span><span class="sxs-lookup"><span data-stu-id="68f58-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="68f58-147">적응 샘플링 hello Application Insights SDK v 2.0.0-beta3 ASP.NET 및 이후 버전에 대해 사용할 수 있으며 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="68f58-148">적응 샘플링 hello 볼륨을 웹 서버 응용 프로그램 toohello Application Insights 서비스에서에서 보낸 원격 분석의 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="68f58-149">hello 볼륨은 자동으로 조정 tookeep 트래픽의 지정 된 최대 속도로 내에서.</span><span class="sxs-lookup"><span data-stu-id="68f58-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="68f58-150">적은 양의 원격 분석에서는 작동하지 않으므로 사용량이 적은 웹 사이트 또는 디버그 중인 앱은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="68f58-151">생성 된 hello 원격 분석 중 일부 tooachieve hello 대상 볼륨 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="68f58-152">하지만 다른 형식의 샘플링의 경우와 마찬가지로 hello 알고리즘 관련된 원격 분석 항목을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="68f58-153">예를 들어 검색의 hello 원격 분석을 검사 하려는 경우 수 toofind hello 요청과 관련 tooa 특정 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="68f58-154">메트릭 또는 같은 요청 속도 예외 비율 샘플링 주기, hello에 대 한 조정 된 toocompensate 메트릭 탐색기에서 올바른 약 값 표시 되도록를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="68f58-155">**프로젝트의 NuGet 업데이트** toohello를 최신 패키지 *시험판* 버전의 Application Insights: hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭, NuGet 패키지 관리 선택 확인 **포함 시험판** Microsoft.ApplicationInsights.Web으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="68f58-156">[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), hello에 여러 매개 변수를 조정할 수 있습니다 `AdaptiveSamplingTelemetryProcessor` 노드.</span><span class="sxs-lookup"><span data-stu-id="68f58-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="68f58-157">표시 된 hello 수치 hello 기본값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="68f58-158">hello 적응 알고리즘 hello 대상 비율 목표에 대 한 **각 서버 호스트에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="68f58-159">웹 앱에서는 많은 호스트에서 실행 하는 경우이 값을 따라서 hello Application Insights 포털에서 트래픽 속도가 대상 내에서 tooremain으로 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="68f58-160">hello 간격을 현재 속도입니다. 원격 분석에는 hello 다시 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="68f58-161">평가는 이동 평균으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="68f58-162">원격 분석은 책임 toosudden 급증 하는 경우이 간격은 tooshorten 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="68f58-163">샘플링 백분율 값을 얼마나 빨리 후 변경이 경우 데이터를 적게 toocapture 백분율을 다시 샘플링 toolower 허용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="68f58-164">샘플링 백분율 값을 얼마나 빨리 후 변경이 म 허용 백분율을 다시 샘플링 tooincrease toocapture 더 많은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="68f58-165">Hello 최소값 비율 샘플링 변경 됨에 따라 란 tooset 허용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="68f58-166">Hello 최 댓 값 이란 비율 샘플링 변경 됨에 따라 tooset 허용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="68f58-167">이동 평균 hello hello 계산을 hello 가중치 toohello 최신 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="68f58-168">1 보다 작은 값 같은 tooor를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="68f58-169">Hello 알고리즘 덜 사후 toosudden 변경을 수행 하는 값이 작을수록 하십시오.</span><span class="sxs-lookup"><span data-stu-id="68f58-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="68f58-170">hello 앱만 시작 될 때 할당 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="68f58-171">디버깅하는 동안 이 값을 줄이지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="68f58-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="68f58-172">세미콜론으로 구분한 목록 toobe 샘플링 하지 않으려면 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="68f58-173">인식되는 형식: 종속성, 이벤트, 예외, 페이지 보기, 요청, 추적</span><span class="sxs-lookup"><span data-stu-id="68f58-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="68f58-174">Hello의 모든 인스턴스를 지정 된 형식을 전송 됩니다. 지정 되지 않은 hello 형식 샘플링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="68f58-175">샘플링 toobe 원하는 형식의 세미콜론으로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="68f58-176">인식되는 형식: 종속성, 이벤트, 예외, 페이지 보기, 요청, 추적</span><span class="sxs-lookup"><span data-stu-id="68f58-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="68f58-177">hello 지정 형식을 샘플링 됩니다. 모든 인스턴스 hello의 유형도 항상 전송 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="68f58-178">**off tooswitch** 적응 샘플링을 applicationinsights-config에서 hello AdaptiveSamplingTelemetryProcessor 노드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="68f58-179">대체: 코드에서 적응 샘플링 구성</span><span class="sxs-lookup"><span data-stu-id="68f58-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="68f58-180">Hello.config 파일의 샘플링을 조정 하는 대신 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="68f58-181">그러면 toospecify hello 샘플링 비율을 다시 평가할 때마다 호출 되는 콜백 함수.</span><span class="sxs-lookup"><span data-stu-id="68f58-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="68f58-182">사용할 수 있습니다, 샘플링 속도 아웃 toofind 사용량 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="68f58-183">Hello 제거 `AdaptiveSamplingTelemetryProcessor` hello.config 파일에서 노드.</span><span class="sxs-lookup"><span data-stu-id="68f58-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="68f58-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="68f58-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

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
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="68f58-185">([원격 분석 프로세서에 대해 알아봅니다](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="68f58-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="68f58-186">JavaScript를 사용하는 웹 페이지에 대한 샘플링</span><span class="sxs-lookup"><span data-stu-id="68f58-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="68f58-187">서버에서 고정 비율 샘플링에 대한 웹 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="68f58-188">때 있습니다 [Application Insights에 대 한 hello 웹 페이지 구성](app-insights-javascript.md), hello Application Insights 포털에서 얻을 수 있는 hello 조각 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="68f58-189">(ASP.NET 응용 프로그램에서 hello 조각은 일반적으로에 포함할지 _Layout.cshtml.)  같은 줄을 삽입 `samplingPercentage: 10,` hello 계측 키 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="68f58-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

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

<span data-ttu-id="68f58-190">Hello 샘플링 비율에 대 한 백분율을 닫기 too100/N 여기서 N은 정수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="68f58-191">현재 샘플링은 다른 값을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="68f58-192">Hello 서버에서 고정 비율 샘플링 사용 하면, 해당에 검색 관련된 페이지 보기 및 요청 간에 탐색할 수 있도록 hello 클라이언트와 서버 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="68f58-193">ASP.NET 웹 사이트에 대한 고정 비율 샘플링</span><span class="sxs-lookup"><span data-stu-id="68f58-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="68f58-194">웹 서버와 웹 브라우저에서 전송 하는 hello 트래픽이 감소 하는 고정된 비율 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="68f58-195">적응 샘플링과 달리 사용자가 결정한 고정 비율로 원격 분석을 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="68f58-196">것도 동기화 hello 클라이언트와 서버 샘플링 하므로 관련된 항목의 보존-예를 들어 검색에서 페이지 보기를 보면 관련된 요청을 찾을 수 있습니다 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="68f58-197">hello 샘플링 알고리즘 관련된 항목을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="68f58-198">각 HTTP 요청 이벤트에 대해 해당 이벤트와 관련 이벤트가 삭제되거나 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="68f58-199">메트릭 탐색기에서 예외 및 요청 수 같은 속도 곱할 hello 샘플링 속도 대 한 계수 toocompensate 약 올바른 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="68f58-200">**프로젝트의 NuGet 패키지를 업데이트** toohello 최신 *시험판* Application Insights의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="68f58-201">솔루션 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭, NuGet 패키지 관리 선택 확인 **시험판 포함** Microsoft.ApplicationInsights.Web으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="68f58-202">**적응 샘플링을 사용 하지 않도록 설정**:에서 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), 제거 하거나 주석으로 hello `AdaptiveSamplingTelemetryProcessor` 노드.</span><span class="sxs-lookup"><span data-stu-id="68f58-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="68f58-203">**Hello 고정 비율 샘플링 모듈을 사용 하도록 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="68f58-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="68f58-204">이 코드 조각이 너무 추가[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="68f58-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="68f58-205">Hello 샘플링 비율에 대 한 백분율을 닫기 too100/N 여기서 N은 정수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="68f58-206">현재 샘플링은 다른 값을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="68f58-207">대체: 서버 코드에서 고정 비율 샘플링을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="68f58-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="68f58-208">Hello.config 파일의 hello 샘플링 매개 변수를 설정 하는 대신 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="68f58-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="68f58-209">*C#*</span></span>

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

<span data-ttu-id="68f58-210">([원격 분석 프로세서에 대해 알아봅니다](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="68f58-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="68f58-211">때 toouse 샘플링?</span><span class="sxs-lookup"><span data-stu-id="68f58-211">When toouse sampling?</span></span>
<span data-ttu-id="68f58-212">ASP.NET SDK 버전 2.0.0-beta3 hello를 사용 하는 경우 적응 샘플링 자동으로 활성화 이상.</span><span class="sxs-lookup"><span data-stu-id="68f58-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="68f58-213">사용하는 SDK 버전에 상관없이 서버에서 수집 샘플링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="68f58-214">대부분의 중소 응용 프로그램은 샘플링하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="68f58-215">hello 가장 유용한 진단 정보와 가장 정확한 통계는 모든 사용자 활동에서 데이터를 수집 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="68f58-216">hello 샘플링의 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="68f58-217">앱이 짧은 시간 간격으로 매우 높은 비율의 원격 분석을 전송할 때 Application Insights 서비스는 ("제한") 데이터 요소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="68f58-218">hello 내 tookeep [할당량](app-insights-pricing.md) 의 가격 책정 계층에 대 한 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="68f58-219">원격 분석의 hello 컬렉션에서 tooreduce 네트워크 트래픽</span><span class="sxs-lookup"><span data-stu-id="68f58-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="68f58-220">어떤 유형의 샘플링을 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="68f58-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="68f58-221">**다음과 같은 경우 수집 샘플링을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="68f58-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="68f58-222">원격 분석의 월간 할당량을 자주 초과하는 경우</span><span class="sxs-lookup"><span data-stu-id="68f58-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="68f58-223">2 이전 hello 샘플링-예를 지원 하지 않는 SDK, hello Java SDK 또는 ASP.NET 버전의 버전을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="68f58-224">사용자의 웹 브라우저에서 많은 원격 분석이 전송되는 경우</span><span class="sxs-lookup"><span data-stu-id="68f58-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="68f58-225">**다음과 같은 경우 고정 비율 샘플링을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="68f58-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="68f58-226">ASP.NET 웹 서비스 버전 2.0.0 hello Application Insights SDK를 사용 하는 이후 버전 및</span><span class="sxs-lookup"><span data-stu-id="68f58-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="68f58-227">원하는 클라이언트와 서버 간에 동기화 된 샘플링의 이벤트를 조사 하려는 경우 있도록 [검색](app-insights-diagnostic-search.md), hello 클라이언트에서 관련된 이벤트 및 페이지 보기 및 http 요청 등 서버 간에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="68f58-228">확신할 hello 적절 한 샘플링 비율의 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="68f58-229">충분히 높은 tooget 정확한 메트릭을 하지만 아래 hello 가격의 할당량을 초과 하는 속도 hello 조절 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="68f58-230">**다음과 같은 경우 적응 샘플링을 사용합니다.**</span><span class="sxs-lookup"><span data-stu-id="68f58-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="68f58-231">그렇지 않은 경우 적응 샘플링을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="68f58-232">이 기능은 hello ASP.NET 서버 SDK, 2.0.0-beta3 버전에서는 기본적으로 사용 이상.</span><span class="sxs-lookup"><span data-stu-id="68f58-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="68f58-233">특정 최소 속도까지 트래픽을 줄이지 않으므로 사용량이 적은 사이트에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="68f58-234">샘플링이 작업 중인지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="68f58-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="68f58-235">실제 toodiscover hello 샘플링 속도 적용 한에 관계 없이 사용 하 여 프로그램 [분석 쿼리에서](app-insights-analytics.md) 이와 같은:</span><span class="sxs-lookup"><span data-stu-id="68f58-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="68f58-236">각 레코드를 유지 `itemCount` hello 원래 레코드 수를 나타내는 것 같으면 too1 + 이전 레코드는 삭제 된 hello 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="68f58-237">샘플링은 어떻게 작동되나요?</span><span class="sxs-lookup"><span data-stu-id="68f58-237">How does sampling work?</span></span>
<span data-ttu-id="68f58-238">고정 속도 및 적응 샘플링은 2.0.0부터에서 ASP.NET 버전 hello SDK의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="68f58-239">수집 샘플링 hello Application Insights 서비스의 기능이 며 hello SDK에서 샘플링을 수행 하지 않는 경우 작업에서 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="68f58-240">hello 샘플링 알고리즘을 원격 분석 항목 toodrop 및 어떤 경우라 tookeep (인지 hello SDK 또는 hello Application Insights 서비스)를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="68f58-241">hello 샘플링 의사 결정 toopreserve 모든 서로 관련 된 데이터 요소를 실행 하 고 축소 된 데이터 집합 된 경우에 신뢰할 수 있는 Application Insights에서 진단 환경을 유지 관리 그대로 유지를 목표로 하는 몇 가지 규칙을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="68f58-242">예를 들어 실패한 요청의 경우 앱이 추가 원격 분석 항목을 전송하면(예: 해당 요청에서 기록된 예외 및 추적) 샘플링은 해당 요청 및 기타 원격 분석을 분할하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="68f58-243">전체를 유지하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="68f58-244">결과적으로, Application Insights에서 hello 요청 세부 정보를 볼 때에 항상 보고서 항목과 연결 된 원격 분석 항목 함께 hello 요청을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="68f58-245">"User"를 정의 하는 응용 프로그램에 대 한 (즉, 가장 일반적인 웹 응용 프로그램), 즉, 특정 사용자에 대 한 모든 원격 분석은 유지 없거나 삭제 hello 사용자 id의 hello 해시를 기반으로 하는 hello 샘플링 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="68f58-246">Hello 유형의 사용자 (예: 웹 서비스)를 정의 하지 않은 응용 프로그램에 대 한 hello 샘플링 의사 결정은 hello 요청의 hello 작업 id를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="68f58-247">마지막으로, (항목에 대 한 예에서는 원격 분석 http 컨텍스트가 없는 비동기 스레드에서 보고) 설정 하는 사용자와 작업 id를도 hello 원격 분석 항목에 대 한 샘플링 간단히 파악 각 유형의 원격 분석 항목의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="68f58-248">원격 분석 백 tooyou를 표시할 때 hello Application Insights 서비스 조정 하 여 hello 메트릭 hello toocompensate hello 누락 된 데이터 요소에 대 한 컬렉션의 hello 시간에 사용 된 동일한 샘플링 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="68f58-249">따라서 Application Insights의 hello 원격 분석을 살펴볼 때는 hello 사용자가 매우 가까운 toohello 실수 있는 올바른 통계적으로 어림 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="68f58-250">hello 근사값의 hello 정확도 대부분 hello 구성 샘플링 비율에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="68f58-251">또한 많은 양의 다양 한 사용자에서에서 일반적으로 유사한 요청을 처리 하는 응용 프로그램에 대 한 hello 정확도 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="68f58-252">에 상당한 부하를 사용 하지 않는 응용 프로그램에 대 한 다른 손 hello, 이러한 응용 프로그램 수 hello 할당량 제한에서 데이터 손실이 발생 하지 않고 이내로 자신의 모든 원격 분석을 전송 일반적으로 샘플링은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="68f58-253">Note Application Insights 샘플링 하지 메트릭 및 세션 원격 분석 유형을 이후에 이러한 형식에 대 한, 감소 hello 정밀도에 방해가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="68f58-254">적응 샘플링</span><span class="sxs-lookup"><span data-stu-id="68f58-254">Adaptive sampling</span></span>
<span data-ttu-id="68f58-255">적응 샘플링 hello SDK에서에서 해당 모니터 hello 현재 속도입니다. 전송 구성 요소를 추가 하 고 hello 샘플링 비율 tootry toostay 내 hello 대상 최대 속도 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="68f58-256">hello 조정 정기적으로 다시 계산 및 전송 속도 나가는 hello의 이동 평균을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="68f58-257">샘플링 및 hello JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="68f58-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="68f58-258">서버 쪽 hello와 함께에서 고정 비율 샘플링에 참여 하는 hello 클라이언트 쪽 (JavaScript) SDK SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="68f58-259">hello 계측 페이지에서 동일한 사용자에는 hello에 대 한 서버 쪽 결정 해당 너무 "sample에." hello만 클라이언트 쪽 원격 분석을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="68f58-260">이 논리는 디자인 된 toomaintain 무결성 사용자 세션을 통해 클라이언트-및 서버-면입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="68f58-261">결과적으로 Application Insights의 특정 원격 분석 항목에서 해당 사용자 또는 세션에 대한 다른 모든 원격 분석 항목을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="68f58-262">*위에 설명한 대로 내 클라이언트 및 서버 측 원격 분석은 조정된 샘플을 표시하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="68f58-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="68f58-263">서버 및 클라이언트 모두에서 고정 비율 샘플링을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="68f58-264">해당 hello SDK 버전 2.0 인지 확인 이상.</span><span class="sxs-lookup"><span data-stu-id="68f58-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="68f58-265">설정 하는 검사 hello 같은 hello 클라이언트와 서버 모두에서 비율 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="68f58-266">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="68f58-266">Frequently Asked Questions</span></span>
<span data-ttu-id="68f58-267">*샘플링은 왜 간단히 "각 원격 분석 형식의 X 퍼센트를 수집"하지 않습니까?*</span><span class="sxs-lookup"><span data-stu-id="68f58-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="68f58-268">이 샘플링 방법을 사용 메트릭 어림 값의 자릿수가 매우 높은 제공 하는 사용자, 세션 및 요청 진단에 대 한 중요 한 당 기능 toocorrelate 진단 데이터 끊어지기 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="68f58-269">따라서 샘플링은 "앱 사용자의 X 퍼센트에 대해 모든 원격 분석 항목 수집" 또는 "앱 요청의 X퍼센트에 대한 모든 원격 분석 수집" 논리를 사용하여 더 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="68f58-270">Hello 요청 (예: 백그라운드 비동기 처리)와 연관 되지 않은 hello 원격 분석 항목에 대 한 hello 년으로 돌아가는 것은 너무 "수집 각 원격 분석 형식에 대 한 모든 항목의 %X."</span><span class="sxs-lookup"><span data-stu-id="68f58-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="68f58-271">*Hello 샘플링 백분율 시간이 지나면서 달라질 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="68f58-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="68f58-272">예, 적응 샘플링 점진적으로 현재 hello 원격 분석의 볼륨을 관찰 하는 hello에 따라 hello 샘플링 비율을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="68f58-273">*고정 비율 샘플링을 사용 하는 경우 어떻게 알 수 있는 샘플링 비율 작동할지 hello 내 앱에 대 한 최상의?*</span><span class="sxs-lookup"><span data-stu-id="68f58-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="68f58-274">한 가지 방법은 toostart 적응 샘플링,에 settles 비율 기능에 대해 알아봅니다 (위 질문 hello 참조) 및 스위치 toofixed 속도 비율을 사용 하 여 다음을 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="68f58-275">그렇지 않으면, tooguess를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="68f58-276">즉 발생 하 고 예상 hello 양의 원격 분석 수집 hello 제한을 눈를 AI에서 현재 원격 분석 사용량을 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="68f58-277">선택한 가격 책정 계층을 함께 이러한 세 개의 입력을 얼마나 tooreduce hello 양의 원격 분석 수집 hello 할 수 있습니다 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="68f58-278">그러나 hello 사용자 수가 증가 또는 일부 다른 시프트 hello 볼륨 원격 분석의 추정치를 무효화 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="68f58-279">*샘플링 비율을 너무 낮게 구성하는 경우 어떻게 됩니까?*</span><span class="sxs-lookup"><span data-stu-id="68f58-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="68f58-280">Application Insights 시도 hello 데이터 볼륨 축소에 대 한 hello 데이터의 toocompensate hello 시각화 하는 경우 지나치게 낮다고 샘플링 비율 (지나친 샘플링) hello 어림 값의 hello 정확도를 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="68f58-281">또한 진단 환경을 부정적인 영향을 받을 수, 일부 자주 실패 하는 hello로 또는 느린 요청 아웃 샘플링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="68f58-282">*샘플링 비율을 너무 높게 구성하는 경우 어떻게 됩니까?*</span><span class="sxs-lookup"><span data-stu-id="68f58-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="68f58-283">원격 분석을 수집 하는 hello 볼륨 hello의 부족 하 여 감소는에서 너무 높게 샘플링 비율 (하지 적극적인 충분히) 결과 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="68f58-284">원격 분석 데이터 손실을 toothrottling와 Application Insights를 사용 하 여 hello 비용 인해 toooverage 요금 계획 된 것 보다 더 높을 수와 관련 된 여전히 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="68f58-285">*샘플링을 어떤 플랫폼에서 사용할 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="68f58-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="68f58-286">수집 샘플링 hello SDK에서 샘플링을 수행 하지 않는 경우 특정 볼륨, 위의 모든 원격 분석을 위한 자동으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="68f58-287">이 작동할 것, 예를 들어 앱 Java 서버를 사용 하거나 이전 버전의 ASP.NET SDK hello 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="68f58-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="68f58-288">ASP.NET SDK 버전 2.0.0을 사용 하 여 이상 (자체 서버 또는 Azure에서 호스팅), 기본적으로 샘플링 적응 얻을 수 있지만 위에 설명 된 대로 toofixed 속도 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="68f58-289">고정 비율 샘플링으로 hello 브라우저 SDK를 자동으로 동기화 toosample 관련 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="68f58-290">*드문 이벤트 toosee 항상 원하는 것은 아닙니다. 어떻게 확인할 수 있 습에 hello 샘플링 모듈을 지 나?*</span><span class="sxs-lookup"><span data-stu-id="68f58-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="68f58-291">새 TelemetryConfiguration (hello 기본값이 아닌 활성)와 TelemetryClient의 별도 인스턴스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="68f58-292">해당 toosend 드문 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f58-293">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68f58-293">Next steps</span></span>
* <span data-ttu-id="68f58-294">[필터링](app-insights-api-filtering-sampling.md) 은 SDK에서 보내는 항목을 더 엄격하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f58-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

