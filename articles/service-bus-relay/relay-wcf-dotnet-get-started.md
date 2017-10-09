---
title: ".NET에서 Azure 릴레이 WCF 릴레이 aaaGet 시작 | Microsoft Docs"
description: "Azure 릴레이 WCF toouse 서로 다른 위치에서 호스팅되는 tooconnect 두 응용 프로그램을 릴레이 하는 방법에 대해 알아봅니다."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Azure 릴레이 WCF toouse.NET에서 릴레이 하는 방법
이 문서에서는 toouse Azure 릴레이 서비스를 hello 하는 방법을 설명 합니다. hello 샘플 C#으로 작성 및 hello 서비스 버스 어셈블리에에서 포함 된 확장 된 hello Windows Communication Foundation (WCF) API를 사용 합니다. Azure 릴레이 대 한 자세한 내용은 참조 hello [Azure 릴레이 개요](relay-what-is-it.md)합니다.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>WCF 릴레이란?

Azure hello [ *WCF 릴레이* ](relay-what-is-it.md) 서비스를 통해 Azure 데이터 센터와 자신의 온-프레미스 엔터프라이즈 환경에서 실행 되는 toobuild 하이브리드 응용 프로그램 있습니다. hello 릴레이 서비스가이 용이 하 게 수 있게 함으로써 toosecurely tooopen 방화벽 연결 하지 않거나 없이도 회사의 엔터프라이즈 네트워크 toohello 공용 클라우드 내에 있는 Windows Communication Foundation (WCF) 서비스를 노출 합니다. 개입 수준이 변경 tooa 회사 네트워크 인프라를 사용 합니다.

