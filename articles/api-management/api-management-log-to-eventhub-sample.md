---
title: "Azure API Management, Event Hubs 및 Runscope를 사용하여 API 모니터링 | Microsoft Docs"
description: "Azure API 관리, Azure 이벤트 허브 및 HTTP 로깅 및 모니터링에 대한 Runscope에 연결하여  log-to-eventhub 정책을 보여주는 샘플 응용 프로그램"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="6c867-103">Azure API 관리, 이벤트 허브 및 Runscope를 사용하여 API 모니터링</span><span class="sxs-lookup"><span data-stu-id="6c867-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="6c867-104">[API 관리 서비스](api-management-key-concepts.md) 는 HTTP API로 전송 된 HTTP 요청의 처리를 향상시키기 위해 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="6c867-105">그러나 요청 및 응답의 존재는 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="6c867-106">요청이 생성되면 API 관리 서비스를 통해 백 엔드 API로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="6c867-107">API는 요청을 처리하고 응답은 API 소비자를 통해 다시 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="6c867-108">API 관리 서비스는 게시자 포털 대시보드에 표시하기 위해 API에 대한 중요한 통계를 일부 유지하지만 세부 정보는 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="6c867-109">API 관리 서비스에서 [로그 이벤트 허브](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [정책](api-management-howto-policies.md)을 사용하여 요청 및 응답에서 [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md)에 세부 정보를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="6c867-110">API로 전송되는 HTTP 메시지에서 이벤트를 생성하려는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="6c867-111">예에는 업데이트의 감사 내역, 사용 분석, 예외 경고 및 타사 통합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="6c867-112">이 문서는 전체 HTTP 요청 및 응답 메시지를 캡처하고 이를 이벤트 허브에 보낸 다음 HTTP 로깅 및 모니터링 서비스를 제공하는 타사 서비스에 해당 메시지를 릴레이하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="6c867-113">API 관리 서비스에서 전송되는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6c867-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="6c867-114">HTTP API 프레임워크에 연결할 수 있는 HTTP 미들웨어를 작성하여 HTTP 요청 및 응답을 캡처하고 로깅 및 모니터링 시스템에 공급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="6c867-115">이 방법의 단점은 HTTP 미들웨어가 백 엔드 API에 통합되어야 하고 API의 플랫폼과 일치해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="6c867-116">여러 API가 있는 경우 각각이 미들웨어를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="6c867-117">백 엔드 API를 업데이트할 수 없는 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="6c867-118">Azure API 관리 서비스를 사용하여 로깅 인프라와 통합하는 작업은 중앙 집중화되고 플랫폼 독립적인 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="6c867-119">또한 부분적으로 Azure API 관리의 [지역에서 복제](api-management-howto-deploy-multi-region.md) 기능으로 인해 확장성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="6c867-120">Azure 이벤트 허브에 전송되는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6c867-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="6c867-121">Azure 이벤트 허브에 지정된 정책을 만드는 이유를 묻는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="6c867-122">내 요청을 로그할 수 있는 여러 위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="6c867-123">최종 대상에 직접 요청을 전송하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6c867-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="6c867-124">이것은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-124">That is an option.</span></span> <span data-ttu-id="6c867-125">그러나 API 관리 서비스에서 로깅 요청을 생성할 때 로깅 메시지가 API의 성능에 미치는 영향을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="6c867-126">로드의 점진적인 증가는 시스템 구성 요소에서 사용할 수 있는 인스턴스를 늘리거나 지역에서 복제를 활용하여 처리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="6c867-127">그러나 로깅 인프라에 대한 요청이 부하로 늦기 시작하는 경우 트래픽의 순간적인 급증은 요청을 상당히 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="6c867-128">Azure 이벤트 허브는 대부분 API 프로세스를 요청하는 HTTP 수 보다 훨씬 많은 이벤트를 처리하는 용량을 보유하여 엄청난 양의 데이터를 수신하도록 설계됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="6c867-129">이벤트 허브는 메시지를 저장하고 처리하는 API 관리 서비스와 인프라 간에 한 종류의 복잡한 버퍼 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="6c867-130">이렇게 하면 API는 로깅 인프라로 인해 성능이 저하되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="6c867-131">데이터가 이벤트 허브에 전달되면 유지되고 이벤트 허브 소비자가 처리하기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="6c867-132">이벤트 허브는 처리 방법이 중요하지 않고 메시지가 성공적으로 전달될 수 있는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="6c867-133">이벤트 허브에는 여러 소비자 그룹에 이벤트를 스트림하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="6c867-134">이렇게 하면 이벤트를 완전히 다른 시스템에서 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="6c867-135">이렇게 하면 하나의 이벤트를 생성해야 하기 때문에 API 관리 서비스 내에서 API 요청의 처리가 추가적으로 지연되지 않고 다양한 통합 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="6c867-136">응용 프로그램/http 메시지를 보내는 정책</span><span class="sxs-lookup"><span data-stu-id="6c867-136">A policy to send application/http messages</span></span>
<span data-ttu-id="6c867-137">이벤트 허브는 이벤트 데이터를 간단한 문자열로 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="6c867-138">이 문자열의 내용은 오직 사용자의 몫입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="6c867-139">HTTP 요청을 패키지하고 이벤트 허브에 보낼 수 있으려면 요청 또는 응답 정보를 사용하여 문자열 형식을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="6c867-140">이런 경우에 다시 사용할 수 있는 기존 형식이 있는 경우 고유한 구문 분석 코드를 작성할 필요가 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="6c867-141">처음 필자는 HTTP 요청 및 응답을 보내는 데 [HAR](http://www.softwareishard.com/blog/har-12-spec/) 를 사용할 생각이었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="6c867-142">그러나 이 형식은 JSON 기반 형식에 일련의 HTTP 요청을 저장하도록 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="6c867-143">연결을 통해 HTTP 메시지를 전달하는 시나리오에 불필요 한 복잡성을 추가하는 여러 가지 필수 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="6c867-144">대체 옵션은 HTTP 사양 [RFC 7230](http://tools.ietf.org/html/rfc7230)에 설명된 대로 `application/http` 미디어 형식을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="6c867-145">이 미디어 형식은 연결을 통해 실제로 HTTP 메시지를 보내는 데 사용되는 것과 동일한 형식을 사용하지만 전체 메시지는 다른 HTTP 요청의 본문에 삽입될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="6c867-146">지금과 같은 경우에 본문을 메시지로 사용하여 이벤트 허브에 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="6c867-147">이 형식을 구문 분석하고 네이티브 `HttpRequestMessage` 및 `HttpResponseMessage` 개체로 변환할 수 있는 [Microsoft ASP.NET Web API 2.2 클라이언트](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) 라이브러리에 존재하는 파서입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="6c867-148">이 메시지를 만들 수 있게 되려면 Azure API 관리에서 C# 기반 [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx) 을 활용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="6c867-149">다음은 Azure 이벤트 허브에 HTTP 요청 메시지를 전송하는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="6c867-150">정책 선언</span><span class="sxs-lookup"><span data-stu-id="6c867-150">Policy declaration</span></span>
<span data-ttu-id="6c867-151">이 정책 식에 대한 몇 가지 특정 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="6c867-152">log-to-eventhub 정책에는 API 관리 서비스 내에서 생성된 로거의 이름을 의미하는 logger-id라는 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="6c867-153">API 관리 서비스에서 이벤트 허브 로거를 설정하는 방법에 대한 세부 정보는 [Azure API 관리에서 Azure 이벤트 허브에 이벤트를 기록하는 방법](api-management-howto-log-event-hubs.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="6c867-154">두 번째 특성은 메시지를 저장하도록 분할하는 이벤트 허브에 지시하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="6c867-155">이벤트 허브는 파티션을 사용하여 확장성을 사용하고 최소한 두 개가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="6c867-156">파티션 내에서 메시지의 순차적인 전달이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="6c867-157">이벤트 허브에 메시지를 저장할 파티션을 지정하지 않는 경우 라운드 로빈 알고리즘을 사용하여 로드를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="6c867-158">그러나 일부 메시지가 순서대로 처리되지 않는 경우가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="6c867-159">파티션</span><span class="sxs-lookup"><span data-stu-id="6c867-159">Partitions</span></span>
<span data-ttu-id="6c867-160">메시지가 순서대로 소비자에게 전달되고 파티션의 부하 배포 기능을 활용하려면 하나의 파티션에 HTTP 요청 메시지를 보내고 다른 파티션에 HTTP 응답 메시지를 보내도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="6c867-161">이렇게 하면 부하가 고르게 분산되고 모든 요청이 순서대로 사용되고 모든 응답도 순서대로 사용되도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="6c867-162">해당 요청 전에 응답이 사용될 수 있지만 응답에 대한 해당 요청이 다른 매커니즘을 가지고 해당 요청이 항상 응답 전에 온다면 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="6c867-163">HTTP 페이로드</span><span class="sxs-lookup"><span data-stu-id="6c867-163">HTTP payloads</span></span>
<span data-ttu-id="6c867-164">`requestLine` 을 빌드한 후에 요청 본문을 잘라냈는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="6c867-165">요청 본문은 1024에만 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="6c867-166">이는 증가할 수 있지만 개별 이벤트 허브 메시지는 256KB로 제한되므로 일부 HTTP 메시지 본문은 단일 메시지에 적합하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="6c867-167">로깅 및 분석을 수행할 때 상당한 양의 정보는 HTTP 요청 라인 및 헤더에서 파생될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="6c867-168">또한 많은 API 요청이 적은 본문을 반환하므로 큰 본문을 자르는 것으로 인한 정보 값의 손실은 모든 본문 내용을 유지하기 위해 전송, 처리 및 저장에 드는 비용 감소에 비교하여 상당히 미미합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="6c867-169">본문을 처리하는 방법에서 한 가지 유의할 점은 본문 내용을 읽지만 백 엔드 API가 본문을 읽을 수 있기를 바라기 때문에 `true`을 As<string>() 메서드에 전달해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="6c867-170">이 메서드를 true로 전달하여 본문을 버퍼링하게 되므로 두 번 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="6c867-171">큰 파일을 업로드하거나 긴 폴링을 사용하는 API가 있는 경우 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="6c867-172">이러한 경우에 본문을 읽는 작업을 피하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="6c867-173">HTTP 헤더</span><span class="sxs-lookup"><span data-stu-id="6c867-173">HTTP headers</span></span>
<span data-ttu-id="6c867-174">HTTP 헤더는 간단한 키/값 쌍 형식인 메시지 형식을 통해 간단히 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="6c867-175">중요한 특정 보안 필드를 제거하여 불필요하게 자격 증명 정보가 누수되는 것을 방지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="6c867-176">분석을 위해 API 키 및 기타 자격 증명은 사용될 가능성이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="6c867-177">사용자 및 사용자가 사용하는 특정 제품에 대한 분석을 수행하려면 `context` 개체에서 얻고 해당 사항을 메시지에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="6c867-178">메시지 메타데이터</span><span class="sxs-lookup"><span data-stu-id="6c867-178">Message Metadata</span></span>
<span data-ttu-id="6c867-179">이벤트 허브로 보낼 전체 메시지를 작성할 때 첫 번째 줄은 실제 `application/http` 메시지의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="6c867-180">첫 번째 줄은 메시지가 응답에 대한 요청을 상호 연결하는 데 사용된 요청 또는 응답 메시지 및 메시지 ID로 구성된 추가 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="6c867-181">메시지 ID는 다음과 같이 다른 정책을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="6c867-182">요청 메시지를 만들고 응답이 반환될 때까지 변수에 저장한 다음 요청 및 응답을 단일 메시지로 전송했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="6c867-183">그러나 요청 및 응답을 독립적으로 전송하고 둘을 상호 연결하는 메시지 ID를 사용하여 메시지 순서를 유지 관리하는 동안 여러 파티션을 활용하는 기능과 같이 메시지 크기 면에서 유연성을 얻고 요청이 곧 로깅 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="6c867-184">또한 유효한 응답이 API 관리 서비스에서 발생한 심각한 요청 오류 때문에 이벤트 허브에 전송되지 않은 일부 시나리오가 있을 수 있지만 아직 요청한 기록은 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="6c867-185">HTTP 응답 메시지를 보내는 정책은 요청과 매우 유사하므로 완성된 정책 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="6c867-186">`set-variable` 정책은 `<inbound>` 섹션 및 `<outbound>` 섹션의 모든 `log-to-eventhub` 정책에서 액세스할 수 있는 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="6c867-187">이벤트 허브에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="6c867-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="6c867-188">Azure 이벤트 허브의 이벤트는 [AMQP 프로토콜](http://www.amqp.org/)를 사용하여 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="6c867-189">Microsoft 서비스 버스 팀 소비 이벤트를 쉽게 만드는 데 사용할 수 있는 클라이언트 라이브러리를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="6c867-190">지원되는 두 가지 방법 중에 하나는 *직접 소비자*가 되는 것이고 다른 하나는 `EventProcessorHost` 클래스를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="6c867-191">이러한 두 방법의 예는 [이벤트 허브 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="6c867-192">차이점은 간략하게 `Direct Consumer`가 완벽한 제어를 제공하고 `EventProcessorHost`가 일부 배관 작업을 수행하지만 이러한 이벤트를 처리하는 방법에 대 해 특정한 가정을 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="6c867-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="6c867-193">EventProcessorHost</span></span>
<span data-ttu-id="6c867-194">이 샘플에서는 간략한 설명을 위해 `EventProcessorHost`를 사용하지만 이는 이 특정 시나리오에 가장 적합한 선택 사항이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="6c867-195">`EventProcessorHost`는 특정 이벤트 프로세서 클래스 내에서 스레딩 문제를 걱정하지 않도록 하는 어려운 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="6c867-196">그러나 시나리오에서는 단순히 메시지를 다른 형식으로 변환하며 비동기 메서드를 사용하여 다른 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="6c867-197">공유 상태를 업데이트할 필요가 없기 때문에 따라서 스레딩 문제의 위험도 없습니다 </span><span class="sxs-lookup"><span data-stu-id="6c867-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="6c867-198">시나리오 중 대부분의 경우 `EventProcessorHost`은 아마도 최고의 선택이며 쉬운 옵션일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="6c867-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="6c867-199">IEventProcessor</span></span>
<span data-ttu-id="6c867-200">`EventProcessorHost`를 사용하할 때 중앙 개념은 `ProcessEventAsync` 메서드를 포함하는 `IEventProcessor` 인터페이스를 구현하도록 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="6c867-201">해당 메서드의 핵심은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-201">The essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="6c867-202">EventData 개체의 목록이 메서드로 전달되고 해당 목록을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="6c867-203">각 메서드의 바이트는 HttpMessage 개체로 구문 분석되고 해당 개체는 IHttpMessageProcessor의 인스턴스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="6c867-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="6c867-204">HttpMessage</span></span>
<span data-ttu-id="6c867-205">`HttpMessage` 인스턴스는 세 가지 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-205">The `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="6c867-206">`HttpMessage` 인스턴스는 개체가 HttpRequestMessage 및 HttpResponseMessage의 인스턴스를 포함하는지를 식별하는 해당 HTTP 응답 및 부울 값에 HTTP 요청을 연결하도록 하는  `MessageId` GUID를 포함합니다. </span><span class="sxs-lookup"><span data-stu-id="6c867-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="6c867-207">`System.Net.Http`에서 기본 제공 HTTP 클래스를 사용하여 `System.Net.Http.Formatting`에 포함된 코드의 `application/http` 구문을 분석하도록 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="6c867-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="6c867-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="6c867-209">`HttpMessage` 인스턴스는 Azure 이벤트 허브에서 이벤트의 수신 및 해석을 분리하고 실제 처리를 위해 만든 인터페이스인 `IHttpMessageProcessor`를 구현하는 데 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="6c867-210">HTTP 메시지 전달</span><span class="sxs-lookup"><span data-stu-id="6c867-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="6c867-211">이 샘플의 경우 [Runscope](http://www.runscope.com)를 통해 HTTP 요청을 푸시해보면 흥미로울 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="6c867-212">Runscope는 HTTP 디버깅, 로깅 및 모니터링을 전문으로 하는 클라우드 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="6c867-213">무료 계층이 있으므로 시도하기 쉽고 API 관리 서비스를 통해 실시간 흐름에서 HTTP 요청을 볼 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="6c867-214">`IHttpMessageProcessor` 구현은 다음과 같습니다</span><span class="sxs-lookup"><span data-stu-id="6c867-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="6c867-215">해당 서비스에 `HttpRequestMessage` 및 `HttpResponseMessage` 인스턴스를 쉽게 푸시하도록 하는 [Runscope용 기존 클라이언트 라이브러리](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha)를 활용할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="6c867-216">Runscope API에 액세스하기 위해 계정 및 API 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="6c867-217">API 키를 가져오는 지침은 [Runscope API에 액세스하는 응용 프로그램 만들기](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) 동영상 가이드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="6c867-218">전체 샘플</span><span class="sxs-lookup"><span data-stu-id="6c867-218">Complete sample</span></span>
<span data-ttu-id="6c867-219">샘플의 [원본 코드](https://github.com/darrelmiller/ApimEventProcessor) 및 테스트는 GitHub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="6c867-220">[API 관리 서비스](api-management-get-started.md), [연결된 이벤트 허브](api-management-howto-log-event-hubs.md) 및 [저장소 계정](../storage/common/storage-create-storage-account.md)이 있어야 스스로 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="6c867-221">샘플은 이벤트 허브에서 들어오는 이벤트를 수신하는 간단한 콘솔 응용 프로그램으로 해당 이벤트를 `HttpRequestMessage` 및 `HttpResponseMessage` 개체에 변환한 다음 Runscope API에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="6c867-222">다음 애니메이션 이미지에서 개발자 포털에서 API에 생성된 요청과 수신, 처리 및 전달된 메시지를 보여주는 콘솔 응용 프로그램 그리고 Runscope 트래픽 관리자에 표시되는 요청 및 응답을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Runscope에 전달된 요청의 데모](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="6c867-224">요약</span><span class="sxs-lookup"><span data-stu-id="6c867-224">Summary</span></span>
<span data-ttu-id="6c867-225">Azure API 관리 서비스는 API간을 이동하는 HTTP 트래픽을 캡처하기 위한 최적의 장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="6c867-226">Azure 이벤트 허브는 해당 트래픽을 캡처하고 로깅, 모니터링 및 기타 복잡한 분석하는 보조 처리 시스템에 전달하기 위한 뛰어난 확장성을 가진 저렴한 비용의 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="6c867-227">Runscope와 같은 타사 트래픽 모니터링 시스템에 연결하는 작업은 간단히 수 십 줄의 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c867-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c867-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c867-228">Next steps</span></span>
* <span data-ttu-id="6c867-229">Azure 이벤트 허브에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="6c867-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="6c867-230">Azure 이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="6c867-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="6c867-231">EventProcessorHost를 사용하여 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="6c867-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="6c867-232">이벤트 허브 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="6c867-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="6c867-233">API 관리 및 이벤트 허브 통합에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="6c867-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="6c867-234">Azure API 관리에서 Azure 이벤트 허브에 이벤트를 기록하는 방법</span><span class="sxs-lookup"><span data-stu-id="6c867-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="6c867-235">로거 엔터티 참조</span><span class="sxs-lookup"><span data-stu-id="6c867-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="6c867-236">log-to-eventhub 정책 참조</span><span class="sxs-lookup"><span data-stu-id="6c867-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
