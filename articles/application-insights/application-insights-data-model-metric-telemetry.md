---
title: "응용 프로그램 Insights 원격 분석 데이터 모델-aaaAzure 메트릭 원격 분석 | Microsoft Docs"
description: "메트릭 원격 분석을 위한 Azure Application Insights 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a><span data-ttu-id="8136d-103">메트릭 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="8136d-103">Metric telemetry: Application Insights data model</span></span>

<span data-ttu-id="8136d-104">[Application Insights](app-insights-overview.md)에서 지원하는 메트릭 원격 분석에는 두 가지 유형, 즉 단일 측정 및 미리 집계된 메트릭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-104">There are two types of metric telemetry supported by [Application Insights](app-insights-overview.md): single measurement and pre-aggregated metric.</span></span> <span data-ttu-id="8136d-105">단일 측정은 이름 및 값만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-105">Single measurement is just a name and value.</span></span> <span data-ttu-id="8136d-106">미리 집계 된 메트릭 hello 집계 간격 및의 표준 편차 hello 메트릭의 최소 및 최대 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-106">Pre-aggregated metric specifies minimum and maximum value of hello metric in hello aggregation interval and standard deviation of it.</span></span>

<span data-ttu-id="8136d-107">미리 집계된 메트릭 원격 분석은 집계 기간을 1분으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-107">Pre-aggregated metric telemetry assumes that aggregation period was one minute.</span></span>

<span data-ttu-id="8136d-108">Application Insights에서는 잘 알려진 몇 가지 메트릭 이름을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-108">There are several well-known metric names supported by Application Insights.</span></span> 

<span data-ttu-id="8136d-109">시스템 및 프로세스 카운터를 나타내는 메트릭:</span><span class="sxs-lookup"><span data-stu-id="8136d-109">Metric representing system and process counters:</span></span>

