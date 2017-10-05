---
title: "Reliable Services 통신 개요 | Microsoft Docs"
description: "서비스에서 수신기 열기, 끝점 확인 및 서비스 간 통신을 비롯한 Reliable Services 통신 모델의 개요입니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="883fe-103">Reliable Services 통신 API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="883fe-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="883fe-104">플랫폼인 Azure 서비스 패브릭은 서비스 간에 이루어지는 통신을 전혀 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="883fe-105">UDP에서 HTTP까지 모든 프로토콜 및 스택이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="883fe-106">서비스 개발자가 서비스가 통신하는 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="883fe-107">Reliable Services 응용 프로그램 프레임워크는 사용자 지정 통신 구성 요소를 빌드하는 데 사용할 수 있는 API 뿐만 아니라 기본 제공 통신 스택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="883fe-108">서비스 통신 설정</span><span class="sxs-lookup"><span data-stu-id="883fe-108">Set up service communication</span></span>
<span data-ttu-id="883fe-109">Reliable Services API는 서비스 통신을 위해 간단한 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="883fe-110">서비스에 대한 끝점을 열려면 다음 인터페이스를 구현하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-110">To open an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="883fe-111">그런 다음 서비스 기본 클래스 메서드 재정의에서 통신 수신기를 반환하여 통신 수신기 구현을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="883fe-112">상태 비저장 서비스의 경우:</span><span class="sxs-lookup"><span data-stu-id="883fe-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="883fe-113">상태 저장 서비스의 경우:</span><span class="sxs-lookup"><span data-stu-id="883fe-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="883fe-114">상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="883fe-115">두 경우 모두 수신기의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="883fe-116">이렇게 하면 서비스가 여러 수신기를 사용하여 서로 다른 프로토콜을 잠재적으로 사용하는 다수의 끝점에서 수신할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="883fe-117">예를 들어 HTTP 수신기 및 별도의 WebSocket 수신기가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="883fe-118">각 수신기는 이름을 가져오며 *이름 : 주소* 쌍의 결과 콜렉션은 클라이언트가 서비스 인스턴스 또는 파티션에 대한 수신 주소를 요청하는 경우 JSON 개체로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="883fe-119">상태 비저장 서비스에서는 재정의가 ServiceInstanceListeners의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="883fe-120">`ServiceInstanceListener`에는 `ICommunicationListener(C#) / CommunicationListener(Java)`를 만들고 이름을 부여하는 함수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="883fe-121">상태 저장 서비스에서는 재정의가 ServiceReplicaListeners의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="883fe-122">이는 `ServiceReplicaListener`에 보조 복제본에서 `ICommunicationListener`를 여는 옵션이 있기 때문에 해당 상태 비저장에 상응하는 것과는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="883fe-123">서비스에서 여러 통신 수신기를 사용할 수 있을 뿐만 아니라 보조 복제본에서 요청을 수락하는 수신기와 주 복제본에서만 수신하는 수신기를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="883fe-124">예를 들어 주 복제본에서는 RPC만 호출하는 ServiceRemotingListener와 HTTP를 통해 보조 복제본에서는 읽기 요청을 수행하는 두 번째 사용자 지정 수신기가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="883fe-125">서비스에 대한 여러 수신기를 만들 때 각 수신기에 고유한 이름을 지정 **해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="883fe-126">마지막으로 끝점의 섹션에 있는 [서비스 매니페스트](service-fabric-application-model.md) 에서 서비스에 필요한 끝점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="883fe-127">통신 수신기는 `ServiceContext`의 `CodePackageActivationContext`에서 할당된 끝점 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="883fe-128">그런 다음 수신기가 열릴 때 요청을 수신하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="883fe-129">끝점 리소스는 전체 서비스 패키지에 공통되며 서비스 패키지가 활성화될 때 서비스 패브릭에서 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="883fe-130">동일한 ServiceHost에서 호스팅되는 여러 서비스 복제본은 동일한 포트를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="883fe-131">이는 통신 수신기가 포트 공유를 지원해야 한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="883fe-132">이에 대한 권장 방법은 통신 수신기가 수신 주소를 생성할 때 파티션 ID 및 복제본/인스턴스 ID를 사용하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="883fe-133">서비스 주소 등록</span><span class="sxs-lookup"><span data-stu-id="883fe-133">Service address registration</span></span>
<span data-ttu-id="883fe-134">*명명 서비스* 라는 시스템 서비스는 서비스 패브릭 클러스터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="883fe-135">명명 서비스는 서비스의 각 인스턴스 또는 복제본이 수신 중인 서비스 및 해당 주소에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="883fe-136">`ICommunicationListener(C#) / CommunicationListener(Java)`의 `OpenAsync(C#) / openAsync(Java)` 메서드가 완료되면 해당 반환 값은 명명 서비스에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="883fe-137">명명 서비스에 게시되는 반환 값은 어떤 값도 가능한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="883fe-138">이 문자열 값은 클라이언트가 명명 서비스에서 서비스에 대한 주소를 요청할 때 표시되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // the string returned here will be published in the Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="883fe-139">Service Fabric은 클라이언트 및 기타 서비스가 서비스 이름별로 이 주소를 요청할 수 있게 해주는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="883fe-140">서비스 주소가 정적이 아니기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-140">This is important because the service address is not static.</span></span> <span data-ttu-id="883fe-141">서비스는 리소스 균형 조정 및 가용성을 위한 클러스터 주변으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="883fe-142">이는 클라이언트가 서비스의 수신 대기 주소를 확인할 수 있도록 하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="883fe-143">C#의 경우는 [OWIN 자체 호스팅이 포함된 Service Fabric 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md)에서 통신 수신기를 작성하는 방법에 대한 전체 연습을 참조합니다. Java의 경우는 HTTP 서버 구현을 직접 작성할 수 있습니다. https://github.com/Azure-Samples/service-fabric-java-getting-started에서 EchoServer 응용 프로그램 예제를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="883fe-144">서비스와 통신</span><span class="sxs-lookup"><span data-stu-id="883fe-144">Communicating with a service</span></span>
<span data-ttu-id="883fe-145">Reliable Services API는 서비스와 통신하는 클라이언트를 작성하도록 다음 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="883fe-146">서비스 끝점 확인</span><span class="sxs-lookup"><span data-stu-id="883fe-146">Service endpoint resolution</span></span>
<span data-ttu-id="883fe-147">서비스와 통신하는 첫 번째 단계는 통신하려는 서비스의 파티션 또는 인스턴스의 끝점 주소를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="883fe-148">`ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` 유틸리티 클래스는 클라이언트가 런타임 시 서비스의 끝점을 확인할 수 있게 도와주는 기본 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="883fe-149">서비스 패브릭 용어로 서비스의 끝점을 결정하는 프로세스를 *서비스 끝점 확인*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="883fe-150">클러스터 내의 서비스에 연결하려면 기본 설정을 사용하여 ServicePartitionResolver를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="883fe-151">다음은 대부분의 상황에 대한 권장 사용법입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="883fe-152">다른 클러스터의 서비스에 연결하면 일련의 클러스터 게이트웨이 끝점으로 ServicePartitionResolver를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="883fe-153">게이트웨이 끝점은 동일한 클러스터에 연결하기 위한 다른 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="883fe-154">예:</span><span class="sxs-lookup"><span data-stu-id="883fe-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="883fe-155">또는 `ServicePartitionResolver`은 `FabricClient`를 만들기 위한 함수를 지정하여 내부적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="883fe-156">`FabricClient` 은 서비스 패브릭 클러스터의 다양한 관리 작업에서 클러스터와 통신하는 데 사용되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="883fe-157">서비스 파티션 확인자가 클러스터가 상호 작용하는 방법을 더 제어하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="883fe-158">`FabricClient`은 내부적으로 캐싱을 수행하며 만드는 데 일반적으로 비용이 많이 드므로 `FabricClient` 인스턴스를 최대한 많이 다시 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="883fe-159">그런 다음 확인 메서드는 분할된 서비스에 대한 서비스의 주소 또는 서비스 파티션을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="883fe-160">서비스 주소는 ServicePartitionResolver를 사용하여 쉽게 확인할 수 있지만 확인된 주소를 올바르게 사용할 수 있는지 확인하려면 더 많은 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="883fe-161">클라이언트는 연결 시도가 일시적 오류(예: 서비스 이동 또는 일시적으로 사용 불가함) 또는 영구 오류(예: 서비스가 삭제되었거나 요청된 리소스가 더 이상 존재하지 않음) 중 어떤 것 때문에 실패했는지를 감지하고 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="883fe-162">서비스 인스턴스 또는 복제본은 여러 가지 이유로 인해 언제든지 노드에서 노드로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="883fe-163">ServicePartitionResolver를 통해 확인된 서비스 주소는 클라이언트 코드가 연결하려고 시도한 시점에 기한이 경과될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="883fe-164">이 경우에 클라이언트가 주소를 다시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="883fe-165">이전 `ResolvedServicePartition` 을 제공하면 해결 프로그램이 캐시된 주소를 간단히 검색하는 대신 다시 시도해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="883fe-166">일반적으로 클라이언트 코드는 ServicePartitionResolver와 직접 연동할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="883fe-167">이 코드가 생성되면 Reliable Services API의 통신 클라이언트 팩터리에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="883fe-168">팩터리는 내부적으로 해결 프로그램을 사용하여 서비스와 통신하는 데 사용할 수 있는 클라이언트 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="883fe-169">통신 클라이언트 및 팩터리</span><span class="sxs-lookup"><span data-stu-id="883fe-169">Communication clients and factories</span></span>
<span data-ttu-id="883fe-170">통신 팩터리 라이브러리는 확인된 서비스 끝점에 대한 연결을 다시 시도하도록 하는 일반적인 오류 처리 재시도 패턴을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="883fe-171">오류 처리기를 제공하는 동안 팩터리 라이브러리는 재시도 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="883fe-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`은 Service Fabric 서비스와 통신할 수 있는 클라이언트를 생성하는 통신 클라이언트 팩터리에서 구현되는 기본 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="883fe-173">CommunicationClientFactory의 구현은 클라이언트가 통신하려고 하는 서비스 패브릭 서비스에서 사용하는 통신 스택에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="883fe-174">Reliable Services API는 `CommunicationClientFactoryBase<TCommunicationClient>`를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="883fe-175">이는 CommunicationClientFactory 인터페이스의 기본 구현을 제공하고 모든 통신 스택에 공통된 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="883fe-176">이러한 작업은 ServicePartitionResolver를 사용하여 서비스 끝점을 확인하는 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="883fe-177">클라이언트는 일반적으로 추상 CommunicationClientFactoryBase 클래스를 구현하여 통신 스택에 특정된 논리를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="883fe-178">통신 클라이언트는 주소를 수신하고 서비스에 연결하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="883fe-179">클라이언트는 원하는 모든 프로토콜을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-179">The client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="883fe-180">클라이언트 팩터리는 주로 통신 클라이언트를 만드는 작업을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="883fe-181">HTTP 클라이언트와 같은 영구 연결을 유지하지 않는 클라이언트의 경우 팩터리는 클라이언트를 만들고 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="883fe-182">또한 일부 이진 프로토콜과 같은 영구 연결을 유지하는 다른 프로토콜은 팩터리를 통해 유효성을 검사하여 연결을 다시 만들어야 하는지 여부를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="883fe-183">마지막으로 예외 처리기는 예외가 발생할 때 수행할 동작을 결정하는 작업을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="883fe-184">예외는 **다시 시도 가능** 및 **다시 시도 불가능**으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="883fe-185">**다시 시도 불가능** 예외는 단순히 다시 호출자로 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="883fe-186">**다시 시도 가능** 예외는 **일시적** 및 **영구** 예외로 더 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="883fe-187">**일시적** 예외는 서비스 끝점 주소를 다시 확인하지 않고 다시 시도할 수 있는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="883fe-188">일시적인 네트워크 문제 또는 서비스 끝점 주소가 존재하지 않음을 나타내는 것 이외의 서비스 오류 응답을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="883fe-189">**영구** 예외는 다시 확인할 서비스 끝점 주소를 필요로 하는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="883fe-190">이는 서비스 끝점에 도달하지 못했음을 나타내는 예외를 포함하며 이는 서비스가 다른 노드로 이동되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="883fe-191">`TryHandleException` 은 주어진 예외에 대한 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="883fe-192">예외에 대해 어떤 결정을 내릴지 **모르는** 경우 **false**를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="883fe-193">어떤 결정을 내릴지 **아는** 경우 결과를 적절하게 설정하여 **true**를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="883fe-194">모든 항목 요약</span><span class="sxs-lookup"><span data-stu-id="883fe-194">Putting it all together</span></span>
<span data-ttu-id="883fe-195">통신 프로토콜을 기반으로 구축한 `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` 및 `IExceptionHandler(C#) / ExceptionHandler(Java)`으로 `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)`는 모두를 함께 래핑하고 이러한 구성 요소에 대한 오류 처리 및 서비스 파티션 주소 확인 루프를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="883fe-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="883fe-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="883fe-196">Next steps</span></span>
* <span data-ttu-id="883fe-197">[GitHub의 C# 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) 또는 [GitHUb의 Java 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog)에서 서비스 간 HTTP 통신의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="883fe-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="883fe-198">Reliable Services 원격을 사용하여 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="883fe-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="883fe-199">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="883fe-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="883fe-200">Reliable Services를 사용한 WCF 통신</span><span class="sxs-lookup"><span data-stu-id="883fe-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
