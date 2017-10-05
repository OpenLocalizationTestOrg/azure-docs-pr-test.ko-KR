---
title: "클라우드 서비스 역할에 대한 통신 | Microsoft Docs"
description: "클라우드 서비스의 역할 인스턴스에는 다른 역할 인스턴스의 외부 또는 그 사이에서 통신하도록 정의된 끝점(http, https, tcp, udp)이 있을 수 있습니다."
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
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="634c4-103">Azure에서 역할 인스턴스에 통신 사용</span><span class="sxs-lookup"><span data-stu-id="634c4-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="634c4-104">클라우드 서비스 역할은 내부 및 외부 연결을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="634c4-105">외부 연결을 **입력 끝점**이라고 하고, 내부 연결을 **내부 끝점**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="634c4-106">이 항목은 [서비스 정의](cloud-services-model-and-package.md#csdef) 를 수정하는 방법을 설명하여 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="634c4-107">입력 끝점</span><span class="sxs-lookup"><span data-stu-id="634c4-107">Input endpoint</span></span>
<span data-ttu-id="634c4-108">입력 끝점이 외부에 포트를 표시하려는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="634c4-109">끝점에 대한 외부 및 내부 포트에 적용되는 끝점의 프로토콜 종류 및 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="634c4-110">원할 경우 [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) 특성을 사용하여 끝점에 다른 내부 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="634c4-111">입력 끝점은 **http, https, tcp, udp**와 같은 프로토콜을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="634c4-112">입력 끝점을 만들려면 **InputEndpoint** 자식 요소를 웹 또는 작업자 역할의 **끝점** 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="634c4-113">인스턴스 입력 끝점</span><span class="sxs-lookup"><span data-stu-id="634c4-113">Instance input endpoint</span></span>
<span data-ttu-id="634c4-114">인스턴스 입력 끝점은 입력 끝점과 유사하지만 사용하면 부하 분산 장치에서 포트 전달을 사용하여 각 개별 역할 인스턴스에 대한 특정 공용 포트를 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="634c4-115">단일 공용 포트 또는 포트의 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="634c4-116">인스턴스 입력 끝점은 프로토콜로 **tcp** 또는 **udp**만을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="634c4-117">인스턴스 입력 끝점을 만들려면 **InstanceInputEndpoint** 자식 요소를 웹 또는 작업자 역할의 **끝점** 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="634c4-118">내부 끝점</span><span class="sxs-lookup"><span data-stu-id="634c4-118">Internal endpoint</span></span>
<span data-ttu-id="634c4-119">내부 끝점은 인스턴스 간 통신에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="634c4-120">포트는 선택적이며 생략하면 끝점에 동적 포트가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="634c4-121">포트 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-121">A port range can be used.</span></span> <span data-ttu-id="634c4-122">역할 당 다섯 개의 내부 끝점으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="634c4-123">내부 끝점은 **http, tcp, udp, any**와 같은 프로토콜을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="634c4-124">내부 입력 끝점을 만들려면 **InternalEndpoint** 자식 요소를 웹 또는 작업자 역할의 **끝점** 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="634c4-125">또한 포트 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="634c4-126">작업자 역할 대 웹 역할</span><span class="sxs-lookup"><span data-stu-id="634c4-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="634c4-127">작업자 및 웹 역할 모두를 사용하여 작업하는 경우 끝점과 한 가지 작은 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="634c4-128">웹 역할에는 최소한 **HTTP** 프로토콜을 사용하는 단일 입력 끝점이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="634c4-129">.NET SDK를 사용하여 끝점에 액세스하려면</span><span class="sxs-lookup"><span data-stu-id="634c4-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="634c4-130">Azure Managed Library는 역할 인스턴스에 대한 메서드를 제공하여 런타임 시 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="634c4-131">역할 인스턴스 내에서 실행되는 코드에서 다른 역할 인스턴스 및 해당 끝점의 존재에 대한 정보 뿐만 아니라 현재 역할 인스턴스에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="634c4-132">클라우드 서비스에서 실행되고 적어도 하나 이상의 내부 끝점을 정의하는 역할 인스턴스에 대한 정보만을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="634c4-133">다른 서비스에서 실행 중인 역할 인스턴스에 대한 데이터를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="634c4-134">[인스턴스](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) 속성을 사용하여 역할의 인스턴스를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="634c4-135">먼저 [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx)를 사용하여 현재 역할 인스턴스에 참조를 반환한 다음 [역할](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) 속성을 사용하여 역할 자체에 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="634c4-136">.NET SDK를 통해 프로그래밍 방식으로 역할 인스턴스에 연결하면 비교적 쉽게 끝점 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="634c4-137">예를 들어 특정 역할 환경에 이미 연결한 후에 이 코드를 사용하여 특정 끝점의 포트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="634c4-138">**인스턴스** 속성은 **RoleInstance** 개체의 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="634c4-139">이 컬렉션은 항상 현재 인스턴스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-139">This collection always contains the current instance.</span></span> <span data-ttu-id="634c4-140">역할이 내부 끝점을 정의하지 않으면 컬렉션에 현재 인스턴스를 포함하지만 다른 인스턴스는 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="634c4-141">내부 끝점이 역할에 대해 정의되지 않는 경우 컬렉션에 있는 역할 인스턴스 수는 항상 1입니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="634c4-142">역할이 내부 끝점을 정의하는 경우 해당 인스턴스는 런타임 시 검색 가능하고 컬렉션의 인스턴스 수는 서비스 구성 파일의 역할에 지정된 인스턴스 수에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="634c4-143">Azure Managed Library는 다른 역할 인스턴스의 상태를 결정하는 수단을 제공하지는 않지만 서비스가 이 기능을 필요로 하는 경우 그러한 상태 평가를 직접 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="634c4-144">[Azure 진단](cloud-services-dotnet-diagnostics.md) 을 사용하여 역할 인스턴스를 실행하는 방법에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="634c4-145">역할 인스턴스의 내부 끝점에서 포트 번호를 확인하려면 [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) 속성을 사용하여 끝점 이름과 해당 IP 주소 및 포트를 포함하는 Dictionary 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="634c4-146">[IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) 속성은 끝점을 지정한 IP 주소 및 포트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="634c4-147">**PublicIPEndpoint** 속성은 끝점을 분산한 부하에 포트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="634c4-148">**PublicIPEndpoint** 속성의 IP 주소 부분을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="634c4-149">역할 인스턴스를 반복하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="634c4-150">서비스 정의를 통해 노출된 끝점을 가져오고 연결을 수신하기 시작하는 작업자 역할의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="634c4-151">이 코드는 배포된 서비스에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="634c4-152">Azure 계산 에뮬레이터에서 실행되는 경우 직접 포트 끝점(**InstanceInputEndpoint** 요소)을 만드는 구성 요소 서비스를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
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
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="634c4-153">역할 통신을 제어하는 네트워크 트래픽 규칙</span><span class="sxs-lookup"><span data-stu-id="634c4-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="634c4-154">내부 끝점을 정의한 후에 역할 인스턴스가 서로 통신할 수 있는 방법을 제어하는 네트워크 트래픽 규칙(만든 끝점에 기반)을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="634c4-155">다음 다이어그램은 역할 통신을 제어하기 위한 몇 가지 일반적인 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="634c4-156">![네트워크 트래픽 규칙 시나리오](./media/cloud-services-enable-communication-role-instances/scenarios.png "네트워크 트래픽 규칙 시나리오")</span><span class="sxs-lookup"><span data-stu-id="634c4-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="634c4-157">다음 코드 예제는 이전 다이어그램에 표시된 역할에 대한 역할 정의를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="634c4-158">각 역할 정의는 정의된 내부 끝점을 적어도 하나 이상 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="634c4-159">고정되고 자동으로 할당된 포트의 내부 끝점으로 역할 간의 통신 제한이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="634c4-160">기본적으로 내부 끝점이 정의된 후에 어떤 역할에서도 제한 없이 역할의 내부 끝점으로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="634c4-161">통신을 제한하려면 **NetworkTrafficRules** 요소를 서비스 정의 파일의 **ServiceDefinition** 요소에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="634c4-162">시나리오 1</span><span class="sxs-lookup"><span data-stu-id="634c4-162">Scenario 1</span></span>
<span data-ttu-id="634c4-163">네트워크 트래픽은 **WebRole1**에서 **WorkerRole1**으로만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="634c4-164">시나리오 2</span><span class="sxs-lookup"><span data-stu-id="634c4-164">Scenario 2</span></span>
<span data-ttu-id="634c4-165">네트워크 트래픽은 **WebRole1**에서 **WorkerRole1** 및 **WorkerRole2**으로만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="634c4-166">시나리오 3</span><span class="sxs-lookup"><span data-stu-id="634c4-166">Scenario 3</span></span>
<span data-ttu-id="634c4-167">네트워크 트래픽은 **WebRole1**에서 **WorkerRole1**, 그리고 **WorkerRole1**에서 **WorkerRole2**로만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="634c4-168">시나리오 4</span><span class="sxs-lookup"><span data-stu-id="634c4-168">Scenario 4</span></span>
<span data-ttu-id="634c4-169">네트워크 트래픽은 **WebRole1**에서 **WorkerRole1**, **WebRole1**에서 **WorkerRole2**, 그리고 **WorkerRole1**에서 **WorkerRole2**로만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

<span data-ttu-id="634c4-170">위의 사용 되는 요소에 대한 XML 스키마 참조를 [여기](https://msdn.microsoft.com/library/azure/gg557551.aspx)서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="634c4-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="634c4-171">Next steps</span></span>
<span data-ttu-id="634c4-172">클라우드 서비스 [모델](cloud-services-model-and-package.md)에 대해 더 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="634c4-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

