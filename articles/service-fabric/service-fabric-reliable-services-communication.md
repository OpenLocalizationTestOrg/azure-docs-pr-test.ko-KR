---
title: "aaaReliable 서비스 통신 개요 | Microsoft Docs"
description: "서비스에서 여는 수신기를 포함 하 여 끝점을 확인 하 고 서비스 간에 통신 hello 신뢰할 수 있는 서비스 통신 모델 사용의 개요를 제공 합니다."
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
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="d5410-103">Toouse는 신뢰할 수 있는 서비스 통신 Api hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d5410-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="d5410-104">플랫폼인 Azure 서비스 패브릭은 서비스 간에 이루어지는 통신을 전혀 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="d5410-105">모든 프로토콜 및 스택 UDP tooHTTP에서 허용 되는입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="d5410-106">가 toohello 서비스 개발자 toochoose 서비스 어떻게 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="d5410-107">hello 신뢰할 수 있는 서비스 응용 프로그램 프레임 워크는 기본 제공 통신 스택 toobuild를 사용할 수 있는 Api 뿐 아니라 사용자 지정 통신 구성 요소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="d5410-108">서비스 통신 설정</span><span class="sxs-lookup"><span data-stu-id="d5410-108">Set up service communication</span></span>
<span data-ttu-id="d5410-109">hello 신뢰할 수 있는 서비스 API는 서비스 통신에 대 한 간단한 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="d5410-110">서비스에 대 한 끝점 tooopen이이 인터페이스를 구현 하기만 하면:</span><span class="sxs-lookup"><span data-stu-id="d5410-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="d5410-111">그런 다음 서비스 기본 클래스 메서드 재정의에서 통신 수신기를 반환하여 통신 수신기 구현을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="d5410-112">상태 비저장 서비스의 경우:</span><span class="sxs-lookup"><span data-stu-id="d5410-112">For stateless services:</span></span>

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

