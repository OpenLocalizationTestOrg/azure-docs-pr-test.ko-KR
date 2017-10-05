---
title: "Azure Service Fabric의 서비스 원격 호출 | Microsoft Docs"
description: "서비스 패브릭 원격 호출을 사용하면 클라이언트와 서비스가 원격 프로시저 호출을 사용하여 서비스와 통신할 수 있도록 합니다."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="8c072-103">Reliable Services로 서비스 원격 호출</span><span class="sxs-lookup"><span data-stu-id="8c072-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c072-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="8c072-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="8c072-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="8c072-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="8c072-106">Reliable Services 프레임워크는 서비스에 대한 원격 프로시저 호출을 쉽고 빠르게 설정하기 위한 원격 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="8c072-107">서비스에 원격 호출 설정</span><span class="sxs-lookup"><span data-stu-id="8c072-107">Set up remoting on a service</span></span>
<span data-ttu-id="8c072-108">서비스에 대한 원격 호출은 간단한 두 가지 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="8c072-109">서비스로 구현할 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="8c072-110">이 인터페이스는 서비스의 원격 프로시저 호출에 사용할 수 있는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="8c072-111">메서드는 작업을 반환하는 비동기 메서드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="8c072-112">인터페이스는 서비스에 원격 호출 인터페이스가 있다는 것을 신호하기 위해 `microsoft.serviceFabric.services.remoting.Service` 를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="8c072-113">서비스에서 원격 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="8c072-114">이것은 원격 호출 기능을 제공하는 `CommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="8c072-115">`FabricTransportServiceRemotingListener`를 사용하여 기본 원격 전송 프로토콜을 통해 원격 수신기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="8c072-116">예를 들어 다음의 상태 비저장 서비스는 단일 메서드를 노출하여 원격 프로시저 호출에 "Hello World"를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="8c072-117">서비스 인터페이스의 인수 및 반환 형식은 간단한 형식, 복합 형식 또는 사용자 지정 형식이 가능하지만 serialization이 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="8c072-118">원격 서비스 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="8c072-118">Call remote service methods</span></span>
<span data-ttu-id="8c072-119">원격 스택을 사용하여 서비스에서 메서드를 호출하는 작업은 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 클래스를 통해 서비스에 대한 로컬 프록시를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="8c072-120">`ServiceProxyBase` 메서드는 서비스가 구현하는 것과 동일한 인터페이스를 사용하여 로컬 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="8c072-121">이 프록시를 통해 원격으로 인터페이스의 메서드를 간단하게 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="8c072-122">원격 호출 프레임워크는 서비스에 throw된 예외를 클라이언트에 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="8c072-123">따라서 `ServiceProxyBase` 을 사용하여 클라이언트에서 논리를 예외 처리하는 작업은 서비스가 throw하는 예외를 직접 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="8c072-124">서비스 프록시 수명</span><span class="sxs-lookup"><span data-stu-id="8c072-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="8c072-125">ServiceProxy 만들기는 가벼운 작업이므로 사용자가 원하는 만큼 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="8c072-126">서비스 프록시는 사용자가 필요할 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="8c072-127">사용자는 예외 발생 시 동일한 프록시를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="8c072-128">각 서비스 프록시는 유선으로 메시지를 보내는 데 사용되는 통신 클라이언트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="8c072-129">API를 호출하는 동안 사용된 통신 클라이언트가 유효한지 내부적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="8c072-130">그 결과에 따라 통신 클라이언트를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="8c072-131">따라서 사용자는 예외 발생 시 serviceproxy를 다시 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="8c072-132">ServiceProxyFactory 수명</span><span class="sxs-lookup"><span data-stu-id="8c072-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="8c072-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory)는 다른 원격 인터페이스를 위한 프록시를 만드는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="8c072-134">프록시를 만들기 위해 API `ServiceProxyBase.create`를 사용하는 경우 프레임워크에서 `FabricServiceProxyFactory`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="8c072-135">[ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) 속성을 재정의해야 하는 경우 수동으로 만드는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="8c072-136">팩터리는 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-136">Factory is an expensive operation.</span></span> <span data-ttu-id="8c072-137">`FabricServiceProxyFactory`는 통신 클라이언트의 캐시를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="8c072-138">`FabricServiceProxyFactory`를 가능한 한 오랫동안 캐시하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="8c072-139">원격 예외 처리</span><span class="sxs-lookup"><span data-stu-id="8c072-139">Remoting Exception Handling</span></span>
<span data-ttu-id="8c072-140">서비스 API에 의해 throw되는 모든 원격 예외는 RuntimeException 또는 FabricException으로 클라이언트에 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="8c072-141">ServiceProxy는 만들어진 서비스 파티션에 대한 모든 장애 조치(failover) 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="8c072-142">장애 조치(Failover) 예외(영구적인 예외)가 있는 경우 끝점을 다시 확인하고 올바른 끝점으로 호출을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="8c072-143">장애 조치(Failover) 예외에 대한 재시도 횟수는 무한합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="8c072-144">TransientExceptions의 경우에는 호출만 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="8c072-145">기본 재시도 매개 변수는 [OperationRetrySettings]에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="8c072-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings)사용자는 OperationRetrySettings 개체를 ServiceProxyFactory 생성자에 전달하여 이러한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c072-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c072-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c072-147">Next steps</span></span>
* [<span data-ttu-id="8c072-148">Reliable Services에 대한 통신 보안 유지</span><span class="sxs-lookup"><span data-stu-id="8c072-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
