---
title: "클라우드 서비스의 역할에 대 한 aaaCommunication | Microsoft Docs"
description: "클라우드 서비스의 역할 인스턴스 끝점 (예: http, https, tcp, udp)에 대해 정의 된 또는 다른 역할 인스턴스 간의 외부 hello와 통신 하는 있을 수 있습니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a>Azure에서 역할 인스턴스에 통신 사용
클라우드 서비스 역할은 내부 및 외부 연결을 통해 통신합니다. 외부 연결을 **입력 끝점**이라고 하고, 내부 연결을 **내부 끝점**이라고 합니다. 이 항목에서는 설명 방법을 toomodify hello [서비스 정의](cloud-services-model-and-package.md#csdef) toocreate 끝점입니다.

## <a name="input-endpoint"></a>입력 끝점
hello 입력된 끝점이 tooexpose 외부 포트 toohello를 원하는 때에 사용 됩니다. Hello 프로토콜 유형 및 hello 끝점에 대 한 두 hello 외부 및 내부 포트에 대 한 적용 하는 hello 끝점의 hello 포트를 지정 합니다. 원하는 경우 hello로 hello 끝점에 대 한 다른 내부 포트를 지정할 수 있습니다 [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) 특성입니다.

hello 입력된 끝점 프로토콜을 따르는 hello צ ְ ײ: **http, https, tcp, udp**합니다.

입력된 끝점 toocreate 추가 hello **InputEndpoint** 자식 요소 toohello **끝점** 웹 또는 작업자 역할의 요소입니다.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>인스턴스 입력 끝점
인스턴스 입력된 끝점은 유사한 tooinput 끝점 하지만 있습니다 hello 부하 분산 장치에 포트 전달을 사용 하 여 각 개별 역할 인스턴스에 대 한 특정 공용 포트를 매핑합니다. 단일 공용 포트 또는 포트의 범위를 지정할 수 있습니다.

hello 인스턴스 입력된 끝점에만 사용할 수 **tcp** 또는 **udp** hello 프로토콜로 합니다.

인스턴스 입력된 끝점 toocreate 추가 hello **InstanceInputEndpoint** 자식 요소 toohello **끝점** 웹 또는 작업자 역할의 요소입니다.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>내부 끝점
내부 끝점은 인스턴스 간 통신에 사용할 수 있습니다. hello 포트는 선택 사항이 며 생략 하면 동적 포트 할당은 toohello 끝점 합니다. 포트 범위를 사용할 수 있습니다. 역할 당 다섯 개의 내부 끝점으로 제한합니다.

hello 내부 끝점 프로토콜을 따르는 hello צ ְ ײ: **http, tcp, udp, 모든**합니다.

내부 입력된 끝점 toocreate 추가 hello **InternalEndpoint** 자식 요소 toohello **끝점** 웹 또는 작업자 역할의 요소입니다.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

또한 포트 범위를 사용할 수 있습니다.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>작업자 역할 대 웹 역할
작업자 및 웹 역할 모두를 사용하여 작업하는 경우 끝점과 한 가지 작은 차이가 있습니다. hello 웹 역할에 있어야 최소한 hello를 사용 하 여 단일 입력된 끝점 **HTTP** 프로토콜입니다.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>Hello.NET SDK tooaccess 끝점을 사용 하 여
hello Azure Managed Library는 역할 인스턴스 toocommunicate 런타임 시에 대 한 메서드를 제공합니다. 역할 인스턴스 내에서 실행 되는 코드를 hello 현재 역할 인스턴스에 대 한 정보 뿐만 아니라 다른 역할 인스턴스 및 해당 끝점의 hello 존재 하는 방법에 대 한 정보를 검색할 수 있습니다.

> [!NOTE]
> 클라우드 서비스에서 실행되고 적어도 하나 이상의 내부 끝점을 정의하는 역할 인스턴스에 대한 정보만을 검색할 수 있습니다. 다른 서비스에서 실행 중인 역할 인스턴스에 대한 데이터를 가져올 수 없습니다.
> 
> 

Hello를 사용할 수 있습니다 [인스턴스](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) 속성 tooretrieve 인스턴스의 역할입니다. 먼저 hello를 사용 하 여 [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn 참조 toohello 현재 역할 인스턴스를 선택한 다음 hello를 사용 하 여 [역할](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) 속성 tooreturn 참조 toohello 역할 자체입니다.

Hello.NET SDK를 통해 프로그래밍 방식으로 tooa 역할 인스턴스를 연결할 때는 상대적으로 쉬운 tooaccess hello 끝점 정보입니다. 예를 들어 tooa 특정 역할 환경이 이미 연결한 후이 코드로 특정 끝점의 hello 포트를 가져올 수 있습니다.

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

hello **인스턴스** 속성의 컬렉션을 반환 **RoleInstance** 개체입니다. 이 컬렉션은 항상 hello 현재 인스턴스를 포함합니다. Hello 역할이 내부 끝점을 정의 하지 않으면, hello 순서가 hello 현재 인스턴스의 있지만 다른 인스턴스를 포함 합니다. hello hello 컬렉션에 있는 역할 인스턴스 수에는 항상 1 hello 역할에 대해 내부 끝점이 정의 되어 있는 경우 모두 hello 됩니다. Hello 역할이 내부 끝점 정의 인스턴스는 런타임에 검색 가능 하 고 hello 컬렉션에 있는 인스턴스의 hello 수 hello 역할 hello 서비스 구성 파일에 지정한 인스턴스 toohello 수에 해당 됩니다.

> [!NOTE]
> hello Azure Managed Library는 다른 역할 인스턴스의 hello 상태를 결정 하는 수단을 제공 하지 않지만 직접 구현할 수 있습니다 이러한 상태 평가 하는 경우이 기능을 필요로 하는 서비스입니다. 사용할 수 있습니다 [Azure 진단](cloud-services-dotnet-diagnostics.md) 역할 인스턴스를 실행 하는 방법에 대 한 tooobtain 정보입니다.
> 
> 

내부 끝점의 역할 인스턴스에서 toodetermine hello 포트 번호를 hello를 사용할 수 있습니다 [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) 속성 tooreturn 끝점 이름과 해당 IP를 포함 하는 사전 개체 주소 및 포트. hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) hello IP 주소와 포트 지정 된 끝점에 대 한 속성을 반환 합니다. hello **PublicIPEndpoint** 속성은 부하 분산 된 끝점에 대 한 hello 포트를 반환 합니다. hello의 hello IP 주소 부분은 **PublicIPEndpoint** 속성이 사용 되지 않습니다.

역할 인스턴스를 반복하는 예는 다음과 같습니다.

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

Hello 서비스 정의 통해 노출 하는 hello 끝점을 가져오고 연결에 대 한 수신을 시작 하는 작업자 역할의 예를 들면 다음과 같습니다.

> [!WARNING]
> 이 코드는 배포된 서비스에서만 작동합니다. Hello Azure 계산 에뮬레이터를 실행 하는 경우에 직접 포트 끝점을 만들 하는 구성 요소 서비스 (**InstanceInputEndpoint** 요소)은 무시 됩니다.
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a>네트워크 트래픽 규칙 toocontrol 역할 통신
내부 끝점을 정의한 후에 네트워크 트래픽 규칙 (만든 hello 끝점에 기반) toocontrol 역할 인스턴스 통신할 수 있는 방법을 서로 추가할 수 있습니다. hello 다음 그림에 역할 통신을 제어 하기 위한 몇 가지 일반적인 시나리오:

![네트워크 트래픽 규칙 시나리오](./media/cloud-services-enable-communication-role-instances/scenarios.png "네트워크 트래픽 규칙 시나리오")

hello 다음 코드 예제에서는 hello 이전 다이어그램에 표시 된 hello 역할에 대 한 역할 정의 합니다. 각 역할 정의는 정의된 내부 끝점을 적어도 하나 이상 포함합니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> 고정되고 자동으로 할당된 포트의 내부 끝점으로 역할 간의 통신 제한이 발생할 수 있습니다.
> 
> 

기본적으로 내부 끝점이 정의 되 면 아무런 제한 없이 역할의 모든 역할 toohello 내부 끝점에서 통신이 흐를 수 있습니다. 추가 해야 toorestrict 통신은 **NetworkTrafficRules** 요소 toohello **ServiceDefinition** hello 서비스 정의 파일의 요소입니다.

### <a name="scenario-1"></a>시나리오 1
네트워크 트래픽을 허용 **WebRole1** 너무**WorkerRole1**합니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a>시나리오 2
네트워크 트래픽만 허용 **WebRole1** 너무**WorkerRole1** 및 **WorkerRole2**합니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a>시나리오 3
네트워크 트래픽만 허용 **WebRole1** 너무**WorkerRole1**, 및 **WorkerRole1** 너무**WorkerRole2**합니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a>시나리오 4
네트워크 트래픽만 허용 **WebRole1** 너무**WorkerRole1**, **WebRole1** 너무**WorkerRole2**, 및  **WorkerRole1** 너무**WorkerRole2**합니다.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

위에서 사용한 hello 요소에 대 한 XML 스키마 참조를 찾을 수 [여기](https://msdn.microsoft.com/library/azure/gg557551.aspx)합니다.

## <a name="next-steps"></a>다음 단계
에 대해 자세히 알아보십시오 hello 클라우드 서비스 [모델](cloud-services-model-and-package.md)합니다.

