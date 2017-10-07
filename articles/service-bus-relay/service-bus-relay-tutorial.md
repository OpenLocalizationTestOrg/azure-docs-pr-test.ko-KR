---
title: "서비스 버스 WCF 릴레이 자습서 aaaAzure | Microsoft Docs"
description: "WCF Relay를 사용하여 Service Bus 클라이언트 응용 프로그램과 서비스를 빌드합니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Azure WCF 릴레이 자습서

이 자습서에서는 간단한 WCF 릴레이 하는 toobuild 방법을 설명 하 고 Azure 릴레이 사용 하 여 서비스 클라이언트 응용 프로그램입니다. [Service Bus 메시징](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)을 사용하는 유사한 자습서는 [Service Bus 큐 시작](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)을 참조하세요.

이 자습서를 통해 작업 hello 단계를 필요한 toocreate WCF 릴레이 클라이언트와 서비스 응용 프로그램의 이해를 제공 합니다. 기존 WCF 대응처럼 서비스는 하나 이상의 끝점을 노출하는 구문으로, 각각 하나 이상의 서비스 작업을 노출합니다. 서비스의 끝점 hello hello 서비스를 찾을 수 있는, 주소 hello 서비스 tooits 클라이언트에서 제공 하는 hello 기능을 정의 하는 계약 hello 서비스와 통신 하는 hello 정보를 포함 하는 바인딩을 지정 합니다. hello는 주요 차이점이 WCF와 WCF 릴레이 컴퓨터에 로컬로 대신 hello 클라우드에서 해당 hello 끝점이 노출 됩니다.

이 자습서의 항목 hello 시퀀스를 통해 작업 한 후 hello 서비스의 hello 작업을 호출할 수 있는 클라이언트 및 서비스를 실행 해야 합니다. hello 첫 번째 항목에 설명 어떻게 tooset 계정. hello 다음 단계로 진행 방법을 toodefine 서비스 및 사용 하는 계약, 어떻게 tooimplement hello 서비스를 어떻게 tooconfigure hello 코드의 서비스입니다. 또한 설명 방법을 hello 서비스 toohost 및 실행 합니다. hello 만들어진 서비스는 자체 호스트 되며 hello에서 실행 하는 hello 클라이언트와 서비스가 동일한 컴퓨터. 코드 또는 구성 파일을 사용 하 여 hello 서비스를 구성할 수 있습니다.

toocreate 클라이언트 응용 프로그램을 hello 클라이언트 응용 프로그램을 구성 하 고 만들고 방법 hello 호스트의 hello 기능에 액세스할 수 있는 클라이언트를 사용 하 여 hello 마지막 세 단계에 설명 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 hello 필요 합니다.