| <span data-ttu-id="8136d-110">**.NET 이름**</span><span class="sxs-lookup"><span data-stu-id="8136d-110">**.NET name**</span></span>             | <span data-ttu-id="8136d-111">**플랫폼 독립적 이름**</span><span class="sxs-lookup"><span data-stu-id="8136d-111">**Platform agnostic name**</span></span> | <span data-ttu-id="8136d-112">**REST API 이름**</span><span class="sxs-lookup"><span data-stu-id="8136d-112">**REST API name**</span></span> | <span data-ttu-id="8136d-113">**설명**</span><span class="sxs-lookup"><span data-stu-id="8136d-113">**Description**</span></span>
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | <span data-ttu-id="8136d-114">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-114">Work in progress...</span></span> | [<span data-ttu-id="8136d-115">processorCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="8136d-115">processorCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | <span data-ttu-id="8136d-116">총 컴퓨터 CPU</span><span class="sxs-lookup"><span data-stu-id="8136d-116">total machine CPU</span></span>
| `\Memory\Available Bytes`                 | <span data-ttu-id="8136d-117">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-117">Work in progress...</span></span> | [<span data-ttu-id="8136d-118">memoryAvailableBytes</span><span class="sxs-lookup"><span data-stu-id="8136d-118">memoryAvailableBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | <span data-ttu-id="8136d-119">디스크의 사용 가능한 메모리</span><span class="sxs-lookup"><span data-stu-id="8136d-119">memory available on disk</span></span>
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | <span data-ttu-id="8136d-120">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-120">Work in progress...</span></span> | [<span data-ttu-id="8136d-121">processCpuPercentage</span><span class="sxs-lookup"><span data-stu-id="8136d-121">processCpuPercentage</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | <span data-ttu-id="8136d-122">Hello 응용 프로그램을 호스트 하는 hello 프로세스의 CPU</span><span class="sxs-lookup"><span data-stu-id="8136d-122">CPU of hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | <span data-ttu-id="8136d-123">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-123">Work in progress...</span></span> | [<span data-ttu-id="8136d-124">processPrivateBytes</span><span class="sxs-lookup"><span data-stu-id="8136d-124">processPrivateBytes</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | <span data-ttu-id="8136d-125">hello 응용 프로그램을 호스트 하는 hello 프로세스에서 사용 하는 메모리</span><span class="sxs-lookup"><span data-stu-id="8136d-125">memory used by hello process hosting hello application</span></span>
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | <span data-ttu-id="8136d-126">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-126">Work in progress...</span></span> | [<span data-ttu-id="8136d-127">processIOBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8136d-127">processIOBytesPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | <span data-ttu-id="8136d-128">hello 응용 프로그램을 호스팅하는 프로세스에 의해 실행 되는 I/O 작업 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-128">rate of I/O operations runs by process hosting hello application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | <span data-ttu-id="8136d-129">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-129">Work in progress...</span></span> | [<span data-ttu-id="8136d-130">requestsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8136d-130">requestsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | <span data-ttu-id="8136d-131">응용 프로그램에서 처리되는 요청 속도</span><span class="sxs-lookup"><span data-stu-id="8136d-131">rate of requests processed by application</span></span> 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | <span data-ttu-id="8136d-132">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-132">Work in progress...</span></span> | [<span data-ttu-id="8136d-133">exceptionsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8136d-133">exceptionsPerSecond</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | <span data-ttu-id="8136d-134">응용 프로그램에서 throw하는 예외 속도</span><span class="sxs-lookup"><span data-stu-id="8136d-134">rate of exceptions thrown by application</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | <span data-ttu-id="8136d-135">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-135">Work in progress...</span></span> | [<span data-ttu-id="8136d-136">requestExecutionTime</span><span class="sxs-lookup"><span data-stu-id="8136d-136">requestExecutionTime</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | <span data-ttu-id="8136d-137">평균 요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="8136d-137">average requests execution time</span></span>
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | <span data-ttu-id="8136d-138">진행 중인 작업...</span><span class="sxs-lookup"><span data-stu-id="8136d-138">Work in progress...</span></span> | [<span data-ttu-id="8136d-139">requestsInQueue</span><span class="sxs-lookup"><span data-stu-id="8136d-139">requestsInQueue</span></span>](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | <span data-ttu-id="8136d-140">큐에 처리 하는 hello에 대 한 대기 중인 요청 수</span><span class="sxs-lookup"><span data-stu-id="8136d-140">number of requests waiting for hello processing in a queue</span></span>

## <a name="name"></a><span data-ttu-id="8136d-141">이름</span><span class="sxs-lookup"><span data-stu-id="8136d-141">Name</span></span>

<span data-ttu-id="8136d-142">이름 hello 메트릭의 Application Insights 포털와 UI에 toosee 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-142">Name of hello metric you'd like toosee in Application Insights portal and UI.</span></span> 

## <a name="value"></a><span data-ttu-id="8136d-143">값</span><span class="sxs-lookup"><span data-stu-id="8136d-143">Value</span></span>

<span data-ttu-id="8136d-144">단일 측정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-144">Single value for measurement.</span></span> <span data-ttu-id="8136d-145">Hello 집계에 대 한 개별 측정값의 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-145">Sum of individual measurements for hello aggregation.</span></span>

## <a name="count"></a><span data-ttu-id="8136d-146">개수</span><span class="sxs-lookup"><span data-stu-id="8136d-146">Count</span></span>

<span data-ttu-id="8136d-147">집계 hello 메트릭의 메트릭 가중치입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-147">Metric weight of hello aggregated metric.</span></span> <span data-ttu-id="8136d-148">측정값에 대해서는 설정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-148">Should not be set for a measurement.</span></span>

## <a name="min"></a><span data-ttu-id="8136d-149">Min</span><span class="sxs-lookup"><span data-stu-id="8136d-149">Min</span></span>

<span data-ttu-id="8136d-150">Hello 집계 메트릭의 최소값입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-150">Minimum value of hello aggregated metric.</span></span> <span data-ttu-id="8136d-151">측정값에 대해서는 설정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-151">Should not be set for a measurement.</span></span>

## <a name="max"></a><span data-ttu-id="8136d-152">max</span><span class="sxs-lookup"><span data-stu-id="8136d-152">Max</span></span>

<span data-ttu-id="8136d-153">Hello 집계 메트릭의 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-153">Maximum value of hello aggregated metric.</span></span> <span data-ttu-id="8136d-154">측정값에 대해서는 설정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-154">Should not be set for a measurement.</span></span>

## <a name="standard-deviation"></a><span data-ttu-id="8136d-155">표준 편차</span><span class="sxs-lookup"><span data-stu-id="8136d-155">Standard deviation</span></span>

<span data-ttu-id="8136d-156">Hello의 표준 편차 메트릭을 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-156">Standard deviation of hello aggregated metric.</span></span> <span data-ttu-id="8136d-157">측정값에 대해서는 설정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-157">Should not be set for a measurement.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="8136d-158">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="8136d-158">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="8136d-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8136d-159">Next steps</span></span>

- <span data-ttu-id="8136d-160">자세한 내용은 방법 toouse [사용자 지정 이벤트 및 메트릭을 대 한 Application Insights API](app-insights-api-custom-events-metrics.md#trackmetric)합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-160">Learn how toouse [Application Insights API for custom events and metrics](app-insights-api-custom-events-metrics.md#trackmetric).</span></span>
- <span data-ttu-id="8136d-161">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8136d-161">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="8136d-162">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8136d-162">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
