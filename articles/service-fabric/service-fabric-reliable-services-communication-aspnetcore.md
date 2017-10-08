---
title: "ASP.NET Core hello와 aaaService 통신 | Microsoft Docs"
description: "자세한 내용은 toouse ASP.NET 신뢰할 수 있는 서비스 상태 비저장 및 상태 저장 서비스의 핵심 방법입니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>Service Fabric Reliable Services의 ASP.NET Core

ASP.NET Core는 웹앱, IoT 앱 및 모바일 백 엔드와 같은 최신 클라우드 기반의 인터넷 연결 응용 프로그램을 빌드하기 위한 새로운 오픈 소스 겸 플랫폼 간 프레임워크입니다. 

이 문서는 hello를 사용 하 여 서비스 패브릭 신뢰할 수 있는 서비스에서 ASP.NET Core 서비스는 상세 가이드 toohosting **Microsoft.ServiceFabric.AspNetCore.** * NuGet 패키지의 집합입니다.

Service Fabric에서 ASP.NET Core의 소개 자습서 및 개발 환경 설정을 가져오는 방법에 대한 지침은 [ASP.NET Core를 사용하여 응용 프로그램에 대한 웹 프런트 엔드 구축](service-fabric-add-a-web-frontend.md)을 참조하세요.

이 문서의 나머지 부분 hello 익숙한 이미 ASP.NET Core 가정 합니다. 그렇지 않은 것이 좋습니다 hello를 읽는 경우 [ASP.NET Core 기본 사항](https://docs.microsoft.com/aspnet/core/fundamentals/index)합니다.

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>Hello 서비스 패브릭 환경에서 ASP.NET Core

ASP.NET Core 응용 프로그램 hello 전체.NET Framework, 현재 서비스 패브릭 서비스 에서만 실행할 수 있습니다 또는.NET Core에서 실행할 수 있습니다 하는 동안 전체.NET Framework hello 합니다. ASP.NET Core 서비스 패브릭 서비스를 빌드할 때 이러한 의미 해야 여전히 대상 전체.NET Framework hello 합니다.

ASP.NET Core는 Service Fabric에서 다음 두 가지 방식으로 사용할 수 있습니다.
 - **게스트 실행 파일로 호스팅됨** - 이 주로 사용 되는 toorun 기존 ASP.NET Core 응용 프로그램 서비스 패브릭에서 코드 변경 없이입니다.
 - **Reliable Service에서 실행** - 이 서비스 패브릭 런타임 hello와의 통합을 ASP.NET Core 상태 저장 서비스 수 있도록 합니다.

이 문서의 나머지 부분 hello toouse ASP.NET Core를 사용 하 여 신뢰할 수 있는 서비스 내 서비스 패브릭 SDK hello로 제공 되는 ASP.NET Core 통합 구성 요소를 hello 하는 방법을 설명 합니다. 

## <a name="service-fabric-service-hosting"></a>Service Fabric 서비스 호스팅

Service Fabric에서 서비스의 인스턴스 및/또는 복제본이 하나 이상 *서비스 호스트 프로세스*(서비스 코드를 실행하는 실행 파일)에서 실행됩니다. 서비스 작성자는 자신이 hello 서비스 호스트 프로세스 및 서비스 패브릭을 활성화 하 고 모니터링 있습니다.

기존 ASP.NET 5 tooMVC) (위쪽 System.Web.dll 통해 밀접 하 게 결합 된 tooIIS입니다. ASP.NET Core hello 웹 서버와 웹 응용 프로그램 간의 분리를 제공합니다. 이 웹 응용 프로그램 toobe 다른 웹 서버 간에 휴대용을 또한 수 있도록 웹 서버 toobe *자체 호스트*을 시작할 수는 웹 서버 사용자가 소유한 프로세스에 전용된 웹이 소유 하는 것과 반대로 tooa 프로세스로 IIS와 같은 서버 소프트웨어입니다. 

순서 toocombine 서비스 패브릭 서비스 및 게스트 실행 파일 또는 신뢰할 수 있는 서비스에서 ASP.NET에서 서비스 호스트 프로세스 내부에 수 toostart ASP.NET 여야 합니다. 자체 호스팅 ASP.NET Core toodo 수 있습니다.이 있습니다.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Reliable Service에서 ASP.NET Core 호스팅
일반적으로 ASP.NET Core 응용 프로그램 자체 호스팅된 응용 프로그램의 진입점 hello 등에서 WebHost를 만들어야 `static void Main()` 메서드에서 `Program.cs`합니다. 이 경우 hello WebHost의 hello 수명 주기는 hello 프로세스의 바인딩된 toohello 수명 주기를입니다.

![프로세스에서 ASP.NET Core 호스팅][0]

그러나 hello 응용 프로그램 진입점이 hello 바로 여기 toocreate 신뢰할 수 있는 서비스에서 WebHost, 해당 서비스의 인스턴스를 만들 수 있도록 hello 서비스 패브릭 런타임을 tooregister 서비스 형식을 hello 응용 프로그램 진입점만 사용 되므로 입력 합니다. hello WebHost 만들지 신뢰할 수 있는 서비스에서 자체입니다. Hello 서비스 호스트 프로세스 내에서 서비스 인스턴스 및/또는 복제본 여러 주기를 수행할 수 있습니다. 

Reliable Service 인스턴스는 `StatelessService` 또는 `StatefulService`에서 파생되는 서비스 클래스로 표현됩니다. 에 포함 된 서비스에 대 한 hello 통신 스택을 `ICommunicationListener` 서비스 클래스에서 구현 합니다. hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 패키지 구현을 포함 `ICommunicationListener` 시작 하 고 Kestrel 또는 WebListener 신뢰할 수 있는 서비스 중 하나에 대 한 hello ASP.NET Core 웹 호스트를 관리 합니다.

![Reliable Service에서 ASP.NET Core 호스팅][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ASP.NET Core ICommunicationListeners
hello `ICommunicationListener` hello Kestrel 및 WebListener 구현을 `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 패키지를 사용 하 여 패턴이 비슷한 하지만 특정 tooeach 웹 서버 약간 다른 작업을 수행 합니다. 

두 통신 수신기 hello 다음 인수를 사용 하는 생성자를 제공 합니다.
 - **`ServiceContext serviceContext`**: hello `ServiceContext` hello 서비스를 실행 하는 방법에 대 한 정보를 포함 하는 개체입니다.
 - **`string endpointName`**: hello 이름을 `Endpoint` ServiceManifest.xml에서 구성 합니다. 이 주로 두 hello 통신 수신기과 다: WebListener **필요** 는 `Endpoint` 구성, Kestrel는 손실 됩니다.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: `IWebHost`를 만들고 반환하는 사용자 구현 람다입니다. 이렇게 하면 tooconfigure `IWebHost` ASP.NET Core 응용 프로그램에서 사용 하는 일반적으로 hello 방법입니다. hello 람다는 URL을 제공 hello 서비스 패브릭 통합에 따라 사용자 옵션을 사용 하 고 hello에 대 한 생성 된 `Endpoint` 제공한 구성 합니다. URL 수정 하거나 수로 사용-toostart hello 웹 서버입니다.

## <a name="service-fabric-integration-middleware"></a>Service Fabric 통합 미들웨어
hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet 패키지에 포함 hello `UseServiceFabricIntegration` 확장 메서드를 `IWebHostBuilder` 서비스 패브릭 인식 미들웨어를 추가 하는 합니다. 이 미들웨어 구성 Kestrel hello 또는 WebListener `ICommunicationListener` tooregister를 고유한 서비스 URL로 서비스 패브릭 명명 서비스 hello 하 고 유효성을 검사 한 다음 toohello 올바른 서비스를 연결 하는 클라이언트 요청 tooensure 클라이언트입니다. 이 서비스 패브릭에서 여러 웹 응용 프로그램 같은 실제 또는 가상 컴퓨터 hello에서 실행할 수는 있지만 실수로 toohello 잘못 된 서비스를 연결 하지 못하도록 tooprevent 클라이언트, 고유 호스트 이름을 사용 하지 않는 위치와 같은 공유 호스트 환경에 필요 합니다. 이 시나리오는 hello 다음 섹션에서 자세히 설명 합니다.

### <a name="a-case-of-mistaken-identity"></a>잘못된 ID의 경우
프로토콜에 관계없이 서비스 복제본은 고유한 IP:포트 조합에서 수신 대기합니다. Ip: port 끝점에서 수신 대기 서비스 복제본 시작 된 후 해당 끝점 주소 toohello 서비스 패브릭 명명 서비스 클라이언트나 다른 서비스에서 검색할 수 있습니다를 보고 합니다. 서비스 응용 프로그램 동적으로 할당 된 포트를 서비스 복제본에 사용할 수 있습니다 동시을 사용 하 여 이전에 있던 다른 서비스의 동일한 ip: port 끝점 hello 경우 hello 같은 실제 또는 가상 컴퓨터. 이렇게 하면 클라이언트 toomistakely toohello 잘못 된 서비스를 연결 합니다. 이 이벤트의 시퀀스를 수행 하는 hello 발생 하는 경우 발생할 수 있습니다.

 1. 서비스 A가 HTTP를 통해 10.0.0.1:30000에서 수신 대기합니다. 
 2. 클라이언트가 서비스 A를 확인하고 10.0.0.1:30000 주소를 가져옵니다.
 3. 서비스 A tooa 다른 노드로 이동합니다.
 4. 서비스 B 10.0.0.1에 배치 되 고 동시 사용 하 여 hello 30000 동일한 포트.
 5. 클라이언트와 캐시 된 주소 10.0.0.1:30000 tooconnect tooservice A를 시도합니다.
 6. 클라이언트는 성공적으로 연결 된 tooservice 인식 하지 못하는 B 연결 되어 이제 toohello 잘못 된 서비스입니다.

어려운 toodiagnose 일 수 있는 임의의 시간에 버그가 발생할 수 있습니다. 

### <a name="using-unique-service-urls"></a>고유한 서비스 URL 사용
이 서비스 tooprevent 끝점 toohello 고유 식별자를 가진 명명 서비스를 게시 하 고 다음 해당 고유 식별자의 유효성을 검사 하는 동안 클라이언트 요청 수입니다. 이 작업은 적대적이지 않은 테넌트가 신뢰할 수 있는 환경에서 서비스 간의 공동 작업이며, 적대적인 테넌트 환경에서는 보안 서비스 인증을 제공하지 않습니다.

신뢰할 수 있는 환경에서 hello 추가 되는 미들웨어를 hello `UseServiceFabricIntegration` 메서드 toohello 명명 서비스에 게시 되 고 해당 식별자 각 요청에 대해 유효성을 검사 하는 고유 식별자 toohello 주소를 자동으로 추가 합니다. Hello 식별자와 일치 하지 않으면 hello 미들웨어는 즉시 HTTP 410 없음 응답을 반환 합니다.

동적으로 할당된 포트를 사용하는 서비스는 이 미들웨어를 사용해야 합니다.

고유한 고정 포트를 사용하는 서비스는 공동 작업 환경에서 이 문제를 가지고 있지 않습니다. 고정된 고유한 포트를 클라이언트 응용 프로그램 tooconnect에 대 한 잘 알려진 포트를 해야 하는 외부 서비스에 일반적으로 사용 됩니다. 예를 들어 대부분의 인터넷 연결 웹 응용 프로그램은 웹 브라우저 연결에 80 또는 443 포트를 사용합니다. 이 경우 고유 식별자 hello을 사용 하지 않아야 합니다.

hello 다음으로 보여 주는 다이어그램 hello 요청 흐름 hello 미들웨어를 사용 하도록 설정 합니다.

![Service Fabric ASP.NET Core 통합][2]

Kestrel와 WebListener `ICommunicationListener` 구현이이 메커니즘을 사용 하 여 정확 하 게 hello에서 같은 방식으로 합니다. WebListener 기본 hello를 사용 하 여 고유 URL 경로에 따라 요청을 내부적으로 구분할 수 있지만 *http.sys* 포트 기능을 하는 기능을 공유 *하지* hello WebListener 에서사용하는`ICommunicationListener` 구현 하므로 앞에서 설명한 hello 시나리오에서 HTTP 503 및 HTTP 404 오류 상태 코드에서 발생 하 합니다. 차례로 어려워집니다 매우 hello 오류의 클라이언트 toodetermine hello 의도 대 한 HTTP 503 및 HTTP 404는 자주 사용 되는 tooindicate 이미 다른 오류를. 따라서 Kestrel와 WebListener `ICommunicationListener` 구현 hello에서 제공 하는 hello 미들웨어에서 표준화 `UseServiceFabricIntegration` 확장 메서드 클라이언트는 서비스 끝점이 tooperform 하기만 다시 해결 있도록 410 HTTP 응답에 대해 작업 합니다.

## <a name="weblistener-in-reliable-services"></a>Reliable Services의 WebListener
Hello를 가져와서 신뢰할 수 있는 서비스에서 사용할 수 WebListener **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet 패키지 합니다. 이 패키지에 포함 `WebListenerCommunicationListener`의 구현을 `ICommunicationListener`, 사용할 수 있는 신뢰할 수 있는 서비스 내에 ASP.NET Core WebHost toocreate WebListener hello 웹 서버로 사용 합니다.

WebListener hello 기반 [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx)합니다. Hello를 사용 하 여이 *http.sys* 커널 드라이버 IIS tooprocess HTTP에서 사용 하는 요청 하 고 웹 응용 프로그램을 실행 하는 게 tooprocesses 라우팅합니다. 이렇게 하면 hello에서 여러 프로세스 동일한 물리적 컴퓨터 또는 가상 컴퓨터 toohost 웹 응용 프로그램에 hello 동일한 포트를 고유 URL 경로 또는 호스트 이름으로을 명확히 구분 합니다. 이러한 기능은 서비스 패브릭에서 유용 hello에 여러 웹 사이트를 호스팅하기 위한 동일한 클러스터입니다.

hello 다음 다이어그램에서는 WebListener hello를 사용 하는 방법을 *http.sys* 포트 공유에 대 한 windows 커널 드라이버:

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>상태 비저장 서비스의 WebListener
toouse `WebListener` 상태 비저장 서비스 재정의 hello `CreateServiceInstanceListeners` 메서드 및 반환 된 `WebListenerCommunicationListener` 인스턴스:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>상태 저장 서비스의 WebListener

`WebListenerCommunicationListener`상태 저장 서비스에서 사용 하기 위해 현재 설계 되지 않았습니다를 hello 기본 due toocomplications *http.sys* 포트 기능을 공유 합니다. 자세한 내용은 hello 섹션 WebListener와 동적 포트 할당에 다음을 참조 하세요. 상태 저장 서비스에 대 한 Kestrel는 웹 서버를 권장 하는 hello입니다.

### <a name="endpoint-configuration"></a>끝점 구성

`Endpoint` 구성은 hello WebListener를 포함 하 여 Windows HTTP Server API를 사용 하는 웹 서버에 대 한 필요 합니다. Hello Windows HTTP Server API를 사용 하는 웹 서버와 해당 URL을 예약 먼저 해야 *http.sys* (hello로 일반적으로 이렇게 [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) 도구). 이 작업을 수행하려면 기본적으로 서비스에 없는 상승된 권한이 필요합니다. hello에 대 한 옵션을 "http" 또는 "https" hello `Protocol` hello 속성 `Endpoint` 구성에 *ServiceManifest.xml* 사용 특히 tooinstruct hello 서비스 패브릭 런타임에서 tooregister 포함하는URL*http.sys* hello를 사용 하 여 사용자 대신 [ *강력한 와일드 카드* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL 접두사입니다.

예를 들어 tooreserve `http://+:80` 서비스에 대 한 hello 다음 구성을 사용 해야 ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

Toohello hello 끝점 이름을 전달 해야 하 고 `WebListenerCommunicationListener` 생성자:

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>정적 포트로 WebListener 사용
정적 포트 WebListener, toouse hello hello 포트 번호를 제공 `Endpoint` 구성:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>동적 포트로 WebListener 사용
toouse WebListener와 동적으로 할당 된 포트 생략 hello `Port` hello에 대 한 속성 `Endpoint` 구성:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

`Endpoint` 구성으로 할당된 동적 포트는 *호스트 프로세스당* 하나의 포트만 제공합니다. hello 호스팅 모델에서는 hello에서 호스팅된 여러 서비스 인스턴스 및/또는 복제본 toobe 현재 서비스 패브릭 동일한 프로세스를 각각 hello hello를 통해 할당 하는 경우 동일한 포트를 공유 합니다 즉 `Endpoint` 구성 합니다. 여러 WebListener 인스턴스 내부 hello를 사용 하는 포트를 공유할 수 *http.sys* 포트 기능을 사용 하지만 하는 공유에서 지원 하지 않는 `WebListenerCommunicationListener` 인해 클라이언트 요청에 대 한 소개 toohello 복잡 합니다. 동적 포트 사용에 대 한 Kestrel는 웹 서버를 권장 하는 hello입니다.

## <a name="kestrel-in-reliable-services"></a>Reliable Services의 Kestrel
Hello를 가져와서 신뢰할 수 있는 서비스에서 사용할 수 kestrel **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet 패키지 합니다. 이 패키지에 포함 `KestrelCommunicationListener`의 구현을 `ICommunicationListener`, 사용할 수 있는 신뢰할 수 있는 서비스 내에 ASP.NET Core WebHost toocreate Kestrel hello 웹 서버로 사용 합니다.

Kestrel은 libuv(플랫폼 간 비동기 I/O 라이브러리)를 기반으로 하는 ASP.NET Core용 플랫폼 간 웹 서버입니다. WebListener와 달리 Kestrel은 *http.sys*와 같은 중앙 집중식 끝점 관리자를 사용하지 않으며, 여러 프로세스 간의 포트 공유도 지원하지 않습니다. Kestrel의 각 인스턴스는 고유한 포트를 사용해야 합니다.

![Kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>상태 비저장 서비스의 Kestrel
toouse `Kestrel` 상태 비저장 서비스 재정의 hello `CreateServiceInstanceListeners` 메서드 및 반환 된 `KestrelCommunicationListener` 인스턴스:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>상태 저장 서비스의 Kestrel
toouse `Kestrel` 상태 저장 서비스 재정의 hello `CreateServiceReplicaListeners` 메서드 및 반환 된 `KestrelCommunicationListener` 인스턴스:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

이 예제에서는의 singleton 인스턴스를 `IReliableStateManager` toohello WebHost 종속성 주입 컨테이너를 제공 합니다. 이 반드시 필요 하지만 toouse 가능 `IReliableStateManager` 및 MVC 컨트롤러 동작 메서드에서 신뢰할 수 있는 컬렉션입니다.

`Endpoint` 구성 이름이 **하지** 너무 제공`KestrelCommunicationListener` 상태 저장 서비스에 있습니다. Hello 다음 섹션에서에서 자세히 설명 합니다.

### <a name="endpoint-configuration"></a>끝점 구성
`Endpoint` 구성이 필요한 toouse Kestrel 않습니다. 

Kestrel 간단한 독립 실행형 웹 서버인; WebListener (또는 HttpListener)와 달리 필요 하지 않습니다는 `Endpoint` 에서 구성을 *ServiceManifest.xml* URL 등록 이전 toostarting 필요 하지 않습니다. 

#### <a name="use-kestrel-with-a-static-port"></a>정적 포트로 Kestrel 사용
Hello에서 정적 포트를 구성할 수 있습니다 `Endpoint` ServiceManifest.xml의 Kestrel 사용 하도록 구성 합니다. 이는 반드시 필요한 것이 아니지만 잠재적인 두 가지 이점을 제공합니다.
 1. Hello 포트 hello 응용 프로그램 포트 범위에 해당 하지 않으면, 열릴 hello OS 방화벽을 통해 서비스 패브릭에서.
 2. 통해 제공 된 URL tooyou hello `KestrelCommunicationListener` 이 포트를 사용 합니다.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

경우는 `Endpoint` 는 구성 이름에 전달 되어야 hello `KestrelCommunicationListener` 생성자: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

경우는 `Endpoint` 구성이 사용 되지 않습니다, hello에 hello 이름을 생략 `KestrelCommunicationListener` 생성자입니다. 이 경우 동적 포트가 사용됩니다. Hello에 대 한 자세한 내용은 다음 섹션을 참조 하십시오.

#### <a name="use-kestrel-with-a-dynamic-port"></a>동적 포트로 Kestrel 사용
Kestrel hello에서 hello 자동 포트 할당을 사용할 수 없습니다 `Endpoint` ServiceManifest.xml에 구성 되므로에서 자동 포트 할당은 `Endpoint` 구성 당 고유한 포트 할당 *호스트 프로세스* 를 단일 호스트 프로세스는 여러 Kestrel 인스턴스를 포함할 수 있습니다. 각 Kestrel 인스턴스를 고유한 포트에서 열어야 하지만 Kestrel에서 포트 공유를 지원하지 않기 때문에 이 기능은 작동하지 않습니다.

Kestrel를 사용 하 여 toouse 동적 포트 할당은 단순히 hello 생략 `Endpoint` ServiceManifest.xml에서 구성을 완전히 끝점 이름 toohello를 통과 하지 못한 및 `KestrelCommunicationListener` 생성자:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

이 구성에서는 `KestrelCommunicationListener` hello 응용 프로그램 포트 범위에서 사용 되지 않는 포트를 자동으로 선택 합니다.

## <a name="scenarios-and-configurations"></a>시나리오 및 구성
Hello 다음 시나리오를 설명 하 고 hello 권장 웹 서버, 포트 구성, 서비스 패브릭 통합 옵션 및 기타 설정이 tooachieve 조합의 정상적으로 작동 하는 서비스를 제공 하는이 섹션:
 - 외부에 노출된 ASP.NET Core 상태 비저장 서비스
 - 내부 전용 ASP.NET Core 상태 비저장 서비스
 - 내부 전용 ASP.NET Core 상태 저장 서비스

**외부로 노출** 서비스는 일반적으로 부하 분산 장치를 통해 hello 클러스터 외부에서 연결할 수 있는 끝점을 노출 하는 하나입니다.

**내부 전용** 서비스는 중요 한 한 끝점이 hello 클러스터 내에서 연결할 수 있습니다.

> [!NOTE]
> 인터넷 toohello를 노출 하는 상태 저장 서비스의 끝점 일반적으로 되지 않아야 합니다. Hello 부하 분산 장치 하지 수 toolocate 되며 트래픽 toohello 라우팅할 이므로 hello Azure 부하 분산 장치 등의 서비스 패브릭 서비스 해상도 인식 하지 않은 부하 분산 장치 뒤에 있는 클러스터 수 없습니다 tooexpose 상태 저장 서비스를 됩니다. 적절 한 상태 저장 서비스 복제본입니다. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>외부에 노출된 ASP.NET Core 상태 비저장 서비스
WebListener는 hello Windows에서 외부, 인터넷 연결 HTTP 끝점을 노출 하는 프런트 엔드 서비스에 대 한 웹 서버를 권장 합니다. 공격에 대한 더 나은 보호를 제공하고, Windows 인증 및 포트 공유와 같이 Kestrel에서 지원하지 않는 기능을 지원합니다. 

현재 Kestrel은 에지(인터넷 연결) 서버로 지원되지 않습니다. IIS 또는 Nginx와 같은 역방향 프록시 서버를 사용 해야 toohandle 트래픽만 hello 공용 인터넷 합니다.
 
노출 된 toohello 인터넷을 상태 비저장 서비스 부하 분산 장치를 통해 연결할 수 있는 잘 알려진과 안정적인 끝점을 사용 해야 합니다. 응용 프로그램의 toousers 제공한 hello URL입니다. 같은 구성이 hello는 사용 하는 것이 좋습니다.

|  |  | **참고 사항** |
| --- | --- | --- |
| 웹 서버 | WebListener | Hello 서비스는 노출 된 tooa 신뢰할 수 있는 네트워크만, 이러한 인트라넷 Kestrel은 사용할 수 있습니다. 그렇지 않으면 WebListener hello 기본 옵션입니다. |
| 포트 구성 | 정적 | Hello에서 잘 알려진 정적 포트를 구성 해야 `Endpoints` 80 HTTP 또는 HTTPS의 경우 443 같은 ServiceManifest.xml의 구성 합니다. |
| ServiceFabricIntegrationOptions | 없음 | hello `ServiceFabricIntegrationOptions.None` hello 서비스는 고유 식별자에 대 한 toovalidate 들어오는 요청 하지 않도록 서비스 패브릭 통합 미들웨어를 구성 하는 경우 옵션을 사용 해야 합니다. Hello 고유한 식별 정보가 hello 미들웨어에서 사용 하는 응용 프로그램의 외부 사용자가 확인할 수 없습니다. |
| 인스턴스 수 | -1 | 일반적인 사용 사례, hello 인스턴스 개수 설정은 설정 해야 너무 "-1" 인스턴스를 부하 분산 장치에서 트래픽을 수신 하는 모든 노드에서 사용할 수 있도록 합니다. |

노드 집합이 동일한 hello를 공유 하는 여러 외부에서 노출 된 서비스 경우 고유 하지만 안정 된 URL 경로 사용 해야 합니다. 이 IWebHost 구성할 때 제공 된 hello URL을 수정 하 여 수행할 수 있습니다. Note tooWebListener만 적용 됩니다.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>내부 전용 ASP.NET Core 상태 비저장 서비스
Hello 클러스터 내에서 호출 되는 상태 비저장 서비스 Url이 고유 해야 하며 여러 서비스 간에 tooensure 협력 포트를 동적으로 할당 합니다. 같은 구성이 hello는 사용 하는 것이 좋습니다.

|  |  | **참고 사항** |
| --- | --- | --- |
| 웹 서버 | Kestrel | 내부 상태 비저장 서비스에 대 한 WebListener를 사용할 수 있지만 Kestrel hello 권장 서버 tooallow 여러 서비스 인스턴스 tooshare 호스트입니다.  |
| 포트 구성 | 동적으로 할당 | 상태 저장 서비스의 여러 복제본에서 호스트 프로세스 또는 호스트 운영 체제를 공유할 수 있으므로 고유한 포트가 필요합니다. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | 이 설정은 동적 포트 할당을 앞에서 설명한 잘못 표시 하는 hello identity 문제를 방지 합니다. |
| InstanceCount | 모든 | hello 인스턴스 개수 설정은 tooany 값 필요한 toooperate hello 서비스를 설정할 수 있습니다. |

### <a name="internal-only-stateful-aspnet-core-service"></a>내부 전용 ASP.NET Core 상태 저장 서비스
Hello 클러스터 내에서 호출 되는 상태 저장 서비스는 여러 서비스 간에 tooensure 협조를 동적으로 할당 된 포트를 사용 해야 합니다. 같은 구성이 hello는 사용 하는 것이 좋습니다.

|  |  | **참고 사항** |
| --- | --- | --- |
| 웹 서버 | Kestrel | hello `WebListenerCommunicationListener` 복제본 호스트 프로세스를 공유 하는 상태 저장 서비스에서 사용 하기 위해 설계 되지 않았습니다. |
| 포트 구성 | 동적으로 할당 | 상태 저장 서비스의 여러 복제본에서 호스트 프로세스 또는 호스트 운영 체제를 공유할 수 있으므로 고유한 포트가 필요합니다. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | 이 설정은 동적 포트 할당을 앞에서 설명한 잘못 표시 하는 hello identity 문제를 방지 합니다. |

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 서비스 패브릭 응용 프로그램 디버그](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