* [Microsoft Visual Studio 2015 이상](http://visualstudio.com). 이 자습서에서는 Visual Studio 2017을 사용합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.

## <a name="create-a-service-namespace"></a>서비스 네임스페이스 만들기

hello 첫 번째 단계는 toocreate 네임 스페이스 및 tooobtain는 [공유 액세스 서명 (SAS)](../service-bus-messaging/service-bus-sas.md) 키입니다. 네임 스페이스 hello 릴레이 서비스를 통해 노출 된 각 응용 프로그램에 대 한 응용 프로그램 경계를 제공 합니다. SAS 키가 서비스 네임 스페이스를 만들 때 hello 시스템에서 자동으로 생성 됩니다. 서비스 네임 스페이스와 SAS 키 조합 hello Azure tooauthenticate access tooan 응용 프로그램에 대 한 hello 자격 증명을 제공합니다. Hello에 따라 [여기에 지침이](relay-create-namespace-portal.md) toocreate 릴레이 네임 스페이스입니다.

## <a name="define-a-wcf-service-contract"></a>WCF 서비스 계약 정의

hello 서비스 계약은 작업 (메서드 또는 함수에 대 한 hello 웹 서비스 용어) hello 서비스에서 지 원하는 사항를 지정합니다. 계약은 C++, C#, 또는 Visual Basic 인터페이스를 정의하여 만듭니다. Hello 인터페이스의 각 메서드에 tooa 특정 서비스 작업에 해당 합니다. 각 인터페이스 hello 있어야 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성이 tooit를 적용 하 고 각 작업에는 hello 있어야 합니다. [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit 특성이 적용 합니다. Hello 변수가 있는 인터페이스의 메서드가 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성에 hello 없는 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 특성을 메서드가 표시 되지 않습니다. 이러한 작업에 대 한 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다. 계약 및 서비스의 더 큰 논의 알려면 [서비스 디자인 및 구현](https://msdn.microsoft.com/library/ms729746.aspx) hello WCF 설명서에에서 있습니다.

### <a name="create-a-relay-contract-with-an-interface"></a>인터페이스와 함께 릴레이 계약 만들기

1. Hello에 hello 프로그램을 마우스 오른쪽 단추로 클릭 하 여 관리자 권한으로 Visual Studio를 열고 **시작** 메뉴에서 **관리자 권한으로 실행**합니다.
2. 새 콘솔 응용 프로그램 프로젝트를 만듭니다. Hello 클릭 **파일** 메뉴와 선택 **새로**, 클릭 **프로젝트**합니다. Hello에 **새 프로젝트** 대화 상자에서 클릭 **Visual C#** (경우 **Visual C#** 가 보이지 않으면에서 **다른 언어**). Hello 클릭 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일을 하 고 이름을 **EchoService**합니다. 클릭 **확인** toocreate hello 프로젝트.

    ![][2]

3. Hello Service Bus NuGet 패키지를 설치 합니다. 이 패키지는 hello WCF 뿐만 아니라 참조 toohello 서비스 버스 라이브러리에 자동으로 추가 **System.ServiceModel**합니다. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) tooprogrammatically 액세스 hello WCF의 기본 기능을 사용 하는 hello 네임 스페이스입니다. 서비스 버스는 여러 hello 개체 및 WCF toodefine 서비스 계약의 특성을 사용합니다.

    솔루션 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리...** . Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다. 해당 hello 프로젝트 이름을 hello에 선택 되어 있는지 확인 **버전** 상자입니다. 클릭 **설치**, hello 사용 약관을 수락 합니다.

    ![][3]
4. 솔루션 탐색기에서 hello Program.cs 파일 tooopen 아직 없는 경우 hello 편집기에서 열을 두 번 클릭 합니다.
5. Hello 다음 추가 hello 파일 hello 상단의 문을 사용 하 여:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. 기본 이름 만으로는 hello 네임 스페이스 이름 변경 **EchoService** 너무**Microsoft.ServiceBus.Samples**합니다.

   > [!IMPORTANT]
   > 이 자습서에서는 hello C# 네임 스페이스 **Microsoft.ServiceBus.Samples**, hello hello 구성 파일에서 사용 되는 형식을 관리 되는 계약 기반 hello의 hello 네임 스페이스는 [hello WCF 클라이언트구성](#configure-the-wcf-client) 단계입니다. 이 샘플; 빌드할 때 원하는 네임 스페이스를 지정할 수 있습니다. 그러나 hello 자습서 수정 하지 않는 한 다음 hello 계약 및 서비스의 네임 스페이스 hello 적절 하 게 hello 응용 프로그램 구성 파일에서 작동 하지 않습니다. hello 파일 이어야 App.config에에서 지정 된 hello 네임을 hello C# 파일에 지정 된 hello 네임 스페이스와 동일 합니다.
   >
   >
