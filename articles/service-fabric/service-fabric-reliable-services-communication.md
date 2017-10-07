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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Toouse는 신뢰할 수 있는 서비스 통신 Api hello 하는 방법
플랫폼인 Azure 서비스 패브릭은 서비스 간에 이루어지는 통신을 전혀 알 수 없습니다. 모든 프로토콜 및 스택 UDP tooHTTP에서 허용 되는입니다. 가 toohello 서비스 개발자 toochoose 서비스 어떻게 전달 해야 합니다. hello 신뢰할 수 있는 서비스 응용 프로그램 프레임 워크는 기본 제공 통신 스택 toobuild를 사용할 수 있는 Api 뿐 아니라 사용자 지정 통신 구성 요소를 제공 합니다.

## <a name="set-up-service-communication"></a>서비스 통신 설정
hello 신뢰할 수 있는 서비스 API는 서비스 통신에 대 한 간단한 인터페이스를 사용합니다. 서비스에 대 한 끝점 tooopen이이 인터페이스를 구현 하기만 하면:

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

그런 다음 서비스 기본 클래스 메서드 재정의에서 통신 수신기를 반환하여 통신 수신기 구현을 추가합니다.

상태 비저장 서비스의 경우:

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

상태 저장 서비스의 경우:

> [!NOTE]
> 상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.
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

두 경우 모두 수신기의 컬렉션을 반환합니다. 이렇게 하면 서로 다른 프로토콜을 사용 하 여 여러 수신기를 사용 하 여 여러 끝점을 서비스 toolisten 수 있습니다. 예를 들어 HTTP 수신기 및 별도의 WebSocket 수신기가 있을 수 있습니다. 각 수신기 이름 및 hello 결과 컬렉션을 가져옵니다 *이름: 주소* 쌍은 클라이언트가 서비스 인스턴스 또는 파티션에 대 한 hello 수신 대기 주소를 요청 하면 JSON 개체로 표현 됩니다.

상태 비저장 서비스 hello 재정의 ServiceInstanceListeners의 컬렉션을 반환 합니다. A `ServiceInstanceListener` 함수 toocreate 포함 한 `ICommunicationListener(C#) / CommunicationListener(Java)` 고에 이름을 제공 합니다. 상태 저장 서비스에 대 한 hello 재정의 ServiceReplicaListeners의 컬렉션을 반환 합니다. 상태 비저장에 대응 간에 약간 차이가 때문에 `ServiceReplicaListener` 옵션 tooopen에는 `ICommunicationListener` 보조 복제본에 있습니다. 서비스에서 여러 통신 수신기를 사용할 수 있을 뿐만 아니라 보조 복제본에서 요청을 수락하는 수신기와 주 복제본에서만 수신하는 수신기를 지정할 수도 있습니다.

예를 들어 주 복제본에서는 RPC만 호출하는 ServiceRemotingListener와 HTTP를 통해 보조 복제본에서는 읽기 요청을 수행하는 두 번째 사용자 지정 수신기가 있을 수 있습니다.

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
> 서비스에 대한 여러 수신기를 만들 때 각 수신기에 고유한 이름을 지정 **해야** 합니다.
>
>

마지막으로 hello 서비스 hello에 대 한 필요한 hello 끝점에 설명 [서비스 매니페스트](service-fabric-application-model.md) 끝점 hello 섹션 아래에 있습니다.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

hello 통신 수신기 tooit hello에서 할당 하는 hello 끝점 리소스에 액세스할 수 `CodePackageActivationContext` hello에 `ServiceContext`합니다. 그런 다음 hello 수신기 열릴 때 요청을 수신 시작할 수 있습니다.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> 끝점 리소스가 일반적인 toohello 전체 서비스 패키지 되며 hello 서비스 패키지 활성화 될 때 서비스 패브릭에서 할당 됩니다. 동일한 ServiceHost를 공유할 수 있습니다 hello에서 호스트 되는 여러 서비스 복제본 hello 동일한 포트입니다. 즉, 해당 hello 통신 수신기에서 포트 공유를 지원 해야 합니다. hello는 hello 수신 주소를 생성할 때 hello 통신 수신기 toouse hello 파티션의 ID 및 복제본/인스턴스 ID는 방법은이 작업을 수행 하는 것이 좋습니다.
>
>

### <a name="service-address-registration"></a>서비스 주소 등록
시스템 서비스는 hello 라는 *명명 서비스* 서비스 패브릭 클러스터에서 실행 됩니다. hello 명명 서비스는 서비스 및 해당 주소에서 수신 대기 중인 각 인스턴스 또는 hello 서비스의 복제본에 대 한 등록 자가입니다. Hello 때 `OpenAsync(C#) / openAsync(Java)` 의 메서드는 `ICommunicationListener(C#) / CommunicationListener(Java)` 완료 되 면 반환 값을 가져옵니다 hello 명명 서비스에에서 등록 합니다. 이렇게 하면 반환 값을 가져오는 명명 서비스에 게시 된 hello는 문자열 값을 갖는 전혀 아무 것도 될 수 있습니다. 이 문자열 값은 클라이언트 hello 명명 서비스에서에서 hello 서비스에 대 한 주소에 대 한 요청은 표시 합니다.

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

