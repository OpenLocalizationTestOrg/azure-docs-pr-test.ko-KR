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
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="cea56-103">Azure에서 역할 인스턴스에 통신 사용</span><span class="sxs-lookup"><span data-stu-id="cea56-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="cea56-104">클라우드 서비스 역할은 내부 및 외부 연결을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="cea56-105">외부 연결을 **입력 끝점**이라고 하고, 내부 연결을 **내부 끝점**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="cea56-106">이 항목에서는 설명 방법을 toomodify hello [서비스 정의](cloud-services-model-and-package.md#csdef) toocreate 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="cea56-107">입력 끝점</span><span class="sxs-lookup"><span data-stu-id="cea56-107">Input endpoint</span></span>
<span data-ttu-id="cea56-108">hello 입력된 끝점이 tooexpose 외부 포트 toohello를 원하는 때에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="cea56-109">Hello 프로토콜 유형 및 hello 끝점에 대 한 두 hello 외부 및 내부 포트에 대 한 적용 하는 hello 끝점의 hello 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="cea56-110">원하는 경우 hello로 hello 끝점에 대 한 다른 내부 포트를 지정할 수 있습니다 [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="cea56-111">hello 입력된 끝점 프로토콜을 따르는 hello צ ְ ײ: **http, https, tcp, udp**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="cea56-112">입력된 끝점 toocreate 추가 hello **InputEndpoint** 자식 요소 toohello **끝점** 웹 또는 작업자 역할의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="cea56-113">인스턴스 입력 끝점</span><span class="sxs-lookup"><span data-stu-id="cea56-113">Instance input endpoint</span></span>
<span data-ttu-id="cea56-114">인스턴스 입력된 끝점은 유사한 tooinput 끝점 하지만 있습니다 hello 부하 분산 장치에 포트 전달을 사용 하 여 각 개별 역할 인스턴스에 대 한 특정 공용 포트를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="cea56-115">단일 공용 포트 또는 포트의 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="cea56-116">hello 인스턴스 입력된 끝점에만 사용할 수 **tcp** 또는 **udp** hello 프로토콜로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="cea56-117">인스턴스 입력된 끝점 toocreate 추가 hello **InstanceInputEndpoint** 자식 요소 toohello **끝점** 웹 또는 작업자 역할의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="cea56-118">내부 끝점</span><span class="sxs-lookup"><span data-stu-id="cea56-118">Internal endpoint</span></span>
<span data-ttu-id="cea56-119">내부 끝점은 인스턴스 간 통신에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="cea56-120">hello 포트는 선택 사항이 며 생략 하면 동적 포트 할당은 toohello 끝점 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="cea56-121">포트 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-121">A port range can be used.</span></span> <span data-ttu-id="cea56-122">역할 당 다섯 개의 내부 끝점으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="cea56-123">hello 내부 끝점 프로토콜을 따르는 hello צ ְ ײ: **http, tcp, udp, 모든**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="cea56-124">내부 입력된 끝점 toocreate 추가 hello **InternalEndpoint** 자식 요소 toohello **끝점** 웹 또는 작업자 역할의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="cea56-125">또한 포트 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="cea56-126">작업자 역할 대 웹 역할</span><span class="sxs-lookup"><span data-stu-id="cea56-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="cea56-127">작업자 및 웹 역할 모두를 사용하여 작업하는 경우 끝점과 한 가지 작은 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="cea56-128">hello 웹 역할에 있어야 최소한 hello를 사용 하 여 단일 입력된 끝점 **HTTP** 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="cea56-129">Hello.NET SDK tooaccess 끝점을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="cea56-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="cea56-130">hello Azure Managed Library는 역할 인스턴스 toocommunicate 런타임 시에 대 한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="cea56-131">역할 인스턴스 내에서 실행 되는 코드를 hello 현재 역할 인스턴스에 대 한 정보 뿐만 아니라 다른 역할 인스턴스 및 해당 끝점의 hello 존재 하는 방법에 대 한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="cea56-132">클라우드 서비스에서 실행되고 적어도 하나 이상의 내부 끝점을 정의하는 역할 인스턴스에 대한 정보만을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="cea56-133">다른 서비스에서 실행 중인 역할 인스턴스에 대한 데이터를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="cea56-134">Hello를 사용할 수 있습니다 [인스턴스](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) 속성 tooretrieve 인스턴스의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="cea56-135">먼저 hello를 사용 하 여 [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn 참조 toohello 현재 역할 인스턴스를 선택한 다음 hello를 사용 하 여 [역할](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) 속성 tooreturn 참조 toohello 역할 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="cea56-136">Hello.NET SDK를 통해 프로그래밍 방식으로 tooa 역할 인스턴스를 연결할 때는 상대적으로 쉬운 tooaccess hello 끝점 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="cea56-137">예를 들어 tooa 특정 역할 환경이 이미 연결한 후이 코드로 특정 끝점의 hello 포트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="cea56-138">hello **인스턴스** 속성의 컬렉션을 반환 **RoleInstance** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="cea56-139">이 컬렉션은 항상 hello 현재 인스턴스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="cea56-140">Hello 역할이 내부 끝점을 정의 하지 않으면, hello 순서가 hello 현재 인스턴스의 있지만 다른 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="cea56-141">hello hello 컬렉션에 있는 역할 인스턴스 수에는 항상 1 hello 역할에 대해 내부 끝점이 정의 되어 있는 경우 모두 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="cea56-142">Hello 역할이 내부 끝점 정의 인스턴스는 런타임에 검색 가능 하 고 hello 컬렉션에 있는 인스턴스의 hello 수 hello 역할 hello 서비스 구성 파일에 지정한 인스턴스 toohello 수에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="cea56-143">hello Azure Managed Library는 다른 역할 인스턴스의 hello 상태를 결정 하는 수단을 제공 하지 않지만 직접 구현할 수 있습니다 이러한 상태 평가 하는 경우이 기능을 필요로 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="cea56-144">사용할 수 있습니다 [Azure 진단](cloud-services-dotnet-diagnostics.md) 역할 인스턴스를 실행 하는 방법에 대 한 tooobtain 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="cea56-145">내부 끝점의 역할 인스턴스에서 toodetermine hello 포트 번호를 hello를 사용할 수 있습니다 [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) 속성 tooreturn 끝점 이름과 해당 IP를 포함 하는 사전 개체 주소 및 포트.</span><span class="sxs-lookup"><span data-stu-id="cea56-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="cea56-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) hello IP 주소와 포트 지정 된 끝점에 대 한 속성을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="cea56-147">hello **PublicIPEndpoint** 속성은 부하 분산 된 끝점에 대 한 hello 포트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="cea56-148">hello의 hello IP 주소 부분은 **PublicIPEndpoint** 속성이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="cea56-149">역할 인스턴스를 반복하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="cea56-150">Hello 서비스 정의 통해 노출 하는 hello 끝점을 가져오고 연결에 대 한 수신을 시작 하는 작업자 역할의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="cea56-151">이 코드는 배포된 서비스에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="cea56-152">Hello Azure 계산 에뮬레이터를 실행 하는 경우에 직접 포트 끝점을 만들 하는 구성 요소 서비스 (**InstanceInputEndpoint** 요소)은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="cea56-153">네트워크 트래픽 규칙 toocontrol 역할 통신</span><span class="sxs-lookup"><span data-stu-id="cea56-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="cea56-154">내부 끝점을 정의한 후에 네트워크 트래픽 규칙 (만든 hello 끝점에 기반) toocontrol 역할 인스턴스 통신할 수 있는 방법을 서로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="cea56-155">hello 다음 그림에 역할 통신을 제어 하기 위한 몇 가지 일반적인 시나리오:</span><span class="sxs-lookup"><span data-stu-id="cea56-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="cea56-156">![네트워크 트래픽 규칙 시나리오](./media/cloud-services-enable-communication-role-instances/scenarios.png "네트워크 트래픽 규칙 시나리오")</span><span class="sxs-lookup"><span data-stu-id="cea56-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="cea56-157">hello 다음 코드 예제에서는 hello 이전 다이어그램에 표시 된 hello 역할에 대 한 역할 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="cea56-158">각 역할 정의는 정의된 내부 끝점을 적어도 하나 이상 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="cea56-159">고정되고 자동으로 할당된 포트의 내부 끝점으로 역할 간의 통신 제한이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="cea56-160">기본적으로 내부 끝점이 정의 되 면 아무런 제한 없이 역할의 모든 역할 toohello 내부 끝점에서 통신이 흐를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="cea56-161">추가 해야 toorestrict 통신은 **NetworkTrafficRules** 요소 toohello **ServiceDefinition** hello 서비스 정의 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="cea56-162">시나리오 1</span><span class="sxs-lookup"><span data-stu-id="cea56-162">Scenario 1</span></span>
<span data-ttu-id="cea56-163">네트워크 트래픽을 허용 **WebRole1** 너무**WorkerRole1**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="cea56-164">시나리오 2</span><span class="sxs-lookup"><span data-stu-id="cea56-164">Scenario 2</span></span>
<span data-ttu-id="cea56-165">네트워크 트래픽만 허용 **WebRole1** 너무**WorkerRole1** 및 **WorkerRole2**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="cea56-166">시나리오 3</span><span class="sxs-lookup"><span data-stu-id="cea56-166">Scenario 3</span></span>
<span data-ttu-id="cea56-167">네트워크 트래픽만 허용 **WebRole1** 너무**WorkerRole1**, 및 **WorkerRole1** 너무**WorkerRole2**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="cea56-168">시나리오 4</span><span class="sxs-lookup"><span data-stu-id="cea56-168">Scenario 4</span></span>
<span data-ttu-id="cea56-169">네트워크 트래픽만 허용 **WebRole1** 너무**WorkerRole1**, **WebRole1** 너무**WorkerRole2**, 및  **WorkerRole1** 너무**WorkerRole2**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

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

<span data-ttu-id="cea56-170">위에서 사용한 hello 요소에 대 한 XML 스키마 참조를 찾을 수 [여기](https://msdn.microsoft.com/library/azure/gg557551.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cea56-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cea56-171">Next steps</span></span>
<span data-ttu-id="cea56-172">에 대해 자세히 알아보십시오 hello 클라우드 서비스 [모델](cloud-services-model-and-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea56-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

