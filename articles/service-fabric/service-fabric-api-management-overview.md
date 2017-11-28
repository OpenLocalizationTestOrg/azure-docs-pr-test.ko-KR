---
title: "Azure Service Fabric 및 API Management 개요 | Microsoft Docs"
description: "이 문서에서는 Service Fabric 응용 프로그램에 대한 게이트웨이로 Azure API Management를 사용하는 것을 소개합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: a3eedacac5efb53f82e46a56285713dece56ffe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a><span data-ttu-id="f08e1-103">Service Fabric 및 API Management 개요</span><span class="sxs-lookup"><span data-stu-id="f08e1-103">Service Fabric with Azure API Management overview</span></span>

<span data-ttu-id="f08e1-104">일반적으로 클라우드 응용 프로그램에는 사용자, 장치 또는 기타 응용 프로그램 수신을 위한 단일 지점을 제공하는 프런트 엔드 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-104">Cloud applications typically need a front-end gateway to provide a single point of ingress for users, devices, or other applications.</span></span> <span data-ttu-id="f08e1-105">Service Fabric에서 게이트웨이는 [ASP.NET Core 응용 프로그램](service-fabric-reliable-services-communication-aspnetcore.md), 트래픽 수신을 위해 설계된 기타 서비스(예: [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/), [Azure API Management](https://docs.microsoft.com/azure/api-management/))와 같은 상태 비저장 서비스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-105">In Service Fabric, a gateway can be any stateless service such as an [ASP.NET Core application](service-fabric-reliable-services-communication-aspnetcore.md), or another service designed for traffic ingress, such as [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/), or [Azure API Management](https://docs.microsoft.com/azure/api-management/).</span></span>

<span data-ttu-id="f08e1-106">이 문서에서는 Service Fabric 응용 프로그램에 대한 게이트웨이로 Azure API Management를 사용하는 것을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-106">This article is an introduction to using Azure API Management as a gateway to your Service Fabric applications.</span></span> <span data-ttu-id="f08e1-107">API Management는 Service Fabric과 직접 통합되므로 다양한 라우팅 규칙 집합을 사용하여 백 엔드 Service Fabric 서비스에 API를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-107">API Management integrates directly with Service Fabric, allowing you to publish APIs with a rich set of routing rules to your back-end Service Fabric services.</span></span> 

## <a name="architecture"></a><span data-ttu-id="f08e1-108">아키텍처</span><span class="sxs-lookup"><span data-stu-id="f08e1-108">Architecture</span></span>
<span data-ttu-id="f08e1-109">공통 Service Fabric 아키텍처는 HTTP API를 노출하는 백 엔드 서비스에 HTTP 호출을 수행하는 단일 페이지 웹 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-109">A common Service Fabric architecture uses a single-page web application that makes HTTP calls to back-end services that expose HTTP APIs.</span></span> <span data-ttu-id="f08e1-110">[Service Fabric 시작 응용 프로그램 예제](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)는 이 아키텍처의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-110">The [Service Fabric getting-started sample application](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) shows an example of this architecture.</span></span>

<span data-ttu-id="f08e1-111">이 시나리오에서는 상태 비저장 웹 서비스가 Service Fabric 응용 프로그램에 대한 게이트웨이로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-111">In this scenario, a stateless web service serves as the gateway into the Service Fabric application.</span></span> <span data-ttu-id="f08e1-112">이 방법에서는 다음 다이어그램에 표시된 것처럼 HTTP 요청을 백 엔드 서비스로 프록시할 수 있는 웹 서비스를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-112">This approach requires you to write a web service that can proxy HTTP requests to back-end services, as shown in the following diagram:</span></span>

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-web-app-stateless-gateway]