<span data-ttu-id="d5410-113">상태 저장 서비스의 경우:</span><span class="sxs-lookup"><span data-stu-id="d5410-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="d5410-114">상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="d5410-115">두 경우 모두 수신기의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="d5410-116">이렇게 하면 서로 다른 프로토콜을 사용 하 여 여러 수신기를 사용 하 여 여러 끝점을 서비스 toolisten 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="d5410-117">예를 들어 HTTP 수신기 및 별도의 WebSocket 수신기가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="d5410-118">각 수신기 이름 및 hello 결과 컬렉션을 가져옵니다 *이름: 주소* 쌍은 클라이언트가 서비스 인스턴스 또는 파티션에 대 한 hello 수신 대기 주소를 요청 하면 JSON 개체로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="d5410-119">상태 비저장 서비스 hello 재정의 ServiceInstanceListeners의 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="d5410-120">A `ServiceInstanceListener` 함수 toocreate 포함 한 `ICommunicationListener(C#) / CommunicationListener(Java)` 고에 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="d5410-121">상태 저장 서비스에 대 한 hello 재정의 ServiceReplicaListeners의 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="d5410-122">상태 비저장에 대응 간에 약간 차이가 때문에 `ServiceReplicaListener` 옵션 tooopen에는 `ICommunicationListener` 보조 복제본에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="d5410-123">서비스에서 여러 통신 수신기를 사용할 수 있을 뿐만 아니라 보조 복제본에서 요청을 수락하는 수신기와 주 복제본에서만 수신하는 수신기를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="d5410-124">예를 들어 주 복제본에서는 RPC만 호출하는 ServiceRemotingListener와 HTTP를 통해 보조 복제본에서는 읽기 요청을 수행하는 두 번째 사용자 지정 수신기가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="d5410-125">서비스에 대한 여러 수신기를 만들 때 각 수신기에 고유한 이름을 지정 **해야** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="d5410-126">마지막으로 hello 서비스 hello에 대 한 필요한 hello 끝점에 설명 [서비스 매니페스트](service-fabric-application-model.md) 끝점 hello 섹션 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="d5410-127">hello 통신 수신기 tooit hello에서 할당 하는 hello 끝점 리소스에 액세스할 수 `CodePackageActivationContext` hello에 `ServiceContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="d5410-128">그런 다음 hello 수신기 열릴 때 요청을 수신 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="d5410-129">끝점 리소스가 일반적인 toohello 전체 서비스 패키지 되며 hello 서비스 패키지 활성화 될 때 서비스 패브릭에서 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="d5410-130">동일한 ServiceHost를 공유할 수 있습니다 hello에서 호스트 되는 여러 서비스 복제본 hello 동일한 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="d5410-131">즉, 해당 hello 통신 수신기에서 포트 공유를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="d5410-132">hello는 hello 수신 주소를 생성할 때 hello 통신 수신기 toouse hello 파티션의 ID 및 복제본/인스턴스 ID는 방법은이 작업을 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="d5410-133">서비스 주소 등록</span><span class="sxs-lookup"><span data-stu-id="d5410-133">Service address registration</span></span>
<span data-ttu-id="d5410-134">시스템 서비스는 hello 라는 *명명 서비스* 서비스 패브릭 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="d5410-135">hello 명명 서비스는 서비스 및 해당 주소에서 수신 대기 중인 각 인스턴스 또는 hello 서비스의 복제본에 대 한 등록 자가입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="d5410-136">Hello 때 `OpenAsync(C#) / openAsync(Java)` 의 메서드는 `ICommunicationListener(C#) / CommunicationListener(Java)` 완료 되 면 반환 값을 가져옵니다 hello 명명 서비스에에서 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="d5410-137">이렇게 하면 반환 값을 가져오는 명명 서비스에 게시 된 hello는 문자열 값을 갖는 전혀 아무 것도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="d5410-138">이 문자열 값은 클라이언트 hello 명명 서비스에서에서 hello 서비스에 대 한 주소에 대 한 요청은 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

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

    // hello string returned here will be published in hello Naming Service.
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

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="d5410-139">서비스 패브릭 서비스 이름으로이 주소에 대 한 클라이언트 및 다른 서비스 toothen 허용 하는 Api 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="d5410-140">Hello 서비스 주소를 고정 없기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="d5410-141">서비스는 리소스 균형 조정 및 가용성 목적으로 hello 클러스터에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="d5410-142">클라이언트는 서비스에 대 한 주소를 수신 대기 tooresolve hello를 허용 하는 hello 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="d5410-143">통신 수신기를 참조 하는 toowrite 방법의 전체 연습 [OWIN 자체 호스트 된 서비스 패브릭 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md) C#, Java 용 작성할 수 있습니다. HTTP 서버 구현이 고유한 반면 EchoServer 응용 프로그램이 표시 됩니다. https://github.com/Azure-Samples/service-fabric-java-getting-started에서 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="d5410-144">서비스와 통신</span><span class="sxs-lookup"><span data-stu-id="d5410-144">Communicating with a service</span></span>
<span data-ttu-id="d5410-145">hello 신뢰할 수 있는 서비스 API는 다음 서비스와 통신 하는 라이브러리 toowrite 클라이언트 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="d5410-146">서비스 끝점 확인</span><span class="sxs-lookup"><span data-stu-id="d5410-146">Service endpoint resolution</span></span>
<span data-ttu-id="d5410-147">서비스와 첫 번째 단계 toocommunication hello tooresolve hello 파티션 또는 인스턴스를 tootalk hello 서비스의 끝점 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="d5410-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` 유틸리티 클래스는 런타임에 서비스의 hello 끝점을 결정 하는 클라이언트는 데 도움이 되는 기본 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="d5410-149">서비스 패브릭 용어, 서비스의 hello 끝점을 결정 하는 hello 프로세스는 참조 된 tooas hello *서비스 끝점 확인*합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="d5410-150">클러스터 내에서 tooconnect tooservices, ServicePartitionResolver 만들 수 있습니다 기본 설정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="d5410-151">이 대부분의 상황에 대 한 사용을 권장 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="d5410-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="d5410-152">다른 클러스터의 tooconnect tooservices는 ServicePartitionResolver 클러스터 게이트웨이 끝점의 집합으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="d5410-153">게이트웨이 끝점 toohello 연결 하기 위한 다른 끝점에는 동일한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="d5410-154">예:</span><span class="sxs-lookup"><span data-stu-id="d5410-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="d5410-155">또는 `ServicePartitionResolver` 을 지정할 수는 함수를 만들기 위한는 `FabricClient` toouse 내부적으로:</span><span class="sxs-lookup"><span data-stu-id="d5410-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

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