7. Hello 바로 뒤 `Microsoft.ServiceBus.Samples` 네임 스페이스 선언을 hello 네임 스페이스 내에서 이라는 새 인터페이스를 정의 하지만 `IEchoContract` hello 적용 `ServiceContractAttribute` 의 네임 스페이스 값을 가진 특성 toohello 인터페이스 `http://samples.microsoft.com/ServiceModel/Relay/`합니다. 코드의 hello 범위 전체에서 사용 하는 hello 네임 스페이스에서 네임 스페이스 값 hello 다릅니다. 대신, hello 네임 스페이스 값이이 계약에 대 한 고유 식별자로 사용 됩니다. Hello 네임 스페이스를 명시적으로 지정 하면 hello 기본 네임 스페이스 값을 toohello 계약 이름에 추가 되지 않습니다. Hello를 hello 네임 스페이스를 선언한 후 코드를 다음에 붙여 넣습니다.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > 일반적으로 hello 서비스 계약 네임 스페이스에 버전 정보를 포함 하는 명명 체계를 포함 합니다. Hello 서비스 계약 네임 스페이스에서 버전 정보를 포함 하 여 새 네임 스페이스로 새 서비스 계약을 정의 하 고 새 끝점에 노출 여 서비스 tooisolate 주요 변경 사항 수 있습니다. 이러한 방식으로 클라이언트 업데이트 toobe 필요 없이 toouse hello 이전 서비스 계약을 계속 수 있습니다. 버전 정보는 날짜 또는 빌드 번호로 구성될 수 있습니다. 자세한 내용은 [서비스 버전 관리](http://go.microsoft.com/fwlink/?LinkID=180498)를 참조하세요. 이 자습서의 hello 위해서 이름 지정 체계 hello 서비스 계약 네임 스페이스의 hello에 버전 정보
   >
   >
8. Hello 내 `IEchoContract` 인터페이스를 hello 단일 작업 hello에 대 한 메서드를 선언 `IEchoContract` hello에 노출 계약 인터페이스 및 hello 적용 `OperationContractAttribute` tooexpose의 일환으로 원하는 특성 toohello 방법을 hello 공용 WCF 릴레이 계약을 다음과 같이 합니다.

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Hello 바로 뒤 `IEchoContract` 인터페이스 정의 둘 다에서 상속 되는 채널을 선언 `IEchoContract` 및 또한 toohello `IClientChannel` 다음과 같이 인터페이스:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    채널은는 hello 호스트와 클라이언트가 전달 정보 tooeach 다른 hello WCF 개체입니다. 이상에서는 hello 두 응용 프로그램 간에 hello 채널 tooecho 정보에 대해 코드를 작성 합니다.
10. Hello에서 **빌드** 메뉴를 클릭 **솔루션 빌드** 하거나 키를 눌러 **Ctrl + Shift + B** tooconfirm hello 정확도 지금까지 작업 합니다.

### <a name="example"></a>예제

hello 코드 다음 WCF 릴레이 계약을 정의 하는 기본적인 인터페이스를 보여 줍니다.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

이제 hello 인터페이스를 만들었으므로 hello 인터페이스를 구현할 수 있습니다.

## <a name="implement-hello-wcf-contract"></a>Hello WCF 계약 구현

Azure 릴레이 만들기를 먼저 만들어야 인터페이스를 사용 하 여 정의 되는 hello 계약 필요 합니다. Hello 인터페이스를 작성 하는 방법에 대 한 자세한 내용은 hello 이전 단계를 참조 하세요. hello 다음 단계는 tooimplement hello 인터페이스입니다. 라는 클래스를 생성이 포함 됩니다 `EchoService` 구현 하는 사용자 정의 hello `IEchoContract` 인터페이스입니다. Hello 인터페이스를 구현한 후 hello 인터페이스는 App.config 구성 파일을 사용 하 여 구성 합니다. hello 구성 파일 hello hello 서비스 이름, hello 이름 hello 계약 및 hello 유형의 프로토콜을 사용 하는 toocommunicate hello 릴레이 서비스와 같은 hello 응용 프로그램에 필요한 정보를 포함 합니다. 이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다. Tooimplement 서비스 계약 하는 방법에 대 한 자세한 논의 알려면 [서비스 계약 구현](https://msdn.microsoft.com/library/ms733764.aspx) hello WCF 설명서에에서 있습니다.

1. 이라는 새 클래스를 만들 `EchoService` hello의 hello 정의 바로 뒤 `IEchoContract` 인터페이스입니다. hello `EchoService` 클래스 구현 hello `IEchoContract` 인터페이스입니다.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    비슷한 tooother 인터페이스 구현에 다른 파일에 hello 정의 구현할 수 있습니다. 그러나이 자습서에서는 hello 구현에 동일한 파일 hello 인터페이스 정의 및 hello hello `Main` 메서드.
2. Hello 적용 [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello 특성 `IEchoContract` 인터페이스입니다. hello 특성 hello 서비스 이름 및 네임 스페이스를 지정합니다. 이렇게 하면 hello `EchoService` 클래스에는 다음과 같이 표시 됩니다.

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. 구현 hello `Echo` hello에 정의 된 메서드 `IEchoContract` hello에 대 한 인터페이스 `EchoService` 클래스입니다.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. 클릭 **빌드**, 클릭 **솔루션 빌드** tooconfirm hello 여 작업이 정확 합니다.

### <a name="define-hello-configuration-for-hello-service-host"></a>Hello 서비스 호스트에 대 한 hello 구성 정의

1. hello 구성 파일은 매우 유사한 tooa WCF 구성 파일. 바인딩 (프로토콜을 사용 하는 toocommunicate hello 유형) hello 및 hello 서비스 이름, 끝점 (즉, hello 위치 서로 toocommunicate 클라이언트와 호스트에 대 한 Azure 릴레이 노출 하는), 포함 됩니다. hello 중요 한 차이점은이 구성 된 서비스 끝점 참조 tooa 한다고 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) 바인딩을 hello.NET Framework의 일부가 아닙니다. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hello 서비스에 의해 정의 된 hello 바인딩 중 하나입니다.
2. **솔루션 탐색기**, App.config 파일 tooopen hello를 두 번 클릭 hello Visual Studio 편집기에서.
3. Hello에 `<appSettings>` 요소 hello 자리 표시자 hello 서비스 네임 스페이스, 이름으로 대체 및 SAS 키를 이전 단계에서 복사한 hello 합니다.
4. Hello 내 `<system.serviceModel>` 태그, 추가 `<services>` 요소입니다. 단일 구성 파일 내에 여러 릴레이 응용 프로그램을 정의할 수 있습니다. 그러나 이 자습서에서는 하나만 정의합니다.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. Hello 내 `<services>` 요소를 추가 `<service>` 요소 toodefine hello hello 서비스 이름입니다.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. Hello 내 `<service>` 요소인 hello 끝점 계약의 hello 위치를 정의 하 고 또한 hello 끝점에 대 한 바인딩 형식을 hello 합니다.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    hello 끝점 hello 호스트 응용 프로그램에 대 한 hello 클라이언트를 찾을 위치를 정의 합니다. 이상 버전에서는 hello 자습서에서는이 단계 toocreate Azure 릴레이 통해 hello 호스트를 완벽 하 게 표시 하는 URI를 사용 합니다. hello 바인딩 hello 릴레이 서비스와 프로토콜 toocommunicate hello 대로 TCP 사용 함을 선언 합니다.
7. Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드** 작업이 tooconfirm hello 정확한 합니다.

### <a name="example"></a>예제

hello 다음 코드에서는 hello 서비스 계약의 hello 구현 된

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

hello 다음 코드에서는 hello hello 서비스 호스트와 연결 된 hello App.config 파일의 기본 형식

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>호스트 및 hello 릴레이 서비스와 기본 웹 서비스 tooregister 실행

이 단계에서는 Azure 릴레이 하는 toorun 어떻게 설명 서비스입니다.

### <a name="create-hello-relay-credentials"></a>Hello 릴레이 자격 증명 만들기

1. `Main()`hello hello 콘솔 창에서 읽는 SAS 키를 어떤 toostore hello 네임 스페이스에 두 개의 변수를 만들고 있습니다.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    hello SAS 키 프로젝트에 사용 되는 이후 tooaccess 됩니다. hello 네임 스페이스 매개 변수로 너무 전달`CreateServiceUri` toocreate 서비스 URI입니다.
2. 사용 하는 [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) 개체를 사용 하려는 SAS 키 hello 자격 증명 유형으로 선언 합니다. Hello 코드 hello 마지막 단계에서 추가한 hello 코드 바로 뒤에 다음을 추가 합니다.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Hello 서비스에 대 한 기본 주소를 만들려면

Hello hello 마지막 단계에서 추가한 코드 뒤 만들기는 `Uri` hello 기준 주소에 대 한 hello 서비스의 인스턴스. 이 URI는 hello 서비스 버스 체계, hello 네임 스페이스 및 hello 서비스 인터페이스의 hello 경로 지정합니다.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

"sb" hello 서비스 버스 체계에 대 한 약어로 hello 프로토콜로 TCP를 사용 함을 나타냅니다. Hello 구성 파일에 이전에 지정 된이 때 [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) hello 바인딩으로 지정 되었습니다.

이 자습서에 대 한 hello URI는 `sb://putServiceNamespaceHere.windows.net/EchoService`합니다.

### <a name="create-and-configure-hello-service-host"></a>만들기 및 hello 서비스 호스트를 구성 합니다.

1. 너무 hello 연결 모드를 설정`AutoDetect`합니다.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    hello 연결 모드와 hello 릴레이 서비스; hello 프로토콜 hello 서비스 사용 하 여 toocommunicate 설명 HTTP 또는 TCP입니다. Hello 기본 설정을 사용 하 여 `AutoDetect`, TCP를 사용할 수 없는 경우 hello 서비스를 사용할 수 있는 경우 TCP 및 HTTP를 통한 tooconnect tooAzure 릴레이 시도 합니다. 클라이언트 통신에 대 한 참고 hello 프로토콜 hello 서비스에서이 점에서 지정 합니다. 해당 프로토콜 사용 하는 hello 바인딩에 의해 결정 됩니다. 예를 들어 서비스 צ ְ ײ hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) 해당 끝점이 HTTP를 통해 클라이언트와 통신 하는 지정 하는 바인딩. 동일한 서비스 지정할 수 있었습니다 **ConnectivityMode.AutoDetect** hello 서비스와 통신 Azure 릴레이 TCP를 통한 되도록 합니다.
2. 이 섹션에서 만든 URI hello를 사용 하 여 hello 서비스 호스트를 만듭니다.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    hello 서비스 호스트는 hello 서비스를 인스턴스화하는 hello WCF 개체입니다. 여기에서는 공용 인터페이스로 전달 전달 hello 유형 toocreate 서비스의 원하는 (는 `EchoService` 유형), 및 tooexpose hello 서비스 원하는 toohello 주소도 합니다.
3. Hello Program.cs 파일의 hello 위쪽 참조를 너무 추가[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) 및 [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description)합니다.

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. 다시 `Main()`, hello 끝점 tooenable 공용 액세스를 구성 합니다.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    이 단계 응용 프로그램 프로젝트에 대 한 hello ATOM 피드를 검사 하 여 공개적으로 찾을 수 있음이 hello 릴레이 서비스에 알립니다. 설정한 경우 **DiscoveryType** 너무**개인**, 클라이언트는 여전히 수 tooaccess hello 서비스 수입니다. 그러나 hello 릴레이 네임 스페이스를 검색할 때 hello 서비스가 표시 되지 않습니다. 대신, 클라이언트 hello 것 tooknow hello 끝점 경로 순서를 사전입니다.
5. 적용 hello 서비스 hello App.config 파일에 정의 된 toohello 서비스 끝점 자격 증명:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Hello 이전 단계에서 언급 한 것 처럼 여러 서비스와 hello 구성 파일에서 끝점을 선언 했을 수 있습니다. 이 코드는 hello 구성 파일 및 검색을 트래버스을 설치한 경우 모든 끝점 toowhich에 대 한 자격 증명을 적용 해야 합니다. 그러나이 자습서에서는 hello 구성 파일에 끝점이 하나 뿐입니다.

### <a name="open-hello-service-host"></a>열기 hello 서비스 호스트

1. Hello 서비스를 엽니다.

    ```csharp
    host.Open();
    ```
2. 알릴 안녕 서비스 hello 사용자를 실행 하 고 설명 방법을 tooshut hello 서비스를 합니다.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. 완료 되 면 hello 서비스 호스트를 닫습니다.

    ```csharp
    host.Close();
    ```
4. 키를 눌러 **Ctrl + Shift + B** toobuild hello 프로젝트.

### <a name="example"></a>예제

완료된 서비스 코드는 다음과 같이 표시됩니다. hello 코드 hello 서비스 계약과 구현이 포함 되어 이전 단계에서 hello 자습서에서 및 호스트 hello 서비스 콘솔 응용 프로그램.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Hello 서비스 계약에 대해 WCF 클라이언트 만들기

다음 단계 hello toocreate 클라이언트 응용 프로그램은 하 고 이후 단계에서 구현 하는 hello 서비스 계약을 정의 합니다. Toocreate 서비스를 사용 하는 hello 단계를 유사한 여러이 단계 참고: 자격 증명 tooconnect toohello 릴레이 서비스를 사용 하 여 파일 및 등 App.config를 편집 하는 계약을 정의 합니다. 이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.

1. Hello 다음을 수행 하 여 hello hello 클라이언트에 대 한 현재 Visual Studio 솔루션에서 새 프로젝트를 만듭니다.

   1. 솔루션 탐색기에서에 hello 서비스가 포함 된 동일한 솔루션 hello hello 현재 솔루션 (하지 hello 프로젝트)를 마우스 오른쪽 단추로 클릭 클릭 **추가**합니다. 그런 후 **새 프로젝트**를 클릭합니다.
   2. Hello에 **새 프로젝트 추가** 대화 상자를 클릭 **Visual C#** (경우 **Visual C#** 가 보이지 않으면 아래를 봅니다 **다른 언어**)을 선택 hello **콘솔 응용 프로그램 (.NET Framework)** 서식 파일을 하 고 이름을 **EchoClient**합니다.
   3. **확인**을 클릭합니다.
      <br />
2. 솔루션 탐색기에서 hello에 hello Program.cs 파일을 두 번 클릭 **EchoClient** 프로젝트 tooopen 아직 없는 경우 hello 편집기에서 엽니다.
3. 기본 이름 만으로는 hello 네임 스페이스 이름 변경 `EchoClient` 너무`Microsoft.ServiceBus.Samples`합니다.
4. Hello 설치 [Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus): 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **EchoClient** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다. Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다. 클릭 **설치**, hello 사용 약관을 수락 합니다.

    ![][3]
5. 추가 `using` hello에 대 한 문을 [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello Program.cs 파일의 네임 스페이스입니다.

    ```csharp
    using System.ServiceModel;
    ```
6. 다음 예제는 hello와 같이 hello 서비스 계약 정의 toohello 네임 스페이스를 추가 합니다. 이 정의 hello에 사용 되는 동일한 toohello 정의 **서비스** 프로젝트. Hello hello 위쪽에이 코드를 추가 해야 `Microsoft.ServiceBus.Samples` 네임 스페이스입니다.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. 키를 눌러 **Ctrl + Shift + B** toobuild hello 클라이언트입니다.

### <a name="example"></a>예제

hello 다음 코드에서는 hello Program.cs 파일의 현재 상태 hello hello **EchoClient** 프로젝트.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Hello WCF 클라이언트 구성

이 단계에서는이 자습서의 앞부분에서 만든 hello 서비스에 액세스 하는 기본적인 클라이언트 응용 프로그램에 대 한 App.config 파일을 만듭니다. 이 App.config 파일에는 hello 계약, 바인딩 및 hello 끝점의 이름을 정의합니다. 이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.

1. Hello의 솔루션 탐색기에서 **EchoClient** 두 번 클릭 **App.config** hello Visual Studio 편집기에서 tooopen hello 파일입니다.
2. Hello에 `<appSettings>` 요소 hello 자리 표시자 hello 서비스 네임 스페이스, 이름으로 대체 및 SAS 키를 이전 단계에서 복사한 hello 합니다.
3. Hello system.serviceModel 요소 내에서 추가 된 `<client>` 요소입니다.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    이 단계에서는 WCF 스타일 클라이언트 응용 프로그램을 정의함을 선언합니다.
4. Hello 내 `client` 요소인 hello 이름, 계약 및 hello 끝점에 대 한 바인딩 형식을 정의 합니다.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    이 단계에는 끝점 hello hello 서비스 및 클라이언트 응용 프로그램 hello toocommunicate TCP를 사용 하 여 Azure 릴레이 된 hello 팩트에 정의 된 hello 계약의 hello 이름을 정의 합니다. hello 끝점 이름이 사용 됩니다 hello 다음 단계에서 toolink hello 서비스 URI와이 끝점 구성입니다.
5. **파일**을 클릭한 다음 **모두 저장**을 클릭합니다.

## <a name="example"></a>예제

hello 다음 코드에서는 Echo 클라이언트 hello에 대 한 hello App.config 파일

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Hello WCF 클라이언트 구현
이 단계에서는이 자습서에서는 이전에 만든 hello 서비스에 액세스 하는 기본적인 클라이언트 응용 프로그램을 구현 합니다. 다양 한 hello 유사한 toohello 서비스 hello client 수행 동일한 작업 tooaccess Azure 릴레이:

1. Hello 연결 모드를 설정 합니다.
2. Hello hello 호스트 서비스를 찾는 URI를 만듭니다.
3. Hello 보안 자격 증명을 정의합니다.
4. Hello toohello 연결 시 자격 증명을 적용합니다.
5. Hello 연결을 엽니다.
6. Hello 응용 프로그램별 작업을 수행합니다.
7. Hello 연결을 닫습니다.

그러나 hello 주요 차이점 중 하나는 hello 클라이언트 응용 프로그램이 채널 tooconnect toohello 릴레이 서비스를 사용 하는 반면 hello 서비스 너무 호출 하 여**ServiceHost**합니다. 이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.

### <a name="implement-a-client-application"></a>클라이언트 응용 프로그램 구현
1. 너무 hello 연결 모드를 설정**자동 검색**합니다. Hello hello 내부에서 코드를 다음 추가 `Main()` hello 방식의 **EchoClient** 응용 프로그램입니다.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. 변수 toohold hello에 대 한 값 hello 서비스 네임 스페이스 및 SAS 키 hello 콘솔에서 읽기를 정의 합니다.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Hello 릴레이 프로젝트에서 hello 호스트의 hello 위치를 정의 하는 URI를 만듭니다.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. 서비스 네임 스페이스 끝점에 대 한 hello 자격 증명 개체를 만듭니다.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Hello App.config 파일에 설명 된 hello 구성을 로드 하는 hello 채널 팩터리를 만듭니다.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    채널 팩터리는 hello 서비스 및 클라이언트 응용 프로그램은 통신 채널을 만드는 WCF 개체입니다.
6. Hello 자격 증명을 적용 합니다.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. 만들고 hello 채널 toohello 서비스를 엽니다.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Hello 기본 사용자 인터페이스와 에코 hello에 대 한 기능을 작성 합니다.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    참고 hello 코드에서는 프록시로 hello 채널 개체의 hello 인스턴스 hello 서비스를 사용 합니다.
9. Hello 채널 및 닫기 hello 팩터리를 닫습니다.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>예제

완성 된 코드는 다음과 같이 표시 되어야 toocreate 클라이언트 응용 프로그램, 어떻게 toocall hello hello 서비스의 작업 및 hello 작업 후 tooclose 클라이언트 hello 어떻게 호출 방법을 표시 끝났습니다.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Hello 응용 프로그램 실행

1. 키를 눌러 **Ctrl + Shift + B** toobuild hello 솔루션입니다. Hello 클라이언트 프로젝트와 hello 이전 단계에서 만든 hello 서비스 프로젝트를 모두 빌드합니다.
2. 실행 중인 hello 클라이언트 응용 프로그램 하기 전에 hello 서비스 응용 프로그램이 실행 되 고 있는지 확인 해야 합니다. Visual Studio에서 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **EchoService** 솔루션을 클릭 한 다음 **속성**합니다.
3. Hello 솔루션 속성 대화 상자에서 클릭 **시작 프로젝트**, 클릭 hello **여러 개의 시작 프로젝트** 단추입니다. 확인 **EchoService** hello 목록에 맨 먼저 나타납니다.
4. 집합 hello **동작** 두 hello에 대 한 상자 **EchoService** 및 **EchoClient** 너무 프로젝트**시작**합니다.

    ![][5]
5. **프로젝트 종속성**을 클릭합니다. Hello에 **프로젝트** 상자 **EchoClient**합니다. Hello에 **에 따라 달라 집니다** 상자의 **EchoService** 을 선택 합니다.

    ![][6]
6. 클릭 **확인** toodismiss hello **속성** 대화 상자.
7. 키를 눌러 **F5** toorun 두 프로젝트입니다.
8. 두 콘솔 창에서 열고 hello 네임 스페이스 이름에 대 한 메시지를 표시 합니다. hello 서비스를 실행 해야 먼저에서 계산 hello **EchoService** 콘솔 창 hello 네임 스페이스를 입력 한 다음 키를 누릅니다 **Enter**합니다.
9. 다음으로, SAS 키를 입력하라는 메시지가 표시됩니다. Hello SAS 키를 입력 하 고 ENTER 키를 누릅니다.

    다음은 hello 콘솔 창에서 예제 출력이입니다. Note는 hello 값 여기에 제공 된 예를 들어 목적 으로만 사용 합니다.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    hello 서비스 응용 프로그램 hello 다음 예제와 같이 toohello 콘솔 창 hello 주소를 수신 대기 중인를 인쇄 합니다.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. Hello에 **EchoClient** 콘솔 창, 입력 hello hello 서비스 응용 프로그램에 대해 이전에 입력 한 동일한 정보입니다. 이전 단계 tooenter hello hello 다음과 같은 서비스 네임 스페이스 및 SAS 키 hello 클라이언트 응용 프로그램에 대 한 값입니다.
11. 이러한 값을 입력 한 후 hello 클라이언트 채널 toohello 서비스 열리고 hello 다음 콘솔 출력 예제와 같이 일부 텍스트 tooenter 하 라는 메시지가 표시 됩니다.

    `Enter text tooecho (or [Enter] tooexit):`

    일부 텍스트 toosend toohello 서비스 응용 프로그램을 입력 하 고 Enter 키를 누릅니다. 이 텍스트 toohello 서비스 hello Echo 서비스 작업을 통해 전송 되 고 다음 예제 출력 hello 같이 hello 서비스 콘솔 창에 나타납니다.

    `Echoing: My sample text`

    hello 클라이언트 응용 프로그램의 hello hello 반환 값을 받는 `Echo` hello 원래 텍스트 이며 출력 작업 tooits 콘솔 창입니다. hello 다음은 hello 클라이언트 콘솔 창 출력 예입니다.

    `Server echoed: My sample text`
12. 이런이 방식으로 hello client toohello 서비스에서 텍스트 메시지를 보내는 작업을 계속할 수 있습니다. 완료 되 면 enter hello 클라이언트 및 서비스 콘솔 windows tooend에서 응용 프로그램을 모두 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서는 toobuild Azure 릴레이 클라이언트 응용 프로그램 및 서비스를 사용 하 여 서비스 버스의 WCF 릴레이 기능을 hello 방법을 배웠습니다. [Service Bus 메시징](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)을 사용하는 유사한 자습서는 [Service Bus 큐 시작](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)을 참조하세요.

Azure 릴레이 대 한 자세한 toolearn hello 다음 항목을 참조 하십시오.

* [Azure Service Bus 아키텍처 개요](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Azure Relay 개요](relay-what-is-it.md)
* [Toouse hello WCF.net 서비스를 릴레이 하는 방법](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