<span data-ttu-id="f08e1-114">응용 프로그램이 복잡해짐에 따라 다양한 백 엔드 서비스 앞에 API를 제공해야 하는 게이트웨이도 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-114">As applications grow in complexity, so do the gateways that must present an API in front of myriad back-end services.</span></span> <span data-ttu-id="f08e1-115">Azure API Management는 최소한의 작업으로 라우팅 규칙, 액세스 제어, 속도 제한, 모니터링, 이벤트 로깅 및 응답 캐싱 등 복잡한 API를 처리하기 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-115">Azure API Management is designed to handle complex APIs with routing rules, access control, rate limiting, monitoring, event logging, and response caching with minimal work on your part.</span></span> <span data-ttu-id="f08e1-116">Azure API Management는 Service Fabric 서비스 검색, 파티션 확인, 요청을 Service Fabric의 백 엔드 서비스에 지능적으로 직접 라우팅할 복제본 선택을 지원하므로 사용자 고유의 상태 비저장 API 게이트웨이를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-116">Azure API Management supports Service Fabric service discovery, partition resolution, and replica selection to intelligently route requests directly to back-end services in Service Fabric so you don't have to write your own stateless API gateway.</span></span> 

<span data-ttu-id="f08e1-117">이 시나리오에서 웹 UI는 여전히 웹 서비스를 통해 제공되지만 다음 다이어그램처럼 HTTP API 호출은 API Management를 통해 관리 및 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-117">In this scenario, the web UI is still served through a web service, while HTTP API calls are managed and routed through Azure API Management, as shown in the following diagram:</span></span>

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-web-app]

## <a name="application-scenarios"></a><span data-ttu-id="f08e1-119">응용 프로그램 시나리오</span><span class="sxs-lookup"><span data-stu-id="f08e1-119">Application scenarios</span></span>

<span data-ttu-id="f08e1-120">Service Fabric의 서비스는 상태 비저장 또는 상태 저장일 수 있으며 단일 항목, int-64 범위 및 이름 지정(named)의 3가지 체계 중 하나를 사용하여 분할될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-120">Services in Service Fabric may be either stateless or stateful, and they may be partitioned using one of three schemes: singleton, int-64 range, and named.</span></span> <span data-ttu-id="f08e1-121">서비스 끝점 확인을 사용하려면 특정 서비스 인스턴스의 특정 파티션을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-121">Service endpoint resolution requires identifying a specific partition of a specific service instance.</span></span> <span data-ttu-id="f08e1-122">서비스 끝점을 확인할 때는 서비스 인스턴스 이름(예: `fabric:/myapp/myservice`)과 서비스의 특정 파티션을 지정해야 합니다(단, 단일 파티션인 경우는 제외).</span><span class="sxs-lookup"><span data-stu-id="f08e1-122">When resolving an endpoint of a service, both the service instance name (for example, `fabric:/myapp/myservice`) as well as the specific partition of the service must be specified, except in the case of singleton partition.</span></span>

<span data-ttu-id="f08e1-123">상태 비저장 서비스, 상태 저장 서비스 및 모든 파티션 체계를 조합하여 Azure API Management를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-123">Azure API Management can be used with any combination of stateless services, stateful services, and any partitioning scheme.</span></span>

## <a name="send-traffic-to-a-stateless-service"></a><span data-ttu-id="f08e1-124">트래픽을 상태 비저장 서비스로 보내기</span><span class="sxs-lookup"><span data-stu-id="f08e1-124">Send traffic to a stateless service</span></span>

<span data-ttu-id="f08e1-125">가장 간단한 경우, 트래픽은 상태 비저장 서비스 인스턴스로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-125">In the simplest case, traffic is forwarded to a stateless service instance.</span></span> <span data-ttu-id="f08e1-126">이를 위해 API Management 작업에는 Service Fabric 백 엔드에서 특정 상태 비저장 서비스 인스턴스에 매핑되는 Service Fabric 백 엔드가 있는 인바운드 처리 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-126">To achieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps to a specific stateless service instance in the Service Fabric back-end.</span></span> <span data-ttu-id="f08e1-127">해당 서비스에 전송된 요청은 상태 비저장 서비스 인스턴스의 임의 복제본으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-127">Requests sent to that service are sent to a random replica of the stateless service instance.</span></span>

