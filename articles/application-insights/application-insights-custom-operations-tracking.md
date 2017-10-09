---
title: "사용자 지정 작업과 Azure Application Insights.NET SDK를 aaaTrack | Microsoft Docs"
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
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="15142-103">Application Insights .NET SDK를 통한 사용자 지정 작업 추적</span><span class="sxs-lookup"><span data-stu-id="15142-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="15142-104">Azure Application Insights Sdk HTTP 요청 및 SQL 쿼리 같은 트랙 들어오는 HTTP 요청 및 toodependent 호출 서비스 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="15142-105">추적과 요청 및 종속성의 상관 관계 사용 하면 hello 전체 한 응용 프로그램의 응답성 및 안정성에 대 한 가시성이 응용이 프로그램을 결합 하는 모든 microservices 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="15142-106">일반적으로는 지원할 수 없는 응용 프로그램 패턴의 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="15142-107">이러한 패턴의 적절한 모니터링에는 수동 코드 계측이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="15142-108">이 문서에서는 사용자 지정 큐 처리 및 장기 실행 백그라운드 작업 실행과 같이 수동으로 계측해야 할 수 있는 몇 가지 패턴에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="15142-109">이 문서와 사용자 지정 작업 tootrack Application Insights SDK hello 하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="15142-110">다음과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="15142-111">.NET용 Application Insights(기본 SDK라고도 함) 버전 2.4+</span><span class="sxs-lookup"><span data-stu-id="15142-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="15142-112">웹 응용 프로그램용 Application Insights(ASP.NET 실행) 버전 2.4+</span><span class="sxs-lookup"><span data-stu-id="15142-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="15142-113">ASP.NET Core용 Application Insights 버전 2.1+</span><span class="sxs-lookup"><span data-stu-id="15142-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="15142-114">개요</span><span class="sxs-lookup"><span data-stu-id="15142-114">Overview</span></span>
<span data-ttu-id="15142-115">작업은 응용 프로그램에서 실행하는 활동의 논리적 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="15142-116">여기에는 이름, 시작 시간, 기간, 결과 및 실행 컨텍스트(예: 사용자 이름, 속성 및 결과)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="15142-117">작업 B에서 작업 A를 시작한 경우 작업 B는 A의 부모로 설정됩니다. 작업에는 하나의 부모만 있을 수 있지만 많은 자식 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="15142-118">작업 및 원격 분석 상관 관계에 대한 자세한 내용은 [Azure Application Insights 원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15142-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="15142-119">Application Insights.NET SDK hello hello 작업 hello 추상 클래스에 의해 설명 [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) 및 하위 항목 [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) 및 [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="15142-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="15142-120">들어오는 작업 추적</span><span class="sxs-lookup"><span data-stu-id="15142-120">Incoming operations tracking</span></span> 
<span data-ttu-id="15142-121">hello Application Insights 웹 SDK는 IIS 파이프라인에서 실행 되는 ASP.NET 응용 프로그램 및 모든 ASP.NET Core 응용 프로그램에 대 한 HTTP 요청을 자동으로 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="15142-122">다른 플랫폼과 프레임워크에 대해서 커뮤니티 지원 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="15142-123">그러나 모든 hello standard 또는 커뮤니티에서 지 원하는 솔루션에서 지원 되지 않으면 hello 응용 프로그램을 계측할 수 있습니다 것 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="15142-124">사용자 지정 추적 해야 하는 또 다른 예로 hello 큐에서 항목을 받는 hello 작업자입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="15142-125">일부 큐에 대 한 hello tooadd toothis 큐를 종속성으로 추적 메시지를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="15142-126">그러나 메시지 처리를 설명 하 고 hello 수준 작업 자동으로 수집 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="15142-127">이러한 작업을 어떻게 추적할 수 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="15142-128">높은 수준의 hello 작업은 toocreate `RequestTelemetry` 알려진된 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="15142-129">Hello 작업이 완료 된 후 hello 원격 분석을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="15142-130">다음 예제는 hello이이 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15142-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="15142-131">Owin 자체 호스팅 앱의 HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="15142-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="15142-132">이 예제에서는 hello 따릅니다 [상관 관계에 대 한 HTTP 프로토콜](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="15142-133">Tooreceive 헤더 없는 설명 하는 하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15142-133">You should expect tooreceive headers that are described there.</span></span>

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

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
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

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="15142-134">HTTP 프로토콜 상관 관계에 대 한 hello hello 선언 `Correlation-Context` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="15142-135">여기서는 간소화하기 위해 생략했습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="15142-136">큐 계측</span><span class="sxs-lookup"><span data-stu-id="15142-136">Queue instrumentation</span></span>
<span data-ttu-id="15142-137">HTTP 통신을 위해 만들었습니다 프로토콜 toopass 상관 관계 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="15142-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="15142-138">일부 큐의 프로토콜을 사용 하 고 수 없는 다른 사용자와 hello 메시지와 함께 추가 메타 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="15142-139">Service Bus 큐</span><span class="sxs-lookup"><span data-stu-id="15142-139">Service Bus queue</span></span>
<span data-ttu-id="15142-140">Azure hello로 [서비스 버스 큐](../service-bus-messaging/index.md), hello 메시지와 함께 속성 모음이 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="15142-141">사용할 수 toopass hello 상관 관계 id입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="15142-142">hello 서비스 버스 큐는 TCP 기반 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="15142-143">Application Insights에서는 큐 작업을 자동으로 추적하지 않으므로 수동으로 추적하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="15142-144">hello 큐에서 제거 작업이 푸시 스타일 API 이며 we're 없습니다 tootrack 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="15142-145">큐에 넣기</span><span class="sxs-lookup"><span data-stu-id="15142-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
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

#### <a name="process"></a><span data-ttu-id="15142-146">Process</span><span class="sxs-lookup"><span data-stu-id="15142-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
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

### <a name="azure-storage-queue"></a><span data-ttu-id="15142-147">Azure Storage 큐</span><span class="sxs-lookup"><span data-stu-id="15142-147">Azure Storage queue</span></span>
<span data-ttu-id="15142-148">hello 방법을 예제와 다음 tootrack hello [Azure 저장소 큐](../storage/queues/storage-dotnet-how-to-use-queues.md) 작업과 hello 생산자, hello 소비자 및 Azure 저장소 간에 상호 연결 시키고 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="15142-149">hello 저장소 큐에 HTTP API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="15142-150">모든 호출 toohello 큐 HTTP 요청에 대 한 응용 프로그램 Insights 종속성 수집기 hello 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15142-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="15142-151">`applicationInsights.config`에 `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="15142-152">없을 경우, 추가에 설명 된 대로 프로그래밍 방식으로 [필터링 및 hello Azure Application Insights SDK에서에서 전처리](app-insights-api-filtering-sampling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="15142-153">Application Insights를 수동으로 구성하는 경우 다음과 비슷하게 `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`을 만들고 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="15142-154">것도 좋습니다 toocorrelate hello Application Insights 작업 ID와 hello 저장소 요청 id입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="15142-155">참조 tooset 및 get 저장소 클라이언트와 서버 요청 ID를 요청 하는 방법에 대 한 내용은 [모니터, 진단 및 Azure 저장소 문제를 해결](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing)합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="15142-156">큐에 넣기</span><span class="sxs-lookup"><span data-stu-id="15142-156">Enqueue</span></span>
<span data-ttu-id="15142-157">저장소 큐 hello HTTP API를 지원 하므로 hello 큐가 있는 모든 작업 Application Insights에서 자동으로 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15142-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="15142-158">대부분의 경우 이 계측으로 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="15142-159">그러나 toocorrelate hello 소비자 쪽에 생산자 추적으로 추적, 일부 상관 관계 컨텍스트를 전달 해야 마찬가지로 toohow 그렇게 hello 상관 관계에 대 한 HTTP 프로토콜에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="15142-160">이 예제에서는 선택적 hello 추적 `Enqueue` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="15142-161">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-161">You can:</span></span>

 - <span data-ttu-id="15142-162">**(있는 경우)에 다시 시도 횟수를 상호 연결**:는 hello 하나의 공통 부모를가지고 있는 것 `Enqueue` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="15142-163">그렇지 않으면 hello 들어오는 요청의 자식 항목으로 추적 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="15142-164">여러 논리 요청 toohello 큐가 있는 경우이 호출 하는 재시도 횟수에 발생 하는 어려운 toofind 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="15142-165">**저장소 상관 관계 지정 로그(필요한 경우)**: Application Insights 원격 분석과의 상관 관계가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="15142-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="15142-166">hello `Enqueue` 작업이 부모 작업 (예를 들어, 들어오는 HTTP 요청)의 hello 자식입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="15142-167">hello HTTP 종속성 호출이 hello의 자식인 hello `Enqueue` hello 들어오는 요청에 대해 작업 하 고 hello 손자:</span><span class="sxs-lookup"><span data-stu-id="15142-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
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

<span data-ttu-id="15142-168">응용 프로그램을 보고 tooreduce hello 양의 원격 분석 또는 tootrack hello 않으려는 `Enqueue` 작업을 사용 하 여 hello 다른 이유로 `Activity` API 직접:</span><span class="sxs-lookup"><span data-stu-id="15142-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="15142-169">만들기 (및 시작) 새 `Activity` hello Application Insights 작업을 시작 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="15142-170">작업을 수행한 *하지* tooassign hello 작업 이름 제외한 모든 속성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="15142-171">직렬화 `yourActivity.Id` 대신 hello 메시지 페이로드에 `operation.Telemetry.Id`합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="15142-172">또한 `Activity.Current.Id`도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="15142-173">큐에서 제거</span><span class="sxs-lookup"><span data-stu-id="15142-173">Dequeue</span></span>
<span data-ttu-id="15142-174">마찬가지로 너무`Enqueue`, 실제 HTTP 요청 toohello 저장소 큐는 Application Insights에서 자동으로 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15142-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="15142-175">그러나 hello `Enqueue` 작업이 아마도 들어오는 요청 컨텍스트에 같이 hello 부모 컨텍스트에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="15142-176">Application Insights Sdk 자동으로 이러한 작업 (및 해당 HTTP 부분이)을 상관 hello 부모 요청 및 hello에 다른 원격 분석 보고 동일한 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="15142-177">hello `Dequeue` 작업은 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="15142-178">hello Application Insights SDK는 자동으로 HTTP 요청을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="15142-179">하지만 hello 메시지를 구문 분석할 때까지 hello 상관 관계 상황에 맞는 알 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="15142-180">Hello 나머지 hello 원격 분석 가능한 toocorrelate hello HTTP 요청 tooget hello 메시지는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="15142-181">대부분의 경우에도 다른 추적과 유용한 toocorrelate hello HTTP 요청 toohello 큐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="15142-182">hello 다음 예제에서는 어떻게 toodo 하기:</span><span class="sxs-lookup"><span data-stu-id="15142-182">hello following example demonstrates how toodo it:</span></span>

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

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
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

#### <a name="process"></a><span data-ttu-id="15142-183">Process</span><span class="sxs-lookup"><span data-stu-id="15142-183">Process</span></span>

<span data-ttu-id="15142-184">다음 예제는 hello, 들어오는 메시지를 추적에서는 들어오는 HTTP 추적에서는 toohow 요청 마찬가지로 방식에서:</span><span class="sxs-lookup"><span data-stu-id="15142-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
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

<span data-ttu-id="15142-185">마찬가지로 다른 큐 작업도 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="15142-186">피크 작업은 큐에서 제거 작업과 비슷한 방식으로 계측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="15142-187">큐 관리 작업 계측은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="15142-188">Application Insights는 HTTP와 같은 작업을 추적하며, 이는 대부분의 경우에 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="15142-189">메시지 삭제를 계측할 때 hello 작업 (상관 관계) 식별자를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="15142-190">Hello 또는 사용할 수 있습니다 `Activity` API입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="15142-191">그런 다음 Application Insights을 수행 하기 때문에 hello 원격 분석 항목에 작업 식별자 tooset 필요 없음:</span><span class="sxs-lookup"><span data-stu-id="15142-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="15142-192">새 `Activity` hello 큐에서 항목을 가져온 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="15142-193">사용 하 여 `Activity.SetParentId(message.ParentId)` toocorrelate 소비자 및 공급자 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="15142-194">Hello 시작 `Activity`합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="15142-195">`Start/StopOperation` 도우미를 사용하여 큐에서 제거, 처리 및 삭제 작업을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="15142-196">이 작업을 수행할 hello에서 동일한 비동기 제어 흐름 (실행 컨텍스트).</span><span class="sxs-lookup"><span data-stu-id="15142-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="15142-197">이런 방식으로 상관 관계가 제대로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="15142-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="15142-198">중지 hello `Activity`합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="15142-199">`Start/StopOperation`을 사용하거나 수동으로 `Track` 원격 분석을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="15142-200">일괄 처리</span><span class="sxs-lookup"><span data-stu-id="15142-200">Batch processing</span></span>
<span data-ttu-id="15142-201">일부 큐의 경우 하나의 요청으로 여러 메시지를 큐에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="15142-202">이러한 메시지를 처리 아마도 독립적 이며 toohello 다른 논리 연산을 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="15142-203">이 경우 없으면 가능한 toocorrelate hello `Dequeue` 작업 tooparticular 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="15142-204">각 메시지는 자체 비동기 제어 흐름에서 처리되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="15142-205">자세한 내용은 참조 hello [나가는 종속성 추적](#outgoing-dependencies-tracking) 섹션.</span><span class="sxs-lookup"><span data-stu-id="15142-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="15142-206">장기 실행 백그라운드 작업 실행 </span><span class="sxs-lookup"><span data-stu-id="15142-206">Long-running background tasks</span></span>
<span data-ttu-id="15142-207">일부 응용 프로그램은 사용자 요청으로 인해 발생할 수 있는 장기 실행 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="15142-208">Hello 추적/계측 관점에서 요청 또는 종속성 계측에서 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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
            // Process hello task.
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

<span data-ttu-id="15142-209">이 예에서는 사용 `telemetryClient.StartOperation` toocreate `RequestTelemetry` 및 채우기 hello 상관 관계 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="15142-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="15142-210">Hello 작업을 예약 하는 들어오는 요청에 의해 생성 된 부모 작업이 있는 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="15142-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="15142-211">으로 `BackgroundTask` 시작 hello 들어오는 요청으로 동일한 비동기 제어 흐름, 해당 부모 작업와 연관 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="15142-212">`BackgroundTask`및 모든 중첩 된 원격 분석 항목은 자동으로 상호 관련 hello 요청 종료 된 후에 일으킨 hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="15142-213">없는 경우 모든 작업을 수행 하는 hello 백그라운드 스레드에서 hello 작업을 시작 하는 경우 (`Activity`) 연결 되어 있어서 `BackgroundTask` 상위 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="15142-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="15142-214">그러나 중첩된 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-214">However, it can have nested operations.</span></span> <span data-ttu-id="15142-215">Hello 작업에서 보고 하는 모든 원격 분석 항목은 상호 관련 된 toohello `RequestTelemetry` 에서 만든 `BackgroundTask`합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="15142-216">나가는 종속성 추적</span><span class="sxs-lookup"><span data-stu-id="15142-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="15142-217">사용자 고유의 종속성 종류 또는 Application Insights에서 지원하지 않는 작업을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="15142-218">hello `Enqueue` 메서드 hello 서비스 버스 큐 또는 hello 저장소 큐는 이러한 사용자 지정 추적에 대 한 예제로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="15142-219">사용자 지정 종속성 추적에 대 한 hello 일반 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="15142-220">Hello 호출 `TelemetryClient.StartOperation` hello 채워지는 (확장) 메서드 `DependencyTelemetry` 상관 관계 및 일부 다른 속성에 필요한 속성 (시작 시간 스탬프, 기간).</span><span class="sxs-lookup"><span data-stu-id="15142-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="15142-221">Hello에 다른 사용자 지정 속성을 설정 `DependencyTelemetry`hello 이름 및 필요한 다른 컨텍스트 등.</span><span class="sxs-lookup"><span data-stu-id="15142-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="15142-222">종속성을 호출하고 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="15142-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="15142-223">사용 하 여 hello 작업 중지 `StopOperation` 완료 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="15142-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="15142-224">예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-224">Handle exceptions.</span></span>

<span data-ttu-id="15142-225">`StopOperation`만 시작 된 hello 작업을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="15142-226">현재 실행 중인 작업 hello toostop, 원하는 하나 hello와 일치 하지 않으면 `StopOperation` 는 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="15142-227">Hello에 동시에 여러 작업을 시작 하는 경우에 이러한 상황이 발생할 수 있습니다 동일한 실행 컨텍스트:</span><span class="sxs-lookup"><span data-stu-id="15142-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="15142-228">항상 `StartOperation`을 호출하고 자체 컨텍스트에서 작업을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="15142-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15142-229">Next steps</span></span>

- <span data-ttu-id="15142-230">hello 기본 사항 알아보기 [원격 분석 상관 관계](application-insights-correlation.md) Application Insights에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="15142-231">Hello 참조 [데이터 모델](application-insights-data-model.md) Application Insights 유형 및 데이터 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="15142-232">사용자 지정 보고서 [이벤트 및 메트릭을](app-insights-api-custom-events-metrics.md) tooApplication Insights 합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="15142-233">컨텍스트 속성 컬렉션에 대한 표준 [구성](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15142-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="15142-234">Hello 확인 [System.Diagnostics.Activity 사용자 가이드](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee 원격 분석 상관 관계 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15142-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