<span data-ttu-id="d5410-156">`FabricClient`hello 클러스터에 대 한 다양 한 관리 작업에 대 한 hello 서비스 패브릭 클러스터를 사용 하는 toocommunicate는 hello 개체가입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="d5410-157">서비스 파티션 확인자가 클러스터가 상호 작용하는 방법을 더 제어하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="d5410-158">`FabricClient`내부적으로 캐싱을 수행 하 고 일반적으로 비용이 많이 드는 toocreate 하는 중요 한 tooreuse 이므로 `FabricClient` 인스턴스를 최대한 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="d5410-159">해결 방법은 사용 되는 tooretrieve hello 주소는 서비스 또는 분할 된 서비스에 대 한 서비스 파티션을 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="d5410-160">ServicePartitionResolver를 사용 하 여 쉽게 서비스 주소를 확인할 수 있지만 더 많은 작업이 필요 tooensure hello 해결 주소를 올바르게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="d5410-161">클라이언트 hello 연결 시도가 일시적인 오류로 인해 실패 하 고 다시 시도할 수 있는지 여부를 toodetect 필요 (예: 이동 서비스나 ब ् ध) 또는 영구 오류가 (예: 서비스가 삭제 되었거나 또는 hello 요청 된 리소스 더 이상 존재 하지).</span><span class="sxs-lookup"><span data-stu-id="d5410-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="d5410-162">서비스 인스턴스 또는 복제본 이동할 수 노드 toonode에서 언제 든 지 여러 가지 이유로.</span><span class="sxs-lookup"><span data-stu-id="d5410-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="d5410-163">클라이언트 코드 시도 tooconnect hello 시간별 ServicePartitionResolver 통해 확인 된 hello 서비스 주소 오래 되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="d5410-164">이 경우 다시 hello 클라이언트 toore 해결 hello 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="d5410-165">이전 hello 제공 `ResolvedServicePartition` 나타냅니다는 확인자 요구 tootry 안녕 보다는 캐시 된 주소를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="d5410-166">일반적으로 hello 클라이언트 코드 필요 하지 hello ServicePartitionResolver 직접 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="d5410-167">생성 되며 toocommunication 클라이언트 팩터리 hello 신뢰할 수 있는 서비스 API에에서 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="d5410-168">hello 팩터리 hello 해결 프로그램을 내부적으로 사용 toogenerate 서비스와 함께 사용 되는 toocommunicate 일 수 있는 클라이언트 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="d5410-169">통신 클라이언트 및 팩터리</span><span class="sxs-lookup"><span data-stu-id="d5410-169">Communication clients and factories</span></span>
<span data-ttu-id="d5410-170">hello 통신 팩터리 라이브러리 다시 시도 중인 연결 tooresolved 서비스 끝점을 더 쉽게 하는 일반적인 오류 처리 재시도 패턴을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="d5410-171">hello 팩터리 라이브러리 hello 오류 처리기를 제공 하는 동안 hello 재시도 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="d5410-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`tooa 서비스 패브릭 서비스를 서로 연결할 수 있는 클라이언트를 생성 하는 통신 클라이언트 팩터리로 구현 된 hello 기본 인터페이스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="d5410-173">안녕 구현의 hello CommunicationClientFactory hello 클라이언트가 toocommunicate 여기서 hello 서비스 패브릭 서비스에서 사용 하는 hello 통신 스택을에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="d5410-174">hello 신뢰할 수 있는 서비스 API를 제공는 `CommunicationClientFactoryBase<TCommunicationClient>`합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="d5410-175">이 hello CommunicationClientFactory 인터페이스의 기본 구현을 제공 하 고 일반적인 tooall hello 통신 스택과 된 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="d5410-176">(이러한 작업을 포함할 ServicePartitionResolver toodetermine hello 서비스 끝점을 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="d5410-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="d5410-177">클라이언트는 일반적으로 특정 toohello 통신 스택을 있는 hello 추상 CommunicationClientFactoryBase 클래스 toohandle 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="d5410-178">hello 통신 클라이언트 주소 방금 받아 tooconnect tooa 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="d5410-179">hello 클라이언트는 원하는 프로토콜을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-179">hello client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="d5410-180">hello 클라이언트 팩터리는 통신 클라이언트 작성을 주로 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="d5410-181">HTTP 클라이언트 등의 영구 연결을 유지 하지 않는 클라이언트에 대 한 hello 팩터리 toocreate와 반환 hello 클라이언트에만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="d5410-182">일부 이진 프로토콜 등의 영구 연결을 유지 관리 하는 다른 프로토콜도 유효성을 검사 해야 hello 팩터리 toodetermine 하 여 hello 연결 toobe 다시 생성 해야 하는지 여부를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

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