#### <a name="example"></a><span data-ttu-id="f08e1-128">예</span><span class="sxs-lookup"><span data-stu-id="f08e1-128">Example</span></span>
<span data-ttu-id="f08e1-129">다음 시나리오에서 Service Fabric 응용 프로그램에는 내부 HTTP API를 노출하는 `fabric:/app/fooservice` 이름의 상태 비저장 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-129">In the following scenario, a Service Fabric application contains a stateless service named `fabric:/app/fooservice`, that exposes an internal HTTP API.</span></span> <span data-ttu-id="f08e1-130">서비스 인스턴스 이름은 잘 알려져 있으며 API Management 인바운드 처리 정책에 직접 하드 코딩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-130">The service instance name is well known and can be hard-coded directly in the API Management inbound processing policy.</span></span> 

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-static-stateless]

## <a name="send-traffic-to-a-stateful-service"></a><span data-ttu-id="f08e1-132">트래픽을 상태 저장 서비스로 보내기</span><span class="sxs-lookup"><span data-stu-id="f08e1-132">Send traffic to a stateful service</span></span>

<span data-ttu-id="f08e1-133">상태 비저장 서비스 시나리오와 마찬가지로 트래픽을 상태 저장 서비스 인스턴스에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-133">Similar to the stateless service scenario, traffic can be forwarded to a stateful service instance.</span></span> <span data-ttu-id="f08e1-134">이 경우 API Management 작업에는 요청을 특정 *상태 저장* 서비스 인스턴스의 특정 파티션에 매핑하는 Service Fabric 백 엔드가 있는 인바운드 처리 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-134">In this case, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps a request to a specific partition of a specific *stateful* service instance.</span></span> <span data-ttu-id="f08e1-135">각 요청을 매핑할 파티션은 들어오는 HTTP 요청에서 입력(예: URL 경로의 값)을 사용하는 람다 메서드를 통해 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-135">The partition to map each request to is computed via a lambda method using some input from the incoming HTTP request, such as a value in the URL path.</span></span> <span data-ttu-id="f08e1-136">요청을 주 복제본에만 또는 읽기 작업을 위해 임의 복제본으로 보내도록 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-136">The policy may be configured to send requests to the primary replica only, or to a random replica for read operations.</span></span>

#### <a name="example"></a><span data-ttu-id="f08e1-137">예</span><span class="sxs-lookup"><span data-stu-id="f08e1-137">Example</span></span>

<span data-ttu-id="f08e1-138">다음 시나리오에서 Service Fabric 응용 프로그램에는 내부 HTTP API를 노출하는 `fabric:/app/userservice` 이름의 분할된 상태 저장 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-138">In the following scenario, a Service Fabric application contains a partitioned stateful service named `fabric:/app/userservice` that exposes an internal HTTP API.</span></span> <span data-ttu-id="f08e1-139">서비스 인스턴스 이름은 잘 알려져 있으며 API Management 인바운드 처리 정책에 직접 하드 코딩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-139">The service instance name is well known and can be hard-coded directly in the API Management inbound processing policy.</span></span>  

<span data-ttu-id="f08e1-140">서비스는 두 파티션을 포함하고 키 범위가 `Int64.MinValue` ~ `Int64.MaxValue`인 Int64 파티션 체계를 사용하여 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-140">The service is partitioned using the Int64 partition scheme with two partitions and a key range that spans `Int64.MinValue` to `Int64.MaxValue`.</span></span> <span data-ttu-id="f08e1-141">여기서 파티션 키 계산을 위해 어떤 알고리즘이라도 사용할 수 있지만, 백 엔드 정책은 URL 요청 경로에 제공된 `id` 값을 64비트 정수로 변환하여 해당 범위 내에서 파티션 키를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-141">The back-end policy computes a partition key within that range by converting the `id` value provided in the URL request path to a 64-bit integer, although any algorithm can be used here to compute the partition key.</span></span> 

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-static-stateful]

## <a name="send-traffic-to-multiple-stateless-services"></a><span data-ttu-id="f08e1-143">트래픽을 여러 상태 비저장 서비스로 보내기</span><span class="sxs-lookup"><span data-stu-id="f08e1-143">Send traffic to multiple stateless services</span></span>

