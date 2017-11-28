---
title: "서비스 패브릭 aaaAzure 역방향 프록시 | Microsoft Docs"
description: "서비스 패브릭 역방향 프록시를 사용 하 여 내부 및 외부 hello 클러스터에서 toomicroservices 통신에 대 한 합니다."
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
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="29b99-103">Azure Service Fabric의 역방향 프록시</span><span class="sxs-lookup"><span data-stu-id="29b99-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="29b99-104">Azure Service Fabric에 기본 제공 되는 역방향 프록시를 hello microservices HTTP 끝점을 노출 하는 hello 서비스 패브릭 클러스터에서 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="29b99-105">마이크로 서비스 통신 모델</span><span class="sxs-lookup"><span data-stu-id="29b99-105">Microservices communication model</span></span>
<span data-ttu-id="29b99-106">일반적으로 서비스 패브릭에서 Microservices hello 클러스터의 가상 컴퓨터의 하위 집합에서 실행 하 고 다양 한 이유로 하나의 가상 컴퓨터 tooanother에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="29b99-107">따라서 microservices에 대 한 hello 끝점 동적으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="29b99-108">hello 대부분의 일반적인 패턴 toocommunicate toohello 마이크로 서비스는 hello 다음 루프를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="29b99-109">Hello 명명 서비스를 통해 처음 hello 서비스 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="29b99-110">Toohello 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-110">Connect toohello service.</span></span>
3. <span data-ttu-id="29b99-111">Hello 연결 실패 원인을 확인 하 고 필요한 경우 hello 서비스 위치를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="29b99-112">이 프로세스는 일반적으로 hello 서비스 확인 및 다시 시도 정책을 구현 하는 다시 시도 루프에서 클라이언트 통신 라이브러리 래핑 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="29b99-113">자세한 내용은 [서비스와 연결 및 통신](service-fabric-connect-and-communicate-with-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29b99-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="29b99-114">Hello 역방향 프록시를 사용 하 여 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="29b99-115">서비스 패브릭에서 역방향 프록시 hello hello 클러스터의 모든 hello 노드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="29b99-116">클라이언트를 대신 하 여 hello 전체 서비스 확인 프로세스를 수행 하 고 hello 클라이언트 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="29b99-117">따라서 hello 클러스터에서 실행 하는 클라이언트에서 로컬로 실행 hello 동일한 노드는 hello 역방향 프록시를 사용 하 여 클라이언트 쪽 HTTP 통신 라이브러리 tootalk toohello 대상 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![내부 통신][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="29b99-119">Hello 클러스터 외부에서 microservices 도달</span><span class="sxs-lookup"><span data-stu-id="29b99-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="29b99-120">microservices hello 기본 외부 통신 모델은 외부 클라이언트에서 직접 각 서비스에 액세스할 수 없는 옵트인 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="29b99-121">[Azure 부하 분산 장치](../load-balancer/load-balancer-overview.md)microservices와 외부 클라이언트 간의 네트워크 경계는 네트워크 주소 변환 하 고 수행한 전달 외부 toointernal ip: port 끝점 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="29b99-122">toomake 마이크로 서비스의 끝점 tooexternal 직접 액세스할 수 있는 클라이언트를 먼저 구성 해야 tooforward 트래픽 tooeach 포트 서비스 hello를 사용 하 여 부하 분산 장치 hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="29b99-123">또한 대부분 microservices, 상태 저장 microservices 특히 hello 클러스터의 모든 노드에서 실시간 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="29b99-124">hello microservices 장애 조치 노드 간에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="29b99-125">이러한 경우 부하 분산 장치 결정할 수 없습니다 효율적으로 hello 위치 hello 복제본 toowhich hello 대상 노드의 트래픽을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="29b99-126">Hello 외부 hello 클러스터에서 역방향 프록시를 통해 microservices 도달</span><span class="sxs-lookup"><span data-stu-id="29b99-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="29b99-127">부하 분산 장치에서 개별 서비스의 hello 포트를 구성 하는 대신 부하 분산 장치에만 hello 포트 hello 역방향 프록시를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="29b99-128">이 구성을 통해 hello 클러스터 외부의 클라이언트가 추가 구성 없이 hello 역방향 프록시를 사용 하 여 hello 클러스터 내 서비스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![외부 통신][0]

> [!WARNING]
> <span data-ttu-id="29b99-130">부하 분산 장치에서 hello 역방향 프록시 포트를 구성 하는 경우 HTTP 끝점을 노출 하는 hello 클러스터의 모든 microservices hello 클러스터 외부에서 주소 지정 가능한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="29b99-131">Hello 역방향 프록시를 사용 하 여 서비스를 해결 하기 위한 URI 형식</span><span class="sxs-lookup"><span data-stu-id="29b99-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="29b99-132">hello 역방향 프록시 사용 하 여 특정 uniform 리소스 URI (identifier) 형식 tooidentify hello 서비스 파티션 toowhich hello 들어오는 요청을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="29b99-133">**http (s):** hello 역방향 프록시 구성된 tooaccept HTTP 또는 HTTPS 트래픽이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="29b99-134">HTTPS 전달 하기 위해 참조 너무[hello 역방향 프록시를 사용 하 여 보안 서비스 tooa 연결](service-fabric-reverseproxy-configure-secure-communication.md) HTTPS에 대해 역방향 프록시 설치 toolisten를 설정한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="29b99-135">**클러스터 정규화 된 도메인 이름 (FQDN) | 내부 IP:** 외부 클라이언트에 대해 구성할 수 있습니다 hello 역방향 프록시 mycluster.eastus.cloudapp.azure.com 같은 hello 클러스터 도메인을 통해 연결할 수 있도록 합니다. 기본적으로 모든 노드에 대해 hello 역방향 프록시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="29b99-136">내부 트래픽에 대 한 역방향 프록시 hello 10.0.0.1와 같은 모든 내부 노드 IP 또는 localhost에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="29b99-137">**포트:** hello 역방향 프록시에 대 한 지정 된 19081, 같은 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="29b99-138">**ServiceInstanceName:** hello hello 없이 tooreach를 시도 하는 배포 된 hello 서비스 인스턴스의 정규화 된 이름 "fabric: /" 구성표입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="29b99-139">예를 들어 tooreach hello *패브릭: / myapp/myservice/* 서비스를 사용 하 여 *myapp/myservice*합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="29b99-140">hello 서비스 인스턴스 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="29b99-141">404 (찾을 수 없음) hello 요청 toofail 되 면 서로 다른 대/소문자를 사용 하 여 hello URL에서 hello 서비스 인스턴스 이름을.</span><span class="sxs-lookup"><span data-stu-id="29b99-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="29b99-142">**경로 접미사:** 같은 hello 실제 URL 경로입니다 *myapi/값/추가/3*, tooconnect를 원하는 hello 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="29b99-143">**PartitionKey:** 분할 된 서비스 tooreach hello 파티션의 hello 계산 된 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="29b99-144">이것은 *하지* hello 파티션 ID GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="29b99-145">이 매개 변수 hello singleton 파티션 구성표를 사용 하는 서비스에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="29b99-146">**PartitionKind:** hello 서비스 파티션 구성표입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="29b99-147">이는 'Int64Range' 또는 'Named'일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="29b99-148">이 매개 변수 hello singleton 파티션 구성표를 사용 하는 서비스에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="29b99-149">**ListenerName** hello 폼의 hello 서비스에서 hello 끝점은 {"끝점": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}.</span><span class="sxs-lookup"><span data-stu-id="29b99-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="29b99-150">이 식별 hello 끝점 hello 서비스에서 여러 끝점을 노출할 때 해당 hello 클라이언트 요청을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="29b99-151">Hello 서비스에 수신기가 하나만 있으면 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="29b99-152">**TargetReplicaSelector** 방법을 hello 대상 복제본 또는 인스턴스 선택 해야 합니다.이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="29b99-153">Hello TargetReplicaSelector hello 다음 중 하나일 수 hello 대상 서비스 이면 상태 저장: 'PrimaryReplica', 'RandomSecondaryReplica' 또는 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="29b99-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="29b99-154">이 매개 변수를 지정 하지 않으면 'PrimaryReplica' hello 기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="29b99-155">Hello 대상 서비스는 상태 비저장 역방향 프록시에서는 hello 서비스 파티션 tooforward hello 요청을의 임의 인스턴스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="29b99-156">**시간 초과:** hello 클라이언트 요청을 대신해 hello 역방향 프록시 toohello 서비스에 의해 만들어진 hello HTTP 요청에 대 한 hello 시간 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="29b99-157">hello 기본값은 60 초입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="29b99-158">선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="29b99-159">사용 예</span><span class="sxs-lookup"><span data-stu-id="29b99-159">Example usage</span></span>
<span data-ttu-id="29b99-160">예를 들어 보겠습니다 hello *패브릭: / MyApp/MyService* hello url에 HTTP 수신기를 서비스:</span><span class="sxs-lookup"><span data-stu-id="29b99-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="29b99-161">다음은 hello 서비스에 대 한 hello 리소스:</span><span class="sxs-lookup"><span data-stu-id="29b99-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="29b99-162">Hello 서비스가 hello singleton 파티션 구성표를 사용 하는 경우 hello *PartitionKey* 및 *PartitionKind* 쿼리 문자열 매개 변수가 필요 하지 않습니다. 및 hello 게이트웨이 사용 하 여 hello 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="29b99-163">외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="29b99-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="29b99-164">내부에서: `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="29b99-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="29b99-165">Hello 서비스가 hello 균일 Int64 파티션 구성표를 사용 하는 경우 hello *PartitionKey* 및 *PartitionKind* 쿼리 문자열 매개 변수가 사용 되는 tooreach hello 서비스의 파티션을 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="29b99-166">외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="29b99-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="29b99-167">내부에서: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="29b99-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="29b99-168">tooreach hello 리소스 hello 서비스를 노출 하는 단순히 hello URL에 hello 서비스 이름 뒤에 오는 hello 리소스 경로 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="29b99-169">외부에서: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="29b99-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="29b99-170">내부에서: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="29b99-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="29b99-171">hello 게이트웨이 이러한 요청 toohello 서비스의이 URL을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="29b99-172">포트 공유 서비스에 대한 특수 처리</span><span class="sxs-lookup"><span data-stu-id="29b99-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="29b99-173">Azure 응용 프로그램 게이트웨이 시도 tooresolve 서비스 다시 주소와 서비스에 연결할 수 없는 경우 hello 요청을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="29b99-174">응용 프로그램 게이트웨이의 큰 장점은 클라이언트 코드는 자체 서비스 해상도 tooimplement 필요 하며 루프를 해결 하지 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="29b99-175">일반적으로 서비스에 연결할 수 없는 경우 hello 서비스 인스턴스나 복제본에 이동의 기본 수명 주기의 일부로 tooa 다른 노드.</span><span class="sxs-lookup"><span data-stu-id="29b99-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="29b99-176">이 경우 응용 프로그램 게이트웨이 네트워크 연결 오류 끝점 임을 나타내는 hello에 긴 열지 않고는 원래 주소 확인을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="29b99-177">그러나 복제 또는 서비스 인스턴스는 호스트 프로세스를 공유할 수 있으며 다음을 비롯하여 http.sys 기반 웹 서버에 의해 호스팅될 경우 포트를 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="29b99-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="29b99-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="29b99-179">ASP.NET 코어 WebListener</span><span class="sxs-lookup"><span data-stu-id="29b99-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="29b99-180">카타나</span><span class="sxs-lookup"><span data-stu-id="29b99-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="29b99-181">이 경우 해당 hello 웹 서버 hello 호스트 프로세스 및 toorequests, 하지만 hello 해결 서비스 인스턴스 또는 복제본을 더 이상 사용할 수 hello 호스트에 응답에서 사용할 수 있는 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="29b99-182">이 경우 hello 게이트웨이 hello 웹 서버에서 HTTP 404 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="29b99-183">따라서 HTTP 404에는 다음과 같은 두 가지 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="29b99-184">사례 #1: hello 서비스 주소가 올바르지만 요청 사용자 hello hello 리소스가 존재 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="29b99-185">사례 2: hello 서비스 주소가 올바르지 않은 및 사용자 요청 hello hello 리소스는 서로 다른 노드에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="29b99-186">hello 첫 번째 경우에는 사용자 오류 하다 고 간주 되는 일반 HTTP 404입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="29b99-187">그러나 hello 두 번째 경우에 hello 사용자가 존재 하는 리소스를 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="29b99-188">응용 프로그램 게이트웨이 없습니다 toolocate hello 서비스 자체 때문에 이동 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="29b99-189">응용 프로그램 게이트웨이 요구 tooresolve hello 주소 다시 및 hello 요청을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="29b99-190">응용 프로그램 게이트웨이 이러한 두 사례 사이의 방식으로 toodistinguish 따라서 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="29b99-191">이러한 방식으로 구분 hello 서버에서 힌트 필수임 toomake 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="29b99-192">기본적으로 응용 프로그램 게이트웨이 대/소문자 #2 맡고 tooresolve 및 문제 hello 요청을 다시 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="29b99-193">tooindicate 사례 #1 tooApplication 게이트웨이, hello 서비스 HTTP 응답 헤더 뒤에 오는 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="29b99-194">이 HTTP 응답 헤더는 hello에 요청 된 리소스가 존재 하지 않습니다, 일반적인 HTTP 404 상황을 나타내고 응용 프로그램 게이트웨이 tooresolve hello 서비스 주소를 다시 시도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="29b99-195">설정 및 구성</span><span class="sxs-lookup"><span data-stu-id="29b99-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="29b99-196">Azure Portal을 통해 역방향 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="29b99-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="29b99-197">Azure 포털은 새 서비스 패브릭 클러스터를 만드는 동안 옵션 tooenable 역방향 프록시를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="29b99-198">아래 **만들 서비스 패브릭 클러스터**, 2 단계: 클러스터 구성에서 노드 유형 구성 너무 hello 확인란을 선택 "역방향 프록시 사용"입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="29b99-199">보안 역방향 프록시를 구성 하는 데 SSL 인증서에에서 지정할 수 3 단계: 클러스터 보안 설정 구성, 확인란 선택 hello 너무 "역방향 프록시에 대 한 SSL 인증서가 포함" 보안과 hello 인증서 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="29b99-200">Azure Resource Manager 템플릿을 통해 역방향 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="29b99-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="29b99-201">Hello를 사용할 수 있습니다 [Azure 리소스 관리자 템플릿](service-fabric-cluster-creation-via-arm.md) tooenable hello 역방향 프록시 서비스 패브릭에서 hello 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="29b99-202">너무 참조[HTTPS 역방향 프록시 구성에서 보안 클러스터](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) Azure 리소스 관리자에 대 한 서식 파일 예제 tooconfigure 보안 역방향 프록시 인증서 및 처리 인증서 롤오버로 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="29b99-203">첫째, 얻게 hello 템플릿 hello 클러스터에 대 한 toodeploy 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="29b99-204">Hello 예제 서식 파일을 사용 하거나 사용자 지정 리소스 관리자 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="29b99-205">그런 다음 단계를 수행 하는 hello를 사용 하 여 hello 역방향 프록시를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="29b99-206">Hello에 hello 역방향 프록시에 대 한 포트 정의 [매개 변수 섹션](../azure-resource-manager/resource-group-authoring-templates.md) hello 템플릿의 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="29b99-207">각 hello에 hello nodetype 개체에 hello 포트를 지정 **클러스터** [리소스 유형 섹션](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="29b99-208">hello 포트 reverseProxyEndpointPort hello 매개 변수 이름으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="29b99-209">1 단계에서 지정한 hello 포트에 대 한 hello Azure 부하 분산 장치 규칙을 설정 해 서 Azure 클러스터 hello 외부에서 tooaddress hello의 역방향 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="29b99-210">hello 역방향 프록시에 대 한 hello 포트에서 SSL 인증서 tooconfigure 추가 hello 인증서 toohello ***reverseProxyCertificate*** hello에 대 한 속성 **클러스터** [리소스 유형 섹션](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="29b99-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="29b99-211">Hello 클러스터 인증서와에서 다른 역방향 프록시 인증서를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="29b99-212">Hello 역방향 프록시 인증서 hello 클러스터를 보호 하는 hello 인증서와에서 다른 경우 다음 hello 이전에 지정한 인증서 hello 가상 컴퓨터에 설치 해야 하 고 서비스 패브릭 수 있도록 toohello 액세스 제어 목록 (ACL)에 추가 액세스.</span><span class="sxs-lookup"><span data-stu-id="29b99-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="29b99-213">Hello에 이렇게 **virtualMachineScaleSets** [리소스 유형 섹션](../resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="29b99-214">설치의 경우 해당 인증서 toohello osProfile를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="29b99-215">hello 서식 파일의 확장명 섹션 hello hello ACL에에서 hello 인증서를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

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
> <span data-ttu-id="29b99-216">Hello 클러스터 인증서 tooenable hello 역방향 프록시를 기존 클러스터의 다른 인증서를 사용할 때 hello 역방향 프록시 인증서를 설치 하 고 hello 역방향 프록시를 사용 하기 전에 hello 클러스터에서 hello ACL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29b99-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="29b99-217">전체 hello [Azure 리소스 관리자 템플릿](service-fabric-cluster-creation-via-arm.md) 배포 언급 된 hello 설정을 사용 하 여 이전에 배포 tooenable hello 역방향 프록시를 시작 하기 전에에 1-4 단계.</span><span class="sxs-lookup"><span data-stu-id="29b99-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29b99-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29b99-218">Next steps</span></span>
* <span data-ttu-id="29b99-219">[GitHub의 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)에서 서비스 간 HTTP 통신의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29b99-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="29b99-220">Hello 역방향 프록시를 사용 하 여 HTTP 서비스 toosecure 전달</span><span class="sxs-lookup"><span data-stu-id="29b99-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="29b99-221">Reliable Services 원격을 사용하여 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="29b99-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="29b99-222">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="29b99-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="29b99-223">Reliable Services를 사용한 WCF 통신</span><span class="sxs-lookup"><span data-stu-id="29b99-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="29b99-224">추가적인 역방향 프록시 구성 옵션은 [Service Fabric 클러스터 설정 사용자 지정](service-fabric-cluster-fabric-settings.md)의 응용 프로그램 게이트웨이/HTTP 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29b99-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