서비스 패브릭 서비스 이름으로이 주소에 대 한 클라이언트 및 다른 서비스 toothen 허용 하는 Api 요청을 제공 합니다. Hello 서비스 주소를 고정 없기 때문에 유용 합니다. 서비스는 리소스 균형 조정 및 가용성 목적으로 hello 클러스터에 이동 합니다. 클라이언트는 서비스에 대 한 주소를 수신 대기 tooresolve hello를 허용 하는 hello 메커니즘입니다.

> [!NOTE]
> 통신 수신기를 참조 하는 toowrite 방법의 전체 연습 [OWIN 자체 호스트 된 서비스 패브릭 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md) C#, Java 용 작성할 수 있습니다. HTTP 서버 구현이 고유한 반면 EchoServer 응용 프로그램이 표시 됩니다. https://github.com/Azure-Samples/service-fabric-java-getting-started에서 예제를 제공 합니다.
>
>

## <a name="communicating-with-a-service"></a>서비스와 통신
hello 신뢰할 수 있는 서비스 API는 다음 서비스와 통신 하는 라이브러리 toowrite 클라이언트 hello를 제공 합니다.

### <a name="service-endpoint-resolution"></a>서비스 끝점 확인
서비스와 첫 번째 단계 toocommunication hello tooresolve hello 파티션 또는 인스턴스를 tootalk hello 서비스의 끝점 주소입니다. hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` 유틸리티 클래스는 런타임에 서비스의 hello 끝점을 결정 하는 클라이언트는 데 도움이 되는 기본 기본 형식입니다. 서비스 패브릭 용어, 서비스의 hello 끝점을 결정 하는 hello 프로세스는 참조 된 tooas hello *서비스 끝점 확인*합니다.

클러스터 내에서 tooconnect tooservices, ServicePartitionResolver 만들 수 있습니다 기본 설정을 사용 하 여 합니다. 이 대부분의 상황에 대 한 사용을 권장 하는 hello:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

다른 클러스터의 tooconnect tooservices는 ServicePartitionResolver 클러스터 게이트웨이 끝점의 집합으로 만들 수 있습니다. 게이트웨이 끝점 toohello 연결 하기 위한 다른 끝점에는 동일한 클러스터입니다. 예:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

또는 `ServicePartitionResolver` 을 지정할 수는 함수를 만들기 위한는 `FabricClient` toouse 내부적으로:

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

`FabricClient`hello 클러스터에 대 한 다양 한 관리 작업에 대 한 hello 서비스 패브릭 클러스터를 사용 하는 toocommunicate는 hello 개체가입니다. 서비스 파티션 확인자가 클러스터가 상호 작용하는 방법을 더 제어하려는 경우에 유용합니다. `FabricClient`내부적으로 캐싱을 수행 하 고 일반적으로 비용이 많이 드는 toocreate 하는 중요 한 tooreuse 이므로 `FabricClient` 인스턴스를 최대한 많이 있습니다.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

해결 방법은 사용 되는 tooretrieve hello 주소는 서비스 또는 분할 된 서비스에 대 한 서비스 파티션을 다음 합니다.

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

ServicePartitionResolver를 사용 하 여 쉽게 서비스 주소를 확인할 수 있지만 더 많은 작업이 필요 tooensure hello 해결 주소를 올바르게 사용할 수 있습니다. 클라이언트 hello 연결 시도가 일시적인 오류로 인해 실패 하 고 다시 시도할 수 있는지 여부를 toodetect 필요 (예: 이동 서비스나 ब ् ध) 또는 영구 오류가 (예: 서비스가 삭제 되었거나 또는 hello 요청 된 리소스 더 이상 존재 하지). 서비스 인스턴스 또는 복제본 이동할 수 노드 toonode에서 언제 든 지 여러 가지 이유로. 클라이언트 코드 시도 tooconnect hello 시간별 ServicePartitionResolver 통해 확인 된 hello 서비스 주소 오래 되었을 수 있습니다. 이 경우 다시 hello 클라이언트 toore 해결 hello 주소가 필요합니다. 이전 hello 제공 `ResolvedServicePartition` 나타냅니다는 확인자 요구 tootry 안녕 보다는 캐시 된 주소를 검색 합니다.

일반적으로 hello 클라이언트 코드 필요 하지 hello ServicePartitionResolver 직접 사용 합니다. 생성 되며 toocommunication 클라이언트 팩터리 hello 신뢰할 수 있는 서비스 API에에서 전달 합니다. hello 팩터리 hello 해결 프로그램을 내부적으로 사용 toogenerate 서비스와 함께 사용 되는 toocommunicate 일 수 있는 클라이언트 개체입니다.

### <a name="communication-clients-and-factories"></a>통신 클라이언트 및 팩터리
hello 통신 팩터리 라이브러리 다시 시도 중인 연결 tooresolved 서비스 끝점을 더 쉽게 하는 일반적인 오류 처리 재시도 패턴을 구현 합니다. hello 팩터리 라이브러리 hello 오류 처리기를 제공 하는 동안 hello 재시도 메커니즘을 제공 합니다.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`tooa 서비스 패브릭 서비스를 서로 연결할 수 있는 클라이언트를 생성 하는 통신 클라이언트 팩터리로 구현 된 hello 기본 인터페이스를 정의 합니다. 안녕 구현의 hello CommunicationClientFactory hello 클라이언트가 toocommunicate 여기서 hello 서비스 패브릭 서비스에서 사용 하는 hello 통신 스택을에 따라 달라 집니다. hello 신뢰할 수 있는 서비스 API를 제공는 `CommunicationClientFactoryBase<TCommunicationClient>`합니다. 이 hello CommunicationClientFactory 인터페이스의 기본 구현을 제공 하 고 일반적인 tooall hello 통신 스택과 된 작업을 수행 합니다. (이러한 작업을 포함할 ServicePartitionResolver toodetermine hello 서비스 끝점을 사용 하 여). 클라이언트는 일반적으로 특정 toohello 통신 스택을 있는 hello 추상 CommunicationClientFactoryBase 클래스 toohandle 논리를 구현 합니다.