![WCF 릴레이 개념](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Azure 릴레이 기존 엔터프라이즈 환경 내에서 WCF 서비스를 toohost 있습니다. 그런 다음 서비스에 대 한 들어오는 세션 및 요청 toothese WCF toohello 릴레이 Azure 내에서 실행 중인 수신 대기를 위임할 수 있습니다. 이 통해 tooexpose 하는 Azure 또는 toomobile 작업자 또는 파트너 엑스트라넷 환경에서 실행 되는 이러한 서비스 tooapplication 코드. 릴레이 통해 세분화 된 수준에서 이러한 서비스에 액세스할 수 있는 toosecurely 제어할을 수 있습니다. 강력 하 고 안전한 방법 tooexpose 응용 프로그램 기능 및 기존 엔터프라이즈 솔루션 및 활용이 hello 클라우드에서 데이터를 제공합니다.

이 문서에서는 Azure 릴레이 toocreate toouse WCF 웹 서비스를 노출 하는 방법을 두 당사자 간에 보안 대화를 구현 하는 TCP 채널 바인딩을 사용 하 여 설명 합니다.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Service Bus NuGet 패키지를 hello
hello [Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus) hello 가장 쉬운 방법은 tooget hello 서비스 버스 API 및 tooconfigure hello 서비스 버스 종속성의 모든 응용 프로그램은 합니다. 프로젝트에서 tooinstall hello NuGet 패키지는 다음 hello지 않습니다.

1. 솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.
2. "서비스 버스" 및 선택 hello에 대 한 검색 **Microsoft Azure 서비스 버스** 항목입니다. 클릭 **설치** toocomplete hello 설치의 경우 다음 hello 다음 대화 상자를 닫습니다.
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>SOAP 웹 서비스를 노출하고 TCP와 함께 이용
통해 외부 기존 WCF SOAP 웹 서비스 tooexpose 변경 toohello 서비스 바인딩 및 주소와 확인 해야 합니다. 이 tooyour 구성 파일을 변경 해야 하거나 설정 하 고 구성 된 WCF 서비스는 방법에 따라 코드 변경 내용을 채워야 합니다. WCF toohave 있는지 있습니다 참고 여러 네트워크 끝점을 통해 동일한 서비스 hello, hello 기존 유지할 수 있도록 외부에 대 한 릴레이 끝점을 추가 하는 동안 내부 끝점에 액세스 hello 동일한 시간입니다.

이 태스크에서는 간단한 WCF 서비스를 빌드 및 릴레이 수신기 tooit 추가 합니다. 이 연습 Visual studio에 대해 어느 정도 알고 있다고 가정 하 고 프로젝트를 만드는 모든 hello 세부 정보를 통해 이동 하지 않습니다. 대신, hello 코드 중점적으로 설명 합니다.

다음이 단계를 시작 하기 전에 hello 환 결 프로시저 tooset 다음을 완료 합니다.

1. Visual Studio 내에서 두 개의 프로젝트가 "클라이언트" 및 "서비스" hello 솔루션 내를 포함 하는 콘솔 응용 프로그램을 만듭니다.
2. Hello Service Bus NuGet 패키지 tooboth 프로젝트를 추가 합니다. 이 패키지는 모든 hello 필요한 어셈블리 참조 tooyour 프로젝트를 추가 합니다.

### <a name="how-toocreate-hello-service"></a>Toocreate 서비스 hello 하는 방법
먼저 hello 서비스 자체를 만듭니다. 모든 WCF 서비스는 적어도 다음 세 가지 요소로 구성되어 있습니다.

* 메시지를 교환 하 고 어떤 작업은 호출 toobe 설명 하는 계약의 정의입니다.
* 해당 계약의 구현
* Hello WCF 서비스를 호스트 하 고 여러 끝점을 노출 하는 호스트입니다.

이 단원의 hello 코드 예제에서는 이러한 각 구성이 요소를 해결합니다.

한 번의 작업을 정의 하는 hello 계약 `AddNumbers`, 두 개의 숫자를 추가 하 고 hello 결과 반환 합니다. hello `IProblemSolverChannel` 인터페이스 사용 hello 클라이언트 toomore는 쉽게 hello 프록시 수명을 관리 합니다. 이러한 인터페이스 생성은 모범 사례로 간주됩니다. 것이 좋습니다 tooput이 계약 별도 파일에는 정의 "클라이언트"와 "서비스" 프로젝트에서 해당 파일을 참조할 수 있지만 두 프로젝트 모두에 hello 코드를 복사할 수도 있습니다.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

Hello 계약 준비에서, 구현 hello는 다음과 같습니다.

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>프로그래밍 방식으로 서비스 호스트를 구성
Hello 계약 및 위치에 대 한 구현을 사용 하 여 hello 서비스를 호스트할 수 있습니다. 호스트 내에서 발생 한 [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) hello 서비스 인스턴스를 관리 처리는 개체를 호스트 hello 메시지를 수신 대기 하는 끝점입니다. hello 다음 코드 hello 및 서비스를 구성 모두 일반 로컬 끝점은 릴레이 끝점 tooillustrate hello 형태를 나란히 내부 및 외부 끝점의 합니다. Hello 문자열 대체 *네임 스페이스* 네임 스페이스 이름을 가진 및 *yourKey* hello 이전 설치 단계에서 얻은 hello SAS 키를 가진 합니다.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

Hello에 있는 두 개의 끝점을 만들면 hello 예제에서는 같은 계약 구현 합니다. 하나는 로컬 끝점이며 다른 하나는 Azure Relay를 통해 프로젝션됩니다. hello 주요 차이점은, hello 바인딩 [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) 로컬 hello에 대 한 및 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) hello 릴레이 끝점 및 hello 주소에 대 한 합니다. hello 로컬 끝점에는 고유한 포트와 로컬 네트워크 주소입니다. hello 릴레이 끝점에는 hello 문자열의 구성 된 끝점 주소 `sb`, 네임 스페이스 이름 및 "찾기" hello 경로 이 인해 hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, 정규화 된 외부 DNS 이름으로 서비스 버스 (릴레이) TCP 끝점으로 hello 서비스 끝점을 식별 합니다. Hello 자리 표시자 hello로 바꿔 hello 코드를 추가 하는 경우 `Main` 함수 hello의 **서비스** 응용 프로그램을 작동 하는 서비스를 갖습니다. 사용자 서비스 toolisten hello 릴레이에 대해서만 하려는 경우에 hello 로컬 끝점 선언을 제거 합니다.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Hello App.config 파일에서 서비스 호스트를 구성 합니다.
Hello App.config 파일을 사용 하 여 hello 호스트를 구성할 수 있습니다. hello 서비스 코드를이 예제의 호스팅 hello 다음 예제에 표시 됩니다.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