<span data-ttu-id="d5410-183">마지막으로 예외 처리기는 예외가 발생할 때 어떤 작업 tootake를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="d5410-184">예외는 **다시 시도 가능** 및 **다시 시도 불가능**으로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="d5410-185">**다시 시도할 수 없는** 예외 단순히 가져오기 다시 throw 백 toohello 호출자입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="d5410-186">**다시 시도 가능** 예외는 **일시적** 및 **영구** 예외로 더 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="d5410-187">**일시적인** 예외는 단순히 다시 hello 서비스 끝점 주소를 확인 하지 않고 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="d5410-188">여기에 일시적인 네트워크 문제 또는 hello 서비스 끝점 주소를 지정 하지 않은 서비스 오류 응답과 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="d5410-189">**일시적이 지 않은** 예외는 hello 서비스 끝점 주소 toobe 다시 확인 해야 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="d5410-190">여기에 hello 서비스 끝점에 연결할 수 없습니다, hello 서비스 tooa 다른 노드로 이동할가 표시 여부를 나타내는 예외 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="d5410-191">hello `TryHandleException` 주어진된 예외에 대 한 결정을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="d5410-192">경우 것 **를 알지 못하고** 돌아가야 하는 예외에 대 한 어떤 결정 toomake **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="d5410-193">경우 것 **알고** 어떤 의사 결정 toomake hello 결과 적절 하 게 설정 하 고 반환 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
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

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="d5410-194">모든 항목 요약</span><span class="sxs-lookup"><span data-stu-id="d5410-194">Putting it all together</span></span>
<span data-ttu-id="d5410-195">와 `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, 및 `IExceptionHandler(C#) / ExceptionHandler(Java)` 통신 프로토콜을 기반으로 구축 된 `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` 모두 함께 배치 되 고 hello 오류 처리 및 서비스 파티션 주소 확인 루프 이러한 구성 요소를 기준 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5410-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
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
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="d5410-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5410-196">Next steps</span></span>
* <span data-ttu-id="d5410-197">[GitHub의 C# 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) 또는 [GitHUb의 Java 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog)에서 서비스 간 HTTP 통신의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5410-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="d5410-198">Reliable Services 원격을 사용하여 원격 프로시저 호출</span><span class="sxs-lookup"><span data-stu-id="d5410-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="d5410-199">Reliable Services에서 OWIN을 사용하는 Web API</span><span class="sxs-lookup"><span data-stu-id="d5410-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d5410-200">Reliable Services를 사용한 WCF 통신</span><span class="sxs-lookup"><span data-stu-id="d5410-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
