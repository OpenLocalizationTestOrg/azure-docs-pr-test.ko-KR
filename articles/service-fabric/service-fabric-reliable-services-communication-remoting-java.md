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
# <a name="service-remoting-with-reliable-services"></a>Reliable Services로 서비스 원격 호출
> [!div class="op_single_selector"]
> * [Windows에서 C#](service-fabric-reliable-services-communication-remoting.md)
> * [Linux에서 Java](service-fabric-reliable-services-communication-remoting-java.md)
>
>

hello 신뢰할 수 있는 서비스 프레임 워크 remoting 메커니즘 tooquickly 제공 및 서비스에 대 한 원격 프로시저 호출을 쉽게 설정할 합니다.

## <a name="set-up-remoting-on-a-service"></a>서비스에 원격 호출 설정
서비스에 대한 원격 호출은 간단한 두 가지 단계로 수행됩니다.

1. 서비스 tooimplement에 대 한 인터페이스를 만듭니다. 이 인터페이스는 서비스에 대 한 원격 프로시저 호출에 사용할 수 있는 hello 메서드를 정의 합니다. hello 메서드는 작업 반환 해야 비동기 메서드. hello 인터페이스를 구현 해야 `microsoft.serviceFabric.services.remoting.Service` 서비스 hello toosignal remoting 인터페이스가 있습니다.
2. 서비스에서 원격 수신기를 사용합니다. 이것은 원격 호출 기능을 제공하는 `CommunicationListener` 구현입니다. `FabricTransportServiceRemotingListener`사용 되는 toocreate hello 기본 remoting 전송 프로토콜을 사용 하 여 원격 수신기 수 있습니다.

예를 들어 hello 다음과 같은 상태 비저장 서비스 노출 원격 프로시저 호출을 통해 단일 메서드 tooget "Hello World" 합니다.

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
> hello 인수와 hello 반환 hello 서비스 인터페이스의 형식에는 임의의 단순, 복합, 또는 사용자 지정 형식으로 될 수 있지만 serializable 이어야 합니다.
>
>

## <a name="call-remote-service-methods"></a>원격 서비스 메서드 호출
Hello 통해 로컬 프록시 toohello 서비스를 사용 하 여 수행 됩니다 hello remoting 스택을 사용 하 여 서비스에서 메서드를 호출 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 클래스입니다. hello `ServiceProxyBase` 메서드 서비스 hello 동일한 인터페이스를 구현 하는 hello를 사용 하 여 로컬 프록시를 만듭니다. 해당 프록시를 호출 하면 메서드 hello 인터페이스에 원격으로 합니다.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

hello remoting 프레임 워크 hello 서비스 toohello 클라이언트에서 throw 된 예외를 전파 합니다. 따라서 예외 처리 논리를 사용 하 여 hello 클라이언트에서 `ServiceProxyBase` hello 서비스에서 throw 하는 예외를 직접 처리할 수 있습니다.

## <a name="service-proxy-lifetime"></a>서비스 프록시 수명
ServiceProxy 만들기는 가벼운 작업이므로 사용자가 원하는 만큼 만들 수 있습니다. 서비스 프록시는 사용자가 필요할 때까지 다시 사용할 수 있습니다. 사용자를 재사용할 수 예외 발생 시 동일한 프록시 hello 합니다. 각 ServiceProxy hello 유선으로 통신 사용 되는 클라이언트 toosend 메시지를 포함합니다. API를 호출 하는 동안 사용 되는 통신 클라이언트가 유효한 경우 내부 검사 toosee가 있는 합니다. 이 결과에 따라 다시 만듭니다 hello 통신 클라이언트를. 따라서 사용자는 toorecreate serviceproxy 예외 발생 시 필요 하지 않습니다.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory 수명
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory)는 다른 원격 인터페이스를 위한 프록시를 만드는 팩터리입니다. 프록시를 만들기 위해 API `ServiceProxyBase.create`를 사용하는 경우 프레임워크에서 `FabricServiceProxyFactory`를 만듭니다.
경우에 하나의 유용한 toocreate 수동으로 toooverride 필요한 [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) 속성입니다.
팩터리는 비용이 많이 드는 작업입니다. `FabricServiceProxyFactory`는 통신 클라이언트의 캐시를 유지 관리합니다.
가장 좋은 방법은 toocache `FabricServiceProxyFactory` 가능한 한 오랫동안에 대 한 합니다.

## <a name="remoting-exception-handling"></a>원격 예외 처리
서비스 API에서 throw 된 모든 hello 원격 예외에는 RuntimeException 또는 FabricException 백 toohello 클라이언트를 전송 됩니다.

ServiceProxy에서에 대해 만들어집니다 hello 서비스 파티션에 대 한 모든 장애 조치 예외 처리 합니다. 다시 hello 올바른 끝점으로 장애 조치 Exceptions(Non-Transient Exceptions) 및 다시 시도 hello 호출이 있는 경우 hello 끝점을 확인 합니다. 장애 조치(Failover) 예외에 대한 재시도 횟수는 무한합니다.
TransientExceptions, 발생 한 경우만 다시 시도 hello 호출 합니다.

기본 재시도 매개 변수는 [OperationRetrySettings]에서 제공됩니다. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) 사용자는 OperationRetrySettings 개체 tooServiceProxyFactory 생성자에 전달 하 여 이러한 값을 구성할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Reliable Services에 대한 통신 보안 유지](service-fabric-reliable-services-secure-communication.md)
