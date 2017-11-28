---
title: "Application Insights에서 aaaUse Powershell tooset 경고 | Microsoft Docs"
description: "메트릭 변경에 대 한 Application Insights tooget 전자 메일의 구성을 자동화 합니다."
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
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="ff92d-103">Application Insights에서 PowerShell tooset 경고를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="ff92d-104">hello 구성을 자동화할 수 있습니다 [경고](app-insights-alerts.md) 에 [Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="ff92d-105">수 또한 [webhook tooautomate 응답 tooan 경고를 설정](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ff92d-106">Toocreate 리소스과 경고를 원하는 경우 hello 동일한 시간을 고려 하십시오 [Azure 리소스 관리자 템플릿을 사용 하 여](app-insights-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="ff92d-107">일 회 설정</span><span class="sxs-lookup"><span data-stu-id="ff92d-107">One-time setup</span></span>
<span data-ttu-id="ff92d-108">아직 Azure 구독에서 PowerShell을 사용한 적이 없을 경우:</span><span class="sxs-lookup"><span data-stu-id="ff92d-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="ff92d-109">Toorun hello 스크립트 저장할 hello 머신에서 hello Azure Powershell 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="ff92d-110">[Microsoft 웹 플랫폼 설치 관리자(v5 이상)](http://www.microsoft.com/web/downloads/platform.aspx)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="ff92d-111">Microsoft Azure Powershell tooinstall 사용</span><span class="sxs-lookup"><span data-stu-id="ff92d-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="ff92d-112">TooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="ff92d-112">Connect tooAzure</span></span>
<span data-ttu-id="ff92d-113">Azure PowerShell을 시작 하 고 [tooyour 구독 연결](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="ff92d-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="ff92d-114">경고 받기</span><span class="sxs-lookup"><span data-stu-id="ff92d-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="ff92d-115">경고 추가</span><span class="sxs-lookup"><span data-stu-id="ff92d-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="ff92d-116">예 1</span><span class="sxs-lookup"><span data-stu-id="ff92d-116">Example 1</span></span>
<span data-ttu-id="ff92d-117">(5 분) 평균 hello 서버 응답 tooHTTP 요청 1 초 보다 느린 경우 내게 메일 보내기.</span><span class="sxs-lookup"><span data-stu-id="ff92d-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="ff92d-118">Application Insights 리소스의 이름이 IceCreamWebApp이며 리소스 그룹 Fabrikam 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="ff92d-119">저는 hello 소유자 hello Azure 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="ff92d-120">hello GUID hello 구독 ID (hello 계측 키가 아니라 hello 응용 프로그램의)입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="ff92d-121">예 2</span><span class="sxs-lookup"><span data-stu-id="ff92d-121">Example 2</span></span>
<span data-ttu-id="ff92d-122">응용 프로그램을 사용 중인 [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport "salesPerHour." 라는 메트릭</span><span class="sxs-lookup"><span data-stu-id="ff92d-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="ff92d-123">평균을 24 시간 이상 100 개 이하로 떨어지면 "salesPerHour" 전자 메일 toomy 동료를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="ff92d-124">hello 메트릭에 대 한 동일한 규칙을 사용할 수는 hello hello를 사용 하 여 보고할 [측정 매개 변수](app-insights-api-custom-events-metrics.md#properties) TrackEvent trackPageView 등 다른 추적 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="ff92d-125">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="ff92d-125">Metric names</span></span>
| <span data-ttu-id="ff92d-126">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="ff92d-126">Metric name</span></span> | <span data-ttu-id="ff92d-127">화면 이름</span><span class="sxs-lookup"><span data-stu-id="ff92d-127">Screen name</span></span> | <span data-ttu-id="ff92d-128">설명</span><span class="sxs-lookup"><span data-stu-id="ff92d-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="ff92d-129">브라우저 예외</span><span class="sxs-lookup"><span data-stu-id="ff92d-129">Browser exceptions</span></span> |<span data-ttu-id="ff92d-130">Hello 브라우저에서 발생 한 예외를 확인할 수 없는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="ff92d-131">서버 예외</span><span class="sxs-lookup"><span data-stu-id="ff92d-131">Server exceptions</span></span> |<span data-ttu-id="ff92d-132">Hello 응용 프로그램에서 throw 된 처리 되지 않은 예외 수</span><span class="sxs-lookup"><span data-stu-id="ff92d-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="ff92d-133">클라이언트 처리 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-133">Client processing time</span></span> |<span data-ttu-id="ff92d-134">Hello DOM 로드 될 때까지 hello 문서의 마지막 바이트 받기 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="ff92d-135">비동기 요청은 계속 처리 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="ff92d-136">페이지 로드 네트워크 연결 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-136">Page load network connect time</span></span> |<span data-ttu-id="ff92d-137">시간 hello 브라우저 tooconnect toohello 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="ff92d-138">캐시된 경우 0일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="ff92d-139">응답 수신 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-139">Receiving response time</span></span> |<span data-ttu-id="ff92d-140">브라우저 요청 toostarting tooreceive 응답을 보내는 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="ff92d-141">요청 전송 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-141">Send request time</span></span> |<span data-ttu-id="ff92d-142">브라우저 toosend 요청에서 사용한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="ff92d-143">브라우저 페이지 로드 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-143">Browser page load time</span></span> |<span data-ttu-id="ff92d-144">사용자가 요청한 때부터 DOM, 스타일시트, 스크립트 및 이미지가 로드될 때까지 소요된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="ff92d-145">사용 가능한 메모리</span><span class="sxs-lookup"><span data-stu-id="ff92d-145">Available memory</span></span> |<span data-ttu-id="ff92d-146">처리를 위해서나 시스템에서 바로 사용할 수 있는 실제 메모리입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="ff92d-147">프로세스 IO 속도</span><span class="sxs-lookup"><span data-stu-id="ff92d-147">Process IO Rate</span></span> |<span data-ttu-id="ff92d-148">두 번째 읽기 및 서 면된 toofiles, 네트워크 및 장치 당 총 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="ff92d-149">예외 속도</span><span class="sxs-lookup"><span data-stu-id="ff92d-149">exception rate</span></span> |<span data-ttu-id="ff92d-150">초당 발생한 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="ff92d-151">CPU 프로세스</span><span class="sxs-lookup"><span data-stu-id="ff92d-151">Process CPU</span></span> |<span data-ttu-id="ff92d-152">hello 응용 프로그램 프로세스에 대 한 hello 프로세서 tooexecution 명령에서 사용 되는 모든 프로세스 스레드의 경과 된 시간의 hello 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="ff92d-153">프로세서 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-153">Processor time</span></span> |<span data-ttu-id="ff92d-154">비 유휴 스레드를에서 소비한 hello 백분율 hello 프로세서 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="ff92d-155">프로세스 전용 바이트</span><span class="sxs-lookup"><span data-stu-id="ff92d-155">Process private bytes</span></span> |<span data-ttu-id="ff92d-156">만 toohello 할당 된 메모리는 응용 프로그램의 프로세스를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="ff92d-157">ASP.NET 요청 실행 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-157">ASP.NET request execution time</span></span> |<span data-ttu-id="ff92d-158">Hello 가장 최근 요청의 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="ff92d-159">실행 큐의 ASP.NET 요청</span><span class="sxs-lookup"><span data-stu-id="ff92d-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="ff92d-160">Hello 응용 프로그램 요청 큐의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="ff92d-161">ASP.NET 요청 속도</span><span class="sxs-lookup"><span data-stu-id="ff92d-161">ASP.NET request rate</span></span> |<span data-ttu-id="ff92d-162">모든 속도 ASP.NET에서 초당 toohello 응용 프로그램을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="ff92d-163">종속성 실패</span><span class="sxs-lookup"><span data-stu-id="ff92d-163">Dependency failures</span></span> |<span data-ttu-id="ff92d-164">실패 한 hello 서버 응용 프로그램 tooexternal 리소스별 호출의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="ff92d-165">서버 응답 시간</span><span class="sxs-lookup"><span data-stu-id="ff92d-165">Server response time</span></span> |<span data-ttu-id="ff92d-166">HTTP 요청 받기와 hello 응답 보내기 완료 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="ff92d-167">요청 속도</span><span class="sxs-lookup"><span data-stu-id="ff92d-167">Request rate</span></span> |<span data-ttu-id="ff92d-168">초당 toohello 응용 프로그램을 요청 하는 모든의 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="ff92d-169">실패한 요청</span><span class="sxs-lookup"><span data-stu-id="ff92d-169">Failed requests</span></span> |<span data-ttu-id="ff92d-170">응답 코드가 400 이상인 HTTP 요청의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="ff92d-171">페이지 보기</span><span class="sxs-lookup"><span data-stu-id="ff92d-171">Page views</span></span> |<span data-ttu-id="ff92d-172">웹 페이지에 대한 클라이언트 사용자 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="ff92d-173">가상 트래픽은 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="ff92d-174">{사용자 지정 메트릭 이름}</span><span class="sxs-lookup"><span data-stu-id="ff92d-174">{your custom metric name}</span></span> |<span data-ttu-id="ff92d-175">{사용자의 메트릭 이름}</span><span class="sxs-lookup"><span data-stu-id="ff92d-175">{Your metric name}</span></span> |<span data-ttu-id="ff92d-176">사용자가 메트릭 값에서 보고 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) 또는 hello [추적 호출의 매개 변수 측정](app-insights-api-custom-events-metrics.md#properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="ff92d-177">hello 메트릭 여러 원격 모듈에 의해 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="ff92d-178">메트릭 그룹</span><span class="sxs-lookup"><span data-stu-id="ff92d-178">Metric group</span></span> | <span data-ttu-id="ff92d-179">수집기 모듈</span><span class="sxs-lookup"><span data-stu-id="ff92d-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="ff92d-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="ff92d-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="ff92d-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="ff92d-181">clientPerformance,</span></span><br/><span data-ttu-id="ff92d-182">view</span><span class="sxs-lookup"><span data-stu-id="ff92d-182">view</span></span> |[<span data-ttu-id="ff92d-183">브라우저 JavaScript</span><span class="sxs-lookup"><span data-stu-id="ff92d-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="ff92d-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="ff92d-184">performanceCounter</span></span> |[<span data-ttu-id="ff92d-185">성능</span><span class="sxs-lookup"><span data-stu-id="ff92d-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="ff92d-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="ff92d-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="ff92d-187">종속성</span><span class="sxs-lookup"><span data-stu-id="ff92d-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="ff92d-188">request,</span><span class="sxs-lookup"><span data-stu-id="ff92d-188">request,</span></span><br/><span data-ttu-id="ff92d-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="ff92d-189">requestFailed</span></span> |[<span data-ttu-id="ff92d-190">서버 요청</span><span class="sxs-lookup"><span data-stu-id="ff92d-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="ff92d-191">Webhook</span><span class="sxs-lookup"><span data-stu-id="ff92d-191">Webhooks</span></span>
<span data-ttu-id="ff92d-192">있습니다 수 [응답 tooan 경고 자동화](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="ff92d-193">경고가 발생한 경우 Azure에서 사용자가 선택한 웹 주소를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ff92d-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff92d-194">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ff92d-194">See also</span></span>
* [<span data-ttu-id="ff92d-195">스크립트 tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff92d-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="ff92d-196">서식 파일에서 Application Insights 및 웹 테스트 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="ff92d-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="ff92d-197">Microsoft Azure 진단 tooApplication Insights 결합 자동화</span><span class="sxs-lookup"><span data-stu-id="ff92d-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="ff92d-198">응답 tooan 경고 자동화</span><span class="sxs-lookup"><span data-stu-id="ff92d-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
