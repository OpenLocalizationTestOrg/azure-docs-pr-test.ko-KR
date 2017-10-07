---
title: "Azure API 관리, 이벤트 허브와 Runscope Api aaaMonitor | Microsoft Docs"
description: "Azure API 관리, Azure 이벤트 허브 및 Runscope HTTP 로깅 및 모니터링에 대 한 연결 하 여 hello 로그 이벤트 허브 정책 보여 주는 샘플 응용 프로그램"
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
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="c13d3-103">Azure API 관리, 이벤트 허브 및 Runscope를 사용하여 API 모니터링</span><span class="sxs-lookup"><span data-stu-id="c13d3-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="c13d3-104">hello [API 관리 서비스](api-management-key-concepts.md) HTTP 전송 된 요청 tooyour HTTP API의 많은 기능 tooenhance hello 처리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="c13d3-105">그러나 hello 요청의 존재를 hello 및 응답은 일시적인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="c13d3-106">hello API 관리 서비스 tooyour 백 엔드 API 통해 전달 되며 hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="c13d3-107">API hello 요청을 처리 하 고 toohello API 소비자를 통해 다시 응답으로 흐르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="c13d3-108">API 관리 서비스 hello hello 게시자 포털 대시보드에서 하지만 그 외에도 표시 하기 위한 Api hello에 대 한 몇 가지 중요 한 통계를 유지, hello 내용은 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="c13d3-109">Hello를 사용 하 여 [로그-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [정책](api-management-howto-policies.md) hello API 관리 서비스에서에서 요청 및 응답 tooan hello에서에서 모든 세부 정보를 보낼 수 있습니다 [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="c13d3-110">다양 한 이유로 tooyour Api에 전송 되는 HTTP 메시지의 toogenerate 이벤트 경우가 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="c13d3-111">예에는 업데이트의 감사 내역, 사용 분석, 예외 경고 및 타사 통합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="c13d3-112">이 문서는 방법을 보여 주는 toocapture hello 전체 HTTP 요청 및 응답 메시지를 이벤트 허브 tooan 보낼 HTTP 로깅 및 모니터링 서비스를 제공 하는 해당 메시지 tooa 제 3 자 서비스를 릴레이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="c13d3-113">API 관리 서비스에서 전송되는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c13d3-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="c13d3-114">HTTP API 프레임 워크 toocapture HTTP 요청 및 응답에 연결 하 고 로깅 및 모니터링 시스템에 이러한를 제공할 수 있는 가능한 toowrite HTTP 미들웨어는</span><span class="sxs-lookup"><span data-stu-id="c13d3-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="c13d3-115">hello 단점은 toothis 방법은 hello HTTP 미들웨어 toobe hello 백 엔드 API에 통합 하며 hello API의 hello 플랫폼과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="c13d3-116">여러 Api 있는 경우 각각 hello 미들웨어를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="c13d3-117">백 엔드 API를 업데이트할 수 없는 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="c13d3-118">로깅 인프라와 Azure API 관리 서비스 toointegrate hello를 사용 하 여 중앙 집중식 및 플랫폼 독립적인 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="c13d3-119">부분적으로 인해 확장 가능한 이기도 toohello [지리적 복제](api-management-howto-deploy-multi-region.md) Azure API 관리의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="c13d3-120">Azure 이벤트 허브 tooan 보낼 이유는?</span><span class="sxs-lookup"><span data-stu-id="c13d3-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="c13d3-121">적절 한 tooask, 특정 tooAzure 이벤트 허브를가 하는 정책을 만드는 이유?</span><span class="sxs-lookup"><span data-stu-id="c13d3-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="c13d3-122">여러 다른 위치 toolog 내 요청 원하는 수 위치로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="c13d3-123">그 이유 hello toohello 최종 대상 직접 요청을 보내기만?</span><span class="sxs-lookup"><span data-stu-id="c13d3-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="c13d3-124">이것은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-124">That is an option.</span></span> <span data-ttu-id="c13d3-125">그러나 API 관리 서비스에서 로깅 요청을 만들 때는 필요한 tooconsider 로깅 메시지 hello API의 hello 성능이 어떻게 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="c13d3-126">로드의 점진적인 증가는 시스템 구성 요소에서 사용할 수 있는 인스턴스를 늘리거나 지역에서 복제를 활용하여 처리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="c13d3-127">그러나 짧은 트래픽 급증 요청 toologging 인프라 tooslow 부하 상태에서 시작 하는 경우 상당히 지연 요청 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="c13d3-128">hello Azure 이벤트 허브는 디자인 된 tooingress 엄청난 양의 데이터, HTTP hello 개수 보다 훨씬 더 높은 수가 이벤트를 처리 하기 위한 용량을 사용 하 여 대부분의 Api 프로세스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="c13d3-129">hello 이벤트 허브 API 관리 서비스 및 hello 인프라를 저장 하 고 hello 메시지를 처리 하는 사이 복잡 한 버퍼의 일종으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="c13d3-130">이렇게 하면 API 성능 toohello 로깅 인프라가 인해 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="c13d3-131">Hello 데이터 tooan 이벤트 허브를 전달한 후 유지 되 고 대기 이벤트 허브 소비자 tooprocess 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="c13d3-132">이벤트 허브 hello 처리 방법을 고려 하지 않고, 방금 hello 메시지가 성공적으로 전달 될 수 있도록 하는 방법에 대 한 관심이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="c13d3-133">이벤트 허브는 hello 기능 toostream 이벤트 toomultiple 소비자 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="c13d3-134">따라서 이벤트 toobe를 완전히 다른 시스템에서 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="c13d3-135">이렇게 하면 추가 지연이 발생 한 이벤트 생성 toobe 요구 사항에 맞춰 hello hello API 요청 hello API 관리 서비스 내에서 처리에 넣지 않고도 다양 한 통합 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="c13d3-136">정책 toosend 응용 프로그램/http 메시지</span><span class="sxs-lookup"><span data-stu-id="c13d3-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="c13d3-137">이벤트 허브는 이벤트 데이터를 간단한 문자열로 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="c13d3-138">이 문자열의 내용을 hello은 완전히 tooyou입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="c13d3-139">toobe 수 toopackage HTTP 요청 및 tooEvent tooformat hello 문자열 hello 요청 또는 응답 정보로 필요 허브 오프 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="c13d3-140">이와 같은 경우에는 기존 형식을에서는 다시 사용할 수 없는 경우 다음 म 없을 수 있습니다 toowrite 구문 분석 코드.</span><span class="sxs-lookup"><span data-stu-id="c13d3-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="c13d3-141">처음 I으로 간주 hello를 사용 하 여 [HAR](http://www.softwareishard.com/blog/har-12-spec/) HTTP 요청 및 응답을 보내기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="c13d3-142">그러나 이 형식은 JSON 기반 형식에 일련의 HTTP 요청을 저장하도록 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="c13d3-143">다양 한 hello 유선을 통해 HTTP hello 메시지를 전달 하는 hello 시나리오에 대 한 불필요 한 복잡성을 추가 하는 필수 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="c13d3-144">다른 옵션은 toouse hello `application/http` hello HTTP 사양에 설명 된 대로 미디어 유형 [RFC 7230](http://tools.ietf.org/html/rfc7230)합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="c13d3-145">미디어 유형은 사용 hello 정확히 동일한 형식 즉 tooactually 사용 되는 HTTP 메시지를 보내며 hello 유선으로 하지만 hello 전체 메시지 hello 다른 HTTP 요청 본문에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="c13d3-146">이 경우에만 하겠습니다 toouse hello 본문 우리의 메시지 toosend tooEvent 허브로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="c13d3-147">편리 하 게에 존재 하는 파서는 [Microsoft ASP.NET Web API 2.2 클라이언트](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) 이 형식을 구문 분석 하 고 hello 네이티브로 변환할 수 있는 라이브러리 `HttpRequestMessage` 및 `HttpResponseMessage` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="c13d3-148">toobe 수 toocreate이이 메시지의 C# 기반 tootake 이점은 필요 [정책 식을](https://msdn.microsoft.com/library/azure/dn910913.aspx) Azure API 관리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="c13d3-149">다음은 HTTP 요청 메시지 tooAzure 이벤트 허브를 전송 하는 hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="c13d3-150">정책 선언</span><span class="sxs-lookup"><span data-stu-id="c13d3-150">Policy declaration</span></span>
<span data-ttu-id="c13d3-151">이 정책 식에 대한 몇 가지 특정 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="c13d3-152">hello 로그 이벤트 허브 정책 toohello hello API 관리 서비스 내에서 생성 된로 거 이름을 참조 하는 거 id 라는 특성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="c13d3-153">어떻게 toosetup hello API 관리 서비스에는 이벤트 허브로 거 있습니다 hello 문서에 대 한 세부 정보를 hello [어떻게 toolog 이벤트 tooAzure Azure API 관리에서 이벤트 허브](api-management-howto-log-event-hubs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="c13d3-154">hello 두 번째 특성은 이벤트 허브 파티션 toostore hello 메시지에 지시 하는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="c13d3-155">이벤트 허브 파티션 tooenable scalabilty 사용 및 두 개 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="c13d3-156">파티션 내에서 메시지의 순차적 전달 hello 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="c13d3-157">파티션 tooplace hello 메시지에 이벤트 허브를 제시 하지 않는 म, 라운드 로빈 알고리즘 toodistribute hello 부하를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="c13d3-158">그러나 하는 순서와 다르게 처리 하는 메시지 toobe 중 일부를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="c13d3-159">파티션</span><span class="sxs-lookup"><span data-stu-id="c13d3-159">Partitions</span></span>
<span data-ttu-id="c13d3-160">toosend HTTP 요청 메시지 tooone 파티션 및 HTTP 응답 메시지 tooa 두 번째 파티션에 tooensure 메시지 tooconsumers 순서 대로 배달 됩니다 파티션의 hello 부하 배포 기능을 활용 하 고, 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="c13d3-161">이렇게 하면 부하가 고르게 분산되고 모든 요청이 순서대로 사용되고 모든 응답도 순서대로 사용되도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="c13d3-162">Hello 해당 요청을 하기 전에 사용 하는 응답 toobe에 대 한 있지만 아니므로 문제가 있으므로 연결 하기 위한 다른 메커니즘 tooresponses를 요청 하 고 요청 응답 하기 전에 항상 들어옵니다 있는지 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="c13d3-163">HTTP 페이로드</span><span class="sxs-lookup"><span data-stu-id="c13d3-163">HTTP payloads</span></span>
<span data-ttu-id="c13d3-164">Hello를 빌드한 후 `requestLine` hello 요청 본문을 잘라내야 하는 경우 toosee 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="c13d3-165">hello 요청 본문은 잘린된 tooonly 1024입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="c13d3-166">이 늘릴 수 없습니다, 개별 이벤트 허브 메시지 사항은 제한 too256KB 일부 HTTP 메시지 활동해왔습니다 단일 메시지에 적합 하지 않습니다는 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="c13d3-167">상당한 양의 정보를 로깅 및 분석을 수행 하는 경우는 방금 hello HTTP 요청 줄 및 헤더에서 파생 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="c13d3-168">또한 많은 API 요청 작은 본문 반환 및 전송의 비교 toohello 감소에 최소한으로 상당히 큰 본문을 잘라 정보 값 hello 손실 이므로 처리 및 저장소 비용이 tookeep 모든 본문 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="c13d3-169">Hello 본문을 처리 하는 방법에 대 한 한 가지 유의할 toopass 필요한은 `true` 으로 toohello<string>() 메서드가 hello 본문 콘텐츠를 읽을 것 때문에 하지만 서버가 이기도 원하는 hello 백 엔드 API toobe 수 tooread hello 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="c13d3-170">True toothis 메서드를 전달 하 여 hello 본문 toobe를 두 번 읽을 수 있도록 버퍼링 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="c13d3-171">이 중요 한 toobe 긴 폴링을 사용 하거나 매우 큰 파일 업로드를 하는 API가 있는 경우 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="c13d3-172">이러한 경우 최상의 tooavoid hello 본문을 전혀 읽고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="c13d3-173">HTTP 헤더</span><span class="sxs-lookup"><span data-stu-id="c13d3-173">HTTP headers</span></span>
<span data-ttu-id="c13d3-174">간단한 키/값 쌍 형식으로 hello 메시지 형식으로를 통해 HTTP 헤더를 단순히 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="c13d3-175">선택한 특정 보안을 확인할 toostrip 중요 한 필드, tooavoid 자격 증명 정보를 누출 불필요 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="c13d3-176">분석을 위해 API 키 및 기타 자격 증명은 사용될 가능성이 적습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="c13d3-177">Hello 사용자 및 hello 특정 제품에 toodo 분석 했는데도 사용 하는 경우 hello에서 신속 하 `context` 해당 toohello 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="c13d3-178">메시지 메타데이터</span><span class="sxs-lookup"><span data-stu-id="c13d3-178">Message Metadata</span></span>
<span data-ttu-id="c13d3-179">Hello 첫 번째 줄은 hello에 실제로 포함 되지 hello 메시지 전체 toosend toohello 이벤트 허브를 만들 때 `application/http` 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="c13d3-180">hello 첫 번째 줄은 여부 hello 메시지는 요청 또는 응답 메시지의 구성 된 추가 메타 데이터 및 사용 되는 toocorrelate 인 메시지 id tooresponses를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="c13d3-181">다음과 같은 다른 정책을 사용 하 여 hello 메시지 id는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="c13d3-182">저장 hello 될 때까지 변수 응답 반환 된 및 다음 단순히 hello 요청 및 응답 메시지로 보내도록 단일는 hello 요청 메시지를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="c13d3-183">그러나 hello 요청 및 응답을 독립적으로 전송 하 고 메시지 id toocorrelate를 사용 하 여 두 개를 hello, 얻을 수 있는 좀 더 유연 하 게 hello 메시지 크기, 여러 개의 파티션이 활용 기능 tootake hello 메시지 순서 및 hello 유지 관리 하는 동안 요청 더 빨리 우리의 로깅 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="c13d3-184">또한 있을 수 있습니다 유효한 응답 toohello 이벤트 허브 hello API 관리 서비스에서 심각한 요청 오류 tooa 인해 수 있는 전송 되지 않습니다 있었지만 아직 hello 요청에 대 한 기록을 몇 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="c13d3-185">hello 정책 toosend hello 응답 HTTP 메시지의 매우 유사한 toohello 요청 모양과 hello 완료 되도록 정책 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="c13d3-186">hello `set-variable` 정책 모두 hello에서 액세스할 수 있는 값을 만듭니다. `log-to-eventhub` hello에 대 한 정책 `<inbound>` 섹션과 hello `<outbound>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="c13d3-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="c13d3-187">이벤트 허브에서 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="c13d3-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="c13d3-188">Hello를 사용 하 여 Azure 이벤트 허브에서 이벤트를 받는 [AMQP 프로토콜](http://www.amqp.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="c13d3-189">hello Microsoft 서비스 버스 팀 내용을 클라이언트 라이브러리 사용 가능한 toomake hello 쉽게 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="c13d3-190">지원 되는 두 가지 방법, 되는 하나는 *직접 소비자* hello 다른 hello를 사용 하 고 `EventProcessorHost` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="c13d3-191">이 두 가지 방법의 예는 hello에서 확인할 수 있습니다 [이벤트 허브 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="c13d3-192">hello 짧은 길이의 hello 차이점은 `Direct Consumer` 을 사용 하면 완전히 제어 및 hello `EventProcessorHost` 하지만 해당 이벤트를 처리 방법에 대 한 특정 가정을 성에 대 한 hello 배관 작업의 일부를 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="c13d3-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c13d3-193">EventProcessorHost</span></span>
<span data-ttu-id="c13d3-194">그러나이 샘플에서는 hello 사용 `EventProcessorHost` 편의상 것 수 하지 hello이 특정 시나리오에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="c13d3-195">`EventProcessorHost`스레딩 특정 이벤트 프로세서 클래스 내에서 문제에 대 한 tooworry 없는의 복잡 한 작업을 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="c13d3-196">그러나이 시나리오에서 단순히 hello 메시지 tooanother 형식으로 변환 했으며 비동기 메서드를 사용 하 여 tooanother 서비스와 함께 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="c13d3-197">공유 상태를 업데이트할 필요가 없기 때문에 따라서 스레딩 문제의 위험도 없습니다 </span><span class="sxs-lookup"><span data-stu-id="c13d3-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="c13d3-198">대부분의 시나리오에 대 한 `EventProcessorHost` 는 hello 가장 적합 하 고 hello 쉽게 옵션으로는 확실히 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="c13d3-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="c13d3-199">IEventProcessor</span></span>
<span data-ttu-id="c13d3-200">사용 하는 경우 중앙 개념 hello `EventProcessorHost` toocreate는는 hello 구현의 `IEventProcessor` hello 방법을 포함 하는 인터페이스 `ProcessEventAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="c13d3-201">해당 메서드의 hello 핵심 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-201">hello essence of that method is shown here:</span></span>

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

<span data-ttu-id="c13d3-202">EventData 개체 목록이 hello 메서드에 전달 된 하 고 해당 목록을 반복 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="c13d3-203">각 방법의 hello 바이트 HttpMessage 개체로 구문 분석 하 고 해당 개체가 IHttpMessageProcessor tooan 인스턴스에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="c13d3-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="c13d3-204">HttpMessage</span></span>
<span data-ttu-id="c13d3-205">hello `HttpMessage` 인스턴스가 세 가지 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="c13d3-206">hello `HttpMessage` 인스턴스에 포함 되어는 `MessageId` toohello 해당 HTTP 응답 및 boolean 값 tooconnect hello HTTP 요청 수 있는 GUID hello 개체는 HttpRequestMessage의 인스턴스를 포함 하는 경우를 식별 하 고 HttpResponseMessage 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="c13d3-207">HTTP 클래스에 기본 제공 hello를 사용 하 여 `System.Net.Http`, 수 tootake hello 활용 하 봤습니다 `application/http` 에 포함 된 코드의 구문을 분석 `System.Net.Http.Formatting`합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="c13d3-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="c13d3-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="c13d3-209">hello `HttpMessage` 인스턴스의 tooimplementation 전달 `IHttpMessageProcessor` 만든 toodecouple hello 수신 호스트와 hello 이벤트 hello 및 Azure 이벤트 허브에서의 처리 실제 인터페이스인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="c13d3-210">Hello HTTP 메시지 전달</span><span class="sxs-lookup"><span data-stu-id="c13d3-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="c13d3-211">이 샘플에 대 한 하기로 결정 하는 것 흥미로운 toopush hello HTTP 요청을 통해 너무[Runscope](http://www.runscope.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="c13d3-212">Runscope는 HTTP 디버깅, 로깅 및 모니터링을 전문으로 하는 클라우드 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="c13d3-213">따라서 쉽게 tootry 되는 API 관리 서비스를 통해 실시간으로 흐르는에서 toosee hello HTTP 요청 수 있으며 무료 계층을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="c13d3-214">hello `IHttpMessageProcessor` 구현은, 다음과 같습니다</span><span class="sxs-lookup"><span data-stu-id="c13d3-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="c13d3-215">수 tootake 활용 하 봤습니다는 [Runscope 용 클라이언트 라이브러리를 기존](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) 쉽게 toopush 따라서 `HttpRequestMessage` 및 `HttpResponseMessage` 를 인스턴스 서비스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="c13d3-216">순서 대로 tooaccess 계정을 API 키가 필요 Runscope API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="c13d3-217">API 키를 가져오기 위한 지침은 hello에 [응용 프로그램 만들기 tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) 캐스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="c13d3-218">전체 샘플</span><span class="sxs-lookup"><span data-stu-id="c13d3-218">Complete sample</span></span>
<span data-ttu-id="c13d3-219">hello [소스 코드](https://github.com/darrelmiller/ApimEventProcessor) 및 GitHub에 있는 hello 샘플에 대 한 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="c13d3-220">해야 합니다는 [API 관리 서비스](api-management-get-started.md), [연결 된 이벤트 허브](api-management-howto-log-event-hubs.md), 및 [저장소 계정](../storage/common/storage-create-storage-account.md) toorun hello 샘플 자신에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="c13d3-221">hello 샘플은 방금 간단한 콘솔 응용 프로그램 이벤트 허브에서 오는 이벤트로 변환에 대 한 수신 대기 하는 `HttpRequestMessage` 및 `HttpResponseMessage` 개체 및 toohello Runscope API에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="c13d3-222">다음 애니메이션된 이미지 hello에서 tooan API hello hello 콘솔 응용 프로그램 표시 된 hello 메시지 수신, 개발자 포털에서에서 수행 하는 요청 처리 및 전달 되 고 다음 요청 및 응답 Runscope 트래픽 hello에 나타나 hello 볼 수 있습니다. 검사기입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![TooRunscope 전달 되 고 요청의 데모](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="c13d3-224">요약</span><span class="sxs-lookup"><span data-stu-id="c13d3-224">Summary</span></span>
<span data-ttu-id="c13d3-225">Azure API 관리 서비스 Api에서 tooand 여행는 간단 하 게 수행할 toocapture hello HTTP 트래픽을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="c13d3-226">Azure 이벤트 허브는 해당 트래픽을 캡처하고 로깅, 모니터링 및 기타 복잡한 분석하는 보조 처리 시스템에 전달하기 위한 뛰어난 확장성을 가진 저렴한 비용의 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="c13d3-227">Too3rd 파티 트래픽 모니터링으로 몇 십 개의 코드 줄은 단순 Runscope와 같은 시스템을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c13d3-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c13d3-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c13d3-228">Next steps</span></span>
* <span data-ttu-id="c13d3-229">Azure 이벤트 허브에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="c13d3-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="c13d3-230">Azure 이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="c13d3-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="c13d3-231">EventProcessorHost를 사용하여 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="c13d3-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="c13d3-232">이벤트 허브 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="c13d3-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="c13d3-233">API 관리 및 이벤트 허브 통합에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="c13d3-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="c13d3-234">어떻게 toolog 이벤트 tooAzure Azure API 관리에서 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="c13d3-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="c13d3-235">로거 엔터티 참조</span><span class="sxs-lookup"><span data-stu-id="c13d3-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="c13d3-236">log-to-eventhub 정책 참조</span><span class="sxs-lookup"><span data-stu-id="c13d3-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
