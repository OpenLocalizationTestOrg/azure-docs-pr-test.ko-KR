---
title: "Azure Service Fabric 역방향 프록시 | Microsoft Docs"
description: "Service Fabric의 역방향 프록시를 사용하여 클러스터 내부 및 외부에서 마이크로 서비스와 통신"
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="af0d8-103">Azure Service Fabric의 역방향 프록시</span><span class="sxs-lookup"><span data-stu-id="af0d8-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="af0d8-104">Azure Service Fabric에 기본 제공되는 역방향 프록시에서는 HTTP 끝점을 노출하는 Service Fabric 클러스터의 마이크로 서비스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="af0d8-105">마이크로 서비스 통신 모델</span><span class="sxs-lookup"><span data-stu-id="af0d8-105">Microservices communication model</span></span>
<span data-ttu-id="af0d8-106">Service Fabric의 마이크로 서비스는 일반적으로 가상 컴퓨터의 일부를 클러스터에서 실행하고 여러 가지 이유로 한 가상 컴퓨터를 다른 VM으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="af0d8-107">따라서 마이크로 서비스에 대한 끝점은 동적으로 변할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="af0d8-108">마이크로 서비스와 통신하는 일반적인 패턴은 다음 확인 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="af0d8-109">처음에는 이름 지정 서비스를 통해 서비스 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="af0d8-110">서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-110">Connect to the service.</span></span>
3. <span data-ttu-id="af0d8-111">연결 실패의 원인을 결정하고 필요한 경우 서비스 위치를 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="af0d8-112">이 프로세스는 일반적으로 서비스 확인 및 재시도 정책을 구현하는 재시도 루프에 클라이언트 쪽 통신 라이브러리의 매핑을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="af0d8-113">자세한 내용은 [서비스와 연결 및 통신](service-fabric-connect-and-communicate-with-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af0d8-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="af0d8-114">역방향 프록시를 사용하여 통신</span><span class="sxs-lookup"><span data-stu-id="af0d8-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="af0d8-115">Service Fabric의 역방향 프록시는 클러스터의 모든 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="af0d8-116">클라이언트를 대신하여 전체 서비스 확인 프로세스를 수행한 다음 클라이언트 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="af0d8-117">따라서 클러스터에서 실행되는 클라이언트는 클라이언트 쪽 HTTP 통신 라이브러리를 사용하여 동일한 노드에서 로컬로 실행되는 역방향 프록시를 사용하여 대상 서비스와 대화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![내부 통신][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="af0d8-119">클러스터 외부에서 마이크로 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="af0d8-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="af0d8-120">마이크로 서비스에 대한 기본 외부 통신 모델은 옵트인 모델이며, 여기서 각 서비스는 외부 클라이언트에서 직접 액세스될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="af0d8-121">마이크로 서비스와 외부 클라이언트 간의 네트워크 경계인 [Azure Load Balancer](../load-balancer/load-balancer-overview.md)는 네트워크 주소 변환을 수행하고 외부 요청을 내부 IP:port 끝점에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="af0d8-122">마이크로 서비스의 끝점에서 외부 클라이언트에 직접 액세스할 수 있도록 하려면 먼저 클러스터의 서비스가 사용하는 각 포트에 트래픽을 전달하도록 부하 분산 장치를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="af0d8-123">그뿐 아니라 대부분 마이크로 서비스( 특히 상태 저장 마이크로 서비스)가 클러스터의 모든 노드에 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="af0d8-124">마이크로 서비스는 장애 조치(Failover) 시 노드 간을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="af0d8-125">이러한 경우 부하 분산 장치를 트래픽을 전달할 복제본의 대상 노드 위치를 효과적으로 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="af0d8-126">클러스터 외부에서 역방향 프록시를 통해 마이크로 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="af0d8-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="af0d8-127">부하 분산 장치에서 개별 서비스의 포트를 구성하는 대신, 부하 분산 장치에서 역방향 프록시 포트만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="af0d8-128">이 구성을 사용하면 클러스터 외부의 클라이언트가 추가 구성 없이 역방향 프록시를 사용하여 클러스터 내부의 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![외부 통신][0]

> [!WARNING]
> <span data-ttu-id="af0d8-130">부하 분산 장치에서 역방향 프록시의 포트를 구성하면 HTTP 끝점을 표시하는 클러스터의 모든 마이크로 서비스의 주소를 클러스터 외부에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="af0d8-131">역방향 프록시를 사용하여 서비스 주소를 지정하기 위한 URI 형식</span><span class="sxs-lookup"><span data-stu-id="af0d8-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="af0d8-132">역방향 프록시는 특정 URI(Uniform Resource Identifier) 형식을 사용하여 수신 요청을 전달해야 하는 서비스 파티션을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="af0d8-133">**http(s):** 역방향 프록시를HTTP 또는 HTTPS 트래픽을 허용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="af0d8-134">HTTPS 전달의 경우 HTTPS에서 수신 대기하도록 역방향 프록시가 설정되면 [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md)(역방향 프록시를 사용하여 보안 서비스에 연결)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af0d8-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="af0d8-135">**클러스터 FQDN(정규화된 도메인 이름) | 내부 IP:** 외부 클라이언트의 경우 클러스터 도메인(예: mycluster.eastus.cloudapp.azure.com)을 통해 도달할 수 있도록 역방향 프록시를 구성할 수 있습니다. 기본적으로 역방향 프록시는 모든 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="af0d8-136">내부 트래픽의 경우 localhost 또는 모든 내부 노드 IP(예: 10.0.0.1)에서 역방향 프록시에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="af0d8-137">**포트:** 역방향 프록시에 대해 지정된 포트(예: 19081)입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="af0d8-138">**ServiceInstanceName:** "fabric:/" 체계 없이 연결하려고 하는 배포된 서비스 인스턴스의 정규화된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="af0d8-139">예를 들어 *fabric:/myapp/myservice/* 서비스에 연결하려면 *myapp/myservice*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="af0d8-140">서비스 인스턴스 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="af0d8-141">URL에서 서비스 인스턴스 이름의 대/소문자 표기가 달라지면 요청이 실패하고 404(찾을 수 없음)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="af0d8-142">**접미사 경로:** *myapi/values/add/3*과 같이 연결할 서비스에 대한 실제 URL 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="af0d8-143">**PartitionKey:** 분할 서비스의 경우 연결할 파티션의 계산된 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="af0d8-144">참고로 이는 파티션 ID GUID가 *아닙니다* .</span><span class="sxs-lookup"><span data-stu-id="af0d8-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="af0d8-145">이 매개 변수는 단일 파티션 체계를 사용하는 서비스에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="af0d8-146">**PartitionKind:** 서비스 파티션 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="af0d8-147">이는 'Int64Range' 또는 'Named'일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="af0d8-148">이 매개 변수는 단일 파티션 체계를 사용하는 서비스에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="af0d8-149">**ListenerName**: 서비스의 끝점 형식은 {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="af0d8-150">서비스에서 여러 끝점을 노출하는 경우 이 매개 변수는 클라이언트 요청을 전달해야 하는 끝점을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="af0d8-151">서비스에 수신기 하나만 있으면 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="af0d8-152">**TargetReplicaSelector**: 대상 복제본 또는 인스턴스를 선택하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="af0d8-153">대상 서비스가 상태 저장인 경우 TargetReplicaSelector는 'PrimaryReplica', 'RandomSecondaryReplica' 또는 'RandomReplica' 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="af0d8-154">이 매개 변수를 지정하지 않으면 기본값은 'PrimaryReplica'입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="af0d8-155">대상 서비스가 상태 비저장인 경우 역방향 프록시는 서비스 파티션의 임의 인스턴스를 선택하여 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="af0d8-156">**Timeout:** 서비스에 대한 역방향 프록시가 클라이언트 요청을 대신하여 만든 HTTP 요청에 대한 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="af0d8-157">기본값은 60초입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-157">The default value is 60 seconds.</span></span> <span data-ttu-id="af0d8-158">선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="af0d8-159">사용 예</span><span class="sxs-lookup"><span data-stu-id="af0d8-159">Example usage</span></span>
<span data-ttu-id="af0d8-160">예를 들어 다음 URL에서 HTTP 수신기를 여는 *fabric:/MyApp/MyService* 서비스를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="af0d8-161">다음은 서비스에 대한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="af0d8-162">서비스가 단일 분할 체계를 사용하는 경우 *PartitionKey* 및 *PartitionKind* 쿼리 문자열 매개 변수는 필요하지 않으며 다음과 같이 게이트웨이를 사용하여 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="af0d8-163">외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="af0d8-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="af0d8-164">내부에서: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="af0d8-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="af0d8-165">서비스가 Uniform Int64 분할 체계를 사용하는 경우 *PartitionKey* 및 *PartitionKind* 쿼리 문자열 매개 변수를 사용하여 서비스의 파티션에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="af0d8-166">외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="af0d8-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="af0d8-167">내부에서: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="af0d8-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="af0d8-168">서비스가 노출하는 리소스에 연결하려면 URL의 서비스 이름 뒤에 리소스 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="af0d8-169">외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="af0d8-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="af0d8-170">내부에서: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="af0d8-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="af0d8-171">그러면 게이트웨이가 이 요청을 서비스의 URL에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="af0d8-172">포트 공유 서비스에 대한 특수 처리</span><span class="sxs-lookup"><span data-stu-id="af0d8-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="af0d8-173">Azure Application Gateway는 서비스 주소의 다시 확인을 시도하고 서비스에 연결할 수 없는 경우 요청을 재시도합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="af0d8-174">이는 클라이언트 코드가 자체 서비스 확인 및 확인 루프를 구현할 필요가 없으므로 Application Gateway의 주요 이점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="af0d8-175">일반적으로 서비스에 연결할 수 없는 경우 서비스 인스턴스 또는 복제가 일반적인 수명 주기의 일부로 다른 노드로 이동된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="af0d8-176">이 경우 Application Gateway는 끝점이 더 이상 원래 확인된 주소에 열려 있지 않음을 나타내는 네트워크 연결 오류를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="af0d8-177">그러나 복제 또는 서비스 인스턴스는 호스트 프로세스를 공유할 수 있으며 다음을 비롯하여 http.sys 기반 웹 서버에 의해 호스팅될 경우 포트를 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="af0d8-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="af0d8-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="af0d8-179">ASP.NET 코어 WebListener</span><span class="sxs-lookup"><span data-stu-id="af0d8-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="af0d8-180">카타나</span><span class="sxs-lookup"><span data-stu-id="af0d8-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="af0d8-181">이 상황에서 웹 서버는 호스트 프로세스에서 사용할 수 있고 요청에 응답할 가능성이 있지만 확인된 서비스 인스턴스 또는 복제는 더 이상 호스트에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="af0d8-182">이 경우 게이트웨이는 웹 서버에서 HTTP 404 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="af0d8-183">따라서 HTTP 404에는 다음과 같은 두 가지 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="af0d8-184">사례 #1: 서비스 주소가 올바르지만 사용자가 요청한 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="af0d8-185">사례 #2: 서비스 주소가 올바르지 않고 사용자가 요청한 리소스가 다른 노드에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="af0d8-186">첫 번째 경우는 사용자 오류로 간주되는 일반적인 HTTP 404입니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="af0d8-187">그러나 두 번째 경우에 사용자는 존재하는 리소스를 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="af0d8-188">서비스 자체가 이동되었으므로 Application Gateway에서 해당 서비스를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="af0d8-189">Application Gateway는 주소를 다시 확인하고 요청을 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="af0d8-190">그러므로 Application Gateway는 두 경우를 구별하는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="af0d8-191">이러한 구별을 하려면 서버에서 제공하는 힌트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="af0d8-192">기본적으로 Application Gateway는 사례 # 2를 가정하여 요청을 다시 확인하고 다시 실행하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="af0d8-193">Application Gateway에 대해 사례 #1을 나타내려면 서비스가 다음과 같은 HTTP 응답 헤더를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="af0d8-194">이 HTTP 응답 헤더는 요청한 리소스가 존재하지 않는 일반적인 HTTP 404 상황을 나타내며, Application Gateway는 서비스 주소를 다시 확인하려고 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="af0d8-195">설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="af0d8-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="af0d8-196">Azure Portal을 통해 역방향 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="af0d8-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="af0d8-197">Azure Portal은 새 Service Fabric 클러스터를 만드는 동안 역방향 프록시를 사용하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="af0d8-198">**Service Fabric 클러스터 만들기**, 2단계: 클러스터 구성, 노드 유형 구성에서 "역방향 프록시 사용"으로 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="af0d8-199">보안 역방향 프록시를 구성하기 위해 SSL 인증서는 3단계: 보안, 클러스터 보안 설정 구성에서 지정되고, "역방향 프록시에 대한 SSL 인증서 포함" 확인란을 선택하고, 인증서 세부 정보를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="af0d8-200">Azure Resource Manager 템플릿을 통해 역방향 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="af0d8-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="af0d8-201">[Azure Resource Manager 템플릿](service-fabric-cluster-creation-via-arm.md)을 사용하여 클러스터에 대해 Service Fabric의 역방향 프록시를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="af0d8-202">인증서로 보안 역방향 프록시를 구성하고 인증서 롤오버를 처리하기 위한 Azure Resource Manager 템플릿 샘플에 대해서는 [보안 클러스터에서 HTTPS 역방향 프록시 구성](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af0d8-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="af0d8-203">먼저 배포하려는 클러스터에 대한 템플릿을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="af0d8-204">예제 템플릿을 사용하거나 사용자 지정 Resource Manager 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="af0d8-205">그런 후 다음 단계를 사용하여 역방향 프록시를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="af0d8-206">템플릿의 [매개 변수 섹션](../azure-resource-manager/resource-group-authoring-templates.md) 에서 역방향 프록시에 대한 포트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="af0d8-207">**클러스터** [리소스 형식 섹션](../azure-resource-manager/resource-group-authoring-templates.md)에서 각 nodetype 개체에 대한 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="af0d8-208">포트는 reverseProxyEndpointPort라는 매개 변수 이름으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="af0d8-209">Azure 클러스터 외부에서 역방향 프록시 주소를 지정하려면 1단계에서 지정한 포트에 대해 Azure Load Balancer 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="af0d8-210">역방향 프록시에 대한 포트에서 SSL 인증서를 구성하려면 **클러스터** [리소스 형식 섹션](../resource-group-authoring-templates.md)에서 해당 인증서를 ***reverseProxyCertificate*** 속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="af0d8-211">클러스터 인증서와 다른 역방향 프록시 인증서 지원</span><span class="sxs-lookup"><span data-stu-id="af0d8-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="af0d8-212">역방향 프록시 인증서가 클러스터를 보호하는 인증서와 다른 경우 이전에 지정한 인증서를 가상 컴퓨터에 설치하고 ACL(액세스 제어 목록)에 추가하여 Service Fabric에서 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="af0d8-213">이 작업은 **virtualMachineScaleSets** [리소스 형식 섹션](../resource-group-authoring-templates.md)에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="af0d8-214">설치의 경우 해당 인증서를 osProfile에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="af0d8-215">템플릿의 확장 섹션은 ACL의 인증서를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-215">The extension section of the template can update the certificate in the ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="af0d8-216">클러스터 인증서와 다른 인증서를 사용하여 기존 클러스터에서 역방향 프록시를 사용하도록 설정하는 경우 먼저 역방향 프록시를 사용하도록 설정하기 전에 클러스터에 역방향 프록시 인증서를 설치하고 ACL을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="af0d8-217">배포를 시작하여 1-4 단계를 통해 역방향 프록시를 사용하도록 설정하기 전에 위에서 언급한 설정을 사용하여 [Azure Resource Manager 템플릿](service-fabric-cluster-creation-via-arm.md) 배포를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="af0d8-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af0d8-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af0d8-218">Next steps</span></span>
* <span data-ttu-id="af0d8-219">[GitHub의 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)에서 서비스 간 HTTP 통신의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af0d8-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="af0d8-220">역방향 프록시를 사용하여 보안 HTTP 서비스에 전달</span><span class="sxs-lookup"><span data-stu-id="af0d8-220">Forwarding to secure HTTP service with the reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="af0d8-221">Reliable Services 원격을 사용하여 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="af0d8-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="af0d8-222">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="af0d8-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="af0d8-223">Reliable Services를 사용한 WCF 통신</span><span class="sxs-lookup"><span data-stu-id="af0d8-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="af0d8-224">추가적인 역방향 프록시 구성 옵션은 [Service Fabric 클러스터 설정 사용자 지정](service-fabric-cluster-fabric-settings.md)의 응용 프로그램 게이트웨이/HTTP 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af0d8-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