<span data-ttu-id="f08e1-144">보다 고급 시나리오에서는 요청을 둘 이상의 서비스 인스턴스로 매핑하는 API Management 작업을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-144">In more advanced scenarios, you can define an API Management operation that maps requests to more than one service instance.</span></span> <span data-ttu-id="f08e1-145">이 경우 각 작업은 요청을 들어오는 HTTP 요청의 값(예: URL 경로 또는 쿼리 문자열, 상태 저장 서비스의 경우 서비스 인스턴스 내에 있는 파티션)에 따라 특정 서비스 인스턴스로 매핑하는 정책을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-145">In this case, each operation contains a policy that maps requests to a specific service instance based on values from the incoming HTTP request, such as the URL path or query string, and in the case of stateful services, a partition within the service instance.</span></span> 

<span data-ttu-id="f08e1-146">이를 위해 API Management 작업에는 들어오는 HTTP 요청에서 검색된 값에 따라 Service Fabric 백 엔드에서 상태 비저장 서비스 인스턴스에 매핑되는 Service Fabric 백 엔드가 있는 인바운드 처리 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-146">To achieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps to a stateless service instance in the Service Fabric back-end based on values retrieved from the incoming HTTP request.</span></span> <span data-ttu-id="f08e1-147">서비스 인스턴스에 대한 요청은 서비스 인스턴스의 임의 복제본으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-147">Requests to a service instance are sent to a random replica of the service instance.</span></span>

#### <a name="example"></a><span data-ttu-id="f08e1-148">예</span><span class="sxs-lookup"><span data-stu-id="f08e1-148">Example</span></span>

<span data-ttu-id="f08e1-149">이 예제에서는 응용 프로그램의 각 사용자에 대한 새로운 상태 비저장 서비스 인스턴스가 다음 수식을 사용하여 동적으로 생성된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-149">In this example, a new stateless service instance is created for each user of an application with a dynamically generated name using the following formula:</span></span>
 
 - `fabric:/app/users/<username>`

 <span data-ttu-id="f08e1-150">각 서비스에는 고유한 이름이 있지만 사용자 또는 관리자 입력에 대한 응답으로 서비스가 생성되어 APIM 정책이나 라우팅 규칙에 하드 코딩될 수 없기 때문에 이름을 미리 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-150">Each service has a unique name, but the names are not known up-front because the services are created in response to user or admin input and thus cannot be hard-coded into APIM policies or routing rules.</span></span> <span data-ttu-id="f08e1-151">대신, 요청을 보낼 서비스 이름은 URL 요청 경로에 제공된 `name` 값에서 백 엔드 정책 정의에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-151">Instead, the name of the service to which to send a request is generated in the back-end policy definition from the `name` value provided in the URL request path.</span></span> <span data-ttu-id="f08e1-152">예:</span><span class="sxs-lookup"><span data-stu-id="f08e1-152">For example:</span></span>

  - <span data-ttu-id="f08e1-153">`/api/users/foo`에 대한 요청은 서비스 인스턴스 `fabric:/app/users/foo`로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-153">A request to `/api/users/foo` is routed to service instance `fabric:/app/users/foo`</span></span>
  - <span data-ttu-id="f08e1-154">`/api/users/bar`에 대한 요청은 서비스 인스턴스 `fabric:/app/users/bar`로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-154">A request to `/api/users/bar` is routed to service instance `fabric:/app/users/bar`</span></span>

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-dynamic-stateless]

## <a name="send-traffic-to-multiple-stateful-services"></a><span data-ttu-id="f08e1-156">트래픽을 여러 상태 저장 서비스로 보내기</span><span class="sxs-lookup"><span data-stu-id="f08e1-156">Send traffic to multiple stateful services</span></span>

<span data-ttu-id="f08e1-157">상태 비저장 서비스 예제와 마찬가지로, API Management 작업에서 요청을 둘 이상의 **상태 저장** 서비스 인스턴스로 매핑할 수 있으며 이 경우 각 상태 저장 서비스 인스턴스에 대해 파티션 확인을 수행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-157">Similar to the stateless service example, an API Management operation can map requests to more than one **stateful** service instance, in which case you also may need to perform partition resolution for each stateful service instance.</span></span>

