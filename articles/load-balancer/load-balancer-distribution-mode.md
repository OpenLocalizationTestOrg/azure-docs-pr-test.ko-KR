---
title: "부하 분산 장치 배포 모드 구성 | Microsoft Docs"
description: "원본 IP 선호도를 지원하도록 Azure 부하 분산 장치 배포 모드를 구성하는 방법입니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="a0dc4-103">부하 분산 장치의 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="a0dc4-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="a0dc4-104">해시 기반 배포 모드</span><span class="sxs-lookup"><span data-stu-id="a0dc4-104">Hash-based distribution mode</span></span>

<span data-ttu-id="a0dc4-105">기본 배포 알고리즘은 트래픽을 사용 가능한 서버에 매핑하는 5개 튜플(원본 IP, 원본 포트, 대상 IP, 대상 포트, 프로토콜 종류) 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="a0dc4-106">전송 세션 내에서만 연결이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="a0dc4-107">동일한 세션의 패킷은 부하 분산 끝점 뒤의 동일한 DIP(데이터 센터 IP) 인스턴스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="a0dc4-108">클라이언트가 동일한 원본 IP에서 새 세션을 시작하는 경우 원본 포트가 변경되어 트래픽이 다른 DIP 끝점으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![해시 기반 부하 분산 장치](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="a0dc4-110">그림 1 - 5개 튜플 배포</span><span class="sxs-lookup"><span data-stu-id="a0dc4-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="a0dc4-111">소스 IP 선호도 모드</span><span class="sxs-lookup"><span data-stu-id="a0dc4-111">Source IP affinity mode</span></span>

<span data-ttu-id="a0dc4-112">원본 IP 선호도(세션 선호도 또는 클라이언트 IP 선호도라고도 함)라는 다른 배포 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="a0dc4-113">2개 튜플(원본 IP, 대상 IP) 또는 3개 튜플(원본 IP, 대상 IP, 프로토콜)을 사용하도록 Azure Load Balancer를 구성하여 사용 가능한 서버에 트래픽을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="a0dc4-114">원본 IP 선호도를 사용하면 동일한 클라이언트 컴퓨터에서 시작된 연결이 동일한 DIP 끝점으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="a0dc4-115">아래 다이어그램은 2개 튜플 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="a0dc4-116">2개 튜플이 부하 분산 장치를 실행하여 가상 컴퓨터 1(VM1)에 도달한 후 VM2 및 VM3으로 백업되는 방식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![세션 선호도](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="a0dc4-118">그림 2 - 2개 튜플 배포</span><span class="sxs-lookup"><span data-stu-id="a0dc4-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="a0dc4-119">원본 IP 선호도는 Azure Load Balancer와 원격 데스크톱(RD) 게이트웨이 간의 비호환성을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="a0dc4-120">이제 단일 클라우드 서비스에서 RD 게이트웨이 팜을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="a0dc4-121">또 다른 사용 시나리오로는 데이터 업로드는 UDP를 통해 수행되지만 제어 영역은 TCP를 통해 구현되는 미디어 업로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="a0dc4-122">클라이언트는 먼저 부하 분산 공용 주소에 대한 TCP 세션을 시작하고 특정 DIP로 전송됩니다. 이 채널은 연결 상태를 모니터링하기 위해 활성 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="a0dc4-123">동일한 클라이언트 컴퓨터에서 동일한 부하 분산 공용 끝점으로 새 UDP 세션이 시작됩니다. 여기서 예상은 TCP를 통해 제어 채널을 유지하는 동시에 높은 처리량으로 미디어 업로드를 실행할 수 있도록 이 연결도 이전 TCP 연결과 동일한 DIP 끝점으로 전송되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="a0dc4-124">부하 분산 집합이 변경되면(가상 컴퓨터 추가 또는 제거) 클라이언트 요청 배포가 다시 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="a0dc4-125">기존 클라이언트의 새 연결이 동일한 서버로 수행된다고 확신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="a0dc4-126">또한 원본 IP 선호도를 사용하는 경우 트래픽이 불규칙하게 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="a0dc4-127">프록시 뒤에서 실행되는 클라이언트는 하나의 고유한 클라이언트 응용 프로그램으로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="a0dc4-128">부하 분산 장치에 대한 원본 IP 선호도 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a0dc4-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="a0dc4-129">가상 컴퓨터의 경우 PowerShell을 사용하여 시간 제한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="a0dc4-130">가상 컴퓨터에 Azure 끝점을 추가하고 부하 분산 장치 배포 모드 설정</span><span class="sxs-lookup"><span data-stu-id="a0dc4-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="a0dc4-131">LoadBalancerDistribution은 2개 튜플(원본 IP, 대상 IP) 부하 분산의 경우 sourceIP로, 3개 튜플(원본 IP, 대상 IP, 프로토콜) 부하 분산의 경우 sourceIPProtocol로 설정할 수 있으며 5개 튜플 부하 분산의 기본 동작을 원하는 경우 none으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="a0dc4-132">다음을 사용하여 끝점 부하 분산 장치 배포 모드 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15
    LoadBalancerDistribution : sourceIP

<span data-ttu-id="a0dc4-133">LoadBalancerDistribution 요소가 없으면 Azure 부하 분산 장치는 기본값인 5개 튜플 알고리즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="a0dc4-134">부하 분산된 끝점 집합에 대한 배포 모드 설정</span><span class="sxs-lookup"><span data-stu-id="a0dc4-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="a0dc4-135">부하 분산 끝점 집합에 끝점이 포함되어 있으면 부하 분산 끝점 집합에 대해 배포 모드를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="a0dc4-136">배포 모드를 변경하는 클라우드 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="a0dc4-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="a0dc4-137">Azure SDK for .NET 2.5(11월 출시)를 사용하여 클라우드 서비스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="a0dc4-138">.csdef에서 클라우드 서비스용 끝점 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="a0dc4-139">클라우드 서비스 배포의 부하 분산 장치 배포 모드를 업데이트하려면 배포를 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="a0dc4-140">아래에 .csdef에서 끝점 설정을 변경하는 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-140">Here is an example of .csdef changes for endpoint settings:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
<InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
    <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
</InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="api-example"></a><span data-ttu-id="a0dc4-141">API 예제</span><span class="sxs-lookup"><span data-stu-id="a0dc4-141">API example</span></span>

<span data-ttu-id="a0dc4-142">service management API를 사용하여 부하 분산 장치 배포를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="a0dc4-143">추가하는 `x-ms-version` 헤더는 버전 `2014-09-01` 이상으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc4-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="a0dc4-144">배포에서 지정한 부하 분산된 집합의 구성 업데이트</span><span class="sxs-lookup"><span data-stu-id="a0dc4-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="a0dc4-145">요청 예제</span><span class="sxs-lookup"><span data-stu-id="a0dc4-145">Request example</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

<span data-ttu-id="a0dc4-146">LoadBalancerDistribution의 값은 2개 튜플 선호도의 경우 sourceIP로, 3개 튜플 선호도의 경우에는 sourceIPProtocol로 설정할 수 있으며 선호도가 없는 경우에는 none으로 설정할 수 있습니다(기본값인</span><span class="sxs-lookup"><span data-stu-id="a0dc4-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="a0dc4-147">5개 튜플이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="a0dc4-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="a0dc4-148">응답</span><span class="sxs-lookup"><span data-stu-id="a0dc4-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="a0dc4-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0dc4-149">Next Steps</span></span>

[<span data-ttu-id="a0dc4-150">내부 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="a0dc4-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="a0dc4-151">인터넷 연결 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="a0dc4-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="a0dc4-152">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a0dc4-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