hello 끝점 정의 hello App.config 파일로 이동 합니다. hello NuGet 패키지는 이미 정의 toohello App.config 파일의 범위를 추가 Azure 릴레이 대 한 필요한 hello 구성 확장은입니다. 다음 예제는 hello 정확한 hello hello 이전 코드에 해당 하는 hello 바로 아래에 표시 되어야 **system.serviceModel** 요소입니다. 이 코드 예제에서는 프로젝트 C# 네임스페이스의 이름이 **Service**라고 가정합니다.
릴레이 네임 스페이스 이름 및 SAS 키와 함께 hello 자리 표시자를 대체 합니다.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

이러한 변경을 수행한 후 hello 서비스가 시작 되 다가, 이전 처럼 두 개의 라이브 끝점으로: 하나의 로컬 및 hello 클라우드에서 하나의 수신 대기 합니다.

### <a name="create-hello-client"></a>Hello 클라이언트 만들기
#### <a name="configure-a-client-programmatically"></a>프로그래밍 방식으로 클라이언트를 구성
tooconsume hello 서비스를 사용 하 여 WCF 클라이언트를 생성할 수 있습니다는 [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) 개체입니다. 서비스 버스는 SAS를 사용하여 구현된 토큰 기반 보안 모델을 사용합니다. hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) 클래스 일부 잘 알려진 토큰 공급자를 반환 하는 기본 제공 팩터리 메서드로 보안 토큰 공급자를 나타냅니다. hello 다음 예제에서는 hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) hello 적절 한 SAS 토큰의 메서드 toohandle hello 획득 합니다. hello 이름과 키를는 hello 이전 섹션에 설명 된 대로 hello 포털에서 가져온 것입니다.

첫 번째, 참조 또는 복사 hello `IProblemSolver` hello 서비스에서 코드를 클라이언트 프로젝트에 계약입니다.

그런 다음 hello의 hello 코드를 대체 `Main` 다시 릴레이 네임 스페이스 및 SAS 키와 함께 hello 개체 틀 텍스트를 대체 하는 hello 클라이언트의 메서드.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

이제 hello 클라이언트와를 실행 하는 hello 서비스를 빌드할 수 있습니다 (hello 서비스를 먼저 실행), hello 클라이언트 hello 서비스를 호출 하 고 출력 및 **9**합니다. 실행할 수 있습니다 hello 클라이언트와 서버가 서로 다른 컴퓨터에서 네트워크를 통해 및 hello 통신은 계속 작동 합니다. hello 클라이언트 코드 hello 클라우드 또는 로컬로 실행할 수도 있습니다.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Hello App.config 파일에 있는 클라이언트 구성
코드 다음 hello tooconfigure hello 클라이언트를 사용 하 여 App.config 파일을 hello 하는 방법을 보여 줍니다.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

hello 끝점 정의 hello App.config 파일로 이동 합니다. hello은 앞에 나열 된 hello 코드와 같은 hello, 다음 예제에서는 직접 아래에 나타납니다 hello `<system.serviceModel>` 요소입니다. 여기에서 이전 처럼 바꿔야 hello 자리 표시자 릴레이 네임 스페이스 및 SAS 키와 함께 합니다.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>다음 단계
릴레이 Azure의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [Azure 릴레이란?](relay-what-is-it.md)
* [Azure Service Bus 아키텍처 개요](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* 서비스 버스 예제를 다운로드할 [Azure 샘플] [ Azure samples] hello 참조 또는 [서비스 버스 예제 개요][overview of Service Bus samples]합니다.

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