<span data-ttu-id="f08e1-158">이를 위해 API Management 작업에는 들어오는 HTTP 요청에서 검색된 값에 따라 Service Fabric 백 엔드에서 상태 저장 서비스 인스턴스에 매핑되는 Service Fabric 백 엔드가 있는 인바운드 처리 정책이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-158">To achieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps to a stateful service instance in the Service Fabric back-end based on values retrieved from the incoming HTTP request.</span></span> <span data-ttu-id="f08e1-159">요청을 특정 서비스 인스턴스에 매핑하는 것 외에도, 요청을 서비스 인스턴스 내의 특정 파티션이나 필요에 따라 해당 파티션 내의 주 복제본 또는 임의 보조 복제본에 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-159">In addition to mapping a request to specific service instance, the request can also be mapped to a specific partition within the service instance, and optionally to either the primary replica or a random secondary replica within the partition.</span></span>

#### <a name="example"></a><span data-ttu-id="f08e1-160">예</span><span class="sxs-lookup"><span data-stu-id="f08e1-160">Example</span></span>

<span data-ttu-id="f08e1-161">이 예제에서는 응용 프로그램의 각 사용자에 대한 새로운 상태 저장 서비스 인스턴스가 다음 수식을 사용하여 동적으로 생성된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-161">In this example, a new stateful service instance is created for each user of the application with a dynamically generated name using the following formula:</span></span>
 
 - `fabric:/app/users/<username>`

 <span data-ttu-id="f08e1-162">각 서비스에는 고유한 이름이 있지만 사용자 또는 관리자 입력에 대한 응답으로 서비스가 생성되어 APIM 정책이나 라우팅 규칙에 하드 코딩될 수 없기 때문에 이름을 미리 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-162">Each service has a unique name, but the names are not known up-front because the services are created in response to user or admin input and thus cannot be hard-coded into APIM policies or routing rules.</span></span> <span data-ttu-id="f08e1-163">대신, 요청을 보낼 서비스 이름은 URL 요청 경로에 제공된 `name` 값에서 백 엔드 정책 정의에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-163">Instead, the name of the service to which to send a request is generated in the back-end policy definition from the `name` value provided the URL request path.</span></span> <span data-ttu-id="f08e1-164">예:</span><span class="sxs-lookup"><span data-stu-id="f08e1-164">For example:</span></span>

  - <span data-ttu-id="f08e1-165">`/api/users/foo`에 대한 요청은 서비스 인스턴스 `fabric:/app/users/foo`로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-165">A request to `/api/users/foo` is routed to service instance `fabric:/app/users/foo`</span></span>
  - <span data-ttu-id="f08e1-166">`/api/users/bar`에 대한 요청은 서비스 인스턴스 `fabric:/app/users/bar`로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-166">A request to `/api/users/bar` is routed to service instance `fabric:/app/users/bar`</span></span>

<span data-ttu-id="f08e1-167">각 서비스 인스턴스는 두 파티션을 포함하고 키 범위가 `Int64.MinValue` ~ `Int64.MaxValue`인 Int64 파티션 체계를 사용해서도 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-167">Each service instance is also partitioned using the Int64 partition scheme with two partitions and a key range that spans `Int64.MinValue` to `Int64.MaxValue`.</span></span> <span data-ttu-id="f08e1-168">여기서 파티션 키 계산을 위해 어떤 알고리즘이라도 사용할 수 있지만, 백 엔드 정책은 URL 요청 경로에 제공된 `id` 값을 64비트 정수로 변환하여 해당 범위 내에서 파티션 키를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-168">The back-end policy computes a partition key within that range by converting the `id` value provided in the URL request path to a 64-bit integer, although any algorithm can be used here to compute the partition key.</span></span> 

![Service Fabric 및 Azure API Management 토폴로지 개요][sf-apim-dynamic-stateful]

## <a name="next-steps"></a><span data-ttu-id="f08e1-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f08e1-170">Next steps</span></span>

<span data-ttu-id="f08e1-171">[빠른 시작 가이드](service-fabric-api-management-quick-start.md)에 따라 API Management가 있는 첫 번째 Service Fabric 클러스터를 설정하고 API Management를 통해 서비스로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f08e1-171">Follow the [quick start guide](service-fabric-api-management-quick-start.md) to set up your first Service Fabric cluster with API Management and flow requests through API Management to your services.</span></span>

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png