hello 통신 클라이언트 주소 방금 받아 tooconnect tooa 서비스를 사용 합니다. hello 클라이언트는 원하는 프로토콜을 사용할 수 있습니다.

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

hello 클라이언트 팩터리는 통신 클라이언트 작성을 주로 담당 합니다. HTTP 클라이언트 등의 영구 연결을 유지 하지 않는 클라이언트에 대 한 hello 팩터리 toocreate와 반환 hello 클라이언트에만 필요 합니다. 일부 이진 프로토콜 등의 영구 연결을 유지 관리 하는 다른 프로토콜도 유효성을 검사 해야 hello 팩터리 toodetermine 하 여 hello 연결 toobe 다시 생성 해야 하는지 여부를 합니다.  

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

마지막으로 예외 처리기는 예외가 발생할 때 어떤 작업 tootake를 결정 합니다. 예외는 **다시 시도 가능** 및 **다시 시도 불가능**으로 분류됩니다.

* **다시 시도할 수 없는** 예외 단순히 가져오기 다시 throw 백 toohello 호출자입니다.
* **다시 시도 가능** 예외는 **일시적** 및 **영구** 예외로 더 세분화됩니다.
  * **일시적인** 예외는 단순히 다시 hello 서비스 끝점 주소를 확인 하지 않고 다시 시도할 수 있습니다. 여기에 일시적인 네트워크 문제 또는 hello 서비스 끝점 주소를 지정 하지 않은 서비스 오류 응답과 존재 하지 않습니다.
  * **일시적이 지 않은** 예외는 hello 서비스 끝점 주소 toobe 다시 확인 해야 하는 것입니다. 여기에 hello 서비스 끝점에 연결할 수 없습니다, hello 서비스 tooa 다른 노드로 이동할가 표시 여부를 나타내는 예외 포함 됩니다.

hello `TryHandleException` 주어진된 예외에 대 한 결정을 내립니다. 경우 것 **를 알지 못하고** 돌아가야 하는 예외에 대 한 어떤 결정 toomake **false**합니다. 경우 것 **알고** 어떤 의사 결정 toomake hello 결과 적절 하 게 설정 하 고 반환 **true**합니다.

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
### <a name="putting-it-all-together"></a>모든 항목 요약
와 `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, 및 `IExceptionHandler(C#) / ExceptionHandler(Java)` 통신 프로토콜을 기반으로 구축 된 `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` 모두 함께 배치 되 고 hello 오류 처리 및 서비스 파티션 주소 확인 루프 이러한 구성 요소를 기준 제공 합니다.

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

## <a name="next-steps"></a>다음 단계
* [GitHub의 C# 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) 또는 [GitHUb의 Java 샘플 프로젝트](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog)에서 서비스 간 HTTP 통신의 예제를 참조하세요.
* [Reliable Services 원격을 사용하여 원격 프로시저 호출](service-fabric-reliable-services-communication-remoting.md)
* [Reliable Services에서 OWIN을 사용하는 Web API](service-fabric-reliable-services-communication-webapi.md)
* [Reliable Services를 사용한 WCF 통신](service-fabric-reliable-services-communication-wcf.md)
