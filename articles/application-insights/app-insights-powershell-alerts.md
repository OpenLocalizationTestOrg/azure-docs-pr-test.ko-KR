---
title: "PowerShell을 사용하여 Application Insights에서 경고 설정 | Microsoft Docs"
description: "Application Insights의 구성을 자동화하여 메트릭 변경 사항에 대한 전자 메일을 받습니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="a969e-103">PowerShell을 사용하여 Application Insights에서 경고 설정</span><span class="sxs-lookup"><span data-stu-id="a969e-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="a969e-104">[Application Insights](app-insights-overview.md)에서 [경고](app-insights-alerts.md)의 구성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="a969e-105">또한 [webhook를 설정하여 경고에 대한 응답을 자동화](../monitoring-and-diagnostics/insights-webhooks-alerts.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a969e-106">리소스와 경고를 동시에 만들려면 [Azure Resource Manager 템플릿을 사용](app-insights-powershell.md)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="a969e-107">일 회 설정</span><span class="sxs-lookup"><span data-stu-id="a969e-107">One-time setup</span></span>
<span data-ttu-id="a969e-108">아직 Azure 구독에서 PowerShell을 사용한 적이 없을 경우:</span><span class="sxs-lookup"><span data-stu-id="a969e-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="a969e-109">스크립트를 실행하려는 컴퓨터에 Azure Powershell 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="a969e-110">[Microsoft 웹 플랫폼 설치 관리자(v5 이상)](http://www.microsoft.com/web/downloads/platform.aspx)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="a969e-111">이를 사용하여 Microsoft Azure Powershell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="a969e-112">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="a969e-112">Connect to Azure</span></span>
<span data-ttu-id="a969e-113">Azure PowerShell을 시작하고 [구독에 연결](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="a969e-114">경고 받기</span><span class="sxs-lookup"><span data-stu-id="a969e-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="a969e-115">경고 추가</span><span class="sxs-lookup"><span data-stu-id="a969e-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="a969e-116">예 1</span><span class="sxs-lookup"><span data-stu-id="a969e-116">Example 1</span></span>
<span data-ttu-id="a969e-117">HTTP 요청에 대한 서버의 응답이 5분 이상 평균 1초보다 느린 경우 전자 메일로 알립니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="a969e-118">Application Insights 리소스의 이름이 IceCreamWebApp이며 리소스 그룹 Fabrikam 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="a969e-119">제가 Azure 구독의 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="a969e-120">GUID는 구독 ID입니다(응용 프로그램의 계측 키 아님).</span><span class="sxs-lookup"><span data-stu-id="a969e-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="a969e-121">예 2</span><span class="sxs-lookup"><span data-stu-id="a969e-121">Example 2</span></span>
<span data-ttu-id="a969e-122">[TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric)을 사용하여 "salesPerHour"라는 메트릭을 보고하는 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="a969e-123">24시간 이상 평균 "salesPerHour"가 100 미만으로 떨어지는 경우 동료에게 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="a969e-124">TrackEvent 또는 trackPageView와 같은 다른 추적 호출의 [측정 매개 변수](app-insights-api-custom-events-metrics.md#properties) 를 사용하여 보고된 메트릭에도 동일한 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="a969e-125">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="a969e-125">Metric names</span></span>
| <span data-ttu-id="a969e-126">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="a969e-126">Metric name</span></span> | <span data-ttu-id="a969e-127">화면 이름</span><span class="sxs-lookup"><span data-stu-id="a969e-127">Screen name</span></span> | <span data-ttu-id="a969e-128">설명</span><span class="sxs-lookup"><span data-stu-id="a969e-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="a969e-129">브라우저 예외</span><span class="sxs-lookup"><span data-stu-id="a969e-129">Browser exceptions</span></span> |<span data-ttu-id="a969e-130">브라우저에서 발생한 확인할 수 없는 예외의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="a969e-131">서버 예외</span><span class="sxs-lookup"><span data-stu-id="a969e-131">Server exceptions</span></span> |<span data-ttu-id="a969e-132">앱에서 발생한 처리되지 않은 예외의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="a969e-133">클라이언트 처리 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-133">Client processing time</span></span> |<span data-ttu-id="a969e-134">DOM을 로드할 때부터 문서의 마지막 바이트를 받는 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="a969e-135">비동기 요청은 계속 처리 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="a969e-136">페이지 로드 네트워크 연결 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-136">Page load network connect time</span></span> |<span data-ttu-id="a969e-137">브라우저가 네트워크에 연결하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="a969e-138">캐시된 경우 0일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="a969e-139">응답 수신 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-139">Receiving response time</span></span> |<span data-ttu-id="a969e-140">브라우저가 요청을 보내서 응답을 받기 시작하는 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="a969e-141">요청 전송 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-141">Send request time</span></span> |<span data-ttu-id="a969e-142">브라우저가 요청을 보내는 데 소요된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="a969e-143">브라우저 페이지 로드 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-143">Browser page load time</span></span> |<span data-ttu-id="a969e-144">사용자가 요청한 때부터 DOM, 스타일시트, 스크립트 및 이미지가 로드될 때까지 소요된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="a969e-145">사용 가능한 메모리</span><span class="sxs-lookup"><span data-stu-id="a969e-145">Available memory</span></span> |<span data-ttu-id="a969e-146">처리를 위해서나 시스템에서 바로 사용할 수 있는 실제 메모리입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="a969e-147">프로세스 IO 속도</span><span class="sxs-lookup"><span data-stu-id="a969e-147">Process IO Rate</span></span> |<span data-ttu-id="a969e-148">파일, 네트워크 및 장치에서 읽고 쓴 초당 총 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="a969e-149">예외 속도</span><span class="sxs-lookup"><span data-stu-id="a969e-149">exception rate</span></span> |<span data-ttu-id="a969e-150">초당 발생한 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="a969e-151">CPU 프로세스</span><span class="sxs-lookup"><span data-stu-id="a969e-151">Process CPU</span></span> |<span data-ttu-id="a969e-152">응용 프로그램 프로세스에 대한 지침 실행을 위해 프로세서가 사용한 모든 프로세스 스레드의 경과 시간 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="a969e-153">프로세서 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-153">Processor time</span></span> |<span data-ttu-id="a969e-154">프로세서가 비 유휴 스레드에 소요한 시간의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="a969e-155">프로세스 전용 바이트</span><span class="sxs-lookup"><span data-stu-id="a969e-155">Process private bytes</span></span> |<span data-ttu-id="a969e-156">모니터링되는 응용 프로그램의 프로세스에 독점적으로 할당된 메모리입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="a969e-157">ASP.NET 요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-157">ASP.NET request execution time</span></span> |<span data-ttu-id="a969e-158">가장 최근 요청의 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="a969e-159">실행 큐의 ASP.NET 요청</span><span class="sxs-lookup"><span data-stu-id="a969e-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="a969e-160">응용 프로그램 요청 큐의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="a969e-161">ASP.NET 요청 속도</span><span class="sxs-lookup"><span data-stu-id="a969e-161">ASP.NET request rate</span></span> |<span data-ttu-id="a969e-162">ASP.NET에서 응용 프로그램에 전송된 모든 요청의 속도(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="a969e-163">종속성 실패</span><span class="sxs-lookup"><span data-stu-id="a969e-163">Dependency failures</span></span> |<span data-ttu-id="a969e-164">서버 응용 프로그램에서 외부 리소스에 보낸 호출이 실패한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="a969e-165">서버 응답 시간</span><span class="sxs-lookup"><span data-stu-id="a969e-165">Server response time</span></span> |<span data-ttu-id="a969e-166">HTTP 요청을 받은 후 응답 전송을 완료한 때까지의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="a969e-167">요청 속도</span><span class="sxs-lookup"><span data-stu-id="a969e-167">Request rate</span></span> |<span data-ttu-id="a969e-168">응용 프로그램에 전송된 모든 요청의 속도(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="a969e-169">실패한 요청</span><span class="sxs-lookup"><span data-stu-id="a969e-169">Failed requests</span></span> |<span data-ttu-id="a969e-170">응답 코드가 400 이상인 HTTP 요청의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="a969e-171">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="a969e-171">Page views</span></span> |<span data-ttu-id="a969e-172">웹 페이지에 대한 클라이언트 사용자 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="a969e-173">가상 트래픽은 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="a969e-174">{사용자 지정 메트릭 이름}</span><span class="sxs-lookup"><span data-stu-id="a969e-174">{your custom metric name}</span></span> |<span data-ttu-id="a969e-175">{사용자의 메트릭 이름}</span><span class="sxs-lookup"><span data-stu-id="a969e-175">{Your metric name}</span></span> |<span data-ttu-id="a969e-176">메트릭 값은 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)에 의해 또는 [추적 호출의 측정 매개 변수](app-insights-api-custom-events-metrics.md#properties)에 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="a969e-177">다음과 같은 다양한 원격 분석 모듈에서 메트릭이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="a969e-178">메트릭 그룹</span><span class="sxs-lookup"><span data-stu-id="a969e-178">Metric group</span></span> | <span data-ttu-id="a969e-179">수집기 모듈</span><span class="sxs-lookup"><span data-stu-id="a969e-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="a969e-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="a969e-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="a969e-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="a969e-181">clientPerformance,</span></span><br/><span data-ttu-id="a969e-182">view</span><span class="sxs-lookup"><span data-stu-id="a969e-182">view</span></span> |[<span data-ttu-id="a969e-183">브라우저 JavaScript</span><span class="sxs-lookup"><span data-stu-id="a969e-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="a969e-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="a969e-184">performanceCounter</span></span> |[<span data-ttu-id="a969e-185">성능</span><span class="sxs-lookup"><span data-stu-id="a969e-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="a969e-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="a969e-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="a969e-187">종속성</span><span class="sxs-lookup"><span data-stu-id="a969e-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="a969e-188">request,</span><span class="sxs-lookup"><span data-stu-id="a969e-188">request,</span></span><br/><span data-ttu-id="a969e-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="a969e-189">requestFailed</span></span> |[<span data-ttu-id="a969e-190">서버 요청</span><span class="sxs-lookup"><span data-stu-id="a969e-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="a969e-191">Webhook</span><span class="sxs-lookup"><span data-stu-id="a969e-191">Webhooks</span></span>
<span data-ttu-id="a969e-192">[경고에 대한 응답을 자동화](../monitoring-and-diagnostics/insights-webhooks-alerts.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="a969e-193">경고가 발생한 경우 Azure에서 사용자가 선택한 웹 주소를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a969e-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="a969e-194">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a969e-194">See also</span></span>
* [<span data-ttu-id="a969e-195">Application Insights를 구성하는 스크립트</span><span class="sxs-lookup"><span data-stu-id="a969e-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="a969e-196">서식 파일에서 Application Insights 및 웹 테스트 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="a969e-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="a969e-197">Application Insights에 Microsoft Azure 진단 결합 자동화</span><span class="sxs-lookup"><span data-stu-id="a969e-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="a969e-198">경고에 대한 응답 자동화</span><span class="sxs-lookup"><span data-stu-id="a969e-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
