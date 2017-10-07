---
title: "Azure 서비스 패브릭에서 aaaService 원격 | Microsoft Docs"
description: "서비스 패브릭 원격 클라이언트 및 원격 프로시저 호출을 사용 하 여 서비스를 사용 하 여 toocommunicate 서비스입니다."
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
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="49efe-103">Reliable Services로 서비스 원격 호출</span><span class="sxs-lookup"><span data-stu-id="49efe-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49efe-104">Windows에서 C#</span><span class="sxs-lookup"><span data-stu-id="49efe-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="49efe-105">Linux에서 Java</span><span class="sxs-lookup"><span data-stu-id="49efe-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="49efe-106">hello 신뢰할 수 있는 서비스 프레임 워크 remoting 메커니즘 tooquickly 제공 및 서비스에 대 한 원격 프로시저 호출을 쉽게 설정할 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="49efe-107">서비스에 원격 호출 설정</span><span class="sxs-lookup"><span data-stu-id="49efe-107">Set up remoting on a service</span></span>
<span data-ttu-id="49efe-108">서비스에 대한 원격 호출은 간단한 두 가지 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="49efe-109">서비스 tooimplement에 대 한 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="49efe-110">이 인터페이스는 서비스에 대 한 원격 프로시저 호출에 사용할 수 있는 hello 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="49efe-111">hello 메서드는 작업 반환 해야 비동기 메서드.</span><span class="sxs-lookup"><span data-stu-id="49efe-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="49efe-112">hello 인터페이스를 구현 해야 `microsoft.serviceFabric.services.remoting.Service` 서비스 hello toosignal remoting 인터페이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="49efe-113">서비스에서 원격 수신기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="49efe-114">이것은 원격 호출 기능을 제공하는 `CommunicationListener` 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="49efe-115">`FabricTransportServiceRemotingListener`사용 되는 toocreate hello 기본 remoting 전송 프로토콜을 사용 하 여 원격 수신기 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="49efe-116">예를 들어 hello 다음과 같은 상태 비저장 서비스 노출 원격 프로시저 호출을 통해 단일 메서드 tooget "Hello World" 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="49efe-117">hello 인수와 hello 반환 hello 서비스 인터페이스의 형식에는 임의의 단순, 복합, 또는 사용자 지정 형식으로 될 수 있지만 serializable 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="49efe-118">원격 서비스 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="49efe-118">Call remote service methods</span></span>
<span data-ttu-id="49efe-119">Hello 통해 로컬 프록시 toohello 서비스를 사용 하 여 수행 됩니다 hello remoting 스택을 사용 하 여 서비스에서 메서드를 호출 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="49efe-120">hello `ServiceProxyBase` 메서드 서비스 hello 동일한 인터페이스를 구현 하는 hello를 사용 하 여 로컬 프록시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="49efe-121">해당 프록시를 호출 하면 메서드 hello 인터페이스에 원격으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="49efe-122">hello remoting 프레임 워크 hello 서비스 toohello 클라이언트에서 throw 된 예외를 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="49efe-123">따라서 예외 처리 논리를 사용 하 여 hello 클라이언트에서 `ServiceProxyBase` hello 서비스에서 throw 하는 예외를 직접 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="49efe-124">서비스 프록시 수명</span><span class="sxs-lookup"><span data-stu-id="49efe-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="49efe-125">ServiceProxy 만들기는 가벼운 작업이므로 사용자가 원하는 만큼 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="49efe-126">서비스 프록시는 사용자가 필요할 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="49efe-127">사용자를 재사용할 수 예외 발생 시 동일한 프록시 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="49efe-128">각 ServiceProxy hello 유선으로 통신 사용 되는 클라이언트 toosend 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="49efe-129">API를 호출 하는 동안 사용 되는 통신 클라이언트가 유효한 경우 내부 검사 toosee가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="49efe-130">이 결과에 따라 다시 만듭니다 hello 통신 클라이언트를.</span><span class="sxs-lookup"><span data-stu-id="49efe-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="49efe-131">따라서 사용자는 toorecreate serviceproxy 예외 발생 시 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="49efe-132">ServiceProxyFactory 수명</span><span class="sxs-lookup"><span data-stu-id="49efe-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="49efe-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory)는 다른 원격 인터페이스를 위한 프록시를 만드는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="49efe-134">프록시를 만들기 위해 API `ServiceProxyBase.create`를 사용하는 경우 프레임워크에서 `FabricServiceProxyFactory`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="49efe-135">경우에 하나의 유용한 toocreate 수동으로 toooverride 필요한 [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="49efe-136">팩터리는 비용이 많이 드는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-136">Factory is an expensive operation.</span></span> <span data-ttu-id="49efe-137">`FabricServiceProxyFactory`는 통신 클라이언트의 캐시를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="49efe-138">가장 좋은 방법은 toocache `FabricServiceProxyFactory` 가능한 한 오랫동안에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="49efe-139">원격 예외 처리</span><span class="sxs-lookup"><span data-stu-id="49efe-139">Remoting Exception Handling</span></span>
<span data-ttu-id="49efe-140">서비스 API에서 throw 된 모든 hello 원격 예외에는 RuntimeException 또는 FabricException 백 toohello 클라이언트를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="49efe-141">ServiceProxy에서에 대해 만들어집니다 hello 서비스 파티션에 대 한 모든 장애 조치 예외 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="49efe-142">다시 hello 올바른 끝점으로 장애 조치 Exceptions(Non-Transient Exceptions) 및 다시 시도 hello 호출이 있는 경우 hello 끝점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="49efe-143">장애 조치(Failover) 예외에 대한 재시도 횟수는 무한합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="49efe-144">TransientExceptions, 발생 한 경우만 다시 시도 hello 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="49efe-145">기본 재시도 매개 변수는 [OperationRetrySettings]에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="49efe-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) 사용자는 OperationRetrySettings 개체 tooServiceProxyFactory 생성자에 전달 하 여 이러한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49efe-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49efe-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49efe-147">Next steps</span></span>
* [<span data-ttu-id="49efe-148">Reliable Services에 대한 통신 보안 유지</span><span class="sxs-lookup"><span data-stu-id="49efe-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
