---
title: "Azure Application Insights .NET SDK를 통한 사용자 지정 작업 추적 | Microsoft Docs"
description: "Azure Application Insights .NET SDK를 통한 사용자 지정 작업 추적 "
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: b31d38fe2f7060597956a1ee9c66f43ce39d7240
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="2fbc7-103">Application Insights .NET SDK를 통한 사용자 지정 작업 추적</span><span class="sxs-lookup"><span data-stu-id="2fbc7-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="2fbc7-104">Azure Application Insights SDK는 들어오는 HTTP 요청과 종속 서비스에 대한 호출(예:HTTP 요청 및 SQL 쿼리)을 자동으로 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="2fbc7-105">요청 및 종속성의 추적과 상관 관계를 사용하면 응용 프로그램을 결합하는 모든 마이크로 서비스에서 전체 응용 프로그램의 응답성 및 안정성을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="2fbc7-106">일반적으로는 지원할 수 없는 응용 프로그램 패턴의 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="2fbc7-107">이러한 패턴의 적절한 모니터링에는 수동 코드 계측이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="2fbc7-108">이 문서에서는 사용자 지정 큐 처리 및 장기 실행 백그라운드 작업 실행과 같이 수동으로 계측해야 할 수 있는 몇 가지 패턴에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="2fbc7-109">여기서는 Application Insights SDK를 통해 사용자 지정 작업을 추적하는 방법에 대한 지침을 제공하며,</span><span class="sxs-lookup"><span data-stu-id="2fbc7-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="2fbc7-110">다음과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="2fbc7-111">.NET용 Application Insights(기본 SDK라고도 함) 버전 2.4+</span><span class="sxs-lookup"><span data-stu-id="2fbc7-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="2fbc7-112">웹 응용 프로그램용 Application Insights(ASP.NET 실행) 버전 2.4+</span><span class="sxs-lookup"><span data-stu-id="2fbc7-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="2fbc7-113">ASP.NET Core용 Application Insights 버전 2.1+</span><span class="sxs-lookup"><span data-stu-id="2fbc7-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="2fbc7-114">개요</span><span class="sxs-lookup"><span data-stu-id="2fbc7-114">Overview</span></span>
<span data-ttu-id="2fbc7-115">작업은 응용 프로그램에서 실행하는 활동의 논리적 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="2fbc7-116">여기에는 이름, 시작 시간, 기간, 결과 및 실행 컨텍스트(예: 사용자 이름, 속성 및 결과)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="2fbc7-117">작업 B에서 작업 A를 시작한 경우 작업 B는 A의 부모로 설정됩니다. 작업에는 하나의 부모만 있을 수 있지만 많은 자식 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="2fbc7-118">작업 및 원격 분석 상관 관계에 대한 자세한 내용은 [Azure Application Insights 원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="2fbc7-119">Application Insights .NET SDK에서 작업은 [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) 추상 클래스 및 해당하는[RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) 및 [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs) 하위 항목으로 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="2fbc7-120">들어오는 작업 추적</span><span class="sxs-lookup"><span data-stu-id="2fbc7-120">Incoming operations tracking</span></span> 
<span data-ttu-id="2fbc7-121">Application Insights 웹 SDK는 IIS 파이프라인과 모든 ASP.NET Core 응용 프로그램에서 실행되는 ASP.NET 응용 프로그램에 대한 HTTP 요청을 자동으로 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="2fbc7-122">다른 플랫폼과 프레임워크에 대해서 커뮤니티 지원 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="2fbc7-123">그러나 응용 프로그램에서 표준 또는 커뮤니티 지원 솔루션으로 지원되지 않으면 수동으로 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="2fbc7-124">사용자 지정 추적이 필요한 또 다른 예로 큐에서 항목을 받는 작업자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="2fbc7-125">일부 큐의 경우 이 큐에 메시지를 추가하는 호출이 종속성으로 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="2fbc7-126">그러나 메시지 처리를 설명하는 상위 수준 작업은 자동으로 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="2fbc7-127">이러한 작업을 어떻게 추적할 수 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="2fbc7-128">상위 수준에서 작업은 `RequestTelemetry`를 만들고 알려진 속성을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="2fbc7-129">작업이 완료되면 원격 분석을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="2fbc7-130">다음 예제에서는 이 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="2fbc7-131">Owin 자체 호스팅 앱의 HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="2fbc7-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="2fbc7-132">이 예제에서는 [상관 관계에 대한 HTTP 프로토콜(영문)](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-132">In this example, we follow the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="2fbc7-133">여기서 설명하는 헤더를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-133">You should expect to receive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="2fbc7-134">상관 관계에 대한 HTTP 프로토콜도 `Correlation-Context` 헤더를 선언하지만,</span><span class="sxs-lookup"><span data-stu-id="2fbc7-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="2fbc7-135">여기서는 간소화하기 위해 생략했습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="2fbc7-136">큐 계측</span><span class="sxs-lookup"><span data-stu-id="2fbc7-136">Queue instrumentation</span></span>
<span data-ttu-id="2fbc7-137">HTTP 통신을 위해 상관 관계 세부 정보를 전달하는 프로토콜을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-137">For HTTP communication, we've created a protocol to pass correlation details.</span></span> <span data-ttu-id="2fbc7-138">일부 큐의 프로토콜을 사용하면 메시지와 함께 추가 메타데이터를 전달할 수 있지만, 다른 프로토콜을 사용하면 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-138">With some queues' protocols, you can pass additional metadata along with the message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="2fbc7-139">Service Bus 큐</span><span class="sxs-lookup"><span data-stu-id="2fbc7-139">Service Bus queue</span></span>
<span data-ttu-id="2fbc7-140">Azure [Service Bus 큐](../service-bus-messaging/index.md)를 사용하면 메시지와 함께 속성 모음을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-140">With the Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with the message.</span></span> <span data-ttu-id="2fbc7-141">이 큐는 상관 관계 ID를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-141">We use it to pass the correlation ID.</span></span>

<span data-ttu-id="2fbc7-142">Service Bus 큐는 TCP 기반 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-142">The Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="2fbc7-143">Application Insights에서는 큐 작업을 자동으로 추적하지 않으므로 수동으로 추적하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="2fbc7-144">큐에서 제거 작업은 푸시 스타일 API이며, 이를 추적할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-144">The dequeue operation is a push-style API, and we're unable to track it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="2fbc7-145">큐에 넣기</span><span class="sxs-lookup"><span data-stu-id="2fbc7-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="2fbc7-146">Process</span><span class="sxs-lookup"><span data-stu-id="2fbc7-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="2fbc7-147">Azure Storage 큐</span><span class="sxs-lookup"><span data-stu-id="2fbc7-147">Azure Storage queue</span></span>
<span data-ttu-id="2fbc7-148">다음 예제에서는 [Azure Storage 큐](../storage/queues/storage-dotnet-how-to-use-queues.md) 작업을 추적하고 생산자, 소비자 및 Azure Storage 간의 원격 분석 상관 관계를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="2fbc7-149">Storage 큐에는 HTTP API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="2fbc7-150">큐에 대한 모든 호출은 HTTP 요청에 대한 Application Insights 종속성 수집기에서 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="2fbc7-151">`applicationInsights.config`에 `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="2fbc7-152">없는 경우 [Application Insights SDK에서 필터링 및 전처리](app-insights-api-filtering-sampling.md)에서 설명한 대로 프로그래밍 방식으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="2fbc7-153">Application Insights를 수동으로 구성하는 경우 다음과 비슷하게 `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`을 만들고 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="2fbc7-154">또한 Application Insights 작업 ID와 Storage 요청 ID 사이의 상관 관계를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="2fbc7-155">Storage 요청 클라이언트와 서버 요청 ID를 설정하고 가져 오는 방법에 대한 자세한 내용은 [Azure Storage 모니터링, 진단 및 문제 해결](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="2fbc7-156">큐에 넣기</span><span class="sxs-lookup"><span data-stu-id="2fbc7-156">Enqueue</span></span>
<span data-ttu-id="2fbc7-157">Storage 큐는 HTTP API를 지원하므로 큐를 통한 모든 작업은 Application Insights에서 자동으로 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="2fbc7-158">대부분의 경우 이 계측으로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="2fbc7-159">그러나 생산자 추적과 소비자 쪽 추적 사이의 상관 관계를 지정하려면 상관 관계에 대한 HTTP 프로토콜에서 수행하는 것과 비슷한 일부 상관 관계 컨텍스트를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="2fbc7-160">이 예제에서는 선택적인 `Enqueue` 작업을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-160">In this example, we track the optional `Enqueue` operation.</span></span> <span data-ttu-id="2fbc7-161">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-161">You can:</span></span>

 - <span data-ttu-id="2fbc7-162">**상관 관계 지정 재시도(있는 경우)**: 모든 작업에는 `Enqueue` 작업인 하나의 공통 부모가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="2fbc7-163">그렇지 않으면 들어오는 요청의 자식으로 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="2fbc7-164">큐에 대한 논리적 요청이 여러 개 있으면 재시도가 발생한 호출을 찾는 것이 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="2fbc7-165">**저장소 상관 관계 지정 로그(필요한 경우)**: Application Insights 원격 분석과의 상관 관계가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="2fbc7-166">`Enqueue` 작업은 부모 작업의 자식(예 : 들어오는 HTTP 요청)입니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="2fbc7-167">HTTP 종속성 호출은 `Enqueue` 작업의 자식 및 들어오는 요청의 손자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="2fbc7-168">응용 프로그램 보고서에서 원격 분석의 양을 줄이거나 다른 이유로 `Enqueue` 작업을 추적하지 않으려면 `Activity` API를 직접 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="2fbc7-169">Application Insights 작업을 시작하는 대신 새 `Activity`를 만듭니다(및 시작합니다).</span><span class="sxs-lookup"><span data-stu-id="2fbc7-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="2fbc7-170">작업 이름을 제외한 모든 속성을 *지정하지 않아도 됩니다*.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="2fbc7-171">`operation.Telemetry.Id` 대신 메시지 페이로드에 `yourActivity.Id`를 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="2fbc7-172">또한 `Activity.Current.Id`도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="2fbc7-173">큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="2fbc7-173">Dequeue</span></span>
<span data-ttu-id="2fbc7-174">`Enqueue`와 비슷하게 Storage 큐에 대한 실제 HTTP 요청은 Application Insights에서 자동으로 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="2fbc7-175">그러나 `Enqueue` 작업은 아마도 들어오는 요청 컨텍스트와 같은 부모 컨텍스트에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="2fbc7-176">Application Insights SDK는 이러한 작업(및 해당하는 HTTP 부분)과 부모 요청 및 동일한 범위에서 보고되는 다른 원격 분석 사이의 상관 관계를 자동으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="2fbc7-177">`Dequeue` 작업은 까다롭습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="2fbc7-178">Application Insights SDK에서 HTTP 요청을 자동으로 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="2fbc7-179">그러나 메시지가 구문 분석될 때까지 상관 관계 컨텍스트를 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="2fbc7-180">원격 분석의 나머지 부분과 메시지를 받기 위한 HTTP 요청 사이의 상관 관계는 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="2fbc7-181">대부분의 경우 큐에 대한 HTTP 요청과 다른 추적 사이의 상관 관계를 지정하는 것도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="2fbc7-182">다음 예제에서는 이를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-182">The following example demonstrates how to do it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="2fbc7-183">Process</span><span class="sxs-lookup"><span data-stu-id="2fbc7-183">Process</span></span>

<span data-ttu-id="2fbc7-184">다음 예제에서는 들어오는 HTTP 요청을 추적하는 방법과 비슷한 방식으로 들어오는 메시지를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-184">In the following example, we trace an incoming message in a manner similarly to how we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="2fbc7-185">마찬가지로 다른 큐 작업도 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="2fbc7-186">피크 작업은 큐에서 제거 작업과 비슷한 방식으로 계측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="2fbc7-187">큐 관리 작업 계측은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="2fbc7-188">Application Insights는 HTTP와 같은 작업을 추적하며, 이는 대부분의 경우에 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="2fbc7-189">메시지 삭제를 계측할 때는 작업(상관 관계) 식별자를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="2fbc7-190">또는 `Activity` API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="2fbc7-191">그러면 Application Insights에서 사용자를 대신하여 이 작업을 수행하므로 원격 분석 항목에서 작업 식별자를 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="2fbc7-192">큐에서 항목을 가져온 후 새 `Activity`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="2fbc7-193">`Activity.SetParentId(message.ParentId)`를 사용하여 소비자와 생산자 로그의 상관 관계를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="2fbc7-194">`Activity`를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-194">Start the `Activity`.</span></span>
- <span data-ttu-id="2fbc7-195">`Start/StopOperation` 도우미를 사용하여 큐에서 제거, 처리 및 삭제 작업을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="2fbc7-196">동일한 비동기 제어 흐름(실행 컨텍스트)에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="2fbc7-197">이런 방식으로 상관 관계가 제대로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="2fbc7-198">`Activity`를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="2fbc7-199">`Start/StopOperation`을 사용하거나 수동으로 `Track` 원격 분석을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="2fbc7-200">일괄 처리</span><span class="sxs-lookup"><span data-stu-id="2fbc7-200">Batch processing</span></span>
<span data-ttu-id="2fbc7-201">일부 큐의 경우 하나의 요청으로 여러 메시지를 큐에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="2fbc7-202">이러한 메시지를 처리하는 것은 아마도 독립적이며 다른 논리 연산에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="2fbc7-203">이 경우 `Dequeue` 작업을 특정 메시지 처리와 상호 연결할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="2fbc7-204">각 메시지는 자체 비동기 제어 흐름에서 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="2fbc7-205">자세한 내용은 [나가는 종속성 추적](#outgoing-dependencies-tracking) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="2fbc7-206">장기 실행 백그라운드 작업 실행 </span><span class="sxs-lookup"><span data-stu-id="2fbc7-206">Long-running background tasks</span></span>
<span data-ttu-id="2fbc7-207">일부 응용 프로그램은 사용자 요청으로 인해 발생할 수 있는 장기 실행 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="2fbc7-208">추적/계측 관점에서 이는 요청이나 종속성 계측과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process the task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="2fbc7-209">이 예에서는 `telemetryClient.StartOperation`을 사용하여 `RequestTelemetry`를 만들고 상관 컨텍스트를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-209">In this example, we use `telemetryClient.StartOperation` to create `RequestTelemetry` and fill the correlation context.</span></span> <span data-ttu-id="2fbc7-210">작업을 예약한 들어오는 요청으로 만들어진 부모 작업이 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="2fbc7-211">들어오는 요청과 동일한 비동기 제어 흐름에서 `BackgroundTask`가 시작되는 한 해당 부모 작업과 상관 관계가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="2fbc7-212">`BackgroundTask` 및 모든 중첩된 원격 분석 항목은 요청이 종료된 후에도 원인이 된 요청과의 상관 관계가 자동으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="2fbc7-213">연결된 작업(`Activity`)이 없는 백그라운드 스레드에서 작업이 시작되면 `BackgroundTask`에는 부모가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="2fbc7-214">그러나 중첩된 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-214">However, it can have nested operations.</span></span> <span data-ttu-id="2fbc7-215">이 작업에서 보고되는 모든 원격 분석 항목과 `BackgroundTask`에서 만들어진 `RequestTelemetry` 사이의 상관 관계가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="2fbc7-216">나가는 종속성 추적</span><span class="sxs-lookup"><span data-stu-id="2fbc7-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="2fbc7-217">사용자 고유의 종속성 종류 또는 Application Insights에서 지원하지 않는 작업을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="2fbc7-218">Service Bus 큐의 `Enqueue` 메서드 또는 Azure Storage 큐는 이러한 사용자 지정 추적의 예제로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="2fbc7-219">사용자 지정 종속성 추적을 위한 일반적인 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="2fbc7-220">상관 관계 및 일부 다른 속성(시작 타임스탬프, 기간)에 필요한 `DependencyTelemetry` 속성을 채우는 `TelemetryClient.StartOperation`(확장) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="2fbc7-221">이름 및 기타 필요한 컨텍스트와 같이 `DependencyTelemetry`에서 다른 사용자 지정 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="2fbc7-222">종속성을 호출하고 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="2fbc7-223">완료되면 `StopOperation`을 통해 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="2fbc7-224">예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-224">Handle exceptions.</span></span>

<span data-ttu-id="2fbc7-225">`StopOperation`은 시작된 작업만 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-225">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="2fbc7-226">현재 실행 중인 작업이 중지하려는 작업과 일치하지 않으면 `StopOperation`에서 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-226">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="2fbc7-227">이 경우 동일한 실행 컨텍스트에서 여러 작업을 동시에 시작하면 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-227">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="2fbc7-228">항상 `StartOperation`을 호출하고 자체 컨텍스트에서 작업을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2fbc7-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2fbc7-229">Next steps</span></span>

- <span data-ttu-id="2fbc7-230">Application Insights에서 [원격 분석 상관 관계](application-insights-correlation.md) 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-230">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="2fbc7-231">Application Insights 유형 및 데이터 모델은 [데이터 모델](application-insights-data-model.md)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-231">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="2fbc7-232">사용자 지정 [이벤트 및 메트릭](app-insights-api-custom-events-metrics.md)을 Application Insights에 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="2fbc7-233">컨텍스트 속성 컬렉션에 대한 표준 [구성](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="2fbc7-234">[System.Diagnostics.Activity 사용자 가이드](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md)에서 원격 분석 상관 관계를 지정하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fbc7-234">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
